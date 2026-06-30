.. _trafficCar:
   
Traffic Car
=====

.. contents:: 
	:local:
	:depth: 2
   
How To Create
----------------

To start creating traffic vehicles, follow the instructions below based on your desired physics and architecture type.

MonoBehaviour-Based Traffic (Hybrid Mono)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   Before starting, ensure that **World simulation type** is set to `Hybrid mono` in the global :ref:`General settings <generalSettingsConfig>`.

#. Open the :ref:`Car Prefab Creator <carPrefabCreator>` tool from the Unity toolbar: ``Spirit604/CityEditor/Car Prefab Creator``.
#. In the **Prefab** tab, set **Car type** to `Traffic` and drag & drop your vehicle models (make sure source models do not contain any default Colliders, Rigidbodies, or Wheel Colliders).
#. In the **Save** tab, set **Entity type** to `Hybrid entity mono physics`.
#. **Choose your controller integration:**
   
	* **For Arcade (built-in sample):** 
		* Set **Controller type** to `Arcade`. 
		* Set your preset/paths in the **Save** tab.
		* Click **Scan**.
		* Adjust **body/wheel offsets** in the **Prefab Info tab**, and press **Create**. 
		* After generation, ensure the raycast layer in `ArcadeVehicleController` matches your **Ground** layer.
	* **For Custom user controller:** 
		* Set **Controller type** to `Custom user`. 
		* Create and assign an adapter script implementing the `IVehicleInput` interface to link traffic logic with your custom controller (see :ref:`Input info <inputInfo>` and the :ref:`VehicleInput example code <vehicleInputCode>`). 
		* Click **Scan**, adjust **body/wheel offsets and steering angle** in the **Prefab Info tab** to match your custom car's setup, and press **Create**.

#. Once generated, the vehicles are automatically added to the :ref:`vehicle collection <vehicleCollection>` and your selected :ref:`preset <trafficPreset>` by default.
#. Find the :ref:`Hub <roadEntitySubscene>` object in your scene and press the **Copy To Subscene** button (this is required to synchronize the active presets between the main scene and the subscene).
#. Open your `EntitySubScene`, locate the `TrafficCarEntityPoolBakerRef` component on both the main scene and the subscene, and make sure the correct preset is assigned.
#. *(Optional)* To prevent your player-controlled car from pushing or glitching through AI traffic, attach the :ref:`CarPlayerBlocker <carPlayerBlocker>` component to the generated vehicle hull prefab and configure its physics layer.

Standard DOTS Traffic (Simple / Custom Physics)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the :ref:`Car Prefab Creator <carPrefabCreator>` tool from the Unity toolbar: ``Spirit604/CityEditor/Car Prefab Creator``.
#. Drag & drop your source prefabs, configure common settings, choose your physics type (**Simple Physics** or **Custom Physics**), and **adjust body/wheel offsets** in the **Prefab Info tab** to ensure the model aligns correctly. Follow the detailed generator steps inside the :ref:`Car Prefab Creator <carPrefabCreator>` guide.
#. Once generated, the vehicles are automatically added to the :ref:`vehicle collection <vehicleCollection>` by default. You can open the collection to ensure they appear in the list.
#. Make sure that your active :ref:`traffic preset <trafficPreset>` includes these new vehicles.
#. Open the global :ref:`Traffic settings <trafficCarSettings>` and ensure the **Entity type** matches your choice (e.g., `Simple physics entity`).
#. Find the :ref:`Hub <roadEntitySubscene>` object in your scene and press the **Copy To Subscene** button (this is required to synchronize the active presets between the main scene and the subscene).
#. Open your `EntitySubScene`, locate the `TrafficCarEntityPoolBakerRef` component on both the main scene and the subscene, and verify that the correct preset is assigned.
#. **Adjust the specific traffic parameters of the created vehicles based on their physics type:**
   
   * For :ref:`Simple physics <trafficCarSettings>`.
   * For :ref:`Custom physics <customPhysicsVehicle>`.

.. _vehicleType:

Vehicle Physics Types
----------------

.. _customPhysicsVehicle:

Custom Physics
~~~~~~~~~~~~

* Entities that are moved by the custom physical system.
* :ref:`Hybrid Entity Custom Physics <entityType>` & :ref:`Pure Entity Custom Physics <entityType>` types refer to this.
* `Youtube tutorial. <https://youtu.be/uxKg2lklHaw>`_

Authoring components
^^^^^^^^^^^^^^^^^^^^^^

