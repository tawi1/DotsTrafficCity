.. _pedestrian:

Pedestrian
=====

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

		.. image:: images/configs/pedestrian/PedestrianSkinFactory.png
	
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
	.. highlight:: C#
	   :linenothreshold: 8
	   
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
	
		.. image:: images/pedestrian/baker/AnimationCollectionExample.png
	
	#. Add and customize desired animations data.
	#. Open on the scene `PedestrianBakedSkinFactory`.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianBakedSkinFactory``

	#. Assign :ref:`Animation Collection <animationBakerAnimationCollection>` to `PedestrianBakedSkinFactory`.
	
		.. image:: images/pedestrian/baker/AddNewEntryPanelExample.png
			
	#. Click `+` to show `New Entry` panel.
	
		.. image:: images/pedestrian/baker/NewEntry.png
	
	#. Enter pedestrian entry name & assign `Skinned Mesh Renderer` or `Mesh` of the target pedestrian.
	#. Click `Add Entry`.	
	
	#. Select created :ref:`Baked Animation Sheet Data <animationBakerAnimationSheetData>`.
	
		.. image:: images/pedestrian/baker/PedestrianAnimationSheetDataExample.png
		
	#. Select the animation in the inspector that you want to assign to the selected character.
	
		.. image:: images/pedestrian/baker/PedestrianAnimationsAssignExample.png
			
	#. Press the `Assign` button according to the selected animation in :ref:`Baked Animation Sheet Data <animationBakerAnimationSheetData>`.
	#. Assign values for each animation in the same way.
	
Baked Custom Animator
""""""""""""""

Baked Custom animator is used for transitions between baked animations (implemented by `PedestrianBakedTransitionAnimatorSystem` system).

**How To Create transition:**
	#. Open on the scene `PedestrianBakedAnimatorAuthoring`.
	
		``Hub/Configs/BakerRefs/Settings/PedestrianBakedAnimatorAuthoring``
		
		.. image:: images/pedestrian/baker/PedestrianBakedAnimatorAuthoring.png

				
	#. Create :ref:`Animator Container <animationBakerAnimatorContainer>` in the project context menu and assign to animator (if necessary).
	#. Assign :ref:`Animation Collection <animationBakerAnimationCollection>` the same as in the :ref:`PedestrianBakedFactory<pedestrianBakedFactory>`.
	#. Press `Open Animator` button.
	#. Enter the name of the trigger in the start node.
	#. Create and connect :ref:`AnimationNode <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
		.. image:: images/pedestrian/baker/StartSitTransitionExample.png
		`Start sit transition example.`
		
		.. image:: images/pedestrian/baker/SitoutTransitionExample.png		

		`Sitout transition example.`
	
	#. Copy & paste acquired hash from `AnimatorContainer` to code (:ref:`usage example <pedestrianBakedFactoryTransitionExample>`).
		
		.. image:: images/pedestrian/baker/AnimatorContainerExample.png		

How To Use
""""""""""""""

**Simple switch animation example:**
	
	.. highlight:: C#
	
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

**Complex animation transition example:**

	.. highlight:: C#
	
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
	* Assign the result to :ref:`PedestrianHybridLegacyFactory <pedestrianHybridLegacy>` :ref:`PedestrianBakedFactory <pedestrianBaked>` according to the chosen :ref:`type of rig <pedestrianSettingsConfig>`.
	
	.. note:: Implemented by `PedestrianRagdollSystem`.

Authoring components
----------------

**Components:**
	* `PedestrianAuthoring` [required].
	* `PlayerTargetAuthoring` [optional for player targeting systems].
	* `PhysicsBody` and `PhysicsShape` [optional for physics related systems].

States
----------------

**Movement States:**

.. _pedestrianActionState:

**Pedestrian Action States:**


Configs
----------------