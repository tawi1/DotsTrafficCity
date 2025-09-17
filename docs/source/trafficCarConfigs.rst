.. _trafficCarConfigs:

Traffic Configs
=====

Traffic Car Spawner Config
------------

	.. image:: /images/configs/traffic/TrafficCarSpawnerConfig.png
	``Hub/Configs/TrafficCarConfigs/CommonConfig``
	
| **Preferable count** : maximum number of cars in the city.
| **HashMap capacity** : initial capacity of the hashmap that contains the data of the traffic cars.
| **Max spawn count by iteration** : maximum number of cars that will be spawned in one iteration.
| **Max parking cars** : maximum number of parked in the city.
| **Min/Max spawn delay** : minimum/maximum duration between spawns.
| **Min spawn distance** : minimum distance for spawning between cars.
	
.. _trafficCarSettings:
	
Traffic Car Settings
------------

	.. image:: /images/configs/traffic/TrafficCarSettingsConfig.png
	``Hub/Configs/TrafficCarConfigs/CommonConfig``
	
.. _entityType:

Entity Type
~~~~~~~~~~~~ 

* **Hybrid entity simple physics** : :ref:`hybrid entities <hybridEntity>` moved by the simple `DOTS` physical system (:ref:`description <simplePhysicsVehicle>`).
* **Hybrid entity custom physics** : :ref:`hybrid entities <hybridEntity>` moved by the custom `DOTS` physical system (:ref:`description <customPhysicsVehicle>`)  
* **Hybrid entity mono physics** : :ref:`hybrid entities <hybridEntity>` moved by the custom `Monobehaviour` controller (:ref:`description <hybridMonoVehicle>`) *(new)*
* **Pure entity custom physics** : :ref:`pure entities <pureEntity>` moved by the custom `DOTS` physical system (:ref:`description <customPhysicsVehicle>`)  
* **Pure entity simple physics** : :ref:`pure entities <pureEntity>` moved by the simple `DOTS` physical system (:ref:`description <simplePhysicsVehicle>`).
* **Pure entity no physics** : :ref:`pure entities <pureEntity>` that moved by transform system without physics (:ref:`description <noPhysicsVehicle>`).

	.. note::
		Depending on which :ref:`entity type <entityType>` such a :ref:`preset <trafficPreset>` is converted.
	
.. _trafficDetectObstacleMode:

Detect Obstacle Mode
~~~~~~~~~~~~ 

* **Hybrid** : combine types `Calculate` and `Raycast`.
* **Calculate only** : mathematically calculates the obstacle.
* **Raycast only** : detect obstacle by raycast (:ref:`more info <trafficCarRaycastInfo>`).
	
	.. note::
		In `Hybrid mode`, raycast is activated only when the selected targets are close to the car (:ref:`more info <trafficCarRaycastInfo>`).
	
Detect Npc Mode
~~~~~~~~~~~~ 

* **Disabled**
* **Calculate** : mathematically calculates the npc.
* **Raycast** : detect obstacle by raycast (npc should have `PhysicsShape` component).
	
Simple Physics Movement Type
~~~~~~~~~~~~ 

* **Car input** : simple emulation of real movement based on traffic input.
* **Follow target** : the vehicle rotation is set based on the destination direction.
	
Common Settings
~~~~~~~~~~~~ 

| **Default lane speed km/h** : default lane speed (if the lane speed limit is set to 0 the default speed will be selected).
| **Health count** : number of hit points of the car (health systems should be enabled).

:ref:`Simple Vehicle <simplePhysicsVehicle>` Settings
~~~~~~~~~~~~ 

| **Max car speed km/h** : maximum speed of the car.
| **Acceleration magnitude** : vehicle acceleration speed.
| **Backward acceleration magnitude** : backward vehicle acceleration speed.
| **Brake power** : brake power.
| **Max steer angle** : max steer angle of the wheels.
| **Steering damping** : wheel turn speed.

**Has rotation lerp** :
	* **Rotation speed** : vehicle rotation speed.
	* **Rotation speed curve** : curve on the dependence of the speed of the car on its speed.
	
