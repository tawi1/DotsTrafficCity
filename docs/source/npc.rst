.. _npcData:

Npc
=====

.. contents::
   :local:
	
Configs
------------

Npc Common Config
~~~~~~~~~~~~

	.. image:: /images/configs/npc/NpcCommonConfig.png
	
| **Npc HashMap capacity** : initial capacity of the hashmap containing data about the NPC (position, state, etc...). 
	
	.. note:: HashMap contains pedestrian npcs, common nps and player npcs.
		
Npc Ground Config
~~~~~~~~~~~~

	.. image:: /images/configs/npc/NpcGroundConfig.png

| **Cast distance** : raycast distance.
| **Stop falling distance** : distance from the surface where the landing animation starts.
| **Falling distance** : min distance from the surface where the falling state starts.
| **Grounded distance** : distance from the surface for ground state.

	.. note:: Currently only used for player NPCs.