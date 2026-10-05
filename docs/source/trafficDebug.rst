.. _trafficDebug:

Traffic Debug
=============

.. contents::
   :local:

How To Open
-----------

`YouTube tutorial. <https://youtu.be/rj1Rww-9Yq8>`_

In the scene, select:

	`CityDebugger/TrafficDebugger/`

.. _trafficDebugSpawnHelper:

Traffic Spawn Button Helper
---------------------------

Manually spawns a vehicle at the :ref:`selected index <trafficNodeIndexDebug>`.

	.. image:: /images/debuggers/traffic/TrafficCarSpawnButtonHelper.png		
	
Traffic Debugger
----------------

	.. image:: /images/debuggers/traffic/TrafficCarDebugger.png		
	
| **Enable debug** : enables/disables traffic debugging.

Debugger Type 
~~~~~~~~~~~~~

Default
"""""""

	.. image:: /images/debuggers/traffic/TrafficCarDebuggerExample.png	
	
Target  
""""""

Shows the current target position of the vehicle.

Approach speed 
""""""""""""""

Shows the vehicle's calculated approach speed.

State 
"""""

Shows the current internal state of the vehicle.

Idle State
""""""""""

Shows the root cause of the vehicle's idle state.

Target index 
""""""""""""

Shows the active target node index of the vehicle.

Path index
""""""""""

Shows the global path index of the vehicle.
 
Speed limit
"""""""""""
	
Shows the current speed and speed limit of the vehicle.
	 
	.. image:: /images/debuggers/traffic/TrafficCarDebuggerSpeedLimitExample.png		

Change lane
"""""""""""

Visualizes the target lane change point along the lane.

Collision
"""""""""

Shows the detected collision contact normal and direction.

Obstacle
""""""""

Shows the detected obstacle entity and reason type.

Obstacle reason types:
    * **Undefined**
    * **DefaultPath** : obstacle present along the current or next connected path.
    * **NeighborPath** : obstacle detected on a neighboring path originating from the same node.
    * **JamCase_1** : car stops before entering an intersection to avoid gridlock.
    * **FewChangeLaneCars** : conflict caused by multiple cars changing lanes simultaneously.
    * **ChangingLane** : lead vehicle is actively changing into the current lane.
    * **Intersect_1_TargetCarCloseToIntersectPoint** : conflicting car is closer to the intersection crossing point.
    * **Intersect_2_TargetCarCloseToIntersectPoint** : conflicting car is already at the intersection point.
    * **Intersect_3_OtherHasPriority** : yielding to another vehicle with higher road priority.
    * **Intersect_4_SamePriority** : vehicles have equal priority; the car closer to the intersection proceeds first.
	
No target
"""""""""

Lists vehicles currently without an assigned destination node.
	 
Settings
~~~~~~~~
	 
| **Text color** : color of the in-scene debug labels.
| **Show obstacle info** : highlights cars with active obstacles in red.
| **Show common info** : displays entity IDs above vehicles.

.. _trafficCarRaycastDebugger:

Traffic Raycast Debugger
------------------------

Visualizes the detection box volume of vehicles (:ref:`Config <trafficCarRaycastConfig>`).

	.. image:: /images/debuggers/traffic/TrafficCarRaycastDebugger.png		
	
| **Enable debug** : enables/disables raycast volume visualization.

Example
~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficCarRaycastDebuggerExample.png		

.. _trafficCarNpcObstacleDebugger:

Traffic NpcObstacle Debugger
----------------------------

Visualizes the NPC calculation area and detected pedestrian obstacles.

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebugger.png		
	
| **Enable debug** : enables/disables visualization.
| **Area color** : color of the NPC calculation bounding box.
| **Selected index** : restricts debugging to a single entity index (-1 displays all).
	
Example
~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficCarNpcObstacleDebuggerExample.png		
	
Traffic Public Debugger
-----------------------
	
Visualizes :ref:`public transport <trafficPublic>` route and schedule data.
	
	.. image:: /images/debuggers/traffic/TrafficPublicDebugger.png		
	
| **Enable debug** : enables/disables visualization.
| **Text color** : text label color.

Example
~~~~~~~

	.. image:: /images/debuggers/traffic/TrafficPublicDebuggerExample.png		
	
Traffic Light Debugger
----------------------

Visualizes the active :ref:`state <trafficLightState>` of scene :ref:`traffic light objects <trafficLightObject>`.

	.. image:: /images/debuggers/traffic/TrafficLightDebugger.png