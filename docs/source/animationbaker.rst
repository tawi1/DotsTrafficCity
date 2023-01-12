.. _animationBaker:

Animation Baker
=====

.. _animationBakerHowTo:

How To Bake
------------

	#. Open baker in the unity toolbar.
	
		``Spirit604/Animation Baker``
		
	#. Customize texture :ref:`settings <animationBakerSettings>`.
	#. Drag & drop selected `SkinnedMeshRenderer` of pedestrians to `skins` :ref:`field <animationBakedSourceData>`.
	#. Drag & drop selected animations of pedestrians to `clips` :ref:`field <animationBakedSourceData>`.
	
		.. image:: images/pedestrian/baker/window/BakedSourceDataExample.png
		`Drag example.`
		
	#. Press `Create new` button.
	
		.. image:: images/pedestrian/baker/window/BakedSourceDataResult.png
		`Multiple animation result example.`
		
	#. Check the created `BakedAnimationData` result in the tab :ref:`BakedAnimationData <animationBakedAnimationData>`.
	
		.. image:: images/pedestrian/baker/window/BakedAnimationDataExample.png
		`AnimationData result example.`
		
Baker Window
------------

.. _animationBakerSettings:

Settings
~~~~~~~~~~~~

	.. image:: images/pedestrian/baker/window/Settings.png
	
| **Frame rate** : frame rate of baked animation.
**Round to size ratio:** rounding texture size.
	* **X texture size ratio** : by X-axis.
	* **Y texture size ratio** : by Y-axis.
**Output type:**
	* **Baked animation data**
	* **Texture**
| **Baked animation data** : :ref:`data <animationBakedAnimationData>` about baked animations in texture.
	
.. _animationBakedSourceData:

Baked Source Data
~~~~~~~~~~~~

	.. image:: images/pedestrian/baker/window/BakedSourceDataExample.png
	.. image:: images/pedestrian/baker/window/BakedSourceDataResult.png
	
| **Skins** : source `SkinnedMeshRenderer` of characters.
**Clips:**
	* **Clip** : reference to clip.
	* **Offset** : offset vertices in baked animation.
	* **Custom animation name** : custom animation name (if the field is empty the name from the clip will be taken).
| **Texture data** : shows a preview of the created texture.
	* **x** : animation frame vertex coordinate.
	* **y** : number of vertexes in the skin.
	
	.. note::
		**Texture [882x1588]:**
			* Texture has 882 animation frames.
			* Skin size 1588 vertices.
	
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
	
Baked Animation Data
~~~~~~~~~~~~

	.. image:: images/pedestrian/baker/window/BakedAnimationDataExample.png
		
| **Sampling skin** : skin on the basis of a playback animation (for :ref:`replace <animationBakedAnimationDataReplace>` purposes only).
**Animation data:**
	* **Source mesh** : source mesh of character.
	* **Source anim** : source animation clip.
	* **New anim** : new animation for :ref:`replace <animationBakedAnimationDataReplace>` source animation.
	* **Animation name** : the name of the animation that will be displayed in :ref:`Baked Animation Sheet Data <animationBakerAnimationSheetData>`.
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
	
	.. image:: images/pedestrian/baker/window/BakedAnimationDataReplaceExample.png
	`Replace example.`
	
	
Custom Baked Animator
------------

Baked Custom animator is used for transitions between baked animations.
	
How To
~~~~~~~~~~~~

Open
""""""""""""""

Open on the scene `PedestrianBakedAnimatorAuthoring`.

	``Hub/Configs/BakerRefs/Settings/PedestrianBakedAnimatorAuthoring``
		
	.. image:: images/pedestrian/baker/animator/PedestrianBakedAnimatorAuthoring.png

Create Node
""""""""""""""

Right-click in the window and select the :ref:`desired node<animationBakerAnimatorNodeTypes>` in the context menu.

Create Sequence
""""""""""""""
	
Create a sequence of nodes StartNode-->AnimNode-->TransitionNode-->AnimNode-->TransitionNode-->AnimNode-->... (:ref:`more detailed example <animationBakerHowToCreateTransition>`).
	
	
Create Transition Layer
""""""""""""""

Press `+` button on the main toolbar at custom animator to create a new layer or press `-` to delete current selected layer.

.. _animationBakerAnimatorNodeTypes:

Node types
~~~~~~~~~~~~

.. _animationBakerAnimatorStartNode:

Start Node
""""""""""""""

Node where the transition begins by trigger.

	.. image:: images/pedestrian/baker/animator/StartNodeExample.png	
		
| **Trigger name** : name of the trigger on which the transition starts.

.. _animationBakerAnimatorAnimationNode:

Animation Node
""""""""""""""

Animation playback node.

	.. image:: images/pedestrian/baker/animator/AnimationNodeExample.png

| **Asset name** : asset data name.
| **Anim name** : animation name (by default is taken from `Anim enum`).
| **Anim enum** : list of available animations in the :ref:`Animation Collection <animationBakerAnimationCollection>`
| **Unique animation** : unique animation mesh instance will be created for this animation.

.. _animationBakerAnimatorTransitionNode:

Transition Node
""""""""""""""

Node with settings for switching between animations.

**Node Type:**

	* **Default** : animations play sequentially one by one without interpolation.
		.. image:: images/pedestrian/baker/animator/TransitionNodeDefaultExample.png	
		
	* **To Start** : previous animation is interpolated to the beginning of the next animation with the set duration.
		.. image:: images/pedestrian/baker/animator/TransitionNodeToStartExample.png
		
	* **To Global Sync** : previous animation is interpolated to the global playback time of the next animation with the set duration.
		.. image:: images/pedestrian/baker/animator/TransitionNodeToGlobalSyncExample.png

	.. image:: images/pedestrian/baker/animator/StartSitTransitionExample.png
	`Start sit transition example.`
		
	.. image:: images/pedestrian/baker/animator/SitoutTransitionExample.png		
	`Sitout transition example.`

.. _animationBakerAnimationCollection:

Animation Collection
------------

Contains meta-data of existing animations for the pedestrians.

How To Create
~~~~~~~~~~~~

In the project context menu:
	
	``Spirit604/Animation Baker/Animation Collection``

Settings
~~~~~~~~~~~~
	
	.. image:: images/pedestrian/baker/animator/AnimationCollectionExample.png


| **Name** : animation name.
**Unique animation** : unique animation mesh instance pool will be created for this animation.
	* **Allow duplicate** : is it allowed to take an animation from the pool if it is already used by another character.
	* **Instance count** : animation pool size.

.. _animationBakerAnimatorContainer:

Animator Container
------------

Contains data about animation transitions.

	.. image:: images/pedestrian/baker/animator/AnimatorContainerExampleSource.png
	
**Layer Data** : contains data about transition.
	* **Entry node** : asset node where the transition begins.
	* **Activate trigger** : name of the transition activation trigger.
	* **Activate trigger hash** : hash of the transition activation trigger.
	* **All nodes** : all transition nodes.