.. _roadSegmentCreator:

Road Segment Creator
=====

`Road Segment Creator` is a tool for creating and customizing a :ref:`RoadSegment<roadSegment>`

.. contents::
   :local:

.. _roadSegmentCreatorHowToUse:

How To Use
------------

`Youtube tutorial. <https://youtu.be/wNa8GgBPyqU>`_

#. Create a :ref:`RoadSegment<roadSegment>`.
#. Place the segment at the desired position.
#. By default, :ref:`RoadSegment<roadSegment>` prefab contains `RoadSegmentCreator` component.
#. Select the :ref:`Road segment type <roadSegmentCreatorGeneralSettings>`.

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorGeneralSettings.png
	
#. Adjust :ref:`general settings<roadSegmentCreatorGeneralSettings>`.
#. Adjust :ref:`custom settings<roadSegmentCreatorCustomSettings>`.
#. Customize :ref:`pedestrian node settings<roadSegmentCreatorPedestrianSettings>`.
#. Customize :ref:`light settings<roadSegmentCreatorLightSettings>`.
#. Customize :ref:`path settings<roadSegmentCreatorPathSettings>`.
#. Add :ref:`RoadSegment<roadSegment>` to the :ref:`RoadParent <roadParent>` as children.
	
.. _roadSegmentCreatorCustomSettings:

Custom Settings
------------

`Youtube tutorial. <https://youtu.be/wNa8GgBPyqU>`_

Default Crossroad
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorDefaultCrossroadSettings.png
	
| **Direction count** : :ref:`info <roadSegmentCreatorId1>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentDefault.png
	`Example`.
	
Turn Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTurnRoadSettings.png
	
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Additional local angle 1** : :ref:`info <roadSegmentCreatorId8>`.
| **Additional local angle 2** : :ref:`info <roadSegmentCreatorId9>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTurnRoad.png
	`Example`.

	
Straight Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentStraightSettings.png
	
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Traffic node height 1** : :ref:`info <roadSegmentCreatorId6>`.
| **Traffic node height 2** : :ref:`info <roadSegmentCreatorId7>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentStraight.png
	`Example`.
	
Merge Crossroad	
~~~~~~~~~~~~
 
	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadSettings.png
	
| **Direction count** : :ref:`info <roadSegmentCreatorId1>`.
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **SubTrafficNode distance from center** : :ref:`info <roadSegmentCreatorId3>`.
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionCrossroad.png
	`Example`.
	
Merge Straight Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionStraightRoadSettings.png
	
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Traffic node height 1** : :ref:`info <roadSegmentCreatorId6>`.
| **Traffic node height 2** : :ref:`info <roadSegmentCreatorId7>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionStraightRoad.png
	`Example`.
	
Merge Crossroad To Oneway Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadToOneWaySettings.png
	
| **Direction count** : :ref:`info <roadSegmentCreatorId1>`.
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **SubTrafficNode distance from center** : :ref:`info <roadSegmentCreatorId3>`.
| **Is enter of oneway** : if it is on, it is the start of one-way traffic, if it is off, it is the end of one-way traffic.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionCrossroadToOneWay.png
	`Example`.
	
Oneway Straight
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentOneWayStraightSettings.png
	
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Traffic node height 1** : :ref:`info <roadSegmentCreatorId6>`.
| **Traffic node height 2** : :ref:`info <roadSegmentCreatorId7>`.
| **Should revert direction** : :ref:`info <roadSegmentCreatorId10>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentOneWayStraight.png
	`Example`.
	
Oneway Turn
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentOneWayTurnSettings.png
	
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Additional local angle 1** : :ref:`info <roadSegmentCreatorId8>`.
| **Additional local angle 2** : :ref:`info <roadSegmentCreatorId9>`.
| **Should revert direction** : :ref:`info <roadSegmentCreatorId10>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentOneWayTurn.png
	`Example`.
		
.. _roadSegmentCreatorCustomStraight:

Custom Straight Road
~~~~~~~~~~~~ 

Creator for creating straight roads of any shape.

`Youtube tutorial. <https://youtu.be/JbhGYxVscew>`_

How To Use
""""""""""""""