Vehicle Authoring
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/vehicleAuthoring.png
	
Wheel
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/wheel.png
	
| **Wheel mass** : wheel mass.
| **Max steering angle** : max steering angle of the steering wheel in degrees.
| **Power steering** : rate of steering improvement.
| **Custom steering limit** : limiting steering angle based on vehicle speed (Y-axis rate value (1 - max steering angle), X-axis speed in metres per second).
| **Radius** : wheel radius.
| **Width** : wheel width.
| **Apply impulse offset** : applying force offset relative to lower point of wheel (without offsetting the force applied to the lower point of the wheel).

**Cast type:**  
	* **Ray** : raycast by ray.
	* **Collider** : raycast by collider (collider size based on wheel radius and width).
	
| **Cast layer** : physical layer that collides with the wheel.

Suspension
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/suspension.png
	
| **Suspension length** : length of suspension.
| **Stiffness** : spring stiffness of suspension.
| **Damping** : force to return spring to its original length.

Friction
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/friction1.png
	
| **Longitudinal** : forward friction curve (Y-axis - forward slip value, X-axis forward speed in metres per second).
| **Lateral** : lateral friction curve (Y-axis - lateral slip value, X-axis lateral speed in metres per second).
| **Forward friction** : forward friction value.
| **Lateral friction** : lateral friction value.
| **Brake friction** : brake friction value.
| **Drag** : drag value of the vehicle.

Transient Forces
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/transientForce.png
	
Transient force is required to hold the car on an inclined ramp during manual braking.
	
| **Use forward transient force** : on/off forward transient force.
| **Min transient forward speed** : min forward speed when transient force is applied.
| **Max forward friction rate** : max friction for transient force calculated by multiplying the entered rate by the forward friction.
| **Forward relax multiplier** : step of forward force increase per frame.

| **Use lateral transient force** : on/off lateral transient force.
| **Min transient lateral speed** : min lateral speed when transient force is applied.
| **Max lateral friction rate** : max friction for transient force calculated by multiplying the entered rate by the lateral friction.
| **Lateral relax multiplier** : step of lateral force increase per frame.

Brakes
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/brakes.png

| **Brake torque** : torque of brake.
| **Handbrake torque** : torque of handbrake.

Engine
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/engine1.png

| **Torque** : engine torque.
| **Transimission rate** : engine torque to wheel speed ratio.

Scene Settings
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/sceneSettings.png
	
| **Show debug** : on/off debugging for wheel and suspension at runtime (`VehicleCustomDebugger`).
| **Show suspension origin** : on/off display of suspension origin.
| **Show suspension** : on/off display of suspension.

**Origin move:**
	* **Disabled** : disabled handle.
	* **Wheel** : on/off handle for wheel origin.
	* **Suspension origin** : on/off handle for suspension origin.
	* **Suspension** : on/off handle for suspension and wheel origin.

Template Settings
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/templateSettings.png

**Tabs:**
	* **Create new** : create a new template settings.
	* **Copy from template** : copy settings from the selected template.
	* **Save to template** : save settings to the selected template.
	
**Copy settings type:**
	* **Physics settings** : copy the physics settings (mass, damping, gravity) of the `PhysicsBody` component.
	* **Center of mass** : copy the center of mass local position of the `PhysicsBody` component.
	* **Offsets** : copy the local offset of the wheels.
	* **Settings** : copy the settings of `the VehicleAuthoring` component.

Wheel Refs
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/wheelRefs.png

| **Wheel** : reference to wheel.
| **Driving** : on/off driving force for the wheel.
| **Brake** :  on/off braking force for the wheel.
| **Brake rate** : brake rate.
| **Handbrake rate** : handbrake rate.

PhysicsBody
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/physicsBody.png
	
PhysicsShape 
""""""""""""""""""

	.. image:: /images/entities/trafficCar/custom/physicsShape.png
	`Example`

.. _simplePhysicsVehicle:

Simple Physics
~~~~~~~~~~~~

* Entities moved by the simple physical system (by simply adding the physics velocity to the physics body).
* :ref:`Settings <trafficCarSettings>`.
* :ref:`Hybrid entity simple physics <entityType>` & :ref:`Pure entity simple physics <entityType>` types refer to this.

Authoring components
^^^^^^^^^^^^^^^^^^^^^^

CarWheelAuthoring
""""""""""""""""""

	.. image:: /images/entities/trafficCar/CarWheelAuthoring.png
	
