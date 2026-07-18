.. _floatingOrigin:

Floating Origin
===============

How To Use
----------

* This instruction is for the demo scene and for demonstrating purposes only. You can use it with your own character and camera by replacing the ``SampleFloatingPlayerService`` and ``SampleCameraHandlerService`` scripts according to your character and camera setup.
* Open the `Demo mono` scene.
* Disable road streaming in the :ref:`Road Streaming Config <roadStreamingConfig>`.
* Configure the Cinemachine camera according to the settings shown in the image below (set `Rotation Control` to `Hard Look At` and in the `Cinemachine Follow` component, set `Binding Mode` to `World Space`).

	.. image:: /images/road/floatingOrigin/floatingOrigin1.png
	.. image:: /images/road/floatingOrigin/floatingOrigin2.png

* Drag and drop the ``FloatingOriginManager`` sample prefab into the scene.

	.. image:: /images/road/floatingOrigin/floatingOrigin3.png
	
* Set the threshold to 10 for testing purposes.
* In the Inspector, press the `Reset` button.

	.. image:: /images/road/floatingOrigin/floatingOrigin4.png
	
* Open the child object named ``Chunk``, which contains the ``FloatingOriginChunkService`` script, and assign the parent objects in the scene that need to be moved.

	.. image:: /images/road/floatingOrigin/floatingOrigin5.png