#. Place the custom  straight segment where you want it.
#. Place the :ref:`traffic nodes <trafficNode>` at the start and the end of the path (or expand the road by holding `left-shift` key and clicking the `left-mouse` button).
#. Rotate the :ref:`TrafficNodes <trafficNode>` in the direction of the route (make sure that the :ref:`rotation of the nodes <trafficNodeRotation>` is set correctly).
#. Adjust the number of lanes and the speed limit of the segment.
#. If necessary, add more additional nodes to the paths (by pressing `+` in the scene) **[optional step]**.
#. Rotate the nodes of the paths according to the direction of the path **[optional step]**.
#. :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to the surface by pressing the `Snap To Surface` button if necessary **[optional step]**.
#. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

Custom Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightCustomSettings.png
	
| **One way** : segment contains only one-way paths.
| **Lock Y axis move** : lock the Y axis to move the nodes.
| **Show Y position** : show Y position of the nodes.

Snap Node Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightSnapNodeSettings.png
	
:ref:`Info <roadSegmentCreatorId11>`.
	
Snap Surface Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightSnapSurfaceSettings.png

| **Snap surface offset** : offset between snap point and the node (Y axis).

**Node Buttons** : which node you want to snap to.
	* All
	* Node1
	* Node2
	
**Buttons:** 
	* Snap to surface: snap selected nodes to the surface.
	
.. _snapLine:
	
Snap Line Settings
""""""""""""""

Creates additional :ref:`path nodes <pathWaypointInfo>` along the curved meshes of the collider to make the :ref:`path <path>` follow the shape of the collider **(v 1.0.4+)**.  

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightSnapLineSettings.png

| **Angle threshold** : minimum angle between normal faces to create new :ref:`path nodes <pathWaypointInfo>`.
| **Min waypoint offset** : min offset between generated :ref:`path nodes <pathWaypointInfo>`.
| **Snap surface offset** : offset between snap point and the node (Y axis).

.. only:: builder_html

	.. image:: /images/road/roadSegment/creator/SnapLineExample.gif
	`Example.`

.. _roadSegmentCreatorCustomStraightPathSettings:

Path Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightPathSettings.png
	
| **Show edit buttons path nodes** : on/off edit (add & remove) button paths of node.
| **Show traffic node handles** : on/off traffic node position handles.
| **Show traffic node forward** : on/off display of node's forward direction.
| **Speedlimit** : speed limit for all paths of the segment.

Examples
""""""""""""""
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentCustomStraight.png
	`Source segment example.`
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentCustomStraight2.png
	`Complex shape example.`
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentCustomStraightSnapExample.png
	`Surface snapping example.`
		
.. _roadSegmentCreatorCustomSegment:

Custom Segment 
~~~~~~~~~~~~ 

Creator for creating segments of any shape and complexity.

`Youtube tutorial. <https://youtu.be/AMrGJ7YGBNo>`_

How To Use
""""""""""""""

#. Place the custom segment where you want it.
#. Toggle on :ref:`Custom settings <roadSegmentCreatorCustomCustomSettingsOption>` parameter.
#. Select the `New node settings type` & create a new :ref:`TrafficNode <trafficNode>` by pressing the `Add Traffic Node` button **[optional step]**.
#. :ref:`Place <roadSegmentCreatorCustomSnapNodeSettings>` & rotate all created :ref:`TrafficNode <trafficNode>` according to your needs (make sure that the :ref:`rotation of the nodes <trafficNodeRotation>` is set correctly).
#. :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to the surface by pressing the `Snap To Surface` button if required **[optional step]**.
#. Open the :ref:`PathCreator tool <pathCreator>` to quickly create :ref:`paths <path>` between :ref:`nodes <trafficNode>`.
#. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

	.. note:: You can convert any :ref:`default template <roadSegmentCreatorCustomSettings>` to `Custom Segment`_ in the `Other settings`_ tab.

New Node Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomNewNodeUniqueSettings.png

	
.. _roadSegmentCreatorCustomCustomSettingsOption:
	
| **Custom settings** : on/off custom settings for advanced node customization.

New node settings type [custom settings enabled] new :ref:`TrafficNode <trafficNode>` will be created like:
	* **Prefab** : new prefab.
	* **Unique** : created with unique defined :ref:`settings <trafficNodeSettings>`.
	* **Copy last** : will be created with the settings of the last created node.
	* **Copy selected** : will be created with the settings of the selected node.
		* **Copy node index**
		
