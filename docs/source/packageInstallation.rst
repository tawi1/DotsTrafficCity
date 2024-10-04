.. _packageInstallation:

Project Requirements
============

Minimum **Unity** version:
	* 2022.3.21+

**Required packages:**
	* `Entities 1.2.0 <https://docs.unity3d.com/Packages/com.unity.entities@1.2/manual/index.html>`_
	* `Entities.Graphics 1.2.0 <https://docs.unity3d.com/Packages/com.unity.entities.graphics@1.2/manual/index.html>`_
	* `Unity.Physics 1.2.0 <https://docs.unity3d.com/Packages/com.unity.physics@1.2/manual/index.html>`_
	* `Custom Physics Authoring <https://docs.unity3d.com/Packages/com.unity.physics@1.2/manual/custom-samples-physics-components.html>`_
	* `Unity.Collections 2.4.0 <https://docs.unity3d.com/Packages/com.unity.collections@2.4/manual/index.html>`_
	* `Burst 1.8.12 <https://docs.unity3d.com/Packages/com.unity.burst@1.8/manual/index.html>`_ 

**Asset store packages:**
	* `Zenject. <https://assetstore.unity.com/packages/tools/utilities/extenject-dependency-injection-ioc-157735>`_ [optional, but recommended].
	* `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_ plugin for the sounds [optional].

Limitations
============

* WebGL not supported.
* Built-in RP not supported.
* :ref:`Roads <road>` can only be modified in the `Editor`.
* Vehicles with trailers or wagons are not currently supported for :ref:`NoPhysics <noPhysicsVehicle>`.
* `Animator <https://docs.unity3d.com/Manual/class-Animator.html>`_ with sceletal bone animation in pure `DOTS <https://unity.com/dots>`_ space currently not available (available only :ref:`hybrid <hybridEntity>` entities with Animator approach or :ref:`pure <pureEntity>` entities with :ref:`GPU <pedestrianGPU>` animations).
* `NavMesh surface <https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.0/manual/NavMeshSurface.html>`_ obstacles only calculated with `NavMeshObstacle <https://docs.unity3d.com/2020.1/Documentation/Manual/class-NavMeshObstacle.html>`_.
* :ref:`Ragdoll <pedestrianRagdoll>` currently only collides with `default colliders <https://docs.unity3d.com/ScriptReference/Collider.html>`_.

Package Installation
============

`Youtube tutorial. <https://youtu.be/q5S5cErl32g>`_

Steps
------------

#. Download & import from the `Unity Asset Store <https://u3d.as/2PCK>`_ .
#. Make sure that you have **Unity 2022.3.21+** (except **2022.3.40**, **2022.3.41**, **2022.3.42**, **2022.3.43**, **2022.3.44**, **2022.3.45**, **2022.3.46**, **2022.3.47**, **2022.3.48**, **2022.3.49** which are `currently broken <https://discussions.unity.com/t/missing-prefab-references-when-baking-a-subscene/1502057>`_).
#. If the script first compilation `hangs <https://forum.unity.com/threads/unity-hangs-on-open-during-script-compilation.1410000>`_ for more than 5 minutes, end the task in your OS's task manager & restart `Unity`.

#. First time initialization window will appear automatically or you can open it manually from the toolbar ``604Spirit/CityEditor/Window/Package Initialization``.

	.. image:: /images/gettingstarted/InitilizationWindow.png
		:scale: 50%

#. Click `Load Packages` to start downloading the packages required for this tool.
#. If you get the error 'No git executable was found', install the :ref:`git <gitFix>` on your PC (:ref:`how to install <gitFix>`) or download these packages from the store.

	.. note::
		**Required custom packages [is optional from version v1.1.0, but recommended]:**
			* **Extenject** (`com.svermeulen.extenject`) - library for injecting dependencies (`Extenject <https://assetstore.unity.com/packages/tools/utilities/extenject-dependency-injection-ioc-157735>`_).

	.. note::
		**Script define symbols required for the project:**
			* **DOTS_CITY**
			* **UNITY_PHYSICS_CUSTOM**
			
#. After the packages have been downloaded & installed, if the console has :ref:`nunit.framework <nunitFix>` error, restart `Unity`.
			
	.. _packageInstallationOptional:
	
#. Click `Load Optional Packages` to start downloading the optional packages *(optional package,* :ref:`git <gitFix>` *required)*.

	.. note::
		**Optional packages:**
			* **Reese's DOTS Navigation** (`com.reese.path`) - Reese's DOTS navigation package for :ref:`navigating <pedestrianNavigation>` on the NavMesh (`original git <https://github.com/reeseschultz/ReeseUnityDemos>`_) (the project uses the `604spirit's fork version <https://github.com/tawi1/ReeseUnityDemos>`_).
		
	.. note::
		**Script define symbols required for the project:**
			* **REESE_PATH**	
		
	.. warning::
		If you get the error 'No git executable was found', read :ref:`this <gitFix>`.
			
#. Download the optional assets from the `Asset Store` `[from version v1.1.0, steps 9-11 are optional, a built-in audio engine is available by default]`:

	.. note::
		**Optional asset store packages:**
			* **FMOD** - asset store plugin for :ref:`game sounds <fmodSound>` `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_
		
	.. note::
		**Script define symbols required for the project:**
			* **FMOD**
			
#. After that, press the `Add Scripting Define` button.
#. Install the :ref:`FMOD sound <fmodSound>` settings.
#. If the project is created from scratch, `Pipeline`, `Layer settings`, `Project settings` are automatically installed & go to the last step, if not, follow the next steps.
#. Open the `Pipeline` tab, press the `Import Graphics` button if you want to use the demo pipelines (optional step), otherwise set `Rendering path` to `Forward+` in your pipeline settings.
#. Open `Layer settings` tab & select the layers to import according to your use case & press `Apply` button.
	
	.. image:: /images/gettingstarted/LayerSettings.png
		:scale: 70%
	
#. **TrafficNode** & **PedestrianNode** layers are **required**, others are optional, read more about project layers :ref:`here <layerInfo>`.
#. Open `Project settings` tab & press `Add all scenes to build` if you want to add demo scenes to your project.
#. The next step is :ref:`to set up the new scene <cityCreation>` or launch the existing :ref:`Demo <demoOpening>` or :ref:`Demo Mono <demoMonoOpening>` scene.