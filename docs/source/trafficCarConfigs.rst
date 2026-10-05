.. _trafficCarConfigs:

Traffic Configs
===============

Traffic Car Spawner Config
--------------------------

	.. image:: /images/configs/traffic/TrafficCarSpawnerConfig.png
	``Hub/Configs/TrafficCarConfigs/CommonConfig``
	
| **Preferable count** : maximum number of cars in the city.
| **HashMap capacity** : initial capacity of the hashmap containing traffic car data.
| **Max spawn count by iteration** : maximum number of cars spawned in a single iteration.
| **Max parking cars** : maximum number of parked cars in the city.
| **Min/Max spawn delay** : minimum/maximum duration between spawns.
| **Min spawn distance** : minimum distance required between cars during spawning.
	
.. _trafficCarSettings:
	
Traffic Car Settings
--------------------

	.. image:: /images/configs/traffic/TrafficCarSettingsConfig.png
	``Hub/Configs/TrafficCarConfigs/CommonConfig``
	
.. _entityType:

Entity Type
~~~~~~~~~~~

* **Hybrid entity simple physics** : :ref:`hybrid entities <hybridEntity>` moved by the simple `DOTS` physics system (:ref:`description <simplePhysicsVehicle>`).
* **Hybrid entity custom physics** : :ref:`hybrid entities <hybridEntity>` moved by the custom `DOTS` physics system (:ref:`description <customPhysicsVehicle>`).
* **Hybrid entity mono physics** : :ref:`hybrid entities <hybridEntity>` moved by the custom `MonoBehaviour` controller (:ref:`description <hybridMonoVehicle>`) *(new)*.
* **Pure entity custom physics** : :ref:`pure entities <pureEntity>` moved by the custom `DOTS` physics system (:ref:`description <customPhysicsVehicle>`).
* **Pure entity simple physics** : :ref:`pure entities <pureEntity>` moved by the simple `DOTS` physics system (:ref:`description <simplePhysicsVehicle>`).
* **Pure entity no physics** : :ref:`pure entities <pureEntity>` moved by the transform system without physics (:ref:`description <noPhysicsVehicle>`).

	.. note::
		The selected :ref:`entity type <entityType>` determines how the :ref:`preset <trafficPreset>` is converted.
	
.. _trafficDetectObstacleMode:

Detect Obstacle Mode
~~~~~~~~~~~~~~~~~~~~

* **Hybrid** : combines `Calculate` and `Raycast` modes.
* **Calculate only** : mathematically calculates obstacle proximity.
* **Raycast only** : detects obstacles via raycasting (:ref:`more info <trafficCarRaycastInfo>`).
	
	.. note::
		In `Hybrid` mode, raycasting activates only when selected targets are close to the vehicle (:ref:`more info <trafficCarRaycastInfo>`).
	
Detect Npc Mode
~~~~~~~~~~~~~~~

* **Disabled**
* **Calculate** : mathematically calculates NPC proximity.
* **Raycast** : detects NPCs via raycasting (NPCs must have a `PhysicsShape` component).
	
Simple Physics Movement Type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Car input** : emulation of real vehicle movement based on traffic input.
* **Follow target** : vehicle rotation is aligned directly toward the destination point.
	
Common Settings
~~~~~~~~~~~~~~~

| **Default lane speed km/h** : default lane speed limit (applied when the lane speed limit is set to 0).
| **Health count** : hit points of the car (health systems must be enabled).

:ref:`Simple Vehicle <simplePhysicsVehicle>` Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| **Max car speed km/h** : maximum speed of the car.
| **Acceleration magnitude** : vehicle acceleration rate.
| **Backward acceleration magnitude** : reverse acceleration rate.
| **Brake power** : braking power.
| **Max steer angle** : maximum steering angle of the wheels in degrees.
| **Steering damping** : wheel turning response speed.

**Has rotation lerp** :
	* **Rotation speed** : vehicle rotation interpolation speed.
	* **Rotation speed curve** : curve defining rotation speed relative to vehicle velocity.
	
