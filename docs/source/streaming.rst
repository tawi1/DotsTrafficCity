.. _streaming:

Streaming
=====

.. contents::
   :local:
   streamingConfigs

.. _cullPointInfo:

Cullpoint Info
-------------------

The cull point is the origin for the surrounding entities (by default, it's a child of the camera). The :ref:`cull state <cullPointStates>` of the surrounding entities varies depending on the distance to the culling point (:ref:`example <cullPointExamples>`).
You can change the distances in the :ref:`cull config <cullConfig>`.

.. _cullPointStates:

States
~~~~~~~~~~~~

* **Culled** : entity is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity is enabled but with limited or modified functionality for better performance.
* **PreInitInCamera** : :ref:`state <extendedStateList>` between to `CloseToCamera` and `InViewOfCamera`, currently used to activate static physics objects **[optional]**.
* **InViewOfCamera** : entity is fully enabled.

Default State List
""""""""""""""

The default list is used for most objects, contains *Culled*, *Close to camera*, *In view of camera* states.

	.. image:: /images/other/CullStateExample1.png
	`Default state list example.`
	
	.. note:: 
		* States add to the prefab entity by `CullComponentsExtension.CullComponentSet` extension method.
	
.. _extendedStateList:
	
Extended State List
""""""""""""""

The extended state list is used for objects that require a pre-init state before viewing in camera state, but earlier than the *close to camera* state, contains *Culled*, *Close to camera*, *Pre-init in camera*, *In view of camera* states.

	.. image:: /images/other/CullStateExample2.png
	`Extended state list example.`
	
	.. note:: 
		* States add to the prefab entity by `CullComponentsExtension.PreinitCullComponentSet` extension method.
		* It is used in the project for static physics objects.
	
Scene Streaming
-------------------

.. _roadStreaming:

Road Streaming
~~~~~~~~~~~~

Road Streaming is needed to split the map into chunks to create huge maps, so that road entities: :ref:`TrafficNodes <trafficNode>`, :ref:`PedestrianNodes <pedestrianNode>`, etc. are only loaded where the player is.

`Youtube tutorial. <https://youtu.be/yoNqa0yjIYA>`_

How To Adjust
""""""""""""""

#. Enable streaming in the :ref:`Road Streaming Config <roadStreamingConfig>` to load road sections at the runtime.
#. Adjust load/unload distance and section cell size.
#. :ref:`TrafficNode <trafficNode>`, :ref:`PedestrianNode <pedestrianNode>`, :ref:`TrafficLightHandler <trafficLightHandler>` automatically attaches to related :ref:`RoadSegment <roadSegment>`.
#. :ref:`Traffic lights <trafficLightObject>` has a :ref:`SectionObjectAuthoring <sectionObject>` component.
#. If you want to add your own section object, add the :ref:`SectionObjectAuthoring <sectionObject>` component and select the appropriate `Section object type`.
#. :ref:`Debug streaming <sectionDebugger>` distance and section size.

	.. image:: /images/other/RoadStreamingExample.png
	`Road streaming example.`
	
.. _sectionObject:

Section Object Authoring
""""""""""""""

	.. image:: /images/other/SectionObjectAuthoring.png
	
**Section object type:**
	* **Attach to closest** : attach to nearest road section.
	* **Create new if nessesary** : create a new road section if doesn't exist with the currently computed section hash.
	* **Provider object** : object has a component that implements the `IProviderObject` interface, that provides a reference to the associated object section.
	* **Custom object** : user's own associated object section.
	
| **Include childs** : all child objects are included in the section of the parent object.

.. _sceneStreaming:

Scene Streaming
~~~~~~~~~~~~

You can split the scene content into chunks for partial loading at runtime.

`Youtube tutorial. <https://youtu.be/6M_dn7yjMNk>`_

How To Create
""""""""""""""

#. Create a new empty `GameObject` and add the :ref:`SubSceneCreator <subSceneCreator>` component. 
#. Adjust the :ref:`chunk settings <subSceneCreatorChunkSettings>`.
#. If necessary, enable :ref:`post process settings <subSceneCreatorPostProcess>` **[optional step]**.
#. Press the `Create` button.
#. Adjust the :ref:`Streaming Level Config <streamingLevelConfig>` to load/unload subscenes at the runtime.

.. _subSceneCreator:

SubScene Chunk Creator
~~~~~~~~~~~~

Content chunking tool to split the scene into chunks. Old objects remain disabled in the old scene and are used to create duplicates in the chunk sub-scenes.

	.. image:: /images/other/subSceneCreator.png
	
Assigments
""""""""""""""

| **Custom parent** : custom parent of subscene.
| **Scene name** : subscene template name.
| **Create path** : create subscenes path.

.. _subSceneCreatorChunkSettings:

Chunk Settings
""""""""""""""

| **Chunk size** : chunk size.

**Position source type** : source position of the object to be assigned to the chunk.
	* **Object position** 
	* **Mesh center** 
	
| **Destroy previous created** : destroy previously created chunks.

**Object find method** : method for finding an object to add to a chunk.
	* **By tag** : by `Unity` tag.
	* **By layer** : by `Unity` layer.
	
| **Target tag** : search tag.
| **Disable old source objects** : turn off the source objects.

**Disable source object type** 
	* **Mesh renderer** : disable meshRenderers of source objects.
	* **Parent** : disable parents of source objects.
	* **Parent if no mesh** : disable the meshRenderer, but if not, disable the parent.
	
| **Assign new layer** : assign new layer to objects created from new chunks.

.. _subSceneCreatorPostProcess:

Post Process Settings
""""""""""""""

| **Copy physics shape** : on/off :ref:`PhysicsShape Transfer <physicsShapeTransfer>` tool.
| **Post process new object** : on/off post processing of the object.
| **Component type name** : target component name.

**Post process type:**
	* **Delete component** : the component found will be deleted.
	* **Delete object** : the object with the found component will be de.

Chunk Data
""""""""""""""

Buttons
""""""""""""""

| **Create** : create subscene chunks.
| **Enable/disable scene objects** : enable/disable source scene objects.
| **Enable/disable sub scene objects** : enable/disable created subscene objects.
| **Reset save path** : reset save path of the subscenes.
| **Clear** : clear created subscene chunks.

.. include:: streamingConfigs.rst