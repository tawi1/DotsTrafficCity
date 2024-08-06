.. _playerCar:

Player Car
=====

.. contents::
   :local:

Built-in Solution
----------------

Common Info
~~~~~~~~~~~~

* Each player car only works in :ref:`Hybrid custom physics <entityType>` type & consists of 2 parts: `DOTS` entity is handled by DOTS systems & `Monobehaviour` hybrid skin (required for camera tracking & npc car layout) that follows the binded :ref:`DOTS entity <playerHybridDots>`.
* Player hybrid skin car should have following components:

	* **Player Actor** : camera tracking component.
	* **PlayerNpcCarBehaviour** : logic of the NPC shooting from the car.
	* **CarSlots** : stores the NPC data that is in the car (Npcs sitting in the car are taken from the `PlayerNpcCarFactory`).

	.. note::
		Look at `PlayerCarSkinBase` prefab example.

.. _playerHybridDots:

Hybrid DOTS
~~~~~~~~~~~~

* Player vehicle physics handled by `DOTS` systems.
* The hybrid skin follows the `DOTS` entity.

How To Create
""""""""""""""

#. Open :ref:`Car Prefab Creator <carPrefabCreator>` & set `Car type` to `Player` in the `Prefab` tab.
#. Set `Player simulation type` to `Hybrid DOTS` in the `Prefab` tab.
#. Make sure `Player simulation type` is set to :ref:`Hybrid DOTS <playerHybridDotsConfig>` in the player car settings (make sure that config on the :ref:`subscene <subscene>` has the same value).
#. Create a vehicle using the :ref:`Car Prefab Creator <carPrefabCreator>` tool.
#. Create prefab variant from the `PlayerCarSkinBase` prefab & assign to :ref:`Player Car Pool <playerCarPool>` according to the vehicle.
#. Customize the car slots in the created prefab if you plan to make the NPC's shooting option from the car **[optional step]**.
#. Enable spawn type to `Car` & select desired `Car model` from the list in the :ref:`PlayerSpawner <playerSpawner>`, if you want the player to spawn in a car initially **[optional step]**.
#. Once all the steps have been completed, reopen :ref:`subscene <subscene>`.

.. _playerHybridMono:

Hybrid Mono
~~~~~~~~~~~~

* Player vehicle physics handled by custom user's `Monobehaviour physics plugin`.
* Unlike the :ref:`Hybrid DOTS <playerHybridDots>`, the entity following & presents collider for `DOTS` world without mesh representation.

* List of vehicle controllers from the Asset Store that can be used for (e.g.) 
	* `Edy's Vehicle Physics <https://assetstore.unity.com/packages/tools/physics/edy-s-vehicle-physics-403>`_
	* `Realistic Car Controller Pro <https://assetstore.unity.com/packages/tools/physics/realistic-car-controller-pro-178967>`_
	* `NWH Vehicle Physics 2 <https://assetstore.unity.com/packages/tools/physics/nwh-vehicle-physics-2-166252>`_
	* `Universal Vehicle Controller Plus <https://assetstore.unity.com/packages/tools/physics/universal-vehicle-controller-plus-176314>`_
	* `MS Vehicle System <https://assetstore.unity.com/packages/tools/physics/ms-vehicle-system-vehicle-controller-88035>`_
	* `Sim-Cade Vehicle Physics <https://assetstore.unity.com/packages/tools/physics/sim-cade-vehicle-physics-243624>`_

How To Create
""""""""""""""

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config (make sure that config on the :ref:`subscene <subscene>` has the same value).
#. Open the :ref:`Car Prefab Creator <carPrefabCreator>` & set `Car type` to `Player` in the `Prefab` tab.
#. Set `Entity type` to `Hybrid entity mono physics` in the `Save` tab.
#. Drag & drop your desired prefabs into the `Prefabs` field.
#. Click the `Scan` button.
#. Customize :ref:`Save settings <carPrefabCreatorSaveSettings>` in the `Save` tab.
#. In the `Prefab Info` tab, enter the vehicle :ref:`ids <trafficId>` (:ref:`ids <trafficId>` should match the traffic cars :ref:`ids <trafficId>` if you want to make option enter & exit for the player npc).
#. Click the `Create` button.
#. Ensure that the bounds of the entities created match the prefabs you have selected.
#. Input for the player vehicle is implemented according to your vehicle controller plugin.
#. The input enable & disable for the car when the player's npc exits & enters the car should be implemented in the `PlayerInteractCarService.cs` in the `EnterCar` & `ExitCar` methods.
#. Enable spawn type to `Car` & select desired `Car model` from the list in the :ref:`PlayerSpawner <playerSpawner>`, if you want the player to spawn in a car initially **[optional step]**.
#. Once all the steps have been completed, reopen :ref:`subscene <subscene>`.

.. _playerCarPool:

Player Car Pool
~~~~~~~~~~~~

Where To Find
""""""""""""""

In the scene:

	``Hub/Pools/Car/PlayerCarPool``
	
	.. image:: /images/configs/player/PlayerCarPool.png
	
How To Use
""""""""""""""

Player cars spawned by `PlayerCarSpawner`.

Example
""""""""""""""

	.. image:: /images/configs/player/PlayerCarPoolExample.png
	
Custom User Solution
----------------

If you want your own script to spawn player car, follow these steps:

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Player controller type` to `Custom` in the :ref:`General settings <generalSettingsConfig>` config.
#. Disable built-in camera on the scene.
#. Make sure your camera has a :ref:`cull point <cullPointInfo>` object as a child.
#. Make sure that you created & selected `Hybrid mono` traffic.
#. Add the `HybridEntityRuntimeAuthoring` component to your prefab.
#. Add `Copy Transform From Game Object`, `Custom Raycast Target` , `PlayerCar` components in the `Hybrid components` list.

	.. image:: /images/configs/player/PlayerCarHybridMono.png

#. Add the `Bounds runtime authoring` component to your prefab.

	.. image:: /images/configs/player/PlayerCarBounds.png
	
#. Make sure that the traffic :ref:`Raycast config <trafficCarRaycastConfig>` includes a player car layer.	
#. If you haven't created your own scene yet, you can try the `Demo Mono` scene for tests.
#. Your player prefab car is ready.