:ref:`Custom Vehicle <customPhysicsVehicle>` Settings
~~~~~~~~~~~~ 

| **Braking input rate** : braking rate if current vehicle speed limit is greater than speed limit.

.. _trafficCarOtherSettings:
	
Other Settings
~~~~~~~~~~~~ 

| **Cull physics** : off physics for the vehicle if they are outside the camera.
| **Cull wheels** : on/off wheel handling if they are outside the camera.

.. _trafficNavMeshObstacle:

| **Has nav obstacle** : on/off navmesh obstacles for traffic :ref:`config <trafficNavMeshLoaderConfig>`.
	
Traffic Nav Config
------------

Config distance to target nodes and traffic light handlers.

	.. image:: /images/configs/traffic/TrafficCarNavConfigConfig.png
	``Hub/Configs/TrafficCarConfigs/NavConfig``
	
| **Min distance to target** : min distance to target :ref:`TrafficNode<trafficNode>`.
| **Min distance to path point target** : min distance to connected :ref:`path point <pathPointConnection>`.
| **Min distance to new light** : minimum distance to the :ref:`TrafficNode<trafficNode>` entity that contains the :ref:`traffic light handler<trafficLightHandler>` entity to assign it to the car entity (if the traffic node entity does not contain a traffic light entity, the index is -1).
| **Min distance from previous light** : minimum distance from the :ref:`TrafficNode<trafficNode>` entity that contains the :ref:`traffic light handler<trafficLightHandler>` entity to unassign it from the car entity (if the traffic node entity does not contain a traffic light entity, the index is -1).
| **Min distance to target route node** : minimum distance to switch to the next waypoint of the :ref:`path<path>`.
| **Min distance to target rail route node** : minimum distance to switch to the next waypoint of the :ref:`path<path>` (rail movement only (tramc etc...)).

**Out of path resolve method:** resolving method in case the car is out of the :ref:`path <path>`.
	* **Disabled** : no actions.
	* **Switch node** : switching to the next waypoint.
	* **Backward** : car will try to reach the missed waypoint by reversing.
	* **Cull** : car will be culled.
	
	.. image:: /images/configs/traffic/TrafficCarNavOutOfPathConfig.png
	
**Out of path resolve method [enabled]:**
	* **Min distance to out of path** : minimum distance from the missed waypoint to the car.
	* **Max distance to out of path** : maximum distance from the missed waypoint to the car.
	
| **No Dst React Type** : the reaction if there is no further destination for the cars (for example, when the road was unloaded by :ref:`road streaming <roadStreaming>`).
	
.. _trafficCarObstacleConfig:
	
Traffic Obstacle Config
------------

Config to calculate obstacles on the path.

	.. image:: /images/configs/traffic/TrafficCarObstacleConfig.png
	``Hub/Configs/TrafficCarConfigs/ObstacleConfig``
	
