.. _monoNetworking:

Mono Networking
===============

This section covers the architecture, lifecycle management, interfaces, services, management components, data payloads, client/server pedestrian and traffic synchronization systems, vehicle network bridges, execution flows, and Unity Netcode for GameObjects (NGO) integration wrappers for the Mono Networking framework in DOTS City Sample.

Overview
--------

High-performance simulation processing and network synchronization are separated using an event-driven lifecycle and framework-agnostic strategies. The network architecture relies on abstract base classes, interfaces, and ScriptableObjects to decouple high-level game logic from underlying networking solutions (such as Unity Netcode for GameObjects, FishNet, or Mirror).

Samples & Demonstration
-----------------------

The framework includes ready-to-use sample scenes for supported networking backends:

* **NGODemo Sample:** Out of the box, the `NGODemo` sample scene demonstrates full integration with Unity Netcode for GameObjects (NGO), including player spawning, pedestrian streaming, traffic batching, and traffic light synchronization[cite: 74].

  * **Documentation:** For detailed setup, configuration, and architectural breakdown, see the :ref:`NetCode For GameObjects <netcodeGo>` documentation[cite: 76].
  * **Setup Requirements:** Requires installing the `com.unity.netcode.gameobjects` package, adding the `CUSTOM_NETWORK` scripting define in Project Settings, and importing the `NetcodeGOPrefabs` upgrade package[cite: 74, 76].

* **FishNetDemo Sample:** Out of the box, the `FishNetDemo` sample scene demonstrates integration with the FishNet networking solution[cite: 74, 75].

  * **Documentation:** For detailed setup, configuration, and architectural breakdown, see the :ref:`FishNet Integration <fishnet>` documentation[cite: 75].
  * **Setup Requirements:** Requires downloading and importing the `FishNet` package, adding the `CUSTOM_NETWORK` scripting define in Project Settings, importing the `FishNetPrefabs` upgrade package, and placing `FishnetPrefabRoot` into the scene[cite: 75].

Architecture Diagram & Execution Flow
------------------------------------

The following diagram illustrates the interaction between scene bootstrapping, strategy providers, core services, pedestrian network broadcasters, traffic adapters, vehicle network bridges, and client/server synchronization systems:

.. code-block:: text

  +-----------------------------------------------------------------------------------+
  |                                   BOOTSTRAP                                       |
  |                                                                                   |
  |                        [ NetworkBootstrapAdapter ]                                |
  |                                    |                                              |
  |                    Delegates stack creation & host check                          |
  |                                    v                                              |
  |                         [ NetworkProviderSO ]                                     |
  |                                    |                                              |
  |             +----------------------+----------------------+                       |
  |             v                                             v                       |
  |  [ NetworkServiceLocator ]                   [ PedestrianBroadcasterService ]     |
  |             |                                             |                       |
  +-------------+---------------------------------------------+-----------------------+
                |                                             |
    Holds INetworkService                         Holds IPedestrianNetworkBroadcaster
                |                                             |
        +-------+---------------------------------------------+-------+
        |                                                             |
        v                                                             v
  +---------------------------------------+     +---------------------------------------+
  |              SERVER SIDE              |     |              CLIENT SIDE              |
  |                                       |     |                                       |
  |  [ PedestrianNetworkInitializer ]     |     |  [ PedestrianNetworkInitializer ]     |
  |    |                                  |     |    |                                  |
  |    +--> [ Server ECS Systems ]        |     |    +--> [ Client ECS Systems ]        |
  |    |    - PedestrianServerSpawnSync   |     |    |    - PedestrianClientSpawnSystem |
  |    |    - PedestrianServerDespawn     |     |    |    - PedestrianClientTransformSync|
  |    |    - PedestrianServerTransformSync|    |    |    - PedestrianClientInterpolation|
  |    |    - PedestrianServerStateSync   |     |    |    - PedestrianClientStateSync   |
  |    |    - PedestrianServerRagdollSync |     |    |    - PedestrianClientRagdollSystem|
  |    |                                  |     |    |    - PedestrianClientCustomAnim  |
  |  [ TrafficLightInitializerBase ]      |     |    |                                  |
  |    |                                  |     |  [ PedestrianClientDespawnHandler ]   |
  |    +--> [ TrafficLightBridge ]        |     |  [ TrafficLightInitializerBase ]      |
  |    +--> [ TrafficLightServerSync ]    |     |    |                                  |
  |  [ ArcadeVehicleNetworkBridge ]       |     |    +--> [ TrafficLightBridge ]        |
  |  [ TrafficAdapter ] (Sender/Broadcast)|     |    +--> [ ClientTrafficLightManager ] |
  |  [ PlayerSpawnerBase ]                |     |  [ ClientTrafficInitializerBase ]     |
  |  [ UniversalServerConnection ]        |     |  [ ClientTrafficManager ]             |
  |                                       |     |  [ ClientVehicleAudioManager ]        |
  |                                       |     |  [ TrafficAdapter ] (Receiver)        |
  |                                       |     |  [ UniversalClientManager ]           |
  +---------------------------------------+     +---------------------------------------+

