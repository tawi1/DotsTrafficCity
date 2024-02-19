.. _packageInstallation:

Project Requirements
============

Minimum **Unity** version:
	* 2022.3.11+

**Required packages:**
	* `Entities 1.1.0.pre-3 <https://docs.unity3d.com/Packages/com.unity.entities@1.1/manual/index.html>`_
	* `Entities.Graphics 1.1.0.pre-3 <https://docs.unity3d.com/Packages/com.unity.entities.graphics@1.1/manual/index.html>`_
	* `Unity.Physics 1.1.0.pre-3 <https://docs.unity3d.com/Packages/com.unity.physics@1.1/manual/index.html>`_
	* `Custom Physics Authoring <https://docs.unity3d.com/Packages/com.unity.physics@1.1/manual/custom-samples-physics-components.html>`_
	* `Unity.Collections 2.3.0.pre-3 <https://docs.unity3d.com/Packages/com.unity.collections@2.3/manual/index.html>`_
	* `Burst 1.8.9 <https://docs.unity3d.com/Packages/com.unity.burst@1.8/manual/index.html>`_ 

**Asset store packages:**
	* `Naughty attributes. <https://assetstore.unity.com/packages/tools/utilities/naughtyattributes-129996>`_
	* `Zenject. <https://assetstore.unity.com/packages/tools/utilities/extenject-dependency-injection-ioc-157735>`_
	* `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_ plugin for the sounds [optional].

Limitations
============

* The project overwrites the settings, so be sure to make a project backup before using the tool.
* :ref:`Roads <road>` can only be modified in the `Editor`.
* Vehicles with trailers or wagons are not currently supported for :ref:`NoPhysics <noPhysicsVehicle>`.
* `Animator <https://docs.unity3d.com/Manual/class-Animator.html>`_ with sceletal bone animation in pure `DOTS <https://unity.com/dots>`_ space currently not available (available only :ref:`hybrid <hybridEntity>` entities with Animator approach or :ref:`pure <pureEntity>` entities with :ref:`GPU <pedestrianGPU>` animations).
* `NavMesh surface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.0/manual/NavMeshSurface.html>`_ obstacles only calculated with `NavMeshObstacle <https://docs.unity3d.com/2020.1/Documentation/Manual/class-NavMeshObstacle.html>`_.
* :ref:`Ragdoll <pedestrianRagdoll>` currently only supported with `default colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_.

Package Installation
============

`Youtube tutorial. <https://youtu.be/q5S5cErl32g>`_

Steps
------------

#. Download & import from the `Unity Asset Store`.

#. First time initialization window will appear automatically or you can open it manually from the toolbar ``604Spirit/CityEditor/Window/Package Initialization``.

	.. image:: /images/gettingstarted/InitilizationWindow.png

#. Click `Load Packages` to start downloading the packages required for this tool.

	.. note::
		**Required custom packages:**
			* **Naughty Attributes** (`com.dbrizov.naughtyattributes`) - extension for unity inspector made by Denis Rizov, also you can manually download it from unity asset store `Naughty Attributes <https://assetstore.unity.com/packages/tools/utilities/naughtyattributes-129996>`_
			* **Extenject** (`com.svermeulen.extenject`) - library for injecting dependencies.

	.. note::
		**Script define symbols required for the project:**
			* **DOTS_CITY**
			* **UNITY_PHYSICS_CUSTOM**
			
	.. warning::
		* If you get the error 'No git executable was found', read :ref:`this <gitFix>`.
		* 'nunit.framework.dll' could not be found, read :ref:`this <nunitFix>`.
			
#. Restart the `Unity` project after all the packages have been downloaded.
			
	.. _packageInstallationOptional:
	
#. Click `Load Optional Packages` to start downloading the optional packages.

	.. note::
		**Optional packages:**
			* **Reese's DOTS Navigation** (`com.reese.path`) - Reese's DOTS navigation package for :ref:`navigating <pedestrianNavigation>` on the NavMesh (`original git <https://github.com/reeseschultz/ReeseUnityDemos>`_) (`604spirit's fork version <https://github.com/tawi1/ReeseUnityDemos>`_).
		
	.. note::
		**Script define symbols required for the project:**
			* **REESE_PATH**	
		
	.. warning::
		If you get the error 'No git executable was found', read :ref:`this <gitFix>`.
			
#. Download the required assets from the `Asset Store`:

	.. note::
		**Required asset store packages:**
			* **FMOD** - asset store plugin for :ref:`game sounds <sound>` `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_
		
	.. note::
		**Script define symbols required for the project:**
			* **FMOD**
			
#. After that, press the `Add Scripting Define` button.
#. For more information on how to add sounds :ref:`click here <sound>`.
#. Next step is :ref:`setting up the scene <cityCreation>`.