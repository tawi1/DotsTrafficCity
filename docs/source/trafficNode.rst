.. _trafficNode:

Traffic Node
=====

``Traffic node is a node for creating pedestrian routes``

Settings
----------------

	.. image:: images/road/trafficNode/TrafficNode.png
	
| **Traffic light handler** : traffic light that the traffic node is linked (:ref:`TrafficLightHandler <trafficLightHandler>`).
| **Lanes** : :ref:`rightside lanes <trafficNodeRightDirection>` (to connect `TrafficNodes` within a :ref:`RoadSegment <roadSegment>`).
| **External lanes** : :ref:`leftside lanes <trafficNodeLeftDirection>` (to connect nodes in external :ref:`RoadSegments <roadSegment>`).
| **Lane count** : number of lanes.
| **Lane width** : lane width.
| **Chance to spawn** : chance of the vehicle spawning in the node.
| **Weight** : weight of the node for route selection by traffic.
| **Custom achieve distance** : custom distance to achieve a node (if 0 value default value will be taken).
| **Capacity** : capacity of the nodes (used for parking, bus station, etc...).
**Traffic node type:** 
	* **Default**
	* **Parking** : node where cars are parked.
	* **Traffic public stop** : node where public traffic stops to pick up passengers. 
	* **Destroy vehicle** : node where the vehicle entity is destroyed (useful for nodes outside the map).
	* **Traffic area** : (:ref:`TrafficArea node <trafficArea>`).
	* **Idle** : node where the vehicle is idling.
| **Has crollwalk** : quick on/off crosswalk option for pedestrians.
| **Allow light for left lanes** : enable traffic light for leftside entities (by default, traffic light is enabled only for rightside lane entities).
| **Is one way** : all lanes are one-way traffic lanes (:ref:`more info <trafficNodeOneWay>`).
| **Is end of one way** : node ends one-way traffic for this :ref:`RoadSegments <roadSegment>` (:ref:`more info <trafficNodeOneWay>`).
| **Lock path auto creation** : on/off prevent auto path creation (:ref:`more info <trafficNodeAutoPathConnection>`).
| **Auto path is created** : (:ref:`more info <trafficNodeAutoPathConnection>`)
	
**Buttons:**
	* **Connect** : node will try to :ref:`connect <trafficNodeAutoPathConnection>` to other nodes if no external paths are created yet.
	* **Force connect** : node will try to :ref:`connect <trafficNodeAutoPathConnection>` to other nodes whether it is :ref:`connected <trafficNodeAutoPathConnection>` now or not.
	* **Resize** : resize (:ref:`collider <trafficNodeCollider>`) of node.
	
.. _trafficNodeOneWay:

OneWay Info
----------------

Oneway node description example:

	.. image:: /images/road/trafficNode/OnewayExample.png
	
Key features:
* **Node 1:**
	* Is one way **[enabled]**
	* Source path is in the : **[Lanes]**
	* External Lanes **[Empty]**
* **Node 2:**
	* Is one way **[enabled]**
	* Is end one way **[enabled]**
	* Source path is in the : **[External Lanes]**
	* Lanes **[Empty]**
	
.. _trafficNodeConnectionInfo:

Direction Connection Info
----------------


.. _trafficNodeRightDirection:
.. _trafficNodeLeftDirection:


.. _trafficNodeAutoPathConnection:

Auto-path Connection
----------------


.. _trafficNodeCollider: collider


.. _trafficNodePathCreator:

TrafficNode Path Creator
=====

	
