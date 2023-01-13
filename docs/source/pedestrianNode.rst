.. _pedestrianNode:

Pedestrian Node
=====

How To Create
----------------

**Ways:**
	#. Create it yourself in the unity toolbar: 
	
		.. image:: images/road/pedestrianNode/PedestrianNodeToolbarExample.png

		`Spirit604/Create/PedestrianNode`
		
	#. To create with :ref:`PedestrianNodeCreator tool <pedestrianNodeCreatorCreate>`.

Pedestrian Node
----------------

``Pedestrian node is a node for creating pedestrian routes``

	.. image:: images/road/pedestrianNode/PedestrianNode.png
	
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

Node for benches, seats, etc.

	.. image:: images/road/pedestrianNode/PedestrianNodeSeatSettings.png

| **Show seats** : enable editor display of seats.
| **Base offset** : offset between the center of the seats and the center of the node.
| **Seat offset** : offset between the seats.
| **Enter seat offset** : offset between the animation start position and the seat.
| **Seat height** : seat height.
| **Capacity** : number of seats (adjustable in the :ref:`settings <pedestrianNodeSettings>` of the node).

	.. note:: Required `PedestrianNodeSeatSettings` component.

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
		
Buttons
~~~~~~~~~~~~

| **Connect** :
| **Attach to closest traffic node** : try to connect close :ref:`TrafficNode <trafficNode>`.
| **Open advanced connection window** : open  :ref:`advanced connection window <pedestrianNodeAdvancedConnection>`.

.. _pedestrianNodeCreator:
		
Pedestrian Node Creator
----------------

`Pedestrian Node Creator` is a tool to quickly create and connect `pedestrian nodes <pedestrianNode>`.
		
How To Create
~~~~~~~~~~~~

Select in the unity toolbar:
	
	.. image:: images/road/pedestianNode/PedestrianNodeCreatorToolbarExample.png
	`Spirit604/Create/PedestrianNodeCreator`

How To
~~~~~~~~~~~~

.. _pedestrianNodeCreatorCreate:

Create Node
""""""""""""""
 
#. Press `Tab` button on keyboard to create preview `PedestrianNode <pedestrianNode>`.
#. Place preview `PedestrianNode <pedestrianNode>` where you want to be.
#. Press `E` button on keyboard for the final creation of the `PedestrianNode <pedestrianNode>`.

	.. note:: You can change the `hotkeys <pedestrianNodeCreatorHotkeys>` to your taste.

.. _pedestrianNodeCreatorSelect:

Select
""""""""""""""

#. Choose `Selection mode <pedestrianNodeCreatorSelectionMode>`.
#. Click `W` over the node to select `PedestrianNode <pedestrianNode>`.

Connect Node
""""""""""""""

#. `Select node <pedestrianNodeCreatorSelect>`.
#.  Click `E` over the target `PedestrianNode <pedestrianNode>` to connect (`Selection mode <pedestrianNodeCreatorSelectionMode>` only).

Locate
""""""""""""""

#. Choose `Selection mode <pedestrianNodeCreatorSelectionMode>`.
#. `Select source nodes <pedestrianNodeCreatorSelect>`.
#. Move the position handle where you want it.

.. _pedestrianNodeCreatorSettings:

Settings
~~~~~~~~~~~~

	.. image:: images/road/pedestianNode/PedestrianNodeCreatorSettings.png
	
| **Show handlers** : on/off position handles for nodes.
**Show handle type:**
	* **Only created** : only the created nodes will have handles shown
	* **Only selected** : only the selected nodes will have handles shown.
	* **All** : all nodes will have handles shown
	
.. _pedestrianNodeCreatorSelectionMode:

**Selection mode:**
	* **Single** : only 1 node is selected.
	* **Multiple** : multiple nodes can be selected.
		* **Multiple handle type:**
			* **Single** : node has a position handle each individually.
			* **All** : all nodes have the same position handle.
		* **Unselect selected** : if you try to select an already selected node, it will be unselected.
