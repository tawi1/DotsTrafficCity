.. _commonDebug:

Common Debug
============

.. contents::
   :local:

`Youtube tutorial. <https://youtu.be/5ZtQahmDoO0&t=331>`_

CullPoint Debugger
------------

Displays the :ref:`cull point <cullPointInfo>` radius (:ref:`example <cullPointExamples>`).

	.. image:: /images/debuggers/other/CullPointDebugger.png		
	
| **Enable debug** : on/off debugger.
	
CullState Object Debugger
------------

Displays the :ref:`cull state <cullPointStates>` of objects in the scene (:ref:`example <cullPointExamples>`).

	.. image:: /images/debuggers/other/CullStateObjectDebugger.png	

.. _cullPointExamples:

Examples
~~~~~~~~~~~~
	
	.. image:: /images/debuggers/other/CullStateObjectDebuggerExample.png		
	`Cull point debug and cull state object debugger are enabled example (red - culled, blue - close to camera, green - in view of camera).`
	
Hashmap Grid Debugger
------------

Displays the size and position of the hashmap cell (can be useful when choosing the basic hashmap cell size in `DOTS` systems).

	.. image:: /images/debuggers/other/HashmapGridDebugger.png	

| **Enable debug** : on/off debugger.
| **Line color** : colour line in the scene.
| **Cell size** : grid cell size.
| **X size** : X grid size.
| **Y size** : Y grid size.

	.. image:: /images/debuggers/other/HashmapGridDebuggerExample.png		
	
.. _sectionDebugger:
	
Section Debugger
------------

Displays the :ref:`load section <roadStreaming>` radius, created road sections, road connections (:ref:`TrafficNodes <trafficNode>` and :ref:`PedestrianNodes <pedestrianNode>`).

	.. image:: /images/debuggers/other/SectionDebugger.png	

| **Enable debug** : on/off debugger.
| **Show traffic path** : on/off display connection of :ref:`TrafficNodes <trafficNode>`.
| **Show pedestrian path** : on/off display connection of :ref:`PedestrianNodes <pedestrianNode>`.
| **Loaded section color** : loaded section color.
| **Unloaded section color** : unloaded section color.
| **Load circle color** : load circle color.
| **Unload circle color** : unload circle color.
| **Pedestrian path color** : connection color of :ref:`PedestrianNodes <pedestrianNode>`.

	.. image:: /images/other/RoadStreamingExample.png
	`Road streaming example.`

	
