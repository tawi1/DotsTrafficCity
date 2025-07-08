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
		Each `Hybrid legacy` pedestrian prefab should have `PedestrianEntityRef` component.
		
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

**Used in systems:**
	* LegacyAnimatorSystem
	* LegacyAnimatorCustomStateSystem
	
.. _legacyAnimatorExample:

Animation authoring
""""""""""""""

* Add your animation to `AnimationState` script file.
* In the scene find:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateAuthoring.png
	`Hub/Configs/PedestrianConfigs/PedestrianAnimationStateAuthoring`.

* Add your animation to the list & enter condition to start the animation from the assigned `Animator`:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateLegacyExample.png
	
	* **State name** : state name of the animation in the `Animator`.
	* **State layer** : number of the layer where the animation is stored in the `Animator`.
	* **Param 1** : first parameter to start animation in the `Animator`.
	* **Param 2** : second parameter to start animation in the `Animator` *[optional]*.
	* **Exit param** : parameter to exit current animation in the `Animator` *[optional]*.
	
* How to play animation described :ref:`here <pedestrianAnimation>`.

.. _pedestrianGPU:

Pure GPU Skin
~~~~~~~~~~~~

`Pure GPU skin` is a :ref:`pure entity <pureEntity>` that combines the GPU texture animations and the DOTS entity.

.. _crowdSkinFactory:

How To Create
""""""""""""""

	#. :ref:`Create textures and animation sheets <animationBakerHowTo>` in the :ref:`Animation baker <animationBaker>` tool.
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

	#. Assign animations to each entry in the same way.
	
	#. Add custom optional animations for the desired pedestrians [optional step].
		#. In the :ref:`Animation Collection <animationGPUAnimationCollection>` add new `Optional` animations.
		#. Tick on `Show optional animation popup` in Pedestrian crowd skin factory settings.
		#. Add desired optional animations in the character list of the factory.
		#. Bind added animations.		

	#. Assign :ref:`Ragdolls <pedestrianRagdoll>` **[optional step]**.
	
		.. image:: /images/pedestrian/baker/PedestrianGPURagdolleExample.png
	
	**Used in systems:**
		* GPUAnimatorSystem
		* GPUAnimatorCustomStateSystem
	
.. _gpuAnimatorExample:

Animation authoring
""""""""""""""

* Add your animation to `AnimationState` script file.
* In the scene find:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateAuthoring.png

	`Hub/Configs/PedestrianConfigs/PedestrianAnimationStateAuthoring`.
	
* Add binding in the list (`AnimationState` is a key, `Animation` from :ref:`Animation collection <animationGPUAnimationCollection>` is a value)

	.. image:: /images/pedestrian/animation/PedestrianAnimationGpuExample.png
	`Example.`
	
* How to play animation described :ref:`here <pedestrianAnimation>`.
			
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

**Used in systems:**
	* GPUAnimatorCustomStateSystem

.. _hybridAndGpu:

Hybrid and GPU
~~~~~~~~~~~~

New hybrid GPU mode that allows you to mix hybrid animator models for near and GPU animation for far at the same time.

How To Create
""""""""""""""

* Create :ref:`Legacy <pedestrianHybridLegacy>` pedestrians.
* Add desired animations in the :ref:`Animation state authoring <legacyAnimatorExample>` for :ref:`Legacy <pedestrianHybridLegacy>` pedestrians.
* Create :ref:`GPU <pedestrianGPU>` pedestrians.
* Add desired animations in the :ref:`Animation state authoring <gpuAnimatorExample>` for :ref:`GPU <pedestrianGPU>` pedestrians.
* Make sure that the number & the order of :ref:`Legacy <pedestrianHybridLegacy>` & :ref:`GPU <pedestrianGPU>` of the models are the same in the factories (`PedestrianSkinFactory` & `PedestrianGPUSkinFactory`).
* How to play animation described :ref:`here <pedestrianAnimation>`.

Cull state
""""""""""""""

* :ref:`InViewOfCamera <cullPointStates>`: :ref:`Hybrid <pedestrianHybridLegacy>` legacy skin is enabled.
* :ref:`CloseToCamera <cullPointStates>`: :ref:`GPU <pedestrianGPU>` skin is enabled.