Execution Order & Data Flow
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Initialization Sequence:**
   * ``NetworkBootstrapAdapter`` runs early (Execution Order ``-2000``).
   * It calls ``NetworkProviderSO.CreateNetworkStack()`` to initialize transport services and ``IPedestrianNetworkBroadcaster``.
   * Servicing references are registered globally in ``NetworkServiceLocator.Instance`` and ``PedestrianBroadcasterService.Instance``.
   * ``PedestrianNetworkInitializer`` executes client or server initialization, spinning up necessary ECS network systems on respective worlds.
   * ``TrafficLightInitializerBase`` (and concrete implementations like ``TrafficLightInitializer``) binds ``TrafficLightBridge`` to ``INetworkService``, initializing ``TrafficLightServerNetworkSyncSystem`` on the server world or ``ClientTrafficLightManager`` on clients.
   * ``TrafficAdapter`` initializes network receivers on clients and acts as a bridge for streaming traffic batches.

2. **Pedestrian Lifecycle & Synchronization Flow:**
   * **Server Entity Creation & Spawning:** ``PedestrianServerSpawnSyncSystem`` queries un-synced pedestrians, assigns network IDs, transmits ``PedestrianSpawnBroadcast`` to clients, and disables sync tags.
   * **Client Connection & Snapshot:** ``PedestrianClientSpawnSystem`` requests an initial snapshot via ``PedestrianBroadcasterService`` upon creation. ``PedestrianServerStateSyncSystem`` receives the request and returns a complete state snapshot of all active scene pedestrians.
   * **Spawning on Client:** Server broadcasts ``PedestrianSpawnBroadcast``; ``PedestrianClientSpawnSystem`` dequeues broadcasts, instantiates entities, and populates ``ClientEntityMap``.
   * **Transform Updates:** Server-side ``PedestrianServerTransformSyncSystem`` queries entity transforms and streams ``PedestrianTransformBroadcast``. Client-side high-frequency updates arrive and are enqueued into a NativeQueue processed by ``PedestrianClientTransformSyncSystem``, updating ``PedestrianNetworkTargetTransform``.
   * **Dead-Reckoning & Interpolation:** ``PedestrianClientInterpolationSystem`` reads ``PedestrianNetworkTargetTransform`` to smoothly interpolate local transform positions/rotations towards target positions and applies dead-reckoning extrapolation if packets are delayed.
   * **States & Events:** ``PedestrianServerStateSyncSystem`` monitors state changes and broadcasts ``PedestrianStateBroadcast``. Client systems (``PedestrianClientStateSyncSystem``, ``PedestrianClientRagdollSystem``, and ``PedestrianClientCustomAnimSystem``) consume state, ragdoll impulse, and animation events.
   * **Ragdoll Physics Sync:** Server-side ``PedestrianServerRagdollSyncSystem`` captures active ragdoll events, sends physical impact parameters via ``PedestrianRagdollBroadcast``, and disables ragdoll components to prevent re-execution.
   * **Despawning:** Server-side ``PedestrianServerDespawnSystem`` monitors pooled or culled entities and sends ``PedestrianDespawnBroadcast``. The payload triggers ``PedestrianClientDespawnHandler`` to destroy ECS entities and clean up local dictionary mappings.

3. **Traffic & Vehicle Synchronization Flow:**
   * **Arcade Vehicle Bridge:** ``ArcadeVehicleNetworkBridge`` runs on execution order ``-90``. In ``FixedUpdate``, it reads physics velocity, control input (throttle/steering), sound culling tags, and horn states across registered vehicles, packing them into ``VehicleSnapshot`` arrays.
   * **Vehicle Spawning & Despawning:** On first detection, ``ArcadeVehicleNetworkBridge`` sends reliable spawn broadcasts (``VehicleSpawnData``) with model indices. Despawned or removed vehicles trigger reliable despawn events (``VehicleDespawnData``).
   * **Batch Streaming:** Server broadcasts batched snapshot arrays via ``TrafficAdapter`` (or any assigned `ITrafficNetworkSender`).
   * **Client Processing & Lazy Spawning:** ``TrafficAdapter`` receives ``TrafficBatchBroadcastData`` and forwards it to ``ClientTrafficManager``, which performs lazy instantiation via global pooling or applies snapshot positions, rotations, and input states.
   * **Vehicle Audio:** ``ClientVehicleAudioManager`` tracks active client vehicles, synchronizes engine sound pitch/volume based on vehicle velocity and gear ratios, and manages secondary concurrent audio tracks like horns.

