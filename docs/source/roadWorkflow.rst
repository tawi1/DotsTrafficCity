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
#. In the :ref:`Road Parent <roadParentInfo>`, press the `Force connect` button if you have created :ref:`new segments <roadSegmentCreator>` (make sure all segments are :ref:`on one line <trafficNodeConnectionInfo>`) or create paths between segments with :ref:`Path creator <pathCreator>`.
#. Then, in the :ref:`Road Parent <roadParentInfo>`, press the :ref:`Bake path data <bakingInfo>` button to bake & validate the road.
#. If the console shows any errors related to the road, use the :ref:`TrafficObjectFinder <trafficObjectFinder>` tool to find broken road objects & fix them according to the message.
#. Click `Generate` button in the :ref:`Entity Subscene Generator <subsceneGenerator>`.

	.. note:: By default, the config from the :ref:`main scene <mainScene>` is copied to the :ref:`subscene <subscene>` when :ref:`subscene <subscene>` generation is repeated.
