.. _trafficNodeDebug:

Traffic Node Debug
============

.. contents::
   :local:

Traffic Node Data Viewer
------------

Tool for finding :ref:`traffic nodes <trafficNode>` with filtering of selected parameters that differ from prefab.

How To Open
~~~~~~~~~~~~

In the `Unity` toolbar:

	`Spirit604/CityEditor/Window/TrafficNode Data Viewer`

	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewerOpenExample.png		
	
How To Filter
~~~~~~~~~~~~

#. Enable `Filter node data` option.
#. If you need to filter by a selected parameter enable `Custom param filter` and add desired parameters.

Settings
~~~~~~~~~~~~
	
	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewer.png		
	
	
| **Traffic node prefab** : :ref:`traffic node <trafficNode>` source prefab for comparison.
| **Traffic node data viewer** : internal filter settings.
| **Filter node data** : on/off filtering
| **Full labels** : show full setting labels.
| **Show only on cursor** : show node traffic data only when the cursor is hovering.
| **Custom param filter** : node filtering by selected parameters.
| **Show select buttons** : on/off select buttons in the scene.
| **Selected node** : :ref:`settings <trafficNodeSettings>` for the selected :ref:`traffic node <trafficNodeSettings>` (here you can quickly tweak the settings).

	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewerExample1.png		
	`Filtering disabled.`
	
	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewerExample2.png		
	`All parameters filtering enabled example.`
	
	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewer2.png		
	.. image:: /images/debuggers/trafficNode/TrafficNodeDataViewerFilterExample.png		
	`Filtering by "capacity" example.`
	
		
Traffic Node Debug
------------

For debugging :ref:`traffic node <trafficNode>` entities in runtime.

	.. image:: /images/debuggers/trafficNode/TrafficNodeDebugger.png		
	
.. _trafficNodeIndexDebug:

Index Debug
~~~~~~~~~~~~

Shows the node index.
For example: 450 (E: 3308) - [local :ref:`index for spawning <trafficDebugSpawnHelper>` a vehicle] [entity index].

	.. image:: /images/debuggers/trafficNode/TrafficNodeDebuggerIndex.png		

Available Debug
~~~~~~~~~~~~

Shows the availability of a node for spawning.

	.. image:: /images/debuggers/trafficNode/TrafficNodeDebuggerAvailableExample.png		

Light State Debug
~~~~~~~~~~~~

Shows :ref:`light state <trafficLightState>` node traffic.

	.. image:: /images/debuggers/trafficNode/TrafficNodeDebuggerLightExample.png	

Capacity Debug
~~~~~~~~~~~~

Shows the capacity of the node and the linked vehicle.

	.. image:: /images/debuggers/trafficNode/TrafficNodeDebuggerCapacityExample.png		

	
