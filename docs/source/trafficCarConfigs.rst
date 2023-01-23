.. _trafficCarConfigs:

Traffic Car Configs
=====

Traffic Car Spawner Config
------------

``Single mode is used to position single objects.``

	.. image:: /images/configs/traffic/TrafficCarSpawnerConfig.png
	
| **Preferable count** : maximum number of cars in the city.
| **HashMap capacity** : initial capacity of the hashmap that contains the data of the traffic cars.
| **Max spawn count by iteration** : maximum number of cars that will be spawned in one iteration.
| **Max parking cars** : maximum number of parked in the city.
| **Min/Max spawn delay** : minimum/maximum duration between spawns.
| **Min spawn distance** : minimum distance for spawning between cars.
	
.. _trafficCarSettings:
	
Traffic Car Settings
------------

``Single mode is used to position single objects.``

	.. image:: /images/configs/traffic/TrafficCarSettingsConfig.png
	

	
**Entity type:**
	* **Hybrid cube entity simple physics**
	* **Hybrid entity full physics** : :ref:`hybrid entities<entityType>` moved by the custom physical system (for example `VehicleMechanics <https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/PhysicsSamples/Assets/Demos/6.%20Use%20Cases/6d.%20Raycast%20Car/Scripts/VehicleMechanics.cs>`_)  
	* **Pure entity full physics** : :ref:`pure entities<entityType>` moved by the custom physical system (for example `VehicleMechanics <https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/PhysicsSamples/Assets/Demos/6.%20Use%20Cases/6d.%20Raycast%20Car/Scripts/VehicleMechanics.cs>`_)  
	* **Pure entity simple physics** : :ref:`pure entities<entityType>` moved by the simple physical system (simply adding physics velocity to the physics body).
	* **Pure entity no physics** : :ref:`pure entities<entityType>` that moved by tranform system without physics.
	
.. _entityType:

	.. note::
		| **Hybrid entity** : entities that combine `DOTS` entities and default `GameObjects` (game objects are tied by position to an entity).
		| **Pure entity** : entities work entirely in the `DOTS` space.
	
.. _trafficDetectObstacleMode:

**Traffic car detect obstacle mode:**
	* **Hybrid** : combine types `Calculate` and `Raycast`.
	* **Calculate only** : mathematically calculates the obstacle.
	* **Raycast only** : detect obstacle by raycast.
	
	.. note::
		In `Hybrid mode`, raycast is activated only when the selected targets are close to the car.
	
**Traffic car detect npc mode:**
	* **Disabled**
	* **Calculate** : mathematically calculates the npc.
	* **Raycast** : detect obstacle by raycast (npc should have `PhysicsShape` component).
	
**Traffic car simple physics type:**
	* **Car input** :
	* **Follow target** :
	
| **Default lane speed km/h** : default lane speed (if the lane speed limit is set to 0 the default speed will be selected).
| **Max car speed km/h** : maximum speed of the car.
| **Acceleration magnitude** : vehicle acceleration speed.
| **Backward acceleration magnitude** : backward vehicle acceleration speed.
| **Brake power** : brake power.
| **Max steer angle** : max steer angle of the wheels.
| **Steering damping** : wheel turn speed.
| **Health amount** : amount of hit points of the car (health systems should be enabled).
**Has rotation lerp** : [for `Simple physics` and `No physics` only]
	* **Rotation speed** : vehicle rotation speed.
	* **Rotation speed curve** : curve on the dependence of the speed of the car on its speed.
	
| **Cull wheels** : on/off wheel handling if they are outside the camera.
| **Has nav obstacle** :
	
Traffic Car Nav Config
------------

Config distance to target nodes and traffic light handlers.

	.. image:: /images/configs/traffic/TrafficCarNavConfigConfig.png
	
| **Min distance to target** : min distance to target :ref:`TrafficNode<trafficNode>`.
| **Min distance to path point target** : min distance to connected :ref:`path point<pathPointConnection>`.
| **Min distance to new light** : minimum distance to the :ref:`TrafficNode<trafficNode>` entity that contains the :ref:`traffic light handler<trafficLightHandler>` entity to assign it to the car entity (if the traffic node entity does not contain a traffic light entity, the index is -1).
| **Min distance from previous light** : minimum distance from the :ref:`TrafficNode<trafficNode>` entity that contains the :ref:`traffic light handler<trafficLightHandler>` entity to unassign it from the car entity (if the traffic node entity does not contain a traffic light entity, the index is -1).
| **Min distance to target route node** : minimum distance to switch to the next waypoint of the :ref:`path<path>`.
| **Min distance to target rail route node** : minimum distance to switch to the next waypoint of the :ref:`path<path>` (rail movement only (tramc etc...)).
**Out of path resolve method:** resolving method in case the car is out of the :ref:`path<path>`.
	* **Disabled** : no actions.
	* **Switch node** : switching to the next waypoint.
	* **Backward** : car will try to reach the missed waypoint by reversing.
	* **Cull** : car will be culled.
| **Continious local node calculation** :

	.. image:: /images/configs/traffic/TrafficCarNavOutOfPathConfig.png
	
