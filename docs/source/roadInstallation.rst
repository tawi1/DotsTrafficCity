.. _roadInstallation:

Installation
=====

Traffic Road Installation
----------------

#. Create initial :ref:`scene <cityCreation>` objects.
#. Create required :ref:`RoadSegments <roadSegment>`. And add them to the :ref:`RoadParent <roadParent>` as children.
#. Create the :ref:`necessary paths <trafficNodePathCreator>`. 
#. Configure :ref:`paths <path>`. 
#. Create required :ref:`PedestrianNode <pedestrianNode>` by :ref:`PedestrianNodeCreator <pedestrianNodeCreator>`.
#. Adjust the :ref:`Traffic lights <trafficLight>`.
#. Create the :ref:`Traffic Areas <trafficArea>` **[optional step]**.
#. Create the :ref:`Public Routes <trafficPublicRoute>` **[optional step]**.
#. Open `RoadParent`.
	
	.. _roadParent:

	.. image:: /images/road/installation/RoadParent.png

#. Press `Reset` button to reset the :ref:`automatically created paths <trafficNodeAutoPathConnection>`.
#. Press `Connect` button to connect segments (make sure all segments are :ref:`on one line <trafficNodeConnectionInfo>`).
#. Press `Bake` button (:ref:`bake info <bakingInfo>`).
#. Create :ref:`subscene <roadEntitySubscene>` **(one-time procedure)**.
#. Read more about :ref:`road <roadEdit>` & :ref:`config <configEdit>` editing workflow.

.. _roadEntitySubscene:

Entity Subscene Creation
----------------
	
From version `DOTS 1.0 <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/index.html>`_ , all entity conversions must be done via subscenes. It's necessary to create a separate :ref:`subscene <subscene>` for roads.

	.. image:: /images/road/installation/Hub.png
	
Steps:
	#. Select :ref:`Hub <hub>` on the scene.
	#. Select `Entity sub scene path` the path to create a `subscene`.
	#. Enter `Entity subscene name` or use default name.
	#. On/off autosync configs (before migrating the configs to the `subscene`, they will be synchronized with the configs that are in the `Hub`).
	#. Press `Generate` button.
	#. All created :ref:`RoadSegments <roadSegment>` and :ref:`PedestrianNodes <pedestrianNode>` will automatically be moved to the :ref:`subscene <subscene>`.

	
