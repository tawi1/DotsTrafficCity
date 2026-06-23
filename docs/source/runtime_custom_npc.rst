.. _runtimeCustomNpc:

Runtime Custom NPC
------------------

The ``RuntimeCustomNpc`` component allows you to instantiate, initialize, and manage custom hybrid NPC entities at runtime within the DOTS-based city simulation. It connects standard Unity GameObjects (with Animators and Transforms) with corresponding High-Performance DOTS Entities.

Unlike pre-spawned crowd agents, a Runtime Custom NPC can be placed directly into a scene or spawned dynamically via script. It manages its own entity lifecycle, handles registration with the EntityManager, and provides clear toggle hooks for active simulation states (e.g., enabling/disabling locomotion and animation tracking).

Demo Sample
~~~~~~~~~~~

The package includes a pre-configured sample prefab to illustrate the correct setup:

* **Character Runtime Sample**: A ready-to-use reference prefab that demonstrates how to layer custom runtime logic on top of the pedestrian simulation infrastructure.

Prefab Structure & Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To ensure standard hybrid workflows and custom execution operate correctly, any custom runtime NPC prefab must include specific component references on its root GameObject.

.. note::
   Since ``PedestrianEntityRef`` inherits directly from ``NpcHybridEntityRef``, you **only need to attach** ``PedestrianEntityRef``. Do not attach both components simultaneously.

**Required Component Hierarchy:**

1. **PedestrianEntityRef**: Required by the core simulation framework to recognize the object as a valid pedestrian agent and interface with standard conversion pipelines. It satisfies all requirements for tracking underlying DOTS entity lifecycles.
2. **RuntimeCustomNpc**: The driver script handling manual/automatic activation loops.

.. code-block:: text

   [Prefab Root]
   ├── Animator
   ├── PedestrianEntityRef (Required - Inherits from NpcHybridEntityRef)
   └── RuntimeCustomNpc

How It Works
~~~~~~~~~~~~

1. **Entity Registration**: On initialization (or via ``autoCreateEntity``), the component queries the unique custom prefab singleton (marked with ``CustomRuntimeNpcPrefabTag``) and instantiates it.
2. **Settings Initialization**: It extracts global configurations from the ``PedestrianSettingsReference`` and seeds random parameter variations for the pedestrian entity.
3. **State Activation/Deactivation**: You can dynamically add the NPC to or remove it from the active movement and pathfinding simulation loops at runtime, shifting control between MonoBehaviours and DOTS systems.

Component API Reference
~~~~~~~~~~~~~~~~~~~~~~~

Properties
""""""""""

* **autoCreateEntity** (``bool``): If enabled, automatically invokes the registration routine during ``OnEnable``.
* **Activated** (``bool``): Read-only flag specifying whether the NPC is currently actively simulated in the world.

Public Methods
""""""""""""""

.. code-block:: csharp

   public void RegisterEntity()

Instantiates the entity representation from the custom NPC prefab, loads individual pedestrian configuration data, and pairs the GameObject's transform with the entity.

.. code-block:: csharp

   public void UnregisterEntity()

Destroys the entity using the referenced ``PedestrianEntityRef`` (via its inherited hybrid reference) and clears the activation state.

.. code-block:: csharp

   public void ActivateNpc()

Activates the NPC agent within the live city ecosystem:

* Binds the GameObject's ``Animator`` to the entity.
* Snaps the entity's position/rotation to the current GameObject coordinates.
* Dynamically locates the nearest navigation path node using ``NodeHashMapSystem.GetClosestNode``.
* Assigns a starting ``DestinationComponent`` and sets up internal system tags (e.g., enabling ``CopyTransformToGameObject``) so that the entity drives the GameObject's movement.

.. code-block:: csharp

   public void DeactivateNpc()

Suspends active simulation behavior for this NPC:

* Detaches the ``Animator`` from the ECS architecture.
* Disables transform propagation components.
* Re-enables ``CustomRuntimeNpcTag`` and switches the component layout back to state-neutral positioning, handing control back to standard Unity workflows.

Usage Guide
~~~~~~~~~~~

Manual Activation Example
"""""""""""""""""""""""""

If you choose to control activation manually, uncheck **Auto Create Entity** in the inspector and trigger the lifetime states programmatically:

.. code-block:: csharp

   using UnityEngine;
   using Spirit604.DotsCity.Gameplay.Npc;

   public class CustomNpcController : MonoBehaviour
   {
       [SerializeField] private RuntimeCustomNpc customNpc;

       void Start()
       {
           // Manually register the DOTS entity footprint
           customNpc.RegisterEntity();
       }

       public void TriggerNpcDeployment()
       {
           if (!customNpc.Activated)
           {
               // Move into active pathfinding simulation
               customNpc.ActivateNpc();
           }
       }

       public void RecallNpc()
       {
           if (customNpc.Activated)
           {
               // Suspend movement systems and take manual MonoBehaviour control
               customNpc.DeactivateNpc();
           }
       }
   }

Integration with Pedestrian States
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once ``ActivateNpc()`` is called, the entity is fed directly into the system workflow described in the :ref:`Pedestrian States <pedestrianStates>` documentation. It obtains destination markers, respects local avoidance data, and handles action/movement updates identically to standard ambient city pedestrians.