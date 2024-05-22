.. _layerInfo

Layer Info
=====

* By default, the layers are stored in the `ProjectConstants.cs` script file. 
* The project uses the following layers:

Road Layers
~~~~~~~~~~~~

* **TrafficNode [20]** : :ref:`TrafficNode <trafficNode>` layer. 
* **PedestrianNode [21]** : :ref:`PedestrianNode <pedestrianNode>` layer. 

Object Layers
~~~~~~~~~~~~

* **Ground [18]** : ground surface layer.
* **Ragdoll [19]** : :ref:`ragdoll <pedestrianRagdoll>` colider layer. 
* **StaticPhysicsShape [22]** : :ref:`Static object <physicsShapeTransfer>` layer collider layer (e.g. house, fence). 
* **Chunk [23]** : layer of :ref:`streaming <sceneStreaming>` 3D chunks in the chunk subscenes created by :ref:`SubsceneChunkCreator <subSceneCreator>` tool. 
* **Props [24]** :  collider layer of :ref:`props <propsInfo>` (e.g. traffic light, hydrant, mailbox). 
* **Combined [25]** : layer of combined meshes into the one by 3rd party combining tool.  

Misc Layers
~~~~~~~~~~~~
		
* **Npc [3]** : :ref:`Player <playerNpc>` & custom NPCs layer.
* **SyncPlayer [13]** : layer of the player's car when using :ref:`Hybrid Mono <playerHybridMono>` for the player.
* **PlayerCar [14]** : :ref:`Player car <playerCar>` layer layer. 
* **PoliceCar [15]** : Police car layer. 
* **TraficCar [16]** : :ref:`Traffic car  <trafficCar>` layer.
* **TriggerLayer [26]** : collider trigger player layer.
