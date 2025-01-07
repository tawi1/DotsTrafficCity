.. _fcg:

Fantastic City Generator
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`Fantastic City Generator (FCG) <https://assetstore.unity.com/packages/3d/environments/urban/fantastic-city-generator-157625>`_

Getting Started
------------

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

#. Select mode type depending on your needs.

Editor Mode
------------

Road segment editor generation from scene `FCGWaypointsContainer` road data.

#. Configure all generator settings in the inspector.
#. Press `Generate` button.
#. Edit road segments in the scene as needed.

Editor Blocks
------------

Road segments are connected with prefab blocks in the `Editor`.

#. Select `Runtime Blocks` type.
#. Generate blocks like in `Runtime blocks` tutorial.
#. Switch back to `Editor Blocks` type.
#. Press the `Generate` button after each city generation using `FCG`.

Runtime Blocks
------------

Runtime chunk generation from `FCG` prefab blocks, can also be used to generate blocks for `Editor blocks`.

#. Select `Runtime Blocks` type.
#. Drag & drop `FCG` road block into the field.

	.. image:: /images/integration/fcg3.png
	
#. Generate `FCG` prefab container.
	
	.. image:: /images/integration/fcg2.png

#. Configure all generator settings in the inspector.
#. Press `Generate` button at the bottom of the inspector.
#. Some of the prefab blocks should be edited because the `FCG` plugin doesn't have enough data to complete the generation (check all selected `Prefab Blocks` & `Broken Blocks` tab in the `Inspector`), for example, let's open the `Border-Flat-Large-Exit` prefab.
#. Roundabout here without exit segment:

	.. image:: /images/integration/fcg4.png
	
#. Create a :ref:`Custom road segment <roadSegmentCreatorCustomSegment>` & connect with others with :ref:`Path Creator <pathCreator>` tool. :ref:`Pedestrian nodes <pedestrianNode>` select & connect with `Tab` hotkey.

	.. image:: /images/integration/fcg5.png
	`Result`
	
#. Now need to bind local block to share the result with the same local blocks.
#. Select generated `FCG prefab container`.

	.. image:: /images/integration/fcg5_2.png
	
#. Tick on `Show scene binding` option in the inspector.
#. Select local block in the prefab stage on the scene.

	.. image:: /images/integration/fcg6.png
	`Example`

#. Inspector example:

	.. image:: /images/integration/fcg7.png
	`Example`
	
#. Press `Create block prefab` button.

	.. image:: /images/integration/fcg8.png
	`Result`
	
#. Now when you regenerate blocks in `FCG Scene Generator`, the local block will be replaced with the previously generated local prefab block.

	.. image:: /images/integration/fcg9.png
	`Created roundabouts are now created for all local blocks`
	
#. The next step is to configure `Runtime Traffic` if you plan to use blocks at runtime otherwise switch back to `Editor Blocks`.

Runtime Traffic
------------

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
