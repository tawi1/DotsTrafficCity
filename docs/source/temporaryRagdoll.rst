---------------------------------
Pedestrian Temporary Ragdoll System
---------------------------------

The pedestrian temporary ragdoll system manages the physical behavior of pedestrians (NPCs) during collisions. It allows them to dynamically transition into a ragdoll state upon impact and automatically recover (stand back up) after a configured duration, provided it is safe to do so.

This feature is built using **Unity DOTS (Entities)** and supports a hybrid infrastructure to seamlessly switch between optimized GPU skinning and full GameObject-based physics components.

---

Enabling the Feature in Pedestrian Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The temporary ragdoll state is globally controlled via the central ``PedestrianSettingsConfig`` asset. To make this functionality available for pedestrians, the following specific flags must be configured within these global configuration settings:

* **Has Ragdoll:** This global toggle must be enabled to allow physical ragdoll interactions for pedestrians upon death or impact.
* **Allow Temporal Ragdoll:** This setting explicitly activates the recovery feature. When enabled, it allows living NPCs with remaining health points to enter a temporary ragdoll state and subsequently stand back up, rather than being permanently incapacitated or destroyed.

---

Animator Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When transitioning out of the ragdoll state, the system relies on Unity's Mecanim Animator system (configured in controllers such as ``PedestrianBaseController``) to handle the standing-up sequence.

* **State Transition:** The transition from the default locomotion or fallen state into the **GettingUp** animation state is driven by the **``GetUp``** float parameter.
* **Activation Condition:** The standing-up sequence triggers automatically when **``GetUp > -1``**.
* **Blend Tree Direction:** The ``GetUp`` parameter also acts as the blending factor in a 1D Blend Tree. This blends between different recovery profiles depending on the orientation of the physical ragdoll asset:
  * **``0``**: Getting Up Face Up (recovering from lying on the back).
  * **``1``**: Standing Up Face Down (recovering from lying on the stomach).

Ragdoll Configuration (Authoring)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

While global activation resides in the pedestrian settings, fine-grained physics behaviors are customized locally using `PedestrianRagdollConfigAuthoring.cs`. These settings are baked into an efficient multi-threaded ``BlobAsset``.

.. list-table:: Ragdoll Runtime Parameters
   :widths: 25 15 60
   :header-rows: 1

   * - Parameter
     - Type
     - Description
   * - **Recovery Duration**
     - ``float``
     - The duration in seconds a pedestrian stays in the ragdoll state before trying to recover.
   * - **Max Distance To Recover**
     - ``float``
     - Maximum allowed distance from the initial impact point for the pedestrian to still be eligible for recovery.
   * - **Force To Damage Multiplier**
     - ``float``
     - Multiplier used to convert physical collision impact force into health component damage.
   * - **Damage Type Index**
     - ``int``
     - The specific damage type index associated with vehicle-pedestrian collisions.

---

State Machine Workflow
~~~~~~~~~~~~~~~~~~~~~~

The underlying logic is driven by `TemporaryRagdollStateSystem.cs`, which processes active entities based on their current ``RagdolState``:

1. **``Default``**
   When a ragdoll activation event triggers, the system clears active anti-stuck components, calculates the target ``RecoveryTime`` based on the config, and disables the default visual skin (deactivating the GameObject or disabling GPU mesh info depending on the rig type). The physical ragdoll instance is then activated.

2. **``Reactivate``**
   Invoked if a pedestrian experiences another impact while recovering. This resets the ``RecoveryTime`` and forces the physical ragdoll back into full simulation.

3. **``Temporal``**
   The pedestrian is actively simulated as a ragdoll on the ground. The ECS entity's position tracks the physical ragdoll's hips. Once the ``RecoveryTime`` expires and no active collisions are present, the system runs a safety check. If safe, it triggers the stand-up animation.

4. **``WaitingForGettingUp``**
   Monitors the getting-up animation. Once complete, the physical ragdoll is returned to the object pool, the appropriate visual skin (Hybrid GameObject or GPU rendering) is re-enabled, movement state tags are updated, and control is handed back to standard navigation.

---

Safety Validation Algorithm
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before a pedestrian transitions out of the ``Temporal`` ragdoll state, the system invokes the ``IsAvailable`` method to prevent entities from glitching into moving traffic or getting stuck under geometry:

.. code-block:: csharp

   // Spatial safety check against nearby vehicles
   float halfWidth = carEntityData.BoundsExtents.x + safetyMargin;
   float halfLength = carEntityData.BoundsExtents.z + safetyMargin;

   bool isUnderCar = math.abs(localPos.x) <= halfWidth &&
                     math.abs(localPos.z) <= halfLength;

* **Grid-Based Lookup:** The system samples the pedestrian's flat position against the current cell and 8 neighboring cells within the ``CarHashMap``.
* **Distance Culling:** Vehicles further than a squared distance of 25 units are instantly ignored.
* **OBB Space Check:** The pedestrian's position is transformed into the vehicle's local space. If the pedestrian falls within the vehicle's bounds extents (padded by the safety margin), the recovery is aborted, and the pedestrian remains down until the vehicle passes.