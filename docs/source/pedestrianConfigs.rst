Npc Configs
=====

.. _pedestrianConfigs:

.. contents::
   :local:

Pedestrian
============

Pedestrian Spawner Config
------------

	.. image:: images/configs/pedestrian/PedestrianSpawnerConfig.png
	
| **Min pedestrian count** : number of pedestrians in the city.
| **Pool size** : _pedestrianRagdoll
| **Ragdoll pool size* : :ref:`pedestrian ragdoll pool size<pedestrianRagdoll>`.
| **Min/Max spawn delay* : minimum and maximum delay between spawn iterations.
	
.. _pedestrianSettingsConfig:
	
Pedestrian Settings Config
------------

	.. image:: images/configs/pedestrian/PedestrianSettingsConfig.png

**Pedestrian skin type:**
	* **Rig show only in view** : rig skin will be loaded in the camera's view area.
	* **Rig and dummy** : rig will be in the camera's view, and the dummy skin will be out of the camera's view.
	* **Dummy show only in view** : dummy skin will be loaded in the camera's view area.
	* **Rig show always** : rig skin will be loaded when the entity is created and will exist until it is destroyed.
	* **Dummy show always** : dummy skin will be loaded when the entity is created and will exist until it is destroyed..
	* **No skin** : entities without a skin will be created.
**Pedestrian rig type:**
	* **Hybrid legacy** : :ref:`hybrid entity with animator component<pedestrianHybridLegacy>`.
	* **Texture baked** : :ref:`pure entity with gpu animations<pedestrianBaked>`.
	
.. _pedestrianEntityType:

**Pedestrian entity type:**
	* **No physics** : pedestrian not contains `PhysicsShape` component.
	* **Physics** : pedestrian contains `PhysicsShape` component.
| **Pedestrian collider radius** : pedestrian collider radius for `No physics` type.
| **Walking speed** : walking speed.
| **Running speed** : running speed.
| **Rotation speed** : rotation speed.
| **Health** : number of hit points for pedestrians.
| **Talking pedestrian spawn chance** : chance of spawning talking pedestrians
| **Min/Max talk time** : min/max talk time.
**Pedestrian navigation type:**
	* **Temp** : navigation will be enabled if necessary.
	* **Persist** : navigation is always on (for `NavMesh` calculation only).
	* **Disabled**
**Obstacle avoidance type:**
	* **Calc nav path** : navigating based on `NavMesh`.
	* **Local avoidance** : simple obstacle avoidance navigation.
**Pedestrian collision type:**
	* **Calculate** :  collision is calculated manually (:ref:`for NoPhysics type<pedestrianEntityType>`).
	* **Physics** : collision is calculated with `Unity.Physics` (:ref:`for Physics type<pedestrianEntityType>`).
	* **Disabled**
| **Has ragdoll** : on/off :ref:`ragdoll<pedestrianRagdoll>` for pedestrian.

Pedestrian Obstacle Local Avoidance Config
------------

	.. image:: images/configs/pedestrian/PedestrianObstacleLocalAvoidanceSettings.png
	
**Obstacle avoidance method:**
	* **Simple** : is able to avoid only 1 object.
	* **Find neighbors** : multiple objects close to each other are grouped as one (more costly in performance).
| **Max surface angle** : maximum surface tilt angle at which the avoidance is calculated.
| **Target point offset** : offset between an obstacle and avoidance waypoints.
| **Achieve distance** : distance to achieve the avoidance waypoint.
	
Pedestrian Trigger Config
------------

	.. image:: images/configs/pedestrian/PedestrianTriggerConfig.png
	
| **Trigger HashMap capacity** : initial hashmap capacity  that contains data of triggers.
| **Trigger HashMap cell size** : hashmap cell size.
**Trigger data:**
	* **Fear Point Trigger** :
		* **Impact trigger duration** : duration of the :ref:`trigger<pedestrianScaryTrigger>` on the pedestrian.

.. _pedestrianScaryTrigger:

Pedestrian Scary Trigger Config
------------

	.. image:: images/configs/pedestrian/PedestrianScaryTriggerConfig.png
	
**Trigger settings:** 
	* **Death trigger squared distance** : death trigger squared distance (squared distance == distance * distance).
	* **Death trigger duration** : death trigger duration.
		
**Sound settings:** 
	* **Has scream sound** : on/off scream sound.
	* **Scream entity limit** : maximum number of screaming pedestrians at the same time.
	* **Chance to scream** : chance of a pedestrian screaming.
	* **Scream delay** : delay between screams.
	* **Scream sound data** : scream :ref:`sound data<soundData>` source.
		
Pedestrian Bench Config
------------

	.. image:: images/configs/pedestrian/PedestrianBenchConfig.png
	
| **Min/Max idle time** : min/max idle duration on the bench.
| **Custom achieve enter point distance** : distance to achieve the entry point on the bench.
| **Idle after achieved exit duration** : idle after achieved exit point duration.
| **Sitting movement speed** : pedestrian movement speed when sitting on the bench.
| **Sitting rotation speed** : pedestrian turn speed when sitting on the bench.
| **Custom achieve sit point distance** :  distance to achieve the sit point on the bench.
	
Pedestrian Common Sound Config
------------

Common pedestrian sound settings

	.. image:: images/configs/pedestrian/PedestrianCommonSoundConfig.png
	
| **Sound death** : sound when a pedestrian died.
| **Enter tram sound** : sound when entering a tram.
| **Exit tram sound** : sound when exiting a tram.
	
Common Npc Configs
============

Npc Common Config
------------

	.. image:: images/configs/pedestrian/NpcCommonConfig.png
	
| **Npc HashMap capacity** : initial capacity of hashmap containing data about npc (position, state, etc...). 
	
