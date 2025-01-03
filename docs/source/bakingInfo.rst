.. _bakingInfo:

Baking Info
=====

* Baking data is required to store calculated data to avoid heavy calculations each time. This should be done after each :ref:`road change <roadEdit>` and before the launch of the scene.
* To validate that all traffic objects are properly configured (use the :ref:`TrafficObjectFinder tool <trafficObjectFinder>` to find the traffic objects with the errors by `InstanceID` shown in the console).

`Youtube tutorial. <https://youtu.be/P1iP4XR383M>`_

**Baked data:**
	* :ref:`Road segment data <roadSegmentBakingInfo>`.
	* :ref:`Path data <pathBakingInfo>`.

How To Bake
-------------------

#. Open :ref:`RoadParent <roadParentInfo>`.
	
	.. _roadParent:

	.. image:: /images/road/bakingInfoExample.png
	`Subscene example.`

	.. image:: /images/road/installation/RoadParent.png

#. Press the `Force connect Segments` button to connect segments (if you are using :ref:`auto-connection <autoPathConnection>`, make sure all segments are :ref:`on one line <trafficNodeConnectionInfo>`). *[optional]*
#. Press the `Bake Path Data` button.
