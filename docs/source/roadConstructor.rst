.. _roadConstructor:

Road Constructor
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`Road Constructor <https://assetstore.unity.com/packages/tools/level-design/road-constructor-287445>`_

Getting Started
------------

#. Open your scene.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`	

#. Select mode type depending on your needs.

Editor Scene
------------

#. Open `RoadConstructorDemoEditor` scene.	
#. Select `Road Constructor` on the scene.
#. Select collider to `Non Convex` if you plan to use vehicles with physics **[optional step]**

	.. image:: /images/integration/rc5.png	
	
#. Tick on `Add Traffic comp`.
	
	.. image:: /images/integration/rc6.png	
	
#. Select `Road Builder Editor` on the scene
#. Press `Initialize` button.
#. Place your roads according to your needs.

	.. image:: /images/integration/rc1.png	
	
#. Then, press `Register scene objects`, `Add traffic components`, `Create waypoints` buttons.

	.. image:: /images/integration/rc2.png	
	
#. Create a new gameobject & add `RC_EditorSceneGenerator` component.

	.. image:: /images/integration/rc3.png	
	
#. Adjust any necessary settings in the `Inspector`. 
#. Press `Generate` button.
#. In the :ref:`Hub <hub>` object in the scene, generate the subscene.
#. If you need to regenerate roads, select :ref:`Hub <hub>`, press `Move back` button, then regenerate roads in `RC_EditorSceneGenerator` & press `Generate` again in the :ref:`hub <hub>`.

Runtime Scene
------------

#. Open `RoadConstructorDemoPlayer` scene.

	.. image:: /images/integration/rc4.png	

#. Create a new gameobject & add `RuntimeRoadManagerCustom` & `RC_RuntimeSceneGenerator` components.
#. In the `RC_RuntimeSceneGenerator` assign `RuntimeRoadManagerCustom` & `Road Constructor` references from the scene in the inspector.
#. Set or duplicate any existing :ref:`Light State Container <sharedLightStates>` & assign it in the `Inspector`.

	.. image:: /images/integration/rc7.png	
	
#. Adjust any necessary settings in the `Inspector`. 
#. Select `Road Constructor` on the scene.
#. Select collider to `Non Convex` if you plan to use vehicles with physics **[optional step]**

	.. image:: /images/integration/rc5.png	
	
#. Tick on `Add Traffic comp`.
	
	.. image:: /images/integration/rc6.png	
		
#. In the :ref:`Hub <hub>` object in the scene, generate the subscene.
#. Launch the scene & place the roads.

Vehicles
------------