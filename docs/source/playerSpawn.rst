.. _playerSpawner:

Player Spawner
=====

.. contents::
   :local:

Info
-------------------	

| `Player Spawner Service` is used to spawn player in the city.

Available spawn types:
	* NPC: spawns the :ref:`Player NPC <playerNpc>`.
	* Car: spawns the :ref:`Player Car <playerCar>`.
	* Free fly camera : spawns free fly camera (should be set in the :ref:`General Settings <generalSettingsConfig>`)

Where To Find
-------------------	

	.. image:: /images/gettingstarted/PlayerSpawner.png
	
How To Use
-------------------	

* Create :ref:`Player NPC <playerNpc>` & :ref:`Player Car <playerCar>`.
* Select spawn type.

How To Replace
-------------------	

You can replace spawner by your own solution.
By default, `Player Spawner Service` implements `IPlayerSpawnerService` interface & called by `PlayerSpawnCommand.cs` script, create your own `Monobehaviour` class that implements `IPlayerSpawnerService` & assign here:

Steps
~~~~~~~~~~~~

* Find on the scene `PlayerInstaller`:

	.. image:: /images/configs/player/PlayerSpawnerInstaller.png
	
* Assign `Player Spawner Service`:
	
	.. image:: /images/configs/player/PlayerSpawnerInstaller2.png