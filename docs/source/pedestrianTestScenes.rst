.. _pedestrianTestScene:

Pedestrian Test Scene
=====

How To Use
------------

`Youtube tutorial. <https://youtu.be/sgFJLXiP4og>`_

#. Create :ref:`pedestrian nodes <pedestrianNodeCreator>` & connect them.
#. Create a parent `GameObject` and add the :ref:`Pedestrian Local Spawner <pedestrianLocalSpawner>` component.
#. In the created component, press the :ref:`Show scene buttons <pedestrianLocalSpawnerCommonSettings>`.
#. Select the :ref:`pedestrian nodes <pedestrianNode>` in the scene where you want the pedestrians to spawn.

	.. image:: /images/testscenes/pedestrian/PedestrianDebugLocalSpawnerExample.png
	`Selection example.`
	
#. Adjust the :ref:`Spawn count <pedestrianLocalSpawnerCommonSettings>`.
#. Start the scene.
#. Click on the `Spawn` button in the component.
#. Learn more about the :ref:`Pedestrian Local Spawner <pedestrianLocalSpawner>` settings.
	
.. _pedestrianLocalSpawner:

Pedestrian Local Spawner
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/PedestrianDebugLocalSpawner.png
	
.. _pedestrianLocalSpawnerCommonSettings:

Common settings
""""""""""""""

| **Spawn on play** : spawn the pedestrian after the start of the scene.
| **Show scene buttons** : show add :ref:`pedestrian node <pedestrianNode>` button to the component in the scene
| **Hightlight added nodes** :  on/off hightlight added :ref:`pedestrian nodes <pedestrianNode>`.
| **Hightlight radius** : hightlight radius.
| **Show child nodes only** : only the child :ref:`pedestrian nodes <pedestrianNode>` will be shown.

Spawn info
""""""""""""""

| **Pedestrian node** : linked :ref:`pedestrian node <pedestrianNode>`.
| **Spawn amount** : number of pedestrians that will be spawned in the :ref:`pedestrian node <pedestrianNode>`.

Test Cases
------------

Walking Test
~~~~~~~~~~~~

Test case to test the :ref:`walking parameters <pedestrianSettingsConfig>`.

	.. image:: /images/testscenes/pedestrian/WalkingTest.png
	`Source nodes.`
	
	.. image:: /images/testscenes/pedestrian/WalkingTest2.png
	`Result.`
	
.. _pedestrianTalkAreaTest:
	
TalkArea Test
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/TalkAreaTest.png
	`Source node.`
		
	.. image:: /images/testscenes/pedestrian/TalkAreaTest2.png
	`Result.`
	
Crossroad Test
~~~~~~~~~~~~

Test case of pedestrians waiting at traffic lights and crossing the crossroad.

	.. image:: /images/testscenes/pedestrian/CrossroadTest.png
	`Source nodes.`
		
	.. image:: /images/testscenes/pedestrian/CrossroadTest2.png
	`Traffic waiting.`
		
	.. image:: /images/testscenes/pedestrian/CrossroadTest3.png
	`Crossing the road.`
	
.. _pedestrianBenchTest:
	
Bench Test
~~~~~~~~~~~~

Test case to test bench :ref:`seating <pedestrianNodeSit>`.

	.. image:: /images/testscenes/pedestrian/BenchTest.png
	`Source nodes.`
	
	.. image:: /images/testscenes/pedestrian/BenchTest2.png
	`Result.`
	
.. _pedestrianHouseTest:
	
House & Idle Test
~~~~~~~~~~~~

Test case for :ref:`idling <pedestrianNodeIdle>` and entering the :ref:`house <pedestrianNodeHouse>`.

	.. image:: /images/testscenes/pedestrian/HouseTest.png
	`Source nodes.`
	
	.. image:: /images/testscenes/pedestrian/HouseTest2.png
	`Result.`
	
.. _pedestrianNavigationTest:

Navigation Test
~~~~~~~~~~~~

Test case for :ref:`navigation <pedestrianNavmeshNavigation>`.
Red circle navigation is disabled. Green circle navigation is enabled.

	.. image:: /images/testscenes/pedestrian/NavigationTest.png
	`Source nodes.`
	
	.. image:: /images/testscenes/pedestrian/NavigationLocalAvoidanceTest.png
	`Local avoidance example.`
	
	.. image:: /images/testscenes/pedestrian/NavigationNavAgentTest.png
	`NavMesh navigating example.`