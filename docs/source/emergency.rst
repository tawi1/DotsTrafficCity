.. _emergencyVehicle

Emergency Vehicle
=================

Overview
--------

The **Emergency Vehicle System** simulates priority emergency vehicles (such as police cars, ambulances, and fire trucks) navigating through city traffic. When an emergency vehicle activates its siren, surrounding traffic dynamically clears a corridor by performing intelligent avoidance maneuvers (lane changing, pulling over to the shoulder, or yielding in place).

This system supports both **AI Traffic Entities** and **Player-Controlled Hybrid Vehicles**.

.. note::
   Traffic vehicles inside the siren radius evaluate approaching emergency vehicles in real-time using high-performance DOTS ECS jobs compiled with Burst.

Key Features & Workflow
-----------------------

1. **Siren Radius & Corridor Clearance**: When active, the siren broadcast radius alerts nearby traffic entities to evaluate whether they block the emergency vehicle's path.
2. **Dynamic Traffic Avoidance**:

   - **Lane Changing**: Vehicles change to adjacent lanes if available and unoccupied.
   - **Pull Over**: On single-lane roads or blocked lanes, vehicles slow down, pull over to the shoulder (right side by default, or left on one-way roads), and wait in a safe zone until the emergency vehicle passes.
   - **Yield / Intersection Clearance**: Vehicles blocking intersections ignore red lights to clear the way or stop in place if pull-over is not possible.

3. **Priority Overrides**: Active emergency vehicles automatically set pathing priority overrides and ignore traffic lights to maintain continuous movement.

Setup & Usage Steps
-------------------

For Traffic Vehicles (AI)
~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Enable Global Feature Support**:
   In :ref:`General settings <generalSettingsConfig>`, ensure that **Emergency Vehicle Support** is enabled.

2. **Add Authoring Component**:
   Add the ``EmergencyVehicleAuthoring`` component to your emergency traffic vehicle entity prefab.

3. **Configure Siren Settings**:

   - Set **Siren Radius** (e.g., ``40.0`` meters).
   - Set **Active By Default** if the siren should be turned on immediately upon spawning.

4. **Bake / Runtime Activation**:
   The baker automatically attaches ``EmergencyVehicleComponent`` during entity conversion.

For Player-Controlled Vehicles (Hybrid)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Enable Global Feature Support**:
   In :ref:`General settings <generalSettingsConfig>`, ensure that **Emergency Vehicle Support** is enabled.
   
2. **Attach Authoring Component**:
   Add ``EmergencyVehicleAuthoring`` to the root GameObject or parent of your hybrid player car.

3. **Runtime Initialization**:
   During vehicle instantiation, call ``Initialize()`` via your vehicle setup pipeline to bind the ``EmergencyVehicleComponent`` to the player's ECS Entity.

4. **Control Siren at Runtime**:
   Use C# API scripts (e.g., keypress handlers) to toggle siren state on and off dynamically.

C# API Examples
---------------

Toggling Siren on Player / Hybrid Vehicle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To activate or deactivate the siren on a hybrid player vehicle via ``EmergencyVehicleAuthoring``:

.. code-block:: csharp

    using Spirit604.DotsCity.Simulation.Traffic;
    using UnityEngine;

    public class PlayerSirenController : MonoBehaviour
    {
        [SerializeField] private EmergencyVehicleAuthoring emergencyAuthoring;

        private void Update()
        {
            // Toggle siren with the "H" key
            if (Input.GetKeyDown(KeyCode.H))
            {
                bool currentState = emergencyAuthoring.GetActiveState();
                emergencyAuthoring.SwitchSirenActive(!currentState);
                
                Debug.Log($"Siren State: {!currentState}");
            }
        }
    }

Toggling Emergency Priority State via Entity Manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To programmatically convert a standard traffic vehicle entity into an emergency priority vehicle using ``TrafficEmergencyEntityUtils``:

.. code-block:: csharp

    using Spirit604.DotsCity.Simulation.Traffic;
    using Unity.Entities;

    public class EmergencyStateSystemExample
    {
        public void SetEmergencyMode(EntityManager entityManager, Entity vehicleEntity, bool enableEmergency)
        {
            // Modifies Priority, PriorityOverride, and sets TrafficState to IgnoreTrafficLight
            TrafficEmergencyEntityUtils.SwitchEmergencyState(entityManager, vehicleEntity, enableEmergency);
        }
    }

Configuration Reference
-----------------------

EmergencyVehicleAuthoring Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :widths: 25 15 60
   :header-rows: 1

   * - Field
     - Type
     - Description
   * - ``sirenRadius``
     - ``float``
     - The detection and influence radius (in meters) within which surrounding traffic will detect the siren and execute avoidance behaviors.
   * - ``activeByDefault``
     - ``bool``
     - If enabled, the siren state starts as active when the entity is baked or initialized at runtime.

TrafficEmergencyConfigAuthoring Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Detailed breakdown of all parameters driving the emergency avoidance FSM:

**Delays & Speeds**

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - ``yieldCorridorResumeDelay``
     - ``float``
     - Delay in seconds before resuming normal driving after stopping/yielding in lane.
   * - ``waitingInSafeZoneResumeDelay``
     - ``float``
     - Delay in seconds before leaving the safe shoulder zone after the emergency vehicle passes.
   * - ``targetPullOverSpeed``
     - ``float``
     - Target cruising speed (in km/h) while vehicles decelerate and search for a clear pull-over spot.
   * - ``speedThresholdTolerance``
     - ``float``
     - Speed tolerance threshold when checking if the vehicle has slowed down enough to start pulling over.
   * - ``waitingForClearSpeedMultiplier``
     - ``float``
     - Multiplier applied to lane speed limit while a vehicle waits in-lane for adjacent lanes to clear.

**Pull Over Distances**

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - ``pullOverLateralOffset``
     - ``float``
     - Lateral distance (in meters) offset from the lane center to the shoulder.
   * - ``pullOverForwardStep1``
     - ``float``
     - Forward distance waypoint for Step 1 (diagonal transition to shoulder).
   * - ``pullOverForwardStep2``
     - ``float``
     - Forward distance waypoint for Step 2 (aligning parallel to shoulder).
   * - ``pullOverAchieveDistance``
     - ``float``
     - Distance threshold to consider pull-over waypoints reached.
   * - ``resumeLaneAchieveDistance``
     - ``float``
     - Distance threshold to consider the return-to-lane waypoint reached.

**Emergency Detection Zone & Corridor**

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - ``speedRadiusMultiplier``
     - ``float``
     - Speed-dependent multiplier that dynamically expands the siren radius at higher speeds.
   * - ``forwardDirectionDotThreshold``
     - ``float``
     - Dot product threshold defining the forward sector of the emergency detection zone.
   * - ``sameDirectionDotThreshold``
     - ``float``
     - Dot product alignment threshold to check if vehicles travel in the same direction.
   * - ``rearJunctionDotThreshold``
     - ``float``
     - Dot product threshold for detecting emergency vehicles approaching from behind on junctions.
   * - ``defaultLookAheadTime``
     - ``float``
     - Look-ahead time (in seconds) used to project future positions during corridor calculations.
   * - ``defaultMaxAvoidanceDist``
     - ``float``
     - Maximum distance for corridor avoidance checks.
   * - ``dangerCorridorHalfWidth``
     - ``float``
     - Inner corridor half-width where vehicles are in immediate collision danger.
   * - ``defaultCorridorHalfWidth``
     - ``float``
     - Outer corridor half-width defining the emergency path zone.
   * - ``rearBehindThreshold``
     - ``float``
     - Distance behind the emergency vehicle past which vehicles can safely resume normal state.
   * - ``criticalBrakeDistance``
     - ``float``
     - Distance threshold to force a hard stop if an oncoming emergency vehicle approaches and target lane is blocked.

**Lateral Hazards & Position**

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - ``maxLateralAvoidanceDistance``
     - ``float``
     - Maximum lateral offset considered for hazard detection.
   * - ``allowLeftPullOver``
     - ``bool``
     - Allows pulling over to the left shoulder on multi-lane two-way roads if the right side is blocked and vehicle is in the leftmost lane.
   * - ``maxPhysicalLateralOffsetThreshold``
     - ``float``
     - Maximum physical lateral offset allowed before forcing opposite side pull-over.

