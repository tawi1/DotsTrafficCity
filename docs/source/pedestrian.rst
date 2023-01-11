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

.. _pedestrianBaked:

Baked skin
~~~~~~~~~~~~

`Baked skin` is a :ref:`pure entity <pureEntity>` that combines the GPU baked animations and the DOTS entity.

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
	
Transitions
""""""""""""""

How To Use
""""""""""""""

.. _pedestrianRagdoll:

Ragdoll
~~~~~~~~~~~~

`RagdollWizard <https://docs.unity3d.com/2021.1/Documentation/Manual/wizard-RagdollWizard.html>`_

Authoring components
----------------

States
----------------

Movement State

.. _pedestrianActionState:

Pedestrian Action State


Configs
----------------