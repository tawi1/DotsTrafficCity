Common Configs
=====

.. _commonConfigs:

.. contents::
   :local:

Common Configs
-------------------

.. _generalSettingsConfig:

General Settings Config
~~~~~~~~~~~~

Config to quickly on/off optional features.

Where To Find
~~~~~~~~~~~~

	.. image:: /images/configs/common/GeneralSettingsOnScene.png
	
Config Example	
~~~~~~~~~~~~

	.. image:: /images/configs/common/GeneralSettingsConfig.png
		:scale: 70%

Traffic Car Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Has traffic** : on/off traffic vehicle in the city.	

**Traffic baking type:**  
	* **Editor subscene** : all traffic entities are converted at editor subscene time.
	* **Runtime** : all traffic entities are converted at runtime.

| **Change lane support** : on/off feature to change lanes for traffic.
| **Antistuck support** : on/off :ref:`antistuck <trafficCarAntistuckConfig>` feature for traffic vehicles.	
| **Avoidance support** : on/off :ref:`avoidance <trafficAvoidance>` of the vehicles.	
| **Car hit collision reaction** : on/off traffic collision reaction to other traffic cars.
| **Wheel system support** : on/off simple wheel system for traffic vehicles.	

Other Settings
^^^^^^^^^^^^^^^^^^^^^^

**World simulation type:**
	* **DOTS** : simulation of traffic entirely in `DOTS` space.
	* **Hybrid mono** : physics simulation run on `Monobehaviour` scripts, but input taken from `DOTS` entities simulation.
	
**Physics simulation type:**
	* **No physics** : dots physics off.
	* **Unity physics** : `Unity` dots physics on.
	* **Havok physics** : `Havok` dots physics on (havok physical package is required).
	
| **Cull physics** : on/off culling of the physics of dynamic objects that are far from the player.
| **Cull static physics** :on/off culling of the physics of static objects that are far from the player.
| **Force legacy physics** : force enable `built-in physics <https://docs.unity3d.com/Manual/PhysicsOverview.html>`_ .
| **Health system support** : on/off health systems for all entities (vehicles, etc...).

.. _propsDamageOption:

| **Props damage system support** : on/off damage systems for :ref:`props <propsInfo>`.

Sound Configs
-------------------	

.. _soundConfig:

Common Sound Config
~~~~~~~~~~~~

	.. image:: /images/configs/common/CommonSoundConfig.png
	``Hub/Configs/SoundConfigs/SoundConfig``
	
| **Has sounds** : on/off `DOTS` sound systems.
| **Custom audio listener** : custom audio listener will follow the player.
| **Force custom traffic sound** : if this option is enabled, sound logic should be provided by the user.
| **Random horns sound** : on/off horn :ref:`sound <soundData>` system for traffic.