.. _upgrade:

Upgrade Guide
=====

v1.0.x to v1.1.0
-------------------

#. Make backup before importing the package.
#. Delete the following files:
 	#. Folder '`DotsCity/Scripts/`'
	#. Folder '`Plugins/Spirit604/`'
	#. File '`Library/ArtifactDB`'
	
#. Import the package.
#. Untick `Import project layers` option.
#. Open `Package initialization window` & press `Clone Collision Matrix` & `Apply` buttons.

	.. image:: /images/faq/Layers_v_1_1_0.png
	
#. Remove old `Naughty attributes` package (if installed).
#. If the `Burst` has errors in the console, restart the project.
#. The project is ready.

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