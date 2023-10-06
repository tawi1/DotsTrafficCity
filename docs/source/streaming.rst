.. _streaming:

Streaming
=====

.. contents::
   :local:

.. _cullPointInfo:

Cullpoint Info
-------------------

The cull point is the point of origin for the surrounding entities (by default, it's a child of the camera). The :ref:`culling state <cullPointStates>` of the surrounding entities varies depending on the distance to the culling point (:ref:`example <cullPointExamples>`).
You can change the distances in the :ref:`cull config <cullConfig>`.

.. _cullPointStates:

States
~~~~~~~~~~~~

* **Culled** : entity is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity enabled but with limited or modified functionality for better performance.
* **InVisionOfCamera** : entity fully enabled.

Scene Streaming
-------------------

.. _roadStreaming:

Road Streaming
~~~~~~~~~~~~

Road Streaming is needed to split the map into chunks to create huge maps, so that road entities: :ref:`TrafficNodes <trafficNode>, :ref:`PedestrianNodes <pedestrianNode>, etc. are only loaded where the player is.

How To Adjust
""""""""""""""

#. Enable streaming in the :ref:`Road Streaming Config <roadStreamingConfig>` to load road sections at the runtime.
#. Adjust load/unload distance and section cell size.
#. :ref:`TrafficNode <trafficNode>`, :ref:`PedestrianNode <pedestrianNode>`, :ref:`TrafficLightHandler <trafficLightHandler>` automatically attaches to related :ref:`RoadSegment <roadSegment>`.
#. :ref:`Traffic lights <trafficLightObject>` has :ref:`SectionObjectAuthoring <sectionObject>` component.
#. If you want to add your own section object, add :ref:`SectionObjectAuthoring <sectionObject>` component and select proper `Section object type`.
#. :ref:`Debug streaming <sectionDebugger>` distance and section size.

	.. image:: /images/other/RoadStreamingExample.png
	`Road streaming example.`
	
.. _sectionObject:

Section Object Authoring
""""""""""""""

	.. image:: /images/other/SectionObjectAuthoring.png
	
**Section object type:**
	* **Attach to closest** : attach to closest road section.
	* **Create new if nessesary** : create new road section if not exist with the current computed section hash.
	* **Provider object** : object has a component that implements the `IProviderObject` interface, which provides a reference to the associated object section.
	* **Custom object** : user's custom related object section.
	
| **Include childs** :  all child objects are included in the section of the parent object.

Content Streaming
~~~~~~~~~~~~

You can divide the scene content into chunks for partial loading at runtime.

How To Create
""""""""""""""

#. Create new empty `GameObject` and add :ref:`SubSceneCreator <subSceneCreator>` component. 
#. Customize :ref:`chunk settings <subSceneCreatorChunkSettings>`.
#. If necessary enable :ref:`post process settings <subSceneCreatorPostProcess>` **[optional step]**.
#. Press `Create` button.
#. Adjust :ref:`Streaming Level Config <streamingLevelConfig>` to load/unload subscenes at the runtime.

.. _subSceneCreator:

Sub Scene Creator
~~~~~~~~~~~~

Content chunking tool to split the scene into chunks. Old objects remain and disabled in the old scene and are used to create duplicates in the chunk sub-scenes.

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
	* **By tag** : by unity tag.
	* **By layer** : by unity layer.
	
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