**Out of path resolve method [enabled]:**
	* **Min distance to out of path** : minimum distance from the missed waypoint to the car.
	* **Max distance to out of path** : maximum distance from the missed waypoint to the car.
	
Traffic Car Obstacle Config
------------

Config to calculate obstacles on the path.

	.. image:: /images/configs/traffic/TrafficCarNavConfigConfig.png
	
| **Max distance to obstacle** : minimum distance to an obstacle (:ref:`example<trafficCarObstacleConfig1>`).
| **Min distance to start approach** : minimum distance to the last car in the current lane to start approaching (stay at the same speed as the target car) (:ref:`example<trafficCarObstacleConfig2>`).
| **Min distance to check next connected path** : minimum distance to check the next path for obstacles (:ref:`example<trafficCarObstacleConfig3>`).
| **Short path length** : if the next path is too short, start checking the next connected paths for obstacles (:ref:`example<trafficCarObstacleConfig4>`).
| **Calculate distance to intersect point** : distance to intersected paths when they are checked for obstacles (:ref:`example<trafficCarObstacleConfig5>`).

**Obstacle intersect calculation method:** method of calculating the intersection of the vehicle and the intersect point.
	* **Distance** : distance between car and intersect point.
	* **Bounds** : calculate intersect point that inside the car bounds.
	
| **Size offset to intersect point** : additional offset to the length of the car bounds to check the closeness to the intersect point.
| **Close enough distance to stop before intersect point** : car is close enough to stop in front of the intersect point if necessary (:ref:`example<trafficCarObstacleConfig5>`).
| **Close enough distance to stop before intersect same target node** : current car is close enough to stop in front if another car approaches the same target node but with a higher priority (:ref:`example<trafficCarObstacleConfig6>`).
| **Close distance to change lane point** : car that is too close to the lane change point is always an obstacle (:ref:`example<trafficCarObstacleConfig7>`).
| **Max distance to obstacle change lane** : (:ref:`example<trafficCarObstacleConfig8>`).
| **Same direction value** : direction of the vehicle to check for obstacles in neighboring paths (paths that start from the same point)(:ref:`example<trafficCarObstacleConfig9>`).
| **Avoid crossroad jam** : car doesn't enter an crossroad if it cannot pass it without jamming (:ref:`example<trafficCarObstacleConfig10>`).
	
	.. note:: 
		**How to calculate the parameters regarding the size of the vehicle hull:**
			* Select the mesh renderer of the vehicle hull and insert to the `Target Car Mesh` field.
			* Press `Recalculate` button.
			* On the traffic test scene, calibrate the parameters depending on your needs.
			
**Parameter visualization:**

.. _trafficCarObstacleConfig1:

	.. image:: /images/configs/traffic/obstacleExamples/ObstacleDistanceExample1.png
	`Obstacle distance example.`
	
.. _trafficCarObstacleConfig2:

	.. image:: /images/configs/traffic/obstacleExamples/ApproachDistanceExample1.png
	`Approach distance example.`
	
.. _trafficCarObstacleConfig3:

	.. image:: /images/configs/traffic/obstacleExamples/MinDistanceToCheckNextConnectedPathExample.png
	`Min distance to check next ConnectedPath example.`
	
.. _trafficCarObstacleConfig4:

	.. image:: /images/configs/traffic/obstacleExamples/CheckShortPathExample.png
	`Short path example.`
	
.. _trafficCarObstacleConfig5:

	.. image:: /images/configs/traffic/obstacleExamples/CalculateDistanceToIntersectExample1.png
	`Calculate distance to intersect example.`
	
.. _trafficCarObstacleConfig6:

	.. image:: /images/configs/traffic/obstacleExamples/CalculateDistanceToIntersectSameTargetExample1.png
	`Calculate distance to intersect same target example.`
	
.. _trafficCarObstacleConfig7:

	.. image:: /images/configs/traffic/obstacleExamples/ChangeLaneCloseDistanceExample.png
	`Change lane close distance to point example.`
	
.. _trafficCarObstacleConfig8:
	.. image:: /images/configs/traffic/obstacleExamples/ChangeLaneExample1.png
	
	.. image:: /images/configs/traffic/obstacleExamples/ChangeLaneExample3.png
	`Short path example.`
	
.. _trafficCarObstacleConfig9:

	.. image:: /images/configs/traffic/obstacleExamples/SameDirectionExample.png
	`Same direction example.`
	
.. _trafficCarObstacleConfig10:

	.. image:: /images/configs/traffic/obstacleExamples/AvoidCrossroadJamExample.png
	`Avoid crossroad jam example.`

			
Traffic Car Approach Config
------------

Config of approaching obstacles and lights.

	.. image:: /images/configs/traffic/TrafficCarApproachConfig.png
	
| **Min approach speed** : min approach speed.
| **On coming to the red light speed** : slowing down the speed of the car when approaching a red light (if the segment speed limit is lower or the speed of the obstacles is lower, the lowest speed of all the conditions will be selected).
| **Stopping distance to light** : distance at which the car slows down.
	
Traffic Car Raycast Config
------------

