.. _pedestrianEntity:

Pedestrian
==========

.. contents::
   :local:


How To Create
-------------

.. _pedestrianHybridLegacy:

Hybrid Legacy Skin
~~~~~~~~~~~~~~~~~~

A `Hybrid legacy skin` is a :ref:`hybrid entity <hybridEntity>` that combines the default `GameObject` (with `animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_) and the DOTS entity.

Factory
"""""""

	#. Open `PedestrianSkinFactory` in the scene.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianSkinFactory``

		.. image:: /images/configs/pedestrian/PedestrianSkinFactory.png
	
	#. Enable the `Show Add New Prefab Settings`.
	#. Drag & drop source prefabs into the `New Prefabs` field.
	#. Customize the prefab names.
	#. Click `Try To Add Prefabs`.
	#. If necessary, configure :ref:`Ragdoll <pedestrianRagdoll>` and assign it to the `Pedestrian Skin Factory Data` (make sure :ref:`Ragdoll <pedestrianRagdoll>` is :ref:`enabled <pedestrianSettingsConfig>`).

	.. note:: 
		Each `Hybrid legacy` pedestrian prefab should have the `PedestrianEntityRef` component.
		
Animations
""""""""""

By default, each pedestrian has a `PedestrianBaseController` animator.

**Animation List:**

+------------------------+--------------+-----------+-----------------------------------+
| Animation name         |  Parameters  |   Value   |   When it starts                  |
+========================+==============+===========+===================================+
| Walking                |- yInput      |   - 0.3   | By default                        |
|                        |- SideMovement|   - 0     |                                   |
+------------------------+--------------+-----------+-----------------------------------+
| Running                |- yInput      |   - 1     | By default                        |
|                        |- SideMovement|   - 0     |                                   |
+------------------------+--------------+-----------+-----------------------------------+
| Idle                   |- yInput      |   - 0     | By default                        |
|                        |- SideMovement|   - 0     |                                   |
+------------------------+--------------+-----------+-----------------------------------+
| Stand To Sit           |- IsSitting   |   - true  | By default                        |
|                        |              |           |                                   |
+------------------------+--------------+-----------+-----------------------------------+
| Sitting Idle           |              |           | Starts when *Stand To Sit*        |
|                        |              |           | is completed                      |
+------------------------+--------------+-----------+-----------------------------------+
| Sit To Stand           |- IsSitting   |   - false | Starts after *Sitting Idle*       |
+------------------------+--------------+-----------+-----------------------------------+
| Talking 1, 2, 3        |- Talking     |   - 0,1,2 | By default                        |
|                        |              |           |                                   |
+------------------------+--------------+-----------+-----------------------------------+
| GettingUp              |- GetUp       |   - 0, 1  | Starts after getting up from      |
|                        |              |           | ragdoll:                          |
|                        |              |           | 0: Getting Up Face Up             |
|                        |              |           | 1: Standing Up Face Down          |
+------------------------+--------------+-----------+-----------------------------------+

**Used in systems:**
	* LegacyAnimatorSystem
	* LegacyAnimatorCustomStateSystem
	
.. _legacyAnimatorExample:

Animation authoring
"""""""""""""""""""

* Add your animation to the `AnimationState` script file.
* In the scene find:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateAuthoring.png
	`Hub/Configs/PedestrianConfigs/PedestrianAnimationStateAuthoring`.

* Add your animation to the list & enter conditions to start the animation from the assigned `Animator`:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateLegacyExample.png
	
	* **State name** : state name of the animation in the `Animator`.
	* **State layer** : number of the layer where the animation is stored in the `Animator`.
	* **Param 1** : first parameter to start animation in the `Animator`.
	* **Param 2** : second parameter to start animation in the `Animator` *[optional]*.
	* **Exit param** : parameter to exit current animation in the `Animator` *[optional]*.
	
* How to play animation is described :ref:`here <pedestrianAnimation>`.

.. _pedestrianGPU:

Pure GPU Skin
~~~~~~~~~~~~~

`Pure GPU skin` is a :ref:`pure entity <pureEntity>` that combines GPU texture animations and the DOTS entity.

.. _crowdSkinFactory:

How To Create
"""""""""""""

	#. Create :ref:`GPU prefabs <animationBakerHowTo>` in the :ref:`Animation baker <animationBaker>` tool.

	#. Open `PedestrianCrowdSkinFactory` in the scene.
	
		``Hub/Pools/Npc/Pedestrian/PedestrianGPUSkinFactory``

	#. Click `+` to show the `New Entry` panel.
	
		.. image:: /images/pedestrian/baker/AddNewEntryPanelExample.png
			
	#. Drag & drop prefabs.
	
		.. image:: /images/pedestrian/baker/animBaker4.png
	
	#. Result example:
	
		.. image:: /images/pedestrian/baker/animBaker5.png

	#. Assign :ref:`Ragdolls <pedestrianRagdoll>` **[optional step]**.
	
		.. image:: /images/pedestrian/baker/animBaker6.png
	
	**Used in systems:**
		* GPUAnimatorSystem
		* GPUAnimatorCustomStateSystem
	
.. _gpuAnimatorExample:

Animation authoring
"""""""""""""""""""

* Add your animation to the `AnimationState` script file.
* In the scene find:

	.. image:: /images/pedestrian/animation/PedestrianAnimationStateAuthoring.png

	`Hub/Configs/PedestrianConfigs/PedestrianAnimationStateAuthoring`.
	
* Add binding in the list (`AnimationState` is a key, `Animation` from :ref:`Animation collection <animationGPUAnimationCollection>` is a value)

	.. image:: /images/pedestrian/animation/PedestrianAnimationGpuExample.png
	`Example.`
	
* How to play animation is described :ref:`here <pedestrianAnimation>`.

Crowd GPU Custom Animator
"""""""""""""""""""""""""

The Crowd GPU Custom animator is used for transitions between baked animations (implemented by the `CrowdAnimatorTransitionSystem` system).

.. _animationBakerHowToCreateTransition:

**How To Create Transition:**
	#. Open `CrowdGPUAnimatorAuthoring` in the scene.
	
		``Hub/Configs/BakerRefs/Settings/CrowdGPUAnimatorAuthoring``
		
		.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png

				
	#. Create an :ref:`Animator Data Container <animationGPUAnimatorContainer>` from the project context menu and assign it to the animator (if required).
	#. Assign the :ref:`Animation Collection <animationGPUAnimationCollection>` same as in the :ref:`PedestrianCrowdSkinFactory <crowdSkinFactory>`.
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
~~~~~~~~~~~~~~

A hybrid GPU mode that allows you to mix hybrid animator models for near view and GPU animation for far view at the same time.

How To Create
"""""""""""""

* Create :ref:`Legacy <pedestrianHybridLegacy>` pedestrians.
* Add desired animations in the :ref:`Animation state authoring <legacyAnimatorExample>` for :ref:`Legacy <pedestrianHybridLegacy>` pedestrians.
* Create :ref:`GPU <pedestrianGPU>` pedestrians.
* Add desired animations in the :ref:`Animation state authoring <gpuAnimatorExample>` for :ref:`GPU <pedestrianGPU>` pedestrians.
* Make sure that the number and order of :ref:`Legacy <pedestrianHybridLegacy>` and :ref:`GPU <pedestrianGPU>` models are the same in both factories (`PedestrianSkinFactory` & `PedestrianGPUSkinFactory`).
* How to play animation is described :ref:`here <pedestrianAnimation>`.

Cull state
""""""""""

* :ref:`InViewOfCamera <cullPointStates>`: :ref:`Hybrid <pedestrianHybridLegacy>` legacy skin is enabled.
* :ref:`CloseToCamera <cullPointStates>`: :ref:`GPU <pedestrianGPU>` skin is enabled.

Hybrid On Request And GPU
~~~~~~~~~~~~~~~~~~~~~~~~~

By default, the entity is animated by `GPU` until a `Hybrid skin` is requested.

How To Create
"""""""""""""

* Create entities as :ref:`Hybrid and GPU <hybridAndGpu>` pedestrians.
* Hybrid skin is enabled if the entity disables the `PreventHybridSkinTag` tag. To switch back to `GPU`, enable the `PreventHybridSkinTag` tag again.

Hybrid Shape GPU
~~~~~~~~~~~~~~~~

`Hybrid Shape GPU skin` is a :ref:`hybrid entity <hybridEntity>` animated on `GPU` in `DOTS` & has a hybrid MonoBehaviour collider to interact with pedestrians in a familiar way.

How To Create
"""""""""""""

* Create :ref:`GPU <pedestrianGPU>` pedestrians.
* The hybrid shape can be edited here:
	
	.. image:: /images/pedestrian/HybridShapeFactory.png	

.. _rukhankaSkin:

Rukhanka
~~~~~~~~

Pure entities animated with the `Rukhanka Animation System <https://assetstore.unity.com/packages/tools/animation/rukhanka-ecs-animation-system-241472>`_ in `DOTS`.

How To Create
"""""""""""""

* Import `Rukhanka` samples (uses the `AnimatedLitShader URP` shader from the sample).

	.. image:: /images/integration/rukhanka0.png	
	
* Unpack `RukhankaSample` prefabs:

	.. image:: /images/integration/rukhanka1.png	
	
* Create a new GameObject in the scene, add an `AnimationCullingConfig` component, and assign the main camera to it.
* Create a pedestrian prefab with the `Animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, add `PedestrianAuthoring` & `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ components, and assign the desired prefab here:

	.. image:: /images/integration/rukhanka2.png	
	
	.. image:: /images/integration/rukhanka3.png	
	
* Animation is taken from :ref:`Animation state authoring <legacyAnimatorExample>` as for :ref:`Hybrid legacy <pedestrianHybridLegacy>` pedestrians.
* If you get a ``Blob asset System.String System.Type::get_FullName() with hash 'Unity.Entities.Hash128' is corrupted.`` error, try closing the subscene (uncheck the box next to `EntitySubscene`) & start the scene again.

.. _rukhankaHybridSkin:

Rukhanka Hybrid
~~~~~~~~~~~~~~~

Hybrid entities animated with the `Rukhanka Animation System <https://assetstore.unity.com/packages/tools/animation/rukhanka-ecs-animation-system-241472>`_ with a hybrid MonoBehaviour collider & Rigidbody to control or interact with pedestrians in a familiar way.

How To Create
"""""""""""""

* Import `Rukhanka` samples (uses the `AnimatedLitShader URP` shader from the sample).

	.. image:: /images/integration/rukhanka0.png	
	
* Unpack `RukhankaSample` prefabs:

	.. image:: /images/integration/rukhanka1.png	
	
* Create a new GameObject in the scene, add an `AnimationCullingConfig` component, and assign the main camera to it.
* Create a pedestrian prefab with the `Animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, add `PedestrianAuthoring` & `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ components, and assign the desired prefab here:

	.. image:: /images/integration/rukhanka2.png	
	
	.. image:: /images/integration/rukhanka3.png	
	
* The hybrid shape can be edited here:
	
	.. image:: /images/pedestrian/HybridShapeFactory.png	
	
* Animation is taken from :ref:`Animation state authoring <legacyAnimatorExample>` as for :ref:`Hybrid legacy <pedestrianHybridLegacy>` pedestrians.
* If you get a ``Blob asset System.String System.Type::get_FullName() with hash 'Unity.Entities.Hash128' is corrupted.`` error, try closing the subscene (uncheck the box next to `EntitySubscene`) & start the scene again.
	
How To Control
""""""""""""""

You can control the `Rukhanka Hybrid` NPC with a MonoBehaviour script:

* Make sure that `HybridShapeFactory` prefab contains `RukhankaEntityAdapter`.
* :ref:`Temporarily remove <pedestrianDisableSimulation>` the entity from the built-in DOTS simulation.
* Methods to control animation work the same way as the `Unity animator <https://docs.unity3d.com/ScriptReference/Animator.html>`_, but using the `RukhankaEntityAdapterBase` component.
* Example:

 	..  code-block:: csharp
	
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
"""""""""""""

If you need to attach a GameObject weapon, e.g.:

* Add `RukhankaHybridBoneAnchorAuthoring` to the entity prefab.
* In `RukhankaHybridBoneAnchorAuthoring`, assign the bone that you want to attach to.
* Attach the anchor with the local index:

 	..  code-block:: csharp
	
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
"""""""""""""""

* In the `RigDefinitionAuthoring <https://docs.rukhanka.com/getting_started#authoring-object-setup>`_ component, enable the `Has Animation Events` option.
* Then, use this sample code:

 	..  code-block:: csharp
	
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
		
.. _animatronSkin:

Animatron
~~~~~~~~~

Pure entities animated with `Animatron <https://assetstore.unity.com/packages/tools/animation/animatron-314750>`_ in `DOTS`.

How To Create
"""""""""""""

#. Unpack `AnimatronSample` prefabs:

	.. image:: /images/integration/animatron1.png
	
#. Imported samples can be found here:

	.. image:: /images/integration/animatron1_2.png
	.. image:: /images/integration/animatron1_3.png
	
#. Create a new `Rig <https://lukaschod.github.io/animatron-docs/manual/authoring/rig.html>`_ asset from the project context menu ``Create/Rig``.

#. In the created rig, drag & drop your FBX file of the pedestrian into the prefab field. Then, press the `Apply` button.

	.. image:: /images/integration/animatron1_4.png
	
#. Drag & drop animation clips into the animation list. The order of animations should match :ref:`Animation authoring <legacyAnimatorExample>`, animation names can be anything. Then, press the `Apply` button.

	.. image:: /images/integration/animatron4.png

#. In the `Skins` tab, keep only the skin being used for the character.

	.. image:: /images/integration/animatron4_2.png
	
#. Drag & drop the created rig into the scene.

	.. image:: /images/integration/animatron5.png

#. Add the `PedestrianAuthoring` component to the created object in the scene.

	.. image:: /images/integration/animatron5_2.png

#. Select `Render Mesh Array` of the character.

	.. image:: /images/integration/animatron5_1.png
	
#. Create a new material & assign the ``Shader Graphs/LitSkinned`` shader to it.
	
	.. image:: /images/integration/animatron5_1_1.png
	
#. Assign your texture to `BaseMap`.

	.. image:: /images/integration/animatron5_1_2.png
	
#. Drag & drop the created material into the material field of the `Render Mesh Array` component.
	
	.. image:: /images/integration/animatron5_1_3.png
	
#. Then, drag & drop the created prefab from the scene into the project view.

	.. image:: /images/integration/animatron6.png

#. Add the resulting prefab to the `Prefab container`.

	.. image:: /images/integration/animatron7.png
	.. image:: /images/integration/animatron8.png
	
#. In the :ref:`Pedestrian settings <pedestrianSettingsConfig>`, select `Animatron` rig type.
#. To quickly create new characters, simply duplicate the `Rig <https://lukaschod.github.io/animatron-docs/manual/authoring/rig.html>`_ asset and assign a new FBX file with different skins. Then, drag and drop it into the scene as before, save it as a prefab, and assign it to the `Prefab container`.

.. _animatronHybridSkin:

Animatron Hybrid
~~~~~~~~~~~~~~~~

Hybrid entities animated with `Animatron <https://assetstore.unity.com/packages/tools/animation/animatron-314750>`_ in `DOTS`.

How To Create
"""""""""""""

#. Follow the steps for :ref:`Animatron <animatronSkin>`.
#. Add the `AnimatronEntityAdapter` component to the `NpcHybridShape` prefab.

	.. image:: /images/integration/animatron9.png
	
#. In the :ref:`Pedestrian settings <pedestrianSettingsConfig>`, select `Animatron hybrid` rig type.
#. Now, you can disable the pedestrian from the :ref:`DOTS simulation <pedestrianDisableSimulation>` at any time and handle it manually via the `AnimatronEntityAdapter` component.
		
Runtime Attachment
""""""""""""""""""

#. Add the `AnimatronRuntimeAttachment` component to your attachment.
#. Use the ``SetAttachment`` method of `AnimatronRuntimeAttachment` to attach to the `AnimatronEntityAdapter` with the specified `Joint name`.

.. _pedestrianRagdoll:

Ragdoll
~~~~~~~

Ragdoll is created at the scene of the pedestrian's death. Make sure ragdoll is :ref:`enabled <pedestrianSettingsConfig>`.

How To Create
"""""""""""""

#. Add all colliders and rigidbodies to the character according to the `RagdollWizard <https://docs.unity3d.com/2021.1/Documentation/Manual/wizard-RagdollWizard.html>`_ tutorial.

	.. image:: /images/pedestrian/RagdollAssignExample.png	
	`RagdollWizard example.`
		
#. Add the `PedestrianRagdoll` component.

	.. image:: /images/pedestrian/RagdollComponent.png	
	
#. For remaining characters, open the `RagdollCloner` tool.

	.. image:: /images/pedestrian/RagdollClonerPath.png	
	.. image:: /images/pedestrian/RagdollCloner1.png	
	
#. Assign the source character created first and the target remaining characters.

	.. image:: /images/pedestrian/RagdollCloner2.png	

#. Click the `Create` button.
#. Assign the result to :ref:`PedestrianHybridLegacyFactory <pedestrianHybridLegacy>` or :ref:`PedestrianCrowdSkinFactory <crowdSkinFactory>` depending on the :ref:`type of rig <pedestrianSettingsConfig>` you have chosen.

	.. note:: 
		* Implemented by `RagdollSystem`.
		* Currently only collides with default `colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_.
		* Make sure that the scene contains `default colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_.
		* Read more info about the :ref:`Physics Transfer Service <physicsShapeTransfer>` on how to clone legacy colliders.

.. _pedestrianNavigation:

Navigation
----------

| Navigation is used for pedestrian obstacle avoidance.
| There are 5 types of navigation:

.. _pedestrianNavmeshNavigation:

Simple NavMesh
~~~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_.

Useful links:
	* :ref:`NavAgent Config <pedestrianNavAgentConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.
	
Installation
""""""""""""

* Make sure that navigation is enabled in the :ref:`General Config <generalSettingsConfig>`.
* Ensure that :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Each dynamic object in the scene must have a `NavMeshObstacle <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshObstacle.html>`_ component.

How To Setup
""""""""""""

* Create a new GameObject & add the `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ component.
* Set `Agent type` to `Humanoid` & press the `Bake` button in the created `NavMeshSurface`.
* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Calc Nav Path`.
* Set :ref:`Pedestrian navigation type <pedestrianNavigationType>` to `Temp` or `Persist` mode.

Pros And Cons
"""""""""""""
	
Pros:
	* High precision.
	* Can avoid any obstacle.
	
Cons:
	* High CPU load.

.. _pedestrianLocalAvoidance:

Local Avoidance 
~~~~~~~~~~~~~~~

DOTS system to avoid local obstacles (vehicles).

Useful links:
	* :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.

How To Setup
""""""""""""

* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Local Avoidance`.
* Configure :ref:`Local Avoidance Config <pedestrianLocalAvoidanceConfig>`.

Pros And Cons
"""""""""""""

Pros:
	* Low CPU load.
	
Cons:
	* Can avoid vehicles only.
	* Works on flat surfaces only.
	
.. _pedestrianCrowdAvoidance:

Crowd Avoidance
~~~~~~~~~~~~~~~

High-performance DOTS-based crowd avoidance system designed for high agent density. It calculates lateral steering and separation/push forces between pedestrians, handles vehicle OBB avoidance with support for merging overlapping vehicle bounds (such as trailers or traffic jams), and dynamically enforces path boundary constraints.

Useful links:
	* :ref:`Crowd Avoidance Config <pedestrianCrowdAvoidanceConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.

How To Setup
""""""""""""

* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Crowd Avoidance`.
* Configure parameters in the `Pedestrian Crowd Avoidance Authoring` component or via the :ref:`Crowd Avoidance Config <pedestrianCrowdAvoidanceConfig>`.

Pros And Cons
"""""""""""""

Pros:
	* High performance and scalability for large crowds.
	* Handles both pedestrian-to-pedestrian separation and vehicle obstacle avoidance.
	* Automatically keeps agents within sidewalk and crosswalk path boundaries.

Cons:
	* Designed primarily for flat surfaces.

.. _pedestrianCrowdAvoidanceNavMesh:

Crowd Avoidance NavMesh
~~~~~~~~~~~~~~~~~~~~~~~

Extends the Crowd Avoidance pipeline with NavMesh query integration. It uses multi-ray fan casts against the NavMesh to detect static geometry, providing wall repulsion and sliding forces, while continuously mapping agent height (`TargetY`) for uneven terrain.

.. warning::
   If **Move Inside Path** is enabled and a `NavMeshObstacle` blocks the path, pedestrians may get stuck permanently. To prevent this, either disable **Move Inside Path** or ensure the path is wide enough for agents to bypass the obstacle.

Useful links:
	* :ref:`Crowd Avoidance Config <pedestrianCrowdAvoidanceConfig>`
	* :ref:`Test scene <pedestrianNavigationTest>`.

How To Setup
""""""""""""

* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Crowd Avoidance NavMesh`.
* Ensure a valid `NavMeshSurface` is baked in the scene.
* Configure parameters in the `Pedestrian Crowd Avoidance Authoring` component (see :ref:`Crowd Avoidance Config <pedestrianCrowdAvoidanceConfig>`).

NavMesh Y-Surface Snapping Only Mode
""""""""""""""""""""""""""""""""""""

You can also use **Crowd Avoidance NavMesh** in a lightweight mode purely for **vertical alignment (Y-axis snapping)** onto the NavMesh surface, without enabling heavy NavMesh pathfinding or obstacle avoidance routines.

* **Height Conformance:** Ideal when pedestrian movement is primarily driven by grid paths or direct node networks, but agents still need to align accurately with uneven terrain, ramps, or subtle elevation changes.
* **Avoid Getting Stuck on Complex Geometry:** Bypasses full NavMesh pathfinding queries. If your NavMesh geometry is overly complex, detailed, or contains narrow topological traps, standard NavMesh navigation can cause agents to get stuck or enter recalculation loops; using pure Y-snapping prevents this entirely.
* **Performance Optimization:** Leverages cached ground height sampling while skipping expensive raycasting and path queries, offering smooth terrain tracking with minimal CPU overhead.
* **Seamless Integration:** Allows standard Crowd Avoidance to handle horizontal density and separation logic while the NavMesh strictly manages vertical placement.

Pros And Cons
"""""""""""""

Pros:
	* Full height-mapping support for sloped or multi-level terrain.
	* Prevents agents from colliding with or walking through static NavMesh walls and obstacles.
	* Can be used purely for Y-surface snapping.
	* Combines dynamic agent crowd separation with static environment boundary logic.

Cons:
	* Slightly higher CPU load compared to flat Crowd Avoidance due to NavMesh raycasting (unless operating in pure Y-snapping mode).

.. _pedestrianAgentsNavigation:

Agents Navigation 
~~~~~~~~~~~~~~~~~

DOTS navigation on `NavMeshSurface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavMeshSurface.html>`_ using `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin.

How To Setup
""""""""""""

* Make sure that you purchased & downloaded the `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin.
* Set :ref:`Avoidance type <pedestrianObstacleAvoidanceType>` to `Agents Navigation`.
* Enable the `Auto Add Agent Components` option for quick prototyping in :ref:`Pedestrian settings <pedestrianSettingsConfig>` & customize settings in the `Agents Navigation Config Authoring` tab (the tab below :ref:`Pedestrian settings <pedestrianSettingsConfig>`), or add agent authoring components to the `PedestrianEntity` prefab from the `Agents Navigation` sample for more flexible settings. (`Agents Navigation doc <https://lukaschod.github.io/agents-navigation-docs/manual/game-objects.html>`_)
* Ensure that :ref:`NavMeshObstacle <trafficNavMeshObstacle>` is enabled for traffic.
* Add `Agent Collider Hybrid Component` to the `HybridEntityRuntimeAuthoring` of your :ref:`player character <playerCustom>` if you want to collide with pedestrians [**optional step**].

.. _pedestrianAnimation:

Animation
---------

.. _customAnimatorState:

Custom Animation
~~~~~~~~~~~~~~~~

To handle custom animations, follow these steps:

* Add custom animations in `Animation state authoring` for pedestrians:
	* :ref:`Hybrid skin <legacyAnimatorExample>` (if using Hybrid animations).
	* :ref:`GPU skin <gpuAnimatorExample>` (if using GPU animations).
	
* Add custom animator state via code:
	
..  code-block:: csharp
	
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
	
* Change to a new state if required:

..  code-block:: csharp

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
	
* After all custom animations have played, turn off the custom animation state:

..  code-block:: csharp

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
		For an example of a system, please inspect the script below:
			* BenchStateSystem.cs.			

.. _pedestrianStates:

States
------

Common Logic
~~~~~~~~~~~~

#. Custom system sets the next :ref:`Action state <pedestrianActionState>` in `NextStateComponent` via a utility method:

	* ``bool NextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight, ref destinationComponent)``
		`Example method: if state cannot be set, target swaps back.`
		
	* ``bool NextStateComponent.TryToSetNextState(ActionState.WaitForGreenLight)``
		`Example method without retargeting.`
	
#. `PedestrianStateSystem` checks `NextStateComponent` for non-default next :ref:`Action state <pedestrianActionState>` and checks if the list of available states contains that state.

	`Available state list for the current state can be defined` :ref:`here <pedestrianStateAuthoring>`.
	
#. If the state is available, set `StateComponent` to the new state and set :ref:`Movement state <pedestrianMovementState>` according to :ref:`Movement binding data <pedestrianStateBinding>`.
#. If you need to implement custom logic, such as enabling a custom tag for a pedestrian entity when it reaches a node with your own custom type, you can modify the code in the `SelectAchievedTargetUtils.ProcessAchievedTarget` method.
#. After :ref:`Movement state <pedestrianMovementState>` is set to a new state, the `MovementStateChangedEventTag` tag is enabled & new movement animation runs in the appropriate animation system.
	* For Legacy skin: :ref:`LegacyAnimatorSystem <legacyAnimatorExample>`.
	* For GPU skin: :ref:`GPUAnimatorSystem <gpuAnimatorExample>`.
	
#. If you want to set a :ref:`Custom animation <customAnimatorState>` for pedestrian, read :ref:`this section <customAnimatorState>`.

How To Change
~~~~~~~~~~~~~

..  code-block:: csharp

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

		// Example red traffic light flag logic
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
~~~~~~~~~~~~~~~~~~~

If you want to temporarily control certain pedestrians with MonoBehaviour, :ref:`read this article <pedestrianDisableSimulation>` or see the sample code below to control pedestrians via a `DOTS` script:

..  code-block:: csharp

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
~~~~~~~~~~~~~~

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
* **CrossingTheRoad** : when a pedestrian is crossing a crosswalk.
* **ScaryRunning** : activated when a pedestrian runs away in panic (for example, at the sound of a gunshot or pedestrian death nearby).
* **Sitting** : when a pedestrian is sitting.
* **Talking** : when a pedestrian is talking.	

	.. note:: 
		You can edit state logic :ref:`here <pedestrianStateAuthoring>`.
				
.. _pedestrianAllowedGroups:

Allowed Groups
--------------

Pedestrians use the ``PedestrianGroupType`` bitmask to filter which nodes they can spawn on and travel through:

* **Node Filtering**: Set the ``AllowedGroups`` mask on each :ref:`PedestrianNode <pedestrianNode>` to specify which types of pedestrians are allowed to spawn on or navigate through that specific node.
* **Prefab Grouping**: Groups can be configured on the ``PedestrianAuthoring`` component of each entity prefab (see :ref:`Entity Customization <entityCustomization>`) to separate different pedestrian types (e.g., Civilians, Police, VIPs) and restrict their movement to designated areas or paths.
* **Bitmask Matching**: For a pedestrian to spawn on or travel through a node, the pedestrian's group mask and the node's ``AllowedGroups`` mask must share at least one common flag (``(pedestrianGroup & nodeAllowedGroups) != 0``).

.. note::
   The count and names of available groups can be modified via the Unity toolbar: **CityEditor/Window/Global settings**, or directly in the ``PedestrianGroupType.cs`` file.

.. _entityCustomization:

Entity Customization
--------------------

By default, 1 entity prefab is shared across all pedestrians. If you want to customize a specific entity for a skin (change spawn weight, set :ref:`allowed group type <pedestrianAllowedGroups>`, add custom entity components, etc.):

* Open :ref:`Pedestrian settings <pedestrianSettingsConfig>`.

	.. image:: /images/configs/pedestrian/entityCustomization1.png
	
* Duplicate the entity prefab. On each prefab's ``PedestrianAuthoring`` component, you can configure unique settings such as its spawn weight (``spawnWeight``) and allowed group mask (``groupType``), as well as add custom entity authorings.
* Set unique customization for prefab authorings (the order of entity prefabs within the prefab container should match that of the factory). 
* See the image below for an example of a prefab container (there are 2 prefabs: 1 standard pedestrian, 1 unique for police):

	.. image:: /images/configs/pedestrian/entityCustomization2.png
	
* The number of entries of entity prefabs in this ScriptableObject should match the factory it uses (``PedestrianSkinFactory`` for hybrid pedestrians or ``PedestrianGPUSkinFactory`` for GPU pedestrians).

.. _pedestrianDisableSimulation:
				
User Custom Control & Interaction
---------------------------------

If you need to temporarily take full control of a specific `Pedestrian` in your own way, use this:

* Get the desired entity using :ref:`either method <pedestrianEntitySelection>`.
* Use this sample code to temporarily remove/restore pedestrians from built-in DOTS systems.

PedestrianInteractUtils Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

	..  code-block:: csharp
	
		// Remove the pedestrian entity from the DOTS simulation. All custom states, locomotion & animation should be handled by custom user code using MonoBehaviour scripts.
		PedestrianInteractUtils.RemoveFromSimulation(entity);
		
	..  code-block:: csharp
	
		// Return the entity to the simulation.
		PedestrianInteractUtils.RestoreToSimulation(entity);
		
Interaction Mono Example
~~~~~~~~~~~~~~~~~~~~~~~~

	..  code-block:: csharp
	
		public class PedestrianInteractable : MonoBehaviour
		{
		private IHybridEntityRef hybridEntityRef;
		private bool activated;

		public bool Activated => activated;

		private void Awake()
		{
			hybridEntityRef = GetComponent<IHybridEntityRef>();

			// Note: NodeHashMapSystem.Register() is called here as an example, 
			// but in production it should be registered once in a dedicated manager or initialization service.
			NodeHashMapSystem.Register();
		}

		/// <summary>
		/// Remove the pedestrian entity from the DOTS simulation. All custom states, locomotion & animation should be handled by custom user code using MonoBehaviour scripts.
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
		/// <param name="reassignClosestNode">Optional flag to set destination to the closest node if pedestrian moved away.</param>
		public bool Deactivate(bool reassignClosestNode = false)
		{
			if (!activated) return false;

			var entity = hybridEntityRef.RelatedEntity;

			if (PedestrianInteractUtils.RestoreToSimulation(entity))
			{
				activated = false;

				// [Optional] Find the closest node and reassign destination if the pedestrian moved away
				if (reassignClosestNode)
				{
					var entityManager = World.DefaultGameObjectInjectionWorld.EntityManager;

					// Find the closest node relative to the pedestrian's current position
					Entity closestNode = NodeHashMapSystem.GetClosestNode(transform.position, out Vector3 nodePosition);

					if (entityManager.HasComponent<DestinationComponent>(entity))
					{
						var destinationComponent = entityManager.GetComponentData<DestinationComponent>(entity);
						destinationComponent.DestinationNode = closestNode;
						destinationComponent.Value = nodePosition;

						entityManager.SetComponentData(entity, destinationComponent);
					}
				}
			}

			return !activated;
		}
		}
		
.. _pedestrianEntitySelection:
		
Entity Selection
----------------
		
Entities can be retrieved using one of these methods:
		
Pure DOTS
~~~~~~~~~

* Create a new GameObject with the `EntitySelectionService` component.
* Use world position to get the nearest entity for that position.

	..  code-block:: csharp
	
		public Entity TryToSelectEntity(Vector3 worldPosition)
		{
			return EntitySelectionService.Instance.SelectEntity(worldPosition, EntityType.Pedestrian, 1f);
		}

Hybrid Mono
~~~~~~~~~~~

Entities can be retrieved if the NPC has a collider:

	..  code-block:: csharp
	
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

.. include:: runtime_custom_npc.rst

.. include:: temporaryRagdoll.rst

Common Info
-----------

Collision
~~~~~~~~~

In some cases, pedestrians can get stuck in obstacles (vehicles). To solve this problem, adjust the :ref:`Antistuck config <pedestrianAntistuckConfig>`.

Authoring Components
--------------------

Authoring components that make up the pedestrian entity.

PedestrianAuthoring
~~~~~~~~~~~~~~~~~~~

Contains the main components of the pedestrian entity **[required]**.

PlayerTargetAuthoring
~~~~~~~~~~~~~~~~~~~~~

Component for player targeting systems **[optional]**.

Physics
~~~~~~~

`PhysicsBody` and `PhysicsShape` components for physics-related systems **[optional]**.

.. _pedestrianConfigs:

Configs
-------

Pedestrian Spawner Config
~~~~~~~~~~~~~~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSpawnerConfig.png
	``Hub/Configs/PedestrianConfigs/CommonConfig``
	
| **Min pedestrian count** : number of pedestrians in the city.
| **Pool size** : pool size of :ref:`HybridLegacy <pedestrianHybridLegacy>` skins.
| **Ragdoll pool size** : :ref:`pedestrian ragdoll pool size<pedestrianRagdoll>`.
| **Min/Max spawn delay** : minimum and maximum delay between spawn iterations.
	
.. _pedestrianSettingsConfig:
	
Pedestrian Settings Config
~~~~~~~~~~~~~~~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianSettingsConfig.png
	``Hub/Configs/PedestrianConfigs/CommonConfig``

Skin Type
"""""""""

* **Rig show only in view** : rig skin will be loaded in the camera's view area.
* **Rig show always** : rig skin will be loaded when the entity is created and will exist until it is destroyed.
* **No skin** : entities without a skin will be created.
	
.. _rigType:
	
Rig Type
""""""""

* :ref:`Hybrid legacy <pedestrianHybridLegacy>` : hybrid entity with animator component.
* :ref:`Pure GPU <pedestrianGPU>` : pure entity with GPU animations.
* :ref:`Hybrid and GPU <hybridAndGpu>` : mode that allows you to mix Hybrid animator models for near view and GPU animation for far view at the same time.
* **Hybrid On Request And GPU** : Hybrid skin will load if the `PreventHybridSkinTag` tag is manually disabled by the user for the specific entity; otherwise, it will be animated by GPU.
* **Hybrid Shape GPU** : hybrid entity animated on GPU in `DOTS` & has a hybrid MonoBehaviour collider to interact with pedestrians in a familiar way.
* :ref:`Rukhanka <rukhankaSkin>` : pure entities animated with the Rukhanka Animation System in `DOTS`.
* :ref:`Rukhanka Hybrid <rukhankaHybridSkin>` : hybrid entities animated with the Rukhanka Animation System with a hybrid MonoBehaviour collider & Rigidbody to control or interact with pedestrians in a familiar way.
* :ref:`Animatron <animatronSkin>` : pure entities animated with the Animatron system in `DOTS`.
* :ref:`Animatron Hybrid <animatronHybridSkin>` : hybrid entities animated with the Animatron System with a hybrid MonoBehaviour collider & Rigidbody to control or interact with pedestrians in a familiar way.

.. _pedestrianEntityType:

Entity Type
"""""""""""

* **No physics** : pedestrian does not contain a `PhysicsShape` component.
* **Physics** : pedestrian contains a `PhysicsShape` component.
	
Common Settings
"""""""""""""""

| **Pedestrian collider radius** : pedestrian collider radius for `No physics` type.
| **Walking speed** : walking speed.
| **Running speed** : running speed.
| **Rotation speed** : rotation speed.
| **Health** : number of hit points for pedestrians.
| **Talking pedestrian spawn chance** : chance of spawning talking pedestrians.
| **Min/Max talk time** : min/max talk time.

.. _pedestrianObstacleAvoidanceType:
	
Obstacle Avoidance Type
"""""""""""""""""""""""

| **Calc nav path** : navigating based on :ref:`NavMesh <pedestrianNavmeshNavigation>` (:ref:`config <pedestrianNavAgentConfig>`).
| **Local avoidance** : simple :ref:`obstacle avoidance <pedestrianLocalAvoidance>` navigation (:ref:`config <pedestrianLocalAvoidanceConfig>`).
| **Agents navigation** : navigating with the `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ plugin (:ref:`how to setup <pedestrianAgentsNavigation>`).
	
.. _pedestrianNavigationType:

Pedestrian Navigation Type **[** :ref:`NavMesh <pedestrianNavmeshNavigation>` **navigation only]**
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

* **Temp** : navigation will be enabled if there is an obstacle in front of the pedestrian.
* **Persist** : navigation is always on.
* **Disabled**	
	
.. _pedestrianCollisionType:
	
Collision type
""""""""""""""

* **Calculate** : collision is calculated manually (:ref:`for NoPhysics type<pedestrianEntityType>`).
* **Physics** : collision is calculated with `Unity.Physics` (:ref:`for Physics type<pedestrianEntityType>`).
* **Disabled**
	
| **Has ragdoll** : on/off :ref:`ragdoll<pedestrianRagdoll>` for pedestrian.

.. _pedestrianNavAgentConfig:

NavAgent Config
~~~~~~~~~~~~~~~

Config for :ref:`NavMesh <pedestrianNavmeshNavigation>` navigation.

	.. image:: /images/configs/pedestrian/NavAgentConfig.png
	``Hub/Configs/PedestrianConfigs/NavAgentConfig``

| **Update frequency** : how often the nav target can be updated.
| **Max distance to target node** : distance to nav path node.
| **Max collision time** : if the pedestrian is stuck for more than the collision time, anti-stuck will be activated.

**Revert target support** : if the steering target is much further than the final target with a given value, the target will be reverted.
	* **Revert steering target distance** : distance to steering target logic for target return.
	* **Revert end target remaining distance** : distance to final target logic for target return.

.. _pedestrianLocalAvoidanceConfig:

Obstacle Local Avoidance Config
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Config for :ref:`Local Avoidance <pedestrianLocalAvoidance>` navigation.

	.. image:: /images/configs/pedestrian/PedestrianObstacleLocalAvoidanceSettings.png
	``Hub/Configs/PedestrianConfigs/LocalAvoidanceConfig``
	
**Obstacle avoidance method:**
	* **Simple** : able to avoid only 1 object.
	* **Find neighbors** : multiple objects close to each other are grouped as one (more performance-intensive).
	
| **Max surface angle** : maximum surface tilt angle at which avoidance is calculated.
| **Target point offset** : offset between an obstacle and avoidance waypoints.
| **Achieve distance** : distance to achieve the avoidance waypoint.
| **Check target availability** : check if destination can be reached; if not and no new target can be found, returns destination.

.. _pedestrianCrowdAvoidanceConfig:

Crowd Avoidance Config
~~~~~~~~~~~~~~~~~~~~~~

Config for :ref:`Crowd Avoidance <pedestrianCrowdAvoidance>` and :ref:`Crowd Avoidance NavMesh <pedestrianCrowdAvoidanceNavMesh>` navigation modes.

Location in project:
	``Hub/Configs/PedestrianConfigs/CrowdAvoidanceConfig``

Key Setup Steps & Recommendations
"""""""""""""""""""""""""""""""""

When tuning the crowd avoidance configuration, follow this recommended sequence to achieve realistic movement and optimal performance:

1. **Base Dimensions First**
   * Adjust **Npc Radius** to match your pedestrian model's visual volume.
   * Set **Effective Radius** based on local density. In dense urban environments, keeping it around 3–5 meters prevents agents from evaluating unnecessary distant interactions, saving CPU performance.

2. **Detection & Early Steering (Look Ahead Pedestrian)**
   * **Look Ahead Pedestrian** is a static configuration value (it does not dynamically scale with runtime speed changes). Set it to a fixed balance value (typically **1.5 – 2.5 meters**):
     * *Why balance matters:* Setting this value too low (< 1.0 m) causes agents to notice collisions too late, leading to abrupt turns. Setting it too high (> 4.0–5.0 m) forces pedestrians to react to distant oncoming agents who would have already passed by, resulting in unnaturally wide avoidance arcs.
   * Pair **Look Ahead Pedestrian** with **Side Bias Intensity** (>0.2) to ensure smooth, natural right-hand passing when two pedestrians meet head-on.
   * **Steering vs Push Balance:** Use **Look Ahead Pedestrian** for smooth early steering reaction. If agents regularly bump into each other before turning, adjust *Look Ahead Pedestrian* before cranking up physical push forces (**Skin Pedestrian** / **Push Intensity**).

3. **Pedestrian Separation & Density**
   * For tight crowds, lower **Skin Pedestrian** and increase **Push Intensity Pedestrian** to enforce tight physical boundaries without visual clipping.
   * If agents appear to "vibrate" or oscillate near their targets, lower **Steering Damping** slightly or increase **Arrival Fade Dist** so avoidance forces naturally decay as they reach their destination.

4. **Vehicle Avoidance Tuning**
   * Set **Look Ahead Car** based on average city traffic speeds. High-speed roads require longer look-ahead distances (8–12 meters).
   * Always enable **Find Neighbors** if your city features large vehicles (articulated buses, trucks with trailers) or frequent traffic jams. This groups individual vehicle bounds into a unified convex shape, eliminating erratic zig-zagging between cars.
   * Adjust **Tangent Blend Weight** (e.g., 0.6–0.8) if pedestrians should smoothly slide along the sides of stopped vehicles rather than bouncing backward.

5. **Sidewalk & Crosswalk Constraints**
   * Enable **Move Inside Path** to keep pedestrians strictly within sidewalk boundaries.
   * If agents get pushed into the street by dense crowds, increase **Spring Multiplier** or **Apply Border Force**.
   * Ensure **Apply Crosswalk Offset** is active if pedestrians need to spread out naturally while crossing roads.

6. **NavMesh Integration (NavMesh Mode Only)**
   * If using `Crowd Avoidance NavMesh`, fine-tune **Look Ahead Navmesh** to match pedestrian movement speed.
   * **Important Trap:** If **Move Inside Path** is enabled alongside static `NavMeshObstacle` elements blocking the walkway, pedestrians may become stuck between path boundaries and NavMesh walls. Either disable **Move Inside Path** for complex custom static obstacles or ensure adequate clearance around obstacles.

Parameters Reference
""""""""""""""""""""

**Steering Settings:**
	* **Steering Damping** : how fast steering force returns to zero for smooth direction changes.
	* **Side Bias Intensity** : artificial offset to break symmetry during head-on pedestrian encounters.
	* **Arrival Fade Dist** : distance to destination where avoidance forces fade out for precise stopping.
	* **Forward Momentum Weight** : weight for maintaining forward momentum (higher = tighter turns, lower = wider arcs).

**Detection Ranges:**
	* **Look Ahead Car** : detection distance for oncoming vehicles.
	* **Look Ahead Pedestrian** : static forward vision distance for detecting nearby pedestrians. Controls early steering reaction before physical contact (recommended 1.5–2.5 m).
	* **Effective Radius** : maximum grid query radius around the agent to ignore distant obstacles.
	* **Find Neighbors** : merges overlapping vehicle bounds (e.g. trucks with trailers or jams) into a single OBB.

**Margins (Skin):**
	* **Npc Radius** : physical radius of the pedestrian.
	* **Skin Car** : safety buffer distance around vehicles.
	* **Skin Pedestrian** : safety buffer distance between pedestrians.

**Force Intensities:**
	* **Force Intensity Car** : multiplier for steering force when avoiding vehicles.
	* **Force Intensity Pedestrian** : multiplier for steering force when avoiding pedestrians.
	* **Push Intensity Car** : physical pushback force applied upon contacting vehicle colliders.
	* **Push Intensity Pedestrian** : separation force preventing pedestrian overlapping.
	* **Push Damping** : decay rate for physical separation and push forces.

**Escape Logic:**
	* **Escape Multiplier** : lateral force multiplier when directly facing an obstacle center.
	* **Separation Buffer** : minimum distance threshold where physical separation push forces begin acting.

**Border Settings:**
	* **Move Inside Path** : constrains agents within sidewalk/path boundaries.
	* **Spring Multiplier** : spring stiffness coefficient for returning agents to the sidewalk.
	* **Apply Border Force** : enables stiff physical correction force when completely breaching sidewalk limits.
	* **Apply Crosswalk Offset** : dynamically expands movement path width on crosswalks.
	* **Crosswalk Offset** : additional path width offset added during crosswalk traversal.

**Car Avoidance Blend Weights:**
	* **Tangent Blend Weight** : weight of contour-sliding tangent vector parallel to vehicle edges (normal push weight derived as `1 - TangentBlendWeight`).

**Bumper Fade Out Settings:**
	* **Bumper Offset** : virtual extension of car length in meters before releasing avoidance control.
	* **Bumper Fade Length** : distance over which avoidance force decays after clearing the bumper zone.

**Global Force Limits:**
	* **Max Push Force** : maximum capped repulsion/push force.
	* **Max Steering Force** : maximum capped steering avoidance force.
	* **Min Collision Speed** : minimum speed threshold used for collision impulse calculations against cars.

**NavMesh Agent Settings (for Crowd Avoidance NavMesh):**
	* **Avoid Navmesh Obstacles** : enables static NavMesh wall and edge avoidance.
	* **Look Ahead Navmesh** : raycast distance along movement direction for wall detection.
	* **Force Intensity Navmesh** : steering force intensity multiplier when NavMesh walls are detected.
	* **Extents** : search box extents used for NavMeshQuery agent positioning.
	* **Nav Agent Index** : NavMesh Agent Type ID.
	* **Area Mask** : bitmask specifying valid NavMesh area types.
	* **Wall Weight** : weight of perpendicular outward wall repulsion.
	* **By Pass Weight** : weight of parallel wall-sliding bypass force.
	* **Nav Mesh Side Padding** : extra side padding offset for left/right raycasts during wall detection.

.. _pedestrianAntistuckConfig:

Antistuck Config
~~~~~~~~~~~~~~~~

Anti-stuck config for pedestrians stuck in a collision.

	.. image:: /images/configs/pedestrian/PedestrianAntistuckConfig.png
	``Hub/Configs/PedestrianConfigs/AntistuckConfig``
	
| **Antistuck enabled** : on/off anti-stuck feature (if disabled, previous target will be selected).
| **Target direction dot** : direction between pedestrian's forward vector and the anti-stuck point.
| **Achieve distance** : achieve distance to the anti-stuck target point.
| **Target point offset** : distance between collision and anti-stuck point.
	
Trigger Config
~~~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianTriggerConfig.png
	``Hub/Configs/PedestrianConfigs/TriggerConfigs/PedestrianCommonTriggerConfig``
	
| **Trigger HashMap capacity** : initial HashMap capacity that contains trigger data.
| **Trigger HashMap cell size** : HashMap cell size.
**Trigger data:**
	* **Fear Point Trigger** :
		* **Impact trigger duration** : duration of the :ref:`trigger<pedestrianScaryTrigger>` on the pedestrian.

.. _pedestrianScaryTrigger:

Scary Trigger Config
~~~~~~~~~~~~~~~~~~~~

	.. image:: /images/configs/pedestrian/PedestrianScaryTriggerConfig.png
	``Hub/Configs/PedestrianConfigs/TriggerConfigs/PedestrianScaryTriggerConfigAuthoring``
	
Trigger settings
""""""""""""""""

| **Death trigger squared distance** : death trigger squared distance (squared distance == distance * distance).
| **Death trigger duration** : death trigger duration.
		
Sound settings
""""""""""""""

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
| **Idle after achieved exit duration** : idle duration after reaching the exit point.
| **Sitting movement speed** : pedestrian movement speed when sitting on the bench.
| **Sitting rotation speed** : pedestrian turn speed when sitting on the bench.
| **Custom achieve sit point distance** : distance to achieve the sit point on the bench.
	
Common Sound Config
~~~~~~~~~~~~~~~~~~~

Common pedestrian sound settings.

	.. image:: /images/configs/pedestrian/PedestrianCommonSoundConfig.png
	``Hub/Configs/PedestrianConfigs/SoundConfig``
	
| **Sound death** : :ref:`sound<soundData>` when a pedestrian dies.
| **Enter tram sound** : :ref:`sound<soundData>` when entering a tram.
| **Exit tram sound** : :ref:`sound<soundData>` when exiting a tram.


.. _pedestrianStateAuthoring:

State Authoring
~~~~~~~~~~~~~~~
	
State Dictionary
""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring1.png
	``Hub/Configs/PedestrianConfigs/PedestrianStateAuthoring``

| **Next states** : which :ref:`states <pedestrianActionState>` can override the current :ref:`state <pedestrianActionState>`.

**State type:** 
	* **Default** : state processed by the `PedestrianStateSystem` system (processing code should be located in `PedestrianStateSystem.cs:144`).
	* **External system** : state processed by an external system (processing code should be in a separate system).
	* **Additive** : additive state flag adds to the current state and is processed by the `External system`.
	* **Additive any** : additive state flag adds to the current state, is processed by the `External system`, and ignores available next state flags.

.. _pedestrianStateBinding:

Movement State Binding Dictionary
"""""""""""""""""""""""""""""""""

	.. image:: /images/configs/pedestrian/PedestrianStateAuthoring2.png
	``Hub/Configs/PedestrianConfigs/PedestrianStateAuthoring``

Contains data mapping which :ref:`Movement state <pedestrianMovementState>` is assigned after an :ref:`Action state <pedestrianActionState>` is set.
	
	.. note:: 
		* Read more about :ref:`state info <pedestrianStates>` & :ref:`available states <pedestrianActionState>`.