| **Max distance to obstacle** : minimum distance to an obstacle (:ref:`example<trafficCarObstacleConfig1>`) (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to start approach** : minimum distance to the last car in the current lane to start (:ref:`approaching <trafficCarApproachConfig>`) (stay at the same speed as the target car) (:ref:`example<trafficCarObstacleConfig2>`) (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to start approach soft** : minimum distance to the last car in the current lane to start (:ref:`approaching <trafficCarApproachConfig>`) (long distance approach at a `soft` speed) (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to check next connected path** : minimum distance to check the next path for obstacles (:ref:`example<trafficCarObstacleConfig3>`) (:ref:`test scene <trafficTestSceneNextConnectedPath>`).
| **Short path length** : if the next path is too short, start checking the next connected paths for obstacles (:ref:`example<trafficCarObstacleConfig4>`).
| **Calculate distance to intersect point** : distance to intersected paths when they are checked for obstacles (:ref:`example<trafficCarObstacleConfig5>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).

**Obstacle intersect calculation method:** method of calculating the intersection of the vehicle and the intersect point.
	* **Distance** : distance between car and intersect point.
	* **Bounds** : calculate intersect point that inside the car bounds.
	
| **Size offset to intersect point** : additional offset to the length of the car bounds to check the closeness to the intersect point (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close enough distance to stop before intersect point** : car is close enough to stop in front of the intersect point if necessary (:ref:`example<trafficCarObstacleConfig5>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close enough distance to stop before intersect same target node** : current car is close enough to stop in front if another car approaches the same target node but with a higher priority (:ref:`example<trafficCarObstacleConfig6>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close distance to change lane point** : car that is too close to the lane change point is always an obstacle (:ref:`example<trafficCarObstacleConfig7>`) (:ref:`test scene <trafficTestSceneChangeLane4>`).
| **Max distance to obstacle change lane** : maximum distance to the obstacle in the target change lane (:ref:`example<trafficCarObstacleConfig8>`).
| **Same direction value** : direction of the vehicle to check for obstacles in neighboring paths (paths that start from the same point)(:ref:`example<trafficCarObstacleConfig9>`).
| **Avoid crossroad jam** : car doesn't enter an crossroad if it cannot pass it without jamming (:ref:`example<trafficCarObstacleConfig10>`) (:ref:`test scene <trafficTestSceneCrossroadJam>`).
	
	.. note:: 
		**How to calculate the parameters relative to the size of the vehicle hull:**
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
	`Maximum distance to the obstacle in the target change lane example.`
		
	.. image:: /images/configs/traffic/obstacleExamples/ChangeLaneExample3.png
	`Short path example.`
	
.. _trafficCarObstacleConfig9:

	.. image:: /images/configs/traffic/obstacleExamples/SameDirectionExample.png
	`Same direction example.`
	
.. _trafficCarObstacleConfig10:

	.. image:: /images/configs/traffic/obstacleExamples/AvoidCrossroadJamExample.png
	`Avoid crossroad jam example.`
			
.. _trafficCarApproachConfig:
			
Traffic Approach Config
------------

Config of approaching obstacles and lights (:ref:`test scene <trafficTestSceneObstacle>`).

	.. image:: /images/configs/traffic/TrafficCarApproachConfig.png
	``Hub/Configs/TrafficCarConfigs/ApproachConfig``
	
| **Min approach speed** : min approach speed.
| **Min approach speed soft** : min approach speed soft at the long distance to obstacle.
| **On coming to the red light speed** : slowing down the speed of the car when approaching a red light (if the segment speed limit is lower or the speed of the obstacles is lower, the lowest speed of all the conditions will be selected).
| **Stopping distance to light** : distance at which the car slows down.

Auto brake before speed limit 
~~~~~~~~~~~~ 

The car automatically brakes to the new speed limit at the selected distance.

| **Soft braking distance** : soft braking distance to new speed limit.
| **Soft braking rate** : soft braking rate when the car is at a soft distance (if it is closer soft distance than the default :ref:`braking rate <trafficCarSettings>`).
| **Braking distance** : braking distance to new speed limit.
| **Skip braking path length distance** : if the next path is too short, the next one is selected.
	
	.. note:: Approach distance set in :ref:`Traffic obstacle config <trafficCarObstacleConfig>`.
	
.. _trafficCarRaycastConfig:
	
Traffic Raycast Config
------------

Traffic raycast Config (:ref:`TrafficDetectObstacleMode<trafficDetectObstacleMode>` raycast or hybrid should be enabled) (:ref:`debug example<trafficCarRaycastDebugger>`) (:ref:`more info <trafficCarRaycastInfo>`).

	.. image:: /images/configs/traffic/TrafficCarRaycastConfig.png
	``Hub/Configs/TrafficCarConfigs/RaycastConfig``
	
| **Side offset** : width of raycast box.
| **Min/Max ray length** : lenght of raycast box.
| **Boxcast height** : height raycast box.
| **Ray Y axis offset** : y-offset position box.
| **Dot direction** : if the raycast is set to :ref:`Hybrid mode<trafficDetectObstacleMode>` than only those targets that are in front of the car with the set dot parameter will be raycasted.
| **Bounds multiplier** : value by which the bounds is multiplied.
	
.. _trafficCarChangeLaneConfig:
	
Traffic Change Lane Config
------------

Config for automatic calculation of lane change by traffic (works for :ref:`paths<path>` with the `Straight road` :ref:`road type<pathRoadType>` only) (:ref:`test scene <trafficTestSceneChangeLane>`).

	.. image:: /images/configs/traffic/TrafficCarChangeLaneConfig.png
	``Hub/Configs/TrafficCarConfigs/ChangeLaneConfig``
	
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
	
Traffic Npc Obstacle Config
------------

Config to calculate npc obstacles (:ref:`example<trafficCarNpcObstacleDebugger>`).

	.. image:: /images/configs/traffic/TrafficCarNpcObstacleConfig.png
	``Hub/Configs/TrafficCarConfigs/NpcObstacleConfig``
	
| **Obstacle pedestrian action state** : the car only reacts to pedestrians with the selected :ref:`Action State<pedestrianActionState>`.
| **Check distance** : obstacle calculation length.
| **Square length** : length of the obstacle calculation square.
| **Side offset X** : width of the obstacle calculation square.
| **Max Y diff** : maximum difference in Y-axis position between the car and the npc.
	
.. _trafficCarParkingConfig:
	
Traffic Parking Config
------------

Config for parking cars (:ref:`test scene <trafficTestSceneParking>`).

	.. image:: /images/configs/traffic/TrafficCarParkingConfig.png
	``Hub/Configs/TrafficCarConfigs/ParkingConfig``

| **Precise Aligmentn At Node** : on/off precise positioning of the car's parking space.
| **Rotation speed** : rotation speed.
| **Complete angle** : angle at which the rotation is complete.
| **Precise position** : on/off minor driving correction speed to parking point.
| **Movement speed** : on/off minor driving correction speed to parking point.
| **Achieve distance** : on/off minor driving correction speed to parking point.

	.. note :: Read more about :ref:`parking states <trafficParking>`.
		
.. _trafficCarAntistuckConfig:
		
Traffic Antistuck Config
------------

Config to culling car in case of stuckness.

	.. image:: /images/configs/traffic/TrafficCarAntistuckConfig.png
	``Hub/Configs/TrafficCarConfigs/AntistuckConfig``

| **Obstacle stuck time** : duration of sighting of the obstacle after which the car will be culled.
| **Stuck distance difference** : if the car moved more than the parameter distance the `Obstacle stuck time` is reset.
| **Cull of out the camera only** : car will be culled only if it is out of the camera's range of vision.
	
Traffic Horn Config
------------

Config to sound random horns when an obstacle is detected. It can be disabled (:ref:`here<soundConfig>`).

	.. image:: /images/configs/traffic/TrafficCarHornConfig.png
	``Hub/Configs/TrafficCarConfigs/HornConfig``

| **Chance to start** : chance to start the horn.
| **Idle time to start** : idle time to start the horn.
| **Delay** : delay between horns.
| **Horn duration** : horn duration.

.. _trafficNavMeshLoaderConfig:

Traffic NavMesh Loader Config
------------

Config to load `Navmesh obstacles <https://docs.unity3d.com/2022.2/Documentation/Manual/class-NavMeshObstacle.html>`_ for traffic. 

	.. image:: /images/configs/traffic/TrafficNavMeshLoaderConfig.png
	``Hub/Configs/TrafficCarConfigs/TrafficNavMeshLoaderConfig``

| **Size offset** : size offset of loaded `NavMeshObstacle <https://docs.unity3d.com/2022.2/Documentation/Manual/class-NavMeshObstacle.html>`_.
| **Load only view** : load `NavMeshObstacle <https://docs.unity3d.com/2022.2/Documentation/Manual/class-NavMeshObstacle.html>`_ in view of camera only.
| **Load frequency** : load frequency of `NavMeshObstacle <https://docs.unity3d.com/2022.2/Documentation/Manual/class-NavMeshObstacle.html>`_ for the car.

	.. note::
		* `NavMeshObstacle <https://docs.unity3d.com/2022.2/Documentation/Manual/class-NavMeshObstacle.html>`_ loading is enabling in the :ref:`Traffic Settings <trafficNavMeshObstacle>` config.
		* Make sure, that the pedestrians have :ref:`NavMesh navigation <pedestrianNavmeshNavigation>`.
		* Make sure, that the `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ is generated.
		
.. _trafficAvoidanceConfig:

Traffic Avoidance Config
------------

Config of traffic :ref:`avoidance <trafficAvoidance>`.

	.. image:: /images/configs/traffic/TrafficAvoidanceConfig.png
	``Hub/Configs/TrafficCarConfigs/AvoidanceConfig``
	
| **Custom achieve distance** : custom achieve distance of avoidance point.
| **Resolve cyclic obstacle** : overcome the cyclical obstacle of cars getting stuck in each other.

Traffic Custom Destination Config
------------

Config for custom destination of the vehicles. Also used by :ref:`traffic avoidance <trafficAvoidance>`.

	.. image:: /images/configs/traffic/TrafficCustomDestinationConfig.png
	``Hub/Configs/TrafficCarConfigs/CustomDestinationConfig``
		
| **Default speed limit** : default speed limit for custom destination (if user doesn't set custom).
| **Check side point** : check that the destination is on the side of the car.
| **Side point speed limit** : custom speed limit when destination is at side point.
| **Side point distance** : distance to side point.
| **Default achieve distance** : achieve distance of destination point.
| **Max duration** : max duration of custom destination state enabled.

.. _trafficRailConfig:

Traffic Rail Config
------------

Config for :ref:`rail movement <trafficRail>` of the vehicles.

	.. image:: /images/configs/traffic/TrafficRailConfig.png
	``Hub/Configs/TrafficCarConfigs/RailConfig``
	
| **Max distance to rail line** : maximum distance between the rail and the vehicle.
| **Lateral speed** : lateral speed of the vehicle to align with the rail.
| **Rotating lerp speed** : rotation lerp speed.
| **Lerp rotation tram** : on/off rotating lerp for tram.
| **Lerp rotation traffic** : on/off rotating lerp for default traffic.

.. _trafficCollisionConfig:

Traffic Collision Config
------------

The config is used in a two-car collision.

	.. image:: /images/configs/traffic/TrafficCollisionConfig.png
	``Hub/Configs/TrafficCarConfigs/CollisionConfig``
	
| **Idle duration** : idling time after collision with other vehicle.
| **Avoid stucked collision** : attempt to :ref:`avoid <trafficAvoidance>` a stuck collision vehicle.
| **Collision duration** : collision time with vehicle to start :ref:`avoidance <trafficAvoidance>`.
| **Ignore collision duration** : duration of collision ignoring since last event.
| **Calculation collision frequency** : calculation frequency of the :ref:`avoidance <trafficAvoidance>`.
| **Repeat avoidance frequency** : frequency of collision :ref:`avoidance <trafficAvoidance>` attempts.
| **Forward direction value** : dot value of the direction of the colliding vehicles along the Z axis.
| **Side direction value** : dot value of the direction of the colliding vehicles along the X axis.

Traffic Behavior Config
------------

Config for setting different driving styles.

| **Tailgate rate** : Tailgate rate. used with :ref:`Traffic Obstacle Config <trafficCarObstacleConfig>` MaxDistanceToObstacle = MaxDistanceToObstacle * TailgateRate.
| **Acceleration rate** : input acceleration speed.
| **Speeding rate** : degree of deviation from the speed limit.
| **Idle input duration** : idle time before starting movement.
| **Random change lane duration** : frequency of random lane changes.
| **Approach distance rate** : approach distance rate. Used with :ref:`Traffic Obstacle Config <trafficCarObstacleConfig>` ApproachDistance = ApproachDistance * ApproachDistanceRate.
| **Approach distance rate soft** : approach distance rate soft. Used with :ref:`Traffic Obstacle Config <trafficCarObstacleConfig>` ApproachDistanceSoft = ApproachDistanceSoft * ApproachDistanceRateSoft.