Traffic car raycast Config (:ref:`TrafficDetectObstacleMode<trafficDetectObstacleMode>` raycast or hybrid should be enabled) (:ref:`example<trafficCarNpcObstacleDebugger>`).

	.. image:: /images/configs/traffic/TrafficCarRaycastConfig.png
	
| **Side offset** : width of raycast box.
| **Min/Max ray length** : lenght of raycast box.
| **Boxcast height** : height raycast box.
| **Ray Y axis offset** : y-offset position box.
| **Dot direction** : if the raycast is set to :ref:`Hybrid mode<trafficDetectObstacleMode>` than only those targets that are in front of the car with the set dot parameter will be raycasted.
| **Bounds multiplier** : value by which the bounds is multiplied.
	
Traffic Car Change Lane Config
------------

Config for automatic calculation of lane change by traffic (works for :ref:`paths<path>` with the `Straight road` :ref:`road type<pathRoadType>` only).

	.. image:: /images/configs/traffic/TrafficCarChangeLaneConfig.png
	
| **Can change lane** : on/off ability to change lanes.
| **Min max change lane offset** : min/max offset in the target lane depending on the speed of the car. (:ref:`example<trafficCarChangeLaneConfig1>`)
| **Max distance to end of path** : maximum distance before the end of a current path at which car can change lanes.
| **Min distance to last car in current lane** : minimum distance to the last car in the current lane. (:ref:`example<trafficCarChangeLaneConfig2>`)
| **Min Max distance to other cars in other lane** : distance to the car in the target lane, the distance is chosen based on the current speed of the calculated car (lerp between 0 speed and max speed of the car (60 km/h by default)) (:ref:`example<trafficCarChangeLaneConfig3>`)
| **Max distance to intersected path** : distance to the crossing, if the car is close to the crossing, the ability to change lanes is disabled. (:ref:`example<trafficCarChangeLaneConfig4>`)
| **Check frequency** : frequency of lane change calculation.
| **Block duration after change lane** : blocking the ability to change lanes after a lane change has been performed.
| **Achieve distance** : distance to achieve the target lane point.
| **Min car count in current lane to change lane** : minimum number of cars in the current lane to change lanes.
| **Min car lane difference count to start change lane** : minimum car difference in the nearest lane to change lanes.
| **Change lane car speed** : lane change speed.
| **Change lane HashMap capacity** : initial capacity hashmap containing data about cars that change lanes.

**Parameter visualization:**

.. _trafficCarChangeLaneConfig1:
	
	.. image:: /images/configs/traffic/changeLaneExamples/MinMaxChangeLaneOffsetExample.png
	`Min/max change lane offset example.`
	
.. _trafficCarChangeLaneConfig2:

	.. image:: /images/configs/traffic/changeLaneExamples/MinDistanceToLastCarExample.png
	`Min distance to last car in current lane example.`
	
.. _trafficCarChangeLaneConfig3:
		
	.. image:: /images/configs/traffic/changeLaneExamples/MinDistanceToOtherCarsInOtherLaneExample.png
	`Min distance to other cars in other lane example.`
	
.. _trafficCarChangeLaneConfig4:
	
	.. image:: /images/configs/traffic/changeLaneExamples/MinDistanceToIntersectedPathExample.png
	`Min distance to intersected path example.`
	
Traffic Car Npc Obstacle Config
------------

Config to calculate npc obstacles (:ref:`example<trafficCarNpcObstacleDebugger>`).

	.. image:: /images/configs/traffic/TrafficCarNpcObstacleConfig.png
	
| **Obstacle pedestrian action state** : will only react to pedestrians with the selected :ref:`PedestrianActionState<pedestrianActionState>`.
| **Check distance** : obstacle calculation length.
| **Square length** : length of the obstacle calculation square.
| **Side offset X** : width of the obstacle calculation square.
| **Max Y diff** : maximum difference in Y-axis position between the car and the npc.
	
Traffic Car Parking Config
------------

	.. image:: /images/configs/traffic/TrafficCarParkingConfig.png

**Rotation aligment at node support** : on/off car automatically turns in alignment with the parking node.
	**Rotation speed** : rotation speed.
	**Complete angle** : angle at which the rotation is complete.
		
.. _trafficCarAntistuckConfig:
		
Traffic Car Antistuck Config
------------

Config to culling car in case of stuckness.

	.. image:: /images/configs/traffic/TrafficCarAntistuckConfig.png

| **Obstacle stuck time** : duration of sighting of the obstacle after which the car will be culled.
| **Stuck distance difference** : if the car moved more than the parameter distance the `Obstacle stuck time` is reset.
| **Cull of out the camera only** : car will be culled only if it is out of the camera's range of vision.
	
Traffic Car Horn Config
------------

Config to sound random horns when an obstacle is detected. It can be disabled (:ref:`here<soundConfig>`).

	.. image:: /images/configs/traffic/TrafficCarHornConfig.png

| **Chance to start** : chance to start the horn.
| **Idle time to start** : idle time to start the horn.
| **Delay** : delay between horns.
| **Horn duration** : horn duration.