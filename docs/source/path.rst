.. _path:

Path
=====

Path Settings
----------------

`Path` is the component to connect the :ref:`traffic nodes<trafficNode>`.
	
Cached values
~~~~~~~~~~~~
	
	.. image:: images/road/path/PathCachedValues.png
	
**Source traffic node** : source node traffic from which the path starts.
**Path connection type:**
	* **Traffic node** :
		* **Connected traffic node** : connected traffic node.
	* **Path point** :
		* **Connected path** : connected path in the custom point.
**Nodes** : node point to create curves (bezier).
**Waypoints** : point of path.
**Custom waypoints** :
**Intersects** : intersection points with other paths (baked data).
	
Settings
~~~~~~~~~~~~

	.. image:: images/road/path/PathSettings.png
		
**Path length** : path length (baked value).
.. _pathCurveType:
**Path curve type:**
	* **Straight line** : default point to point line.
	* **Bezier cube** : bezier cube curved line.
	* **Bezier quad** : bezier quad curved line.
**Path road type:**
	* **Straight road** : is used to automatically calculate lane changes by traffic.
	* **Turn road**
.. _pathTrafficType:
**Traffic type:** the type of traffic vehicle that can go on this path.
	* **Default**
	* **Tram**
	* **Traffic public**
.. _pathPriority:
**Priority** : order of crossing intersected paths (vehicle with the higher priority gets through first).
.. _pathWaypointsPerCurve:
**Waypoints count per curve** : number of waypoints in the curve segment.
**Path speed limit** : speed limit for the entire route
**Connected lane index** : connected lane index.
**Hightlight normalized length** : normalized length of the highlighted path (for editor only).
**Reversed connection side** :
	
Visual Settings
~~~~~~~~~~~~

	.. image:: images/road/path/PathVisualSettings.png

**Show info on select** : shared parameter between paths instances that automatically enables `Show info waypoints` on selecting new path.
**Show info waypoints** : show info of waypoints on the scene.
**Lock Y axis** : lock Y-axis for position handles of nodes.
**Show intersected points** : show intersected points on the scene.
**Show handles** : show position handles for nodes.
**Show edit buttons** : show edit buttons for path (add/remove nodes).
**Hightlight color** : hightlight color of the path.
**Show Y position** : show Y-position of nodes.

Buttons
~~~~~~~~~~~~

**Open path settings** : open :ref:`Path settings window<pathSettingsWindow>`.
**Open attach window** : open :ref:`Attach path window<pathAttachWindow>`.
**Create path** : generation and positioning of waypoints based on the position of the nodes and the selected curve.
**Add custom light** : custom :ref:`TrafficLightHandler<trafficLightHandler>`. will be added to the path.
**Reset speed limit** : each waypoint will be assigned a common speed limit of path.
	
.. _pathSettingsWindow:

Path advanced settings window
----------------

	.. image:: images/road/path/PathSettingsWindow1.png
	
Common settings
~~~~~~~~~~~~

:ref:`Path curve type<pathCurveType>`.
:ref:`Path traffic type<pathTrafficType>`.
:ref:`Waypoints count per curve<pathWaypointsPerCurve>`.
:ref:`Priority<pathPriority>`.
**Draw additional settings** : displays additional settings for each waypoint (`Backward movement`).

Custom settings
~~~~~~~~~~~~

**Speedlimit change type** :

Single
""""""""""""""

Multiple
""""""""""""""

All way
""""""""""""""

Custom section
""""""""""""""

.. _pathAttachWindow:

Attach path window
----------------