Core Architecture & Utilities
-----------------------------

NetworkBootstrapAdapterBase & NetworkBootstrapAdapter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`NetworkBootstrapAdapterBase` serves as the primary entry point for network initialization. `NetworkBootstrapAdapter` extends it to delegate transport creation and host evaluation to an assigned `NetworkProviderSO`.

* **Execution Order:** Defaults to `-2000` to execute prior to standard scene components.
* **Responsibilities:**
  * Creates and registers transport-agnostic `INetworkService` and `IPedestrianNetworkBroadcaster` via `NetworkProviderSO`.
  * Subscribes to transport connection and disconnection events (`OnServerStarted`, `OnServerStopped`, `OnClientConnected`, `OnClientDisconnected`).
  * Orchestrates `SimulationBootstrap` startup and passes injected services down to all registered `NetworkInitializerBase` components.

NetworkServiceLocator
~~~~~~~~~~~~~~~~~~~~~

`NetworkServiceLocator` is a global static service locator providing decoupled access to the active `INetworkService` instance across traffic, pedestrian, and city logic systems.

NetworkLogger
~~~~~~~~~~~~~

`NetworkLogger` is a global logging service featuring static helpers (`Log`, `LogWarning`, `LogError`). Methods use `[Conditional]` attributes to strip execution from release builds unless `UNITY_EDITOR` or `DEVELOPMENT_BUILD` is defined.

NetworkInitializerBase
~~~~~~~~~~~~~~~~~~~~~~

`NetworkInitializerBase` is an abstract base class for components requiring managed lifecycle hooks tied to network initialization and shutdown.

* **Responsibilities:**
  * Holds references to `ServerWorld` and `ClientWorld`.
  * Provides abstract methods `InitializeServer(bool isHost)` and `InitializeClient(bool isHost)` for system setup.
  * Provides virtual cleanup hooks `UninitializeServer()` and `UninitializeClient()` for safe handler unregistration upon disconnection.

PlayerSpawnerBase
~~~~~~~~~~~~~~~~~

`PlayerSpawnerBase` extends `NetworkInitializerBase` to handle networked player instantiation and spawn location management.

* **Key Features:**
  * Implements a singleton reference (`PlayerSpawnerBase.Instance`) with duplicate component cleanup.
  * Manages cyclic selection across an array of assigned spawn points.
  * Exposes `OnSpawned` and `OnLocalSpawned` events for dependent systems.

Universal Client & Lobby Management
-----------------------------------

UniversalClientManager
~~~~~~~~~~~~~~~~~~~~~~

`UniversalClientManager` extends `ClientManagerBase` to provide transport-agnostic client lifecycle control.

* Subscribes to transport connection events (`OnClientConnected`, `OnClientDisconnected`) via `NetworkServiceLocator`.
* Binds local player instantiation events (`OnLocalSpawned`) from `PlayerSpawnerBase` to `PlayerNetworkInteractionBridge`.

UniversalLobbyAdapter
~~~~~~~~~~~~~~~~~~~~~

`UniversalLobbyAdapter` implements `INetworkLobbyAdapter`. It transmits a `PlayerReadySignalData` message to the server once local scene loading completes.

Strategy Patterns
-----------------

NetworkProviderSO
~~~~~~~~~~~~~~~~~

`NetworkProviderSO` is an abstract `ScriptableObject` factory strategy.

* **Methods:**
  * `CreateNetworkStack()`: Instantiates and configures transport-specific `INetworkService` and `IPedestrianNetworkBroadcaster` implementations.
  * `CheckIsHost()`: Evaluates if the running transport instance is currently operating in Host mode.

NetworkPlayerSpawnerSO
~~~~~~~~~~~~~~~~~~~~~~

`NetworkPlayerSpawnerSO` is an abstract `ScriptableObject` strategy for player prefab instantiation.

* **Methods:**
  * `SpawnPlayer(...)`: Encapsulates framework-specific network spawning logic and ownership assignment on the server.

UI & Connection Management
--------------------------

ServerConnectionBase & UniversalServerConnection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`ServerConnectionBase` provides abstract UI state management for connection controls (Client, Server, Host, and Start buttons). `UniversalServerConnection` implements it by binding UI controls directly to `INetworkTransport` events.

