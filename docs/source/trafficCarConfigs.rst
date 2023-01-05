.. _trafficCarConfigs:

Traffic Configs
============

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
	* **Hybrid** :
	* **Calculate only** :
	* **Raycast only** :
	
**Traffic car detect npc mode:**
	* **Disabled** :
	* **Calculate** :
	* **Raycast** :
	
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
	
| **Max distance to obstacle** :
| **Min distance to start approach** :
| **Min distance to check next connected path** :
| **Short path length** :
**Calculate distance to intersect point** :
	**Obstacle intersect calculation method:**
	* **Distance** :
	* **Bounds** :
| **Size offset to intersect point** :
| **Close enough distance to stop before intersect point** :
| **Close enough distance to stop before intersect same target node** :
| **Close distance to change lane point** :
| **Max distance to obstacle change lane** :
**Same direction value** :
	**Avoid crossroad jam** :
	
	.. note:: 
		**How to calculate the parameters regarding the size of the vehicle hull:**
			* Select the mesh renderer of the vehicle hull and insert to the `Target Car Mesh` field.
			* Press `Recalculate` button.
			* On the traffic test scene, calibrate the parameters depending on your needs.
			
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
	
| **Can change lane** :
| **Min max change lane offset** :
| **Max distance to end of path** :
| **Min distance to last car in current lane** :
| **Min Max distance to other cars in other lane** :
| **Max distance to intersected path** :
| **Check frequency** :
| **Block duration after change lane** :
| **Achieve distance** :
| **Min car count in current lane to change lane** :
| **Min car lane difference count to start change lane** :
| **Change lane car speed** :
| **Change lane HashMap capacity** :
	
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



		