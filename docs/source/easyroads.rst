.. _easyroads:

EasyRoads3D
============

How To Use
------------

#. Buy & download, import the following asset plugin:

	`EasyRoads3D <https://assetstore.unity.com/packages/tools/terrain/easyroads3d-pro-v3-469>`_

#. Open your scene.
#. Create a new game object & add `ER3D_RSGenerator` component.
#. In the `Config` field select default config or duplicate exist sample config.
#. Set `Min road length` to the desired value to ignore short roads.
#. Select any 2-lane road in the scene.

	.. image:: /images/integration/easyroads1.png
	
#. Press `left-arrow` button in the inspector.		
	
	.. image:: /images/integration/easyroads2.png
		
#. Check `Road width` & set lane width in the `ER3D_RSGenerator` accordingly.

	.. image:: /images/integration/easyroads3.png
	
#. For example, 8 road width & 2 lanes => lane width is 4.
	
	.. image:: /images/integration/easyroads3_1.png
	
#. Set `Ignore road names` to ignore roads that aren't intended for traffic. **[optional step]**
#. Set `Speed limits` for crossings. **[optional step]**

	.. image:: /images/integration/easyroads3_2.png
	
#. Add `Custom Datas` if you want to override the settings for certain straight roads with specific text. **[optional step]**

	.. image:: /images/integration/easyroads3_3.png
	
#. If your scene have custom road prefabs with `ER Crossing Prefabs` component:
	#. Create the :ref:`Road segment <roadSegmentCreator>` where your custom prefab road is located.
	
		.. image:: /images/integration/easyroads4.png
		`Example`		
		
	#. Add the `RSPrefabBinding` component to the created `Road segment`.
	#. In the `RSPrefabBinding` component, enter `ERCrossingPrefabs` text into the `Script binding type` field *[one-time step]*.
	#. Press the `Find` button.
	#. Press `+` button on scene.
	
		.. image:: /images/integration/easyroads5.png
		`Example`		
		
	#. Make sure the `Selected scene object` field have the correct scene road.
	
		.. image:: /images/integration/easyroads6.png

	#. Press the `Bind` button.
	
		.. image:: /images/integration/easyroads7.png

	#. Save created `Road segment` to prefabs.	
	#. Add created prefab to the `ER3D_RSGenerator` into the `Custom prefabs` field.
	
		.. image:: /images/integration/easyroads8.png
	
#. Press the `Generate` button.
#. Open the `Generated data` tab.

	.. image:: /images/integration/easyroads9.png
		:scale: 70%

#. Check the generated data for errors & dead ends.
#. If you want to customize road & exclude the desired road from being deleted for the new generation:
	#. Select the desired `Road segment` on the scene.
	#. In the `RSSceneBinding` component, tick on the `Lock auto recreation` option.
	#. If you now regenerate roads with `ER3D_RSGenerator`, this road will be saved for destruction.
		