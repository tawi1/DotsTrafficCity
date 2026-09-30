.. _fishnet:

FishNet
=======

This page covers the FishNet integration setup, configuration, and architectural details for the Mono Networking framework in DOTS City Sample.

Installation & Setup
--------------------

1. Download and import the `FishNet <https://assetstore.unity.com/packages/tools/network/fishnet-networking-evolved-207815>`_ package[cite: 73].
2. Add the ``CUSTOM_NETWORK`` scripting define in **Project Settings > Player > Scripting Define Symbols**[cite: 73].
3. Unpack the ``DotsCity/Packages/Upgrades/FishNetPrefabs`` package[cite: 73].
4. In the :ref:`Cull Config <cullConfig>`, set the calculation mode to **Multiplayer Calculate Distance** or **Multiplayer Camera View**[cite: 73].
5. Drag & drop ``FishnetPrefabRoot`` into the scene[cite: 73]. In that root, on the ``PrefabRootResolve`` component, click the **Resolve Refs** button (for new scenes)[cite: 73].
6. From the Unity toolbar, select ``Window > Multiplayer > Play Mode Tools``[cite: 73]. Ensure that **Play Mode Type** is set to ``Client & Server`` (if running a local simulation)[cite: 73].
7. Install the `Multiplayer Play Mode <https://docs.unity3d.com/Packages/com.unity.multiplayer.playmode@2.0/manual/index.html>`_ package to simulate multiple players locally *(optional)*[cite: 73].
8. Open the ``FishNetDemo`` scene to test the sample implementation[cite: 73].

   .. note:: 
      By default, only the ``FishNetDemo`` sample works out of the box with FishNet without extra setup[cite: 73].

Architecture & Component Breakdown
----------------------------------

The FishNet adapter bridges the transport-agnostic ``INetworkService`` and ``INetworkTransport`` interfaces with FishNet's native ``ServerManager``, ``ClientManager``, and ``IBroadcast`` messaging infrastructure[cite: 73]. 

Components are strictly categorized into player-level prefabs, vehicle-level prefabs, and global/scene services.

1. Player Components (Player Prefab Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These components are attached directly to the Player prefab, inherit from FishNet's ``NetworkBehaviour``[cite: 78, 79, 81], and manage local ownership, input processing, and client interactions:

* **FishNetPlayerMovementAdapter:** Attached alongside ``PlayerMovementCore`` and ``NetworkObject``[cite: 78]. Enables input and movement logic strictly on the owning client (``IsOwner``) while disabling simulation for non-owning remote proxies[cite: 78].
* **FishNetPlayerRpcTransport:** Implements ``IPlayerRpcTransport`` and ``INetworkBehaviour``[cite: 79]. Handles vehicle entry and exit requests sent via ``[ServerRpc]`` (``ServerCmdRequestEnter``, ``ServerCmdRequestExit``) and broadcasts interactions globally via ``[ObserversRpc]`` (``RpcOnEnteredVehicle``, ``RpcOnExitedVehicle``)[cite: 79].
* **FishNetPlayerSpawnNotifier:** Manages client lifecycle hooks (``OnStartClient``, ``OnStopClient``), registers the player instance in the global ``PlayerRegistry`` using ``OwnerId``, and notifies ``PlayerSpawnerBase`` when local instantiation completes[cite: 81].
* **FishNetCullPointAdapter:** Attached alongside ``CullPointCore`` and ``NetworkObject``[cite: 76]. Captures local camera view matrices and transmits them to the server via ``[ServerRpc]`` (``SubmitCullPointServerRpc``) for server-side ECS interest management, handling cleanup upon client despawn[cite: 76].

2. Vehicle Components (Vehicle Prefab Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These components are attached directly to synchronized Vehicle prefabs to manage network ownership, synchronization variables, and driver inputs:

* **FishNetNetworkVehicleObserver:** Attached to vehicle prefabs alongside ``NetworkObject``[cite: 77]. Implements ``INetworkVehicleObserver``[cite: 77], synchronizes unique vehicle IDs via ``SyncVar<int>``[cite: 77], and triggers client-side spawn/despawn hooks in ``MonoVehicleNetworkSyncBase``[cite: 77].
* **FishNetVehicleInputSyncAdapter:** Attached to controllable vehicles alongside ``VehicleInputSyncCore`` and ``NetworkObject``[cite: 82]. Propagates vehicle throttle, steering, and handbrake inputs across the network using ``SyncVar`` fields updated via owner ``[ServerRpc]``[cite: 82].
* **FishNetVehicleNetworkSync:** Inherits from ``MonoVehicleNetworkSyncBase``[cite: 83]. Manages server-side driver assignment, physics toggles, and network ownership delegation (using ``GiveOwnership`` or spawning unspawned network objects) when players enter or exit vehicles[cite: 83].

3. Global & Scene Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **FishNetProviderSO:** ScriptableObject strategy extending ``NetworkProviderSO``[cite: 73]. Resolves global ``InstanceFinder.NetworkManager``, instantiates ``FishNetTransport``, registers custom payload serializers, and sets up the pedestrian broadcaster[cite: 73].
* **FishNetPlayerSpawnerSO:** ScriptableObject extending ``NetworkPlayerSpawnerSO``[cite: 80]. Executes server-side player instantiation via FishNet's ``ServerManager.Spawn()`` with assigned connection ownership[cite: 80].
* **FishNetTransport:** Low-level transport bridge implementing ``INetworkTransport``[cite: 73]. Maps connection state events and routes broadcasts via ``BroadcastInvoker<T>``[cite: 73].
* **FishNetMessageRegistry:** Central binder connecting data payloads to FishNet ``IBroadcast`` wrappers inside ``UniversalNetworkService``[cite: 73].
* **FishNetIdentityWrapper & FishNetBehaviourWrapper:** Framework wrappers implementing ``INetworkIdentity`` and ``INetworkBehaviour`` over FishNet's ``NetworkObject``[cite: 73].

Data Payloads & Custom Serialization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Custom Serializers:**
  
  * ``VehicleSnapshotSerializers``: Provides custom extension methods for FishNet ``Writer`` and ``Reader`` to efficiently serialize individual ``VehicleSnapshot`` structures and zero-allocation ``ArraySegment<VehicleSnapshot>`` buffers[cite: 74].
  * ``PedestrianSerializers``: Serializes pedestrian lifecycle broadcasts (initial states, requests, transforms, animations, and ragdoll sync)[cite: 73].

* **Broadcast Wrappers:** Structs implementing ``IBroadcast`` (e.g., ``FishNetTrafficLightBroadcast``, ``VehicleSpawnDataWrapper``, ``VehicleDespawnDataWrapper``, ``PedestrianSpawnBroadcastWrapper``)[cite: 73, 75].