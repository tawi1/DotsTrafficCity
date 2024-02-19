.. _roadSegment:

Road Segment
=====

`Road Segment` is the main component of the road that contains :ref:`traffic nodes <trafficNode>`, :ref:`paths <path>`, and :ref:`pedestrian nodes <pedestrianNode>`.

`Youtube tutorial. <https://youtu.be/wNa8GgBPyqU>`_

How To Create
------------

Select from the `Unity` toolbar:

	.. image:: /images/road/installation/RoadSegmentCreation.png
	
	
How To Customize
------------

By default, `RoadSegment` contains :ref:`RoadSegmentCreator <roadSegmentCreator>` component that can be used to customize a segment.
	
	
Main Components
------------

Road Segment
~~~~~~~~~~~~

Component for connection to other road segments.

	.. image:: /images/road/roadSegment/RoadSegment.png
	
Variables
""""""""""""""

| **Road segment placer** : reference to the :ref:`RoadSegmentPlacer <roadSegmentPlacer>`.
| **Short title name** : short name for :ref:`RoadSegmentPlacer <roadSegmentPlacer>`.
| **Show intersected paths** : on/off :ref:`intersection points <roadSegmentIntersectionExample>` in the scene.
	
Buttons
""""""""""""""

| **Connect nodes** : :ref:`auto-connect <autoPathConnection>` :ref:`Traffic Nodes<trafficNode>`.
| **Reset nodes** : reset already :ref:`auto-connected <autoPathConnection>` paths of :ref:`Traffic Nodes<trafficNode>` (except :ref:`locked <trafficNode>` nodes).
| **Bake data** : :ref:`bake <roadSegmentBakingInfo>` all :ref:`paths <path>` data (path's length, intersections).
	
.. _trafficLightCrossroad:
	
TrafficLightCrossroad
~~~~~~~~~~~~

Component for handling traffic lights at crossroad. For a quick look at timelines of city crossroads and traffic light connections, :ref:`see here <trafficLight>`.

Cached
""""""""""""""

	.. image:: /images/road/roadSegment/TrafficLightCrossroadCached.png
	
| **Shared state container** : :ref:`shared light state container <sharedLightStates>`, that contain common traffic light timings that are shared with other light crossroads.
| **Traffic nodes** : all :ref:`Traffic Nodes <trafficNode>` of `RoadSegment`.
| **Traffic light handler data** : light index and light handlers that are linked to the `TrafficLightCrossroad`.

Timeline common
""""""""""""""
	
Timeline common uses the timeline from the :ref:`Shared state container <sharedLightStates>`.
	
	.. image:: /images/road/roadSegment/TrafficLightCrossroadLightTimeline.png
	
	.. note::
		You can easily replace the :ref:`shared state container <sharedLightStates>` for all crossroads using the :ref:`Global Light Settings <trafficLightGlobalLight>` tool.

Timeline custom
""""""""""""""

``Custom timeline is designed for custom timings of the traffic light segment``

	.. image:: /images/road/roadSegment/TrafficLightCrossroadCustomTimelineExample1.png
		
**How to add states:**
	#. Enable `custom settings`.
	#. Select the desired :ref:`TrafficLightHandler <trafficLightHandler>`.
	#. Press the `+` button.
	#. Add desired :ref:`states <trafficLightState>`.
	#. Enter the duration of the :ref:`state <trafficLightState>`.
		
	.. image:: /images/road/roadSegment/TrafficLightCrossroadCustomTimeline.png
	
Once you have set up 1 `TrafficLightHandler`, you can loop to the 2nd :ref:`TrafficLightHandler <trafficLightHandler>`.
	
**How to loop timeline:**
	#. Select the :ref:`TrafficLightHandler <trafficLightHandler>` to be looped.
	#. Enter the `Source Data Handler Index` parameter based on which to loop.
	
		.. image:: /images/road/roadSegment/TrafficLightCrossroadCustomTimelineLoopExample1.png
		`Settings example.`
		
	#. Click the `Loop Time` button.
	
**Loop result:**

	.. image:: /images/road/roadSegment/TrafficLightCrossroadCustomTimelineLoopExample2.png

Custom arrow lights
""""""""""""""

Arrows are used for the custom traffic light for the selected :ref:`path <path>`.

**How to create arrows:**
	#. Click `Show Custom Arrow Light Setup`.
	#. Select `Custom Related Light Index`.
	#. Select related :ref:`TrafficNode <trafficNode>` from the toolbar.
	
		.. image:: /images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample.png
			
	#. Select related :ref:`path <path>` from the toolbar.
	
		.. image:: /images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample2.png
		`Selected path example.`
		
	#. Click the `Add Custom Light` button.
	
	.. note:: To remove the light arrow, select the appropriate `TrafficNode` and `Path` and press the `Remove Selected Path` button.

.. _roadSegmentBakingInfo:

Baking info
------------

The intersection of :ref:`paths <pathBakingInfo>` is only baked in those :ref:`paths <pathBakingInfo>` that are in the segment. How to :ref:`bake <bakingInfo>`.

.. _roadSegmentIntersectionExample:

	.. image:: /images/road/roadSegment/RoadSegmentIntersectionExample.png
	`Intersection points example.`


	

