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

How To Use
~~~~~~~~~~~~


Hybrid Entities
-------------------

How To Create
~~~~~~~~~~~~

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

Custom reset of hydrants, example code:

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