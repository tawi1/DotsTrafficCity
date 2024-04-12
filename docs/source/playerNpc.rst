.. _playerNpc:

Player Npc
=====

.. contents::
   :local:

Components
-------------------	

:ref:`Player <playerNpcFactory>` npc components:

	.. image:: /images/configs/player/PlayerNpcComponents.png
	
* **Player actor** : camera tracking component **[required]**.
* **Npc behaviour entity** : holds reference to bind entity & read input from `DOTS entity world`, also controls animator & npc weapon behaviour **[required]**.
* **Npc weapon holder** : reference to the anchor bone that holds the weapon & reference to the weapon.
* **Npc hit reaction behaviour** : behaviour that handles the reaction to a bullet hit.
* **Ragdoll base** : activates `Ragdoll` when the NPC dies.
* **Npc health entity behaviour** : wrapper for entity health in the `Monobehaviour` world.

	.. note::
	
		* Spawned by `PlayerSpawner`.
			.. image:: /images/configs/player/PlayerSpawner.png
		
		* Entity movement controlled by systems:
			* `NpcControllerSystem`.
			* `NpcGroundStateSystem`.
			* `NpcRaycastGroundSystem`.
			* `NpcFreezeVerticalRotationSystem`.
	
.. _playerNpcFactory:
	
Factory
-------------------	

Factory that contains player NPCs;

	.. image:: /images/configs/player/PlayerNpcFactory.png