Hybrid On Request And GPU
~~~~~~~~~~~~

By default, the entity is animated by the `GPU` until a `Hybrid skin` is requested.

How To Create
""""""""""""""

* Create entity as :ref:`Hybrid and GPU <hybridAndGpu>` pedestrians.
* Hybrid skin is enabled if the entity disables the `PreventHybridSkinTagTag` tag, to switch back to `GPU`, enable `PreventHybridSkinTagTag` tag again.

Hybrid Shape GPU
~~~~~~~~~~~~

`Hybrid Shape GPU skin` is a :ref:`hybrid entity <hybridEntity>` animated on `GPU` in `DOTS` & has hybrid monobehaviour collider to interact with pedestrians in a familiar way.

How To Create
""""""""""""""

* Create :ref:`GPU <pedestrianGPU>` pedestrians.
* The hybrid shape can be edited here:
	
	.. image:: /images/pedestrian/HybridShapeFactory.png	

.. _rukhankaSkin:

Rukhanka
~~~~~~~~~~~~

Pure entities animated with `Rukhanka Animation System <https://assetstore.unity.com/packages/tools/animation/rukhanka-ecs-animation-system-241472>`_ in `DOTS`.

How To Create
""""""""""""""

* Import `Rukhanka` samples (it uses `AnimatedLitShader URP` shader from the sample).

	.. image:: /images/integration/rukhanka0.png	
	
* Unpack `RukhankaSample` prefabs:

	.. image:: /images/integration/rukhanka1.png	
	
* Create a new gameobject on the scene & add an `AnimationCullingConfig` component & assign the main camera to it.
* Create a pedestrian prefab with the `Animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, add `PedestrianAuthoring` & `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ components & assign desired prefab here:

	.. image:: /images/integration/rukhanka2.png	
	
	.. image:: /images/integration/rukhanka3.png	
	
* Animation taken from :ref:`Animation state authoring <legacyAnimatorExample>` as for :ref:`Hybrid legacy <pedestrianHybridLegacy>` pedestrian.
* If you get a ``Blob asset System.String System.Type::get_FullName() with hash 'Unity.Entities.Hash128' is corrupted.`` error, try closing the subscene (uncheck the box next to `EntitySubscene`) & start the scene again.

.. _rukhankaHybridSkin:

Rukhanka Hybrid
~~~~~~~~~~~~

Hybrid entities animated with `Rukhanka Animation System <https://assetstore.unity.com/packages/tools/animation/rukhanka-ecs-animation-system-241472>`_ with hybrid monobehaviour collider & rigidbody to control or interact with pedestrians in a familiar way.

How To Create
""""""""""""""

* Import `Rukhanka` samples (it uses `AnimatedLitShader URP` shader from the sample).

	.. image:: /images/integration/rukhanka0.png	
	
* Unpack `RukhankaSample` prefabs:

	.. image:: /images/integration/rukhanka1.png	
	
* Create a new gameobject on the scene & add an `AnimationCullingConfig` component & assign the main camera to it.
* Create a pedestrian prefab with the `Animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, add `PedestrianAuthoring` & `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ components & assign desired prefab here:

	.. image:: /images/integration/rukhanka2.png	
	
	.. image:: /images/integration/rukhanka3.png	
	
* The hybrid shape can be edited here:
	
	.. image:: /images/pedestrian/HybridShapeFactory.png	
	
* Animation taken from :ref:`Animation state authoring <legacyAnimatorExample>` as for :ref:`Hybrid legacy <pedestrianHybridLegacy>` pedestrian.
* If you get a ``Blob asset System.String System.Type::get_FullName() with hash 'Unity.Entities.Hash128' is corrupted.`` error, try closing the subscene (uncheck the box next to `EntitySubscene`) & start the scene again.
	
How To Control
""""""""""""""

You can control the `Rukhanka Hybrid` npc with the monobehaviour script:

