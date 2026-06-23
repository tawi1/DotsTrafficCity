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
#. Select the :ref:`Road segment type <roadSegmentCreatorGeneralSettings>` depending on the :ref:`shape <roadSegmentCreatorCustomSettings>` of your intersection.
	* :ref:`Standard shape <roadSegmentCreatorCustomSettings>` used for the most common shapes (T-cross, X-cross & etc).
	* :ref:`Custom segment <roadSegmentCreatorCustomSegment>` used for intersection with custom shape.
	* :ref:`Custom straight <roadSegmentCreatorCustomStraight>` used on straight roads with curves or long straight roads.

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorGeneralSettings.png

#. In the other tab, you can convert any :ref:`Standard shape <roadSegmentCreatorCustomSettings>` segment to a :ref:`Custom segment <roadSegmentCreatorCustomSegment>` for more flexibility (also check out the new :ref:`Auto-Crossroads <roadSegmentCreatorAuto>` feature for automatic crossroad generation).
#. In the :ref:`general settings<roadSegmentCreatorGeneralSettings>`, adjust lane count, lane width, crossroad width.
#. In the :ref:`custom settings<roadSegmentCreatorCustomSettings>`, adjust settings according its type.
#. In the :ref:`pedestrian node settings<roadSegmentCreatorPedestrianSettings>`, you can customize pedestrian crosswalks.
#. In the :ref:`light settings<roadSegmentCreatorLightSettings>`, you can set offsets of the traffic lights or disable them.
#. In the :ref:`path settings<roadSegmentCreatorPathSettings>`, you can enable traffic node handles, adjust speed limit & waypoints of the paths of the created intersection.
#. Add :ref:`RoadSegment<roadSegment>` to the :ref:`RoadParent <roadParent>` as children.
	
.. _roadSegmentCreatorCustomSettings:

Standard Shapes
------------

`Youtube tutorial. <https://youtu.be/wNa8GgBPyqU>`_

Default Crossroad
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadsegmentCreatorDefaultCrossroadSettings.png
	
| **Direction count** : number of sides of the crossroad.

	.. image:: /images/road/roadSegment/examples/RoadSegmentDefault.png
	`Example`.
	
Turn Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTurnRoadSettings.png
	
| **Node 1 offset** : node 1 offset on the X-axis.
| **Node 2 offset** : node 2 offset on the X-axis.
| **Additional local angle 1** : additional node 1 rotation angle.
| **Additional local angle 2** : additional node 2 rotation angle.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTurnRoad.png
	`Example`.

	
Straight Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentStraightSettings.png
	
| **Node 1 offset** : node 1 offset on the X-axis.
| **Node 2 offset** : node 2 offset on the X-axis.
| **Traffic node height 1** : node 1 offset on the Y-axis.
| **Traffic node height 2** : node 2 offset on the Y-axis.

	.. image:: /images/road/roadSegment/examples/RoadSegmentStraight.png
	`Example`.
	
Merge Crossroad	
~~~~~~~~~~~~
 
	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadSettings.png
	
| **Direction count** : number of sides of the crossroad.
| **Sub-lane count** : number of sub-lanes (a sub-lane is a lane with a different number of lanes than the main lane).
| **SubTrafficNode distance from center** : distance between the `SubTrafficNode` (node that contains a sub-lane) and the center of the segment.
	
	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionCrossroad.png
	`Example`.
	
Merge Straight Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionStraightRoadSettings.png
	
| **Sub-lane count** : number of sub-lanes (a sub-lane is a lane with a different number of lanes than the main lane).
| **Node 1 offset** : node 1 offset on the X-axis.
| **Node 2 offset** : node 2 offset on the X-axis.
| **Traffic node height 1** : node 1 offset on the Y-axis.
| **Traffic node height 2** : node 2 offset on the Y-axis.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionStraightRoad.png
	`Example`.
	
Merge Crossroad To Oneway Road
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentTransitionCrossroadToOneWaySettings.png
	
