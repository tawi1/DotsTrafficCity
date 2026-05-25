.. _roadNetworkWorkflow:

Road Network Workflow
=====================

This guide covers the full step-by-step process of building and configuring a functional city road network from scratch.

Phase 1: Initial Setup
----------------------

#. Create the initial :ref:`scene base <cityCreation>` objects via the Unity toolbar.
#. Create the required :ref:`Road Segments <roadSegment>`. 
#. Add all created segments as children to the **Road Parent** object in your scene hierarchy.

Phase 2: Path & Node Creation
-----------------------------

#. Create the :ref:`necessary paths <pathCreator>` using the editor tools.
#. Configure specific path parameters such as speed limits, traffic groups, and lanes (read more about :ref:`path customization <pathCustomize>`).
#. Connect the adjacent road segments together. For detailed instructions on automation and manual tools, see the :ref:`How To Connect Roads <howToConnectRoad>` guide.
#. Adjust the :ref:`Traffic lights <trafficLight>` and intersection timings.

Phase 3: Baking & Subscenes
---------------------------

#. Select the **Road Parent** component in the hierarchy.
	
   .. image:: /images/road/installation/RoadParent.png
      :alt: Road Parent Inspector View
      :align: center

#. Click the **Bake** button. 
   
   .. warning:: Data baking must be done after *every* road modification and strictly before entering Play Mode. For more details, see :ref:`Baking Info <bakingInfo>`.

#. Generate the :ref:`Entity Subscene <roadEntitySubscene>`. This is a **one-time procedure** to convert standard GameObjects into high-performance DOTS entities.

Next Steps
----------

For any further modifications to existing roads, layouts, or runtime parameters, please refer to the :ref:`Road Editing Workflow <roadEdit>`.

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

.. _configEdit:

Config Editing Workflow
----------------

There are 4 variants to edit configs:

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

Manual Sync Local Config
~~~~~~~~~~~~

Steps
""""""""""""""

#. Change the desired value of the desired config.
#. After that, the `Sync To Subscene` button will appear to synchronize this config with the subscene.

Auto-Sync Local Config
~~~~~~~~~~~~

Steps
""""""""""""""

#. Open project settings from the `Unity` toolbar:

	* `Edit/ProjectSettings/604Spirit/City Settings/`
	
#. Tick on `Sync Config On Change`.
#. After that, any configuration changes made to the main scene are automatically synchronized to the subscene.	
