.. _packageInstallation:

Package Installation
============

`Getting started tutorial <https://youtu.be/Y_LklnjDQ2U>`_

Steps
------------

#. Download & import from unity asset store.

#. First time initialization window will appear automatically or you can open it manually in toolbar ``604Spirit/CityEditor/Window/Package Initialization``.

	.. image:: /images/gettingstarted/InitilizationWindow.png

#. Set the root path of the tool, it is automatically detected (or manually press the `Detect Root` button if you changed the root of the tool prefab path).

#. Click `Load Packages` to start download packages required for this tool.

	.. note::
		**Required custom packages:**
			* **Naughty Attributes** (`com.dbrizov.naughtyattributes`) - extension for unity inspector made by Denis Rizov, also you can manually download it from unity asset store `Naughty Attributes <https://assetstore.unity.com/packages/tools/utilities/naughtyattributes-129996>`_
			* **Extenject** (`com.svermeulen.extenject`) - library for injecting dependencies.

	.. note::
		**Script define symbols required for the project:**
			* **DOTSCITY**
			
.. _packageInstallationOptional:

#. Click `Load Optional Packages` to start download optional packages.

	.. note::
		**Optional packages:**
			* **Reese's DOTS Navigation** - Reese's DOTS navigation package for :ref:`navigating <pedestrianNavigation>` on the NavMesh (`original git <https://github.com/reeseschultz/ReeseUnityDemos>`_) (`604spirit's fork version <https://github.com/tawi1/ReeseUnityDemos>`_).
		
	.. note::
		**Script define symbols required for the project:**
			* **REESE_PATH**	
			
#. Download the required assets from the `Asset Store`:

	.. note::
		**Required asset store packages:**
			* **FMOD** - asset store plugin for :ref:`game sounds <sound>` `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_
		
	.. note::
		**Script define symbols required for the project:**
			* **FMOD**
			
#. After that, press `Add Scripting Define` button.
#. For more information on how to add sounds :ref:`click here <sound>`.
#. Next step is :ref:`setting up the scene <sceneInitialization>`.