| **Direction count** : number of sides of the crossroad.
| **Sub-lane count** : number of sub-lanes (a sub-lane is a lane with a different number of lanes than the main lane).
| **SubTrafficNode distance from center** : distance between the `SubTrafficNode` (node that contains a sub-lane) and the center of the segment.
| **Is enter of oneway** : if it is on, it is the start of one-way traffic, if it is off, it is the end of one-way traffic.

	.. image:: /images/road/roadSegment/examples/RoadSegmentTransitionCrossroadToOneWay.png
	`Example`.
	
Oneway Straight
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentOneWayStraightSettings.png
	
| **Node 1 offset** : node 1 offset on the X-axis.
| **Node 2 offset** : node 2 offset on the X-axis.
| **Traffic node height 1** : node 1 offset on the Y-axis.
| **Traffic node height 2** : node 2 offset on the Y-axis.
| **Should revert direction** : direction of the crossroad lanes will be reversed.

	.. image:: /images/road/roadSegment/examples/RoadSegmentOneWayStraight.png
	`Example`.
	
Oneway Turn
~~~~~~~~~~~~ 

	.. image:: /images/road/roadSegment/creator/RoadSegmentOneWayTurnSettings.png
	
| **Node 1 offset** : node 1 offset on the X-axis.
| **Node 2 offset** : node 2 offset on the X-axis.
| **Additional local angle 1** : additional node 1 rotation angle.
| **Additional local angle 2** : additional node 2 rotation angle.
| **Should revert direction** : direction of the crossroad lanes will be reversed.

	.. image:: /images/road/roadSegment/examples/RoadSegmentOneWayTurn.png
	`Example`.
		
.. _roadSegmentCreatorCustomStraight:

Custom Straight Road
------------

Creator for creating straight roads of any shape.

`Youtube tutorial. <https://youtu.be/JbhGYxVscew>`_

How To Use
~~~~~~~~~~~~

#. Place the custom  straight segment where you want it.
#. Place the :ref:`traffic nodes <trafficNode>` at the start and the end of the path (or expand the road by holding `left-shift` key and clicking the `left-mouse` button).
#. Rotate the :ref:`TrafficNodes <trafficNode>` in the direction of the route (make sure that the :ref:`rotation of the nodes <trafficNodeRotation>` is set correctly).
#. Adjust the number of lanes and the speed limit of the segment.
#. If necessary, add more additional nodes to the paths (by pressing `+` in the scene) **[optional step]**.
#. Rotate the nodes of the paths according to the direction of the path **[optional step]**.
#. :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to the surface by pressing the `Snap To Surface` button if necessary **[optional step]**.
#. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

Settings
~~~~~~~~~~~~

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
------------ 

Creator for creating segments of any shape and complexity.

`Youtube tutorial. <https://youtu.be/AMrGJ7YGBNo>`_

How To Use
~~~~~~~~~~~~

#. Place the custom segment where you want it.
#. Choose one of the following methods to create your intersection or layout:

**Option A: Manual Connection (Fine-tuning)**
""""""""""""""
     
* Toggle on the :ref:`Custom settings <roadSegmentCreatorCustomCustomSettingsOption>` parameter.
* Select the `New node settings type` and create new :ref:`TrafficNodes <trafficNode>` by pressing the **Add Traffic Node** button.
* :ref:`Place <roadSegmentCreatorCustomSnapNodeSettings>` and rotate all created nodes according to your needs (ensure correct :ref:`node rotation <trafficNodeRotation>`).
* :ref:`Snap <roadSegmentCreatorCustomSnapNodeSettings>` :ref:`TrafficNodes <trafficNode>` to the surface by pressing the **Snap To Surface** button if required.
* Open the manual :ref:`PathCreator tool <pathCreator>` to manually create and link :ref:`paths <path>` between the nodes.

**Option B: Auto-Crossroads Mode (From Scratch)**
""""""""""""""
     
* Create and arrange your child :ref:`Traffic nodes <trafficNode>` inside this custom segment at the entry and exit points of the intersection.
* Open the **Path settings** tab and change **Additional Settings** to ``AutoCrossroad``.
* Press **Clear** to wipe any existing paths, then click **Create** to automatically calculate crossroad geometry and build all traffic paths.

**Option C: Intersection Creation Mode (From Existing Scene Roads)**
""""""""""""""
     
	.. note::
	   You do **not** need to manually add or create new Traffic Nodes for this method. The creator will automatically generate internal nodes based on your scene selection.