:ref:`Custom Vehicle <customPhysicsVehicle>` Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| **Braking input rate** : braking input intensity applied when the current speed exceeds the limit.

.. _trafficCarOtherSettings:
	
Other Settings
~~~~~~~~~~~~~~

| **Cull physics** : disables vehicle physics simulation outside the camera view.
| **Cull wheels** : enables/disables wheel rotation processing outside the camera view.

.. _trafficNavMeshObstacle:

| **Has nav obstacle** : enables/disables NavMesh obstacles for traffic (:ref:`config <trafficNavMeshLoaderConfig>`).
	
Traffic Nav Config
------------------

Configures distances to target nodes and traffic light handlers.

	.. image:: /images/configs/traffic/TrafficCarNavConfigConfig.png
	``Hub/Configs/TrafficCarConfigs/NavConfig``
	
| **Min distance to target** : minimum distance required to reach the target :ref:`TrafficNode <trafficNode>`.
| **Min distance to path point target** : minimum distance to reach a connected :ref:`path point <pathPointConnection>`.
| **Min distance to new light** : minimum distance to the :ref:`TrafficNode <trafficNode>` holding the :ref:`traffic light handler <trafficLightHandler>` entity to assign it to the car (index is -1 if absent).
| **Min distance from previous light** : minimum distance from the :ref:`TrafficNode <trafficNode>` holding the :ref:`traffic light handler <trafficLightHandler>` entity to unassign it from the car (index is -1 if absent).
| **Min distance to target route node** : minimum distance to switch to the next waypoint of the :ref:`path <path>`.
| **Min distance to target rail route node** : minimum distance to switch to the next waypoint of the :ref:`path <path>` (rail movement only, e.g., trams).

**Out of path resolve method:** resolution strategy when a car leaves its designated :ref:`path <path>`.
	* **Disabled** : no corrective action.
	* **Switch node** : switches to the next waypoint along the route.
	* **Backward** : vehicle attempts to reach the missed waypoint in reverse.
	* **Cull** : vehicle is culled and despawned.
	
	.. image:: /images/configs/traffic/TrafficCarNavOutOfPathConfig.png
	
**Out of path resolve method [enabled]:**
	* **Min distance to out of path** : minimum distance from the missed waypoint to trigger out-of-path resolution.
	* **Max distance to out of path** : maximum distance threshold before triggering resolution.
	
| **No Dst React Type** : reaction behavior when no further destination exists (e.g., when a road is unloaded by :ref:`road streaming <roadStreaming>`).
	
.. _trafficCarObstacleConfig:
	
Traffic Obstacle Config
-----------------------

Configures obstacle detection and trajectory checks.

	.. image:: /images/configs/traffic/TrafficCarObstacleConfig.png
	``Hub/Configs/TrafficCarConfigs/ObstacleConfig``

