.. _cityCreation:

City Creation
============

New Scene
------------

#. Create new `scene`.
#. In the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`
	
	.. image:: /images/gettingstarted/CityBase.png
		
#. Initial scene example:

	.. image:: /images/gettingstarted/ExampleScene.png
	
#. Create a `SpawnPoint object` (any transform) in the scene where you want the player to spawn & assign it to :ref:`PlayerSpawner <playerSpawner>`.

	.. image:: /images/gettingstarted/PlayerSpawner.png
	`Scene hierarchy example.`
	
	.. image:: /images/gettingstarted/PlayerSpawner1.png
	`Component example.`
	
#. In the :ref:`PlayerSpawner <playerSpawner>` select which type of player you want to spawn first, NPC or Car. 
	
	.. image:: /images/gettingstarted/PlayerSpawner2.png

#. Select the `Player agent type` in the :ref:`General Settings <generalSettingsConfig>` to spawn the `Player` or the `Free fly camera`.

	.. image:: /images/gettingstarted/CitySettingsInitializer.png
	
#. If you want to add your own player, :ref:`read here <playerCustom>`, otherwise you can use the temporary built-in :ref:`Player NPC <playerNpc>` & :ref:`Player car <playerCar>` **[optional step]**.
#. Add :ref:`Road segments <roadSegmentCreatorHowToUse>` to the scene.

	.. only:: builder_html

		.. image:: /images/gettingstarted/Tutorial1.gif
	
#. In the :ref:`Road Parent <roadParentInfo>` press `Force connect segments` button.

	.. only:: builder_html

		.. image:: /images/gettingstarted/Tutorial2.gif
	
#. Create & connect :ref:`Pedestrian nodes <pedestrianNode>` using the :ref:`Pedestrian Node Creator <pedestrianNodeCreatorCreate>` (`W` hotkey to select node, `E` hotkey to connect nodes)

	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial3.gif
		
#. In the :ref:`Road Parent <roadParentInfo>` press :ref:`Bake Path Data <bakingInfo>` button (should be done after each road edit & before starting the scene) & select :ref:`Hub <Hub>` object on the scene & generate a :ref:`subscene <roadEntitySubscene>`.

	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial4.gif
		
#. For more information on how to create a road, read the :ref:`road installation <roadInstallation>`.	
#. Create ground, if missing (`GlobalSurfaceCollider` example prefab) & set the layer for your ground surfaces to :ref:`Ground (18) <layerInfo>` & layer for your static objects to :ref:`StaticPhysicsShape (22) <layerInfo>` (read more about :ref:`PhysicsShapeTransfer <physicsShapeTransfer>` service, if you are going to use `DOTS` only).

	.. only:: builder_html
	
		.. image:: /images/gettingstarted/Tutorial5.gif

#. Set desired local position of :ref:`Cull point <cullPointInfo>` & :ref:`Culling distances <cullConfig>` at which road objects, traffic, pedestrians etc. will be activated.
#. By default, the cull point is the child in the `Main Camera City`, but if you want to use your own :ref:`player & camera <playerCustom>`: **[optional step]**	
	
	.. image:: /images/gettingstarted/CityCreation1.png
					
	* Select `CitySettingsInitializer` on the scene:

		.. image:: /images/gettingstarted/CityCreation2.png
		
	* Set the `Player controller type` to `Custom` in the :ref:`General Settings <generalSettingsConfig>` config.
	
		.. image:: /images/gettingstarted/CityCreation3.png
		
	* Disable the `Main Camera City`.
	
		.. image:: /images/gettingstarted/CityCreation4.png
					
	* Create a new gameobject, add a `CullPointRuntimeAuthoring` component & add this object by child to your camera (set local position to zero) or add it to the scene not too far from the roads, if the camera is not yet created.
		
	.. only:: builder_html
			
		.. image:: /images/gettingstarted/Tutorial6.gif
		`New cull point example.`
				
#. Create :ref:`traffic vehicles <trafficCar>`.
#. Create :ref:`pedestrians <pedestrian>`.
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

	`DotsCity/Scenes/Demo`
	
#. Press `Play` button.
#. Read more about :ref:`Project Scenes <projectScenes>` & :ref:`Scene Structure <sceneStructure>`.

.. _demoMonoOpening:

Demo Mono Scene
------------

#. In the `Project Folder` view, select the following scene:

	`DotsCity/Scenes/Demo Mono`
	
#. Press `Play` button.
#. Read more about :ref:`Project Scenes <projectScenes>` & :ref:`Scene Structure <sceneStructure>`.