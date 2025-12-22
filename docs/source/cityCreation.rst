.. _cityCreation:

Quick Start
============

Initial Components
------------

#. Create a new `scene`.
#. In the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`
	
	.. image:: /images/gettingstarted/CityBase.png
	
#. This window appears for the first time:

	.. image:: /images/gettingstarted/CityBase2.png

#. Select `Hub` or `Hub Base` according to your needs (in most cases `Hub Base` will be suitable for you if you don't need sample scripts (built-in player, UI, camera, etc))

#. Description:
	* **Hub** : root prefab used in `Demo` & `Demo Mono` scenes & contains demo sample dependencies.
	* **Hub Base** : clean root prefab with just traffic & pedestrian simulation without any extra stuff (:ref:`player <playerCustom>` should be spawned with your own script or simply drag & drop into the scene).

#. Press `Create` button.
#. Continue with the `Hub Base`_ or :ref:`Hub <demoCity>` article, depending on your choice.
		
Hub Base
~~~~~~~~~~~~

#. Initial scene example:

	.. image:: /images/gettingstarted/ExampleScene2.png
	
#. By default, the :ref:`Cull point <cullPointInfo>` is automatically generated as a child of the main camera.	
#. If you want to add your own player that interacts with traffic, :ref:`read here <playerCustom>` **[optional step]**.
#. The next step is to configure `Scene`_

.. _sceneCreation:

Scene
------------

#. Add :ref:`Road segments <roadSegmentCreatorHowToUse>` to the scene (Use `Ctrl+D` to duplicate and `Caps Lock` to rotate).

	.. only:: builder_html

		.. image:: /images/gettingstarted/Tutorial1.gif
	
#. In the :ref:`Road Parent <roadParentInfo>` press `Force connect segments` button.

	.. only:: builder_html

		.. image:: /images/gettingstarted/Tutorial2.gif
	
#. Create & connect :ref:`Pedestrian nodes <pedestrianNode>` using the :ref:`Pedestrian Node Creator <pedestrianNodeCreatorCreate>` (`W` hotkey to select node, `E` hotkey to connect nodes) or tick on `Connect crosswalk` option in the :ref:`Road Parent <roadParentInfo>` & press `Force connect segments` button again (Use `Tab` and `E` hotkeys to place new nodes)
	
	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial3.gif
		
#. In the :ref:`Road Parent <roadParentInfo>` press :ref:`Bake Path Data <bakingInfo>` button (should be done after each road edit & before starting the scene) & select :ref:`Hub <Hub>` object on the scene & generate a :ref:`subscene <roadEntitySubscene>`.

	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial4.gif
		
#. For more information on how to create a road, read the :ref:`road installation <roadInstallation>`.	
#. Create a ground, if missing (`GlobalSurfaceCollider` example prefab) & set the layer for your ground surfaces to :ref:`Ground (18) <layerInfo>` & layer for your static objects to :ref:`StaticPhysicsShape (22) <layerInfo>` (read more about :ref:`PhysicsShapeTransfer <physicsShapeTransfer>` service, if you are going to use `DOTS` only). For DOTS cars, the ground surface should be on a sub-scene. For mono cars, the ground surface should be on the main scene.

	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial5.gif
				
#. If you plan to use :ref:`Hybrid Mono <hybridMonoVehicle>` vehicles, set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config **[optional step]**.
#. Create your own :ref:`traffic vehicles <trafficCar>` or temporarily use the built-in traffic already added **[optional step]**.
#. If you have created your own traffic, make sure the raycasting layer matches your ground collider layer (traffic prefabs can be found in :ref:`TrafficCarEntityPoolBakerRef <trafficPreset>` at the scene).
#. Create your own :ref:`pedestrians <pedestrian>` or temporarily use the built-in pedestrians already added **[optional step]**.
#. In the :ref:`Cull config <cullConfig>`, adjust culling distance at which road objects, traffic, pedestrians etc. will be activated & use :ref:`Cull debug <cullPointDebug>` to view culling states **[optional step]**.
#. In the :ref:`Traffic settings <trafficCarSettings>`, disable `Cull physics` if you don't want cars to disable their physics when they're far away **[optional step]**.
#. Add & customize :ref:`game sounds <sound>` **[optional step]**.
#. By default, the `Unity.Entities <https://docs.unity3d.com/Packages/com.unity.entities@1.2/>`_ is not rendered on the `Sceneview`, to fix this follow these steps:
	#. In the `Unity editor` toolbar select:
		
		``Edit/Preferences``

	#. Select the `Entities` tab.
	#. Set `Scene view mode` to `Runtime Data`.
	
		.. image:: /images/gettingstarted/EntitiesDisplay.png
			:scale: 70%
	
#. Launch the scene.

	.. only:: builder_html
			
		.. image:: /images/gettingstarted/Tutorial7.gif
		`Result example.`

.. _demoOpening:

Demo Scene
------------

#. In the `Project Folder` view, select the following scene:

	`DotsCity/Samples/Demo City/Scenes/Demo`
	
#. Press `Play` button.
#. Read more about :ref:`Project Scenes <projectScenes>` & :ref:`Scene Structure <sceneStructure>`.

.. _demoMonoOpening:

Demo Mono Scene
------------

#. In the `Project Folder` view, select the following scene:

	`DotsCity/Samples/Demo City/Scenes/Demo Mono`
	
#. Press `Play` button.
#. Read more about :ref:`Project Scenes <projectScenes>` & :ref:`Scene Structure <sceneStructure>`.