* Make sure that `HybridShapeFactory` prefab contains `RukhankaEntityAdapter`.
* :ref:`Temporarily remove <pedestrianDisableSimulation>` the entity from the built-in DOTS simulation.
* Methods to control animation in the same way as the `Unity animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, but using `RukhankaEntityAdapterBase` component.
* Example:

 	..  code-block:: r
	
		public struct AnimationControlExample : MonoBehaviour
		{		  
			private RukhankaEntityAdapterBase adapter;
			
			private void Awake()
			{
				adapter = GetComponent<RukhankaEntityAdapterBase>();			
			}
			
			private void SetTriggerByName(string name)
			{
				adapter.SetTrigger(name);
			}		
			
			private void SetTriggerByHash(string name)
			{
				var hash = RukhankaUtils.GetHash(name);
				adapter.SetTrigger(hash);
			}		
		}
		
How To Attach
""""""""""""""

If you need to attach some gameobject weapon e.g:

* Add `RukhankaHybridBoneAnchorAuthoring` to entity prefab.
* In `RukhankaHybridBoneAnchorAuthoring` assign bone that you want to attach.
* Attach the anchor with the local index:

 	..  code-block:: r
	
		public struct AttachExample : MonoBehaviour
		{		  
			[SerializeField] private GameObject attachment;
		
			private RukhankaEntityAdapterBase adapter;
			
			private void Awake()
			{
				adapter = GetComponent<RukhankaEntityAdapterBase>();			
			}
			
			private void Attach()
			{
				// Attach to anchor with local index 0
				adapter.AttachToBone(attachment, 0);
			}		
			
			private void Release()
			{
				adapter.ReleaseAttachment(0);
			}	
		}
		
Animation Event
""""""""""""""

* In `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ component enable `Has Animation Events` option.
* Then, use this sample code:

 	..  code-block:: r
	
		public struct AnimationEventExample : MonoBehaviour
		{		  
			[SerializeField] private string desiredAnimationEventName;
		
			private RukhankaEntityAdapterBase adapter;
			private uint desiredAnimationEventHash;
			
			private void Awake()
			{
				adapter = GetComponent<RukhankaEntityAdapterBase>();
				adapter.OnAnimationEvent += RukhankaEntityAdapter_OnAnimationEvent;
				
				desiredAnimationEventHash = RukhankaUtils.GetHash(desiredAnimationEventName);				
			}
			
			private void RukhankaEntityAdapter_OnAnimationEvent(AnimationEventComponent animationEvent)
			{
				if (animationEvent.nameHash == desiredAnimationEventHash)
				{
					// Take action
				}
			}
		}
		

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
| There are 3 types of navigation:

.. _pedestrianNavmeshNavigation:

NavMesh Navigating
~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ .

Useful links:
	* :ref:`NavAgent Config <pedestrianNavAgentConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.
	
Installation
""""""""""""""

* Check that the :ref:`Navigation package <packageInstallationOptional>` is installed.
* Make sure that navigation is enabled in the :ref:`General Config <generalSettingsConfig>`.
* Ensure that :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Each dynamic object in the scene must have a `NavMeshObstacle <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshObstacle.html>`_ component.

How To Setup
""""""""""""""

* Create a new gameobject & add `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ component.
* Set `Agent type` to `Humanoid` & press the `Bake` button in the created `NavMeshSurface`.
* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Calc Nav Path`.
* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` or `Persist` mode.

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

* Set the :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Local Avoidance`.
* Configure :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`.

Pros And Cons
""""""""""""""

Pros:
	* Low CPU load.
	
Cons:
	* Can avoid vehicles only.
	* Works on flat surfaces only.
	
.. _pedestrianAgentsNavigation:

Agents Navigation 
~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_  using `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin.

How To Setup
""""""""""""""

* Make sure that you purchased & downloaded `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin.
* Set the :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Agents Navigation`.
* Enable the `Auto Add Agent Components` option for quick prototyping & customize the settings in the `Agents Navigation Config Authoring` tab, or add agent authoring components to the `PedestrianEntity` prefab from the `Agents Navigation` sample for more flexible settings. (`Agents Navigation doc <https://lukaschod.github.io/agents-navigation-docs/manual/game-objects.html>`_)
* Ensure that :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Add `Agent Collider Hybrid Component` to the `HybridEntityRuntimeAuthoring` of your player NPC if you want to collide with pedestrians [**optional step**]

.. _pedestrianAnimation:

Animation
----------------

.. _customAnimatorState:

Custom Animation
~~~~~~~~~~~~

To handle custom animation, follow these steps:

