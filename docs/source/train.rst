.. _train:

Train
=====

Mono
------------

How To Create
~~~~~~~~~~~~ 

#. Create a vehicle as well as :ref:`Arcade vehicle <hybridMonoVehicle>`.
#. In the `Traffic preset`, open `Hull` prefab (all presets assigned in `TrafficCarEntityPoolBakerRef`, in this case :ref:`HybridEntityMonoPhysics <entityType>` type).

	.. image:: /images/entities/train/train0-1.png

#. Remove the `ArcadeVehicleController` component & reference to `ArcadeVehicleController` from the `ScriptSwitcher` component.
#. Copy paste parent & unpack prefab for all wagons.

	.. image:: /images/entities/train/train0.png

#. Add `Train Runtime Authoring` to the hull of the train.

	.. image:: /images/entities/train/train2.png
	
#. Add `Train Wagon Runtime Authoring` & `Train Wagon Mono Adapter` components  to the wagons of the train.

	.. image:: /images/entities/train/train3.png
	
#. In the `Train Runtime Authoring` assign all wagons.

	.. image:: /images/entities/train/train4.png
	
#. In the `Traffic preset`, open `Entity` prefab.

	.. image:: /images/entities/train/train5.png
	
#. Add :ref:`Traffic public <trafficPublic>` components.
	
	.. image:: /images/entities/train/train6.png
	
#. In the :ref:`Car Capacity Authoring <trafficPublic>` create entries for pedestrians.
#. Copy paste parent & unpack prefab for all wagons for entity prefab.

	.. image:: /images/entities/train/train7.png
	
#. Add `Traffic Parent Wagon Authoring` to parent & assign created wagons.

	.. image:: /images/entities/train/train8.png
	
#. Create a :ref:`Public route <trafficPublicRoute>` & select `Forbidden/Everything` :ref:`Traffic Group Mask <groupMaskType>` for each path of the route to prevent other vehicles from spawning.

Settings
------------

Train settings for the built-in solution can be found in ``Configs/TrafficCarConfigs/RailConfig/Train Settings``.

	.. image:: /images/entities/train/trainSettings.png
