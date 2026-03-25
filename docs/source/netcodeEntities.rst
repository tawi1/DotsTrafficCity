.. _netcode:

NetCode For Entities
=====

* Install `NetCode for Entities` package.
* Unpack ``DotsCity/Packages/Upgrades/NetcodePrefabs`` package if you installed Netcode manually; otherwise, it was unpacked automatically.
* In the player settings set `Run In Background`.

	.. image:: /images/multiplayer/netcode1.png

* In the :ref:`Cull config <cullConfig>`, make sure `Multiplayer Calculate Distance` or `Multiplayer Camera View` type.
* Add a new gameobject to the subscene with the `NetcodeCullPointPrefab` component and assign the `NetcodeCullPoint` prefab to it. The sample scene contains this prefab by default.
* From the Unity toolbar, select ``Window > Multiplayer > Play Mode Tools``. Make sure that the `Play Mode Type` is set to ``Client & Server`` (if you are running a local simulation).
* Install `Multiplayer Play Mode <https://docs.unity3d.com/Packages/com.unity.multiplayer.playmode@2.0/manual/index.html>`_ package to simulate a few players locally **(optional)**. 
* Import & open `NetCode demo scene` for sample.

NetCode Sample
============================

The sample utilizes a custom initialization flow to automate the connection process between client and server.

* **GameBootstrap**: Inherits from ``ClientServerBootstrap``. It automatically configures the network settings, such as setting the ``AutoConnectPort`` to **7979**, ensuring that the client and server worlds are synchronized upon startup without manual intervention.

Connection Management (GoInGameSystem)
--------------------------------------

To start synchronized gameplay, the connection must be transitioned to the "In-Game" state.

* **GoInGameSystem**: This system monitors the established network connection. 
* Once a ``NetworkId`` is assigned to a connection entity, it adds the ``NetworkStreamInGame`` component.
* **Ghost Synchronization**: This transition is critical; without it, NetCode will not transmit ghost snapshots (player entities, vehicles, or traffic) between the server and clients.

Client Manager (PlayerClientSpawnListenerSystem)
------------------------------------------------

The **Client Manager** logic is encapsulated in the ``PlayerClientSpawnListenerSystem``. It is responsible for handling the local representation of the player once the server spawns the ghost.

* **Local Ownership**: It identifies the specific ``PlayerTag`` entity that belongs to the local user by filtering for the ``GhostOwnerIsLocal`` component.
* **Local Component Initialization**: 
    * Adds the ``PlayerTagLocal`` marker to distinguish the local player from other network ghosts.
    * Initializes local-only interaction data: ``EnterVehicleData`` and ``CanEnterVehicleTag``.
* **OnPlayerSpawn Event**: This system provides a C# event hook, which is the recommended place to attach a Camera Follow script or initialize the local Gameplay UI (HUD).

Player Spawning (Server-Side)
-----------------------------

Spawning is controlled by the **PlayerSpawnSystem** on the server.

* **RPC Driven**: The process starts when the server receives a ``PlayerReadyRpc`` from a client.
* **Spawn Points**: The system uses a ``SpawnIndexTracker`` and a buffer of ``SpawnPointElement`` to determine the player's starting position.
* **Ownership**: The server assigns a ``GhostOwner`` component to the spawned prefab, ensuring the client has authority for movement prediction.

Player Interaction System
-------------------------

The Client Manager coordinates how the player interacts with the environment, specifically vehicles:

* **Proximity Detection**: Using settings from ``VehicleDetectionConfig``, the client performs local raycasts or distance checks to find nearby interactable vehicles.
* **State Management**:
    * When a vehicle is in range, the ``CanEnterVehicleTag`` is enabled.
    * The entity of the target vehicle is stored in ``EnterVehicleData``.
    * This local state is used to show "Press [E] to Enter" UI prompts.

Vehicle Entry/Exit Flow
-----------------------

Interactions follow a **Request-Response** pattern to ensure server authority while maintaining client responsiveness:

1. **Local Action**: When the player presses the interaction key, the client sends an ``EnterVehicleRequest`` RPC to the server.
2. **Server Validation**: The server checks if the vehicle is available and if the player is in range.
3. **Ghost Ownership Transfer**: Upon successful entry, the server updates the ``GhostOwner`` of the vehicle to match the player's ``NetworkId``. This allows the player to have **predicted movement** while driving, eliminating input lag.
4. **Client Synchronization**: The ``PlayerCarClientListenerSystem`` detects the change in the ``PlayerInCar`` component and:
    * Updates local tags (``PlayerVehicleTag``).
    * Synchronizes visual states (hiding the player model or parenting it to the seat).

Visual & Physical Parenting
---------------------------

The **Client Manager** works with ``NetcodeInteractUtils`` to handle the transition between walking and driving:

* **Hierarchy**: The player entity is parented to the vehicle entity.
* **Smoothing**: The system disables ``PhysicsGraphicalSmoothing`` on the player while inside a car to prevent "ghosting" effects where the character model lags behind the fast-moving vehicle.
* **Collision Layers**: It temporarily moves the player to a "No Physics" world index to prevent the character's collider from interfering with the vehicle's physics body.

Manual Control & Input Routing
------------------------------

Once the Client Manager identifies the local player and the entry RPC is processed, the input routing changes:

* **Walking Mode**: The ``PlayerControllerSystem`` reads ``PlayerInput`` and directly modifies ``PhysicsVelocity``.
* **Driving Mode**:
    * The ``PlayerInCarTag`` is enabled.
    * The ``PlayerCarInputSystem`` continues to update the player's ``PlayerInput``.
    * The server-side ``ServerSyncPlayerVehicleInputSystem`` reads the input from the driver (Player entity) and copies it to the vehicle's ``VehicleInputReader``.
* **Authority**: This ensures that even while driving, the player's inputs are handled via the same networked component, maintaining consistency.

Input Flow
----------

This diagram illustrates how user keystrokes travel from the local hardware to the physical simulation on the server.

.. code-block:: text

    [ Hardware Input ] 
           |
           v
    [ Unity Input System ] -> Reads Action Map ("Player")
           |
           v
    [ PlayerCarInputSystem ] -> Updates local 'PlayerInput' component
           |
           v
    [ Client Prediction ] -> Immediate local movement (PhysicsVelocity)
           |
           v
    [ Ghost Snapshot ] --(Network)--> [ Server Simulation ]
                                             |
                                             +-- Walking: PlayerControllerSystem
                                             |
                                             +-- Driving: ServerSyncPlayerVehicleInputSystem
                                                           (Copies Input to VehicleInputReader)
                                             |
                                             v
                                      [ Physics World ]

Interaction Flow
----------------

The vehicle entry process utilizes a request-response pattern to maintain server authority over entity ownership.

.. code-block:: text

    1. [ Detection ] : Client Manager checks proximity via 'VehicleDetectionConfig'.
    2. [ UI Prompt ] : 'CanEnterVehicleTag' enables "Press E" interaction.
    3. [ Request ]   : Client sends 'EnterVehicleRequest' RPC to the Server.
    4. [ Validation ]: Server checks vehicle availability and player distance.
    5. [ Authority ] : Server updates 'GhostOwner' of the vehicle to Player's NetworkId.
    6. [ Parenting ] : 'NetcodeInteractUtils' attaches Player to Vehicle hierarchy.
    7. [ Sync ]      : Server sends Snapshot -> All clients hide player visuals.