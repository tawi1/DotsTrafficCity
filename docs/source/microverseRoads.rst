.. _mvr:

MicroVerse Roads
============

How To Use
------------

#. Buy & download, import the following asset plugins:

	* `MicroVerse - Core Collection <https://assetstore.unity.com/packages/tools/terrain/microverse-core-collection-232976>`_ or (`MicroVerse <https://assetstore.unity.com/packages/tools/terrain/microverse-232972>`_ & `MicroVerse - Splines <https://assetstore.unity.com/packages/tools/terrain/microverse-splines-232974>`_)
	* `MicroVerse - Roads <https://assetstore.unity.com/packages/tools/terrain/microverse-roads-208590>`_

Getting Started
------------

#. Unpack microverse prefab package:

	.. image:: /images/integration/mvr1.png

#. Open `Roads Demo` or your scene.
#. Create :ref:`City base <cityCreation>`.
#. Create a new gameobject & add `MVR_Generator` component.
#. Assign `MVR config` & `config` from the list. 

	.. image:: /images/integration/mvr2.png
	
#. Customize all settings according to your needs.
#. Press `Generate` button
#. View a `Generated data`, fix any problems if this tab has them & generate again.

	.. image:: /images/integration/mvr3.png
	`Result example.`
		
#. If you have `Not found` road objects in the `Inspector` and are using your own microverse road objects, use ``MVR UserPrefab`` to add the prefabs in ``MVR Config`` if your prefab is repeatable and not unique or use ``MVR UserSceneSegment`` if you have a unique road segment for a road object. After adding these components, regenerate the scene.
#. Generate a :ref:`subscene <subscene>`.
#. If you want to regenerate roads, press `Move back` button in the :ref:`Hub <hub>` & regenerate roads in `MVR_Generator` & generate subscene in the :ref:`Hub <hub>` again.

MVR UserPrefab
------------

This component helps users conveniently add prefabs to the MVR config.

How To Use
~~~~~~~~~~~~

* Create a road segment in the scene where you want your custom intersection.
* Add your segment to prefabs.
* Add ``MVR_UserPrefab`` component.
* Select the `Intersection` in the scene by pressing the `Select` button.
* Press `Add Prefab` button in the inspector.
* Now, your prefab addded to MVR config & you can regenerate the scene.

MVR UserSceneSegment
------------

This component prevents the road segment from being cleaned up during regeneration, useful for unique road objects.

How To Use
~~~~~~~~~~~~

* Create a road segment in the scene where you want your custom intersection.
* Add ``MVR_UserSceneSegment`` component.
* In the inspector, press `Sync Position` to synchronize the intersection and segment positions.
