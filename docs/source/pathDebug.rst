.. _pathDebug:

Path Debug
============

.. contents::
   :local:

.. _pathDebugger:

Path Debugger
------------

How To Open
~~~~~~~~~~~~

In the scene, select:

	`CityDebugger/PathDebugger`
	
Settings
~~~~~~~~~~~~
	
	.. image:: /images/debuggers/path/PathDebugger.png		
	
| **Draw editor traffic path** : on/off :ref:`path <path>` visualisation on the scene in `Editor`.
**Draw entity traffic path** : on/off entity :ref:`path <path>` visualisation on the scene at runtime.
	* **Draw entity traffic node connection** : on/off draw :ref:`TrafficNode <trafficNode>` entity connection debug at runtime.
**Draw pedestrian connection path** : on/off :ref:`PedestrianNode <pedestrianNode>` connection visualisation on the scene in the `Editor`.
	
.. _pathDataViewer:

Path Data Viewer
------------

Tool for quick visualisation of :ref:`path <path>` parameters.

How To Open
~~~~~~~~~~~~

In the `Unity` toolbar:

	`Spirit604/CityEditor/Window/Path Data Viewer`

	.. image:: /images/debuggers/path/PathDataViewerOpenExample.png		
	
How To Use
~~~~~~~~~~~~

#. Select :ref:`Path view type <pathDataViewerSettings>`.
#. In the :ref:`Colors info <pathDataViewerSettings>` tab, press `-` to hide the paths with the selected option.
#. Press `+` to display the hidden path with the selected option again.
#. Press `x` to reset saved color of the parameter.

.. _pathDataViewerSettings:

Settings
~~~~~~~~~~~~

	.. image:: /images/debuggers/path/PathDataViewer.png		
	
| **Default color** : default :ref:`path <path>` color.

**Path view type:** selected :ref:`parameter <pathSettings>` for visualisation (:ref:`examples <pathDataViewerExamples>`)
	* **Speed limit**
	* **Priority**
	* **Path type**
	* **Traffic type**
	* **Node direction**
	
| **Draw custom colors** : on/off custom colors of the :ref:`paths <path>` on the scene.
| **Show world buttons** : Show world :ref:`path <path>` selection buttons.
| **Show intersect point** : on/off visual :ref:`intersection points <pathIntersects>` on the scene.
| **Show waypoints** : on/off waypoints of the :ref:`path <path>` on the scene.
| **Show path handles** : on/off :ref:`path <path>` position handles of the selected path.
| **Show path edit buttons** : on/off :ref:`path <path>` edit buttons of the selected path.
| **Refresh** : update :ref:`path <path>` data in the viewer.

.. _pathDataViewerExamples:

Examples
~~~~~~~~~~~~

	.. image:: /images/debuggers/path/PathDataViewerPathTypeExample.png		
	`Path type example.`
	
	.. image:: /images/debuggers/path/PathDataViewerPriorityExample.png		
	`Priority path example.`
		
	.. image:: /images/debuggers/path/PathDataViewerSpeedLimit.png		
	`Speed limit path example.`
	
Path Index Debugger
------------

How To Open
~~~~~~~~~~~~

In the scene, select:

	`CityDebugger/PathDebugger`
	
Settings
~~~~~~~~~~~~

	.. image:: /images/debuggers/path/Runtime/PathIndexDebugger.png		
	
| **Should debug** : on/off debugger.
| **Select path** : on/off path selection settings.
| **Selected path index** : display the data for the selected path (-1 path is not selected).
**Path debug mode** :
	* **Default** : only the current path index is shown.
	* **Parallel** : parallel path indexes.
	* **Neighbor paths** : neighbor path indexes (paths that start from the same point).
	* **Next connected paths** : indexes to which the current path is connected.
	* **Intersected paths** : intersection paths indexes.
	* **Car count** : number of cars with the current path index.
	
Index example:
	* 543 (544, 545, 546) - current path index is 543. Other relevant path indexes, depending on the chosen `Path debug mode`.
	
Examples
~~~~~~~~~~~~

	.. image:: /images/debuggers/path/Runtime/PathIndexDebuggerExample1.png	
	`Default "Path debug mode" example`.
	
	.. image:: /images/debuggers/path/Runtime/PathIndexDebuggerExample2.png		
	`Parallel paths "Path debug mode" example`.