* Add custom animations in the `Animation state authoring` for pedestrians.
	* :ref:`Hybrid skin <legacyAnimatorExample>` (if you are using Hybrid animations).
	* :ref:`GPU skin <gpuAnimatorExample>` (if you are using GPU animations).
	
* Add custom animator state by code:
	
..  code-block:: r
	
	// IJobEntity entity example
    void Execute(
        Entity entity,
        ref AnimationStateComponent animationStateComponent)
    {
		// Some condition
		bool condition = true;
		
		if (condition)
		{
			// Replace 'AnimationState.StandToSit' with your animation.
			AnimatorStateExtension.AddCustomAnimatorState(ref CommandBuffer, entity, ref animationStateComponent, AnimationState.StandToSit);
		}
    }
	
* Change to new state if required, code:

..  code-block:: r

	// IJobEntity entity example
    void Execute(
        Entity entity,
        ref AnimationStateComponent animationStateComponent)
    {
		// Some condition
		bool condition = true;
		
		if (condition)
		{
			// Replace 'AnimationState.SitToStand' with your animation.
			AnimatorStateExtension.ChangeAnimatorState(ref CommandBuffer, entity, ref animationStateComponent, AnimationState.SitToStand);
		}
    }
	
* After all the custom animations have been played, turn off the custom animation state.

..  code-block:: r

	// IJobEntity entity example
    void Execute(
        Entity entity,
        ref AnimationStateComponent animationStateComponent)
    {
		// Some condition
		bool condition = true;
		
		if (condition)
		{
			AnimatorStateExtension.RemoveCustomAnimator(ref CommandBuffer, entity);
		}
    }	

	.. note::
		For an example of a system, please read the script below:
			* BenchStateSystem.cs.			

.. _pedestrianStates:

States
----------------

Common Logic
~~~~~~~~~~~~

#. Custom system set the next :ref:`Action state <pedestrianActionState>` in the `NextStateComponent` by utils method.

	* bool NextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight, ref destinationComponent)
		`Example method, if state can't be set, then target swap back.`
		
	* bool NextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight)
		`Example method without retargeting.`
	
#. `PedestrianStateSystem` is checking `NextStateComponent` for non-default next :ref:`Action state <pedestrianActionState>` and checks if the list of available states contains that state.

	`Available state list for the current state can be defined` :ref:`here <pedestrianStateAuthoring>`.
	
#. If state is available, set `StateComponent` to the new state and set :ref:`Movement state <pedestrianMovementState>` according to :ref:`Movement binding data <pedestrianStateBinding>`.
#. After the :ref:`Movement state <pedestrianMovementState>` is set to a new state, the `MovementStateChangedEventTag` tag is enabled & new animation movement animation is running in the appropriate animation system.
	* For Legacy skin :ref:`LegacyAnimatorSystem <legacyAnimatorExample>`.
	* For GPU skin :ref:`GPUAnimatorSystem <gpuAnimatorExample>`.
	
#. If you want to set the :ref:`Custom animation <customAnimatorState>` for pedestrian read :ref:`this <customAnimatorState>`.

How To Change
~~~~~~~~~~~~

..  code-block:: r

	// Switch state example
	
    [WithDisabled(typeof(WaitForGreenLightTag))]
    [BurstCompile]
    public partial struct CheckTrafficLightJob : IJobEntity
    {
	
    void Execute(
	ref DestinationComponent destinationComponent,
	ref NextStateComponent nextStateComponent,
	EnabledRefRW<WaitForGreenLightTag> waitForGreenLightTagRW,
	EnabledRefRW<CheckTrafficLightStateTag> checkTrafficLightStateTagRW)
	{
		// Tag is triggering system
		checkTrafficLightStateTagRW.ValueRW = false;

		//Example red traffic light flag logic
		bool redLight = true;
		
		if (redLight)
		{
			// If the next state is available, start waiting for a green light. 
			
			if (nextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight, ref destinationComponent))
			{
				// Some logic
			
				waitForGreenLightTagRW.ValueRW = true;
			
				// If the entity has a custom animation for this state, use the 'AnimatorStateExtension.AddCustomAnimatorState' method
			}
			else
			{
				// Otherwise return to previous destination, for example
			}				
		}
		else
		{
			// Not red traffic light then set cross the road state										
			nextStateComponent.TryToSetNextState(ActionState.CrossingTheRoad);
		}
	}
	}
	
