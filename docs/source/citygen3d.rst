.. _cityGen3D:

CityGen3D
============

Limitations
------------

* For some complex generated roads may end up with artifact & may require manual fixing for them.
* Currently, pedestrian nodes are not generated.

How To Use
------------

#. Buy & download, import the following asset plugin:

	`CityGen3D <https://assetstore.unity.com/packages/tools/terrain/citygen3d-162468>`_

Getting Started
------------

#. Add the `CITYGEN_3D` scripting define to the `Player Settings` of the project.
#. Open your scene.
#. Create `City base`, in the `Unity` toolbar open:

	`Spirit604/CityEditor/Create/City Base`
	
#. Create a new game object & add `CityGen3D_RoadGenerator` component.
#. By default `CityGen3D` overrides layers, to assign the required layer for the current project, open the package init window:

	.. image:: /images/integration/citygen1.png
	
#. Untick all toggles, set new layers for `Traffic` & `Pedestrian` nodes (for example 13 & 14) & press `Apply` button.

	.. image:: /images/integration/citygen2.png
	
#. Open `CityGen3D` `Data` tab.

	.. image:: /images/integration/citygen3.png
	
#. In the `Data` tab:

	#. Set `Data source` to `Download`.
	#. Make sure the `Locked` toggle is unchecked.
	#. Place the cursor on the `OSM` map for the desired location.
	#. Press `Download` button.
	
		.. image:: /images/integration/citygen4.png
		
#. After the download is complete, scroll to the bottom of the page.

	.. image:: /images/integration/citygen5.png	

#. Press `Process`, `Load Generator`, `Run Generator` buttons in sequence.

	.. image:: /images/integration/citygen6.png	
	`Result`
		
#. In the `CityGen3D_RoadGenerator`, press `Generate` button.	
	
	.. image:: /images/integration/citygen7.png	
	
#. In the `Debug` tab, enable `Show select buttons`.
#. In the `Generated tab`, check all problems, also check for road artifacts in the scene & fix them by selecting segments & fixing nodes & paths for them.

	.. image:: /images/integration/citygen8.png	
	
#. Generate a :ref:`subscene <subscene>` when all steps are done.
#. If you want to regenerate roads, press `Move back` button in the :ref:`Hub <hub>` & regenerate roads in `CityGen3D_RoadGenerator` & generate subscene in the :ref:`Hub <hub>` again.