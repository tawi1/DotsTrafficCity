.. _pedestrianEntity:

Pedestrian
=====

.. contents::
   :local:


How To Create
----------------

.. _pedestrianHybridLegacy:

Hybrid legacy skin
~~~~~~~~~~~~

`Hybrid legacy skin` is a :ref:`hybrid entity <hybridEntity>` that combines the default `GameObject` (with animator) and the DOTS entity.

Factory
""""""""""""""

	#. Open on the scene `PedestrianSkinFactory`.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianSkinFactory``

		.. image:: /images/configs/pedestrian/PedestrianSkinFactory.png
	
	#. Enable `Show Add New Prefab Settings`.
	#. Drag & drop source prefabs to the `New Prefabs` field.
	#. Customize prefab names.
	#. Click `Try To Add Prefabs`.
	#. If you needed configure :ref:`Ragdoll <pedestrianRagdoll>` and assign to the `Pedestrian Skin Factory Data` (make sure ragdoll is :ref:`enabled <pedestrianSettingsConfig>`).

	.. note:: 
		Every `hybrid legacy` pedestrian prefab should have `PedestrianReferences` component.
		
How To Use
""""""""""""""

| **Code example:**

..  code-block:: r
	
	Entities
	.WithoutBurst()
	.ForEach((
		Entity entity,
		Animator animator) =>
	{
		animator.SetFloat("yInput", 1f);
	}).Run();
		
**Used in systems:**
	* PedestrianLegacyAnimatorSystem
	* PedestrianSittingLegacyAnimatorSystem

.. _pedestrianBaked:

Baked skin
~~~~~~~~~~~~

`Baked skin` is a :ref:`pure entity <pureEntity>` that combines the GPU baked animations and the DOTS entity.

.. _pedestrianBakedFactory:

Factory
""""""""""""""

	#. :ref:`Create textures and animation sheets <animationBaker>`.
	#. Create :ref:`Animation Collection <animationBakerAnimationCollection>` in the project context menu.
	
		``Spirit604/Animation Baker/Animation Collection``
	
		.. image:: /images/pedestrian/baker/animator/AnimationCollectionExample.png
	
	#. Add and customize desired animations data.
	#. Open on the scene `PedestrianBakedSkinFactory`.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianBakedSkinFactory``

	#. Assign :ref:`Animation Collection <animationBakerAnimationCollection>` to `PedestrianBakedSkinFactory`.
	
		.. image:: /images/pedestrian/baker/AddNewEntryPanelExample.png
			
	#. Click `+` to show `New Entry` panel.
	
		.. image:: /images/pedestrian/baker/NewEntry.png
	
	#. Enter pedestrian entry name & assign `Skinned Mesh Renderer` or `Mesh` of the target pedestrian.
	#. Click `Add Entry`.	
	
	#. Select created :ref:`Baked Animation Sheet Data <animationBakerAnimationSheetData>`.
	
		.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample.png
		
	#. Select the animation in the inspector that you want to assign to the selected character.
	
		.. image:: /images/pedestrian/baker/PedestrianAnimationsAssignExample.png
			
	#. Press the `Assign` button according to the selected animation in :ref:`Baked Animation Sheet Data <animationBakerAnimationSheetData>`.
	#. Assign values for each animation in the same way.
	
.. _animationBakerAnimationSheetData:

Baked Animation Sheet Data
""""""""""""""

Data about baked animations in texture (:ref:`How to create <animationBakerHowTo>`). 
	
	.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample.png	
	
Baked Custom Animator
""""""""""""""

Baked Custom animator is used for transitions between baked animations (implemented by `PedestrianBakedTransitionAnimatorSystem` system).

.. _animationBakerHowToCreateTransition:

**How To Create Transition:**
	#. Open on the scene `PedestrianBakedAnimatorAuthoring`.
	
		``Hub/Configs/BakerRefs/Settings/PedestrianBakedAnimatorAuthoring``
		
		.. image:: /images/pedestrian/baker/animator/PedestrianBakedAnimatorAuthoring.png

				
	#. Create :ref:`Animator Data Container <animationBakerAnimatorContainer>` in the project context menu and assign to animator (if necessary).
	#. Assign :ref:`Animation Collection <animationBakerAnimationCollection>` the same as in the :ref:`PedestrianBakedFactory<pedestrianBakedFactory>`.
	#. Press `Open Animator` button.
	#. Create :ref:`new transition layer <animationBakerAnimatorNewTransitionLayer>` (if needed).
	#. Enter the name of the trigger in the :ref:`StartNode <animationBakerAnimatorStartNode>`.
	#. Create and connect :ref:`AnimationNode <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
		.. image:: /images/pedestrian/baker/animator/StartSitTransitionExample.png
		`Start sit transition example.`
		
		.. image:: /images/pedestrian/baker/animator/SitoutTransitionExample.png		

		`Sitout transition example.`
	
	#. Copy & paste :ref:`generated hash <animationBakerAnimatorTriggerHash>` from `AnimatorContainer` to code (:ref:`usage example <pedestrianBakedFactoryTransitionExample>`).
		
		.. image:: /images/pedestrian/baker/animator/AnimatorContainerExample.png		