Custom State System
~~~~~~~~~~~~

If you want to temporarily control certain pedestrians with monobehaviour :ref:`read this article <pedestrianDisableSimulation>` or see the sample code below to control pedestrians with `DOTS` script:

..  code-block:: r

	// Custom state system example
	
    [BurstCompile]
    public partial struct CustomStateJob : IJobEntity
    {
	
	void Execute(
	ref StateComponent stateComponent,
	ref NextStateComponent nextStateComponent,
	EnabledRefRW<WaitForGreenLightTag> waitForGreenLightTagRW)
	{
		// Some logic for waiting traffic light
		bool greenLight = true;
		
		if (!greenLight)
		{
			// Some logic while waiting for the green light			
		}
		
		// If the traffic light is green or another system has changed state, leave current system
		var leaveState = greenLight || !stateComponent.HasActionState(in nextStateComponent, ActionState.WaitForGreenLight);
		
		if (leaveState)
		{
			waitForGreenLightTagRW.ValueRW = false;
			
			if (greenLight)
			{
				nextStateComponent.TryToSetNextState(ActionState.CrossingTheRoad);
			}
			else
			{
				// Otherwise logic if the state is interrupted with another system
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
				
.. _pedestrianDisableSimulation:
				
User Custom Control & Interaction
----------------

If you need to temporarily take full control of specific `Pedestrian` in your own way, use this:

* Get the desired entity using :ref:`either method <pedestrianEntitySelection>`.
* Use this sample code to temporarily remove/restore pedestrians from built-in DOTS systems.

PedestrianInteractUtils Methods
~~~~~~~~~~~~

	..  code-block:: r
	
		// Remove the pedestrian entity from the DOTS simulation. All custom states, locomotion & animation should be handled by custom user code using monobehaviour scripts.
		PedestrianInteractUtils.RemoveFromSimulation(entity);
		
	..  code-block:: r
	
		// Return the entity to the simulation.
		PedestrianInteractUtils.RestoreToSimulation(entity);
		
Interaction Mono Example
~~~~~~~~~~~~

	..  code-block:: r
	
		public class PedestrianInteractable : MonoBehaviour
		{
			private IHybridEntityRef hybridEntityRef;
			private bool activated;

			public bool Activated => activated;

			private void Awake()
			{
				hybridEntityRef = GetComponent<IHybridEntityRef>();
			}

			/// <summary>
			/// Remove the pedestrian entity from the DOTS simulation. All custom states, locomotion & animation should be handled by custom user code using monobehaviour scripts.
			/// </summary>
			public bool Activate()
			{
				if (activated) return false;

				if (PedestrianInteractUtils.RemoveFromSimulation(hybridEntityRef.RelatedEntity))
				{
					activated = true;
				}

				return activated;
			}

			/// <summary>
			/// Return the entity to the simulation.
			/// </summary>
			public bool Deactivate()
			{
				if (!activated) return false;

				if (PedestrianInteractUtils.RestoreToSimulation(hybridEntityRef.RelatedEntity))
				{
					activated = false;
				}

				return !activated;
			}
		}		
		
.. _pedestrianEntitySelection:
		
Entity Selection
----------------
		
Entity can be retrieved using one of these methods:
		
Pure DOTS
~~~~~~~~~~~~

* Create a new gameobject with `EntitySelectionService` component
* Use world position to get the nearest entity for that position.

	..  code-block:: r
	
		public Entity TryToSelectEntity(Vector3 worldPosition)
		{
			return EntitySelectionService.Instance.SelectEntity(worldPosition, EntityType.Pedestrian, 1f);
		}

Hybrid Mono
~~~~~~~~~~~~

Entity can be retrieved if the NPC has a collider:

	..  code-block:: r
	
			private Entity GetEntity()
			{
				Entity entity = Entity.Null;
				
			    if (Physics.Raycast(transform.position, Vector3.forward, out hit, 1.0f))
				{
					var hybridEntityRef = hit.collider.GetComponent<IHybridEntityRef>();
					entity = hybridEntityRef.RelatedEntity;
				}				
				
				return entity;
			}		

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

.. _pedestrianConfigs:

Configs
----------------

Pedestrian Spawner Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSpawnerConfig.png
	``Hub/Configs/PedestrianConfigs/CommonConfig``
	
| **Min pedestrian count** : number of pedestrians in the city.
| **Pool size** : pool size of :ref:`HybridLegacy <pedestrianHybridLegacy>` skins.
| **Ragdoll pool size** : :ref:`pedestrian ragdoll pool size<pedestrianRagdoll>`.
| **Min/Max spawn delay** : minimum and maximum delay between spawn iterations.
	
.. _pedestrianSettingsConfig:
	
Pedestrian Settings Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSettingsConfig.png
	``Hub/Configs/PedestrianConfigs/CommonConfig``

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
* **Hybrid and GPU** : :ref:`New hybrid GPU <hybridAndGpu>` mode that allows you to mix hybrid animator models for near and GPU animation for far at the same time.

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
| **Agents navigation** : navigating with `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin (:ref:`how to setup <pedestrianAgentsNavigation>`).
	
.. _pedestrianNavigationType:

Pedestrian Navigation Type **[** :ref:`NavMesh <pedestrianNavmeshNavigation>` **navigation only]**
""""""""""""""""""

* **Temp** : navigation will be enabled if there is an obstacle in front of pedestrian.
* **Persist** : navigation is always on.
* **Disabled**	
	
.. _pedestrianCollisionType:
	
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
	``Hub/Configs/PedestrianConfigs/NavAgentConfig``

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
	``Hub/Configs/PedestrianConfigs/LocalAvoidanceConfig``
	
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
	``Hub/Configs/PedestrianConfigs/AntistuckConfig``
	
| **Antistuck enabled** : on/off anti-stuck feature (if disabled previous target will be selected).
| **Target direction dot** : direction between the pedestrian's forward and the anti-stuck point.
| **Achieve distance** : achieve distance to the antistuck target point.
| **Target point offset** : distance between collision and anti-stuck point.
	
Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianTriggerConfig.png
	``Hub/Configs/PedestrianConfigs/TriggerConfigs/PedestrianCommonTriggerConfig``
	
| **Trigger HashMap capacity** : initial hashmap capacity  that contains data of triggers.
| **Trigger HashMap cell size** : hashmap cell size.
**Trigger data:**
	* **Fear Point Trigger** :
		* **Impact trigger duration** : duration of the :ref:`trigger<pedestrianScaryTrigger>` on the pedestrian.

.. _pedestrianScaryTrigger:

Scary Trigger Config
~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianScaryTriggerConfig.png
	``Hub/Configs/PedestrianConfigs/TriggerConfigs/PedestrianScaryTriggerConfigAuthoring``
	
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
	``Hub/Configs/PedestrianConfigs/BenchConfig``
	
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
	``Hub/Configs/PedestrianConfigs/SoundConfig``
	
| **Sound death** : :ref:`sound<soundData>` when a pedestrian died.
| **Enter tram sound** : :ref:`sound<soundData>` when entering a tram.
| **Exit tram sound** : :ref:`sound<soundData>` when exiting a tram.


.. _pedestrianStateAuthoring:

State Authoring
~~~~~~~~~~~~
	
State Dictionary
""""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring1.png
	``Hub/Configs/PedestrianConfigs/PedestrianStateAuthoring``

| **Next states** : which :ref:`states <pedestrianActionState>` can override the current :ref:`state <pedestrianActionState>`.

**State type:** 
	* **Default** : the state proccessed by `PedestrianStateSystem` system (code processing for state should be there PedestrianStateSystem.cs:144).
	* **External system** : the state proccessed by external system (code processing for state should be in the separate system).
	* **Additive** : additive state flag adds to the current state and is processed by the `External system`.
	* **Additive any** : additive state flag adds to the current state and is processed by the `External system` & ignores available next state flags.

.. _pedestrianStateBinding:

Movement State Binding Dictionary
""""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring2.png
	``Hub/Configs/PedestrianConfigs/PedestrianStateAuthoring``

Contains data - which :ref:`Movement state <pedestrianMovementState>` is assigned after the :ref:`Action state <pedestrianActionState>` is assigned.
	
	.. note:: 
		* Read more the :ref:`state info <pedestrianStates>` & :ref:`available states <pedestrianActionState>`.