| **Wheel base** : wheel radius.
| **All wheels** : all wheels of the vehicle.
| **Steering wheels** : wheels that can turn.

PhysicsBody
""""""""""""""""""

	.. image:: /images/entities/trafficCar/PhysicsBody.png
	
PhysicsShape 
""""""""""""""""""

	.. image:: /images/entities/trafficCar/physicsShape.png
	`Example`

Optional components if the car moves with physics.

.. _noPhysicsVehicle:

No Physics
~~~~~~~~~~~~

* :ref:`Pure entities <pureEntity>` that moved by transform system without physics.
* Contains the same components as :ref:`Simple Physics <simplePhysicsVehicle>`.
* :ref:`Settings <trafficCarSettings>`.
* :ref:`Pure entity no physics <entityType>` type refer to this.


.. _hybridMonoVehicle:

Hybrid Mono
~~~~~~~~~~~~

* Before using this vehicle type, make sure that you selected `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>`.
* :ref:`Hybrid entities <hybridEntity>` that moved by custom monobehaviour controller.
* :ref:`Hybrid entity mono physics <entityType>` type refer to this.
* Full creation process is described in the :ref:`How To Create <trafficCar>` section above.

.. _inputInfo:

Input info
~~~~~~~~~~
* Throttle [1] : forward motion.
* Throttle [-1] : reverse motion.
* Throttle [0] : hand brake.
* Throttle [-0.9] : braking, for example, if the current speed is higher than permitted. (the value can be changed in the :ref:`Traffic settings <trafficCarSettings>`)
* Steering [-1, 1]

.. _vehicleInputCode:

VehicleInput example code
~~~~~~~~~~~~~~~~~~~~~~~~~

	..  code-block:: r

		public class UVC_adapter : MonoBehaviour, IVehicleInput
		{
			// Replace by your custom controller script.
			// The example uses a "Universal Vehicle Controller".
			// https://assetstore.unity.com/packages/tools/physics/universal-vehicle-controller-plus-176314
			public UVC_AIControl carControllerInput;

			public float Throttle
			{
				get => carControllerInput.Acceleration;
				set
				{
					if (value > 0)
					{
						carControllerInput.SetAcceleration(value);
						carControllerInput.SetBrakeReverse(0);
						carControllerInput.SetHandBrake(false);
					}
					else
					{
						carControllerInput.SetAcceleration(0);
						carControllerInput.SetBrakeReverse(Mathf.Abs(value));

						if (value == 0)
							carControllerInput.SetHandBrake(true);
					}
				}
			}

			public float Steering { get => carControllerInput.Horizontal; set => carControllerInput.SetSteer(value); }
			public bool Handbrake { get => carControllerInput.HandBrake; set => carControllerInput.SetHandBrake(value); }

			public void SwitchEnabledState(bool isEnabled)
			{
				carControllerInput.enabled = isEnabled;
			}
		}

.. _carPlayerBlocker:

Car Player Blocker
^^^^^^^^^^^^^^^^^^^^^^

The ``CarPlayerBlocker`` component is designed specifically for **Hybrid Mono** vehicles. It prevents a custom player physics controller from pushing or moving AI traffic vehicles upon collision. 

It achieves this by dynamically creating an independent kinematic collider on a dedicated physics layer. This layer forces the player's controller to recognize the traffic car as an immovable obstacle, while the traffic car itself ignores this internal blocker collider to prevent self-jittering.

.. note:: 
   This component works **only** for vehicles with the `Hybrid entity mono physics` type. It does not affect Pure DOTS entities.

How It Works
""""""""""""""

1. **Editor Generation:** The editor script copies the dimensions and center boundaries of your vehicle's main source collider (supports ``BoxCollider`` or ``MeshCollider``).
2. **Layer Isolation:** It places this newly generated box collider onto a custom physics layer (e.g., `PlayerBlocker`).
3. **Kinematic Rigidbody:** A kinematic ``Rigidbody`` is automatically attached to the blocker object, making it completely unyielding to the player's physical forces.
4. **Collision Filtering:** At runtime (in ``Awake``), the script automatically configures Unity's physics engine to ignore collisions between the vehicle's driving colliders and this blocker collider.

Inspector Parameters
""""""""""""""""""""

