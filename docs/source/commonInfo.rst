.. _commonInfo:

Common Info
=====

.. contents::
   :local:

.. _cullPointInfo:

Cullpoint Info
-------------------

The cull point is the point of origin for the surrounding entities (by default, it's a child of the camera). The :ref:`culling state <cullPointStates>` of the surrounding entities varies depending on the distance to the culling point (:ref:`example <cullPointExamples>`).
You can change the distances in the :ref:`cull config <cullConfig>`.

.. _cullPointStates:

States
~~~~~~~~~~~~

* **Culled** : entity is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity enabled but with limited or modified functionality for better performance.
* **InVisionOfCamera** : entity fully enabled.

Scene Streaming
-------------------

Road Streaming
~~~~~~~~~~~~

The current version of the project does not support streaming of road-related entities.

Content Streaming
~~~~~~~~~~~~

You can divide the scene content into chunks for partial loading at runtime.

How To Create
""""""""""""""

#. Create new empty `GameObject` and add :ref:`SubSceneCreator <subSceneCreator>` component. 
#. Customize :ref:`chunk settings <subSceneCreatorChunkSettings>`.
#. If necessary enable :ref:`post process settings <subSceneCreatorPostProcess>` **[optional step]**.
#. Press `Create` button.
#. Adjust :ref:`Streaming Level Config <streamingLevelConfig>` to load/unload subscenes in the runtime.

.. _subSceneCreator:

Sub Scene Creator
~~~~~~~~~~~~

Content chunking tool to split the scene into chunks. Old objects remain and disabled in the old scene and are used to create duplicates in the chunk sub-scenes.

	.. image:: /images/other/subSceneCreator.png
	
Assigments
""""""""""""""

| **Custom parent** : custom parent of subscene.
| **Scene name** : subscene template name.
| **Create path** : create subscenes path.

.. _subSceneCreatorChunkSettings:

Chunk Settings
""""""""""""""

| **Chunk size** : chunk size.

**Position source type** : source position of the object to be assigned to the chunk.
	* **Object position** 
	* **Mesh center** 
	
| **Destroy previous created** : destroy previously created chunks.

**Object find method** : method for finding an object to add to a chunk.
	* **By tag** : by unity tag.
	* **By layer** : by unity layer.
	
| **Target tag** : search tag.
| **Disable old source objects** : turn off the source objects.

**Disable source object type** 
	* **Mesh renderer** : disable meshRenderers of source objects.
	* **Parent** : disable parents of source objects.
	* **Parent if no mesh** : disable the meshRenderer, but if not, disable the parent.
	
| **Assign new layer** : assign new layer to objects created from new chunks.

.. _subSceneCreatorPostProcess:

Post Process Settings
""""""""""""""

| **Post process new object** : on/off post processing of the object.
| **Component type name** : target component name.

**Post process type:**
	* **Delete component** : the component found will be deleted.
	* **Delete object** : the object with the found component will be de.

Chunk Data
""""""""""""""

Buttons
""""""""""""""

| **Create** : create subscene chunks.
| **Enable/disable scene objects** : enable/disable source scene objects.
| **Enable/disable sub scene objects** : enable/disable created subscene objects.
| **Reset save path** : reset save path of the subscenes.
| **Clear** : clear created subscene chunks.

Hybrid Entities
-------------------

Entities that combine `DOTS` entities and default `GameObjects` (game objects are tied by position to an entity).

How To Create
~~~~~~~~~~~~

#. Create an entity through the `baking <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/baking.html>`_ .
#. Add ``CopyTransformToGameObject`` component and add your custom init component to the `baking <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/baking.html>`_ process for initialization, pseudo code example:

	..  code-block:: r
	
		public struct InitComponentExample : IComponentData, IEnableableComponent
		{		  
		}
		
#. Create your own init system to initialize your hybrid entity, pseudo code example:

	..  code-block:: r
	
		[UpdateInGroup(typeof(InitializationSystemGroup))]
		public partial class InitSystemExample : SystemBase
		{
			private ExampleFactory exampleFactory;			
			private EndInitializationEntityCommandBufferSystem entityCommandBufferSystem;

			protected override void OnCreate()
			{
				base.OnCreate();

				entityCommandBufferSystem = World.GetOrCreateSystemManaged<EndInitializationEntityCommandBufferSystem>();
			}

			protected override void OnUpdate()
			{
				var commandBuffer = entityCommandBufferSystem.CreateCommandBuffer();
				
				Entities
				.WithoutBurst()
				.WithAll<InitComponentExample>()
				.ForEach((
					Entity entity) =>
				{
					var exampleObject = exampleFactory.Get();
					
					EntityManager.AddComponentObject(entity, exampleObject.transform); //bind transform to entity
					
					commandBuffer.SetComponentEnabled<InitComponentExample>(entity, false); //disable init component
				
				}).Run();
				
				entityCommandBufferSystem.AddJobHandleForProducer(Dependency);
			}
			
			//some factory that is assigned from outside
			
			public void Initialize (ExampleFactory exampleFactory)
			{
				this.exampleFactory = exampleFactory; 
			}		
		}
		
	.. warning:: All code provided in the example is not part of `DOTS City` and is not for production.

.. _propsInfo:

Props
-------------------

Props are active entities that have a reaction to damage.

How To Use
~~~~~~~~~~~~

#. Create props prefab.
#. Add :ref:`Props Authoring <propsAuthoring>` component.
#. Tick if necessary `Has Custom Prop Reset`.
#. Make sure that :ref:`test scene example <propsDamageOption>` is enabled.
#. Use :ref:`test scene <propsTestScene>` to check that the props are working.

.. _propsAuthoring:

Props Authoring
~~~~~~~~~~~~


	.. image:: /images/other/PropsAuthoring.png
	
| Has custom prop reset : if enabled, a custom reset system must be implemented for this object that contains `PropsCustomResetTag` component.

Custom reset of hydrant, example code:

..  code-block:: r

	Entities
	.WithoutBurst()
	.WithAll<PropsCustomResetTag>()
	.WithAll<HydrantTag>()
	.ForEach((
		Entity entity,
		ref PropsVFXData propsVFXData) =>
	{
		if (propsVFXData.RelatedEntity != Entity.Null)
		{
			var particleSystem = EntityManager.GetComponentObject<ParticleSystem>(propsVFXData.RelatedEntity);
			particleSystem.Stop();
			particleSystem.gameObject.ReturnToPool();
	
			commandBuffer1.DestroyEntity(propsVFXData.RelatedEntity);
			propsVFXData.RelatedEntity = Entity.Null;
		}
	
		commandBuffer.SetComponentEnabled<PropsCustomResetTag>(entity, false);
		commandBuffer.SetComponentEnabled<PropsDamagedTag>(entity, false);
	
	}).Run();