* **Features:**
  * Handles Client, Dedicated Server, and Host mode state transitions dynamically.
  * Updates button interactability, panel visibility, and text color indicators (`stoppedColor`, `changingColor`, `startedColor`).
  * Includes `EditorResolve()` for locating UI references in the Unity Editor.

Entity Identification & Registration
-----------------------------------

NetworkId
~~~~~~~~~

`NetworkId` is a lightweight `MonoBehaviour` wrapper attached to scene `GameObject` instances. It maintains a unique integer identifier (`Id`) utilized by both client and server systems to resolve and bind entity references across the network.

NetworkEntityId
~~~~~~~~~~~~~~~

`NetworkEntityId` is an ECS component (`IComponentData`) holding a unique network integer identifier. It bridges DOTS entities on the client and server for entity association and lookups.

VehicleNetworkRegister
~~~~~~~~~~~~~~~~~~~~~~

`VehicleNetworkRegister` acts as a registration bridge attached directly to individual vehicle GameObjects.

* **Responsibilities:**
  * Caches local component references such as `Rigidbody` and `IVehicleInput`.
  * Automatically registers itself with `ArcadeVehicleNetworkBridge` during `OnEnable()` and unregisters during `OnDisable()`.

ArcadeVehicleNetworkBridge
~~~~~~~~~~~~~~~~~~~~~~~~~~

`ArcadeVehicleNetworkBridge` is a singleton manager executing early at order `-90` that collects vehicle inputs, physics transforms, sound tags, and horn states on the server.

* **Key Features:**
  * **Snapshot Packing:** Serializes up to 1000 vehicle snapshots into `VehicleSnapshot` structs using `half3` velocities, 8-bit packed yaws, and 8-bit clamped input controls.
  * **Lifecycle & Caching:** Caches entity references, GameObjects, and model indices (`CarModelComponent`).
  * **Automated Broadcasts:** Triggers `VehicleSpawnData` when vehicles appear and `VehicleDespawnData` when vehicles are destroyed or unmanaged.
  * **Player Vehicle Tracking:** Manages `RegisterPlayerVehicle` and `UnregisterPlayerVehicle` for seamless player entry/exit lookups.

Network Services & Systems
--------------------------

UniversalNetworkService
~~~~~~~~~~~~~~~~~~~~~~~

`UniversalNetworkService` is a fully typed implementation of `INetworkService`.

* Guarantees zero runtime allocations and zero boxing during message registration and broadcasting.
* Uses internal `BroadcastSender` and `BroadcastDispatcher` implementations to wrap and unwrap network payloads (`TData`) to transport-specific serialization wrappers (`TWrapper`).

Traffic Light Systems, Bridges & Initializers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **TrafficLightBridge:** Transport-agnostic bridge implementing `ITrafficLightNetworkBridge` and `INetworkReceiver<TrafficLightBroadcastData>`. Uses a resized `sendBuffer` to broadcast snapshot buffers without runtime allocations, and invokes `OnStateReceived` on connected clients.
* **TrafficLightInitializerBase:** Abstract base initializer deriving from `NetworkInitializerBase`. Injects `INetworkService` into `TrafficLightBridge`, subscribes client receivers during client startup, and initializes `TrafficLightServerNetworkSyncSystem` on the server world.
* **TrafficLightInitializer:** Default concrete implementation of `TrafficLightInitializerBase` working with any active `INetworkTransport`.
* **TrafficLightServerNetworkSyncSystem:** Server-side ECS system executing in `MainThreadLateGroup`. Uses native ECS change filtering (`WithChangeFilter<LightHandlerComponent>`) to collect modified traffic light states and broadcast them via `ITrafficLightNetworkBridge`.
* **ClientTrafficLightManager:** Client-side component subscribing to network state updates (`OnStateReceived`) from `ITrafficLightNetworkBridge` and applying them to `TrafficLightHybridService`.

Pedestrian Network Infrastructure
---------------------------------

PedestrianBroadcasterService
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`PedestrianBroadcasterService` is a static service locator holding the global reference to `IPedestrianNetworkBroadcaster`.

PedestrianBroadcaster
~~~~~~~~~~~~~~~~~~~~~

`PedestrianBroadcaster` is a zero-allocation, pure C# core implementation of `IPedestrianNetworkBroadcaster`.

* Implements strongly-typed receivers (`INetworkReceiver<T>`) for all pedestrian broadcasts.
* Utilizes a static generic cache `BroadcastSender<T>` to execute delegate routing without boxing or GC allocations.

PedestrianNetworkInitializer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`PedestrianNetworkInitializer` extends `NetworkInitializerBase` to configure and register pedestrian ECS synchronization systems.

