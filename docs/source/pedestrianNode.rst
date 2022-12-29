Pedestrian Node
=====

.. _pedestrianNode:

Pedestrian Node
----------------

``Pedestrian node is a node for creating pedestrian routes``

	.. image:: images/configs/road/PedestrianNode.png
	
	**Connected data:**
		**Connected traffic node** : connect traffic node (for parking).
		**Related traffic light handler** : connected traffic light.
		**Auto connected pedestrian nodes** : connected other nodes along selected direction.
		**Default connected pedestrian nodes** : connected other nodes by the user.
		**Directions of auto-connections** : direction of raycasts to connect with other nodes (can be useful for generating squared scenes).
	**Settings:**
		**Pedestrian node type:**
			* **Default** : default node for the route.
			* **Sit** : node for benches, seats, etc. (required `PedestrianNodeSeatSettings` component)
				* **Show seats** : enable editor display of seats.
				* **Base offset** : offset between the center of the seats and the center of the node.
				* **Seat offset** : offset between the seats.
				* **Enter seat offset** : offset between the animation start position and the seat.
				* **Seat height** : seat height.
				* **Capacity** : number of seats (adjustable in the settings of the node).
			* **House** : node for entry/exit to the house.
			* **Idle** : node for temporary idling pedestrians;
			* **Car parking** : node to enter/exit a parked car.
			* **Talk area** : node for crowd conversations of pedestrians.
				* **Area shape type:**
					* **Square**
					* **Circle**
				* **Area size** :
				* **Min/Max spawn count** :
				* **Unlimited talk time** :
				* **Show bounds** :
			**Traffic public stop station** : node for waiting for public transport.
			**Traffic public entry** : node for entering public transport.
		**Can spawn in view** : can spawn in view of camera or not.
		**Capacity** : -1 value is unlimited; Capacity for objects like benchs, houses etc...
		**Priority weight** : weight for choosing random node by pedestrian.
		**Custom achieve distance** : custom achieve distance for pedestrian. If 0 then default value is taken.
		**Chance to spawn** : chance to spawn pedestrian at node: 0 = 0%, 1 = 100%.
		**Max path width** : maximum width of the route around the node.
		**Has movement random offset** : are supposed to randomize the position around a node.
		
Pedestrian Node Creator
----------------

``Pedestrian node is a node for creating pedestrian routes``

	.. image:: images/configs/road/PedestrianNodeCreatorSettings.png
	
	**Settings:**
		**Show handlers**
		**Show handle type:**
			* **Only created**
			* **Only selected**
			* **All**
		**Selection mode:**
			**Single**
			**Multiple**
		**Max path width** :
		**Connect with previous node** :
		**Auto select connected node** :
		**Allow connect traffic node** :
		**Auto split connection** :
			**Disabled** :
			**Right angle** :
			**Custom angle** :
		**Auto rejoin line** :
		**Auto attach to surface** :
			**Surface mask** :
			**Attach type** :
		**Auto snap position** :
			**Snap value** :
	
	.. image:: images/configs/road/PedestrianNodeCreatorSceneSettings.png
	
	**Scene Settings:**
		**Show path** :
		**Show path type:**
			**All** :
			**Only created** :
		**Show node buttons** :
		**Show node type:**
			**Delete**
			**Unselect**
		**Show unique info** :
		**Show reset custom route buttons** :
		**Show border routes** :
		**Show traffic node connection** :
		**Show selected node settings** :

