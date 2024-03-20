.. _streamingConfigs:

Configs
-------------------
	
.. _cullConfig:

Cull Config
~~~~~~~~~~~~

Config of the :ref:`cull point <cullPointInfo>`.

	.. image:: /images/configs/common/CullConfig.png
	
**Has cull:**
	* **Max distance** : maximum distance to activate entities.
	* **Visible distance** : distance to activate visual features of entities.
| **Show debug** : on/off visual culling circle in the scene.
	
.. _roadStreamingConfig:

Road Streaming Config
~~~~~~~~~~~~

Config for :ref:`load/unload <roadStreaming>` road sections from the entity :ref:`subscene <subscene>`.

	.. image:: /images/configs/common/RoadStreamingConfig.png
	
| **Streaming is enabled** : on/off streaming.
| **Ignore Y** : ignore calculation of distance to road section for Y axis.
| **Distance for streaming in** : distance at what the road section is loaded.
| **Distance for streaming out** : distance at what the road section is unloaded.
| **Section cell size** : cell size of the road section.
| **Node cell size** : node size for :ref:`TrafficNode <trafficNode>` and :ref:`PedestrianNode <pedestrianNode>` in order to compute a unique position hash for them.

.. _streamingLevelConfig:

Streaming Level Config
~~~~~~~~~~~~

Config for :ref:`load/unload <sceneStreaming>` content subscenes.

	.. image:: /images/configs/common/StreamingLevelConfig.png
	
**Streaming is enabled:**
	* **Distance for streaming in** : distance at what the subscene is loaded.
	* **Distance for streaming out** : distance at what the subscene is unloaded.