* **Server Initialization:** Registers server spawn, despawn, transform, state, and ragdoll sync systems on `ServerWorld`.
* **Client Initialization:** Registers client spawn, transform sync, interpolation, state sync, custom animation, and ragdoll systems on `ClientWorld`.

Server Pedestrian Systems
-------------------------

PedestrianServerSpawnSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Server-side system executing in `MainThreadLateGroup`.

* Queries newly created pedestrians with `PedestrianSpawnSyncedTag`.
* Assigns unique `NetworkEntityId` values, transmits `PedestrianSpawnBroadcast` payloads, and disables `PedestrianSpawnSyncedTag` to prevent duplicate processing.

PedestrianServerTransformSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Server-side system running in `MainThreadLateGroup`. Periodically queries `LocalTransform` components of active pedestrians and broadcasts `PedestrianTransformBroadcast` updates to connected clients.

PedestrianServerStateSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Monitors animation, action, and movement states of pedestrians.

* Tracks historical entity states using `NativeHashMap<int, PedestrianStateBroadcast>` to send delta state updates only when changes occur.
* Subscribes to `RegisterServerInitialStateReceiver` to generate and send full `PedestrianInitialStateSnapshot` arrays to late-joining clients upon request.

PedestrianServerRagdollSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Server system running in `MainThreadEventGroup` processing physical ragdoll activation.

* Broadcasts physical impact parameters (`Position`, `Rotation`, `ForceDirection`, `ForceMultiplier`, `DamageType`) via `PedestrianRagdollBroadcast`.
* Runs Burst-compiled `ActivateRagdollJob` to disable `RagdollComponent` and prevent re-triggering while recording NPC death event data.

PedestrianServerDespawnSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Server-side system running in `BeforeDestroyGroup`. Monitors pedestrian entities flagged with `PooledEventTag` or `CulledEventTag` and broadcasts `PedestrianDespawnBroadcast` payloads to clean up client instances.

Client Pedestrian Systems, Components & Handlers
------------------------------------------------

PedestrianNetworkTargetTransform
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ECS component (`IComponentData`) storing spatial target history, velocity vectors, and timestamps (`TargetPosition`, `TargetRotation`, `PreviousPosition`, `PreviousRotation`, `Velocity`, `LastReceiveTime`) for client-side interpolation.

PedestrianClientSpawnSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Client-side system responsible for consuming spawn broadcasts and initial state snapshots.

* Maintains `ClientEntityMap` (`NativeHashMap<int, Entity>`) for fast lookup of network entity instances on clients.
* Instantiates visual pedestrian entities from `PedestrianEntityPrefabContainer` buffers based on skin indices and initial state parameters.

PedestrianClientTransformSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Burst-compiled `ISystem` running in `LateInitGroup` for high-performance transform update processing.

* Direct execution on the main thread draining unmanaged `NativeQueue<PedestrianTransformBroadcast>` structures.
* Updates `PedestrianNetworkTargetTransform` components with target positions, rotations, and calculated velocity vectors.

PedestrianClientInterpolationSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Client system executing spatial interpolation and dead-reckoning extrapolation.

* Smoothly lerps entity positions and slerps rotations towards target transform states stored in `PedestrianNetworkTargetTransform` using configurable `InterpolationSpeed`.
* Extrapolates predicted target positions using velocity vectors if network packets are delayed past threshold limits.

PedestrianClientStateSyncSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Processes incoming `PedestrianStateBroadcast` messages. Updates `StateComponent` and triggers `MovementStateChangedEventTag` and `AnimationStateComponent` updates.

PedestrianClientRagdollSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Consumes physical ragdoll events (`PedestrianRagdollBroadcast`) from a thread-safe queue. Applies impact force vectors, force multipliers, and damage types to `RagdollComponent` while enabling `RagdollActivateClientEventTag`.

PedestrianClientCustomAnimSystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Consumes `PedestrianCustomAnimBroadcast` queue payloads. Dynamically enables or disables `HasCustomAnimationTag` and `CustomAnimatorStateTag` components on local client entities.

PedestrianClientDespawnHandler
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Static client-side handler method for despawning pedestrians. Looks up entities in `PedestrianClientSpawnSystem.ClientEntityMap`, destroys them via `PoolEntityUtils.DestroyEntity`, and removes key mappings.

Client Traffic & Audio Management
---------------------------------

ClientTrafficManager
~~~~~~~~~~~~~~~~~~~~

Client-side singleton managing traffic vehicle spawning, physical state tracking, lazy instantiation, and smooth Target-position interpolation.

