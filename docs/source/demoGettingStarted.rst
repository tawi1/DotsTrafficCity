.. _demoCity:

Demo City
----------------

Getting Started
~~~~~~~~~~~~

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
	
#. If you want to add your own player, :ref:`read here <playerCustom>`, otherwise you can use the temporary built-in :ref:`Player Character <playerNpc>` & :ref:`Player car <playerCar>` **[optional step]**.
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
		
#. The next step is to configure `Scene`_