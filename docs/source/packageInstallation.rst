.. _packageInstallation:

Project Requirements
====================

Minimum **Unity** version:
	* 2022.3.21+ or 6.0.23+ (`except 2022.3.40 - 2022.3.50 <https://discussions.unity.com/t/missing-prefab-references-when-baking-a-subscene/1502057>`_).

**Required packages:**
	* `Entities 1.2.0 <https://docs.unity3d.com/Packages/com.unity.entities@1.2/manual/index.html>`_
	* `Entities.Graphics 1.2.0 <https://docs.unity3d.com/Packages/com.unity.entities.graphics@1.2/manual/index.html>`_ [not required for :ref:`Mono <hybridMonoVehicle>` cars]
	* `Unity.Physics 1.2.0 <https://docs.unity3d.com/Packages/com.unity.physics@1.2/manual/index.html>`_ [not required for :ref:`Mono <hybridMonoVehicle>` cars]
	* `Custom Physics Authoring <https://docs.unity3d.com/Packages/com.unity.physics@1.2/manual/custom-samples-physics-components.html>`_ [not required for :ref:`Mono <hybridMonoVehicle>` cars]
	* `Unity.Collections 2.4.0 <https://docs.unity3d.com/Packages/com.unity.collections@2.4/manual/index.html>`_
	* `Burst 1.8.12 <https://docs.unity3d.com/Packages/com.unity.burst@1.8/manual/index.html>`_ 

**Asset store packages:**
	* `Zenject <https://assetstore.unity.com/packages/tools/utilities/extenject-dependency-injection-ioc-157735>`_ [optional, but recommended].
	* `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_ plugin for the sounds [optional].

Limitations
===========

* WebGL not supported.
* Vehicles with trailers or wagons are not currently supported for :ref:`NoPhysics <noPhysicsVehicle>`.

Package Installation
====================

`Youtube tutorial. <https://youtu.be/q5S5cErl32g>`_

Steps
-----

#. Download & import from the `Unity Asset Store <https://u3d.as/2PCK>`_ .
#. First time initialization window will appear automatically or you can open it manually from the toolbar ``604Spirit/CityEditor/Window/Package Initialization``.

	.. image:: /images/gettingstarted/InitilizationWindow2.png
		:scale: 50%

#. Click `Load Packages` to start downloading the packages required for this tool.

	.. note::
		**Recommended custom packages [optional from version v1.1.0 onwards, but is recommended for advanced users]:**
			* **Extenject** (`com.svermeulen.extenject`) - library for injecting dependencies (`Extenject <https://assetstore.unity.com/packages/tools/utilities/extenject-dependency-injection-ioc-157735>`_).

	.. note::
		**Script define symbols required for the project:**
			* **DOTS_CITY**
			* **UNITY_PHYSICS_CUSTOM**
			
#. After the packages have been downloaded & installed, if the console has :ref:`nunit.framework <nunitFix>` or `Burst` compilation errors, restart `Unity`.
			
	.. _packageInstallationOptional:
	
#. Download the optional assets from the `Asset Store` `[from version v1.1.0, steps 5-7 are optional, a built-in audio engine is available by default]`:

	.. note::
		**Optional asset store packages:**
			* **FMOD** - asset store plugin for :ref:`game sounds <fmodSound>` `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_
		
	.. note::
		**Script define symbols required for the project:**
			* **FMOD**
			
#. After that, press the `Add Scripting Define` button.
#. Install the :ref:`FMOD sound <fmodSound>` settings.

	.. note::
		* If the project is created from scratch, the **Pipeline**, **Layer settings**, and **Project settings** will be configured automatically. You can skip the next steps and proceed directly to **Step 11**.
		* If you are updating an existing project, follow steps **8 to 10** manually inside the initialization window.

#. **[Manual Setup]** Open the `Pipeline` tab, press the `Import Graphics` button if you want to use the demo pipelines (optional step), otherwise set `Rendering path` to `Forward+ <https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@14.0/manual/rendering/forward-plus-rendering-path.html>`_ in your pipeline settings.
#. **[Manual Setup]** Open the `Layer settings` tab, select the layers to import according to your use case, and press the `Apply` button.
   
   .. image:: /images/gettingstarted/LayerSettings.png 
      :scale: 70%
	
   .. note::
      The **TrafficNode** layer are **required** for :ref:`TrafficNode <trafficNode>` prefab; others are optional. Read more about project layers :ref:`here <layerInfo>`.

#. **[Manual Setup]** Open the `Project settings` tab & press `Add all scenes to build` if you want to add demo scenes to your project.
#. In the appeared `License Manager` window, enter your `invoice ID <https://support.unity.com/hc/en-us/articles/205790859-How-can-I-get-an-invoice-for-an-Asset-Store-purchase>`_ .

	.. image:: /images/gettingstarted/License.png

#. The next step is :ref:`to set up the new scene <cityCreation>` or launch the existing :ref:`Demo <demoOpening>` or :ref:`Demo Mono <demoMonoOpening>` scene.