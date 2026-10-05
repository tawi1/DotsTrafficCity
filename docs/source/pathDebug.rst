.. _pathDebug:

Path Debug
==========

.. contents::
   :local:

.. _pathDebugger:

Path Debugger
-------------

`YouTube tutorial. <https://youtu.be/93772MIsD2Q>`_

How To Open
~~~~~~~~~~~

In the scene, select:

	`CityDebugger/PathDebugger`
	
Settings
~~~~~~~~
	
	.. image:: /images/debuggers/path/PathDebugger.png		
	
| **Draw editor traffic path** : enables/disables :ref:`path <path>` visualization in the Scene view during editing.
**Draw entity traffic path** : enables/disables runtime entity :ref:`path <path>` visualization.
	* **Draw entity traffic node connection** : toggles runtime :ref:`TrafficNode <trafficNode>` connection lines.
**Draw pedestrian connection path** : enables/disables :ref:`PedestrianNode <pedestrianNode>` connection lines in the editor.
	
.. _pathDataViewer:

Path Data Viewer
----------------

Tool for inspecting and validating :ref:`path <path>` parameters across the city.

How To Open
~~~~~~~~~~~

From the Unity toolbar:

	`Spirit604/CityEditor/Window/Path Data Viewer`

	.. image:: /images/debuggers/path/PathDataViewerOpenExample.png		
	
How To Use
~~~~~~~~~~

#. Select the desired :ref:`Path view type <pathDataViewerSettings>`.
#. In the :ref:`Colors info <pathDataViewerSettings>` list, click `-` to hide paths matching that parameter.
#. Click `+` to show hidden paths again.
#. Click `x` to reset the saved color for a parameter.

.. _pathDataViewerSettings:

Settings
~~~~~~~~

	.. image:: /images/debuggers/path/PathDataViewer.png		
	
| **Default color** : default display color for paths.

**Path view type:** parameter displayed in the Scene view:
	* **Speed limit** : speed limits of :ref:`paths <path>`.
	* **Priority** : priority values of :ref:`paths <path>`.
	* **Path type** : road types of :ref:`paths <path>`.
	* **Traffic path group** : :ref:`traffic group <pathTrafficGroup>` masks of :ref:`paths <path>`.
	* **Traffic path node group** : :ref:`traffic group <pathTrafficGroup>` of individual :ref:`waypoints <pathWaypointInfo>`.
	* **Node direction** : forward or reverse direction of :ref:`waypoints <pathWaypointInfo>`.
	* **Arrow light** : paths assigned custom light arrows.
	* **Rail** : paths configured for :ref:`rail movement <trafficRail>`.
	
| **Draw custom colors** : enables/disables custom parameter coloring.
| **Show world buttons** : displays in-scene path selection buttons.
| **Show intersect point** : visualizes :ref:`intersection points <pathIntersects>`.
| **Show waypoints** : displays :ref:`waypoints <pathWaypointInfo>` along paths.
| **Show path handles** : displays position handles on the selected path.
| **Show path edit buttons** : displays node addition/removal buttons.
| **Multiple selection** : enables selecting multiple paths simultaneously.
| **Show unselect buttons** : displays deselect buttons in multi-selection mode.
| **Refresh** : refreshes cached path data.

.. _pathDataViewerExamples:

Examples
~~~~~~~~

	.. image:: /images/debuggers/path/PathDataViewerPathTypeExample.png		
	`Path type example.`
	
	.. image:: /images/debuggers/path/PathDataViewerPriorityExample.png		
	`Priority path example.`
		
	.. image:: /images/debuggers/path/PathDataViewerSpeedLimit.png		
	`Speed limit path example.`
	
Path Index Debugger
-------------------

How To Open
~~~~~~~~~~~

In the scene, select:

	`CityDebugger/PathDebugger`
	
Settings
~~~~~~~~

	.. image:: /images/debuggers/path/Runtime/PathIndexDebugger.png		
	
| **Should debug** : enables/disables index debugging.
| **Select path** : enables path selection filters.
| **Selected path index** : target path index to inspect (-1 shows all).
**Path debug mode** :
	* **Default** : displays current path index only.
	* **Parallel** : displays parallel path indices.
	* **Neighbor paths** : displays neighbor path indices originating from the same node.
	* **Next connected paths** : displays next connected route indices.
	* **Intersected paths** : displays intersecting path indices.
	* **Car count** : displays number of cars currently traversing the path.
	
Index format:
	* ``543 (544, 545, 546)`` — active path index followed by related indices depending on the mode.