.. _howToConnectRoad:

How To Connect Roads
====================

Overview
--------

There are three ways to connect road segments in the scene:

Force connection
  Connecting segments automatically using the **Road Parent** object. This method connects nodes that face each other and is ideal for tiled grid layouts.

Manual connection
  Manually connecting specific nodes using the **Path Creator** tool.

Merge connection
  Connecting two segments by dragging their :ref:`Traffic nodes <trafficNode>` close to each other, which causes them to merge automatically.

Force Connection
----------------

#. Open the :ref:`Road Parent <roadParentInfo>` component.
	
   .. image:: /images/road/installation/RoadParent.png
      :alt: Road Parent Inspector
      :align: center

#. Press the **Force connect** button to connect segments. 

   .. note:: Ensure that adjacent segments are properly aligned and facing each other so their :ref:`external nodes <trafficNodeConnectionInfo>` can detect each other.

#. **Source segments before connection:**

   .. image:: /images/road/installation/howToConnect1.png
      :alt: Segments Before Force Connection
      :align: center

#. **Result after connection:**

   .. image:: /images/road/installation/howToConnect2.png
      :alt: Segments After Force Connection
      :align: center

Manual Connection
-----------------

#. Open the :ref:`Path creator <pathCreator>` tool.
	
#. In the Scene view, select the :ref:`Traffic nodes <trafficNode>` that you want to connect.

   .. image:: /images/road/installation/howToConnect3.png
      :alt: Selecting Traffic Nodes
      :align: center
	
#. You will see a green preview of the paths that will be created.

   .. image:: /images/road/installation/howToConnect4.png
      :alt: Path Connection Preview
      :align: center
	
#. In the **Path creator** inspector, press the **Create** button to complete the connection.

   .. image:: /images/road/installation/howToConnect5.png
      :alt: Completed Path Connection
      :align: center

Merge Connection
----------------

#. Select the desired road segment in the scene.

   .. image:: /images/road/installation/howToConnect6.png
      :alt: Selecting Segment for Merge
      :align: center

#. Drag the :ref:`Traffic node <trafficNode>` close to another segment's node. They will automatically merge into a single connection point.