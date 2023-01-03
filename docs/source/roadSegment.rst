.. _roadSegment:

Road Segment
=====

``Road Segment is the main component of the road that contains :ref:`traffic node<trafficNode>`, :ref:`paths<path>`, and :ref:`pedestrian nodes<pedestrianNode>` ``

How To Create
------------

	.. image:: images/road/roadSegment/RoadSegmentCreation.png
	
	
Main Components
------------

Road Segment
~~~~~~~~~~~~

	.. image:: images/road/roadSegment/RoadSegment.png
	
TrafficLightCrossroad
~~~~~~~~~~~~

Cached
""""""""""""""

	.. image:: images/road/roadSegment/TrafficLightCrossroadCached.png


Timeline common
""""""""""""""

	.. image:: images/road/roadSegment/TrafficLightCrossroadLightTimeline.png

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
	#. Select related :ref:`TrafficNode <trafficNode>`.
	
		.. image:: images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample.png
			
	#. Select related :ref:`path <path>`.
	
		.. image:: images/road/roadSegment/TrafficLightCrossroadLightArrowSettingsExample2.png
		`Selected path example`
		
	#. Click `Add Custom Light` button.
	
	..note: To remove the light arrow, select appropriate `TrafficNode` and `path` and press `Remove Selected Path` button.
		

How To Customize
------------

By default `RoadSegment` contains `RoadSegmentCreator` component which can be used to customize a segment.



	

