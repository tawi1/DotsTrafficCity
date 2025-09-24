.. _demoConfigs:

Demo Configs
=====

.. contents::
   :local:
	
Configs
------------

General Settings Config
~~~~~~~~~~~~

Config to quickly on/off optional features.

Where To Find
~~~~~~~~~~~~

	.. image:: /images/configs/common/GeneralSettingsOnScene.png
	
Config Example	
~~~~~~~~~~~~

	.. image:: /images/configs/common/GeneralSettingsConfigDemo.png
		:scale: 70%

Player Settings
^^^^^^^^^^^^^^^^^^^^^^
	
**Player agent type:**
	* **Player** : player will be spawned.
	* **Free fly camera** :	flying camera will be spawned.
	
**Player controller type:**
	* **Built In** : the player spawned by the built-in solution & has an example built-in controller.
	* **Built In Custom** : the player spawned by the built-in solution, but the player NPC has a custom character controller & taken from `PlayerCustomHybridMonoNpcFactory`.
	* **Custom** : the player is spawned & handled entirely by the user's custom solution.
	
**Vehicle interaction type:**
	* **Built In** : the player interacting with cars by the built-in solution.
	* **Custom** : the player interacting with the cars by the custom user solution.
			
**Bullet collision type:** method of calculating collisions for a bullet.
	* **Calculate collision** : manual calculating.
	* **Raycast** : by raycast.
	
**Shoot direction source:**
	* **Joystick** : target of the firing in the direction of the joystick.
	* **Crosshair** : target of the shooting in the direction of the crosshair position.

Player Target Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Max target distance** : maximum distance for crosshair target capture *(crosshair mode only)*.
| **Max capture angle** :	maximum angle for crosshair target capture *(crosshair mode only)*.
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

**World simulation type:**
	* **DOTS** : simulation of traffic & pedestrians entirely in `DOTS` space.
	* **Hybrid mono** : physics simulation run on `Monobehaviour` scripts, but input taken from `DOTS` entities simulation.
	
**Physics simulation type:**
	* **No physics** : dots physics off.
	* **Unity physics** : `Unity` dots physics on.
	* **Havok physics** : `Havok` dots physics on (havok physical package is required).
	
| **Cull physics** : on/off culling of the physics of dynamic objects that are far from the player.
| **Cull static physics** :on/off culling of the physics of static objects that are far from the player.
| **Force legacy physics** : force enable `built-in physics <https://docs.unity3d.com/Manual/PhysicsOverview.html>`_ , otherwise `built-in physics <https://docs.unity3d.com/Manual/PhysicsOverview.html>`_ will be disabled when :ref:`ragdoll <pedestrianRagdoll>` is disabled.
| **Health system support** : on/off health systems for all entities (vehicles, pedestrians, etc...).
| **Navigation support** : on/off navigation systems for pedestrians.
| **Props damage system support** : on/off damage systems for :ref:`props <propsInfo>`.
| **Target FPS** : target fps of the device.
| **Hide UI** : on/off UI.
| **Show FPS** : on/off fps ui panel.
		
Npc Ground Config
~~~~~~~~~~~~

	.. image:: /images/configs/npc/NpcGroundConfig.png

| **Cast distance** : raycast distance.
| **Stop falling distance** : distance from the surface where the landing animation starts.
| **Falling distance** : min distance from the surface where the falling state starts.
| **Grounded distance** : distance from the surface for ground state.

	.. note:: Currently only used for player NPCs.