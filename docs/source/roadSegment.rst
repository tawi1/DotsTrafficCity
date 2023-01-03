.. _roadSegment:

Road Segment
=====

`Road Segment` is the main component of the road that contains :ref:`traffic node<trafficNode>`, :ref:`paths<path>`, and :ref:`pedestrian nodes<pedestrianNode>`.

How To Create
------------

Select in the unity toolbar:

	.. image:: images/road/roadSegment/RoadSegmentCreation.png
	
	
Main Components
------------

Road Segment
~~~~~~~~~~~~

Component to connect with other road segments.

	.. image:: images/road/roadSegment/RoadSegment.png
	
Variables
""""""""""""""

| **Road segment placer** : reference to :ref:`RoadSegmentPlacer<roadSegmentPlacer>`.
| **Short title name** : short name for `RoadSegmentPlacer`.
| **Show intersected paths** :
	
Buttons
""""""""""""""

| **Connect nodes** : auto-connect :ref:`traffic Nodes<trafficNode>`.
| **Reset nodes** : reset already auto-connected paths of :ref:`traffic Nodes<trafficNode>`.
| **Bake data** : bake all :ref:`paths<path>` data (path's length, intersections).
	
TrafficLightCrossroad
~~~~~~~~~~~~

Component for handling traffic lights at crossroad.

Cached
""""""""""""""

	.. image:: images/road/roadSegment/TrafficLightCrossroadCached.png
	
	**Traffic crossroad settings** : settings that contain general traffic light timings.
	**Traffic nodes** : all nodes of `RoadSegment`.
	**Traffic light handler data** : light handlers that contain `TrafficLightCrossroad`.

Timeline common
""""""""""""""
	
Timeline common uses the timeline from the `TrafficCrossroadSettings`.
	
	.. image:: images/road/roadSegment/TrafficLightCrossroadLightTimeline.png
	
	.. note:: You can change the common timeline for the current segment by adding new settings `TrafficCrossroadSettings`.

Timeline custom
""""""""""""""

``Custom timeline is designed for custom timings of the traffic light segment``

	.. image:: images/road/roadSegment/TrafficLightCrossroadCustomTimeline.png
	
After you have set up 1 `TrafficLightHandler`, it can be looped to the 2nd `TrafficLightHandler`.
	
**How to loop timeline:**
	#. Select the `TrafficLightHandler` that should be looped.
	#. Enter `Source Data Handler Index` parameter based on which to loop.
	
		.. image:: images/road/roadSegment/TrafficLightCrossroadCustomTimelineLoopExample1.png
		`Settings example`
		
	#. Click `Loop Time`.
	
**Loop result:**

	.. image:: images/road/roadSegment/TrafficLightCrossroadCustomTimelineLoopExample2.png

Custom arrow lights
""""""""""""""

Arrows are used for the custom traffic light for the selected :ref:`path <path>`.

**How to create arrows:**
	#. Click `Show Custom Arrow Light Setup`.
	#. Select `Custom Related Light Index`.
	#. Select related :ref:`TrafficNode <trafficNode>` in the toolbar.
	
		.. image:: images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample.png
			
	#. Select related :ref:`path <path>` in the toolbar.
	
		.. image:: images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample2.png
		`Selected path example`
		
	#. Click `Add Custom Light` button.
	
	.. note:: To remove the light arrow, select appropriate `TrafficNode` and `path` and press `Remove Selected Path` button.
		

How To Customize
------------

By default `RoadSegment` contains :ref:`RoadSegmentCreator <roadSegmentCreator>` component which can be used to customize a segment.



	

