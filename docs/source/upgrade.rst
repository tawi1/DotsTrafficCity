.. _upgrade:

Upgrade Guide
=====

# Upgrading to Full Version (Quick Start)
-------------------

The upgrade process is fully automated across several phases to handle code compilation and package extraction cleanly. 

Instructions
~~~~~~~~~~~~

#. **Start the Upgrade:** Locate the **Project Unpacker** asset in your project, select it, and click the **Update To Full** button in the Inspector.
#. **Wait for Domain Reload:** Unity will clear the console, import core constants, and force a script compilation. The editor will briefly freeze—**do not close Unity** during this reload.
#. **Automatic Package Extraction:** Once scripts are compiled, the system automatically triggers `OnScriptsReloaded` on the Main Thread. It will extract core packages, clone prefabs, and adapt your project settings (`PhaseImportingPackages`).
#. **Completion:** When everything stabilizes, a final confirmation message will appear in your console: `"The project is upgraded"`.

Troubleshooting
~~~~~~~~~~~~

If the process is interrupted midway (due to an unexpected crash, closing the editor, etc.), it will not break your project. Simply select the **Project Unpacker** asset again and re-click **Update To Full** to restart the automated pipeline from scratch.

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

#. Make sure you have downloaded `Cinemachine v3 <https://docs.unity3d.com/Packages/com.unity.cinemachine@3.1/manual/index.html>`_ package.
#. Unpack `Main Camera City CM_v3` package.
	
	.. image:: /images/faq/cmv3_1.png
	
#. Select `UIInstaller`.

	.. image:: /images/faq/cmv3_2.png
	
#. Drag & drop `Camera` object into `Main Camera Base` field in `UIInstaller`.

	.. image:: /images/faq/cmv3_3.png
	
#. Right click on this field & press `Apply to Prefab Hub`.

	.. image:: /images/faq/cmv3_4.png
	
Cinemachine v2
-------------------

#. Unpack `Main Camera City CM_v2_legacy` package.
	
	.. image:: /images/faq/cmv2_1.png
	
#. Select `UIInstaller`.

	.. image:: /images/faq/cmv3_2.png
	
#. Drag & drop `Camera` object into `Main Camera Base` field in `UIInstaller`.

	.. image:: /images/faq/cmv3_3.png
	
#. Right click on this field & press `Apply to Prefab Hub`.

	.. image:: /images/faq/cmv3_4.png