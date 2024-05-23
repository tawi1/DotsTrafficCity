.. _customCamera:

Custom Camera
=====

Info
-------------------	

If you want to add your own camera solution, follow these steps:

Steps
~~~~~~~~~~~~

#. Implement the class that derived from `CameraBase` & add to your camera (the code example in the `Code Example` section below).
#. Find the `UIInstaller` object on the scene.

	.. image:: /images/integration/CustomCameraExample1.png
	
#. Assign the new camera to the `Main Camera Base` field.
	
	.. image:: /images/integration/CustomCameraExample2.png
	
#. Create a :ref:`Cull point <cullPointInfo>` child for the new camera by adding a `CullPointRuntimeAuthoring` to the new gameobject.
#. Make sure you have deleted or disabled the old camera.

Code example
-------------------	

..  code-block:: r

	// The class should be derived from 'CameraBase'
    public class ExampleCamera : CameraBase
    {
		// Your own camera solution example
        public vThirdPersonCamera cam;

        [Inject]
        public override void Construct(PlayerActorTracker playerActorTracker)
        {
            base.Construct(playerActorTracker);
        }

        protected override void PlayerActorTracker_OnSwitchActor(PlayerActor newPlayerActor)
        {
			// Set the player transform target
            cam.SetTarget(newPlayerActor.transform);
        }
    }