.. _upgrade:

Upgrade Guide
=====

v1.0.x to v1.1.0
-------------------

#. Make backup before importing the package.
#. Delete the following folders:

 	* `DotsCity/Scripts/`
	* `Plugins/Spirit604/`
	
#. Import the package.
#. Open `Package initialization window`.

	.. image:: /images/faq/Layers_v_1_1_0_1.png
		:scale: 50%
	
#. Select `Layer settings` tab.
#. Untick `Import all project layers` option.
#. Press `Import Collision Matrix` & `Apply` buttons.

	.. image:: /images/faq/Layers_v_1_1_0_2.png
		:scale: 50%
	
#. Remove old `Naughty attributes` package (if installed).
#. Restart the `Unity`.
#. If the scene has lost the references, close the Unity & delete this file:

	* `[ProjectFolder]/Library/ArtifactDB`
	
#. The new project is ready.

.. _hdrp:

HDRP
-------------------

#. Download `HDRP` template project.
#. Remove `URP` packages in the `Package Manager` (if exist).
#. Unpack `HDRP` package.

	.. image:: /images/faq/HDRP_pack.png
	
#. Open quality settings from the `Unity` toolbar:

	``Edit/Project settings/Quality``

#. Set the `Render pipeline asset` from the `HDRP sample`.

	.. image:: /images/faq/HDRP_quality.png
	
#. Open assigned pipeline asset & disable `Motion Vectors` option.

	.. image:: /images/faq/HDRP_asset.png
	
#. Set the `Light settings` for the desired scene (light settings can be taken from the `HDRP sample`).

	.. image:: /images/faq/HDRP_light.png
	`Example.`

#. Set `Environment settings` for the desired scene.

	.. image:: /images/faq/HDRP_env.png
	`Example.`
	
.. _cinemachineV3:

Cinemachine v3 Upgrade
-------------------

#. Unpack `Main Camera City CM_v3` package.
	
	.. image:: /images/faq/cmv3_1.png
	
#. Open `UIInstaller`.

	.. image:: /images/faq/cmv3_2.png
	
#. Drag & drop `Camera` object into `Main Camera Base` field in `UIInstaller`.

	.. image:: /images/faq/cmv3_3.png
	
#. Right click on this field & press `Apply to Prefab Hub`.

	.. image:: /images/faq/cmv3_4.png