* **Lazy Spawning & Snapshot Processing:** Consumes `VehicleSnapshot` batch streams, instantiating missing vehicles dynamically via `TrafficCarPoolGlobal`.
* **Network Conversions:** Supports converting dummy AI traffic vehicles into interactive networked objects via `ConvertToNetworkVehicle`, transferring physical controller states seamlessly.
* **Kinematic & Physics Interpolation:** Soft-corrects dynamic rigidbodies and interpolates kinematic transforms based on distance error thresholds (`positionCorrectionThreshold`, `maxTeleportDistance`).

ClientVehicleAudioManager
~~~~~~~~~~~~~~~~~~~~~~~~~

Event-driven audio manager leveraging `BuiltInSoundService` to drive dual-layer vehicle sounds.

* **Layer 1 (Engine):** Dynamically updates engine audio pitch and volume based on vehicle speed, gear ratios, and custom pitch parameters.
* **Layer 2 (Secondary):** Handles concurrent one-shot audio events (such as horn tracks) without interrupting primary engine loops.
* **Seamless Transfer:** Binds audio tracks to new network GameObjects during traffic-to-network vehicle conversions.

TrafficAdapter
~~~~~~~~~~~~~~

Universal network-agnostic adapter implementing `ITrafficNetworkSender`, `ITrafficSpawnBroadcaster`, and client network receivers (`INetworkReceiver<TrafficBatchBroadcastData>`, `VehicleSpawnData`, `VehicleDespawnData`).

* **Server Role:** Broadcasts unreliable batch traffic snapshots (`SendTrafficBatch`) and reliable spawn/despawn events.
* **Client Role:** Forwards received traffic batches and explicit spawn/despawn requests directly to `ClientTrafficManager`.

Network Abstraction Interfaces
------------------------------

INetworkService & INetworkTransport
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

High-level, zero-allocation messaging service (`INetworkService`) and low-level transport wrapper (`INetworkTransport`).

* **Key Features:**
  * `BroadcastToClients<T>`, `BroadcastToClient<T>`, and `SendToServer<T>` for generic message transmission.
  * Strongly-typed `INetworkReceiver<T>` (client) and `INetworkServerReceiver<T>` (server) for handling messages without boxing or GC allocations.

INetworkBehaviour & INetworkIdentity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abstraction wrappers decoupling component-level ownership and network identities from underlying networking libraries:

* **INetworkIdentity:** Provides access to network `Id`, `OwnerId`, `IsOwner`, `IsSpawned`, and methods for ownership transfers (`GiveOwnership`, `RemoveOwnership`).
* **INetworkBehaviour:** Exposes server/client flags, ownership state, and references to the parent `INetworkIdentity`.

IPedestrianNetworkBroadcaster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abstraction layer defining high-performance network broadcasting and snapshot synchronization for mass pedestrian simulation.

* Handles client receiver registration, streaming transforms, state updates, ragdoll activation, and targeted initial snapshot delivery for late-joining clients.

Traffic & Vehicle Interfaces
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **ITrafficNetworkSender:** Batch-transmits compressed vehicle state snapshots (`VehicleSnapshot`) across active transports.
* **ITrafficSpawnBroadcaster:** Broadcasts reliable vehicle spawn (`VehicleSpawnData`) and despawn (`VehicleDespawnData`) events.
* **INetworkVehicleObserver:** Contract for framework-specific vehicle network observers managing ID synchronization and lifecycle.
* **ITrafficLightNetworkBridge:** Decouples traffic light ECS simulation from specific networking transport layers for state synchronization.

Network Data Payloads & Messages
--------------------------------

Pedestrian Snapshots & Broadcasts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lightweight unmanaged structs used by the pedestrian synchronization layer:

* **PedestrianSpawnBroadcast:** Payload containing spawn parameters (NetworkId, SkinIndex, AnimationSpeed, SpawnPosition, SpawnRotation).
* **PedestrianDespawnBroadcast:** Payload for despawning pedestrian entities on clients.
* **PedestrianTransformBroadcast:** Unreliable payload streaming compressed position (`float3`) and rotation (`quaternion`) updates.
* **PedestrianStateBroadcast:** Synchronizes action states, additive state flags, movement states, and animation states.
* **PedestrianCustomAnimBroadcast:** Toggles custom animation and animator states on pedestrian entities.
* **PedestrianRagdollBroadcast:** Triggers ragdoll activation on clients with impact force vectors and damage types.
* **PedestrianInitialStateRequest & PedestrianInitialStateSnapshot:** Enables late-joining clients to request and receive full state snapshots of all active scene pedestrians.

