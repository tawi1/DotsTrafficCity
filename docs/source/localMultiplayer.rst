.. _netcodeLocal:

Local Split Screen Multiplayer
=====

To create a local split screen for use by multiple players:

* In the :ref:`Cull config <cullConfig>`, make sure `Multiplayer Calculate Distance` or `Multiplayer Camera View` type.
* Create a `Cull Point` as a child of your camera and add the `CullCameraRuntimeAuthoring` component. Then, assign the camera reference in the Inspector.

	.. image:: /images/multiplayer/splitScreen1.png