Node Handles
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentNodeHandles.png
	
| **Show traffic node handles** : on/off handles of :ref:`TrafficNodes <trafficNode>`
| **Show traffic node forward** : on/off display of :ref:`TrafficNode <trafficNode>` forwading.
	
Parking Builder
""""""""""""""

:ref:`Parking Builder info <roadSegmentCreatorParkingBuilder>`.
	
Custom Settings
""""""""""""""
	
	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomCustomSettings.png
	
| **Lock Y axis move** : lock the Y axis to move the nodes.
| **Show Y position** : show Y position of the nodes.
	
.. _roadSegmentCreatorCustomSnapNodeSettings:

Snap Node Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomSnapNodeSettings.png
	
:ref:`Info <roadSegmentCreatorId11>`.
	
Custom TrafficNode Editor Window
""""""""""""""
		
Window that you can configure each :ref:`TrafficNode settings <trafficNodeSettings>`. :ref:`Custom settings <roadSegmentCreatorCustomCustomSettingsOption>` should be enabled.

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomTrafficNodeEditorWindow.png
	
	
Examples
""""""""""""""

	.. image:: /images/road/roadSegment/examples/RoadSegmentCustomExample.png
	`Example`.
	
Settings Description
~~~~~~~~~~~~ 

Common
""""""""""""""

.. _roadSegmentCreatorId1:

| **Direction count** : number of sides of the crossroad.

.. _roadSegmentCreatorId2:

| **Sub-lane count** : number of sub-lanes (sub-lane is a lane with a different number of bands from the main lane count).

.. _roadSegmentCreatorId3:

| **SubTrafficNode distance from center** : distance between the `SubTrafficNode` (node that contains a sub-lane) and the center of the segment.

.. _roadSegmentCreatorId4:

| **Node 1 offset** : node 1 offset on the X-axis.

.. _roadSegmentCreatorId5:

| **Node 2 offset** : node 2 offset on the X-axis.

.. _roadSegmentCreatorId6:

| **Traffic node height 1** :  node 1 offset on the Y-axis.

.. _roadSegmentCreatorId7:

| **Traffic node height 2** : node 2 offset on the Y-axis.

.. _roadSegmentCreatorId8:

| **Additional local angle 1** : additional node 1 rotation angle.

.. _roadSegmentCreatorId9: 

**Additional local angle 2** : additional node 2 rotation angle.

.. _roadSegmentCreatorId10:

**Should revert direction** : direction of the crossroad lanes will be reversed

.. _roadSegmentCreatorId11:

Snap Node Settings
""""""""""""""

**Snap object type:**
	* **All** : snap `TrafficNode` & `Path node`.
	* **Traffic node** : only `TrafficNode`.
	* **Path node** : only `Path node`.
	
**Auto-snap position** on/off position snapping.
	* **Add half offset** : the snapped object is shifted by half of the set snapping size.
	
| **Auto snap custom size** : snapping value.
**Auto round rotation:** : on/off rotation snapping.
	* **Round angle** : snapping angle value.

Components
------------

.. _roadSegmentCreatorGeneralSettings:

General settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorGeneralSettings.png

| **Lane count** : number of lanes.
| **Lane width** : lane width.
| **Crossroad width** : distance between :ref:`traffic nodes <trafficNode>`.
| **Path corner offset** : offset to change the rotation angle of curved paths.

Custom settings
~~~~~~~~~~~~ 

:ref:`Custom settings <roadSegmentCreatorCustomSettings>`.

.. _roadSegmentCreatorPedestrianSettings:

Pedestrian node settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorGeneralSettings.png	

| **Add pedestrian nodes** : add a :ref:`pedestrian nodes <pedestrianNode>` to the segment.
| **Unique crosswalk offset** : set up a unique offset for the selected crosswalk.
| **Crosswalk offset** : set up a common offset for the crosswalks.
| **Pedestrian route width** : :ref:`pedestrian route width <pedestrianNodeSettings>`.
| **Custom crosswalk** : on/off selected crosswalk.
| **Has crosswalk** : on/off :ref:`crosswalk <trafficNodeSettings>` for pedestrians.

