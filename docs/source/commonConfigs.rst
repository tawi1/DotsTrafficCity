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

	.. image:: /images/configs/common/GeneralSettingsConfig.png
	
**Player agent type:**
	* **Player** : player will be spawned.
	* **Free fly camera** :	flying camera will be spawned.
	
| **Player support** : on/off systems related to the player.
| **Bullet support** : on/off systems related to the bullets.	

**Bullet collision type:** method of calculating collisions for a bullet.
	* **Calculate collision** : manual calculating.
	* **Raycast** : by raycast.
	
**Shoot direction source:**
	* **Joystick** : target of the firing in the direction of the joystick.
	* **Crosshair** : target of the shooting in the direction of the crosshair position.
	
| **Max target distance** : maximum distance for crosshair target capture.
| **Max capture angle** :	maximum angle for crosshair target capture.
| **Default aim point distance** : distance between the player and the crosshair if there is no target.	
| **Default aim point Y position** : default Y-axis crosshair position.	
| **Vehicle mechanics** :	on/off vehicle mechanics system.
| **Car visual damage system support** : on/off visual hit feature for traffic vehicles by bullets.	
| **Has traffic** : on/off traffic vehicle in the city.	
| **Change lane support** : on/off feature to change lanes for traffic.
| **Traffic public support** : on/off public traffic vehicle in the city.	
| **Antistuck support** :	on/off :ref:`antistuck <trafficCarAntistuckConfig>` feature for traffic vehicles.	
| **Car hit collision reaction** : on/off traffic collision reaction to other traffic cars.
| **Wheel system support** : on/off simple wheel system for traffic vehicles.	
| **Has pedestrian** : on/off pedestrians in the city.	
| **Pedestrian trigger system support** : on/off trigger feature for pedestrians (fear running due bullets etc...).

**Physics simulation type:**
	* **No physics** : dots physics off.
	* **Unity physics** : unity dots physics on.
	* **Havok physics** : havok dots physics on (havok physical package is required).
	
| **Health system support** :	on/off health systems for all entities (vehicles, pedestrians, etc...).
| **Navigation support** : on/off navigation systems for pedestrians.

.. _propsDamageOption:

| **Props damage system support** : on/off damage systems for :ref:`props <propsInfo>`.
| **Show fps** : on/off fps ui panel.
	
.. _cullConfig:

Cull Config
~~~~~~~~~~~~

Config of the :ref:`cull point <cullPointInfo>`.

	.. image:: /images/configs/common/CullConfig.png
	
**Has cull:**
	* **Max distance** : maximum distance to activate entities.
	* **Visible distance** : distance to activate visual features of entities.
| **Show debug** : on/off visual culling circle on the scene.
	
.. _streamingLevelConfig:

Streaming Level Config
~~~~~~~~~~~~

Config for loading/unloading subscenes.

	.. image:: /images/configs/common/StreamingLevelConfig.png
	
**Streaming is enabled:**
	* **Distance for streaming in** : distance at what the subscene is loaded.
	* **Distance for streaming out** : distance at what the subscene is unloaded.

Player Configs
-------------------	

Player Npc Sound Config
~~~~~~~~~~~~

	.. image:: /images/configs/common/PlayerNpcSoundConfig.png
	
| **Footstep frequency** : :ref:`sound <soundData>` frequency of the player's footsteps.
	
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

Сonfig for crowd background sound. The sound of the crowd is calculated on the basis of two areas: the inner circle and the outer circle. The sound in the inner circle is louder than the sound in the outer circle.

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
