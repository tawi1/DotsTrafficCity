.. _trafficCarConfigs:

Traffic Configs
=====

Traffic Car Spawner Config
------------

``Single mode is used to position single objects.``

	.. image:: images/configs/traffic/TrafficCarSpawnerConfig.png
	
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

	.. image:: images/configs/traffic/TrafficCarSettingsConfig.png
	
**Entity type:**
	* **Hybrid cube entity simple physics** :
	* **Hybrid entity full physics** :
	* **Pure entity full physics** :
	* **Pure entity simple physics** :
	* **Pure entity no physics** :
	
**Traffic car detect obstacle mode:**
	* **Hybrid** : combine types `Calculate` and `Raycast`.
	* **Calculate only** : mathematically calculates the obstacle.
	* **Raycast only** : detect obstacle by raycast.
	
**Traffic car detect npc mode:**
	* **Disabled** :
	* **Calculate** : mathematically calculates the npc.
	* **Raycast** : detect obstacle by raycast (npc should have `PhysicsShape` component).
	
**Traffic car simple physics type:**
	* **Car input** :
	* **Follow target** :
	
| **Default lane speed km/h** :
| **Max car speed km/h** :
| **Acceleration magnitude** :
| **Backward acceleration magnitude** :
| **Brake power** :
| **Max steer angle** :
| **Steering damping** :
| **Health amount** :
**Has rotation lerp** :
	**Rotation speed** :
	**Rotation speed curve** :
	
| **Cull wheels** :
| **Has nav obstacle** :
	
Traffic Car Nav Config
------------

	.. image:: images/configs/traffic/TrafficCarNavConfigConfig.png
	
| **Min distance to target** :
| **Min distance to path point target** :
| **Min distance to new light** :
| **Min distance from previous light** :
| **Min distance to target route node** :
| **Min distance to target rail route node** :
**Out of path resolve method:** 
	**Disabled** : 
	**Switch node** : 
	**Backward** : 
	**Cull** : 
| **Continious local node calculation** :
	
Traffic Car Obstacle Config
------------

	.. image:: images/configs/traffic/TrafficCarNavConfigConfig.png
	
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
| **Same direction value** : direction of the vehicle to check for obstacles in neighboring paths (:ref:`example<trafficCarObstacleConfig9>`).
| **Avoid crossroad jam** : car doesn't enter an crossroad if it cannot pass it without jamming (:ref:`example<trafficCarObstacleConfig10>`).
	
	.. note:: 
		**How to calculate the parameters regarding the size of the vehicle hull:**
			* Select the mesh renderer of the vehicle hull and insert to the `Target Car Mesh` field.
			* Press `Recalculate` button.
			* On the traffic test scene, calibrate the parameters depending on your needs.
			
**Parameter visualization:**

.. _trafficCarObstacleConfig1:

	.. image:: images/configs/traffic/obstacleExamples/ObstacleDistanceExample1.png
	`Obstacle distance example.`
	
.. _trafficCarObstacleConfig2:

	.. image:: images/configs/traffic/obstacleExamples/ApproachDistanceExample1.png
	`Approach distance example.`
	
.. _trafficCarObstacleConfig3:

	.. image:: images/configs/traffic/obstacleExamples/MinDistanceToCheckNextConnectedPathExample.png
	`Min distance to check next ConnectedPath example.`
	
.. _trafficCarObstacleConfig4:

	.. image:: images/configs/traffic/obstacleExamples/CheckShortPathExample.png
	`Short path example.`
	
.. _trafficCarObstacleConfig5:

	.. image:: images/configs/traffic/obstacleExamples/CalculateDistanceToIntersectExample1.png
	`Calculate distance to intersect example.`
	
.. _trafficCarObstacleConfig6:

	.. image:: images/configs/traffic/obstacleExamples/CalculateDistanceToIntersectSameTargetExample1.png
	`Calculate distance to intersect same target example.`
	
.. _trafficCarObstacleConfig7:

	.. image:: images/configs/traffic/obstacleExamples/ChangeLaneCloseDistanceExample.png
	`Change lane close distance to point example.`
	
.. _trafficCarObstacleConfig8:
	.. image:: images/configs/traffic/obstacleExamples/ChangeLaneExample1.png
	
	.. image:: images/configs/traffic/obstacleExamples/ChangeLaneExample3.png
	`Short path example.`
	
.. _trafficCarObstacleConfig9:

	.. image:: images/configs/traffic/obstacleExamples/SameDirectionExample.png
	`Same direction example.`
	
.. _trafficCarObstacleConfig10:

	.. image:: images/configs/traffic/obstacleExamples/AvoidCrossroadJamExample.png
	`Avoid crossroad jam example.`

			
Traffic Car Approach Config
------------

	.. image:: images/configs/traffic/TrafficCarApproachConfig.png
	
| **Min approach speed** :
| **On coming to the red light speed** :
| **Stopping distance to light** :
	
Traffic Car Raycast Config
------------

	.. image:: images/configs/traffic/TrafficCarRaycastConfig.png
	
| **Side offset** :
| **Min/Max ray length** :
| **Boxcast height** :
| **Ray Y axis offset** :
| **Dot direction** :
| **Bounds multiplier** :
	
Traffic Car Change Lane Config
------------

	.. image:: images/configs/traffic/TrafficCarChangeLaneConfig.png
	
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
	
	.. image:: images/configs/traffic/changeLaneExamples/MinMaxChangeLaneOffsetExample.png
	`Min/max change lane offset example.`
	
.. _trafficCarChangeLaneConfig2:

	.. image:: images/configs/traffic/changeLaneExamples/MinDistanceToLastCarExample.png
	`Min distance to last car in current lane example.`
	
.. _trafficCarChangeLaneConfig3:
		
	.. image:: images/configs/traffic/changeLaneExamples/MinDistanceToOtherCarsInOtherLaneExample.png
	`Min distance to other cars in other lane example.`
	
.. _trafficCarChangeLaneConfig4:
	
	.. image:: images/configs/traffic/changeLaneExamples/MinDistanceToIntersectedPathExample.png
	`Min distance to intersected path example.`
	
Traffic Car Npc Obstacle Config
------------

	.. image:: images/configs/traffic/TrafficCarNpcObstacleConfig.png
	
| **Check distance** :
| **Square length** :
| **Side offset X** :
| **Max Y diff** :
	
Traffic Car Parking Config
------------

	.. image:: images/configs/traffic/TrafficCarParkingConfig.png

**Rotation aligment at node support** :
	**Rotation speed** :
	**Complete angle** :
		
Traffic Car Antistuck Config
------------

	.. image:: images/configs/traffic/TrafficCarAntistuckConfig.png

| **Obstacle stuck time** :
| **Stuck distance difference** :
| **Cull of out the camera only** :
	
Traffic Car Horne config
------------

	.. image:: images/configs/traffic/TrafficCarHorneConfig.png

| **Chance to start** :
| **Idle time to start** :
| **Delay** :
| **Horne duration** :
	
Public Traffic Configs
============

Traffic Public Spawner Settings
------------

	.. image:: images/configs/traffic/TrafficPublicSpawnerSettings.png
	
| **Spawn frequency** :
| **Traffic public to car model dictionary** :



		