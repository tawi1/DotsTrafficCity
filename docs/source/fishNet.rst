.. _fishnet:

FishNet
=======

This page covers the FishNet integration setup, configuration, and architectural details for the Mono Networking framework in DOTS City Sample.

Installation & Setup
--------------------

1. Download and import the `FishNet <https://assetstore.unity.com/packages/tools/network/fishnet-networking-evolved-207815>`_ package.
2. Add the ``CUSTOM_NETWORK`` scripting define in **Project Settings > Player > Scripting Define Symbols**.
3. Unpack the ``DotsCity/Packages/Upgrades/FishNetPrefabs`` package.
4. In the :ref:`Cull Config <cullConfig>`, set the calculation mode to **Multiplayer Calculate Distance** or **Multiplayer Camera View**.
5. Drag & drop ``FishnetPrefabRoot`` into the scene. In that root, on the ``PrefabRootResolve`` component, click the **Resolve Refs** button (for new scenes).
7. Install the `Multiplayer Play Mode <https://docs.unity3d.com/Packages/com.unity.multiplayer.playmode@2.0/manual/index.html>`_ package to simulate multiple players locally *(optional)*.
8. Open the ``FishNetDemo`` scene to test the sample implementation.

   .. note:: 
      By default, only the ``FishNetDemo`` sample works out of the box with FishNet without extra setup.

Architecture & Component Breakdown
----------------------------------

The FishNet adapter bridges the transport-agnostic ``INetworkService`` and ``INetworkTransport`` interfaces with FishNet's native ``ServerManager``, ``ClientManager``, and ``IBroadcast`` messaging infrastructure. 

Components are strictly categorized into player-level prefabs, vehicle-level prefabs, and global/scene services.

1. Player Components (Player Prefab Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These components are attached directly to the Player prefab, inherit from FishNet's ``NetworkBehaviour``, and manage local ownership, input processing, and client interactions:

* **FishNetPlayerMovementAdapter:** Attached alongside ``PlayerMovementCore`` and ``NetworkObject``. Enables input and movement logic strictly on the owning client (``IsOwner``) while disabling simulation for non-owning remote proxies.
* **FishNetPlayerRpcTransport:** Implements ``IPlayerRpcTransport`` and ``INetworkBehaviour``. Handles vehicle entry and exit requests sent via ``[ServerRpc]`` (``ServerCmdRequestEnter``, ``ServerCmdRequestExit``) and broadcasts interactions globally via ``[ObserversRpc]`` (``RpcOnEnteredVehicle``, ``RpcOnExitedVehicle``).
* **FishNetPlayerSpawnNotifier:** Manages client lifecycle hooks (``OnStartClient``, ``OnStopClient``), registers the player instance in the global ``PlayerRegistry`` using ``OwnerId``, and notifies ``PlayerSpawnerBase`` when local instantiation completes.
* **FishNetCullPointAdapter:** Attached alongside ``CullPointCore`` and ``NetworkObject``. Captures local camera view matrices and transmits them to the server via ``[ServerRpc]`` (``SubmitCullPointServerRpc``) for server-side ECS interest management, handling cleanup upon client despawn.

2. Vehicle Components (Vehicle Prefab Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These components are attached directly to synchronized Vehicle prefabs to manage network ownership, synchronization variables, and driver inputs:

* **FishNetNetworkVehicleObserver:** Attached to vehicle prefabs alongside ``NetworkObject``. Implements ``INetworkVehicleObserver``, synchronizes unique vehicle IDs via ``SyncVar<int>``, and triggers client-side spawn/despawn hooks in ``MonoVehicleNetworkSyncBase``.
* **FishNetVehicleInputSyncAdapter:** Attached to controllable vehicles alongside ``VehicleInputSyncCore`` and ``NetworkObject``. Propagates vehicle throttle, steering, and handbrake inputs across the network using ``SyncVar`` fields updated via owner ``[ServerRpc]``.
* **FishNetVehicleNetworkSync:** Inherits from ``MonoVehicleNetworkSyncBase``. Manages server-side driver assignment, physics toggles, and network ownership delegation (using ``GiveOwnership`` or spawning unspawned network objects) when players enter or exit vehicles.

3. Global & Scene Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **FishNetProviderSO:** ScriptableObject strategy extending ``NetworkProviderSO``. Resolves global ``InstanceFinder.NetworkManager``, instantiates ``FishNetTransport``, registers custom payload serializers, and sets up the pedestrian broadcaster.
* **FishNetPlayerSpawnerSO:** ScriptableObject extending ``NetworkPlayerSpawnerSO``. Executes server-side player instantiation via FishNet's ``ServerManager.Spawn()`` with assigned connection ownership.
* **FishNetTransport:** Low-level transport bridge implementing ``INetworkTransport``. Maps connection state events and routes broadcasts via ``BroadcastInvoker<T>``.
* **FishNetMessageRegistry:** Central binder connecting data payloads to FishNet ``IBroadcast`` wrappers inside ``UniversalNetworkService``.
* **FishNetIdentityWrapper & FishNetBehaviourWrapper:** Framework wrappers implementing ``INetworkIdentity`` and ``INetworkBehaviour`` over FishNet's ``NetworkObject``.

Data Payloads & Custom Serialization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Custom Serializers:**
  
  * ``VehicleSnapshotSerializers``: Provides custom extension methods for FishNet ``Writer`` and ``Reader`` to efficiently serialize individual ``VehicleSnapshot`` structures and zero-allocation ``ArraySegment<VehicleSnapshot>`` buffers.
  * ``PedestrianSerializers``: Serializes pedestrian lifecycle broadcasts (initial states, requests, transforms, animations, and ragdoll sync).

* **Broadcast Wrappers:** Structs implementing ``IBroadcast`` (e.g., ``FishNetTrafficLightBroadcast``, ``VehicleSpawnDataWrapper``, ``VehicleDespawnDataWrapper``, ``PedestrianSpawnBroadcastWrapper``).