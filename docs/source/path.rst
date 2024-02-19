.. _path:

Path
=====

`Path` is a set of :ref:`waypoints <pathWaypointInfo>` along which :ref:`vehicles <trafficCar>` travel and is a connection between :ref:`traffic nodes <trafficNode>`.

How To Create
----------------

`Paths` are generated in :ref:`RoadSegment<roadSegment>` using :ref:`RoadSegmentCreator <roadSegmentCreator>` or you can add them to existing :ref:`Road Segments <roadSegment>` using the :ref:`Path Creator tool <pathCreator>`

.. _pathCustomize:

How To Customize
----------------

Settings
~~~~~~~~~~~~

There are two ways to edit:
	#. Directly in the :ref:`Inspector <pathSettings>`.
	#. Using the :ref:`Advanced Settings Window <pathSettingsWindow>`.

Nodes
~~~~~~~~~~~~

How To Move
""""""""""""""

#. Enable :ref:`Show handles <pathSettings>` option.
#. Drag the desired path handles.

How Add & Remove
""""""""""""""

#. Enable :ref:`Show handles <pathSettings>` option.
#. Enable :ref:`Show edit buttons <pathSettings>` option.
#. Press the `+` button to add or press the `x` to remove node.

Path Settings
----------------
	
.. _pathCachedValues:
	
Cached values
~~~~~~~~~~~~
	
	.. image:: /images/road/path/PathCachedValues.png
	
| **Source traffic node** : source node traffic from which the path starts.
**Path connection type:**
	* **Traffic node** :
		* **Connected traffic node** : :ref:`connected traffic node <trafficNodeConnection>`.
	* **Path point** :
		* **Connected path** : connected path in the :ref:`custom point <pathPointConnection>`.
| **Nodes** : key nodes for creating curves (Bezier).
| **Waypoints** : :ref:`waypoints <pathWaypointInfo>` of path.

.. _pathIntersects:

| **Intersects** : intersection points with other paths (:ref:`baked data<pathBakingInfo>`) (:ref:`example <roadSegmentIntersectionExample>`).
	
.. _pathSettings:
	
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

**Traffic mask group:** :ref:`group types <pathTrafficGroup>` of traffic vehicles that can go on this path.
	
.. _pathPriority:

| **Priority** : order of crossing intersected paths (vehicle with the higher priority gets through first).

.. _pathWaypointsPerCurve:

| **Waypoints count per curve** : number of waypoints in the curve segment.
| **Path speed limit** : speed limit for the entire route
| **Connected lane index** : connected lane index.
| **Hightlight normalized length** : normalized length of the highlighted path (editor only).
| **Rail** : cars entering this path will move with a :ref:`rail movement <trafficRail>`.
| **Reversed connection side** : path will be connected to the :ref:`opposite side of the node <trafficNodeConnectionInfo>`.
	
.. _pathVisualSettings:
	
Visual Settings
~~~~~~~~~~~~

	.. image:: /images/road/path/PathVisualSettings.png

Common settings
""""""""""""""

| **Show info on select** : shared parameter between paths instances that automatically enables `Show info waypoints` on selecting new path.
| **Show info waypoints** : show info of waypoints in the scene.
| **Lock Y axis** : lock Y-axis for position handles of nodes.
| **Show intersected points** : show intersected points in the scene.
| **Show handles** : show position handles for nodes.
| **Show edit buttons** : show edit buttons for path (add/remove nodes).
| **Hightlight color** : hightlight color of the path.
| **Show Y position** : show Y-position of nodes.

Curved settings
""""""""""""""

	.. image:: /images/road/path/PathCurveSettings.png

| **Draw tangent** : on/off tangents in the scene.
| **Clamp tangent** : two position handles of tangent will move together.
| **Convert to StraightLine** : converts a :ref:`Curved line <pathCurveType>` into a :ref:`Straight line <pathCurveType>`.

.. _pathPathPointVisualSettings:

Path point settings
""""""""""""""

	.. image:: /images/road/path/PathPointSettings.png

| **Auto attach path** : automatically attach the last node of the source to the connected path.
| **Show attach path buttons** : on/off connect path buttons in the scene.

Buttons
~~~~~~~~~~~~

| **Open path settings** : open :ref:`Path Settings Window<pathSettingsWindow>`.
| **Create path** : generation and positioning of waypoints based on the position of the nodes and the selected curve.
| **Add custom light** : custom :ref:`TrafficLightHandler<trafficLightHandler>` will be added to the path.
| **Reset speed limit** : each waypoint will be assigned a common speed limit of path.
	
.. _trafficNodeConnection:
	
Traffic Node connection
~~~~~~~~~~~~
	
Default connection between :ref:`traffic nodes <trafficNode>` in :ref:`road segment <roadSegment>`, used in most cases.
	
.. _pathPointConnection:
	
Path Point connection
~~~~~~~~~~~~

Is used to connect one path to another in a path in a custom point (generated by parking builder :ref:`example <roadSegmentCreatorParkingBuilderPathExample>`).

How To Use
""""""""""""""

#. Select source path in the scene.
#. Select :ref:`Path connection type <pathCachedValues>` to `Path Point` in the inspector.
#. Enable :ref:`Show attach path buttons <pathPathPointVisualSettings>`.
#. Select desired path.
#. Customize position handles of source path nodes.

.. _pathWaypointInfo:

Waypoint Info
----------------

The path is made up of these waypoints, which direct each :ref:`vehicle <trafficCar>`.

	.. image:: /images/road/path/PathNode.png