Traffic & Vehicle Payloads
~~~~~~~~~~~~~~~~~~~~~~~~~~

* **VehicleSnapshot:** Compact struct for streaming vehicle transforms, velocity (`half3`), packed yaw (`byte`), input controls (`sbyte` throttle/steering), and `VehicleStateFlags` (sound culling, physics, horn, braking).
* **VehicleStateFlags:** Bitwise enum describing sound, physics, horning, and braking status.
* **VehicleSpawnData:** Contains initial position, rotation, vehicle ID, and car model index for spawning client vehicle instances.
* **VehicleDespawnData:** Contains the unique `VehicleId` of a vehicle to be despawned across clients.
* **VehicleInputData:** Struct containing client input values (`Steering`, `Throttle`, `Handbrake`) sent to the server for authority processing.
* **TrafficBatchBroadcastData:** Array segment payload (`ArraySegment<VehicleSnapshot>`) for batched streaming of active traffic snapshots.

Traffic Light Synchronization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **TrafficLightSnapshot:** Lightweight struct storing crossroad `HandlerId` and state byte value.
* **TrafficLightBroadcastData:** Wraps an array or segment (`ArraySegment<TrafficLightSnapshot>`) for batched transmission of light updates.

Signal Handlers
~~~~~~~~~~~~~~~

* **PlayerReadySignalData:** Empty signal payload sent by clients upon completing scene initialization to trigger player spawning on the server.

Player & Vehicle Interaction Subsystem
--------------------------------------

Player Character & Spawning Components
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PlayerRegistry
^^^^^^^^^^^^^^

``PlayerRegistry`` is a global singleton registry mapping network connection and owner IDs to active player GameObjects. It enables remote clients and server systems to locate specific driver instances during network synchronization.

UniversalPlayerSpawner
^^^^^^^^^^^^^^^^^^^^^^

``UniversalPlayerSpawner`` extends ``PlayerSpawnerBase`` and implements ``INetworkServerReceiver<PlayerReadySignalData>`` to process client connection signals on the server. Upon receiving a ready signal, it calculates spawn coordinates and delegates instantiation and network ownership assignment to an assigned ``NetworkPlayerSpawnerSO`` strategy.

PlayerMovementCore
^^^^^^^^^^^^^^^^^^

``PlayerMovementCore`` is a framework-agnostic character controller managing camera-relative translation, rotation, jumping, and gravity via ``CharacterController`` and Unity Input System.

* **Camera-Relative Vectoring:** Calculates movement vectors relative to ``Camera.main`` transform axes.
* **Rotation Smoothing:** Smoothly interpolates character rotation towards the movement vector using ``Quaternion.Slerp``.
* **Input Map Control:** Exposes ``EnableInput(bool)`` to activate or deactivate local movement action maps when entering or exiting vehicles.

PlayerVisualController
^^^^^^^^^^^^^^^^^^^^^^

``PlayerVisualController`` toggles character renderers, colliders, and ``CharacterController`` components without deactivating the underlying ``GameObject``. This ensures RPC handlers and network communication bridges remain active while the player is inside a vehicle.

PlayerInteractCasterBase
^^^^^^^^^^^^^^^^^^^^^^^^

``PlayerInteractCasterBase`` provides periodic forward raycasting to detect interactable world objects (such as vehicles). It manages raycast frequency, target switching state, and notifies listeners via the ``OnCastStateChanged`` event.

MonoVehicleInteractCaster
^^^^^^^^^^^^^^^^^^^^^^^^^

``MonoVehicleInteractCaster`` extends ``PlayerInteractCasterBase`` to handle interaction casting specifically for vehicles. It validates driver availability via ``MonoVehicleNetworkSyncBase`` and delegates entry and exit requests to an assigned ``IVehicleNetworkBridge`` upon input detection.

Vehicle Network Synchronization & Driver Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IPlayerNetworkInteractionBridge
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``IPlayerNetworkInteractionBridge`` is a transport-agnostic interface defining methods for sending vehicle entry (``RequestEnter``) and exit (``RequestExit``) requests.

IPlayerRpcTransport
^^^^^^^^^^^^^^^^^^^

``IPlayerRpcTransport`` provides a network abstraction contract for broadcasting RPC events (such as ``SendServerRequestEnter``, ``SendServerRequestExit``, ``BroadcastEnteredVehicle``, and ``BroadcastExitedVehicle``) across different networking backends.

IVehicleNetworkBridge
^^^^^^^^^^^^^^^^^^^^^

``IVehicleNetworkBridge`` provides an interface for client-to-server vehicle entry and exit requests (``RequestEnterVehicle``, ``RequestExitVehicle``) along with server/client environment checks.