**Intersection & Safety Radius**

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - ``defaultMaxStopDistance``
     - ``float``
     - Maximum distance from intersection entry line to stop when yielding.
   * - ``defaultSafetyRadius``
     - ``float``
     - Safety radius (in meters) around intersections and path clearance zones.
   * - ``defaultPullOverClearanceRadius``
     - ``float``
     - Radius checked around pull-over target points to ensure shoulder is clear of obstacles/parked cars.
   * - ``defaultPullOverExtraSafetyOffset``
     - ``float``
     - Additional longitudinal buffer offset to prevent clipping adjacent vehicles during pull-over.

Fine-Tuning Guidelines & Scenario Recommendations
-------------------------------------------------

Setting up the configuration depends heavily on road widths, city speed profiles, and traffic density. Below are key recommendations for common project scenarios:

1. High-Density Urban Traffic (Narrow Streets & Frequent Intersections)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In dense cities with 2–3 narrow lanes and close intersections, cars can easily block each other when trying to pull over.

- ``pullOverLateralOffset``: Reduce to **1.8 – 2.2** meters to prevent cars from clipping into building colliders or sidewalk props.
- ``pullOverForwardStep1`` / ``Step2``: Reduce to **2.5** and **3.5** meters for sharper, more compact pull-over trajectories.
- ``targetPullOverSpeed``: Lower to **10 – 12** km/h so vehicles decelerate quickly without rear-ending traffic ahead.
- ``allowLeftPullOver``: Set to **true** on multi-lane streets so vehicles stranded in the left lane can yield without crossing multiple lanes of traffic.
- ``defaultPullOverClearanceRadius``: Keep around **3.0** meters to ensure vehicles don't pull over into roadside obstacles or parked cars.

2. High-Speed Highways / Suburbs (Wide Multi-Lane Roads)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Fast-moving traffic requires earlier detection and wider lateral steps.

- ``speedRadiusMultiplier``: Increase to **2.0 – 3.0** so fast-moving emergency vehicles clear traffic far ahead.
- ``defaultMaxAvoidanceDist``: Increase to **40.0 – 60.0** meters.
- ``pullOverForwardStep1`` / ``Step2``: Increase to **6.0** and **10.0** meters for smooth, high-speed diagonal transitions.
- ``pullOverLateralOffset``: Set to **3.5 – 4.0** meters to ensure full clearance of wide lanes.
- ``criticalBrakeDistance``: Increase to **20.0 – 25.0** meters to give fast oncoming traffic sufficient stopping distance.

3. Stylized / Arcade Driving (Fast Reaction & Immediate Clearance)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For action-heavy games where the player controls the emergency vehicle and needs an instant "Moses effect" clearing the road.

- ``waitingInSafeZoneResumeDelay``: Lower to **1.5 – 2.0** seconds so AI traffic quickly resumes normal flow after the player zooms past.
- ``targetPullOverSpeed``: Set higher (**25 – 30** km/h) for fast, snappy pull-over animations.
- ``yieldCorridorResumeDelay``: Set to **1.0 – 2.0** seconds.
- ``defaultCorridorHalfWidth``: Slightly expand to **2.2 – 2.5** meters to create a wider, more forgiving driving lane for the player.

Common Pitfalls & What to Watch Out For
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Vehicles Getting Stuck in Intersections**: If traffic stops inside junction bounds, increase ``defaultMaxStopDistance`` or verify that ``rearJunctionDotThreshold`` is properly set so vehicles detect emergency vehicles approaching from side junction paths.
- **Overlapping Vehicles on Shoulders**: If two vehicles target the same shoulder spot, increase ``defaultPullOverClearanceRadius`` and ``defaultPullOverExtraSafetyOffset``.
- **Jittery Lane Changing**: If cars rapidly switch between trying to change lanes and pulling over, check that ``waitingForClearSpeedMultiplier`` is set below ``0.5`` so decelerating vehicles create enough space for lane transitions.