| **Max distance to obstacle** : maximum distance threshold to detect and calculate obstacles ahead (:ref:`example <trafficCarObstacleConfig1>`) (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to start approach** : distance to the vehicle ahead in the lane to begin speed matching (:ref:`approaching <trafficCarApproachConfig>`) (:ref:`example <trafficCarObstacleConfig2>`) (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to start approach soft** : distance to the vehicle ahead to start long-distance deceleration at a gentle speed profile (:ref:`test scene <trafficTestSceneObstacle>`).
| **Min distance to check next connected path** : distance threshold to inspect the upcoming connected path for obstacles (:ref:`example <trafficCarObstacleConfig3>`) (:ref:`test scene <trafficTestSceneNextConnectedPath>`).
| **Short path length** : threshold below which the system checks subsequent connected paths in advance (:ref:`example <trafficCarObstacleConfig4>`).
| **Calculate distance to intersect point** : lookahead distance checked on intersecting paths (:ref:`example <trafficCarObstacleConfig5>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).

**Obstacle intersect calculation method:** method used to compute car-intersection clearance.
	* **Distance** : radial distance between vehicle origin and intersection point.
	* **Bounds** : intersection point checked inside oriented bounding box (OBB).
	
| **Size offset to intersect point** : longitudinal offset added to car bounds when evaluating intersection closeness (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close enough distance to stop before intersect point** : distance threshold to come to a full stop before reaching an intersection point (:ref:`example <trafficCarObstacleConfig5>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close enough distance to stop before intersect same target node** : stopping distance applied when another vehicle approaches the same target node with higher priority (:ref:`example <trafficCarObstacleConfig6>`) (:ref:`test scene <trafficTestSceneIntersectedPath>`).
| **Close distance to change lane point** : distance threshold where a car close to the lane transition point is treated as an active obstacle (:ref:`example <trafficCarObstacleConfig7>`) (:ref:`test scene <trafficTestSceneChangeLane4>`).
| **Max distance to obstacle change lane** : maximum distance checked for obstacles in the target lane during lane changes (:ref:`example <trafficCarObstacleConfig8>`).
| **Same direction value** : dot product alignment threshold to evaluate vehicles on neighboring paths starting from the same junction (:ref:`example <trafficCarObstacleConfig9>`).
| **Avoid crossroad jam** : prevents entering an intersection if the exit lane cannot accommodate the vehicle (:ref:`example <trafficCarObstacleConfig10>`) (:ref:`test scene <trafficTestSceneCrossroadJam>`).
	
	.. note:: 
		**How to calculate parameters relative to vehicle dimensions:**
			* Select the vehicle hull mesh renderer and assign it to the `Target Car Mesh` field.
			* Click the `Recalculate` button.
			* Calibrate parameters in the traffic test scene according to your project requirements.
	
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
-----------------------

Configures vehicle deceleration when approaching obstacles and traffic signals (:ref:`test scene <trafficTestSceneObstacle>`).

	.. image:: /images/configs/traffic/TrafficCarApproachConfig.png
	``Hub/Configs/TrafficCarConfigs/ApproachConfig``
	
| **Min approach speed** : minimum speed when closing in on an obstacle.
| **Min approach speed soft** : minimum cruising speed during soft, long-distance approaches.
| **On coming to the red light speed** : speed target when approaching a red traffic signal.
| **Stopping distance to light** : distance before the stop line where the car comes to a complete halt.

Auto brake before speed limit 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Automatically brakes the vehicle to match a lower upcoming speed limit in advance.

| **Soft braking distance** : lookahead distance to initiate gradual deceleration.
| **Soft braking rate** : deceleration intensity during soft braking.
| **Braking distance** : final distance threshold for standard braking.
| **Skip braking path length distance** : if the current path is shorter than this value, the system evaluates the subsequent path.
	
	.. note:: Approach distances are configured in :ref:`Traffic obstacle config <trafficCarObstacleConfig>`.
	
.. _trafficCarRaycastConfig:
	
Traffic Raycast Config
----------------------

Configures raycast bounds and detection volumes (:ref:`TrafficDetectObstacleMode <trafficDetectObstacleMode>` must be set to `Raycast` or `Hybrid`).

	.. image:: /images/configs/traffic/TrafficCarRaycastConfig.png
	``Hub/Configs/TrafficCarConfigs/RaycastConfig``
	
| **Side offset** : width of the raycast box volume.
| **Min/Max ray length** : minimum and maximum length of the detection box.
| **Boxcast height** : vertical height of the boxcast volume.
| **Ray Y axis offset** : vertical offset from vehicle origin.
| **Dot direction** : in `Hybrid` mode, only targets within this forward dot threshold are raycasted.
| **Bounds multiplier** : multiplier applied to target bounds during evaluation.
	
.. _trafficCarChangeLaneConfig:
	
Traffic Change Lane Config
--------------------------

Configures automatic lane change behavior (operates exclusively on straight road paths) (:ref:`test scene <trafficTestSceneChangeLane>`).

	.. image:: /images/configs/traffic/TrafficCarChangeLaneConfig.png
	``Hub/Configs/TrafficCarConfigs/ChangeLaneConfig``

| **Can change lane** : enables/disables lane changing across traffic.
| **Min max change lane offset** : speed-dependent forward offset along the target lane (:ref:`example <trafficCarChangeLaneConfig1>`).
| **Max distance to end of path** : maximum distance before path termination where lane changing remains permitted.
| **Min distance to last car in current lane** : minimum safety distance behind the lead vehicle (:ref:`example <trafficCarChangeLaneConfig2>`).
| **Min Max distance to other cars in other lane** : required gap between vehicles in the destination lane, interpolated based on current speed (:ref:`example <trafficCarChangeLaneConfig3>`).
| **Max distance to intersected path** : distance before an intersection beyond which lane changes are prohibited (:ref:`example <trafficCarChangeLaneConfig4>`).
| **Check frequency** : frequency of lane change condition evaluations in seconds.
| **Block duration after change lane** : cooldown duration preventing consecutive lane changes.
| **Achieve distance** : distance tolerance to consider the lane change maneuver complete.
| **Min car count in current lane to change lane** : minimum number of vehicles ahead required to trigger an overtaking lane change.
| **Min car lane difference count to start change lane** : required vehicle count difference in adjacent lanes before changing.
| **Change lane car speed** : speed maintained during the transition maneuver.
| **Change lane HashMap capacity** : initial capacity of the hashmap storing active lane-change states.
	
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
---------------------------

Configures vehicle reaction to pedestrian obstacles (:ref:`example <trafficCarNpcObstacleDebugger>`).

	.. image:: /images/configs/traffic/TrafficCarNpcObstacleConfig.png
	``Hub/Configs/TrafficCarConfigs/NpcObstacleConfig``
	
| **Obstacle pedestrian action state** : pedestrian :ref:`Action State <pedestrianActionState>` that triggers a vehicle reaction.
| **Check distance** : forward length of the NPC detection zone.
| **Square length** : length of the detection calculation box.
| **Side offset X** : lateral width of the detection zone.
| **Max Y diff** : maximum vertical altitude difference between vehicle and NPC to be registered.
	
.. _trafficCarParkingConfig:
	
Traffic Parking Config
----------------------

Configures parking maneuvers (:ref:`test scene <trafficTestSceneParking>`).

	.. image:: /images/configs/traffic/TrafficCarParkingConfig.png
	``Hub/Configs/TrafficCarConfigs/ParkingConfig``

| **Precise Alignment At Node** : enables/disables precise slot alignment when parking.
| **Rotation speed** : turning speed during parking alignment.
| **Complete angle** : angle threshold to consider slot rotation finished.
| **Precise position** : enables/disables minor position correction when entering the parking slot.
| **Movement speed** : driving speed during slot entry correction.
| **Achieve distance** : distance threshold to consider the parking target reached.

	.. note:: Read more about :ref:`parking states <trafficParking>`.
		
.. _trafficCarAntistuckConfig:
		
Traffic Antistuck Config
------------------------

Configures anti-stuck detection and despawning behavior.

	.. image:: /images/configs/traffic/TrafficCarAntistuckConfig.png
	``Hub/Configs/TrafficCarConfigs/AntistuckConfig``

| **Obstacle stuck time** : duration vehicle must remain blocked before being despawned.
| **Stuck distance difference** : movement distance required to reset the stuck timer.
| **Cull out of camera only** : restricts despawning to vehicles outside the active camera frustum.
	
Traffic Horn Config
-------------------

Configures random horn sounding when an obstacle blocks the vehicle (:ref:`Sound Config <soundConfig>`).

	.. image:: /images/configs/traffic/TrafficCarHornConfig.png
	``Hub/Configs/TrafficCarConfigs/HornConfig``

| **Chance to start** : probability of sounding the horn upon encountering an obstacle.
| **Idle time to start** : delay before sounding the horn while waiting.
| **Delay** : cooldown delay between consecutive honks.
| **Horn duration** : duration of each horn sound.

.. _trafficNavMeshLoaderConfig:

Traffic NavMesh Loader Config
-----------------------------

Loads runtime `NavMeshObstacle` components around traffic vehicles.

	.. image:: /images/configs/traffic/TrafficNavMeshLoaderConfig.png
	``Hub/Configs/TrafficCarConfigs/TrafficNavMeshLoaderConfig``

| **Size offset** : dimensional padding added to the generated `NavMeshObstacle`.
| **Load only view** : restricts NavMesh obstacle creation to vehicles in the camera frustum.
| **Load frequency** : update frequency of NavMesh obstacle generation.

	.. note::
		* NavMesh obstacle loading is enabled in the :ref:`Traffic Settings <trafficNavMeshObstacle>` config.
		* Ensure pedestrians utilize :ref:`NavMesh navigation <pedestrianNavmeshNavigation>`.
		* Ensure a valid `NavMeshSurface` is baked in the scene.
		
.. _trafficAvoidanceConfig:

Traffic Avoidance Config
------------------------

Configures traffic dynamic :ref:`avoidance <trafficAvoidance>`.

	.. image:: /images/configs/traffic/TrafficAvoidanceConfig.png
	``Hub/Configs/TrafficCarConfigs/AvoidanceConfig``
	
| **Custom achieve distance** : distance threshold to consider avoidance waypoints reached.
| **Resolve cyclic obstacle** : resolves circular deadlock situations where multiple vehicles block each other.

Traffic Custom Destination Config
---------------------------------

Configures custom routing destinations and :ref:`traffic avoidance <trafficAvoidance>`.

	.. image:: /images/configs/traffic/TrafficCustomDestinationConfig.png
	``Hub/Configs/TrafficCarConfigs/CustomDestinationConfig``
		
| **Default speed limit** : default speed limit applied when routing toward a custom destination.
| **Check side point** : checks if the destination point is laterally adjacent to the vehicle.
| **Side point speed limit** : speed limit when steering toward a lateral point.
| **Side point distance** : distance threshold to lateral points.
| **Default achieve distance** : arrival tolerance for destination points.
| **Max duration** : timeout duration for the custom destination state.

.. _trafficRailConfig:

Traffic Rail Config
-------------------

Configures :ref:`rail movement <trafficRail>` for tracked vehicles (e.g., trams).

	.. image:: /images/configs/traffic/TrafficRailConfig.png
	``Hub/Configs/TrafficCarConfigs/RailConfig``
	
| **Max distance to rail line** : maximum allowable distance between vehicle and rail track.
| **Lateral speed** : lateral correction speed to keep the vehicle aligned with the rail.
| **Rotating lerp speed** : angular interpolation speed along rail curves.
| **Lerp rotation tram** : enables/disables rotation lerping for trams.
| **Lerp rotation traffic** : enables/disables rotation lerping for default traffic along rails.

.. _trafficCollisionConfig:

Traffic Collision Config
------------------------

Configures vehicle collision reaction and resolution between vehicles.

	.. image:: /images/configs/traffic/TrafficCollisionConfig.png
	``Hub/Configs/TrafficCarConfigs/CollisionConfig``
	
| **Idle duration** : pause duration after colliding with another vehicle.
| **Avoid stucked collision** : attempts :ref:`avoidance <trafficAvoidance>` when jammed against another vehicle.
| **Collision duration** : contact duration required before initiating avoidance.
| **Ignore collision duration** : cooldown duration where subsequent collisions are ignored.
| **Calculation collision frequency** : evaluation frequency for collision avoidance checks.
| **Repeat avoidance frequency** : retry frequency for avoidance maneuvers.
| **Forward direction value** : longitudinal alignment threshold (Z-axis dot product) between colliding vehicles.
| **Side direction value** : lateral alignment threshold (X-axis dot product) between colliding vehicles.

Traffic Behavior Config
-----------------------

Configures driving personality profiles and behaviors.

| **Tailgate rate** : tailgating multiplier applied to obstacle distance (``MaxDistanceToObstacle = MaxDistanceToObstacle * TailgateRate``).
| **Acceleration rate** : acceleration intensity multiplier.
| **Speeding rate** : speed limit deviation multiplier.
| **Idle input duration** : startup delay before beginning movement.
| **Random change lane duration** : frequency of voluntary lane change attempts.
| **Approach distance rate** : distance multiplier applied to standard deceleration approach.
| **Approach distance rate soft** : distance multiplier applied to soft approach deceleration.