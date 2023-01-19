.. _roadSegmentCreator:

Road Segment Creator
=====

`Road Segment Creator` is a tool for creating and customizing a :ref:`RoadSegment<roadSegment>`

.. contents::
   :local:

.. _roadSegmentCreatorHowToUse:

How To Use
------------

#. Create :ref:`RoadSegment<roadSegment>`.
#. Set the segment to the desired position.
#. By default, :ref:`RoadSegment<roadSegment>` prefab contains `RoadSegmentCreator` component.
#. Select :ref:`road segment type<roadSegmentCreatorGeneralSettings>`.

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorGeneralSettings.png
	
#. Adjust :ref:`general settings<roadSegmentCreatorGeneralSettings>`.
#. Adjust :ref:`custom settings<roadSegmentCreatorCustomSettings>`.
#. Customize :ref:`pedestrian node settings<roadSegmentCreatorPedestrianSettings>`.
#. Customize :ref:`light settings<roadSegmentCreatorLightSettings>`.
#. Customize :ref:`path settings<roadSegmentCreatorPathSettings>`.
	
.. _roadSegmentCreatorCustomSettings:

Custom Settings
------------

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
	
Transition Crossroad	
~~~~~~~~~~~~
 
	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadSettings.png
	
| **Direction count** : :ref:`info <roadSegmentCreatorId1>`.
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **SubTrafficNode distance from center** : :ref:`info <roadSegmentCreatorId3>`.
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionCrossroad.png
	`Example`.
	
Transition Straight Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionStraightRoadSettings.png
	
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **Node 1 offset** : :ref:`info <roadSegmentCreatorId4>`.
| **Node 2 offset** : :ref:`info <roadSegmentCreatorId5>`.
| **Traffic node height 1** : :ref:`info <roadSegmentCreatorId6>`.
| **Traffic node height 2** : :ref:`info <roadSegmentCreatorId7>`.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionStraightRoad.png
	`Example`.
	
Transition Crossroad To Oneway Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadToOneWaySettings.png
	
| **Direction count** : :ref:`info <roadSegmentCreatorId1>`.
| **Sub-lane count** : :ref:`info <roadSegmentCreatorId2>`.
| **SubTrafficNode distance from center** : :ref:`info <roadSegmentCreatorId3>`.
| **Is enter of oneway** : if it is on, it is the beginning of one-way traffic, if it is off, it is the end of one-way traffic.

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

How To Use
""""""""""""""

#. Place the custom  straight segment where you want it.
#. Place the :ref:`traffic nodes <trafficNode>` where the beginning and the end of the path.
#. Rotate the :ref:`TrafficNodes <trafficNode>` in the direction of the route (make sure that the :ref:`rotation of the nodes <trafficNodeRotation>` is set correctly).
#. Customize the number of lanes and speed limit of segment.
#. Add additional nodes to the paths if necessary **[optional step]**.
#. Rotate the nodes of paths according to the direction of the path **[optional step]**.
#. :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to surface by pressing `Snap To Surface` button if required **[optional step]**.
#. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

Custom Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomStraightCustomSettings.png
	
| **One way** : segment contains only one-way paths.
| **Lock Y axis move** : lock the Y axis to move the nodes.
| **Show Y position** : show Y position of the nodes.

Snap Node Settings
""""""""""""""

:ref:`Info <roadSegmentCreatorId11>`.

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

How To Use
""""""""""""""

#. Place the custom segment where you want it.
#. Toggle on :ref:`Custom settings <roadSegmentCreatorCustomCustomSettingsOption>` parameter.
#. Select `New node settings type` & create new :ref:`TrafficNode <trafficNode>` by pressing `Add Traffic Node` button **[optional step]**.
#. :ref:`Place <roadSegmentCreatorCustomSnapNodeSettings>` & rotate all created :ref:`TrafficNode <trafficNode>` according to your needs (make sure that the :ref:`rotation of the nodes <trafficNodeRotation>` is set correctly).
#. :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to surface by pressing `Snap To Surface` button if required **[optional step]**.
#. Open :ref:`TrafficNodePathCreator tool <trafficNodePathCreator>` to quickly create :ref:`paths <path>` between :ref:`nodes <trafficNode>`.
#. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

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
	* **Reverse snapping** : snapping object will be shifted to the edge of the default snap.
| **Auto snap custom size** : snapping value.
**Auto round rotation:** : on/off rotation snapping.
	* **Round angle** : snapping angle value.
	
.. _roadSegmentCreatorParkingBuilder:

Parking Builder
------------

A tool to quickly create a parking space. Is part of the :ref:`RoadSegmentCreator <roadSegmentCreator>` and can only be enabled in the :ref:`custom segment <roadSegmentCreatorCustomSegment>`.

How To Use
~~~~~~~~~~~~ 
	
#. Position a :ref:`custom segment <roadSegmentCreatorCustomSegment>` on the road where the parking spaces will be.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment.png
	
#. Set the size of the parking slot, the direction of the parking line and the direction of the node (:ref:`settings <roadSegmentCreatorParkingBuilderCommonSettings>`).

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings1.png
	
#. Position parking pointer where the line will start.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment2.png

#. Enter the :ref:`number of parking slots <roadSegmentCreatorParkingBuilderCommonSettings>`.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment3.png
	
