.. _trafficDebug:

Traffic Debug
============

.. contents::
   :local:

How To Open
------------

On the scene select:

	`CityDebugger/TrafficDebugger/`

.. _trafficDebugSpawnHelper:

Traffic Spawn Button Helper
------------

For manual spawn of a car by the :ref:`selected index <trafficNodeIndexDebug>`.

	.. image:: /images/debuggers/traffic/TrafficCarSpawnButtonHelper.png		
	
Traffic Debugger
------------

	.. image:: /images/debuggers/traffic/TrafficCarDebugger.png		
	
| **Enable debug** : on/off debugger.

**Debugger type** : 
	* **Default**
	
		.. image:: /images/debuggers/traffic/TrafficCarDebuggerExample.png	
		
	* **Target** :  shows the target position of the vehicle.
	* **Approach speed** : shows the vehicle's approach speed.
	* **State** : shows the state of the vehicle.
	* **Target index** : shows the target indexes of the vehicle.
	* **Path index** : shows the path index of the vehicle.
	* **Speed limit** : shows the current speed and the speed limit of the vehicle.
		
		.. image:: /images/debuggers/traffic/TrafficCarDebuggerSpeedLimitExample.png		
	
	* **Change lane** : 
	
| **Text color** : colour of scene text UI.
| **Show obstacle info** : display obstacles for vehicles (red color vehicle has obstacle).
| **Show common info** : show the entity index of the vehicles.

.. _trafficCarNpcObstacleDebugger:

TrafficNpcObstacleDebugger
------------

Shows the calculation area and the vehicle's obstacle NPCs.

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebugger.png		
	
| **Enable debug** : on/off debugger.
| **Area color** : colour of the area where the vehicle calculates the npc obstacles.
| **Selected index** : only for this entity index will debug be enabled (-1 all entities).
	
Example:

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebuggerExample.png		
	
Traffic Public Debugger
------------
	
Shows :ref:`public transport traffic <trafficPublic>` data.
	
	.. image:: /images/debuggers/traffic/TrafficPublicDebugger.png		
	
| **Enable debug** : on/off debugger.
| **Text color** : colour of scene text UI.

Example:

	.. image:: /images/debuggers/traffic/TrafficPublicDebuggerExample.png		
	
Traffic Light Debugger
------------

Shows the :ref:`state <trafficLightState>` of :ref:`traffic light objects <trafficLightObject>`.

	.. image:: /images/debuggers/traffic/TrafficLightDebugger.png		