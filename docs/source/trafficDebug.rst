.. _trafficDebug:

Traffic Debug
============

.. contents::
   :local:

How To Open
------------

`Youtube tutorial. <https://youtu.be/rj1Rww-9Yq8>`_

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

Debugger Type 
~~~~~~~~~~~~ 

Default
""""""""""""""""""

	.. image:: /images/debuggers/traffic/TrafficCarDebuggerExample.png	
	
Target  
""""""""""""""""""

Shows the target position of the vehicle.

Approach speed 
""""""""""""""""""

Shows the vehicle's approach speed.

State 
""""""""""""""""""

Shows the state of the vehicle.

Target index 
""""""""""""""""""

Shows the target indexes of the vehicle.

Path index
""""""""""""""""""

Shows the path index of the vehicle.
 
Speed limit
""""""""""""""""""
	
Shows the current speed and the speed limit of the vehicle.
	 
	.. image:: /images/debuggers/traffic/TrafficCarDebuggerSpeedLimitExample.png		

Change lane
""""""""""""""""""

Shows the change lane point on the lane in the scene.	

Collision
""""""""""""""""""

Shows the collision direction of the vehicle.

Obstacle
""""""""""""""""""

Shows the obstacle entity & obstacle reason type of the vehicle.

Obstacle reason type:
    * Undefined
    * DefaultPath : default obstacle in the current path or next connected path of the vehicle.
    * NeighborPath : obstacle on neighbouring paths, that starts from the current path.
    * JamCase_1 : the vehicle stays at the entrance of the crossroad & doesn't enter to avoid traffic jams.
    * FewChangeLaneCars : obstacle when the current vehicle and the obstacle vehicle change lanes at the same time.
    * ChangingLane : the obstacle vehicle changes lanes to the lane of the current vehicle.
    * Intersect_1_TargetCarCloseToIntersectPoint : target obstacle vehicle too close to intersection of two paths (both vehicles are close, but the target vehicle is closer).
    * Intersect_2_TargetCarCloseToIntersectPoint : target obstacle vehicle too close to intersection of two paths (only target vehicle is too close).
    * Intersect_3_OtherHasPriority : vehicles meeting at an intersection of two paths have different priorities, with the higher priority vehicle passing first (unless the vehicle is too close to the intersection).
    * Intersect_4_SamePriority : vehicles that meet at an intersection of two paths have the same priority, whichever vehicle is closer to the intersection that passes first.
	
No target
""""""""""""""""""

Shows the list of vehicles without a destination.
	 
Settings
~~~~~~~~~~~~ 
	 
| **Text color** : colour of scene text UI.
| **Show obstacle info** : display obstacles for vehicles (red color vehicle has obstacle).
| **Show common info** : show the entity index of the vehicles.

.. _trafficCarRaycastDebugger:

Traffic Raycast Debugger
------------

Shows the raycast box of the car. (:ref:`Config <trafficCarRaycastConfig>`) (:ref:`info <trafficCarRaycastInfo>`)

	.. image:: /images/debuggers/traffic/TrafficCarRaycastDebugger.png		
	
| **Enable debug** : on/off debugger.

Example
~~~~~~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficCarRaycastDebuggerExample.png		

.. _trafficCarNpcObstacleDebugger:

Traffic NpcObstacle Debugger
------------

Shows the calculation area and the vehicle's obstacle NPCs.

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebugger.png		
	
| **Enable debug** : on/off debugger.
| **Area color** : colour of the area where the vehicle calculates the npc obstacles.
| **Selected index** : only for this entity index will debug be enabled (-1 all entities).
	
Example
~~~~~~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebuggerExample.png		
	
Traffic Public Debugger
------------
	
Shows :ref:`public transport traffic <trafficPublic>` data.
	
	.. image:: /images/debuggers/traffic/TrafficPublicDebugger.png		
	
| **Enable debug** : on/off debugger.
| **Text color** : colour of scene text UI.

Example
~~~~~~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficPublicDebuggerExample.png		
	
Traffic Light Debugger
------------

Shows the :ref:`state <trafficLightState>` of :ref:`traffic light objects <trafficLightObject>`.

	.. image:: /images/debuggers/traffic/TrafficLightDebugger.png		