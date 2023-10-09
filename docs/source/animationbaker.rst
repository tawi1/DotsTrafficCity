.. _animationBaker:

Animation Baker
=====

.. contents::
   :local:


.. _animationBakerHowTo:

How To Bake
------------

	#. Open baker in the unity toolbar.
	
		``Spirit604/Animation Baker``
		
	#. Customize texture :ref:`settings <animationBakerSettings>`.
	#. Drag & drop selected `SkinnedMeshRenderer` of pedestrians to `skins` :ref:`field <animationBakedSourceData>`.
	#. Drag & drop selected animations of pedestrians to `clips` :ref:`field <animationBakedSourceData>`.
	
		.. image:: /images/pedestrian/baker/window/BakedSourceDataExample.png
		`Drag & drop example.`
		
	#. Press `Create new` button.
	
		.. image:: /images/pedestrian/baker/window/BakedSourceDataResult.png
		`Multiple animation result example.`
		
	#. Check the created `BakedAnimationData` result in the tab :ref:`BakedAnimationData <animationBakedAnimationData>`.
	
		.. image:: /images/pedestrian/baker/window/BakedAnimationDataExample.png
		`AnimationData result example.`
		
Baker Window
------------

.. _animationBakerSettings:

Settings
~~~~~~~~~~~~

	.. image:: /images/pedestrian/baker/window/Settings.png
	
| **Animation material base** : base animation material.
| **Frame rate** : frame rate of baked animation.
| **Make squared texture** : rounding texture size.
| **Add normal texture** : add normal texture.

**Compression type:**
	* **Uncompressed** : uncompressed format of baked texture.
	* **Compressed** : compressed format of baked texture. **[currently not available]**

**Texture bake type:**
	* **Single texture** : bake all characters to single texture.
	* **Multiple textures** : bake each character to unique texture.
	
| **Clip data template path** : path to clip templates.
| **Save texture data path** : creating path of :ref:`texture animation data <animationBakedAnimationData>`.
| **Save texture path** : creating path of baked textures.
| **Created texture data** : :ref:`data <animationBakedAnimationData>` about baked animations in texture.
	
.. _animationBakedSourceData:

Source Data
~~~~~~~~~~~~

	.. image:: /images/pedestrian/baker/window/SourceDataExample.png
	.. image:: /images/pedestrian/baker/window/SourceDataResult.png
	
Data
""""""""""""""

| **Skins** : source `SkinnedMeshRenderer` of characters.

**Clips:**
	* **Clip** : reference to clip.
	* **Offset** : local offset of vertices in baked animation.
	* **Custom animation name** : custom animation name (if the field is empty the name from the clip will be taken).
	* **Preview** : on/off preview playback of baked animation (make sure the texture is created and any character is selected in the toolbar).
	
**Texture data** : shows a preview of the created texture.
	* **x** : animation frame vertex coordinate.
	* **y** : number of vertexes in the skin.
	
	.. note::
		**Texture [2008x1287]:**
			* Texture has 2008 animation frames.
			* Max skin size 1287 vertices.
	
	.. tip:: Texture rounding to the POT4 format is used for texture compression (256x256, 256х512, 512x512, etc...).
	
Buttons
""""""""""""""

| **Create new** : create a new texture.
| **Add to exist texture** : adds new animations to an existing texture.
| **Resize texture** : texture resizing according to rounding parameters.
| **Save as new** : save the texture as a new asset.
| **Save to exist** : save the texture to an existing asset.
| **Clear** : clean up the texture.
	
.. _animationBakedAnimationData:
	
Animation Texture Data
~~~~~~~~~~~~

	.. image:: /images/pedestrian/baker/window/AnimationDataExample.png
		
| **Sampling skin** : skin on the basis of a playback animation (for :ref:`replace <animationBakedAnimationDataReplace>` purposes only).

**Animation data:**
	* **Source mesh** : source mesh of character.
	* **Source anim** : source animation clip.
	* **New anim** : new animation for :ref:`replace <animationBakedAnimationDataReplace>` source animation.
	* **Animation name** : the name of the animation that will be displayed in :ref:`Baked Animation Sheet Data <animationTextureData>`.
	* **Frame rate** : frame rate of baked animation.
	* **Texture offset** : texture offset of baked animation.
	* **Frame count** : frame count of baked animation.
	
.. _animationBakedAnimationDataReplace:

How To Replace
""""""""""""""

	#. Drag & drop target character prefab to the scene.
	#. Drag & drop `SkinnedMeshRenderer` of the target character from the scene to `Sampling skin` field.
	#. Drag & drop new animation clip to `New anim` field.
	#. Press `Replace` button.
	
	.. image:: /images/pedestrian/baker/window/AnimationDataReplaceExample.png
	`Replace example.`
	
	
Crowd GPU Animator
------------

