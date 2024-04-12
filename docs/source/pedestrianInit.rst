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

A `Hybrid legacy skin` is a :ref:`hybrid entity <hybridEntity>` that combines the default `GameObject` (with `animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_) and the DOTS entity.

Factory
""""""""""""""

	#. Open `PedestrianSkinFactory` in the scene.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianSkinFactory``

		.. image:: /images/configs/pedestrian/PedestrianSkinFactory.png
	
	#. Enable the `Show Add New Prefab Settings`.
	#. Drag & drop source prefabs into the `New Prefabs` field.
	#. Customize the prefab names.
	#. Click the `Try To Add Prefabs`.
	#. If necessary, configure :ref:`Ragdoll <pedestrianRagdoll>` and assign to the `Pedestrian Skin Factory Data` (make sure :ref:`Ragdoll <pedestrianRagdoll>` is :ref:`enabled <pedestrianSettingsConfig>`).

	.. note:: 
		Each `Hybrid legacy` pedestrian prefab should have `PedestrianReferences` component.
		
Animations
""""""""""""""

By default, each pedestrian has a `PedestrianBaseController` animator.

**Animation List:**

+------------------------+--------------+-----------+--------------+
| Animation name         |  Parameters  |   Value   |   When it    |
|                        |              |           |   starts     |
+========================+==============+===========+==============+
| Walking                |- yInput      |   - 0.3   | By default   |
|                        |- SideMovement|   - 0     |              |
+------------------------+--------------+-----------+--------------+
| Running                |- yInput      |   - 1     | By default   |
|                        |- SideMovement|   - 0     |              |
+------------------------+--------------+-----------+--------------+
| Idle                   |- yInput      |   - 0     | By default   |
|                        |- SideMovement|   - 0     |              |
+------------------------+--------------+-----------+--------------+
| Stand To Sit           |- IsSitting   |   - true  | By default   |
|                        |              |           |              |
+------------------------+--------------+-----------+--------------+
| Sitting Idle           |              |           | Starts when  |
|                        |              |           |*Stand To Sit*|            
|                        |              |           |is completed  |
+------------------------+--------------+-----------+--------------+
| Sit To Stand           |- IsSitting   |   - false | Starts after |
|                        |              |           |*Sitting Idle*|
+------------------------+--------------+-----------+--------------+
| Talking 1, 2, 3        |- Talking     |   - 0,1,2 | By default   |
|                        |              |           |              |
+------------------------+--------------+-----------+--------------+

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

.. _crowdSkinFactory:

How To Create
""""""""""""""

	#. :ref:`Create textures and animation sheets <animationBaker>`.
	#. Create :ref:`Animation Collection <animationGPUAnimationCollection>` from the project context .
	
		``Spirit604/Animation Baker/Animation Collection``
	
		.. image:: /images/pedestrian/baker/animator/AnimationCollectionExample.png
	
	#. Add and customize desired animations data.
	#. Open in the scene `PedestrianCrowdSkinFactory`.
	
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
		
	#. Assign `Default Atlas Texture` (if selected pedestrians have the same texture material). **[optional step]**

		.. image:: /images/pedestrian/baker/SettingsExample3.png
			
	#. One by one click `Select` and `Add entry` button. Or click the `Add all entries` button to add all entries in the container.	
	
		.. image:: /images/pedestrian/baker/NewEntry2.png
			
	#. Turn on the `Find Related Animations` button.
	
		.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample2.png
			
	#. Generate Animation Material.
		#. Assign main texture of selected model **[if missing]**.
		#. Press the `Generate` button.
	
			.. image:: /images/pedestrian/baker/GenerateMaterialExample.png
		
	#. Select entry & assign animations:	
	
		#. **Animation baker binding:**
			#. :ref:`Bind <animationBakerBind>` the animation on the baking texture step.
		
		#. **Manual way:**
			#. In the inspector, select the animation that you want to assign to the selected character.
		
				.. image:: /images/pedestrian/baker/PedestrianAnimationsAssignExample.png
				
			#. Press the `Assign` button according to the selected animation in :ref:`Animation Texture Data <animationTextureData>`.
		
		#. **Automated way:**
			#. Automatic assignment works if the animation in the list matches (or partially matches) the animation name in the selected container.
			#. Press the `Auto Bind Animations` button.
			#. Make sure, that all animations are assigned.
			
				.. image:: /images/pedestrian/baker/PedestrianAnimationsAssignExample2.png

		.. note:: In the current version of the project, all pedestrians should have all the animations from the :ref:`Animation Collection <animationGPUAnimationCollection>` (will be changed in the near future).
		
	#. Assign animations to each entry in the same way.
	
	#. Add custom optional animations for the desired pedestrians [optional step].
		#. In the :ref:`Animation Collection <animationGPUAnimationCollection>` add new `Optional` animations.
		#. Tick on `Show optional animation popup` in Pedestrian crowd skin factory settings.
		#. Add desired optional animations in the character list of the factory.
		#. Bind added animations.		

	#. Assign :ref:`Ragdolls <pedestrianRagdoll>`. **[optional step]**.
	
		.. image:: /images/pedestrian/baker/PedestrianGPURagdolleExample.png
	
How To Use
""""""""""""""

| **Code example:**

..  code-block:: r
	
        private NativeHashMap<SkinAnimationHash, HashToIndexData> hashToLocalDataLocalRef;

        void ISystemStartStop.OnStartRunning(ref SystemState state)
        {
            hashToLocalDataLocalRef = CrowdSkinProviderSystem.HashToLocalDataStaticRef;
        }

        [BurstCompile]
        void ISystem.OnUpdate(ref SystemState state)
        {
            var switchAnimJob = new SwitchAnimJob()
            {
                HashToLocalData = hashToLocalDataLocalRef,
            };

            switchAnimJob.Schedule();
        }

        [BurstCompile]
        public partial struct SwitchAnimJob : IJobEntity
        {
            [ReadOnly]
            public NativeHashMap<SkinAnimationHash, HashToIndexData> HashToLocalData;

            void Execute(
                Entity entity,
                ref SkinUpdateComponent skinUpdateComponent,
                EnabledRefRW<UpdateSkinTag> updateSkinTagRW)
            {
				// Some animation hash calculated from animation name & AnimUtils.StringToHash method
                var animHash = 54335363; 

				AnimEntitiesUtils.UpdateAnimation(ref skinUpdateComponent, ref updateSkinTagRW, animHash);
            }
        }
    }
		
**Used in systems:**
	* GPUAnimatorSystem
	* GPUAnimatorCustomSitStateSystem
	* GPUTalkAnimatorSystem
	
.. _animationTextureData:

Animation Texture Data
""""""""""""""

Data about baked animations in texture (:ref:`How to create <animationBakerHowTo>`). 
	
	.. image:: /images/pedestrian/baker/PedestrianAnimationSheetDataExample3.png	
	
Crowd GPU Custom Animator
""""""""""""""

The Crowd GPU Custom animator is used for transitions between baked animations (implemented by `CrowdAnimatorTransitionSystem` system).

.. _animationBakerHowToCreateTransition:

**How To Create Transition:**
	#. Open in the scene `CrowdGPUAnimatorAuthoring`.
	
		``Hub/Configs/BakerRefs/Settings/CrowdGPUAnimatorAuthoring``
		
		.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png

				
	#. Create an :ref:`Animator Data Container <animationGPUAnimatorContainer>` from the project context  and assign it to the animator (if required).
	#. Assign :ref:`Animation Collection <animationGPUAnimationCollection>` the same as in the :ref:`PedestrianCrowdSkinFactory <crowdSkinFactory>`.
	#. Press the `Open Animator` button.
	#. Create a :ref:`new transition layer <animationBakerAnimatorNewTransitionLayer>` (if needed).
	#. Enter the name of the trigger in the :ref:`StartNode <animationBakerAnimatorStartNode>`.
	#. Create and connect :ref:`AnimationNode <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
		.. image:: /images/pedestrian/baker/animator/StartSitTransitionExample.png
		`Start sit transition example.`
		
		.. image:: /images/pedestrian/baker/animator/SitoutTransitionExample.png		

		`Sitout transition example.`
	
	#. Copy & paste the :ref:`generated hash <animationBakerAnimatorTriggerHash>` from the `AnimatorContainer` into the code (:ref:`usage example <pedestrianGPUFactoryTransitionExample>`).
		
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

#. Add all the colliders and rigidbodies to character according to the `RagdollWizard <https://docs.unity3d.com/2021.1/Documentation/Manual/wizard-RagdollWizard.html>`_ tutorial.

	.. image:: /images/pedestrian/RagdollAssignExample.png	
	`RagdollWizard example.`
		
#. Add the `PedestrianRagdoll` component.

	.. image:: /images/pedestrian/RagdollComponent.png	
	
#. For the remaining characters, open the `RagdollCloner` tool.

	.. image:: /images/pedestrian/RagdollClonerPath.png	
	.. image:: /images/pedestrian/RagdollCloner1.png	
	
#. Assign the source character created first and the target remaining characters.

	.. image:: /images/pedestrian/RagdollCloner2.png	

#. Click the `Create` button.
#. Assign the result to :ref:`PedestrianHybridLegacyFactory <pedestrianHybridLegacy>` or :ref:`PedestrianCrowdSkinFactory <crowdSkinFactory>` depending on the :ref:`type of rig <pedestrianSettingsConfig>` you have chosen.

	.. note:: 
		* Implemented by `RagdollSystem`.
		* Currently only collides with default `colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_
		* Make sure, that the scene contains `default colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_.
		* Read more info about the :ref:`Physics Transfer Service <physicsShapeTransfer>` on how to clone legacy colliders.

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
* Make sure that navigation is enabled in the :ref:`General Config <generalSettingsConfig>`.
* Ensure that :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Each dynamic object in the scene must have a `NavMeshObstacle <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshObstacle.html>`_ component.

How To Setup
""""""""""""""

* Create & customize `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_.
* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` or `Persist` mode.
* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Calc Nav Path`.
		
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

DOTS system to avoid local obstacles (vehicles).

Useful links:
	* :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.

How To Setup
""""""""""""""

* Set the :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` mode.
* Set the :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Local Avoidance`.
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

In some cases pedestrians can get stuck in obstacles (vehicles), to solve this problem, adjust the :ref:`Antistuck config <pedestrianAntistuckConfig>`.

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

How To Change
~~~~~~~~~~~~

..  code-block:: r

	//Switch state example
	
    [WithAll(typeof(CheckTrafficLightStateTag))]
    [BurstCompile]
    public partial struct CheckTrafficLightJob : IJobEntity
    {
        public EntityCommandBuffer.ParallelWriter CommandBuffer;

        void Execute(
            Entity entity,
            [ChunkIndexInQuery] int entityInQueryIndex,
            ref DestinationComponent destinationComponent,
            ref NextStateComponent nextStateComponent)
		{
			//Example red traffic light flag logic
			bool redLight = true;
			
			if (redLight)
			{
				if (nextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight, ref destinationComponent))
				{
					 CommandBuffer.SetComponentEnabled<WaitForGreenLightTag>(entityInQueryIndex, entity, true);
					 //Logic
				}
			}
		}
	}

.. _pedestrianMovementState:

Movement State
~~~~~~~~~~~~

* Default
* Idle
* Walking
* Running

.. _pedestrianActionState:

Action State
~~~~~~~~~~~~

* **Default** : no state.
* **Idle** : when a pedestrian is waiting.
* **MovingToNextTargetPoint** : when going from :ref:`PedestrianNode <pedestrianNode>` to :ref:`PedestrianNode <pedestrianNode>` (excluding crosswalk).
* **WaitForGreenLight** : when a pedestrian is waiting for a green traffic light.
* **CrossingTheRoad** : when a pedestrian goes crossing a crosswalk.
* **ScaryRunning** : activated when a pedestrian runs away in a panic (for example, the sound of a gunshot or the death of a pedestrian nearby).
* **Sitting** : when a pedestrian is sitting.
* **Talking** : when a pedestrian is talking.	

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

Skin Type
""""""""""""""""""

* **Rig show only in view** : rig skin will be loaded in the camera's view area.
* **Rig and dummy** : rig will be in the camera's view, and the dummy skin will be out of the camera's view.
* **Dummy show only in view** : dummy skin will be loaded in the camera's view area.
* **Rig show always** : rig skin will be loaded when the entity is created and will exist until it is destroyed.
* **Dummy show always** : dummy skin will be loaded when the entity is created and will exist until it is destroyed..
* **No skin** : entities without a skin will be created.
	
Rig Type
""""""""""""""""""

* **Hybrid legacy** : :ref:`hybrid entity with animator component <pedestrianHybridLegacy>`.
* **Pure GPU** : :ref:`pure entity with gpu animations <pedestrianGPU>`.

.. _pedestrianEntityType:

Entity Type
""""""""""""""""""

* **No physics** : pedestrian not contains `PhysicsShape` component.
* **Physics** : pedestrian contains `PhysicsShape` component.
	
Common Settings
""""""""""""""""""

| **Pedestrian collider radius** : pedestrian collider radius for `No physics` type.
| **Walking speed** : walking speed.
| **Running speed** : running speed.
| **Rotation speed** : rotation speed.
| **Health** : number of hit points for pedestrians.
| **Talking pedestrian spawn chance** : chance of spawning talking pedestrians
| **Min/Max talk time** : min/max talk time.

.. _pedestrianObstacleAvoidanceType:
	
Obstacle Avoidance Type
""""""""""""""""""

| **Calc nav path** : navigating based on :ref:`NavMesh <pedestrianNavmeshNavigation>` (:ref:`config <pedestrianNavAgentConfig>`).
| **Local avoidance** : simple :ref:`obstacle avoidance <pedestrianLocalAvoidance>` navigation (:ref:`config <pedestrianLocalAvoidanceConfig>`).
	
.. _pedestrianNavigationType:

Pedestrian Navigation Type **[** :ref:`NavMesh <pedestrianNavmeshNavigation>` **navigation only]**
""""""""""""""""""

* **Temp** : navigation will be enabled if there is an obstacle in front of pedestrian.
* **Persist** : navigation is always on.
* **Disabled**	
	
Collision type
""""""""""""""""""

* **Calculate** :  collision is calculated manually (:ref:`for NoPhysics type<pedestrianEntityType>`).
* **Physics** : collision is calculated with `Unity.Physics` (:ref:`for Physics type<pedestrianEntityType>`).
* **Disabled**
	
| **Has ragdoll** : on/off :ref:`ragdoll<pedestrianRagdoll>` for pedestrian.

.. _pedestrianNavAgentConfig:

NavAgent Config
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

Obstacle Local Avoidance Config
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

Antistuck Config
~~~~~~~~~~~~

Anti-stuck config for pedestrians stucked in a collision.

	.. image:: /images/configs/pedestrian/PedestrianAntistuckConfig.png
	
| **Antistuck enabled** : on/off anti-stuck feature (if disabled previous target will be selected).
| **Target direction dot** : direction between the pedestrian's forward and the anti-stuck point.
| **Achieve distance** : achieve distance to the antistuck target point.
| **Target point offset** : distance between collision and anti-stuck point.
	
Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianTriggerConfig.png
	
| **Trigger HashMap capacity** : initial hashmap capacity  that contains data of triggers.
| **Trigger HashMap cell size** : hashmap cell size.
**Trigger data:**
	* **Fear Point Trigger** :
		* **Impact trigger duration** : duration of the :ref:`trigger<pedestrianScaryTrigger>` on the pedestrian.

.. _pedestrianScaryTrigger:

Scary Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianScaryTriggerConfig.png
	
Trigger settings
""""""""""""""""""

| **Death trigger squared distance** : death trigger squared distance (squared distance == distance * distance).
| **Death trigger duration** : death trigger duration.
		
Sound settings
""""""""""""""""""

| **Has scream sound** : on/off scream sound.
| **Scream entity limit** : maximum number of screaming pedestrians at the same time.
| **Chance to scream** : chance of a pedestrian screaming.
| **Scream delay** : delay between screams.
| **Scream sound data** : scream :ref:`sound data<soundData>` source.
		
Bench Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianBenchConfig.png
	
| **Min/Max idle time** : min/max idle duration on the bench.
| **Custom achieve enter point distance** : distance to achieve the entry point on the bench.
| **Idle after achieved exit duration** : idle after achieved exit point duration.
| **Sitting movement speed** : pedestrian movement speed when sitting on the bench.
| **Sitting rotation speed** : pedestrian turn speed when sitting on the bench.
| **Custom achieve sit point distance** :  distance to achieve the sit point on the bench.
	
Common Sound Config
~~~~~~~~~~~~

Common pedestrian sound settings

	.. image:: /images/configs/pedestrian/PedestrianCommonSoundConfig.png
	
| **Sound death** : :ref:`sound<soundData>` when a pedestrian died.
| **Enter tram sound** : :ref:`sound<soundData>` when entering a tram.
| **Exit tram sound** : :ref:`sound<soundData>` when exiting a tram.


.. _pedestrianStateAuthoring:

State Authoring
~~~~~~~~~~~~
	
State Dictionary
""""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring1.png

| **Next states** : which :ref:`states <pedestrianActionState>` can override the current :ref:`state <pedestrianActionState>`.

**State type:** 
	* **Default** : the state proccessed by `PedestrianStateSystem` system (code processing for state should be there).
	* **External system** : the state proccessed by external system (code processing for state should be in the separate system).
	* **Additive** : additive state flag adds to the current state and is processed by the `External system`.
	* **Additive any** : additive state flag adds to the current state and is processed by the `External system` & ignores available next state flags.


Movement State Binding Dictionary
""""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring2.png

Contains data - which :ref:`Movement state <pedestrianMovementState>` is assigned after the :ref:`Action state <pedestrianActionState>` is assigned.
	
	.. note:: 
		You can read about available states :ref:`here <pedestrianStates>`.