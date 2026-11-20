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
#. Create the necessary :ref:`Pedestrian nodes <pedestrianNode>` using the :ref:`PedestrianNode Creator <pedestrianNodeCreator>` if your city requires walking NPCs.
#. Adjust the :ref:`Traffic lights <trafficLight>` and intersection timings.

Phase 3: Advanced Elements (Optional)
-------------------------------------

* **Traffic Areas:** Create :ref:`Traffic Areas <trafficArea>` if your map includes specific zones like congested parking lots.
* **Public Transport:** Set up :ref:`Public Routes <trafficPublicRoute>` if you are planning to use :ref:`Buses or Trains <trafficPublic>` with predefined routes.

Phase 4: Baking & Subscenes
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
------------------------

From `DOTS 1.0 <https://docs.unity3d.com/Packages/com.unity.entities@1.0/manual/index.html>`_ onwards, all entity conversions must be done using subscenes. It's necessary to create a separate :ref:`subscene <subscene>` for roads.

	.. image:: /images/road/installation/Hub.png

Steps
~~~~~

#. Select :ref:`Hub <hub>` in the scene.
#. Set ``Entity subscene path`` to specify where to create the :ref:`subscene <subscene>`.
#. Enter the ``Entity subscene name`` or use the default name.
#. Toggle ``Autosync configs`` on or off (before migrating configs to the :ref:`subscene <subscene>`, they will be synchronized with the configs in the :ref:`Hub <hub>`).
#. Toggle ``Copy physics shapes`` on or off (read more about :ref:`physics shape transferring <physicsShapeTransfer>`) **[required if you plan to use DOTS physics]**.
#. Press the ``Generate`` button.
#. All created :ref:`RoadSegments <roadSegment>` and :ref:`PedestrianNodes <pedestrianNode>` will automatically be moved to the :ref:`subscene <subscene>`.

.. _configEdit:

Config Editing Workflow
-----------------------

Why Configs Exist on Both Scenes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In Unity DOTS, the **Entity SubScene** and the **Main Scene** serve different roles and both need access to the same configuration assets:

* **Entity SubScene:** Bakers convert these configs into ECS entity components and ``BlobAssets`` used by DOTS simulation systems.
* **Main Scene:** MonoBehaviour initializers and managers use the same configs at runtime to initialize main-scene systems, hybrid components, and scene-level dependencies.

Because both scenes hold their own references to these config assets, they must stay synchronized. If the assigned assets differ, a ``[Config Sync Mismatch]`` error will be logged upon entering Play Mode.

There are 4 ways to edit and synchronize configs:

Auto-Sync Local Config (Recommended)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Steps
"""""

#. Open Project Settings from the Unity toolbar:

   * ``Edit/ProjectSettings/604Spirit/City Settings/``

#. Enable ``Sync Config On Change``.
#. Any config changes made on the Main Scene will now automatically synchronize to the SubScene.

Manual Sync Local Config
~~~~~~~~~~~~~~~~~~~~~~~~

Steps
"""""

#. Change the target field or assign a new asset on the config component in the Main Scene.
#. A ``Sync To Subscene`` button will appear in the component's Inspector — press it to synchronize this config with the SubScene.

Main Scene Editing
~~~~~~~~~~~~~~~~~~

	.. image:: /images/road/installation/MainSceneExample.png

Steps
"""""

#. Edit or reassign the required config on the Main Scene.
#. Select :ref:`Hub <subsceneGenerator>` in the scene and press ``Copy To Subscene``. If the config is not a ScriptableObject, apply the prefab override for the selected config row.

	.. image:: /images/road/installation/Hub.png

Direct SubScene Editing
~~~~~~~~~~~~~~~~~~~~~~~

	.. image:: /images/road/installation/EntitySubSceneExample.png

Steps
"""""

#. Open the ``EntitySubScene`` :ref:`subscene <subscene>`.
#. Edit or reassign the required config.
#. In :ref:`Hub <subsceneGenerator>`, press ``Copy From Subscene``. If the config is not a ScriptableObject, apply the prefab override for the selected config row in the SubScene.
#. Save & close the :ref:`subscene <subscene>`.