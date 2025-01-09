.. _playerCustom:

User Custom Solution
=====

This topic about how to replace the player with a custom user solution.
	
Player Character
----------------

If you want your own script to spawn player character, follow these steps:

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Player controller type` to `Custom` in the :ref:`General settings <generalSettingsConfig>` config.
#. Disable built-in camera on the scene (this step is irrelevant if you are using the `Hub Base` instead of the `Hub`).

	.. image:: /images/gettingstarted/CityCreation4.png
				
#. Make sure your camera has a :ref:`cull point <cullPointInfo>` object as a child (set local position to zero).
#. Add the `HybridEntityRuntimeAuthoring` component to your prefab.
#. Add `Copy Transform From Game Object`, `Player Npc` components in the `Hybrid components` list.

	.. image:: /images/configs/player/PlayerNpcHybridAuthoring.png
	
#. If you haven't created your own scene yet, you can try the `Demo Mono` scene for tests.
#. Custom player only works with :ref:`Hybrid Mono <hybridMonoVehicle>` vehicles.
#. Your player prefab character is ready.

Player Car
----------------

If you want your own script to spawn player car, follow these steps:

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Player controller type` to `Custom` in the :ref:`General settings <generalSettingsConfig>` config.
#. Disable built-in camera on the scene (this step is irrelevant if you are using the `Hub Base` instead of the `Hub`).

	.. image:: /images/gettingstarted/CityCreation4.png
	
#. Make sure your camera has a :ref:`cull point <cullPointInfo>` object as a child (set local position to zero).
#. Make sure that you created & selected `Hybrid mono` traffic.
#. Add the `HybridEntityRuntimeAuthoring` component to your prefab.
#. Add `Copy Transform From Game Object`, `Custom Raycast Target` , `PlayerCar` components in the `Hybrid components` list.

	.. image:: /images/configs/player/PlayerCarHybridMono.png

#. Add the `Bounds runtime authoring` & `Velocity runtime authoring`  components to your prefab if you want to have :ref:`calculated collisions <pedestrianCollisionType>` with pedestrians. *(optional step)*

	.. image:: /images/configs/player/PlayerCarBounds.png
	`Bounds component example.`
	
	.. image:: /images/configs/player/PlayerCarVelocity.png
	`Velocity component example.`
	
#. Make sure that the traffic :ref:`Raycast config <trafficCarRaycastConfig>` includes a player car layer.	
#. If you haven't created your own scene yet, you can try the `Demo Mono` scene for tests.
#. Custom player car only works with :ref:`Hybrid Mono <hybridMonoVehicle>` vehicles.
#. Your player prefab car is ready.
