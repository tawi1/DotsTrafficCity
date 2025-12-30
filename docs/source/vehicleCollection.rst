.. _vehicleCollection:

Vehicle Collection
=====

The `Vehicle collection` contains data on all vehicles in the city and their :ref:`shared settings <sharedSoundSettings>`.

	.. image:: /images/entities/trafficCar/vehicleCollection/VehicleCollection.png
		:scale: 50%
		
	.. note::
		`VehicleDataHolder` contains a reference to the vehicle collection.

How To
----------------
	
Add To Collection
~~~~~~~~~~~~
	
Vehicles can only be added to the collection using the :ref:`Car Prefab Creator <carPrefabCreator>` tool.
	
Override Settings
~~~~~~~~~~~~

Steps
""""""""""""""

#. Tick on `Show Custom Data`.

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep1.png
	
#. Change `Show Type` to `Toolbar`.

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep2-0.png
	
#. Select desired vehicle.
	
	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep2.png
	
#. Select the `Settings Type` to `Custom Engine` and `Custom Sound` (if you want to override both).

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep3.png
	
#. Customize :ref:`custom sound settings <sharedSoundSettings>`.

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep4.png
	
#. Add :ref:`custom sounds <sharedSounds>`.
	
	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep4-0.png
	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep5.png
		
Entity Conversion
~~~~~~~~~~~~

Vehicle collection assigned to the `VehicleDataHolder` and converted in the :ref:`EntitySubScene <subscene>` subscene.

	.. image:: /images/entities/trafficCar/vehicleCollection/VehicleCollectHolder.png

.. _trafficId:

Unique ID
----------------

| **ID** - is the unique, immutable ID based on the main mesh name of the vehicle.

.. _carModel:

Car Model
----------------

| **Car model** - the name of the vehicle that is assigned to the :ref:`Vehicle data <vehicleCollection>` and associated with an immutable :ref:`ID <trafficId>` (the :ref:`ID <trafficId>` can be found in the :ref:`Collection <vehicleCollection>` before the name of the car). 

	.. note::
		You can change the `CarModel` name at any time in the :ref:`Collection <vehicleCollection>` tab.

.. _sharedSoundSettings:

Sound Settings
----------------
	
	.. image:: /images/entities/trafficCar/vehicleCollection/SharedSoundSettings.png
	
| **Min pitch** : minimum pitch of the car engine.
| **Max pitch** : maximum pitch of the car engine.
| **Max load speed** : speed at which the engine has the maximum pitch.
| **Max volume speed** : speed at which the engine has the maximum volume.
| **Min volume** : minimum engine volume.

.. _sharedSounds:

Sounds
----------------

	.. image:: /images/entities/trafficCar/vehicleCollection/SharedSounds.png

* **Ignition** : playback during engine start of the vehicle.
* **Idle** : idle sound of the vehicle.
* **Driving** : plays when pedestrian or player driving the vehicle.
* **Horn** : plays when the horn of the vehicle is active.
* **Enter car** : plays when pedestrian or player enters vehicle.
* **Exit car** : plays when pedestrian or player exits vehicle.		
