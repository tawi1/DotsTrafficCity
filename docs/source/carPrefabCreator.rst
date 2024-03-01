.. _carPrefabCreator:

Car Prefab Creator
=====

`Youtube tutorial. <https://youtu.be/7or3H0GB1HQ>`_

How To Use
----------------

#. From the `Unity` toolbar, open `Car Prefab Creator`.

	``Spirit604/CityEditor/Car Prefab Creator``
	
	.. image:: /images/entities/trafficCar/carPrefabCreator/CarPrefabCreatorToolbar.png
	
#. Drag & drop source cars from scene or project to `Prefabs` field depends on `Prefab Source Type` parameter.

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabSettings.png
	
#. Configure the :ref:`Common settings <carPrefabCreatorCommonSettings>` for creating a car.

	.. image:: /images/entities/trafficCar/carPrefabCreator/CommonSettings.png
	
#. If the vehicle is the :ref:`Simple vehicle <simplePhysicsVehicle>` type, enable `Add wheel offset` in the :ref:`Common settings <carPrefabCreatorCommonSettings>` tab.

	.. image:: /images/entities/trafficCar/custom/physicsShape.png
	:ref:`Custom physics entity <customPhysicsVehicle>` `shape result example`
	
	.. image:: /images/entities/trafficCar/physicsShape.png
	:ref:`Simple physics entity <simplePhysicsVehicle>` `shape result example`
	
#. Configure the :ref:`Save settings <carPrefabCreatorSaveSettings>` for creating a car.

	.. image:: /images/entities/trafficCar/carPrefabCreator/SaveSettings.png
	
#. Change the :ref:`Template settings <carPrefabCreatorTemplateSettings>` depending on the name of the car body (if it is a child) and the pattern of the names of the wheels.
#. Click `Scan` button.
#. Open :ref:`Additional Settings <carPrefabCreatorAdditionalSettings>` tab, adjust common settings for all vehicles.

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings.png

#. After, open :ref:`Prefab Info <carPrefabCreatorPrefabInfo>` tab, adjust unique settings for each vehicle.

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabInfo.png
	
#. Once all the settings have been customised, click `Create` to create the prefabs.

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
| **Vehicle data collection** : reference to the :ref:`collection <vehicleCollection>` of all vehicles.
| **Traffic car convert template** : template which contains traffic prefab template.
| **Player car convert template** : template which contains player prefab template.
		
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
	* **Scene**: add the created prefabs to an existing :ref:`preset <trafficPreset>` in the scene.
	* **Selected**: add the created prefabs to selected :ref:`preset <trafficPreset>`.

**New preset settings:**
	* **Assign new preset to scene** : :ref:`preset <trafficPreset>` will replace an existing :ref:`preset <trafficPreset>` on scene.
	* **New preset path** : project path where to create a new :ref:`preset <trafficPreset>`.
	* **New preset name** : new :ref:`preset <trafficPreset>` name.
	
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

Common Settings
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings.png
	
| **Wheel radius** : wheel radius.
| **Wheel offset** : wheel offset by Y-axis of the vehicle.
| **Suspension length** : suspension length of the vehicle. **[Custom physics vehicles only]**

	.. note::
		* Editing additional parameters will affect all cars in the :ref:`Prefab Info <carPrefabCreatorPrefabInfo>` tab, to make unique parameters check the toolbox opposite on the parameter in the :ref:`Prefab Info <carPrefabCreatorPrefabInfo>`.
		* Arrow-button applies the setting for the selected parameter.
		
Physics
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings2-1.png
	
| **Size offset** : size offset of physics shape.
| **Center offset** : center offset of physics shape.
| **Center of mass** : center of mass of the vehicle.
| **Bevel radius** : bevel radius of physics shape.
| **Mass** : mass of the vehicle.
 
Info Tab
^^^^^^^^^^^^^^^^^^^^^^

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings2-2.png

Graphics
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings3-1.png
	
**Wheel source type:** 
	* **Model unique** : the wheels remain as in the original model.
	* **Shared from model** : the wheel model selected by the user from the original model is used for all wheels.
	* **Shared all** : the wheel model selected by the user shared between all wheels.
	
**Wheel rotation type [shared wheel only]:** 
	* **Source** : the wheel rotation remains unchanged.
	* **Flip left row** : rotate the wheel in the left-hand row by 180° if you are using the wheel model from the right-hand row..
	* **Flip right row** : rotate the wheel in the left-hand row by 180° if you are using the wheel model from the right-hand row..
	
**Has lods:** on/off LODs for vehicle.
	* **Lod 0, 1, 2 screen size** : screen size of LOD.
	
	.. note:: 
		Wheel sharing is useful for using the same wheel model for all wheels to reduce drawcalls.
	
Info Tab
^^^^^^^^^^^^^^^^^^^^^^

	.. image:: /images/entities/trafficCar/carPrefabCreator/AdditionalSettings3-2.png
	
.. _carPrefabCreatorPrefabInfo:
	
Prefab Info
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabInfo.png
	
Car Info
~~~~~~~~~~~~

* **Prefab** : reference to source prefab.
* **Name** : user's :ref:`name <carModel>` of the vehicle.
* **ID** : new :ref:`ID <trafficId>` entry for :ref:`vehicle collection <vehicleCollection>`.
* **Traffic group** : :ref:`traffic group <pathTrafficGroup>` of the vehicle.

* **Override entity type** : new :ref:`entity type <trafficCarSettings>` for selected vehicle (might be useful for specific vehicles such as `tram`).
	* **Entity type**
	
* **Public transport** : on/off :ref:`public transport <trafficPublic>` feature. (:ref:`Settings <trafficPublicAuthoring>`)
	* **Predefined road** 
	* **Capacity** 
	* **Entries**
	
* **Settings type:** 
	* **New** : user-defined settings.
	* **Template** : vehicle settings are copied from the selected template **[custom physics vehicle only]**.
	* **Clone model** : vehicle settings are copied from the selected `CarModel` in the list.
	
* **Wheel radius** : wheel radius. **(can be unique value)**
* **Wheel offset** : wheel offset by Y-axis of the vehicle. **(can be unique value)**
* **Suspension length** : suspension length of the vehicle. **(can be unique value)** **[Custom physics vehicles only]**
		
Buttons
----------------

	.. image:: /images/entities/trafficCar/carPrefabCreator/Buttons.png
	
| **Scan** : scan the added prefabs and add information about new ones to the `Prefab Info` tab.
| **Create** : create new entity prefabs based on the added prefabs.