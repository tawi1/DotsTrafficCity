.. _roadConstructor:

Road Constructor
============

Where To Find
------------

#. Buy & download, import the following asset plugin:

	`Road Constructor <https://assetstore.unity.com/packages/tools/level-design/road-constructor-287445>`_

Limitations
------------

* Roundabouts are not currently supported.

Getting Started
------------

#. Open your scene.
#. Add the `ROAD_CONSTRUCTOR` scripting define to the `Player Settings` of the project.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`	

#. Open each prefab in the prefab stage.

	.. image:: /images/integration/rc10.png	
	
#. Then, add the `RC_TrafficLightConverter` component & press the `Create` button.

	.. image:: /images/integration/rc11.png	
	
#. Activate `TrafficLightHybridService`.

	.. image:: /images/integration/rc13.png	
	`Hub/Controllers/Road/TrafficLightHybridService`

#. Select scene type depending on your needs.

Editor Scene
------------

#. Open `RoadConstructorDemoEditor` scene.	
#. Select `Road Constructor` on the scene.
#. Set collider type to `Non Convex` if you plan to use vehicles with physics **[optional step]**

	.. image:: /images/integration/rc5.png	
	
#. Select the layer of the ground collider according to your vehicle's ground raycasting. **[optional step]**	

	.. image:: /images/integration/rc8.png	
	
#. Tick on `Add Traffic comp`.
	
	.. image:: /images/integration/rc6.png	
	
#. Select `Road Builder Editor` on the scene
#. Press `Initialize` button.

	.. image:: /images/integration/rc1.png	
	
#. Place your roads according to your needs.

	.. image:: /images/integration/rc14.png	
	`Example.`
	
#. Then, press `Register scene objects`, `Add Traffic Components`, `Create Waypoints` buttons.

	.. image:: /images/integration/rc2.png	
	
#. Create a new gameobject & add `RC_EditorSceneGenerator` component.

	.. image:: /images/integration/rc3.png	
	
#. Adjust any necessary settings in the `Inspector`. 
#. Press `Generate` button.

	.. image:: /images/integration/rc15.png	
	`Result example.`
	
#. Select :ref:`Hub <subsceneGenerator>` object in the scene
#. Untick `Move lights` option.

	.. image:: /images/integration/rc9.png	
	
#. In the :ref:`Hub <subsceneGenerator>`, generate the subscene.
#. If you need to regenerate roads, select :ref:`Hub <subsceneGenerator>`, press `Move back` button, then regenerate roads in `RC_EditorSceneGenerator` & press `Generate` again in the :ref:`Hub <subsceneGenerator>`.
#. The next step is to set up `Vehicles`_

Runtime Scene
------------

#. Add the `RUNTIME_ROAD` scripting define to the `Player Settings` of the project.
#. Open `RoadConstructorDemoPlayer` scene.
#. Create a new gameobject & add `RuntimeRoadManagerCustom` & `RC_RuntimeSceneGenerator` components.

	.. image:: /images/integration/rc4.png	
	
#. In the `RC_RuntimeSceneGenerator` assign `RuntimeRoadManagerCustom` & `Road Constructor` references from the scene in the inspector.
#. Set or duplicate any existing :ref:`Light State Container <sharedLightStates>` & assign it in the `Inspector`.

	.. image:: /images/integration/rc7.png	
	
#. Adjust any necessary settings in the `Inspector`. 
#. Select `Road Constructor` on the scene.
#. Select collider to `Non Convex` if you plan to use vehicles with physics **[optional step]**

	.. image:: /images/integration/rc5.png	
	
#. Select the layer of the ground collider according to your vehicle's ground raycasting. **[optional step]**	

	.. image:: /images/integration/rc8.png	
	
#. Tick on `Add Traffic comp`.
	
	.. image:: /images/integration/rc6.png	
		
#. In the :ref:`Hub <subsceneGenerator>` object in the scene, generate the subscene.
#. The next step is to set up `Vehicles`_
#. Launch the scene & place the roads.

Vehicles
------------

Hybrid Mono
~~~~~~~~~~~~

Physics simulation vehicles run on standart `Monobehaviour` scripts.

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Find the `HybridTrafficCarMonoSkinBase Arcade` prefab & set the ground layer to match the ground collider layer in the `Road Constructor`.
#. Create :ref:`Hybrid Mono <hybridMonoVehicle>` vehicles. 

No Physics
~~~~~~~~~~~~

Vehicles without physics.

#. Set the `World simulation type` to `DOTS` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Physics simulation type` to `No physics` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set `Entity type` to :ref:`Pure entity no physics <entityType>` in the :ref:`Traffic Settings  <trafficCarSettings>`
#. Create :ref:`No physics <trafficCar>` vehicles. 

Custom Physics
~~~~~~~~~~~~

Vehicles with `DOTS` physics (works only in the `Editor scene`).

#. Set the `World simulation type` to `DOTS` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set the `Physics simulation type` to `Unity physics` in the :ref:`General settings <generalSettingsConfig>` config.
#. Set `Entity type` to :ref:`Pure custom physics <entityType>` in the :ref:`Traffic Settings  <trafficCarSettings>`
#. Select :ref:`Hub <subsceneGenerator>` object in the scene
#. Enable the `Copy Physics Shapes` option to clone surfaces from the :ref:`main scene <mainScene>` to the :ref:`sub-scene <subScene>` after each :ref:`sub-scene <subScene>` regeneration.
#. Add layer according to your ground layer in the `Road Constructor` (read more about :ref:`physics shape transferring <physicsShapeTransfer>`)

	.. image:: /images/integration/rc12.png	
	
#. Create :ref:`Custom physics <trafficCar>` vehicles. 