**Pedestrian corner connection type:**
	* **Disabled**
	* **Corner** : will be created corner :ref:`pedestrian node <pedestrianNode>` to connect crosswalks.
	* **Straight** : crosswalks will be connected directly.

.. _roadSegmentCreatorLightSettings:

Light settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorLightSettings.png
	
`Youtube tutorial. <https://youtu.be/r85kMJ4BL5E>`_
	
How To Use
""""""""""""""

#. Turn on traffic light option.
#. Select `Light prefab type`.
#. Set the traffic light offset or enable `Light handle type`.
#. If you want to configure the traffic lights individually, select the `Node` button.
	
Traffic lights
""""""""""""""

| **Show light indexes** : on/off display light :ref:`TrafficLightHandler <trafficLightHandler>` index around :ref:`traffic nodes <trafficNode>` and traffic lights in the scene.
| **Min TrafficNodes count for add light** : minimum number of :ref:`traffic nodes <trafficNode>` in the segment to add traffic light.
| **Add traffic light** : add traffic light to the segment.

**Light handle type:** 
	* **None**
	* **Position** : enable position handle for traffic lights.
	* **Rotation** : enable rotation handle for traffic lights.
	
**Selected light prefab type** : prefab of the traffic light to be added [can be changed in creator settings].
	* **Oneway**
	* **Two way**
	* **Four way**
	
**Light location** :
	* **Right** : will be added to the right of the :ref:`traffic nodes <trafficNode>`.
	* **Left** : will be added to the left of the :ref:`traffic nodes <trafficNode>`.
	* **Right left** : will be added on both sides of the :ref:`traffic node <trafficNode>`.
	
| **Traffic lights offset** : local traffic light offset relative to :ref:`traffic node <trafficNode>`.

**Light angle offset settings:** 
	* **Angle offset** : local rotation angle of the traffic light.
	* **Flip index** : switches to the opposite :ref:`light index <trafficLightIndex>` in the traffic light.
	
Pedestrian lights
""""""""""""""

| **Add pedestrian lights** : add pedestrian light to the segment.
| **Pedestrian light offset** : local pedestrian light offset relative to :ref:`traffic node <trafficNode>`
| **Pedestrian angle offset** : pedestrian light rotation angle offset.
	
.. _roadSegmentCreatorPathSettings:

Path settings
~~~~~~~~~~~~ 
	
	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorPathSettings.png
	
Node selection panel
""""""""""""""

**How to customize path:**
	#. Select `TrafficNode` on the inspector panel.
	#. Select desired :ref:`path <path>` on the inspector panel (it will be highlighted in the scene).
	#. Adjust the position of the path nodes (make sure :ref:`path handles <roadSegmentCreatorPathSceneSettings>` is enabled).
	#. Press `Open Path Settings` button to customize :ref:`Path settings window<pathSettingsWindow>`.
	
Road settings
""""""""""""""

**StraightRoad settings:** [:ref:`settings <pathSettings>` for straight paths of the segment]
	* **Waypoint Straightroad count** 
	* **Straight road path speed limit** 
	* **Straight road priority** 

**TurnRoad settings:** [:ref:`settings <pathSettings>` for turn paths of the segment]
	* **Turn curve type** 
	* **Waypoint turn curve count** 
	* **Turnroad path speed limit** 
	* **Turnroad priority** 

.. _roadSegmentCreatorPathSceneSettings:

Scene settings
""""""""""""""

**Show path handles** : on/off position handles in the scene.
	* **Show edit buttons path nodes** : on/off `add` & `remove` buttons nodes in the scene.
**Show waypoints** : on/off visual circle position of the waypoint in the scene.
	* **Show waypoints info** : on/off info of waypoints (local index, speedlimit).

Turn connection settings
""""""""""""""

| **Custom node turn settings** : on/off the turn settings for each :ref:`traffic node <trafficNode>`.
| **Left turn count** : number of left turns from the :ref:`traffic node <trafficNode>`.
| **Right turn count** : number of right turns from the :ref:`traffic node <trafficNode>`.
| **Lane left turn connection count** : number of connections to the left from the lane traffic lane.
| **Lane right turn connection count** : number of connections to the right from the lane traffic lane.

