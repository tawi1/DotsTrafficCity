.. _carPrefabCreator:

Car Prefab Creator
=====

How To Use
----------------

Description of the vehicle creation process described :ref:`here <trafficCarHowTo>`.

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
	
| **Cache container** : cache data of saved vehicles.
| **Vehicle data collection** : reference to :ref:`collection <vehicleCollection>` of all vehicles.
| **Traffic car convert template** : template which contains traffic prefab template.
| **Player car convert template** : template which contains traffic prefab template.
		
.. _carPrefabCreatorCommonSettings:

Common Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/CommonSettings.png
	
**Assign hull mesh:** should find the hull of the car.
	* **Parent is hull mesh** : car root contains a car mesh.
| **Fit physics shape to mesh** : physical shape will be resized to the mesh size.
| **Has wheels** : should search for wheels on a :ref:`template <carPrefabCreatorTemplateSettings>`.
**Has navmesh obstacle:** does the car contain `NavMeshObstacle <https://docs.unity3d.com/Manual/class-NavMeshObstacle.html>`_ component. 
	* **Move threshold**
	* **Carve stationary**
	* **Carve time to stationary**
**Add offset:** offset of the vehicle hull along the Y axis.
	* **Fix pivot** : fixes the pivot point if the pivot point is in the centre of the mesh.
	* **Add wheel offset** : adds wheel offset size.
	* **Local offset** : custom offset value.
	
.. _carPrefabCreatorSaveSettings:
	
Save Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/SaveSettings.png
	
**Save to exist preset:** 
	* **Scene**: add the created prefabs to an existing preset on the scene.
	* **Selected**: add the created prefabs to selected preset.

**New preset settings:**
	* **Assign new preset to scene** : preset will replace an existing preset on scene.
	* **New preset path** : project path where to create a new preset.
	* **New preset name** : new preset name.
	
| **Entity type** : :ref:`entity type of the vehicle <trafficCarSettings>`.

**Prefab save type:**
	* **Override source** : selected prefabs will be replaced by new ones.
	* **Create new if not exist** : new prefabs will be created only if there are no previously created ones by the selected path.
	* **Override target** : previously created prefabs will be overwritten in case of a duplicate.
	
**Prefab save path type:**
	* **Original prefab path** : prefabs will be created in the directory where the selected prefabs are located.
	* **Template prefab path** : Prefabs will be created in the directory where the template is located.
	* **Custom path** : user's path of creation. 
	
| **New prefab template name** : pattern of the name of the created prefab (for instance *Car1* (source name) + "_new" (pattern) = Car1_new).

**Collection edit type:**
	* **Add to exist** : add vehicles to exist :ref:`vehicle collection <vehicleCollection>`.
	* **Override** : overrides :ref:`vehicle collection <vehicleCollection>` by created vehicles.
	
**Material type:**
	* **Source** : material is copied from the source prefab.
	* **Custom atlas material** : user's custom atlas material.
	* **New unique material** : new material is generated based on the user's own material.
	
.. _carPrefabCreatorTemplateSettings:
	
Template Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/TemplateSettings.png
	
| **Hull name templates** : keyword phrases for automatic hull searches.

**Wheel name templates** : keyword phrases for automatic wheels searches.
	* **Wheel FR** : forward right wheel.
	* **Wheel FL** : forward left wheel.
	* **Wheel BR** : backward right wheel.
	* **Wheel BL** : backward left wheel.
	* **Wheel Middle** : additional wheels.
	
Preview Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/PreviewSettings.png
	
| **Show preview** : on/off preview image of the prefab on the `Prefab Info` tab.
| **Show additional settings** : on/off display of the additional settings of the prefab on the `Prefab Info` tab.
| **Show custom settings** : on/off display of the custom settings of the prefab on the `Prefab Info` tab.

.. _carPrefabCreatorAdditionalSettings:

Additional Settings
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings.png
	
| **Wheel radius** : wheel radius.
| **Wheel offset** : wheel offset by Y-axis of the vehicle.
| **Suspension length** : suspension length of the vehicle. **[Custom physics vehicles only]**

	.. note::
		Editing addtional parameters affects all cars in `Prefab Info` tab.
	
.. _carPrefabCreatorPrefabSettings:
	
Prefab Info
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabInfo.png
	
Car Info
~~~~~~~~~~~~

* **Prefab** : reference to source prefab.
* **Name** : user's name of the vehicle.
* **ID** : new `ID` entry for :ref:`vehicle collection <vehicleCollection>`.
* **Traffic group** : :ref:`traffic group <pathTrafficGroup>` of the vehicle.
* **Override entity type** : new entity type for selected vehicle (might be useful for specific vehicles such as `tram`).
	* **Entity type**
* **Public transport** : on/off :ref:`public transport <trafficPublic>` feature. (:ref:`Settings <trafficPublicAuthoring>`)
	* **Predefined road** 
	* **Capacity** 
	* **Entries**
* **Wheel radius** : wheel radius. **(can be unique value)**
* **Wheel offset** : wheel offset by Y-axis of the vehicle. **(can be unique value)**
* **Suspension length** : :ref:`traffic group <vehicleCollection>` of the vehicle. **(can be unique value)** **[Custom physics vehicles only]**
		
Buttons
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/Buttons.png
	
| **Scan** : scan the added prefabs and add information about new ones to the `Prefab Info` tab.
| **Create** : create new entity prefabs based on the added prefabs.