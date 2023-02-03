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
	
.. cullConfig:

Cull Config
~~~~~~~~~~~~

Config of the :ref:`cull point <cullPointInfo>`.

	.. image:: /images/configs/common/CullConfig.png
	
**Has cull:**
	* **Max distance** : maximum distance to activate entities.
	* **Visible distance** : distance to activate visual features of entities.
| **Show debug** : on/off visual culling circle on the scene.
	
.. streamingLevelConfig:

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
	
| **Footstep frequency** : sound frequency of the player's footsteps.
	
Sound Configs
-------------------	

.. _soundConfig:

Common Sound Config
~~~~~~~~~~~~

	.. image:: /images/configs/common/CommonSoundConfig.png
	
| **Has sounds** : on/off dots sound systems.
| **Crowd sound** : on/off crowd sound system for pedestrians.
| **Random hornes sound** : on/off horne sound system for traffic.
	
Crowd Sound Config
~~~~~~~~~~~~

	.. image:: /images/configs/common/CrowdSoundConfig.png
	
| **Crowd sound data** : crowd sound data.
| **Inner crowd sound count** :
| **Outer crowd sound count** :
| **Min crowd sound count** :
| **Max volume** : maximum volume level for the crowd sound.
| **Outer max volume** :
| **Min volume** : minimum volume level for the crowd sound.
| **Inner cell offset** :
| **Outer cell offset** :
| **Lerp volume speed** :
