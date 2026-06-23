.. _layerInfo:

Layer Info
=====

* By default, the layers are stored in the `ProjectConstants.cs` script file. 
* The project uses the following layers:

Road Layers
~~~~~~~~~~~~

* **TrafficNode [20]** : :ref:`TrafficNode <trafficNode>` layer is used for `TrafficNode` prefab **[required]**. 

Object Layers
~~~~~~~~~~~~

* **Ground [18]** : ground surface layer, but you can use any custom ground layer you want if you set it in the `Traffic` cars for ground detection. *[optional]*
* **StaticPhysicsShape [22]** : :ref:`Static object <physicsShapeTransfer>` layer collider layer (e.g. house, fence). *[optional, only used for DOTS scenes]* 
* **Props [23]** :  collider layer of :ref:`props <propsInfo>` (e.g. traffic light, hydrant, mailbox). *[optional]*

Misc Layers
~~~~~~~~~~~~
		
* **Traffic [16]** : :ref:`Traffic car  <trafficCar>` layer. *[demo scene only, optional]*