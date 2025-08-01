.. _layerInfo:

Layer Info
=====

* By default, the layers are stored in the `ProjectConstants.cs` script file. 
* The project uses the following layers:

Road Layers
~~~~~~~~~~~~

* **TrafficNode [20]** : :ref:`TrafficNode <trafficNode>` layer is used for `TrafficNode` prefab **[required]**. 
* **PedestrianNode [21]** : :ref:`PedestrianNode <pedestrianNode>` layer is used for `PedestrianNode` prefab **[required]**. 

Object Layers
~~~~~~~~~~~~

* **Ground [18]** : ground surface layer, but you can use any custom ground layer you want if you set it in the `Traffic` cars for ground detection. *[optional]*
* **Ragdoll [19]** : :ref:`ragdoll <pedestrianRagdoll>` collider layer. *[optional]*
* **StaticPhysicsShape [22]** : :ref:`Static object <physicsShapeTransfer>` layer collider layer (e.g. house, fence). *[optional, only used for DOTS scenes]* 
* **Chunk [23]** : layer of :ref:`streaming <sceneStreaming>` 3D chunks in the chunk subscenes created by :ref:`SubsceneChunkCreator <subSceneCreator>` tool. *[optional, only used for DOTS scenes]*
* **Props [24]** :  collider layer of :ref:`props <propsInfo>` (e.g. traffic light, hydrant, mailbox). *[optional]*
* **Combined [25]** : layer of combined meshes into the one by 3rd party combining tool *(demo scene only)*. *[optional]*

Misc Layers
~~~~~~~~~~~~
		
* **CollidableNpc [15]** : player npc layer. *[demo scene built-in player, optional]*
* **TraficCar [16]** : :ref:`Traffic car  <trafficCar>` layer. *[demo scene only, optional]*
* **Npc [17]** : :ref:`Pedestrian <pedestrianEntity>` npc layer. *[demo scene only, optional]*