#. Open :ref:`Path <roadSegmentCreatorParkingBuilderPath>` tab.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentPathTab.png
	
#. Toggle on `Show select path buttons` option.
#. Select the source path on the scene.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment4.png

#. Select `Enter` tab and press `Create` button.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings2.png
	
#. In the created path create additional waypoint nodes by pressing `+` on the scene.
	
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment6.png
	
#. Customize :ref:`Initial speed limit <roadSegmentCreatorParkingBuilderPath>` and :ref:`Node clone count <roadSegmentCreatorParkingBuilderPath>` parameters.

	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings3.png
	.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegment7.png
	
#. Repeat the same steps (8 - 10) for the :ref:`exit path <roadSegmentCreatorParkingBuilderPath>`.

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
		Created lines can be deleted in the `Created lines` tab.
			.. image:: /images/road/roadSegment/ParkingBuilder/PlaceCustomSegmentSettings7.png

Settings
~~~~~~~~~~~~ 

.. _roadSegmentCreatorParkingBuilderCommonSettings:

Common
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderCommon.png
	
| **Place TrafficNode type** : :ref:`TrafficNode type <trafficNodeSettings>`.
| **Parking TrafficNode weight** : :ref:`TrafficNode weight <trafficNodeSettings>`.
| **Node custom achieve distance** : custom distance to achieve a node (if 0 value default value will be taken).
| **Place count** : number of parking slots.
| **Parking place spacing offset** : distance between parking slots.
| **Line start point local** : local parking line start position.
| **Place size** : parking lot size.
| **Node direction** : local direction of :ref:`TrafficNode <trafficNode>` in the parking place.
| **Line direction** : local direction of parking line.
	
.. _roadSegmentCreatorParkingBuilderPath:

Path
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentCustomParkingBuilderPath.png

**Parking connection source type** :
	* **Path** [paths will be connected to the `Parking source path` (:ref:`PathPoint connection <pathPointConnection>`)]
		* **Parking source path** : path from which the created parking slot paths will start and end.
		* **Show select path buttons** : on/off display exist paths of the segment to add a parking source path.
	* **Node** [paths will be connected to the target `TrafficNode` (:ref:`TrafficNode connection <trafficNodeConnection>`)]
		* **Source TrafficNode** : node from which the created parking slot paths will start.
		* **Target TrafficNode** : node to which the paths connected from the parking place.

| **Auto recalculate parking paths** : paths ends will be recalculated when changing the position of the parking line.
| **Show path parking handles** : on/off position handles of the path.
| **Show edit path parking buttons** : on/off edit (add & remove) buttons of the path.

**Path Selection Panel:**
	* **None** : displayed `Enter` & `Exit` paths.
	* **Enter** : displayed only `Enter` paths.
		* **Initial path speed limit** : initial speed limit of `Enter` paths.
		* **Node clone count** : number of nodes in the next paths that are will clone position from source path.
	* **Exit** : displayed only `Exit` paths
		* **Initial path speed limit** : initial speed limit of exit paths.
		* **Node skip last count** : number of last nodes in the next paths that are will clone position the last nodes from source path.
	
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
	
Traffic lights
""""""""""""""

| **Show semaphore indexes** : on/off display semaphore :ref:`TrafficLightHandler <trafficLightHandler>` index around :ref:`traffic nodes <trafficNode>` and traffic lights on the scene.
| **Min TrafficNodes count for add light** : minimum number of :ref:`traffic nodes <trafficNode>` in the segment to add traffic light.
| **Add traffic light** : add traffic light to the segment.
**Selected light prefab type** : prefab of the traffic light to be added [can be changed in creator settings].
	* **Oneway**
	* **Two way**
	* **Four way**
**Light location** :
	* **Right** : will be added to the right of the :ref:`traffic nodes <trafficNode>`.
	* **Left** : will be added to the left of the :ref:`traffic nodes <trafficNode>`.
	* **Right left** : will be added on both sides of the :ref:`traffic node <trafficNode>`.
| **Traffic lights offset** : local traffic light offset relative to :ref:`traffic node <trafficNode>`.
**Light angle offset settings** :
	* **Angle index** : rotation angle index (0 - 0°, 1 - 90°, 2 - 180°, 3 - 270°).
	* **Revert** :
	
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
	#. Select desired :ref:`path <path>` on the inspector panel (it will be highlighted on the scene).
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

**Show path handles** : on/off position handles on the scene.
	* **Show edit buttons path nodes** : on/off `add` & `remove` buttons nodes on the scene.
**Show waypoints** : on/off visual circle position of the waypoint on the scene.
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
| **Even size snapping** : snapping object will be shifted to the edge of the default snap.
| **Custom snap size** : snapping value.
| **Snap surface offset** : snap surface offset.
| **Snap layer mask** : snap layermask.
| **Snap segment to surface** : snap the segment to the surface.
	
Other settings
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorOtherSettings.png
		
| **Save prefab paths** : segment save prefab path.

Buttons
""""""""""""""

| **Rotate -90°/90°** : rotate segment by 90° degree.
| **Recreate** : recreate segment.
| **Clear** : clear segment.
| **Save to prefab** : save segment to prefab

Hotkeys
~~~~~~~~~~~~ 

| **Capslock** : rotate segment by 90° degree.



	



	

