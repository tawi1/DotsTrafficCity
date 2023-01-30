.. _pedestrianTestScene:

Pedestrian Test Scene
=====

How To Use
------------

#. Create :ref:`pedestrian nodes <pedestrianNodeCreator>` & connect them.
#. Create parent `GameObject` and add :ref:`Pedestrian Local Spawner <pedestrianLocalSpawner>` component.
#. In the created component, press :ref:`Show scene buttons <pedestrianLocalSpawnerCommonSettings>`.
#. Select the `pedestrian nodes <pedestrianNode>` on the scene where you want the pedestrians to spawn.

	.. image:: /images/testscenes/pedestrian/PedestrianDebugLocalSpawner.png
	`Selection example.`
	
#. Adjust the :ref:`Spawn amount <pedestrianLocalSpawnerCommonSettings>`.
#. Start the scene.
#. Click `Spawn` button in the component.
#. Learn more about :ref:`Pedestrian Local Spawner <pedestrianLocalSpawner>` settings.
	
.. _pedestrianLocalSpawner:

Pedestrian Local Spawner
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/PedestrianDebugLocalSpawner.png
	
.. _pedestrianLocalSpawnerCommonSettings:

Common settings
""""""""""""""

| **Spawn on play** : spawn the pedestrian after the start of the scene.
| **Show scene buttons** : show add :ref:`pedestrian node <pedestrianNode>` button to the component on the scene
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

	.. image:: /images/testscenes/pedestrian/WalkingTest.png
	.. image:: /images/testscenes/pedestrian/WalkingTest2.png
	
TalkArea Test
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/TalkAreaTest.png
	.. image:: /images/testscenes/pedestrian/TalkAreaTest2.png
	
Bench Test
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/BenchTest.png
	.. image:: /images/testscenes/pedestrian/BenchTest2.png
	
House Test
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/HouseTest.png
	.. image:: /images/testscenes/pedestrian/HouseTest2.png
	
.. _pedestrianNavigationTest:

Navigation Test
~~~~~~~~~~~~

	.. image:: /images/testscenes/pedestrian/NavigationTest.png