.. _roadSegmentCreatorSegmentSettings:

Segment handler settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorSegmentHandlerSettings.png
	
| **Show segment position handle** : on/off position handle for segment.
| **Snap segment position** : on/off snap segmant position.
| **Add half offset** : the snapped object is shifted by half of the set snapping size.
| **Custom snap size** : snapping value.
| **Snap surface offset** : snap surface offset.
| **Snap layer mask** : snap layermask.
| **Snap segment to surface** : snap the segment to the surface.
	
Other settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorOtherSettings.png
		
| **Merge segment** : opens the merge segment tool.
| **Convert to custom** : converts the current segment to :ref:`custom segment <roadSegmentCreatorCustomSegment>`.

| **Save prefab paths** : segment save prefab path.
| **Save to prefab** : save segment to prefab.

Buttons
""""""""""""""

| **Rotate -90°/90°** : rotate segment by 90° degree.
| **Recreate** : recreate segment.
| **Clear** : clear segment.

Hotkeys
~~~~~~~~~~~~ 

| **Capslock** : rotate segment by 90° degree.


.. _roadSegmentCreatorParkingBuilder:

Parking Builder
------------

A tool to quickly create a parking space. Is part of the :ref:`RoadSegmentCreator <roadSegmentCreator>` and can only be enabled in the :ref:`custom segment <roadSegmentCreatorCustomSegment>`.

`Youtube tutorial. <https://youtu.be/1F-8J0WC83Y>`_

How To Use
~~~~~~~~~~~~ 
		
#. Position a :ref:`custom segment <roadSegmentCreatorCustomSegment>` on the road where the parking spaces will be.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment.png
		
#. Set the size of the parking slot (:ref:`settings <roadSegmentCreatorParkingBuilderCommonSettings>`).

#. Enable position handle

	.. image:: /images/road/roadSegment/ParkingBuilder/ParkingBuilderExample1.png
		
#. Position the parking pointer where you want the line to start.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment2.png
	
#. Enable rotation handle and set the rotation of the parking slot by dragging a circle in the scene.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/ParkingBuilderExample2.png
	
#. Set the object parking line to `parking line` and rotate the direction of the parking line by dragging a circle in the scene.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/ParkingBuilderExample3.png
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings1.png

#. Enter the :ref:`number of parking slots <roadSegmentCreatorParkingBuilderCommonSettings>`.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment3.png
	
#. Open the :ref:`Path <roadSegmentCreatorParkingBuilderPath>` tab.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentPathTab.png
	
#. Toggle on `Show select path buttons` option.
#. Select the source path in the scene.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment4.png

#. Select the `Enter` tab and press the `Create` button.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings2.png
	
#. In the created path create additional waypoint nodes by pressing `+` in the scene.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment6.png	

#. Customize :ref:`Traffic Group <pathTrafficGroup>`, :ref:`Initial speed limit <roadSegmentCreatorParkingBuilderPath>` and :ref:`Node Clone Count <roadSegmentCreatorParkingBuilderPath>` parameters.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings3.png
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment7.png
	
#. Open the `Offsets` tab and adjust the position handle for each node individually if required **[optional]**.		
#. Repeat the same steps (11 - 14) for the :ref:`exit path <roadSegmentCreatorParkingBuilderPath>`.

	.. _roadSegmentCreatorParkingBuilderPathExample:
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment10.png
	
#. Open :ref:`Pedestrian <roadSegmentCreatorParkingBuilderPedestrian>` tab.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings5.png
	
#. Customize `Weight`, `Parking node offset` and `Parking enter node offset`

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment11.png
	`Blue circle - enter parking car PedestrianNode. Green circle - default PedestrianNode linked to the parking PedestrianNode.` 
		
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment12.png
	`Preview parking line result.`
	
#. Press `Create Line` button.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment13.png
	`Create line result.`
	
#. :ref:`Connect the pedestrian nodes <pedestrianNodeCreator>` to the :ref:`pedestrian nodes <pedestrianNode>` of the city.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment14.png
	
	.. note::
		Created lines can be edited or deleted in the `Created lines` tab.
			.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings7.png

Settings
~~~~~~~~~~~~ 

