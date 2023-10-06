.. _pedestrianEntity:

Pedestrian
=====

.. contents::
   :local:


How To Create
----------------

.. _pedestrianHybridLegacy:

Hybrid Legacy Skin
~~~~~~~~~~~~

`Hybrid legacy skin` is a :ref:`hybrid entity <hybridEntity>` that combines the default `GameObject` (with `animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_) and the DOTS entity.

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

.. _pedestrianGPU:

Pure GPU Skin
~~~~~~~~~~~~

`Pure GPU skin` is a :ref:`pure entity <pureEntity>` that combines the GPU texture animations and the DOTS entity.

.. _pedestrianCrowdSkinFactory:

Factory
""""""""""""""

	#. :ref:`Create textures and animation sheets <animationBaker>`.
	#. Create :ref:`Animation Collection <animationGPUAnimationCollection>` in the project context menu.
	
		``Spirit604/Animation Baker/Animation Collection``
	
		.. image:: /images/pedestrian/baker/animator/AnimationCollectionExample.png
	
	#. Add and customize desired animations data.
	#. Open on the scene `PedestrianCrowdSkinFactory`.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianCrowdSkinFactory``

	#. Assign :ref:`Animation Collection <animationGPUAnimationCollection>` to `PedestrianCrowdSkinFactory`.
	
		.. image:: /images/pedestrian/baker/AddNewEntryPanelExample.png
		
	#. Click `+` to show `New Entry` panel.
	
		.. image:: /images/pedestrian/baker/NewEntry.png
			
	#. Select created :ref:`Baked Animation Sheet Data <animationTextureData>`.
	
		.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample.png
			
	#. Open factory settings.
	#. Select `Entry Key Source Type` to `Selected Mesh Name` (or select `Custom` if you want to enter the name manually).
	
		.. image:: /images/pedestrian/baker/SettingsExample1.png
			
	#. Select `Entry Mesh Source Type` to `Selected Sheet` (or select `Custom` if you want to enter the mesh data manually).

		.. image:: /images/pedestrian/baker/SettingsExample2.png
		
	#. Assign `Default Atlas Texture` (if selected pedestrians has the same texture material). **[optional step]**

		.. image:: /images/pedestrian/baker/SettingsExample3.png
			
	#. One by one click `Select` and `Add entry` button. Or click `Add all entries` button to add all entries in the container.	
	
		.. image:: /images/pedestrian/baker/NewEntry2.png
			
	#. Turn on `Find Related Animations` button.
	
		.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample2.png
			
	#. Generate Animation Material.
		#. Assign main texture of selected model **[if missing]**.
		#. Press `Generate` button.
	
			.. image:: /images/pedestrian/baker/GenerateMaterialExample.png
		
	#. Select entry & assign animations:
	
		#. **Manual way:**
			#. Select the animation in the inspector that you want to assign to the selected character.
		
				.. image:: /images/pedestrian/baker/PedestrianAnimationsAssignExample.png
				
			#. Press the `Assign` button according to the selected animation in :ref:`Animation Texture Data <animationTextureData>`.
		
		#. **Automated way:**
			#. Automatic assignment works if the animation in the list matches (or partially matches) the animation name in the selected container.
			#. Press `Auto Bind Animations` button.
			#. Make sure, that all animations are assigned.
			
				.. image:: /images/pedestrian/baker/PedestrianAnimationsAssignExample2.png

	#. Assign animations for each entry in the same way.
	#. Assign :ref:`ragdolls <pedestrianRagdoll>`. **[optional step]**.
	
		.. image:: /images/pedestrian/baker/PedestrianGPURagdolleExample.png
	
.. _animationTextureData:

Animation Texture Data
""""""""""""""

Data about baked animations in texture (:ref:`How to create <animationBakerHowTo>`). 
	
	.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample3.png	
	
Crowd GPU Custom Animator
""""""""""""""

Crowd GPU Custom animator is used for transitions between baked animations (implemented by `CrowdAnimatorTransitionSystem` system).

.. _animationBakerHowToCreateTransition:

**How To Create Transition:**
	#. Open on the scene `CrowdGPUAnimatorAuthoring`.
	
		``Hub/Configs/BakerRefs/Settings/CrowdGPUAnimatorAuthoring``
		
		.. image:: /images/pedestrian/baker/animator/PedestrianBakedAnimatorAuthoring.png

				
	#. Create :ref:`Animator Data Container <animationGPUAnimatorContainer>` in the project context menu and assign to animator (if necessary).
	#. Assign :ref:`Animation Collection <animationGPUAnimationCollection>` the same as in the :ref:`PedestrianCrowdSkinFactory <pedestrianCrowdSkinFactory>`.
	#. Press `Open Animator` button.
	#. Create :ref:`new transition layer <animationBakerAnimatorNewTransitionLayer>` (if needed).
	#. Enter the name of the trigger in the :ref:`StartNode <animationBakerAnimatorStartNode>`.
	#. Create and connect :ref:`AnimationNode <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
		.. image:: /images/pedestrian/baker/animator/StartSitTransitionExample.png
		`Start sit transition example.`
		
		.. image:: /images/pedestrian/baker/animator/SitoutTransitionExample.png		

		`Sitout transition example.`
	
	#. Copy & paste :ref:`generated hash <animationBakerAnimatorTriggerHash>` from `AnimatorContainer` to code (:ref:`usage example <pedestrianGPUFactoryTransitionExample>`).
		
		.. image:: /images/pedestrian/baker/animator/AnimatorContainerExample.png		

How To Use
""""""""""""""

**Simple switch animation code example:**
	
..  code-block:: r
    
	Entities
	.WithoutBurst()
	.WithNone<UpdateSkinTag>()
	.WithAll<HasSkinTag, GPUSkinTag>()
	.ForEach((
		Entity entity,
		ref GPUSkinUpdateComponent gpuSkinUpdateComponent) =>
	{
		gpuSkinUpdateComponent.NewAnimationHash = PedestrianGPUAnimationsConstans.SittingIdle_Anim_Hash; //int animation hash
		commandBuffer.SetComponentEnabled<UpdateSkinTag>(entity, true);
	}).Schedule();
	

.. _pedestrianGPUFactoryTransitionExample:

**Complex animation transition code example:**

..  code-block:: r
	
	public partial class PedestrianSittingGPUAnimatorExampleSystem : SystemBase
	{
		private const int StartSitAnimHash = -1880722739; //StartSit hash trigger

		private BeginPresentationEntityCommandBufferSystem entityCommandBufferSystem;
		private CrowdTransitionProviderSystem crowdTransitionProviderSystem;

		protected override void OnCreate()
		{
			base.OnCreate();
			entityCommandBufferSystem = World.GetOrCreateSystemManaged<BeginPresentationEntityCommandBufferSystem>();
			crowdTransitionProviderSystem = World.DefaultGameObjectInjectionWorld.GetOrCreateSystemManaged<CrowdTransitionProviderSystem>();
		}

		protected override void OnUpdate()
		{
			var transitions = crowdTransitionProviderSystem.Transitions;

			if (!transitions.IsCreated)
			{
				return;
			}

			var commandBuffer = entityCommandBufferSystem.CreateCommandBuffer();

			Entities
			.WithoutBurst()
			.WithReadOnly(transitions)
			.WithAll<HasSkinTag, GPUSkinTag>()
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
	* LoadGPUSkinSystem
	* CrowdAnimatorTransitionSystem
	* GPUSittingAnimatorSystem

.. _pedestrianRagdoll:

Ragdoll
~~~~~~~~~~~~

Ragdoll is created at the scene of the pedestrian's death. Make sure ragdoll is :ref:`enabled <pedestrianSettingsConfig>`.

How To Create
""""""""""""""

#. Add all colliders and rigidbodies according to the tutorial `RagdollWizard <https://docs.unity3d.com/2021.1/Documentation/Manual/wizard-RagdollWizard.html>`_ to character.

	.. image:: /images/pedestrian/RagdollAssignExample.png	
	`RagdollWizard example.`
		
#. Add `PedestrianRagdoll` component.

	.. image:: /images/pedestrian/RagdollComponent.png	
	
#. For remain characters, open `RagdollCloner` tool.

	.. image:: /images/pedestrian/RagdollClonerPath.png	
	.. image:: /images/pedestrian/RagdollCloner1.png	
	
#. Assign source character first created and target characters remain characters.

	.. image:: /images/pedestrian/RagdollCloner2.png	

#. Click `Create` button.
#. Assign the result to :ref:`PedestrianHybridLegacyFactory <pedestrianHybridLegacy>` or :ref:`PedestrianCrowdSkinFactory <pedestrianCrowdSkinFactory>` according to the chosen :ref:`type of rig <pedestrianSettingsConfig>`.

	.. note:: 
		* Implemented by `PedestrianRagdollSystem`.
		* Currently collides only with default `colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_

.. _pedestrianNavigation:

Navigation
----------------

| Navigation is used for pedestrian obstacle avoidance.
| There are 2 types of navigation:

.. _pedestrianNavmeshNavigation:

NavMesh Navigating
~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ .

Useful links:
	* :ref:`NavAgent Config <pedestrianNavAgentConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.
	
Installation
""""""""""""""

* Check that the :ref:`navigation package <packageInstallationOptional>` is installed.
* Make sure that navigation is enabled in the :ref:`general config <generalSettingsConfig>`.
* Make sure :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Each dynamic object on the scene must have a `NavMeshObstacle <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshObstacle.html>`_ component.

How To Setup
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

How To Setup
""""""""""""""

* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` mode.
* Set :ref:`Obstacle avoidance type <pedestrianObstacleAvoidanceType>` to `Local avoidance`.
* Configure :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`.

Pros And Cons
""""""""""""""

Pros:
	* Low CPU load.
	
Cons:
	* Can avoid vehicles only.
	* Works on flat surfaces only.

Common Info
----------------

Collision
~~~~~~~~~~~~

In some cases pedestrians can get stuck in obstacles (vehicles), to solve this problem, adjust :ref:`Antistuck config <pedestrianAntistuckConfig>`.

Authoring Components
----------------

Authoring components that make up the pedestrian entity.

PedestrianAuthoring
~~~~~~~~~~~~

Contains the main components of pedestrian entity **[required]**.

PlayerTargetAuthoring
~~~~~~~~~~~~

Component for player targeting systems **[optional]**.

Physics
~~~~~~~~~~~~

`PhysicsBody` and `PhysicsShape` components for physics related systems **[optional]**.

.. _pedestrianStates:

States
----------------

.. _pedestrianMovementState:

Movement State
""""""""""""""""""

* **Default**
* **Idle**
* **Walking**
* **Running**

.. _pedestrianActionState:

Pedestrian Action State
^^^^^^^^^^^^^^^^^^^^^^

* **Default** : no state.
* **Idle** : when a pedestrian is waiting.
* **MovingToNextTargetPoint** : when going from :ref:`PedestrianNode <pedestrianNode>` to :ref:`PedestrianNode <pedestrianNode>` (excluding crosswalk).
* **WaitForGreenLight** : when a pedestrian is waiting for a green traffic light.
* **CrossingTheRoad** : when a pedestrian goes crossing a crosswalk.
* **ScaryRunning** : activated when a pedestrian runs away in a panic (for example, the sound of a gunshot or the death of a pedestrian nearby).
* **Sitting** : when a pedestrian sits.
* **Talking** : when a pedestrian talks.	

	.. note:: 
		You can edit state logic :ref:`here <pedestrianStateAuthoring>`.

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

Pedestrian Skin Type
^^^^^^^^^^^^^^^^^^^^^^

* **Rig show only in view** : rig skin will be loaded in the camera's view area.
* **Rig and dummy** : rig will be in the camera's view, and the dummy skin will be out of the camera's view.
* **Dummy show only in view** : dummy skin will be loaded in the camera's view area.
* **Rig show always** : rig skin will be loaded when the entity is created and will exist until it is destroyed.
* **Dummy show always** : dummy skin will be loaded when the entity is created and will exist until it is destroyed..
* **No skin** : entities without a skin will be created.
	
Pedestrian Rig Type
^^^^^^^^^^^^^^^^^^^^^^

* **Hybrid legacy** : :ref:`hybrid entity with animator component <pedestrianHybridLegacy>`.
* **Pure GPU** : :ref:`pure entity with gpu animations <pedestrianGPU>`.

.. _pedestrianEntityType:

Pedestrian Entity Type
^^^^^^^^^^^^^^^^^^^^^^

* **No physics** : pedestrian not contains `PhysicsShape` component.
* **Physics** : pedestrian contains `PhysicsShape` component.
	
Common Settings
^^^^^^^^^^^^^^^^^^^^^^

| **Pedestrian collider radius** : pedestrian collider radius for `No physics` type.
| **Walking speed** : walking speed.
| **Running speed** : running speed.
| **Rotation speed** : rotation speed.
| **Health** : number of hit points for pedestrians.
| **Talking pedestrian spawn chance** : chance of spawning talking pedestrians
| **Min/Max talk time** : min/max talk time.

.. _pedestrianNavigationType:

Pedestrian Navigation Type **[NavMesh navigation only]**
^^^^^^^^^^^^^^^^^^^^^^

* **Temp** : navigation will be enabled if there is an obstacle in front of pedestrian.
* **Persist** : navigation is always on (for :ref:`NavMesh <pedestrianNavmeshNavigation>` calculation only).
* **Disabled**
	
.. _pedestrianObstacleAvoidanceType:
	
Obstacle Avoidance Type
^^^^^^^^^^^^^^^^^^^^^^

* **Calc nav path** : navigating based on :ref:`NavMesh <pedestrianNavmeshNavigation>` (:ref:`config <pedestrianNavAgentConfig>`).
* **Local avoidance** : simple :ref:`obstacle avoidance <pedestrianLocalAvoidance>` navigation (:ref:`config <pedestrianLocalAvoidanceConfig>`).
	
Collision type
^^^^^^^^^^^^^^^^^^^^^^

* **Calculate** :  collision is calculated manually (:ref:`for NoPhysics type<pedestrianEntityType>`).
* **Physics** : collision is calculated with `Unity.Physics` (:ref:`for Physics type<pedestrianEntityType>`).
* **Disabled**
	
| **Has ragdoll** : on/off :ref:`ragdoll<pedestrianRagdoll>` for pedestrian.

.. _pedestrianNavAgentConfig:

Pedestrian NavAgent Config
~~~~~~~~~~~~

Config for :ref:`NavMesh <pedestrianNavmeshNavigation>` navigating.

	.. image:: /images/configs/pedestrian/NavAgentConfig.png

| **Update frequency** : how often the nav target can be updated.
| **Max distance to target node** : distance to nav path node.
| **Max collision time** : if the pedestrian is stuck for more than the collision time, the anti-stuck will be activated.

**Revert target support** : if steering target is much further than final target with a given value the target will be reverted.
	* **Revert steering target distance** : distance to steering target logic for target return.
	* **Revert end target remaining distance** : distance to final target logic for target return.

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
| **Check target availability** : check if destination can be reached, if not and can't be found new, destination returns.

.. _pedestrianAntistuckConfig:

Pedestrian Antistuck Config
~~~~~~~~~~~~

Anti-stuck config for pedestrians stucked in a collision.

	.. image:: /images/configs/pedestrian/PedestrianAntistuckConfig.png
	
| **Antistuck enabled** : on/off anti-stuck feature (if disabled previous target will be selected).
| **Target direction dot** : direction between the pedestrian's forward and the anti-stuck point.
| **Achieve distance** : achieve distance to the antistuck target point.
| **Target point offset** : distance between collision and anti-stuck point.
	
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
	
Trigger settings
^^^^^^^^^^^^^^^^^^^^^^

| **Death trigger squared distance** : death trigger squared distance (squared distance == distance * distance).
| **Death trigger duration** : death trigger duration.
		
Sound settings
^^^^^^^^^^^^^^^^^^^^^^

| **Has scream sound** : on/off scream sound.
| **Scream entity limit** : maximum number of screaming pedestrians at the same time.
| **Chance to scream** : chance of a pedestrian screaming.
| **Scream delay** : delay between screams.
| **Scream sound data** : scream :ref:`sound data<soundData>` source.
		
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


.. _pedestrianStateAuthoring:

Pedestrian State Authoring
~~~~~~~~~~~~
	
State Dictionary
^^^^^^^^^^^^^^^^^^^^^^

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring1.png

| **Next states** : which states can override the current state.

**State type:** 
	* Default : the state proccessed by `PedestrianStateSystem` system (code processing for state should be there).
	* External system : the state proccessed by external system (code processing for state should be in the separate system).
	* Additive : additive state flag adds to the current state and is processed by the `External system`.


Movement State Binding Dictionary
^^^^^^^^^^^^^^^^^^^^^^

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring2.png

Contains data - which :ref:`Movement state <pedestrianMovementState>` is assigned after the :ref:`Action state <pedestrianActionState>` is assigned.
	
	.. note:: 
		You can read about available states :ref:`here <pedestrianStates>`.