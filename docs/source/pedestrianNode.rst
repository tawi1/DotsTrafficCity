.. _pedestrianNode:

Pedestrian Node
=====

How To Create
----------------

Pedestrian Node
----------------

``Pedestrian node is a node for creating pedestrian routes``

	.. image:: images/configs/road/PedestrianNode.png
	
Connected data
~~~~~~~~~~~~

| **Connected traffic node** : connect traffic node (for parking).
| **Related traffic light handler** : connected traffic light.
| **Auto connected pedestrian nodes** : connected other nodes along selected direction.
| **Default connected pedestrian nodes** : connected other nodes by the user.
| **Directions of auto-connections** : direction of raycasts to connect with other nodes (can be useful for generating squared scenes).

Custom Node Settings
~~~~~~~~~~~~

Default
""""""""""""""

Default node for the route.
 
Sit
""""""""""""""

Node for benches, seats, etc. (required `PedestrianNodeSeatSettings` component).

| **Show seats** : enable editor display of seats.
| **Base offset** : offset between the center of the seats and the center of the node.
| **Seat offset** : offset between the seats.
| **Enter seat offset** : offset between the animation start position and the seat.
| **Seat height** : seat height.
| **Capacity** : number of seats (adjustable in the :ref:`settings <pedestrianNodeSettings>` of the node).

House
""""""""""""""

Node for entry/exit to the house.

Idle
""""""""""""""

Node for temporary idling pedestrians.

Car parking
""""""""""""""

Node to enter/exit a parked car.

Talk area
""""""""""""""

Node for crowd conversations of pedestrians.

**Area shape type:** type of area shape.
	* **Square**
	* **Circle**
| **Area size** : area size.
| **Min/Max spawn count** : min/max number of pedestrians that the area can contain.
| **Unlimited talk time** : on/off infinite conversation for pedestrians in the talk area.
| **Show bounds** : show bounds of area.

Traffic public stop station
""""""""""""""

Node for waiting for public transport.

Traffic public entry
""""""""""""""

Node for entering public transport.
	
.. _pedestrianNodeSettings:

Common Settings
~~~~~~~~~~~~

| **Can spawn in view** : can spawn in view of camera or not.
| **Capacity** : -1 value is unlimited; Capacity for objects like benchs, houses etc...
| **Priority weight** : weight for choosing random node by pedestrian.
| **Custom achieve distance** : custom achieve distance for pedestrian. If 0 then default value is taken.
| **Chance to spawn** : chance to spawn pedestrian at node [0 = 0%, 1 = 100%].
| **Max path width** : maximum width of the route around the node.
| **Has movement random offset** : are supposed to randomize the position around a node.
		
.. _pedestrianNodeCreator:
		
Pedestrian Node Creator
----------------

``Pedestrian node is a node for creating pedestrian routes``
		
How To Create
~~~~~~~~~~~~

Select in the unity toolbar:
	
``Spirit604/Create/PedestrianNodeCreator``


How To Create Node
~~~~~~~~~~~~

#. Press `Tab` button on keyboard to create `PedestrianNode`.
#. Press `Tab` button on keyboard.

How To Connect Node
~~~~~~~~~~~~


Settings
~~~~~~~~~~~~

	.. image:: images/configs/road/PedestrianNodeCreatorSettings.png
	
| **Show handlers** : on/off position handles for nodes.
**Show handle type:**
	* **Only created** : only the created nodes will have handles shown
	* **Only selected** : only the selected nodes will have handles shown.
	* **All** : all nodes will have handles shown
**Selection mode:**
	* **Single** : only 1 node is selected.
	* **Multiple** : multiple nodes can be selected.
| **Max path width** : global width of routes for all nodes (enable preview `here <creatorShowBorders>`, save global width `here <creatorSaveGlobalWidth>`).
| **Connect with previous node** : currently created node will be connected to the previously created node.
| **Auto select connected node** : node will be selected after it is connected to the source node.
| **Allow connect traffic node** : on/of feature to connect to the :ref:`TrafficNode <trafficNode>`.
**Auto split connection** : if a node is located between a connection of existing nodes, the connection will be reconnected between them (made with a raycast).
	* **Disabled**
	* **Right angle** : 90° angle.
	* **Custom angle** : user custom angle.
| **Auto rejoin line** : if there are other nodes on the connection line, they will automatically be connected to each other in one row.
**Auto attach to surface** : auto attach created node to surface.
	* **Surface mask** : layer mask to attach.
	* **Attach type:**
		* **Collider** : attach to collider.
		* **Mesh** : attach to mesh.
**Auto snap position** : auto snap node position during creation.
	* **Snap value** : snapping value.
	
Scene Settings
~~~~~~~~~~~~

	.. image:: images/configs/road/PedestrianNodeCreatorSceneSettings.png
		
| **Show path** : show pedestrian node routes.
**Show path type:**
	* **All** : all the nodes will be shown.
	* **Only created** : only the nodes created by the creator will be shown.
| **Show node buttons** : on/off display custom buttons of selected nodes.
	* **Node button type:**
		* **Delete** : node will be deleted by clicking.
		* **Unselect** node will be unselected by clicking.
| **Show unique info** : unique information of the node will be displayed (different from the original prefab).
| **Show reset custom route buttons** : for nodes with a custom route width, the reset buttons will be displayed.
.. _creatorShowBorders: **Show border routes** :
	* **Current** : route will be displayed with the assigned width of the nodes.
	* **Selected** : route will be displayed with the selected route width in the `creator settings <creatorSaveGlobalWidth>`.
| **Show traffic node connection** : on/off display the connection to the :ref:`TrafficNode <trafficNode>`.
| **Show selected node settings** : shows :ref:`node settings <pedestrianNodeSettings>` in the inspector.

Buttons
~~~~~~~~~~~~

| **Create node** :
| **Add all scene pedestrian nodes** :
| **Add all scene custom pedestrian nodes** :
| .. _creatorSaveGlobalWidth: **Save global path width** :
| **Reset all custom path width** :
| **Clear created nodes info** :
| **Clear selection** :

