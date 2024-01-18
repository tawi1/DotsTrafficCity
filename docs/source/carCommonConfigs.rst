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
		
Car Ignition Config
------------

	.. image:: /images/configs/cars/CarIgnitionConfig.png
	
| **Has ignition** : on/off ignition state of the car when the NPCs enters the car.
| **Idle before start** : idle before starting ignition.
| **Ignition duration** : ignition duration.
| **Engine started time duration** : time to end of ignition state after which the engine start sound is emitted (if value = 0, engine start sound is not emitted).
| **Max pitch** : max pitch of the ignition sound.
| **Max volume** : max volume of ignition sound.
| **Curve blob steps count** : count of steps in the blob curve.
| **Pitch animation curve** : pitch ignition curve. Y - pitch value. X - normalized duration time.
| **Volume animation curve** : volume ignition curve. Y - volume value. X - normalized duration time.
	
Car Stopping Engine Config
------------

	.. image:: /images/configs/cars/CarStoppingEngineConfig.png
	
| **Has stop engine** :
| **Stopping duration** :
| **Idle after stopping** :
| **Target min pitch** :
| **Target min volume** :
	
Car Common Sound Config
------------

	.. image:: /images/configs/cars/CarCommonSoundConfig.png

| **Collision sound** :
| **Car explode sound** :
| **Bullet hit sound** :