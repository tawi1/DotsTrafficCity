.. _layerInfo:

Layer Info
=====

* By default, the layers are stored in the `ProjectConstants.cs` script file. 
* The project uses the following layers:

Road Layers
~~~~~~~~~~~~

* **TrafficNode [20]** : :ref:`TrafficNode <trafficNode>` layer **[required]**. 
* **PedestrianNode [21]** : :ref:`PedestrianNode <pedestrianNode>` layer **[required]**. 

Object Layers
~~~~~~~~~~~~

* **Ground [18]** : ground surface layer.
* **Ragdoll [19]** : :ref:`ragdoll <pedestrianRagdoll>` colider layer. 
* **StaticPhysicsShape [22]** : :ref:`Static object <physicsShapeTransfer>` layer collider layer (e.g. house, fence). 
* **Chunk [23]** : layer of :ref:`streaming <sceneStreaming>` 3D chunks in the chunk subscenes created by :ref:`SubsceneChunkCreator <subSceneCreator>` tool. 
* **Props [24]** :  collider layer of :ref:`props <propsInfo>` (e.g. traffic light, hydrant, mailbox). 
* **Combined [25]** : layer of combined meshes into the one by 3rd party combining tool *(demo scene only)*.  

Misc Layers
~~~~~~~~~~~~
		
* **CollidableNpc [15]** : player npc layer. 
* **TraficCar [16]** : :ref:`Traffic car  <trafficCar>` layer.
* **Npc [17]** : :ref:`Pedestrian <pedestrianEntity>` npc layer.