| **Source Collider** : The main physical collider of the traffic vehicle.
| **Player Blocker Layer** : The physics layer intended to collide exclusively with your Player Controller.
| **Size Offset** : Additional padding added to the blocker collider dimensions to detect or block the player slightly outside the mesh bounds.
| **Physics Switcher** : Reference to the ``PhysicsSwitcher`` component to properly reset and synchronize collider states during culling.
| **Created Collider** : The automatically generated ``BoxCollider`` slot.

Step-by-Step Configuration
""""""""""""""""""""""""""

Follow these steps to set up the blocker for your vehicles:

#. **Create a New Layer:** Open your Unity project settings and add a new layer (e.g., name it ``PlayerBlocker``).
#. **Attach the Component:** Add the ``CarPlayerBlocker`` component to your vehicle's hull prefab.
#. **Configure the Blocker:** 
	* Assign the **Source Collider** and the **Physics Switcher**.
	* Set the **Player Blocker Layer** to the layer you created in Step 1.
	* Click the **Create** button in the inspector. This will spawn a child GameObject named ``PlayerBlocker`` with a box collider and a kinematic rigidbody.
#. **Configure the Layer Collision Matrix:**
	* Navigate to **Project Settings -> Physics**.
	* Locate the **Layer Collision Matrix** grid.
	* For the ``PlayerBlocker`` layer, **untick all checkboxes** except for the layer used by your **Player** character/vehicle controller. 

.. note:: 
   This matrix setup ensures the blocker collider interacts *only* with the player and remains completely invisible to traffic, NPCs, raycasts, and ground physics layers.
   
Components
""""""""""""""

**CarEntityAdapter**

	.. image:: /images/entities/trafficCar/hybridMono/CarEntityAdapter.png
	
Component to syncronize gameobject & entity, also to switch physics & scripts of the :ref:`vehicle <hybridMonoVehicle>` when :ref:`cull state <cullPointStates>` changes with `PhysicsSwitcher` & `ScriptSwitcher` components.
	
	.. note:: You can turn off traffic physics culling in the :ref:`Traffic settings <trafficCarSettings>`.
	
**PhysicsSwitcher**
	
	.. image:: /images/entities/trafficCar/hybridMono/PhysicsSwitcher.png
	
Component to on/off physics of the vehicle.
	
**ScriptSwitcher**
	
	.. image:: /images/entities/trafficCar/hybridMono/ScriptSwitcher.png
	
Component to on/off scripts of the vehicle.

Common Authoring Components
----------------

.. _trafficCarEntityAuthoring:

TrafficCarEntityAuthoring
~~~~~~~~~~~~
	
	.. image:: /images/entities/trafficCar/TrafficCarEntityAuthoring.png
	
Main component of traffic entity **[required]**.
	
| **Hull mesh renderer** : vehicle hull mesh renderer reference.
| **Physics shape** : vehicle entity `PhysicsShape` reference.
| **Faction type** : selected :ref:`faction type <factions>` of vehicle.
| **Car type** : selected :ref:`car type <carType>` of vehicle.
| **Bounds source type** : selected bounds source for the entity bounds.
| **Traffic group** : selected :ref:`traffic group <pathTrafficGroup>`.

Shared Settings
~~~~~~~~~~~~

Each vehicle has a common set of settings that are described :ref:`here <vehicleCollection>`

NavMeshObstacleAuthoring
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/NavMeshObstacleAuthoring.png
	
`NavMeshObstacleData` entity component for runtime loading of `NavMeshObstacle` objects for :ref:`pedestrian navigation <pedestrianNavmeshNavigation>`. Make sure, that option is enabled in the :ref:`traffic settings <trafficNavMeshObstacle>` **[optional]**.
	
CarSoundAuthoring
~~~~~~~~~~~~

	.. image:: /images/entities/trafficCar/CarSoundAuthoring.png
	
Component for vehicle :ref:`sounds <sharedSoundSettings>` **[optional]**.
	
HealthAuthoring
~~~~~~~~~~~~

Vehicle health component for damage system (DOTS only) **[optional]**.

CarDamageEngineAuthoring
~~~~~~~~~~~~

Component for visual presentation of damage in the damage systems (DOTS only) **[optional]**.

PlayerTargetAuthoring
~~~~~~~~~~~~

Component for player targeting systems **[optional]**.

CullState Info
----------------

:ref:`States <cullPointInfo>`
~~~~~~~~~~~~

* **Culled** : entity is destroyed.