.. _roadSegmentCreatorParkingBuilderCommonSettings:

Common
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderCommon.png

| **Place count** : number of parking slots.
| **Parking place spacing offset** : distance between parking slots.

**Line object type:** 
	* **Parking place** : handle parking place.
	* **Parking line** : handle parking line.
	
**Handles:**
	* **None** : no handles.
	* **Position** : enabled position handle for the place or line.
	* **Rotation** : enabled rotation handle for the place or line.
	
| **Line start point local** : local parking line start position.
| **Place size** : parking lot size.
| **Node direction** : local direction of the :ref:`TrafficNode <trafficNode>` in the parking place.
| **Line direction** : local direction of the parking line.
	
.. _roadSegmentCreatorParkingBuilderPath:

Path
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderPath.png

**Parking connection source type** :
	* **Path** [paths will be connected to the `Parking source path` (:ref:`PathPoint connection <pathPointConnection>`)]
		* **Parking source path** : path from which the created parking slot paths will start and end.
		* **Show select path buttons** : on/off display exist paths of the segment to add a parking source path.
	* **Node** [paths will be connected to the selected `TrafficNodes` (:ref:`TrafficNode connection <trafficNodeConnection>`)]
		* **Source TrafficNode** : node from which the created parking slot paths will start.
		* **Target TrafficNode** : node to which the paths connected from the parking place.
	* **Single node** [paths will be connected to the selected single `TrafficNode` (same node for enter & exit paths)]
		* **Source TrafficNode** : enter & exit :ref:`TrafficNode <trafficNode>` for parking :ref:`paths <path>` are the same.

| **Auto recalculate parking paths** : paths ends will be recalculated when changing the position of the parking line.

**Rail type:**
	* **None** : :ref:`Rail Movement <trafficRail>` is disabled.
	* **Enter only** : the vehicles entering the car park have a :ref:`Rail Movement <trafficRail>`.
	* **Exit only** : the vehicles leaving the car park have a :ref:`Rail Movement <trafficRail>`.
	* **Enter & exit** : enter & exit paths have a :ref:`Rail Movement <trafficRail>`.

| **Traffic mask group** : :ref:`group <pathTrafficGroup>` of the vehicles that allowed on the parking.
| **Show edit path parking buttons** : on/off edit (add & remove) buttons of the path.

**Handles Panel:**
	* **None** : handles disabled.
	* **Handles** : position handles of the path enabled for first parking place.
	* **Offsets** : position handles for all parking places.
	
**Path Selection Panel:**
	* **None** : displayed `Enter` & `Exit` paths.
	* **Enter** : displayed only `Enter` paths.
		* **Initial path speed limit** : initial speed limit of `Enter` paths.
		* **Node clone count** : number of nodes in the next paths that are will clone position from source path.
	* **Exit** : displayed only `Exit` paths
		* **Initial path speed limit** : initial speed limit of exit paths.
		* **Node skip last count** : number of last nodes in the next paths that are will clone position the last nodes from source path.
		
Node
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderNode.png

| **Place TrafficNode type** : :ref:`TrafficNode type <trafficNodeSettings>`.
| **Parking TrafficNode weight** : :ref:`TrafficNode weight <trafficNodeSettings>`.
| **Node custom achieve distance** : custom distance to achieve a node (if 0 value default value will be taken).
	
.. _roadSegmentCreatorParkingBuilderPedestrian:
	
Pedestrian
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderPedestrian.png

| **Add parking pedestrian nodes** : add an :ref:`entry parking node <pedestrianNode>` and a :ref:`node <pedestrianNode>` linking it. 
| **Parking pedestrian node type** : :ref:`parking node type <pedestrianNodeSettings>`.
| **Auto connect nodes** : auto connect created entry parking node and nearby created node.
| **Parking pedestrian node weight** : :ref:`weight <pedestrianNodeSettings>` entry parking node.
| **Parking node offset** : :ref:`entry parking node <pedestrianNode>` offset relative to :ref:`traffic nodes <trafficNode>`.
| **Parking enter node offset** : :ref:`node <pedestrianNode>` that connected to :ref:`entry parking node <pedestrianNode>` relative to :ref:`traffic nodes <trafficNode>`.



	



	

