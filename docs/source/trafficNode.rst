.. _trafficNode:

Traffic Node
=====

``Traffic node is a set of traffic node entities that are connected to other traffic node entities by ``:ref:`path <paths>`

.. _trafficNodeSettings:

Settings
----------------

	.. image:: images/road/trafficNode/TrafficNode.png
	
| **Traffic light handler** : traffic light that the traffic node is linked (:ref:`TrafficLightHandler <trafficLightHandler>`).
| **Lanes** : :ref:`rightside lanes <trafficNodeRightDirection>` (to connect `TrafficNodes` within a :ref:`RoadSegment <roadSegment>`).
| **External lanes** : :ref:`leftside lanes <trafficNodeLeftDirection>` (to connect nodes in :ref:`external RoadSegments <trafficNodeConnectionExample>`) (:ref:`additonal info <trafficNodeLeftDirectionInfo>`).
| **Lane count** : number of lanes.
| **Lane width** : lane width.
| **Chance to spawn** : chance of the vehicle spawning in the node.
| **Weight** : weight of the node for route selection by traffic.
| **Custom achieve distance** : custom distance to achieve a node (if 0 value default value will be taken).
| **Capacity** : capacity of the nodes (used for parking, bus station, etc...).

**Traffic node type:** 
	* **Default**
	* **Parking** : node where cars are parked.
	* **Traffic public stop** : node where :ref:`public traffic <trafficPublic>` stops to pick up passengers. 
	* **Destroy vehicle** : node where the vehicle entity is destroyed (useful for nodes outside the map).
	* **Traffic area** : :ref:`TrafficArea node <trafficArea>`.
	* **Idle** : node where the vehicle is idling.
	
| **Has crollwalk** : quick on/off crosswalk option for pedestrians.
| **Allow light for left lanes** : enable traffic light for leftside entities (by default, traffic light is enabled only for rightside lane entities).
| **Is one way** : all lanes are one-way traffic lanes (:ref:`more info <trafficNodeOneWay>`).
| **Is end of one way** : node ends one-way traffic for this :ref:`RoadSegments <roadSegment>` (:ref:`more info <trafficNodeOneWay>`).
| **Lock path auto creation** : on/off prevent auto path creation (:ref:`more info <trafficNodeAutoPathConnection>`).
| **Auto path is created** : auto path is created (:ref:`more info <trafficNodeAutoPathConnection>`).
	
**Buttons:**
	* **Connect** : node will try to :ref:`connect <trafficNodeAutoPathConnection>` to other nodes if no external paths are created yet.
	* **Force connect** : node will try to :ref:`connect <trafficNodeAutoPathConnection>` to other nodes whether it is :ref:`connected <trafficNodeAutoPathConnection>` now or not (except `Lock path auto creation` option is enabled).
	* **Resize** : resize :ref:`collider <trafficNodeCollider>` of node.
	
.. _trafficNodeOneWay:

OneWay Node Info
----------------

Oneway node description example:

	.. image:: /images/road/trafficNode/OnewayExample.png
	
Node example key features:
	* **Node 1:**
		* Is one way **[enabled]**
		* Source path is in the : **[Lanes]**
		* External Lanes **[Always empty]**
	* **Node 2:**
		* Is one way **[enabled]**
		* Is end one way **[enabled]**
		* Source path is in the : **[External Lanes]**
		* Lanes **[Always empty]**
	
.. _trafficNodeConnectionInfo:

Direction Connection Info
----------------

.. _trafficNodeRightDirection:

Rightside Lanes
~~~~~~~~~~~~ 

Rightside lanes (default lanes) connect :ref:`TrafficNodes <trafficNode>` within a :ref:`RoadSegment <roadSegment>`.

	.. image:: /images/road/trafficNode/ConnectionInfoExampleRightSide.png
	`Rightside lanes example.`

.. _trafficNodeLeftDirection:

Leftside Lanes
~~~~~~~~~~~~ 

Leftside lanes (external lanes) connect :ref:`TrafficNodes <trafficNode>` in external :ref:`RoadSegments <roadSegment>` (:ref:`external connection example <trafficNodeConnectionExample>`).

	.. image:: /images/road/trafficNode/ConnectionInfoExampleLeftSide.png
	`Leftside lanes example.`
	
.. _trafficNodeLeftDirectionInfo:

	.. warning:: Intersected `External paths` should be replaced by a separate :ref:`segment <roadSegment>` to :ref:`bake the intersection of the paths <roadSegmentBakingInfo>`.
	
.. _trafficNodeRotation:

Node Rotation
~~~~~~~~~~~~ 
	
Direction of each :ref:`TrafficNode <trafficNode>` must be opposite to the center of the segment

	.. image:: /images/road/trafficNode/TrafficNodeDirectionExample.png

**Example description:**
	* Arrow represents the forward rotation of the :ref:`node <trafficNode>`.
	* Purple arrows the direction of the outer :ref:`nodes <trafficNode>` of the :ref:`segment <roadSegment>`.
	* Blue arrows the direction of the internal :ref:`segment <roadSegment>` :ref:`oneway nodes <trafficNodeOneWay>`.

.. _trafficNodeAutoPathConnection:

Auto-path Connection
----------------

* To quickly generate connections between :ref:`RoadSegments <roadSegment>` on the same line is used auto-path connection. 
* If the :ref:`segments <roadSegment>` are not on the same line you should to create another :ref:`Custom straight road segment <roadSegmentCreatorCustomStraight>` or :ref:`Custom segment <roadSegmentCreatorCustomSegment>` between them and do the same connection.
* Also you can manually create paths between :ref:`segments <roadSegment>` with :ref:`TrafficNodePathCreator tool <trafficNodePathCreator>`.

How To Use
~~~~~~~~~~~~ 

* To activate auto-connection paths for all nodes you can in :ref:`RoadParent <roadParent>` by pressing `Connect` button. 
* Every time you create a new :ref:`RoadSegment <roadSegment>` or move an existing :ref:`RoadSegment <roadSegment>`, press `Reset` and press `Connect` in :ref:`RoadParent <roadParent>`, then `Bake Path Data` (:ref:`baking info <pathBakingInfo>`).

.. _trafficNodeCollider:

	.. note:: 
		* To prevent auto-path connection for the selected :ref:`TrafficNode <trafficNode>` enable **Lock path auto creation** in the :ref:`settings <trafficNodeSettings>` of the node.
		* Every :ref:`TrafficNode <trafficNode>` has a `box collider` that is size calculated based on the number of lanes, their width, and the type of lanes (:ref:`oneway <trafficNodeOneWay>` or not).
		* Make sure that the :ref:`direction of the node <trafficNodeRotation>` is set correctly.
		
.. _trafficNodeConnectionExample:

	.. image:: /images/road/trafficNode/AutopathConnectionExample2.png
	`Auto path connection example.`