| **Speed limit** : the maximum speed of the vehicle when it reaches this waypoint.
| **Backward direction** : when this option is activated, the vehicle will reverse (:ref:`test scene <trafficTestSceneTrafficReverse>`).
| **Custom group** : override :ref:`traffic group <pathTrafficGroup>` for the current path node.

	.. note::
		You can debug the group nodes :ref:`here <pathDataViewer>`.

.. _pathTrafficGroup:

Traffic Group Info
----------------

* Each path contains a mask which, depending on the :ref:`mask type <groupMaskType>`, contains a group of the selected `TrafficGroupType`. 
* A vehicle that has the correct :ref:`TrafficGroupType <trafficCarEntityAuthoring>` can be driven or spawned on this path.
* If the vehicle enters the forbidden :ref:`path <pathWaypointInfo>` or :ref:`path node <pathWaypointInfo>`, it will automatically try to change the current lane (:ref:`test scene <trafficTestSceneTrafficGroup>`).

	.. note::
		* You can change the available types in the `Global Settings` or in the enum file:
			* **TrafficGroupType.cs**
		* You can debug the path group :ref:`here <pathDataViewer>`.
			
How To Change
~~~~~~~~~~~~

#. Open the `Global Settings` window.

	.. image:: /images/road/path/GlobalSettingsOpen.png
	
#. Select the `Traffic Group Types` tab.
	
	.. image:: /images/road/path/GlobalSettingsTab.png
	
#. Rename, remove, add groups as you wish.
#. After making any changes, click on the `Save` button.

Traffic Group Settings
~~~~~~~~~~~~

How To Create
""""""""""""""

Settings automatically created if missing in project path `Assets/Resources/Spirit604/TrafficGroupMaskSettings.asset`.

	.. image:: /images/road/path/TrafficGroupSettingsProjectPath.png
	
.. _trafficGroupSettings:

Settings
""""""""""""""	

Contains the types of default group and user-created groups.

	.. image:: /images/road/path/TrafficGroupSettings.png

.. _groupMaskType:

Mask Types
~~~~~~~~~~~~

Default
""""""""""""""

Default group of the :ref:`TrafficGroupType <pathTrafficGroup>` that defined in the :ref:`settings <trafficGroupSettings>`.

Allowed
""""""""""""""

User-selected :ref:`TrafficGroupType <pathTrafficGroup>` types that can go through the path.

Forbidden
""""""""""""""

User-selected :ref:`TrafficGroupType <pathTrafficGroup>` types that are forbidden the path (not selected in the list is allowed).

Custom Group
""""""""""""""

Custom group of :ref:`TrafficGroupType <pathTrafficGroup>` that defined in the :ref:`settings <trafficGroupSettings>`.

.. _pathSettingsWindow:

Advanced Settings Window
----------------

How To Open
~~~~~~~~~~~~

#. Select the `Path`.
#. Press `Open Path Settings` button in the inspector.

Settings
~~~~~~~~~~~~

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow1.png
	
Common settings
~~~~~~~~~~~~

| :ref:`Path curve type<pathCurveType>`.
| :ref:`Traffic mask group <pathTrafficGroup>`.
| :ref:`Waypoints count per curve<pathWaypointsPerCurve>`.
| :ref:`Priority<pathPriority>`.
| :ref:`Draw additional settings<pathDrawAdditionalSettingsExample>` : displays additional settings for each waypoint (`Backward Movement`, `Traffic Group`).

Custom settings
~~~~~~~~~~~~

**Speedlimit change type** :

Single
""""""""""""""

`Single` - change each waypoint one at a time.

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow1.png
	
.. _pathDrawAdditionalSettingsExample:
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindow2.png
	`Draw additional settings enabled.`

Multiple
""""""""""""""

`Multiple` - the speed limit will be changed on the selected section.
	
	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowMultiple1.png

**Multiple node change type:**
 	* **Fixed** : all waypoints change speed limit.
 	* **Interpolate** : speed will be interpolated from the beginning of the section to the end.
		* **Interpolate type** :
			* **Node index** : speed is interpolated relative to the waypoint index.
			* **Distance** : speed is interpolated relative to the position of the waypoint.
		* **Start speed limit** : initial speed limit of the section.
		* **End speed limit** : end speed limit of the section.
		
**How to use:**
	* Select the start and end of the section in the window or switch on the `Draw Select Buttons` and select the start (`S`) and end (`E`) in the scene.
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
	* Click the `Set Speed Limit` button.
		.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowAllway2.png
		`Result.`

Custom section
""""""""""""""

`Custom section` - the section with the custom speed is automatically generated depending on the parameters.

	.. image:: /images/road/path/pathSettingsWindow/PathSettingsWindowSection1.png
	
**Path section type:**
	* **Start of path** : section will be created at the beginning of the path.
	* **End of path** : section will be created at the end of the path.
	* **All path** : section will be generated all along the path.
**Path section create type:**
	* **Clear path nodes** : waypoints will be generated anew each time a section is created.
	* **Use exist nodes** : existing waypoints will be used for the section.
| **Section length** : length of the created section.
| **Section waypoints** : number of waypoints of the created section.
| **Start speed limit** : initial speed of the section.
| **End speed limit** : end speed of the section.

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
How to :ref:`bake <bakingInfo>`.

**Baked Data:**
	* :ref:`Path Length<pathLength>` (is used to calculate obstacles on the path by `TrafficCarObstacleSystem`).
	* :ref:`Intersection data <pathIntersects>` (:ref:`segment baking info<roadSegmentBakingInfo>`) (used by `TrafficCarObstacleSystem` to order the intersection of intersecting paths).