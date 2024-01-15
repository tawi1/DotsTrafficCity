.. _trafficTestScene:

Traffic Test Scene
=====

How To Use
------------

`Youtube tutorial. <https://youtu.be/OtIERf2qEm0>`_
	
#. Create :ref:`road segment <roadSegmentCreator>`.
#. Create parent `GameObject` and add :ref:`TrafficCarRoadDebugger <testSceneTrafficCarRoadDebugger>` component.
#. In the created component, press :ref:`Show buttons <testSceneTrafficCarRoadDebuggerSceneSettings>`.
#. Select the paths on the scene where you want the vehicle to spawn.
#. Adjust the normalized :ref:`path <path>` position to set the spawn point.
#. Start the scene.
#. Click `Spawn` button in the component.
#. Learn more about :ref:`TrafficCarRoadDebugger <testSceneTrafficCarRoadDebugger>` settings.

Test Cases
------------

.. _trafficTestSceneObstacle:

Check Obstacle
~~~~~~~~~~~~

Config :ref:`obstacle <trafficCarObstacleConfig>` parameters.

	.. image:: /images/testscenes/traffic/CheckObstacleTest.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/CheckObstacleTest2.png
	`Test case result.`
	
.. _trafficTestSceneNextConnectedPath:

Check Next Connected Path
~~~~~~~~~~~~

Config :ref:`Next connected path <trafficCarObstacleConfig>` parameter.

	.. image:: /images/testscenes/traffic/CheckNextConnectedPathTest.png
	`Source settings.`
		
	.. image:: /images/testscenes/traffic/CheckNextConnectedPathTest2.png
	.. image:: /images/testscenes/traffic/CheckNextConnectedPathTest3.png
	`Test case result.`

.. _trafficTestSceneIntersectedPath:

Check Intersected Path
~~~~~~~~~~~~

Config :ref:`Intersected <trafficCarObstacleConfig>` parameters.

Two cars
""""""""""""""

	.. image:: /images/testscenes/traffic/IntersectedPathTest.png
	`Source settings.`
		
	.. image:: /images/testscenes/traffic/IntersectedPathTest2.png
	`Test case result.`
	
Multiple cars
""""""""""""""

	.. image:: /images/testscenes/traffic/IntersectedPathTest3.png
	`Source settings.`
		
	.. image:: /images/testscenes/traffic/IntersectedPathTest4.png
	`Test case result.`
	
.. _trafficTestSceneCrossroadJam:
	
Check Crossroad Jam
~~~~~~~~~~~~

Config :ref:`Avoid crossroad jam <trafficCarObstacleConfig>` parameter.

	.. image:: /images/testscenes/traffic/CheckJamTest.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/CheckJamTest2.png
	`Test case result.`
	
.. _trafficTestSceneChangeLane:
	
Check Change Lane
~~~~~~~~~~~~

Config :ref:`parameters <trafficCarChangeLaneConfig>`.

Traffic jam in the lane
""""""""""""""

	.. image:: /images/testscenes/traffic/ChangeLaneTest1.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/ChangeLaneTest2.png
	`Test case result.`
	
.. _trafficTestSceneTrafficGroup:
	
Traffic fobbidden node test
""""""""""""""

	.. image:: /images/testscenes/traffic/ChangeLaneNodeTest1.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/ChangeLaneNodeTest2.png
	`Test case result.`
	
Multiple lanes test 1
""""""""""""""

	.. image:: /images/testscenes/traffic/ChangeLaneTest3.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/ChangeLaneTest4.png
	`Test case result.`
	
Multiple lanes test 2
""""""""""""""

	.. image:: /images/testscenes/traffic/ChangeLaneTest5.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/ChangeLaneTest6.png	
	`Test case result.`
	
.. _trafficTestSceneChangeLane4:
	
High speed change lane
""""""""""""""
	
	.. image:: /images/testscenes/traffic/ChangeLaneTest7.png
	`Source settings.`
		
	.. image:: /images/testscenes/traffic/ChangeLaneTest8.png
	`Test case result.`	
	
	
.. _trafficTestSceneParking:
	
Check Traffic Parking
~~~~~~~~~~~~

Config :ref:`parameters <trafficCarParkingConfig>`.

	.. image:: /images/testscenes/traffic/ParkingTest1.png
	`Source settings.`
	
	.. image:: /images/testscenes/traffic/ParkingTest2.png
	`Source car.`	
	
	.. image:: /images/testscenes/traffic/ParkingTest3.png
	`Test case result.`	

.. _trafficTestSceneTrafficReverse:
	
Check Traffic Reverse
~~~~~~~~~~~~

	.. image:: /images/testscenes/traffic/BackwardTest1.png
	`Source.`
		
	.. image:: /images/testscenes/traffic/BackwardTest2.png
	`Final result result.`
	
.. _testSceneTrafficCarRoadDebugger:

TrafficCar Road Debugger	
------------

	.. image:: /images/testscenes/traffic/TrafficCarRoadDebugger.png

.. _testSceneTrafficCarRoadDebuggerSceneSettings:

Scene settings
~~~~~~~~~~~~
	
| **Vehicle data collection** : reference to :ref:`collection <vehicleCollection>` of all vehicles.
| **Enable visual debug** : on/off visual debug on the scene.
| **Show buttons** : show add :ref:`path <path>` button to the component on the scene.
| **Highlight path after add** : on/off highlight :ref:`path <path>` after adding.
	
Spawn settings
~~~~~~~~~~~~

| **Spawn on play** : spawn the cars after the start of the scene.
| **Auto clear on spawn** : previously created cars in the test case will be destroyed on a new spawn.
| **Spawn car model** : :ref:`car model <carModel>` of spawning cars.
| **Disable lane changing** : forcibly disabling the ability for vehicles to change lanes.

Other settings
~~~~~~~~~~~~

| **Show description** : show description of test case.

Traffic spawn test entry
~~~~~~~~~~~~

| **Related trafficlight crossroad** : linked :ref:`trafficlight crossroad <trafficLightCrossroad>`.
| **Path** : linked :ref:`path <path>` for the spawned cars.
| **Highlight** : on/off highlight :ref:`path <path>`.
| **Show info** : on/off visual info of spawned cars on the scene.
| **Idle car** : on/off vehicle idle of the spawned vehicle.
| **Normalized path position** : min approach speed.
| **Spawn delay** : delayed vehicle spawn after test case spawn has started.




