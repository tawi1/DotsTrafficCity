.. _upgrade:

Upgrade Guide
=====

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