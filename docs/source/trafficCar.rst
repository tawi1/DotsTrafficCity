.. _trafficCar:
   
Traffic Car
=====

.. contents::
   :local:
   

How to create
----------------

#. In the Unity toolbar, open `Car Prefab Creator`. More info about :ref:`Car Prefab Creator<carPrefabCreator>`.

	``Spirit604/CityEditor/Car Prefab Creator``
	
	.. image:: /images/entities/trafficCar/carPrefabCreator/CarPrefabCreatorToolbar.png
	
#. Drag & drop source cars from scene or project to `Prefabs` field depends on `Prefab Source Type` parameter.

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabSettings.png
	
#. Configure the :ref:`common settings <carPrefabCreatorCommonSettings>` for creating a car.

	.. image:: /images/entities/trafficCar/carPrefabCreator/CommonSettings.png
	
#. Configure the :ref:`save settings <carPrefabCreatorSaveSettings>` for creating a car.

	.. image:: /images/entities/trafficCar/carPrefabCreator/SaveSettings.png
	
#. Change the :ref:`template settings <carPrefabCreatorTemplateSettings>` depending on the name of the car body (if it is a child) and the pattern of the names of the wheels.

	.. image:: /images/entities/trafficCar/carPrefabCreator/TemplateSettings.png
	
#. Click `Scan` button.

	.. image:: /images/entities/trafficCar/carPrefabCreator/PrefabInfo.png
	
#. In the `Prefab Info` tab, change the name of the enum of the cars if you needed.
#. To create new enums, click the button `Add Enum Types`.
#. After the enums are created, click `Create` to create the prefabs.

Authoring components
----------------

TrafficCarEntityAuthoring
~~~~~~~~~~~~
	
	.. image:: /images/entities/trafficCar/TrafficCarEntityAuthoring.png
	
| **Hull mesh renderer** : vehicle hull mesh renderer reference.
| **Physics shape** : vehicle entity `PhysicsShape` reference.
| **Nav mesh obstacle** : vehicle `NavMeshObstcale` reference.
| **Car model** : selected enum of vehicle.	
| **Faction type** : selected :ref:`faction type <factions>` of vehicle.
| **Car type** : selected :ref:`car type <carType>` of vehicle.
| **Bounds source type** : selected bounds source for the entity bounds.
| **Traffic type** : Selected traffic type (Default, :ref:`Tram, Traffic public<trafficPublic>`).
		
CarWheelAuthoring
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/CarWheelAuthoring.png
	
| **Wheel base** : wheel radius.
| **All wheels** : all wheels of the vehicle.
| **Steering wheels** : wheels that can turn.
	
CarSoundAuthoring
~~~~~~~~~~~~
	
	.. image:: /images/entities/trafficCar/CarSoundAuthoring.png
	
	|
	
| **Min pitch** : minimum pitch of the car engine.
| **Max pitch** : maximum pitch of the car engine.
| **Max load speed** : speed at which the engine has the maximum pitch.
| **Max volume speed** : speed at which the engine has the maximum volume.
| **Min volume** : minimum engine volume.
**Sounds:**
	* **Ignition**
	* **Idle**
	* **Driving**
	* **Horn**
	* **Enter car**
	* **Exit car**		

	.. note::
		:ref:`Fmod plugin<sound>` for sounds should be installed.
		
PhysicsShape & PhysicsBody
~~~~~~~~~~~~

Optional components if the car moves with physics.

	.. include:: trafficCarConfigs.rst
		:start-line : 0