.. _trafficCar:
   
Traffic Car
=====

.. contents::
   :local:
   
How To Create
----------------

#. Create a vehicle using the :ref:`Car Prefab Creator <carPrefabCreator>` tool (for example :ref:`Simple physics entity <entityType>` type).

	.. image:: /images/entities/trafficCar/howTo/Step1.png
	:ref:`Car Prefab Creator <carPrefabCreator>` final step example.
	
#. Make sure, that the :ref:`vehicle collection <vehicleCollection>` contains vehicle you have created.

	.. image:: /images/entities/trafficCar/howTo/Step2.png
	
#. Make sure, that the :ref:`preset <trafficPreset>` contains the vehicle.

	.. image:: /images/entities/trafficCar/howTo/Step3.png

#. Open the :ref:`Traffic settings <trafficCarSettings>` and select the :ref:`Simple physics entity <entityType>` type (if you have created a `Simple physics entity`).

	.. image:: /images/entities/trafficCar/howTo/Step4.png
	
#. Open the :ref:`Hub <roadEntitySubscene>` object in the scene and press the `Copy To Subscene` button.

	.. image:: /images/entities/trafficCar/howTo/Step5.png
	
#. Open the `EntitySubScene`, find the `TrafficCarEntityPoolBakerRef` gameobject, make sure the correct :ref:`preset <trafficPreset>` is assigned.

	.. image:: /images/entities/trafficCar/howTo/Step6.png
	
#. Adjust the traffic settings of the created vehicles.
	* For :ref:`simple physics <trafficCarSettings>`.
	* For :ref:`custom physics <customPhysicsVehicle>`. 

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

	.. image:: /images/entities/trafficCar/custom/friction.png
	
| **Longitudinal** : forward friction curve (Y-axis - forward slip value, X-axis forward speed in metres per second).
| **Lateral** : lateral friction curve (Y-axis - lateral slip value, X-axis lateral speed in metres per second).
| **Forward friction** : forward friction value.
| **Lateral friction** : lateral friction value.
| **Brake friction** : brake friction value.

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

	.. image:: /images/entities/trafficCar/custom/engine.png

| **Torque** : engine torque.
| **Transimission rate** : engine torque to wheel speed ratio.
| **Drag** : drag value of the vehicle.

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
	* **Create new** : create new template settings.
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

Vehicle health component for damage system **[optional]**.

CarDamageEngineAuthoring
~~~~~~~~~~~~

Component for visual presentation of damage in the damage systems **[optional]**.

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

.. _trafficRail:

Rail Movement
----------------

The `Rail movement` is used to drive the vehicle precisely along the :ref:`path <path>`, which can be useful in small enclosed :ref:`parking areas <path>`, for example.
To enable rail movement, tick on the `Rail` parameter in the :ref:`path settings <pathSettings>`.
Open the :ref:`rail config <trafficRailConfig>` to adjust the `Rail` parameters.

	.. note:: Enabled by default for :ref:`trams <trafficPublicType>`.

Obstacle Detection
----------------

.. _trafficCarRaycastInfo:

Raycast
~~~~~~~~~~~~

:ref:`Config. <trafficCarRaycastConfig>`

Modes:
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
* **Temp raycast CollisionFilter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of hybrid raycast mode.
* **Raycast always CollisionFilter** : `collision filter <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/collision-queries.html#filtering>`_ of raycast only mode.
		
	.. note:: You can also dynamically change the raycast target by adding or removing the `TrafficCustomRaycastTargetTag` component.