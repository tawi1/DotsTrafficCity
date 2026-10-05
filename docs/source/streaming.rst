.. _streaming:

Streaming
=========

.. contents::
   :local:
   streamingConfigs

.. _cullPointInfo:

Cullpoint Info
--------------

The cull point is the origin for the surrounding entities (by default, it's a child of the camera). The :ref:`cull state <cullPointStates>` of surrounding entities varies depending on the distance to the culling point (:ref:`example <cullPointExamples>`).
You can change the global distances in the :ref:`cull config <cullConfig>` & :ref:`debug <cullPointDebug>`.

.. note::
   Culling distances can also be overridden on a per-entity or prefab basis using the :ref:`CullStateEntityAuthoring <cullStateEntityAuthoring>` or :ref:`CullStateConfigEntityAuthoring <cullStateConfigEntityAuthoring>` components.

.. _cullPointStates:

States
~~~~~~

* **Culled** : entity is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity is enabled but with limited or modified functionality for better performance.
* **InViewOfCamera** : entity is fully enabled.

Default State List
""""""""""""""""""

The default list is used for most objects and contains *Culled*, *Close to camera*, and *In view of camera* states.

	.. image:: /images/other/CullStateExample1.png
	`Default state list example.`
	
	.. note:: 
		* States are added to the prefab entity via the `CullComponentsExtension.CullComponentSet` extension method.

.. _overrideCullDistances:

Overriding Culling Distances
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If specific entities or entity prefabs require custom culling parameters (e.g., larger view distances for large buildings or custom camera viewports), you can override the global settings using one of the following authoring components:

.. _cullStateEntityAuthoring:

CullStateEntityAuthoring
""""""""""""""""""""""""
Allows overriding culling parameters (such as `maxDistance`, `visibleDistance`, and behind-camera thresholds) directly on a specific GameObject/Prefab within the Inspector.

.. _cullStateConfigEntityAuthoring:

CullStateConfigEntityAuthoring
""""""""""""""""""""""""""""""
Allows assigning a custom `CullConfig` ScriptableObject to override culling parameters for a specific entity or prefab, enabling shared custom culling profiles across multiple objects.

Scene Streaming
---------------

.. _roadStreaming:

Road Streaming
~~~~~~~~~~~~~~

Road Streaming is needed to split the map into chunks to support large-scale maps, ensuring that road entities (:ref:`TrafficNodes <trafficNode>`, :ref:`PedestrianNodes <pedestrianNode>`, etc.) are loaded only where the player is located.

`Youtube tutorial. <https://youtu.be/yoNqa0yjIYA>`_

How To Adjust
"""""""""""""

#. Enable streaming in the :ref:`Road Streaming Config <roadStreamingConfig>` to load road sections at runtime.
#. Adjust load/unload distance and section cell size.
#. :ref:`TrafficNode <trafficNode>`, :ref:`PedestrianNode <pedestrianNode>`, and :ref:`TrafficLightHandler <trafficLightHandler>` automatically attach to their related :ref:`RoadSegment <roadSegment>`.
#. :ref:`Traffic lights <trafficLightObject>` have a :ref:`SectionObjectAuthoring <sectionObject>` component attached.
#. If you want to add your own section object, add the :ref:`SectionObjectAuthoring <sectionObject>` component and select the appropriate `Section object type`.
#. :ref:`Debug streaming <sectionDebugger>` distance and section size.

	.. image:: /images/other/RoadStreamingExample.png
	`Road streaming example.`
	
.. _sectionObject:

Section Object Authoring
""""""""""""""""""""""""

	.. image:: /images/other/SectionObjectAuthoring.png
	
**Section object type:**
	* **Attach to closest** : attach to the nearest road section.
	* **Create new if necessary** : create a new road section if one doesn't exist with the currently computed section hash.
	* **Provider object** : object has a component implementing the `IProviderObject` interface that provides a reference to the associated object section.
	* **Custom object** : user-defined associated object section.
	
| **Include childs** : all child objects are included in the section of the parent object.

.. _sceneStreaming:

Scene Streaming
~~~~~~~~~~~~~~~

You can split scene content into chunks for partial loading at runtime (`DOTS` simulation only).

`Youtube tutorial. <https://youtu.be/6M_dn7yjMNk>`_

How To Create
"""""""""""""

#. Create a new empty `GameObject` and add the :ref:`SubSceneCreator <subSceneCreator>` component. 
#. Adjust the :ref:`chunk settings <subSceneCreatorChunkSettings>`.
#. If necessary, enable :ref:`post process settings <subSceneCreatorPostProcess>` **[optional step]**.
#. Press the `Create` button.
#. Adjust the :ref:`Streaming Level Config <streamingLevelConfig>` to load/unload subscenes at runtime.

.. _subSceneCreator:

SubScene Chunk Creator
~~~~~~~~~~~~~~~~~~~~~~

Content chunking tool to split the scene into chunks. Original objects remain disabled in the source scene and are used to create duplicates in the chunk subscenes.

	.. image:: /images/other/subSceneCreator.png
	
Assignments
"""""""""""

| **Custom parent** : custom parent transform for the generated subscenes.
| **Scene name** : subscene template name.
| **Create path** : subscene output save path.

.. _subSceneCreatorChunkSettings:

Chunk Settings
""""""""""""""

| **Chunk size** : size of each chunk cell.

**Position source type** : source position method used to assign objects to chunks:
	* **Object position** 
	* **Mesh center** 
	
| **Destroy previous created** : destroy previously created chunks before re-generating.

**Object find method** : search method for locating objects to include in chunks:
	* **By tag** : search by `Unity` tag.
	* **By layer** : search by `Unity` layer.
	
| **Target tag** : target search tag.
| **Disable old source objects** : disable source objects in the scene after chunk generation.

**Disable source object type** 
	* **Mesh renderer** : disable `MeshRenderer` components of source objects.
	* **Parent** : disable parent GameObjects of source objects.
	* **Parent if no mesh** : disable `MeshRenderer` if present, otherwise disable the parent GameObject.
	
| **Assign new layer** : assign a new layer to objects created within new chunks.

.. _subSceneCreatorPostProcess:

Post Process Settings
"""""""""""""""""""""

| **Copy physics shape** : toggle the :ref:`PhysicsShape Transfer <physicsShapeTransfer>` tool.
| **Post process new object** : toggle post-processing for created objects.
| **Component type name** : target component type name for post-processing.

**Post process type:**
	* **Delete component** : the matching component will be removed.
	* **Delete object** : the GameObject with the matching component will be deleted.

Chunk Data
""""""""""

Buttons
"""""""

| **Create** : generate subscene chunks.
| **Enable/disable scene objects** : toggle visibility/state of source scene objects.
| **Enable/disable sub scene objects** : toggle visibility/state of generated subscene objects.
| **Reset save path** : reset subscene save path to default.
| **Clear** : clear generated subscene chunks.

.. include:: streamingConfigs.rst