* **CloseToCamera:** 
	* Cull physics (if :ref:`enabled <trafficCarOtherSettings>`) : :ref:`custom physics <customPhysicsVehicle>` & :ref:`simple physics <simplePhysicsVehicle>` temporarily converted to :ref:`no physics <noPhysicsVehicle>` entity.
	* Cull wheel (if :ref:`enabled <trafficCarOtherSettings>`) : disabling wheel rotating.

* **InVisionOfCamera** : entity fully enabled.

.. _trafficParking:

Parking
----------------

Сar parking consists of the following states:

Entering parking states
~~~~~~~~~~~~

#. The car has chosen the path containing the :ref:`parking node <trafficNode>`.
#. The car links the :ref:`parking node <trafficNode>` to prevent it from being selected by other cars (the list of linked nodes can be customized :ref:`here <trafficRoadConfig>`).
#. When the car reaches the :ref:`parking node <trafficNode>`, the car position correction is activated for precise parking (if disabled in the :ref:`parking config <trafficCarParkingConfig>`, this step is skipped).
#. Stopping the engine state is starting (if enabled in the :ref:`stopping engine config <carStoppingConfig>` & vehicle in view of camera's player).
#. Pedestrian gets out of the car.

Exiting parking states
~~~~~~~~~~~~

#. The Pedestrian enters the :ref:`pedestrian parking node <pedestrianNode>`, if available.
#. The parking car removes link with :ref:`TrafficNode <trafficNode>`.
#. Ignition state system starts (if enabled in :ref:`ignition config <carIgnitionConfig>`).
#. Once the car has started the engine, the car starts moving.

.. _trafficAvoidance:

Avoidance
----------------

| Avoidance is used in the case of stuck vehicles.
Currently enabled in the following situations:
	* A cyclical obstacle where cars get stuck in each other (:ref:`avoidance config <trafficAvoidanceConfig>`).
	* A car has collided frontally with another car (:ref:`collision config <trafficCollisionConfig>`).
	
	.. image:: /images/entities/trafficCar/avoidance/AvoidanceExample1.png
	`Cyclical obstacle example.`
	
	.. image:: /images/entities/trafficCar/avoidance/AvoidanceExample2.png
	`Avoiding cyclical obstacle example.`
	
	.. note:: Test scene :ref:`example <trafficTestSceneAvoidance>`.

.. _trafficEntitySelection:
		
Entity Selection
----------------
		
Entity can be retrieved using one of these methods:
		
Pure DOTS
~~~~~~~~~~~~

* Create a new gameobject with `EntitySelectionService` component
* Use world position to get the nearest entity for that position.

	..  code-block:: r
	
		public Entity TryToSelectEntity(Vector3 worldPosition)
		{
			return EntitySelectionService.Instance.SelectEntity(worldPosition, EntityType.Traffic, 1f);
		}

Hybrid Mono
~~~~~~~~~~~~

Entity can be retrieved if the car has a collider:

	..  code-block:: r
	
			private Entity GetEntity()
			{
				Entity entity = Entity.Null;
				
			    if (Physics.Raycast(transform.position, Vector3.forward, out hit, 1.0f))
				{
					var hybridEntityRef = hit.collider.GetComponent<IHybridEntityRef>();
					entity = hybridEntityRef.RelatedEntity;
				}				
				
				return entity;
			}		

.. _trafficRail:

Rail Movement
----------------

The `Rail movement` is used to drive the vehicle precisely along the :ref:`path <path>`, which can be useful in small enclosed :ref:`parking areas <path>`, for example.
To enable rail movement, tick on the `Rail` parameter in the :ref:`path settings <pathSettings>`.
Open the :ref:`rail config <trafficRailConfig>` to adjust the `Rail` parameters (DOTS only).

	.. note:: Enabled by default for :ref:`trams <trafficPublicType>`.

Obstacle Detection
----------------

.. _trafficCarRaycastInfo:

Raycast
~~~~~~~~~~~~

**Config**

:ref:`TrafficCarRaycastConfig. <trafficCarRaycastConfig>`

**Debugger**

:ref:`TrafficCarRaycastDebugger. <trafficCarRaycastDebugger>`

**Modes**

* `Hybrid mode` : raycast is activated only when the selected targets are close to the car.
* `Raycast only` : raycasts are sent constantly.
	
To define raycast targets for `Hybrid` or `Raycast only` modes, redefine the `GetTargetQuery` method in the ``TrafficCarRaycastObstacleTargetQueryProvider`` class, which returns the `EntityQuery <https://docs.unity.cn/Packages/com.unity.entities@1.0/api/Unity.Entities.EntityQuery.html>`_ of the targets.