| **Max path width** : global width of routes for all nodes (enable preview `here <creatorShowBorders>`, save global width `here <creatorSaveGlobalWidth>`).
| **Connect with previous node** : currently created node will be connected to the previously created node.
| **Auto select connected node** : node will be selected after it is connected to the source node.
| **Allow connect traffic node** : on/of feature to connect to the :ref:`TrafficNode <trafficNode>`.
**Auto split connection** : if a node is located between a connection of existing nodes, the connection will be reconnected between them (made with a `Raycast`).
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

	.. image:: images/road/pedestianNode/PedestrianNodeCreatorSceneSettings.png
		
| **Show path** : show pedestrian node routes.
**Show path type:**
	* **All** : all the nodes will be shown.
	* **Only created** : only the nodes created by the creator will be shown.
**Show node buttons** : on/off display custom buttons of selected nodes.
	* **Node button type:**
		* **Delete** : node will be deleted by clicking.
		* **Unselect** node will be unselected by clicking.
| **Show unique info** : unique information of the node will be displayed (different from the original prefab).
| **Show reset custom route buttons** : for nodes with a custom route width, the reset buttons will be displayed.

.. _creatorShowBorders: 

**Show border routes** :
	* **Current** : route will be displayed with the assigned width of the nodes.
	* **Selected** : route will be displayed with the selected route width in the `creator settings <creatorSaveGlobalWidth>`.
| **Show traffic node connection** : on/off display the connection to the :ref:`TrafficNode <trafficNode>`.
| **Show selected node settings** : shows :ref:`node settings <pedestrianNodeSettings>` in the inspector.

Buttons
~~~~~~~~~~~~

| **Create node** : create preview node.
| **Add all scene pedestrian nodes** : all nodes will be added to the creator.
| **Add all scene custom pedestrian nodes** : only nodes with custom widths will be added to the creator.

.. _creatorSaveGlobalWidth: 

| **Save global path width** : сhange the width of the route for all nodes.
| **Reset all custom path width** : for all nodes with custom widths will be assigned the default value.
| **Clear created nodes info** : clear the list of nodes created by the creator.
| **Clear selection** : clear selected nodes [multiple selection mode only].
| **Snap to grid** : snap selected node position [for :ref:`selected node <pedestrianNodeCreatorSelect>` only, :ref:`auto snap <pedestrianNodeCreatorSettings>` should be enabled].
| **Open advanced connection window** : open  :ref:`advanced connection window <pedestrianNodeAdvancedConnection>` [for :ref:`selected node <pedestrianNodeCreatorSelect>` only].

.. _pedestrianNodeCreatorHotkeys:

Hotkeys
~~~~~~~~~~~~

	.. image:: images/road/pedestianNode/PedestrianNodeCreatorHotkeyConfig.png

.. _pedestrianNodeAdvancedConnection: 

PedestrianNode Advanced Connection Window
----------------

Help window for advanced node connection settings.

Split Connection
~~~~~~~~~~~~

Split the existing connection into several nodes.

	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/SplitConnection.png
	
| **Target pedestrian node** : selected node where the split connections will be.
| **Split count** : number of new nodes created between the selected two.
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/SplitConnectionExample1.png
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/SplitConnectionExample2.png
	`Split connection example.`

	.. note:: Can split already connected nodes only.

Join To Connection
~~~~~~~~~~~~
	
Connect the selected node to an existing connection.
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/JoinToConnection.png
	
| **Target pedestrian node 1** : target node 1 of selected connection.
| **Target pedestrian node 2** : target node 2 of selected connection.
| **Attach to line** : source node will be moved to the line connecting target nodes.
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/JoinToConnectionExample1.png
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/JoinToConnectionExample2.png
	`Join to connection example 1.`

|
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/JoinToConnectionExample3.png
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/JoinToConnectionExample4.png
	`Join to connection example 2 (attach to line enabled).`

Create Custom Route Width
~~~~~~~~~~~~
	
Create a custom route with custom width between two nodes.
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/CreateCustomRouteWidth.png
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/CreateCustomRouteWidthExample1.png
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/CreateCustomRouteWidthExample2.png
	`Create custom route width example.`

Change Current Route Width
~~~~~~~~~~~~	
	
Set the custom width to the two selected nodes.
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/ChangeCurrentRouteWidth.png
	
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/ChangeCurrentRouteWidthExample1.png
	.. image:: images/road/pedestianNode/AdvancedConnectionWindow/ChangeCurrentRouteWidthExample2.png
	`Change current route width example.`
