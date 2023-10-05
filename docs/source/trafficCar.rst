.. _trafficCar:
   
Traffic Car
=====

.. contents::
   :local:
   
How To Create
----------------

#. Create vehicle using the :ref:`Car Prefab Creator <carPrefabCreator>` tool (for example :ref:`Simple physics entity <entityType>` type).

	.. image:: /images/entities/trafficCar/howTo/Step1.png
	:ref:`Car Prefab Creator <carPrefabCreator>` tool example.
	
#. Make sure, that the :ref:`vehicle collection <vehicleCollection>` contains the created vehicle.

	.. image:: /images/entities/trafficCar/howTo/Step2.png
	
#. Make sure, that the :ref:`preset <trafficPreset>` contains the vehicle.

	.. image:: /images/entities/trafficCar/howTo/Step3.png

#. Open :ref:`Traffic settings <trafficCarSettings>` and select :ref:`Simple physics entity <entityType>` type.

	.. image:: /images/entities/trafficCar/howTo/Step4.png
	
#. Open :ref:`Hub <roadEntitySubscene>` object on the scene and press `Copy To Subscene` button.

	.. image:: /images/entities/trafficCar/howTo/Step5.png
	
#. Open `EntitySubScene`, find `TrafficCarEntityPoolBakerRef` gameobject, make sure the correct :ref:`preset <trafficPreset>` is assigned.

	.. image:: /images/entities/trafficCar/howTo/Step6.png
	
#. Adjust traffic settings.
	* For :ref:`simple physics <trafficCarSettings>`.
	* For :ref:`custom physics <trafficCarSettings>`. 

Common Info
----------------

Obstacle Info
~~~~~~~~~~~~

.. _trafficCarRaycastInfo:

Raycast
""""""""""""""

:ref:`Config. <trafficCarRaycastConfig>`

Modes:
	* `Hybrid mode` : raycast is activated only when the selected targets are close to the car.
	* `Raycast only` : raycasts are sent constantly.
	
To define raycast targets for `Hybrid` or `Raycast only` modes, redefine the `GetTargetQuery` method in the ``TrafficCarRaycastObstacleTargetQueryProvider`` class, which returns the `EntityQuery <https://docs.unity.cn/Packages/com.unity.entities@1.0/api/Unity.Entities.EntityQuery.html>`_ of the targets.

..  code-block:: r

	public static EntityQuery GetTargetQuery(
			   SystemBase sourceSystem,
			   TrafficCarDetectObstacleMode trafficCarDetectObstacleMode,
			   TrafficCarDetectNpcMode trafficCarDetectNpcMode,
			   out CollisionFilter tempRaycastCollisionFilter,
			   out CollisionFilter raycastAlwaysCollisionFilter);
		
* :ref:`TrafficCarDetectObstacleMode. <trafficDetectObstacleMode>`
* :ref:`TrafficCarDetectNpcMode. <trafficDetectObstacleMode>`
* **Temp raycast CollisionFilter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of hybrid raycast mode.
* **Raycast always CollisionFilter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of raycast only mode.
		
	.. note:: You can also dynamically change the raycast target by adding or removing the `TrafficCustomRaycastTargetTag` component.

Authoring components
----------------

.. _trafficCarEntityAuthoring:

TrafficCarEntityAuthoring
~~~~~~~~~~~~
	
	.. image:: /images/entities/trafficCar/TrafficCarEntityAuthoring.png
	
| **Hull mesh renderer** : vehicle hull mesh renderer reference.
| **Physics shape** : vehicle entity `PhysicsShape` reference.
| **Faction type** : selected :ref:`faction type <factions>` of vehicle.
| **Car type** : selected :ref:`car type <carType>` of vehicle.
| **Bounds source type** : selected bounds source for the entity bounds.
| **Traffic group** : selected :ref:`traffic group <pathTrafficGroup>`.

Shared Settings
~~~~~~~~~~~~

Each vehicle has a common set of settings that are described :ref:`here <vehicleCollection>`
		
CarWheelAuthoring
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/CarWheelAuthoring.png
	
| **Wheel base** : wheel radius.
| **All wheels** : all wheels of the vehicle.
| **Steering wheels** : wheels that can turn.

	.. note:: Simple vehicles only.

		
PhysicsShape & PhysicsBody
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/PhysicsBody.png

Optional components if the car moves with physics.