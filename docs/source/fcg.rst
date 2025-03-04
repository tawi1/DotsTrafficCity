.. _fcg:

Fantastic City Generator
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`Fantastic City Generator (FCG) <https://assetstore.unity.com/packages/3d/environments/urban/fantastic-city-generator-157625>`_

Getting Started
------------

#. Add the `FCG` scripting define to the `Player Settings` of the project.
#. Open your scene.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`
	
#. Create a new game object & add `FCGSceneGenerator` component.

#. Generate a new config:

	.. image:: /images/integration/fcg1.png

#. Set the `World simulation type` to `Hybrid mono` in the :ref:`General settings <generalSettingsConfig>` config.
#. Find the `HybridTrafficCarMonoSkinBase Arcade` prefab & set the ground layer to `Default`.
#. Open the folder where the `FCG` traffic light prefabs are stored.

	.. image:: /images/integration/fcg1_2.png

#. Open each prefab in the prefab stage & add the `FCGTrafficLightConverter` component & press the `Create` button.

	.. image:: /images/integration/fcg1_3.png	

#. Remove or disable built-in traffic system.

	.. image:: /images/integration/fcg10.png	

#. Import `FCG` templates.

	.. image:: /images/integration/fcg11.png
	
#. Select `Import template road blocks` mode in the inspector.

	.. image:: /images/integration/fcg12.png

#. Drag & drop all FCG prefabs
#. Select Template container from the list
#. Press `Generate` button

	.. image:: /images/integration/fcg13.png
	`Example`
	
#. Select mode type depending on your needs.

Editor Mode
------------

:ref:`Road segments <roadSegment>` are connected with pregenerated prefab blocks in the `Editor`.

#. Switch to `Connect Editor Blocks` mode in `FCG Scene Generator`
#. Press `Generate` button

Runtime Mode
------------

#. Add the `RUNTIME_ROAD` scripting define to the `Player Settings` of the project.
#. After the generation of `Runtime Blocks` is finished, add a new gameobject & add a `RuntimeRoadManager` component.
#. Replace the code in `RunTimeSample.cs` with the `GenerateCityAtRuntime` method:

	..  code-block:: r
	
		public void GenerateCityAtRuntime(int citySize)
		{
			ObjectUtils.FindObjectOfType<RuntimeRoadManager>().RegenerateGraphAsync(() =>
			{
				generator = cg.GetComponent<CityGenerator>();

				generator.GenerateCity(citySize, false, false); // (city size:  1 , 2, 3 or 4) 
			});
		}
