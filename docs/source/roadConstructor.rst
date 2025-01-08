.. _roadConstructor:

Road Constructor
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`Road Constructor <https://assetstore.unity.com/packages/tools/level-design/road-constructor-287445`_

Getting Started
------------

#. Open your scene.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`	

#. Select mode type depending on your needs.

Editor Scene
------------

#. Open `RoadConstructorDemoEditor` scene.
#. Select `Road Builder Editor` on the scene
#. Place your roads according to your needs.
#. Press `Initialize` button.

	.. image:: /images/integration/rc1.png	
	
#. Then, press `Register`, `Add traffic components`, `Create waypoints` buttons.

	.. image:: /images/integration/rc2.png	
	
#. Create a new gameobject & add `RC_EditorSceneGenerator` component.

	.. image:: /images/integration/rc3.png	
	
#. Adjust any necessary settings in the `Inspector`. 
#. Press `Generate` button.
#. In the :ref:`Hub <hub>` object in the scene, generate the subscene.
#. If you need to regenerate roads, select :ref:`hub <hub>`, press `Move back` button, then regenerate roads in `FCGSceneGenerator` & press `Generate` again in the :ref:`hub <hub>`.
