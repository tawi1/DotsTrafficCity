.. _vehicleCollection:

Vehicle Collection
=====

Vehicle collection contains data on all vehicles in the city and their shared settings.

	.. image:: /images/entities/trafficCar/vehicleCollection/VehicleCollection.png
	
	
		.. note::
		:ref:`Fmod plugin <sound>` for sounds should be installed.
	
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
	
#. Select `Settings Type` to `Custom Engine` and `Custom Sound` (if you want override both).

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep3.png
	
#. Customize :ref:`custom sound settings <sharedSoundSettings>`.

	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep4.png
	
#. Add :ref:`custom sounds <sharedSounds>`.
	
	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep4-0.png
	.. image:: /images/entities/trafficCar/vehicleCollection/OverrideStep5.png
		
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

* **Ignition**
* **Idle**
* **Driving**
* **Horn**
* **Enter car**
* **Exit car**		

	.. note::
		:ref:`Fmod plugin <sound>` for sounds should be installed.