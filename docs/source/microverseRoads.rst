.. _mvr:

MicroVerse Roads
============

How To Use
------------

#. Buy & download, import the following asset plugins:

	`MicroVerse - Core Collection <https://assetstore.unity.com/packages/tools/terrain/microverse-core-collection-232976>`_ or (`MicroVerse <https://assetstore.unity.com/packages/tools/terrain/microverse-232972>`_ & `MicroVerse - Splines <https://assetstore.unity.com/packages/tools/terrain/microverse-splines-232974>`_)
	`MicroVerse - Roads <https://assetstore.unity.com/packages/tools/terrain/microverse-roads-208590>`_

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
		
#. Generate a :ref:`subscene <subscene>`.
#. If you want to regenerate roads, press `Move back` button in the :ref:`Hub <hub>` & regenerate roads in `MVR_Generator` & generate subscene in the :ref:`Hub <hub>` again.

