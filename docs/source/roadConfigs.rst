.. _roadConfigs:

Road Configs
=====

Overlap Config
------------

Config of overlapping of :ref:`traffic cars <trafficCar>` with :ref:`traffic nodes <trafficNode>`.

	.. image:: /images/configs/road/TrafficRoadOverlapConfig.png
	
**Calculate method:**
	* **Low accuracy** : low accuracy of calculation based on distance, but higher performance.
	* **High accuracy** : higher accuracy of calculation based on bounds, but little bit lower performance.

| **Size multiplier** : size multiplier of the :ref:`traffic car <trafficCar>`.
	
.. _trafficRoadConfig:

Traffic Road Config
------------

The config contains which categories each :ref:`traffic nodes <trafficNode>` belongs to.

	.. image:: /images/configs/road/TrafficRoadConfig.png
	
| **Route randomize nodes** : list of allowed nodes to randomly spawn on the path between those nodes.
| **Available for spawn nodes** : list of allowed :ref:`traffic nodes <trafficNode>` where :ref:`traffic cars <trafficCar>` can spawn.
| **Available for spawn target nodes** : list of allowed :ref:`traffic nodes <trafficNode>` that can be selected for a target at spawn.
| **Linked nodes** : nodes that are linked to a specific :ref:`traffic car <trafficCar>` which approaching a linked node (:ref:`parking example <trafficParking>`).

