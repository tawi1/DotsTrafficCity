.. _commonCarConfigs:

Common Car Configs
=====

.. contents::
   :local:

Car Engine Damage System Settings
------------

	.. image:: /images/configs/cars/CarEngineDamageSystemSettings.png
	
**Damage states:**
	* **Min/max hp** : min/max vehicle health (as % of maximum health) at which engine damage starts to appear.
	* **Prefab** : VFX prefab.
	
.. _carIgnitionConfig:
	
Car Ignition Config
------------

Config used by :ref:`parking states <trafficParking>`.

	.. image:: /images/configs/cars/CarIgnitionConfig.png
	``Hub/Configs/CarConfigs/IgnitionConfig``
	
| **Has ignition** : on/off ignition state of the car when the NPCs enters the car.
| **Idle before start** : idle before starting ignition.
| **Ignition duration** : ignition duration.
| **Engine started time duration** : time to end of ignition state after which the engine start sound is emitted (if value = 0, engine start sound is not emitted).
| **Max pitch** : max pitch of the ignition sound.
| **Max volume** : max volume of ignition sound.
| **Curve blob steps count** : count of steps in the blob curve.
| **Pitch animation curve** : pitch ignition curve. Y - pitch value. X - normalized duration time.
| **Volume animation curve** : volume ignition curve. Y - volume value. X - normalized duration time.
	
.. _carStoppingConfig:
	
Car Stopping Engine Config
------------

	.. image:: /images/configs/cars/CarStoppingEngineConfig.png
	``Hub/Configs/CarConfigs/StoppingEngineConfig``
	
| **Has stop engine** :
| **Stopping duration** :
| **Idle after stopping** :
| **Target min pitch** :
| **Target min volume** :

.. _carCommonSoundConfig:

Car Common Sound Config
------------

	.. image:: /images/configs/cars/CarCommonSoundConfig.png
	``Hub/Configs/CarConfigs/CommonSoundConfig``

| **Collision sound** : sound data for car collisions.
| **Car explode sound** : sound data for car explosions.
| **Bullet hit sound** : sound data for bullet impacts.
| **Npc hit sound** : sound data when a vehicle hits an NPC.

**Sound culling type:**
	* **By Layer** : the sound will be enabled for the vehicle when it's within the player's camera's field of view.
	* **By Distance** : the sound will be enabled when the vehicle is within the player's camera's field of view and the specified radius.

| **Enable distance** : radius distance within which the sound is enabled (active only if *By Distance* culling type is selected).