.. _roadInstallation:

Installation
=====

Traffic Road Installation
----------------

#. Create initial :ref:`scene <cityCreation>` objects.
#. Create the required :ref:`RoadSegments <roadSegment>`. And add them as children to the :ref:`RoadParent <roadParent>`.
#. Create the :ref:`necessary paths <pathCreator>`. 
#. Configure the :ref:`paths <pathCustomize>`. 
#. Create the necessary :ref:`PedestrianNode <pedestrianNode>` using the :ref:`PedestrianNodeCreator <pedestrianNodeCreator>`.
#. Adjust the :ref:`Traffic lights <trafficLight>`.
#. Create the :ref:`Traffic Areas <trafficArea>`, for example if you have a congested car park **[optional step]**.
#. Create the :ref:`Public Routes <trafficPublicRoute>` if you have :ref:`Public transport <trafficPublic>` with a given route **[optional step]**.
#. Open the :ref:`Road Parent <roadParentInfo>`.
	
	.. _roadParent:

	.. image:: /images/road/installation/RoadParent.png

#. Press `Force connect` button to connect segments (make sure all segments are :ref:`on one line <trafficNodeConnectionInfo>`).
#. Press the `Bake` button (should be done after each road edit & before starting the scene, for more info the :ref:`bake info <bakingInfo>`).
#. Create the :ref:`subscene <roadEntitySubscene>` **(one-time procedure)**.
#. For further changes to roads and configs, read the :ref:`Road <roadEdit>` & to sync both scenes, read the :ref:`Config <configEdit>` editing workflow.

.. _roadEntitySubscene:

Entity Subscene Creation
----------------
	
From `DOTS 1.0 <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/index.html>`_ onwards, all entity conversions must be done using subscenes. It's necessary to create a separate :ref:`subscene <subscene>` for roads.

	.. image:: /images/road/installation/Hub.png
	
Steps:
	#. Select :ref:`Hub <hub>` in the scene.
	#. Select `Entity subscene path` the path to create a :ref:`subscene <subscene>`.
	#. Enter the `Entity subscene name` or use the default name.
	#. On/off autosync configs (before migrating the configs to the :ref:`subscene <subscene>`, they will be synchronized with the configs that are in the :ref:`Hub <hub>`).
	#. On/off copy physics shapes feature (read more about :ref:`physics shape transferring <physicsShapeTransfer>`) **[required if you plan to use DOTS physics]**.
	#. Press the `Generate` button.
	#. All created :ref:`RoadSegments <roadSegment>` and :ref:`PedestrianNodes <pedestrianNode>` will automatically be moved to the :ref:`subscene <subscene>`.

.. _configEdit:

Config Editing Workflow
----------------

There are 2 variants to edit configs:

Main Scene Editing
~~~~~~~~~~~~

	.. image:: /images/road/installation/MainSceneExample.png

Steps
""""""""""""""

#. Select :ref:`Hub <hub>` in the scene.
#. After editing any config in the main scene :ref:`Hub <subsceneGenerator>` press the `Copy To Subscene` button or if the config is a non-scriptable object, apply the prefab to the selected config row.
	
	.. image:: /images/road/installation/Hub.png
	
Directional Editing
~~~~~~~~~~~~

	.. image:: /images/road/installation/EntitySubSceneExample.png
	
Steps
""""""""""""""

#. Open the `EntitySubScene` :ref:`subscene <subscene>`.
#. Edit any config.
#. After editing any config in the subscene, in the :ref:`Hub <subsceneGenerator>` press the `Copy From Subscene` button or if the config is a non-scriptable object, apply the prefab to the selected config row in the subscene.
#. Save & close :ref:`subscene <subscene>`.
	
