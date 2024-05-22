.. _playerNpc:

Player Npc
=====

.. contents::
   :local:

Hybrid DOTS
-------------------	

:ref:`Player <playerNpcFactory>` npc components:

Components
~~~~~~~~~~~~

The player NPC behaviour is handled by the `DOTS` systems.

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
~~~~~~~~~~~~

Factory that contains player `Hybrid DOTS` NPCs.

	.. image:: /images/configs/player/PlayerNpcFactory.png
			
Hybrid Mono
-------------------	

The player NPC behaviour is handled by the user's character controller (your own implementation).

Use Cases
~~~~~~~~~~~~

* Useful if you want to simulate :ref:`NPCs <pedestrian>` without traffic with your own controller based on a `Monobehaviour` script (e.g. for different ancient cities).

	.. note:: `DOTS` traffic collision with `Hybrid Mono player` is not implemented yet.
	
Components
~~~~~~~~~~~~

	.. image:: /images/configs/player/PlayerNpcHybridMono.png
	
* **Player actor** : camera tracking component **[required]**.
* **Npc hybrid entity ref** : component that contains the reference to `Entity` **[required]**.
	
	
.. _playerHybridMonoFactory:
	
Factory
~~~~~~~~~~~~

Factory that contains player `Hybrid Mono` NPCs.

	.. image:: /images/configs/player/PlayerNpcHybridMonoFactory.png