* Open the **Path settings** tab and set **Additional Settings** to ``IntersectionCreation``.
* In the *Scene View*, select **two or more** existing :ref:`TrafficNodes <trafficNode>` belonging to different independent roads already placed on your scene.
* Configure the merging behavior in the inspector:

	* **Auto Merge Nodes**: Terminal nodes of your straight roads will automatically align and link for a seamless mesh transition.
	* **Auto Generate Crossing**: Automatically triggers path solving between the chosen roads.

* Click the **Create** button. The component will automatically match the node count, clone all settings from the selected scene nodes, align crosswalks, and build the intersection paths.


3. Complete all the :ref:`default steps <roadSegmentCreatorHowToUse>`.

	.. note:: You can convert any :ref:`default template <roadSegmentCreatorCustomSettings>` to `Custom Segment`_ in the `Other settings`_ tab.
	
Settings
~~~~~~~~~~~~

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
			
Custom Path Settings
""""""""""""""

	.. image:: /images/road/roadSegment/creator/RoadSegmentNodeHandles.png
	
| **Show traffic node handles** : on/off handles of :ref:`TrafficNodes <trafficNode>`
| **Show traffic node forward** : on/off display of :ref:`TrafficNode <trafficNode>` forwading.

Additional Settings
~~~~~~~~~~~~

.. _extrudeLane:

Extrude Lane
""""""""""""""

	.. image:: /images/road/roadSegment/creator/ExtrudeLaneSettings.png
	
**How to use:**
	
#. Drag the green sphere from where you want the new lane to start.
#. Drop the cursor where you want the lane to end.
#. Adjust the position handle of the new path.
#. Press `E` key or press `Create` button in the inspector to create new lane.
	
.. only:: builder_html

	.. image:: /images/road/roadSegment/creator/ExtrudeLaneExample.gif
	`Example.`
	
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
#. If you want to configure the traffic lights individually, select the `Node` button with the appropriate index.
	
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

.. _roadSegmentCreatorAuto:

Auto Crossroad
------------

For automatic generation of custom crossroads, use this feature.

How To Use
~~~~~~~~~~~~ 

#. Create a :ref:`Custom road segment <roadSegmentCreatorCustomSegment>`.

	.. image:: /images/road/roadSegment/auto/AutoCrossroad0.png
	
#. Open the `Path Settings` tab & enable the `Auto-Crossroads` option in the `Additional Settings` dialog.

	.. image:: /images/road/roadSegment/auto/AutoCrossroad1.png
	
#. Press the `Clear` button to delete existing :ref:`paths <path>`.	
#. Place :ref:`Traffic nodes <trafficNode>` at the entrances/exits of the intersection.

	.. image:: /images/road/roadSegment/auto/AutoCrossroad2.png
	
#. Press the `Create` button.

	.. image:: /images/road/roadSegment/auto/AutoCrossroad3.png
	
#. If you want to avoid connection for certain :ref:`Traffic nodes <trafficNode>` select indexes according to scene indexes & press `Add` button, then press `Create` button again.

#. For example 1-3 & 3-1 nodes.
	.. image:: /images/road/roadSegment/auto/AutoCrossroad4.png
	
#. 1-3 & 3-1 nodes no longer connected.

	.. image:: /images/road/roadSegment/auto/AutoCrossroad5.png
	`Example result.`
	
#. If you are missing a connection, use the :ref:`Path Creator <pathCreator>` to add missing paths.

.. _deadEnd:

Dead End
------------

Destroy
~~~~~~~~~~~~

If you want traffic to be destroyed at the dead end (e.g. when it drives beyond the scene), enable the `Destroy vehicle` type in the :ref:`Traffic node <trafficNode>`.

U Turn
~~~~~~~~~~~~ 

To create u turn path:

#. Open :ref:`Path Creator <pathCreator>` tool.
#. Select desired :ref:`Traffic node <trafficNode>` for u turn.
#. Enable `U turn` option in the `Node settings` tab.
#. Enable `Connect same side` option & set `Source node side` to `External side`.
#. Press `Create` button.


	



	

