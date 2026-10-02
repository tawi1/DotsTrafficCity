.. _netcodeGo:

NetCode For GameObjects
=======================

Installation
------------

#. Import Netcode sample.
#. Install `NetCode for GameObjects <https://docs.unity3d.com/Packages/com.unity.netcode.gameobjects@2.13/manual/index.html>`_ package.
#. Add `CUSTOM_NETWORK` scripting define to the project settings.
#. Unpack ``DotsCity/Packages/Upgrades/NetcodeGOPrefabs`` package.
#. In the :ref:`Cull Config <cullConfig>`, set the calculation mode to `Multiplayer Calculate Distance` or `Multiplayer Camera View`.
#. Drag & drop `NGOPrefabRoot` into the scene & in that root, in the `PrefabRootResolve` component, press the `Resolve Refs` button (new scene only).
#. Install `Multiplayer Play Mode <https://docs.unity3d.com/Packages/com.unity.multiplayer.playmode@2.0/manual/index.html>`_ package to simulate multiple local players **(optional)**.
#. Open `NGODemo` sample scene.

	.. note:: 
		By default, only the `NGODemo` scene works out of the box.

Architecture & Code Structure
-----------------------------

The Netcode for GameObjects (NGO) integration in **DotsCity** provides a network transport layer, object wrappers, and efficient serialization wrappers for traffic, pedestrians, and traffic lights.

System Services & Providers
~~~~~~~~~~~~~~~~~~~~~~~~~~~

System-level services and infrastructure providers that handle network session setup, low-level messaging, and object lifetime:

* **NgoProviderSO**: A ScriptableObject provider (`NetworkProviderSO`) that initializes the NGO network stack, registers all message types in `UniversalNetworkService`, and creates the `PedestrianBroadcaster`.
* **NgoTransport**: Implements `INetworkTransport` using NGO's `CustomMessagingManager`. Handles server/client session lifecycle, message sending (`Reliable` / `Unreliable`), and event callbacks.
* **NgoMessageRegistry**: A static registry that links internal network messages (traffic batches, pedestrian spawns, traffic light states, etc.) with their respective NGO serialization wrappers.
* **NgoPlayerSpawnerSO**: ScriptableObject spawner that handles server-side instantiation and NGO `NetworkObject` spawning with client ownership assignment.
* **NgoVehicleNetworkSync**: Central scene/system manager that synchronizes vehicle ownership and state between NGO and the DOTS/Mono hybrid traffic system. Manages driver assignment, physics toggling, ownership changes, and enables/disables `NetworkTransform` components upon entering/exiting vehicles.

Player-Attached Components
~~~~~~~~~~~~~~~~~~~~~~~~~~

Components and adapters attached directly to the **Player Prefab**:

* **NgoPlayerMovementAdapter**: Attached to the player prefab. Controls movement activation and input handling, enabling local simulation exclusively for the owning client.
* **NgoPlayerRpcTransport**: Attached to the player prefab. Transmits vehicle enter/exit ServerRPCs and ClientsRPCs, bridging client interactions with `PlayerNetworkInteractionBridge`.
* **NgoPlayerSpawnNotifier**: Attached to the player prefab. Handles player lifecycle events, registers spawned instances in `PlayerRegistry`, and notifies local spawners upon client initialization.

Vehicle-Attached Components
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Components and adapters attached directly to **Vehicle Prefabs**:

* **NgoNetworkVehicleObserver**: Attached to vehicle prefabs. Synchronizes unique vehicle IDs via `NetworkVariable<int>` and triggers client-side vehicle spawn/despawn hooks in `NgoVehicleNetworkSync`.
* **NgoVehicleInputSyncAdapter**: Attached to vehicle prefabs. Synchronizes vehicle control inputs (throttle, steering, handbrake) from owner clients to the server via ServerRPCs and distributes them using `NetworkVariable`.

Scene & Culling Adapters
~~~~~~~~~~~~~~~~~~~~~~~~

* **NgoCullPointAdapter**: Attached to camera/cull point GameObjects. Acts as a network bridge for `CullPointCore`, streaming client camera position and view projection matrix to the server ECS via `SubmitCullPointServerRpc`.
* **NgoIdentityWrapper & NgoBehaviourWrapper**: Generic Mono/NGO adapters for `NetworkObject` and `NetworkBehaviour` components, conforming them to internal `INetworkIdentity` and `INetworkBehaviour` interfaces.

Data Serialization & Wrappers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To minimize GC allocations and optimize bandwidth, custom serialization wrappers implementing `INetworkSerializable` are used:

* **Vehicles**: `NgoTrafficBatchBroadcast`, `VehicleSpawnDataWrapper`, and `VehicleDespawnDataWrapper`. Uses `NgoVehicleSnapshotSerializers` with pre-allocated static read buffers.
* **Traffic Lights**: `NgoTrafficLightBroadcast` serializes traffic light states using reusable array buffers.
* **Pedestrians**: Wrappers including `PedestrianSpawnBroadcastWrapper`, `PedestrianTransformBroadcastWrapper`, `PedestrianStateBroadcastWrapper`, `PedestrianRagdollBroadcastWrapper`, and initial state sync wrappers.
* **Player Signals**: `NgoPlayerReadySignalWrapper` for synchronization of player readiness signals.