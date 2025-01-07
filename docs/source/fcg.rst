.. _fcg:

Fantastic City Generator
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`Fantastic City Generator <https://assetstore.unity.com/packages/3d/environments/urban/fantastic-city-generator-157625>`_

Getting Started
------------

#. Open your scene.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`
	
#. Create a new game object & add `FCG_SceneGenerator` component.

#. Generate a new config:

	.. image:: /images/integration/fcg1.png

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Find the `HybridTrafficCarMonoSkinBase Arcade` prefab & set the ground layer to `Default`.
#. Select type.

Editor Mode
------------

Road segment editor generation from FCG raw data.

#. Configure generator settings.
#. Press `Generate` button.
#. Edit road segments in the scene as needed.

Editor Blocks
------------

#. Select `Runtime Blocks` type.
#. Generate blocks like in `Runtime blocks` tutorial.
#. Switch back to `Editor Blocks` type.
#. Press the `Generate` button after each city generation using `FCG`.

Runtime Blocks
------------

Runtime chunk generation from `FCG` prefab blocks, can also be used to generate blocks for `Editor blocks`.

#. Select `Runtime Blocks` type.
#. Drag & drop `FCG` road block into the field.

	.. image:: /images/integration/fcg3.png
	
#. Generate FCG prefab container.
	
	.. image:: /images/integration/fcg2.png

#. Configure generator settings.
#. Press `Generate` button.
#. Some of the prefab blocks should be edited because the FCG plugin doesn't have enough data to complete the generation, for example, let's open the `Border-Flat-Large-Exit` prefab.
#. Roundabout here without exit segment:

	.. image:: /images/integration/fcg4.png
	
#. Create a :ref:`Custom road segment <roadSegmentCreatorCustomSegment>` & connect with others with :ref:`Path Creator <pathCreator>` tool. :ref:`Pedestrian nodes <pedestrianNode>` select & connect with `Tab` hotkey.

	.. image:: /images/integration/fcg5.png
	`Result`
	
#. Now need to bind local block to share the result with the same blocks.
#. Select generated `FCG prefab container`.

	.. image:: /images/integration/fcg5_2.png
	
#. Tick on `Show scene binding` option.
#. Select local block in the prefab stage on the scene.

	.. image:: /images/integration/fcg6.png
	`Example`

#. Inspector example:

	.. image:: /images/integration/fcg7.png
	`Example`
	
#. Press `Create block prefab` button.

	.. image:: /images/integration/fcg7.png
	`Result`
	
#. Now when you regenerate blocks in `FCG Scene Generator`, the local block will be replaced with the previously generated prefab block.
