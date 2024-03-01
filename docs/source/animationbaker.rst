.. _animationBaker:

Animation Baker
=====

.. contents::
   :local:


.. _animationBakerHowTo:

How To Bake
------------

	#. Open `Baker` from the `Unity` toolbar.
	
		``Spirit604/Animation Baker``
		
	#. Customize texture :ref:`settings <animationBakerSettings>`.
	#. Drag & drop selected `SkinnedMeshRenderer` of pedestrians into `Skins` :ref:`field <animationBakedSourceData>`.
	#. Drag & drop selected animations of pedestrians into the `Clips` :ref:`field <animationBakedSourceData>`.
	
		.. image:: /images/pedestrian/baker/window/SourceDataExample.png
		`Drag & drop example.`
		
	#. Press the `Create new` button.
	
		.. image:: /images/pedestrian/baker/window/SourceDataResult1.png
		`Multiple animation result example.`
		
	#. In the tab :ref:`Animation Texture Data <animationBakedAnimationData>` tab, check the `Animation Texture Data` result.
	
		.. image:: /images/pedestrian/baker/window/AnimationDataExample.png
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
	
.. _animationBakerToolbar:
	
Toolbar
""""""""""""""

	.. image:: /images/pedestrian/baker/window/Toolbar.png
	
| **Skins** : source `SkinnedMeshRenderer` of characters.
| **Skin toolbar** : character selection toolbar for selecting preview animation.
	
Clip Data
""""""""""""""

	.. image:: /images/pedestrian/baker/window/ClipData.png

* **Clip** : reference to the clip.
* **Custom frame rate** : custom frame rate of the clip.
* **Interpolate** : on/off interpolation feature for the clip.
* **Offset** : local offset of vertices in baked animation.
* **Custom animation name** : custom animation name (if the field is empty the name from the clip will be taken).
* **Preview** : on/off preview playback of baked animation (make sure the texture is created and any character is selected in the :ref:`toolbar <animationBakerToolbar>`).
		
Texture Data
""""""""""""""

Shows a preview of the created texture.

	.. image:: /images/pedestrian/baker/window/TextureData.png

**Texture size:** 
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

	#. Drag & drop the target character's `Prefab` into the scene.
	#. Drag & drop `SkinnedMeshRenderer` of the target character from the scene into the `Sampling Skin` field.
	#. Drag & drop the new animation clip into the `New anim` field.
	#. Press the `Replace` button.
	
	.. image:: /images/pedestrian/baker/window/AnimationDataReplaceExample.png
	`Replace example.`
	
	
Crowd GPU Animator
------------

The `Crowd GPU Animator` is used for transitions between GPU animations.
	
How To
~~~~~~~~~~~~

Open
""""""""""""""

Open in the scene `CrowdGPUAnimatorAuthoring`.

	``Hub/Configs/BakerRefs/Settings/CrowdGPUAnimatorAuthoring``
		
	.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png
	
Initial Set Up
""""""""""""""

**Steps:**
	#. Create an :ref:`Animator Data Container <animationGPUAnimatorContainer>` from the project context  and assign it to the custom animator (if necessary).
	#. Create (if necessary) and assign :ref:`Animation Collection <animationGPUAnimationCollection>` the same as in the :ref:`PedestrianCrowdSkinFactory <pedestrianCrowdSkinFactory>`.

	.. image:: /images/pedestrian/baker/animator/CrowdGPUAnimatorAuthoring.png
	
Create Node
""""""""""""""

Right-click in the window and select the :ref:`desired node<animationBakerAnimatorNodeTypes>` from the context menu.

Create Transition
""""""""""""""
	
Transition is a sequential set of nodes StartNode-->AnimNode-->TransitionNode-->AnimNode-->TransitionNode-->AnimNode-->... (:ref:`example <animationBakerAnimatorTransitionExample>`).
	
**Steps:**
	#. Create a :ref:`new transition layer <animationBakerAnimatorNewTransitionLayer>` (if required).
	#. Enter the name of the trigger in the :ref:`StartNode <animationBakerAnimatorStartNode>`.
	#. Create and connect :ref:`AnimationNodes <animationBakerAnimatorAnimationNode>` and :ref:`TransitionNodes <animationBakerAnimatorTransitionNode>`.
	
.. _animationBakerAnimatorNewTransitionLayer:

Create Transition Layer
""""""""""""""

Press the `+` button on the main toolbar at custom animator to create a new layer, or press `-` to delete the currently selected layer.

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
		
	* **To Start** : the previous animation is interpolated to the beginning of the next animation with the set duration.
		.. image:: /images/pedestrian/baker/animator/TransitionNodeToStartExample.png
		
	* **To Global Sync** : the previous animation is interpolated to the global playback time of the next animation with the set duration.
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

From the project context :
	
	``Spirit604/Animation Baker/Animation Collection``

Settings
~~~~~~~~~~~~
	
	.. image:: /images/pedestrian/baker/animator/AnimationCollectionExample.png


| **Name** : animation name.
**Unique animation** : a unique animation mesh instance pool will be created for this animation.
	* **Allow duplicate** : is it allowed to take an animation from the pool if it is already being used by another character.
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