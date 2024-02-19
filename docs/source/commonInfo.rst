.. _commonInfo:

Common Info
=====

.. contents::
   :local:

Hybrid Entities
-------------------

Entities that combine `DOTS` entities and default `GameObjects` (game objects are tied by position to an entity).

How To Create
~~~~~~~~~~~~

#. Create a prefab entity through the `baking <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/baking.html>`_.
#. Add the ``CopyTransformToGameObject`` component and add your custom init component to the `baking <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/baking.html>`_ process for initialization, pseudocode example:

	..  code-block:: r
	
		public struct InitComponentExample : IComponentData, IEnableableComponent
		{		  
		}
		
#. Spawn a prefab entity at runtime.
#. Create your own init system to initialize your hybrid entity, pseudocode example:

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
				.WithStructuralChanges()
				.WithAll<InitComponentExample>()
				.ForEach((
					Entity entity) =>
				{
					var exampleObject = exampleFactory.Get();
					
					//Bind transform to entity
					EntityManager.AddComponentObject(entity, exampleObject.transform); 
					
					//Add required component if missing
					commandBuffer.AddComponent<CopyTransformToGameObject>(entity); 
					
					//Disable init component
					commandBuffer.SetComponentEnabled<InitComponentExample>(entity, false); 
				
				}).Run();
				
				entityCommandBufferSystem.AddJobHandleForProducer(Dependency);
			}
			
			//Some factory that is assigned from outside
			
			public void Initialize (ExampleFactory exampleFactory)
			{
				this.exampleFactory = exampleFactory; 
			}		
		}
		
	.. warning:: All code provided in the example is not part of `DOTS City` and is not intended for production.

.. _propsInfo:

Props
-------------------

Props are active entities that react to damage.

How To Use
~~~~~~~~~~~~

#. Create props prefab.
#. Add :ref:`Props Authoring <propsAuthoring>` component.
#. Tick if necessary `Has Custom Prop Reset`.
#. Make sure that :ref:`Props damage system support <propsDamageOption>` option is enabled.
#. Use a :ref:`test scene <propsTestScene>` to check that the props work.

.. _propsAuthoring:

Props Authoring
~~~~~~~~~~~~


	.. image:: /images/other/PropsAuthoring.png
	
| **Has custom prop reset** : if checked, a custom reset system must be implemented for this object that contains `PropsCustomResetTag` component.

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