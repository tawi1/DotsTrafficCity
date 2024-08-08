.. _playerNpc:

Player Npc
=====

.. contents::
   :local:

Built-in Solution
----------------

Hybrid DOTS
~~~~~~~~~~~~

The player NPC behaviour is handled by the `DOTS` systems.

How To Create
""""""""""""""

#. Add an `Animator` component to your character if it's missing & assign a `PlayerBaseController` if you want to use project animations.
#. Add all required components to your character from the list below.
#. Create a new `ID` in the enum `NpcId.cs` file.
#. Add the result to the :ref:`PlayerNpcFactory <playerNpcFactory>`.
#. Make sure that `NPC` & `Hybrid DOTS` are selected in the :ref:`PlayerSpawner <playerSpawner>`.
#. Select your character from the list in the :ref:`PlayerSpawner <playerSpawner>`.

Components
""""""""""""""

	.. image:: /images/configs/player/PlayerNpcComponents.png
	
* **Player actor** : camera tracking component **[required]**.
* **Npc behaviour entity** : holds reference to bind entity & read input from `DOTS entity world`, also controls animator & npc weapon behaviour **[required]**.
* **Npc weapon holder** : reference to the anchor bone that holds the weapon & reference to the weapon.
* **Npc hit reaction behaviour** : behaviour that handles the reaction to a bullet hit.
* **Ragdoll base** : activates `Ragdoll` when the NPC dies.
* **Npc health entity behaviour** : wrapper for entity health in the `Monobehaviour` world.

	.. note::
	
		* Spawned by :ref:`PlayerSpawner <playerSpawner>`.
			.. image:: /images/configs/player/PlayerSpawner.png
		
		* Entity movement controlled by systems:
			* `NpcControllerSystem`.
			* `NpcGroundStateSystem`.
			* `NpcRaycastGroundSystem`.
			* `NpcFreezeVerticalRotationSystem`.
			
		* `Gangster outside Player` is example prefab.
			
.. _playerNpcFactory:
	
Factory
""""""""""""""

Factory that contains player `Hybrid DOTS` NPCs.

	.. image:: /images/configs/player/PlayerNpcFactory.png
			
Hybrid Mono
~~~~~~~~~~~~

The player NPC behaviour is handled by the mono controller.

How To Create
""""""""""""""

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Add animator to your model & assign `PlayerBaseController` into the controller field.
#. Add all required components to your character from the list below.
#. Add the result to the :ref:`PlayerHybridMonoFactory <playerHybridMonoFactory>`.
#. Make sure that `NPC` & `Hybrid Mono` are selected in the :ref:`PlayerSpawner <playerSpawner>`.
#. Select your character from the list in the :ref:`PlayerSpawner <playerSpawner>`.

	.. note:: `Demo Mono` scene & `Gangster Mono outside Player` prefab are examples.
	
Components
""""""""""""""

* **Player actor** : camera tracking component **[required]**.
* **Character controller** : default unity component **[required]**.
* **Npc motion behaviour** : component that handles NPC behaviour **[required]**.
* **Player npc input behaviour** :  contains input from the player **[required]**.
* **Npc weapon holder** : reference to the anchor bone that holds the weapon & reference to the weapon.
* **Npc hit reaction behaviour** : behaviour that handles the reaction to a bullet hit.
* **Ragdoll base** : activates `Ragdoll` when the NPC dies.
* **Hybrid entity runtime authoring** : automatically  load the entity on enable at runtime for this gameobject. **[required]**.
* **Npc health behaviour** : health component.

.. _playerHybridMonoFactory:

Factory
""""""""""""""

Factory that contains player `Hybrid Mono` NPCs.

	.. image:: /images/configs/player/PlayerNpcHybridMonoFactory.png
	
.. _customCamera:
		
Custom Camera
~~~~~~~~~~~~	

Info
""""""""""""""

If you want to add your own camera solution, follow these steps:

Steps
""""""""""""""

#. Create a new `MonoBehaviour` script & implement the class that derived from `CameraBase` & add it to the root of your custom camera (the code example in the `Code Example` section below).
#. Find the `UIInstaller` object on the scene.

	.. image:: /images/integration/CustomCameraExample1.png
	
#. Assign the new camera to the `Main Camera Base` field.
	
	.. image:: /images/integration/CustomCameraExample2.png
	
#. Create a :ref:`Cull point <cullPointInfo>` child for the new camera by adding a `CullPointRuntimeAuthoring` to the new gameobject.
#. Make sure you have deleted or disabled the old camera.

Code example
""""""""""""""

..  code-block:: r

	// The new MonoBehaviour script that derived from 'CameraBase'
    public class ExampleCamera : CameraBase
    {
		// Your own camera solution example
        public vThirdPersonCamera cam;

		// Injecting PlayerActorTracker via Zenject (mandatory code)
        [Inject]
        public override void Construct(PlayerActorTracker playerActorTracker)
        {
            base.Construct(playerActorTracker);
        }

		// Override this event method to set target for your custom camera, pseudo code example:
        protected override void PlayerActorTracker_OnSwitchActor(Transform newPlayerActor)
        {
			// Set the player transform target
            cam.SetTarget(newPlayerActor);
        }
    }
	
Custom User Solution
----------------

If you want your own script to spawn player npc, follow these steps:

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Player controller type` to `Custom` in the :ref:`General settings <generalSettingsConfig>` config.
#. Disable built-in camera on the scene.
#. Make sure your camera has a :ref:`cull point <cullPointInfo>` object as a child.
#. Add the `HybridEntityRuntimeAuthoring` component to your prefab.
#. Add `Copy Transform From Game Object`, `Player Npc` components in the `Hybrid components` list.

	.. image:: /images/configs/player/PlayerNpcHybridAuthoring.png
	
#. If you haven't created your own scene yet, you can try the `Demo Mono` scene for tests.
#. Your player prefab npc is ready.