Crowd GPU Animator is used for transitions between GPU animations.
	
How To
~~~~~~~~~~~~

Open
""""""""""""""

Open on the scene `CrowdGPUAnimatorAuthoring`.

	``Hub/Configs/BakerRefs/Settings/CrowdGPUAnimatorAuthoring``
		
	.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png
	
Initial Set Up
""""""""""""""

**Steps:**
	#. Create :ref:`Animator Data Container <animationGPUAnimatorContainer>` in the project context menu and assign to custom animator (if necessary).
	#. Create (if necessary) and assign :ref:`Animation Collection <animationGPUAnimationCollection>` the same as in the :ref:`PedestrianCrowdSkinFactory <pedestrianCrowdSkinFactory>`.

	.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png
	
Create Node
""""""""""""""

Right-click in the window and select the :ref:`desired node<animationBakerAnimatorNodeTypes>` in the context menu.

Create Transition
""""""""""""""
	
Transition is a sequential set of nodes StartNode-->AnimNode-->TransitionNode-->AnimNode-->TransitionNode-->AnimNode-->... (:ref:`example <animationBakerAnimatorTransitionExample>`).
	
**Steps:**
	#. Create :ref:`new transition layer <animationBakerAnimatorNewTransitionLayer>` (if needed).
	#. Enter the name of the trigger in the :ref:`StartNode <animationBakerAnimatorStartNode>`.
	#. Create and connect :ref:`AnimationNode <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
.. _animationBakerAnimatorNewTransitionLayer:

Create Transition Layer
""""""""""""""

Press `+` button on the main toolbar at custom animator to create a new layer or press `-` to delete current selected layer.

.. _animationBakerAnimatorNodeTypes:

Graph Nodes
~~~~~~~~~~~~

.. _animationBakerAnimatorStartNode:

Start Node
""""""""""""""

Node where the transition begins by trigger.

	.. image:: /images/pedestrian/baker/animator/StartNodeExample.png	
		
| **Trigger name** : name of the trigger on which the transition starts.
| **Hash** : hash of the trigger on which the transition starts.

.. _animationBakerAnimatorTriggerHash:

	.. note:: Hash from trigger name generated by Unity method `Animator.StringToHash <https://docs.unity3d.com/ScriptReference/Animator.StringToHash.html>`_  

.. _animationBakerAnimatorAnimationNode:

Animation Node
""""""""""""""

Animation playback node.

	.. image:: /images/pedestrian/baker/animator/AnimationNodeExample.png

| **Asset name** : asset data name.
| **Anim name** : animation name (by default is taken from `Anim enum`).
| **Anim enum** : list of available animations in the :ref:`Animation Collection <animationGPUAnimationCollection>`
| **Unique animation** : unique animation mesh instance will be created for this animation.

.. _animationBakerAnimatorTransitionNode:

Transition Node
""""""""""""""

Node with settings for switching between animations.

**Node Type:**

	* **Default** : animations play sequentially one by one without interpolation.
		.. image:: /images/pedestrian/baker/animator/TransitionNodeDefaultExample.png	
		
	* **To Start** : previous animation is interpolated to the beginning of the next animation with the set duration.
		.. image:: /images/pedestrian/baker/animator/TransitionNodeToStartExample.png
		
	* **To Global Sync** : previous animation is interpolated to the global playback time of the next animation with the set duration.
		.. image:: /images/pedestrian/baker/animator/TransitionNodeToGlobalSyncExample.png


.. _animationBakerAnimatorTransitionExample:

Transition example
""""""""""""""

	.. image:: /images/pedestrian/baker/animator/StartSitTransitionExample.png
	`Start sit transition example.`
		
	.. image:: /images/pedestrian/baker/animator/SitoutTransitionExample.png		
	`Sitout transition example.`

.. _animationGPUAnimationCollection:

Animation Collection
------------

Contains meta-data of existing animations for the pedestrians.

How To Create
~~~~~~~~~~~~

In the project context menu:
	
	``Spirit604/Animation Baker/Animation Collection``

Settings
~~~~~~~~~~~~
	
	.. image:: /images/pedestrian/baker/animator/AnimationCollectionExample.png


| **Name** : animation name.
**Unique animation** : unique animation mesh instance pool will be created for this animation.
	* **Allow duplicate** : is it allowed to take an animation from the pool if it is already used by another character.
	* **Instance count** : animation pool size.

.. _animationGPUAnimatorContainer:

Animator Data Container
------------

Contains data about animation transitions.

	.. image:: /images/pedestrian/baker/animator/AnimatorContainerExampleSource.png
	
**Layer Data** : contains data about transition.
	* **Entry node** : asset node where the transition begins.
	* **Activate trigger** : name of the transition activation trigger.
	* **Activate trigger hash** : hash of the transition activation trigger.
	* **All nodes** : all transition nodes.