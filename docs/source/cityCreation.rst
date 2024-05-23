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
	
#. Create your own :ref:`Player NPC <playerNpc>` & :ref:`Player car <playerCar>`, if required **[optional step]**.
#. Create a :ref:`Custom camera <customCamera>` if you want to use your own camera solution **[optional step]**.
#. Go through all the steps to create :ref:`road for traffic <roadInstallation>`.
#. Generate a :ref:`subscene <roadEntitySubscene>`.
#. Create :ref:`traffic vehicles <trafficCar>`.
#. Create :ref:`pedestrians <pedestrian>`.
#. Set desired local position of :ref:`Cull point <cullPointInfo>` & :ref:`Culling distances <cullConfig>` at which road objects, traffic, pedestrians etc. will be activated.
	
	.. note:: By default, the cull point is the child in the `Main Camera`.
	
#. Set the layer for your ground surfaces to :ref:`Ground (18) <layerInfo>` & layer for your static objects to :ref:`StaticPhysicsShape (22) <layerInfo>` (read more about :ref:`PhysicsShapeTransfer <physicsShapeTransfer>` service).
#. Add & customize :ref:`game sounds <sound>`.
#. Launch the scene.

.. _demoOpening:

Demo Scene
------------

#. In the `Project Folder` view, select the following scene:

	`DotsCity/Scenes/Demo`
	
#. Press `Play` button.
#. Read more about :ref:`Project Scenes <projectScenes>` & :ref:`Scene Structure <sceneStructure>`.