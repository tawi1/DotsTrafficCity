.. _path:

Path
=====

`Path` is the component to connect the :ref:`traffic nodes<trafficNode>`.

How To Create
----------------

`Paths` are generated in :ref:`RoadSegment<roadSegment>` with :ref:`RoadSegmentCreator<roadSegmentCreator>` or you can add them to existing :ref:`road segments<roadSegment>` with :ref:`TrafficNodePathCreator<trafficNodePathCreator>`

Path Settings
----------------
	
Cached values
~~~~~~~~~~~~
	
	.. image:: /images/road/path/PathCachedValues.png
	
| **Source traffic node** : source node traffic from which the path starts.
**Path connection type:**
	* **Traffic node** :
		* **Connected traffic node** : connected traffic node.
	* **Path point** :
		* **Connected path** : connected path in the :ref:`custom point<pathPointConnection>`.
| **Nodes** : node point to create curves (bezier).
| **Waypoints** : point of path.
| **Custom waypoints** :

.. _pathIntersects:

| **Intersects** : intersection points with other paths (:ref:`baked data<pathBakingInfo>`) (:ref:`example <roadSegmentIntersectionExample>`).
	
Settings
~~~~~~~~~~~~

	.. image:: /images/road/path/PathSettings.png
		
.. _pathLength:
		
| **Path length** : path length (:ref:`baked value<pathBakingInfo>`).

.. _pathCurveType:

**Path curve type:**
	* **Straight line** : default point to point line.
	* **Bezier cube** : bezier cube curved line.
	* **Bezier quad** : bezier quad curved line.
	
.. _pathRoadType:
	
**Path road type:**
	* **Straight road** : is used to automatically calculate lane changing by traffic.
	* **Turn road**
	
.. _pathTrafficType:

**Traffic type:** the type of traffic vehicle that can go on this path.
	* **Default**
	* **Tram**
	* **Traffic public**
	
.. _pathPriority:

| **Priority** : order of crossing intersected paths (vehicle with the higher priority gets through first).

.. _pathWaypointsPerCurve:

| **Waypoints count per curve** : number of waypoints in the curve segment.
| **Path speed limit** : speed limit for the entire route
| **Connected lane index** : connected lane index.
| **Hightlight normalized length** : normalized length of the highlighted path (for editor only).
| **Reversed connection side** : path will be connected to the :ref:`opposite side of the node<trafficNodeConnectionInfo>`.
	
Visual Settings
~~~~~~~~~~~~

	.. image:: /images/road/path/PathVisualSettings.png

| **Show info on select** : shared parameter between paths instances that automatically enables `Show info waypoints` on selecting new path.
| **Show info waypoints** : show info of waypoints on the scene.
| **Lock Y axis** : lock Y-axis for position handles of nodes.
| **Show intersected points** : show intersected points on the scene.
| **Show handles** : show position handles for nodes.
| **Show edit buttons** : show edit buttons for path (add/remove nodes).
| **Hightlight color** : hightlight color of the path.
| **Show Y position** : show Y-position of nodes.

Buttons
~~~~~~~~~~~~

| **Open path settings** : open :ref:`Path Settings Window<pathSettingsWindow>`.
| **Create path** : generation and positioning of waypoints based on the position of the nodes and the selected curve.
| **Add custom light** : custom :ref:`TrafficLightHandler<trafficLightHandler>` will be added to the path.
| **Reset speed limit** : each waypoint will be assigned a common speed limit of path.
	
	
.. _trafficNodeConnection:
	
Traffic Node connection
~~~~~~~~~~~~
	
	
.. _pathPointConnection:
	
Path Point connection
~~~~~~~~~~~~






.. _pathSettingsWindow:

Path advanced settings window
----------------

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow1.png
	
Common settings
~~~~~~~~~~~~

| :ref:`Path curve type<pathCurveType>`.
| :ref:`Path traffic type<pathTrafficType>`.
| :ref:`Waypoints count per curve<pathWaypointsPerCurve>`.
| :ref:`Priority<pathPriority>`.
| :ref:`Draw additional settings<pathDrawAdditionalSettingsExample>` : displays additional settings for each waypoint (`Backward Movement`).

Custom settings
~~~~~~~~~~~~

**Speedlimit change type** :

Single
""""""""""""""

`Single` - change each waypoint one by one.

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow1.png
	
.. _pathDrawAdditionalSettingsExample:
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow2.png
	`Draw additional settings enabled.`

Multiple
""""""""""""""

`Multiple` - speed limit will be changed on the selected section.
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple1.png

**Multiple node change type:**
 	* **Fixed** : all waypoints change speed limit.
 	* **Interpolate** : speed will be interpolated from the beginning of the section to the end.
		* **Interpolate type** :
			* **Node index** : speed is interpolated regarding to the waypoint index.
			* **Distance** : speed is interpolated regarding the position of the waypoint.
		* **Start speed limit** : initial speed limit of the section.
		* **End speed limit** : end speed limit of the section.
		
**How to use:**
	* Select the start and end of the section in the window or turn on `Draw Select Buttons` and select start (`S`) and end (`E`) on the scene.
	* Set the parameter `Selected Path Speed Limit` to the value you need.
		.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple5.png
	* Click `Set Speed Limit`.
		.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple6.png
		`Result.`
				
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple2.png
	`Source path example.`
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple3.png
	`Draw Select Buttons enabled "S" (start) "E" (End) example.`
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple4.png
	`Path section selected (green circles start & end of section) example.`

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple7.png
	`Interpolating settings example.`
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple8.png
	`Interpolating result.`

All way
""""""""""""""

`All way` - all path waypoints will change the speed limit according to the set options.

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowAllway1.png

**Multiple node change type:**
 	* **Fixed** : all waypoints change speed limit.
 	* **Interpolate** : speed will be interpolated from the beginning of the section to the end.
		* **Interpolate type** :
			* **Node index** : speed is interpolated regarding to the waypoint index.
			* **Distance** : speed is interpolated regarding the position of the waypoint.
		* **Start speed limit** : initial speed limit of the section.
		* **End speed limit** : end speed limit of the section.

**How to use:**
	* Set the parameter `Selected Path Speed Limit` to the value you need.
		.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowAllway1.png
	* Click `Set Speed Limit`.
		.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowAllway2.png
		`Result.`

Custom section
""""""""""""""

`Custom section` - section with the custom speed will be automatically generated depending on the parameters.

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowSection1.png
	
**Path section type:**
	* **Start of path** : section will be created at the beginning of the path.
	* **End of path** : section will be created at the end of the path
	* **All path** : section will be generated all along the path.
**Path section create type:**
	* **Clear path nodes** : waypoints will be generated anew each time a section is created.
	* **Use exist nodes** : existing waypoints will be used for the section.
| **Section length** : length of the created section.
| **Section waypoints** : number of waypoints of the created section.
| **Start speed limit** : initial speed of the section.
| **End speed limit** : end speed of the section

**How to use:**
	* Set all parameters.
	* Click `Create SpeedLimit Segment`.
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowSection2.png
	`Source path.`
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowSection3.png
	`Result.`
	
.. _pathBakingInfo:
	
Baking Info
----------------

Each `path` bakes the data to speed up the entity conversion.
Baking is activated in the :ref:`road parent<roadParent>`.

**Baked Data:**
	* :ref:`Path Length<pathLength>` (is used to calculate obstacles on the path by `TrafficCarObstacleSystem`).
	* :ref:`Intersects data <pathIntersects>` (:ref:`segment baking info<roadSegmentBakingInfo>`) (is used to order the crossing of intersecting paths by `TrafficCarObstacleSystem`).