How To Use
""""""""""""""

**Simple switch animation code example:**
	
..  code-block:: r
    
	Entities
	.WithoutBurst()
	.WithNone<UpdateSkinTag>()
	.WithAll<HasSkinTag, BakedSkinTag>()
	.ForEach((
		Entity entity,
		ref BakedUpdateSkinComponent bakedUpdateSkinComponent) =>
	{
		bakedUpdateSkinComponent.NewAnimationHash = PedestrianBakedAnimationsConstans.SittingIdle_Anim_Hash; //int animation hash
		commandBuffer.SetComponentEnabled<UpdateSkinTag>(entity, true);
	}).Schedule();
	

.. _pedestrianBakedFactoryTransitionExample:

**Complex animation transition code example:**

..  code-block:: r
	
	public partial class PedestrianSittingBakedAnimatorExampleSystem : SystemBase
	{
		private const int StartSitAnimHash = -1880722739; //StartSit hash trigger

		private BeginPresentationEntityCommandBufferSystem entityCommandBufferSystem;
		private PedestrianBakedTransitionProviderSystem pedestrianBakedTransitionProviderSystem;

		protected override void OnCreate()
		{
			base.OnCreate();
			entityCommandBufferSystem = World.GetOrCreateSystemManaged<BeginPresentationEntityCommandBufferSystem>();
			pedestrianBakedTransitionProviderSystem = World.DefaultGameObjectInjectionWorld.GetOrCreateSystemManaged<PedestrianBakedTransitionProviderSystem>();
		}

		protected override void OnUpdate()
		{
			var transitions = pedestrianBakedTransitionProviderSystem.Transitions;

			if (!transitions.IsCreated)
			{
				return;
			}

			var commandBuffer = entityCommandBufferSystem.CreateCommandBuffer();

			Entities
			.WithoutBurst()
			.WithReadOnly(transitions)
			.WithAll<HasSkinTag, BakedSkinTag>()
			.ForEach((
				Entity entity,
				ref AnimationTransitionData animationTransitionData) =>
			{
				Entity animStateEntity = Entity.Null;

				transitions.TryGetValue(StartSitAnimHash, out animStateEntity);

				if (animStateEntity != Entity.Null)
				{                 
					animationTransitionData.CurrentAnimationState = animStateEntity;
					commandBuffer.SetComponentEnabled<HasAnimTransitionTag>(entity, true);
				}
			}).Schedule();
			
			entityCommandBufferSystem.AddJobHandleForProducer(Dependency);
		}
	}

**Used in systems:**
	* PedestrianLoadBakedSkinSystem
	* PedestrianBakedTransitionAnimatorSystem
	* PedestrianSittingBakedAnimatorSystem

.. _pedestrianRagdoll:

Ragdoll
~~~~~~~~~~~~

Ragdoll is created at the scene of the pedestrian's death. Make sure ragdoll is :ref:`enabled <pedestrianSettingsConfig>`.

**How To Create:**
	* Add all colliders and rigidbodies according to the tutorial `RagdollWizard <https://docs.unity3d.com/2021.1/Documentation/Manual/wizard-RagdollWizard.html>`_ to character.
	* Add `PedestrianRagdoll` component.
	* Assign the result to :ref:`PedestrianHybridLegacyFactory <pedestrianHybridLegacy>` or :ref:`PedestrianBakedFactory <pedestrianBaked>` according to the chosen :ref:`type of rig <pedestrianSettingsConfig>`.
	
	.. note:: Implemented by `PedestrianRagdollSystem`.


.. _pedestrianNavigation:

Navigation
----------------

| Navigation is used for pedestrian obstacle avoidance.
| There are 2 types of navigation:

.. _pedestrianNavmeshNavigation:

NavMesh Navigating
~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ (:ref:`test scene <pedestrianNavigationTest>`).

Installation
""""""""""""""

* Check that the :ref:`navigation package <packageInstallationOptional>` is installed.
* Make sure that navigation is enabled in the :ref:`general config <generalSettingsConfig>`.
* Make sure :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Each dynamic object on the scene must have a `NavMeshObstacle <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshObstacle.html>`_ component.

How To Enable
""""""""""""""

* Create & customize `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_.
* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` Or `Persist` mode.
* Set :ref:`Obstacle avoidance type <pedestrianObstacleAvoidanceType>` to `Calc nav path`.
		
Pros And Cons
""""""""""""""
	
Pros:
	* High precision.
	* Can avoid any obstacle.
	
Cons:
	* High CPU load.

.. _pedestrianLocalAvoidance:

Local Avoidance 
~~~~~~~~~~~~

DOTS system for avoiding local obstacles (vehicles).

Useful links:
	* :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.

How To Enable
""""""""""""""

* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` mode.
* Set :ref:`Obstacle avoidance type <pedestrianObstacleAvoidanceType>` to `Local avoidance`.

Pros And Cons
""""""""""""""

Pros:
	* Low CPU load.
	
Cons:
	* Can avoid vehicles only.
	* Works on flat surfaces only.

Authoring Components
----------------

PedestrianAuthoring
~~~~~~~~~~~~

Contains the main components of pedestrian entity **[required]**.

PlayerTargetAuthoring
~~~~~~~~~~~~

Component for player targeting systems **[optional]**.

Physics
~~~~~~~~~~~~

`PhysicsBody` and `PhysicsShape` components for physics related systems **[optional]**.

States
----------------

**Movement State:**
	* **Default**
	* **Idle**
	* **Walking**
	* **Running**

.. _pedestrianActionState:

**Pedestrian Action State:**
	* **Default** : no state.
	* **Idle** : when a pedestrian is waiting.
	* **MovingToNextTargetPoint** : when going from `PedestrianNode <pedestrianNode>` to `PedestrianNode <pedestrianNode>` (excluding crosswalk).
	* **WaitForGreenLight** : when a pedestrian is waiting for a green traffic light.
	* **CrossingTheRoad** : when a pedestrian goes crossing a crosswalk.
	* **ScaryRunning** : activated when a pedestrian runs away in a panic (for example, the sound of a gunshot or the death of a pedestrian nearby).
	* **Sitting** : when a pedestrian sits.
	* **Talking** : when a pedestrian talks.

.. _pedestrianConfigs:

Configs
----------------

Pedestrian Spawner Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSpawnerConfig.png
	
| **Min pedestrian count** : number of pedestrians in the city.
| **Pool size** : pool size of :ref:`HybridLegacy <pedestrianHybridLegacy>` skins.
| **Ragdoll pool size** : :ref:`pedestrian ragdoll pool size<pedestrianRagdoll>`.
| **Min/Max spawn delay** : minimum and maximum delay between spawn iterations.
	
.. _pedestrianSettingsConfig:
	
Pedestrian Settings Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSettingsConfig.png

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

.. _pedestrianNavigationType:

**Pedestrian navigation type:**
	* **Temp** : navigation will be enabled if there is an obstacle in front of pedestrian.
	* **Persist** : navigation is always on (for :ref:`NavMesh <pedestrianNavmeshNavigation>` calculation only).
	* **Disabled**
	
.. _pedestrianObstacleAvoidanceType:
	
**Obstacle avoidance type:**
	* **Calc nav path** : navigating based on :ref:`NavMesh <pedestrianNavmeshNavigation>`.
	* **Local avoidance** : simple :ref:`obstacle avoidance <pedestrianLocalAvoidance>` navigation .
	
**Pedestrian collision type:**
	* **Calculate** :  collision is calculated manually (:ref:`for NoPhysics type<pedestrianEntityType>`).
	* **Physics** : collision is calculated with `Unity.Physics` (:ref:`for Physics type<pedestrianEntityType>`).
	* **Disabled**
	
| **Has ragdoll** : on/off :ref:`ragdoll<pedestrianRagdoll>` for pedestrian.

.. _pedestrianLocalAvoidanceConfig:

Pedestrian Obstacle Local Avoidance Config
~~~~~~~~~~~~

Config for :ref:`Local Avoidance <pedestrianLocalAvoidance>` navigating.

	.. image:: /images/configs/pedestrian/PedestrianObstacleLocalAvoidanceSettings.png
	
**Obstacle avoidance method:**
	* **Simple** : is able to avoid only 1 object.
	* **Find neighbors** : multiple objects close to each other are grouped as one (more costly in performance).
| **Max surface angle** : maximum surface tilt angle at which the avoidance is calculated.
| **Target point offset** : offset between an obstacle and avoidance waypoints.
| **Achieve distance** : distance to achieve the avoidance waypoint.
	
Pedestrian Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianTriggerConfig.png
	
| **Trigger HashMap capacity** : initial hashmap capacity  that contains data of triggers.
| **Trigger HashMap cell size** : hashmap cell size.
**Trigger data:**
	* **Fear Point Trigger** :
		* **Impact trigger duration** : duration of the :ref:`trigger<pedestrianScaryTrigger>` on the pedestrian.

.. _pedestrianScaryTrigger:

Pedestrian Scary Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianScaryTriggerConfig.png
	
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
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianBenchConfig.png
	
| **Min/Max idle time** : min/max idle duration on the bench.
| **Custom achieve enter point distance** : distance to achieve the entry point on the bench.
| **Idle after achieved exit duration** : idle after achieved exit point duration.
| **Sitting movement speed** : pedestrian movement speed when sitting on the bench.
| **Sitting rotation speed** : pedestrian turn speed when sitting on the bench.
| **Custom achieve sit point distance** :  distance to achieve the sit point on the bench.
	
Pedestrian Common Sound Config
~~~~~~~~~~~~

Common pedestrian sound settings

	.. image:: /images/configs/pedestrian/PedestrianCommonSoundConfig.png
	
| **Sound death** : :ref:`sound<soundData>` when a pedestrian died.
| **Enter tram sound** : :ref:`sound<soundData>` when entering a tram.
| **Exit tram sound** : :ref:`sound<soundData>` when exiting a tram.