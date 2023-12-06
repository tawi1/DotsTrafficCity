.. _bakingInfo:

Baking Info
=====

Baking data is required to store calculated data to avoid heavy calculations each time. This should be done after each :ref:`road change <roadEdit>` and before the launch of the scene.

`Youtube tutorial. <https://youtu.be/6d7nuWSFSzk>`_

**Baked data:**
	* :ref:`Road segment data <roadSegmentBakingInfo>`.
	* :ref:`Path data <pathBakingInfo>`.

How To Bake
-------------------

#. Open :ref:`RoadParent <roadParentInfo>` in the main scene or :ref:`subscene <subscene>` (:ref:`recommended <roadEdit>` in the main scene for performance purposes).
	
	.. _roadParent:

	.. image:: /images/road/bakingInfoExample.png
	`Subscene example.`

#. Press `Reset Segments` button to reset the :ref:`automatically created paths <autoPathConnection>`.

	.. image:: /images/road/installation/RoadParent.png
	
#. Press `Connect Segments` button to connect segments (make sure all segments are :ref:`on one line <trafficNodeConnectionInfo>`).
#. Press `Bake Path Data` button.
