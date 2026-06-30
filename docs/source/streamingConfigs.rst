.. _streamingConfigs:

Configs
-------------------
	
.. _cullConfig:

Cull Config
~~~~~~~~~~~~

Config of the :ref:`cull point <cullPointInfo>`.

	.. image:: /images/configs/common/CullConfig.png
	``Hub/StreamingConfigs/CullConfig``
	
| **Has cull** : Enable or disable the culling system.
| **Ignore Y** : If enabled, the Y-axis distance will be ignored during culling calculations.
| **Cull Method** : Method used to calculate culling:
	* **Calculate Distance** : Culling based strictly on distance.
	* **Camera View** : Culling based on distance to camera & view port.
	* **Custom** : User's custom culling solution.

**Has cull enabled settings:**
	* **Max distance** : This is the distance at which the entity has limited functionality (e.g. movement without physics). Entities can also spawn at node entities at this distance (spawn culling state can be changed in the CitySpawnConfig). Any entities beyond this distance are automatically removed.
	* **Preinit distance** : This distance is used for special entities that should be activated between the camera view & close to camera culling states.
	* **Visible distance** : The camera view distance at which where visual features of entities (e.g. physics) are activated. By default, spawning doesn't not occur at this distance (spawn culling state can be changed in the CitySpawnConfig).
	* **Threshold** : The buffer threshold value for culling calculations to prevent frequent state switching.

**Camera View method settings:**
	* **View port square size** : Size of the viewport square used for the viewport culling calculation.
	* **Override behind camera** : Enable to use separate culling distance settings for entities located behind the camera.

**Behind camera settings:**
	* **Behind max distance** : Behind camera, maximum distance to activate entities.
	* **Behind preinit distance** : Behind camera, maximum distance for pre-initialization of special entities.
	* **Behind visible distance** : Behind camera, distance to activate visual features of entities.
	
.. _roadStreamingConfig:

Road Streaming Config
~~~~~~~~~~~~

Config for :ref:`load/unload <roadStreaming>` road sections from the entity :ref:`subscene <subscene>`.

	.. image:: /images/configs/common/RoadStreamingConfig.png
	``Hub/StreamingConfigs/RoadStreamingConfig``
	
| **Streaming is enabled** : on/off streaming.
| **Ignore Y** : ignore calculation of distance to road section for Y axis.
| **Distance for streaming in** : distance at what the road section is loaded.
| **Distance for streaming out** : distance at what the road section is unloaded.
| **Section cell size** : cell size of the road section.
| **Node cell size** : node size for :ref:`TrafficNode <trafficNode>` in order to compute a unique position hash for them.

.. _streamingLevelConfig:

Streaming Level Config
~~~~~~~~~~~~

Config for :ref:`load/unload <sceneStreaming>` content subscenes (DOTS subscenes only).

	.. image:: /images/configs/common/StreamingLevelConfig.png
	``Hub/StreamingConfigs/StreamingLevelConfig``
	
**Streaming is enabled:**
	* **Distance for streaming in** : distance at what the subscene is loaded.
	* **Distance for streaming out** : distance at what the subscene is unloaded.