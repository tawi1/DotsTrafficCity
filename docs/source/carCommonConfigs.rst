.. _commonCarConfigs:

Common Car Configs
==================

.. contents::
   :local:

Car Engine Damage System Settings
---------------------------------

	.. image:: /images/configs/cars/CarEngineDamageSystemSettings.png
	
**Damage states:**
	* **Min/max hp** : vehicle health threshold range (percentage of max HP) where engine smoke/damage VFX begins.
	* **Prefab** : VFX damage prefab to instantiate.
	
.. _carIgnitionConfig:
	
Car Ignition Config
-------------------

Configures engine startup behavior used during :ref:`parking states <trafficParking>`.

	.. image:: /images/configs/cars/CarIgnitionConfig.png
	``Hub/Configs/CarConfigs/IgnitionConfig``
	
| **Has ignition** : enables/disables the engine startup sequence when NPCs enter the vehicle.
| **Idle before start** : initial delay before ignition kicks in.
| **Ignition duration** : total duration of the ignition startup phase.
| **Engine started time duration** : duration threshold after which the startup sound triggers (if 0, sound is omitted).
| **Max pitch** : maximum pitch of the engine startup sound.
| **Max volume** : maximum volume of the startup sound.
| **Curve blob steps count** : resolution steps used for curve evaluation.
| **Pitch animation curve** : pitch curve evaluated over normalized duration time.
| **Volume animation curve** : volume curve evaluated over normalized duration time.
	
.. _carStoppingConfig:
	
Car Stopping Engine Config
--------------------------

Configures engine shutdown behavior when parking or idling.

	.. image:: /images/configs/cars/CarStoppingEngineConfig.png
	``Hub/Configs/CarConfigs/StoppingEngineConfig``
	
| **Has stop engine** : enables/disables the engine shutdown sequence when parking.
| **Stopping duration** : duration of the shutdown sequence in seconds.
| **Idle after stopping** : delay to remain idle after the engine turns off.
| **Target min pitch** : minimum target sound pitch reached during engine spin-down.
| **Target min volume** : minimum target sound volume reached during engine spin-down.

.. _carCommonSoundConfig:

Car Common Sound Config
-----------------------

	.. image:: /images/configs/cars/CarCommonSoundConfig.png
	``Hub/Configs/CarConfigs/CommonSoundConfig``

| **Collision sound** : audio data for vehicle collision impacts.
| **Car explode sound** : audio data for vehicle explosions.
| **Bullet hit sound** : audio data for bullet impacts on vehicle hulls.
| **Npc hit sound** : audio data for collisions with pedestrians.

**Sound culling type:**
	* **By Layer** : audio is active whenever the vehicle is inside the player camera's field of view.
	* **By Distance** : audio is active only when within the camera frustum and within the specified radius.

| **Enable distance** : radius distance within which vehicle sounds are enabled (applies only in *By Distance* mode).