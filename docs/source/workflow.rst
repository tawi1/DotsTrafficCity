.. _workflow:

Workflow
============

.. _roadEdit:

Road Editing
----------------

Any change of road can take a while if it is done in a :ref:`subscene <subscene>`, so make changes to the road in the :ref:`main scene <mainScene>` for `Editor` performance reasons:

Steps
~~~~~~~~~~~~

#. Open the :ref:`Hub <hub>` on the scene.
#. Select the :ref:`Entity Subscene Generator <subsceneGenerator>`.
#. Click `Move Back` button to move road from subscene to main scene.
#. Make any change in the road.
#. :ref:`Bake <bakingInfo>` the road.
#. Click `Generate` button in the :ref:`Entity Subscene Generator <subsceneGenerator>`.

.. _configEdit:

Config Editing
----------------

There are 2 variants to edit configs:

Main Scene Editing
~~~~~~~~~~~~

	.. image:: /images/road/installation/MainSceneExample.png

Steps
""""""""""""""

#. Select :ref:`Hub <hub>` on the scene.
#. After editing any config in the main scene :ref:`Hub <subsceneGenerator>` press `Copy To Subscene` button.
	
	.. image:: /images/road/installation/Hub.png
	
Directional Editing
~~~~~~~~~~~~

	.. image:: /images/road/installation/EntitySubSceneExample.png
	
Steps
""""""""""""""

#. Open the `EntitySubScene` :ref:`subscene <subscene>`.
#. Edit any config.
#. Save & close :ref:`subscene <subscene>`.