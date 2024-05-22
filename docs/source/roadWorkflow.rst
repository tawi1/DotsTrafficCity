.. _workflow:

Workflow
============

.. _roadEdit:

Road Editing
----------------

Any change of road can take a while if it is done in a :ref:`subscene <subscene>`, so make changes to the road in the :ref:`main scene <mainScene>` for `Editor` performance reasons:

Steps
~~~~~~~~~~~~

#. Open the :ref:`Hub <hub>` in the scene.
#. Select the :ref:`Entity Subscene Generator <subsceneGenerator>`.
#. Click `Move Back` button to move road from subscene to main scene.
#. Make any change in the road.
#. :ref:`Bake <bakingInfo>` the road.
#. Click `Generate` button in the :ref:`Entity Subscene Generator <subsceneGenerator>`.

	.. note:: By default, the config from the :ref:`main scene <mainScene>` is copied to the :ref:`subscene <subscene>` when :ref:`subscene <subscene>` generation is repeated.