..  code-block:: r

	public static EntityQuery GetTargetQuery(
			   SystemBase sourceSystem,
			   TrafficCarDetectObstacleMode trafficCarDetectObstacleMode,
			   TrafficCarDetectNpcMode trafficCarDetectNpcMode,
			   out CollisionFilter tempRaycastCollisionFilter,
			   out CollisionFilter raycastAlwaysCollisionFilter);
		
* :ref:`TrafficCarDetectObstacleMode. <trafficDetectObstacleMode>`
* :ref:`TrafficCarDetectNpcMode. <trafficDetectObstacleMode>`
* **Hybrid Mode Filter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of hybrid raycast mode.
* **Raycast Only Filter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of raycast only mode.
		
	.. note:: 
		* You can also dynamically change the raycast target for `Hybrid mode` by adding or removing the `TrafficCustomRaycastTargetTag` component.
		* Layer constants are stored in the `ProjectConstants.cs` file.
		
Obstacle Avoidance
----------------

If you want the traffic to avoid obstacles, follow these steps:

* Make sure that obstacle detection is set to either `Hybrid` or `Raycast` in the :ref:`Traffic config <trafficDetectObstacleMode>`.
* Ensure that `Advanced avoidance` is enabled in the :ref:`Collision config <trafficCollisionConfig>`.
* Make sure that the traffic :ref:`Raycast config <trafficCarRaycastConfig>` includes an obstacle layer.
* Add components to the obstacle object from the example below, depending on the type of obstacle.

Player Character
~~~~~~~~~~~~

	.. image:: /images/configs/player/PlayerCharacterAvoidance.png
	
	.. note:: Make sure that `Player Npc Hybrid Component` is removed.

Player Car
~~~~~~~~~~~~

	.. image:: /images/configs/player/PlayerCarAvoidance.png

Dynamic Obstacle
~~~~~~~~~~~~

	.. image:: /images/configs/player/CustomObstacleAvoidance.png

Static Obstacle
~~~~~~~~~~~~

	.. image:: /images/configs/player/CustomStaticObstacleAvoidance.png
	
Left-hand Drive
----------------

To make the traffic left-hand drive:

* Find & open ``ProjectConstants`` script.
* Change the ``LaneHandDirection`` variable to ``-1``.

	.. note:: Changing this parameter will only affect newly created scenes. Old scenes with a different lane direction will not work.
	
Pathfinding
----------------

Custom Point
~~~~~~~~~~~~

To set a custom destination for a specific traffic car, do the following:

* Create a new gameobject with ``EntitySelectionService`` component.
* Create a new gameobject with ``TrafficCustomPathService`` component.
* Use this sample code:

	..  code-block:: r

		private void Awake()
		{
			PathHashMapSystem.Register();
		}

		public void SetEntity(Vector3 trafficPosition, Vector3 destination)
		{
			var trafficEntity = EntitySelectionService.Instance.SelectEntity(trafficPosition, EntitySelectionService.EntityType.Traffic, 2f);
			TrafficCustomPathService.Instance.SetFollowPath(trafficEntity, destination);
		}
		
* Use the ``OnStatusUpdated`` callback in ``TrafficCustomPathService`` to listen to the current state of the traffic car's pathfinding.
		
Custom Node
~~~~~~~~~~~~

To set a custom node destination for a specific traffic car, do the following:

* Create a new gameobject with ``EntitySelectionService`` component.
* Create a new gameobject with ``TrafficCustomPathService`` component.
* Use this sample code:

	..  code-block:: r
	
		private void Awake()
		{
			PathHashMapSystem.Register();
		}

		public void SetEntity(Vector3 trafficPosition, Vector3 destination)
		{
			var trafficEntity = EntitySelectionService.Instance.SelectEntity(trafficPosition, EntitySelectionService.EntityType.Traffic, 2f);
			var destinationPath = PathHashMapSystem.GetClosestPath(destination);

			TrafficCustomPathService.Instance.SetFollowPath(trafficEntity, destinationPath);
		}
		
* Use the ``OnStatusUpdated`` callback in ``TrafficCustomPathService`` to listen to the current state of the traffic car's pathfinding.
* As an alternative, you can check the ``TrafficPathSelector`` prefab for an interactive user-selected path used in the `RuntimeTileRoad Demo` scene (runtime sample should be imported & :ref:`RUNTIME_ROAD <runtimeTileDemo>` scripting define added).