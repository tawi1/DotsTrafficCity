.. _carPrefabCreator:

Car Prefab Creator
=====

Prefab Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabSettings.png

	**Prefab source type:**
		* **Scene**
			* **Targets prefab parent** : prefabs will be taken from the selected root from the scene.
		* **Project**
			* **Prefabs** : selected prefabs from the project.
	**Car type:**
		* **Traffic** : prefab car will be created for the traffic.
		* **Player** : prefab car will be created for the player.
	**Traffic car convert template** : template which contains traffic prefab template.
	**Player car convert template** : template which contains traffic prefab template.
	**Custom atlas material** : custom material for created vehicles.
		
		
.. _carPrefabCreatorCommonSettings:

Common Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/CommonSettings.png
	
	**Assign hull mesh:** should find the hull of the car.
		* **Parent is hull mesh** : car root contains a car mesh.
	**Fit physics shape to mesh** : physical shape will be resized to the mesh size.
	**Has wheels** : should search for wheels on a :ref:`template <carPrefabCreatorTemplateSettings>`.
	**Has navmesh obstacle:** does the car contain `NavMeshObstacle <https://docs.unity3d.com/Manual/class-NavMeshObstacle.html>`_ component. 
		* **Move threshold**
		* **Carve stationary**
		* **Carve time to stationary**
	**Corrective hull mesh pivot:** offset of the vehicle hull along the Y axis.
		* **Additional pivot offset** : value of offset.
	
.. _carPrefabCreatorSaveSettings:
	
Save Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/SaveSettings.png
	
	**Save to exist preset** : add the created prefabs to an existing preset on the scene.
	**New preset settings:**
		* **Assign new preset to scene** : preset will replace an existing preset on scene.
		* **New preset path** : project path where to create a new preset.
		* **New preset name** : new preset name.
	**Entity type** : :ref:`entity type of the vehicle <trafficCarSettings>`.
	**Prefab save type:**
		* **Override source** : selected prefabs will be replaced by new ones.
		* **Create new if not exist** : new prefabs will be created only if there are no previously created ones by the selected path.
		* **Override target** : previously created prefabs will be overwritten in case of a duplicate.
	**Prefab save path type:**
		* **Original prefab path** : prefabs will be created in the directory where the selected prefabs are located.
		* **Template prefab path** : Prefabs will be created in the directory where the template is located.
		* **Custom path** : user's path of creation. 
	**New prefab template name** : pattern of the name of the created prefab (for instance *Car1* (source name) + "_new" (pattern) = Car1_new).
	
.. _carPrefabCreatorTemplateSettings:
	
Template Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/TemplateSettings.png
	
	**Hull name templates** : keyword phrases for automatic hull searches.
	
	**Wheel name templates** : keyword phrases for automatic wheels searches.
		* **Wheel FR** : forward right wheel.
		* **Wheel FL** : forward left wheel.
		* **Wheel BR** : backward right wheel.
		* **Wheel BL** : backward left wheel.
	
Prefab Info
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabInfo.png
	
	
	**Prefab car info:**
		* **Prefab** : reference to source prefab.
		* **New enum type** : :ref:`CarModel<carModel>` enum for created prefab entity.
		
Buttons
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/Buttons.png
	
	**Scan** : scan the added prefabs and add information about new ones to the `Prefab Info` tab.
	**Add enum types** : add new :ref:`CarModel<carModel>` enums from the `Prefab Info` tab.
	**Create** : create new entity prefabs based on the added prefabs.