PlayerNetworkInteractionBridge
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``PlayerNetworkInteractionBridge`` acts as the transport-agnostic bridge for vehicle entry and exit requests. It coordinates with ``IPlayerRpcTransport`` to send client requests and handle server-to-client RPC callbacks:

* **Client Entry/Exit Requests:** ``RequestEnter(vehicleId)`` and ``RequestExit(vehicleId)`` send requests to the server via ``IPlayerRpcTransport``.
* **Server Request Handling:** ``ProcessServerRequestEnter`` and ``ProcessServerRequestExit`` validate requests, register network override flags in ``ClientTrafficManager``, and invoke driver assignment in ``MonoVehicleNetworkSyncBase``.
* **Client Broadcast Callbacks:** ``ProcessClientEnteredVehicle`` and ``ProcessClientExitedVehicle`` locate the target driver via ``PlayerRegistry``, parent/unparent transforms, update visual states, and notify ``InteractionHandler``.

InteractionHandler
^^^^^^^^^^^^^^^^^^

``InteractionHandler`` is a singleton handling raycasting for interactable vehicles. It works with ``IPlayerNetworkInteractionBridge`` to manage client-side state transitions when entering or leaving vehicles.

MonoVehicleNetworkSyncBase
^^^^^^^^^^^^^^^^^^^^^^^^^^

``MonoVehicleNetworkSyncBase`` is an abstract base manager for vehicle network synchronization, driver tracking, DOTS-to-Mono vehicle conversion, and local state setup.

* **Driver Management:** Tracks driver GameObjects and network IDs in internal dictionaries (``vehicleDrivers``, ``vehicleDriverNetworkIds``).
* **Server Driver Assignment:** ``ServerTryAssignDriver`` converts AI traffic vehicles to player vehicles via ``EnterCar``, registers them in ``ArcadeVehicleNetworkBridge``, and assigns driver references.
* **Client Local Setup:** ``OnEnteredVehicleClient`` parents the player transform to the vehicle, hides visual mesh renderers via ``PlayerVisualController``, strips AI input components (``TrafficHybridInputControl``), and attaches ``PlayerInputVehicleControl`` for local players or sets ``Rigidbody.isKinematic = true`` for remote players.
* **Client Exit Setup:** ``OnExitedVehicleClient`` unparents the player transform, calculates safe exit offsets (``GetExitPosition``), restores visual state, and restores vehicle physics.
* **DOTS Entity Conversion:** ``DestroyTrafficComponents`` strips traffic ECS tags (``TrafficTag``, ``MonoAdapterComponent``, ``MonoAdapterCullStateComponent``) and reconfigures ``TrafficObstacleTag`` to treat the vehicle as a player obstacle.

Vehicle Input Synchronization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PlayerInputVehicleControl
^^^^^^^^^^^^^^^^^^^^^^^^^

``PlayerInputVehicleControl`` implements ``IVehicleInput`` to capture player input via ``VehicleInputProvider``. It reads move vectors and handbrake states from Unity Input System action maps.

VehicleInputSyncCore
^^^^^^^^^^^^^^^^^^^^

``VehicleInputSyncCore`` tracks vehicle inputs and filters transmissions using an epsilon threshold (``Epsilon = 0.01f``). It triggers ``OnInputChanged`` events only when throttle, steering, or handbrake states exceed the threshold, feeding both local and remote ``ArcadeVehicleController`` instances.

VehicleInputProvider
^^^^^^^^^^^^^^^^^^^^

``VehicleInputProvider`` is a singleton configuration component holding references to the global ``InputActionAsset``, action map names, and action names for vehicle control.

Client Culling Subsystem
~~~~~~~~~~~~~~~~~~~~~~~~

ClientCullInitializer
^^^^^^^^^^^^^^^^^^^^^

``ClientCullInitializer`` initializes client-side culling systems (such as ``InitCameraCullingSystem`` or ``CalcCullingSystem``) and spawns follower entities upon player connection. It attaches a ``CullPointFollower`` to track the player's position or camera transform in the ECS world.

CullPointCore
^^^^^^^^^^^^^

``CullPointCore`` samples local camera matrices (position, view, and projection) at configurable intervals (``sendInterval``). It dispatches ``OnCullDataSampled`` events on the client and updates or destroys corresponding server-side ECS culling entities (``CullPointTag``, ``CameraData``) upon network updates or disconnections.

CullPointFollower
^^^^^^^^^^^^^^^^^

``CullPointFollower`` is a utility component that synchronizes the position of an ECS culling entity (``cullEntity``) with a target Unity ``Transform`` during ``LateUpdate``.