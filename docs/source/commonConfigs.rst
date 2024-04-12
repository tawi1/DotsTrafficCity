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

Player Settings
^^^^^^^^^^^^^^^^^^^^^^
	
**Player agent type:**
	* **Player** : player will be spawned.
	* **Free fly camera** :	flying camera will be spawned.
	
| **Player support** : on/off systems related to the player.

**Bullet collision type:** method of calculating collisions for a bullet.
	* **Calculate collision** : manual calculating.
	* **Raycast** : by raycast.
	
**Shoot direction source:**
	* **Joystick** : target of the firing in the direction of the joystick.
	* **Crosshair** : target of the shooting in the direction of the crosshair position.

Player Target Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Max target distance** : maximum distance for crosshair target capture.
| **Max capture angle** :	maximum angle for crosshair target capture.
| **Default aim point distance** : distance between the player and the crosshair if there is no target.	
| **Default aim point Y position** : default Y-axis crosshair position.	

Common Car Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Car visual damage system support** : on/off visual hit feature for traffic vehicles by bullets.	

Traffic Car Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Has traffic** : on/off traffic vehicle in the city.	

**Traffic baking type:**  
	* **Editor subscene** : all traffic entities are converted at editor subscene time.
	* **Runtime** : all traffic entities are converted at runtime.

| **Change lane support** : on/off feature to change lanes for traffic.
| **Traffic public support** : on/off public traffic vehicle in the city.	
| **Antistuck support** : on/off :ref:`antistuck <trafficCarAntistuckConfig>` feature for traffic vehicles.	
| **Avoidance support** : on/off :ref:`avoidance <trafficAvoidance>` of the vehicles.	
| **Car hit collision reaction** : on/off traffic collision reaction to other traffic cars.
| **Wheel system support** : on/off simple wheel system for traffic vehicles.	

Pedestrian Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Has pedestrian** : on/off pedestrians in the city.	

**Pedestrian baking type:**  
	* **Editor subscene** : all pedestrian entities are converted at editor subscene time.
	* **Runtime** : all pedestrian entities are converted at runtime.
	
| **Pedestrian trigger system support** : on/off trigger feature for pedestrians (fear running due bullets etc...).

Other Settings
^^^^^^^^^^^^^^^^^^^^^^

**Physics simulation type:**
	* **No physics** : dots physics off.
	* **Unity physics** : `Unity` dots physics on.
	* **Havok physics** : `Havok` dots physics on (havok physical package is required).
	
| **Cull physics** : on/off culling of the physics of dynamic objects that are far from the player.
| **Cull static physics** :on/off culling of the physics of static objects that are far from the player.
| **Force legacy physics** : force enable `built-in physics <https://docs.unity3d.com/Manual/PhysicsOverview.html>`_ , otherwise `built-in physics <https://docs.unity3d.com/Manual/PhysicsOverview.html>`_ will be disabled when :ref:`ragdoll <pedestrianRagdoll>` is disabled.
| **Health system support** : on/off health systems for all entities (vehicles, pedestrians, etc...).
| **Navigation support** : on/off navigation systems for pedestrians.

.. _propsDamageOption:

| **Props damage system support** : on/off damage systems for :ref:`props <propsInfo>`.
| **Target FPS** : target fps of the device.
| **Hide UI** : on/off UI.
| **Show FPS** : on/off fps ui panel.

Sound Configs
-------------------	

.. _soundConfig:

Common Sound Config
~~~~~~~~~~~~

	.. image:: /images/configs/common/CommonSoundConfig.png
	
| **Has sounds** : on/off `DOTS` sound systems.
| **Crowd sound** : on/off :ref:`crowd sound <soundCrowdConfig>` system for pedestrians.
| **Random horns sound** : on/off horn :ref:`sound <soundData>` system for traffic.
	
.. _soundCrowdConfig:
	
Crowd Sound Config
~~~~~~~~~~~~

Сonfig for crowd background sound. The sound of the crowd is calculated based on of two areas: the inner circle and the outer circle. The sound in the inner circle is louder than the sound in the outer circle.

	.. image:: /images/configs/common/CrowdSoundConfig.png
	
| **Crowd sound data** : crowd :ref:`sound <soundData>` data.
| **Inner crowd sound count** : maximum volume for a given number of pedestrians in the inner circle.
| **Outer crowd sound count** : maximum volume for a given number of pedestrians in the outer circle.
| **Min crowd sound count** : minimum number of pedestrians to play the crowd sound.
| **Max volume** : maximum volume level for the crowd sound.
| **Outer max volume** : maximum volume in the outer circle.
| **Min volume** : minimum volume level for the crowd sound.
| **Inner cell offset** : offset of neighbouring cells relative to current cell in hashmap in the inner circle.
| **Outer cell offset** : offset of neighbouring cells relative to current cell in hashmap in the outer circle.
| **Lerp volume speed** : speed of sound volume change between current value and target value.
