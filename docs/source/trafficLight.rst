.. _trafficLight:

************
Traffic Light
************

.. _trafficLightGlobalSemaphoreHowToUse:

How To Customize City Crossroads
------------
	
#. Open :ref:`Global Semaphore Settings <trafficLightGlobalSemaphore>`.

	`Spirit604/CityEditor/Window/Global Semaphore Settings`
	
	.. image:: /images/road/trafficLight/GlobalSemaphoreConnectionSettingsOpen.png
	
#. Enable :ref:`Show world info <trafficLightGlobalSemaphoreCommonSettings>`.

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewExample1.png
	
#. You can now quickly see and adjust the timelines of all the crossroads.
#. Enable :ref:`Show disabled lights <trafficLightGlobalSemaphoreCommonSettings>` to see crossroads with traffic lights off.

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewExample2.png
	
#. Select the desired crossroad and press `Select`.
#. Now in the :ref:`TrafficLightCrossroad <trafficLightCrossroad>` component you can adjust timings.

How To Assign Light
------------

#. Open :ref:`Global Semaphore Settings <trafficLightGlobalSemaphoreHowToUse>`.
#. Enable :ref:`Show light connections <trafficLightGlobalSemaphoreConnectionSettings>`.

	.. image:: /images/road/trafficLight/GlobalSemaphoreConnectionSettings.png
	
#. Select :ref:`Light connection type <trafficLightGlobalSemaphoreConnectionSettings>` for example :ref:`traffic node <trafficNode>`.

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewTrafficNodeConnection.png
	
#. Select :ref:`H0 <trafficLightGlobalSemaphoreObjectDescription>` or :ref:`H1 <trafficLightGlobalSemaphoreObjectDescription>` depending on the desired semaphore index.
#. Next, select desired :ref:`T <trafficLightGlobalSemaphoreObjectDescription>` (:ref:`TrafficNode <trafficNode>`).
#. Now, the selected :ref:`TrafficNode <trafficNode>` will have the selected  :ref:`TrafficLightHandler <trafficLightHandler>`.
#. In the same way, you can assign :ref:`PedestrianNodes <pedestrianNode>` and :ref:`Light objects <trafficLightObject>` by changing :ref:`Light connection type <trafficLightGlobalSemaphoreConnectionSettings>`.

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewPedestrianConnection.png
	`Pedestrian node connection example.`
	
	.. image:: /images/road/trafficLight/GlobalSemaphoreViewLightConnection2.png
	`Light object connection example.`

.. _trafficLightGlobalSemaphore:

Global Semaphore Settings 
------------

Window for quick display of crossroad timings and for connecting the traffic lights to different entities.

	.. image:: /images/road/trafficLight/GlobalSemaphoreSettings.png

.. _trafficLightGlobalSemaphoreCommonSettings:

Common Settings
~~~~~~~~~~~~

| **Focus on select** : move the `SceneView` camera to the selected traffic light crossroad when you select.
| **Show world info** : show enabled traffic light data on the scene (:ref:`example <trafficLightSceneInfo>`).
| **Show disabled lights** : show all traffic light data (include disabled) on the scene (:ref:`example <trafficLightSceneInfo2>`).

.. _trafficLightSceneInfo:

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewExample1.png
	`Scene light info example.`
	
.. _trafficLightSceneInfo2:

	.. image:: /images/road/trafficLight/GlobalSemaphoreViewExample2.png
	`Scene light info (include disabled) example.`

.. _trafficLightGlobalSemaphoreConnectionSettings:

Connection Settings
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/GlobalSemaphoreConnectionSettings.png
	
| **Show light connections** : on/off light connections on the scene.
| **Auto unselect handler** : auto unselect :ref:`TrafficLightHandler <trafficLightHandler>` when connecting :ref:`TrafficLightHandler <trafficLightHandler>` traffic lights to any object.
| **Allow override light index** : allow index traffic light overrides in traffic :ref:`light objects <trafficLightObject>`.
| **Reparent light** : traffic :ref:`light object <trafficLightObject>` will be a child of the connected crossroad.
**Light connection type** : 
	* **All** : show all connection types.
	* **Traffic node** : show :ref:`traffic node <trafficNode>` connection only.
	* **Pedestrian node** : show :ref:`pedestrian node <pedestrianNode>` connection only.
	* **Light** : show light object connection only.
| **Show connection buttons** : show connection buttons for selected `Light connection type`.
| **Semaphore index** : objects with a selected :ref:`semaphore index <trafficLightSemaphoreIndex>` are displayed (-1 value - all indexes are displayed).
	
	.. image:: /images/road/trafficLight/GlobalSemaphoreViewTrafficNodeConnection2.png
	`Selected Light connection type : [TrafficNode] and Semaphore index : [0] example.`
		
World Semaphores
~~~~~~~~~~~~

| **Custom settings** : on/off custom timeline settings for selected crossroad.
**Timeline:** shows :ref:`light states <trafficLightState>` of crossroad and total duration.
	* **TrafficLight [0]** : :ref:`TrafficLightHandler <trafficLightHandler>` with :ref:`semaphore index <trafficLightSemaphoreIndex>` 0.
	* **TrafficLight [1]** : :ref:`TrafficLightHandler <trafficLightHandler>` with :ref:`semaphore index <trafficLightSemaphoreIndex>` 1.
	
.. _trafficLightGlobalSemaphoreObjectDescription:
	
SceneView Light Objects Description
~~~~~~~~~~~~

Select:
	* H0/H1 : :ref:`TrafficLightHandler <trafficLightHandler>` (index 0, index 1).
	* T0/T1/T : :ref:`TrafficNode <trafficNode>` (index 0, index 1, no index).
	* P0/P1/P : :ref:`PedestrianNode <pedestrianNode>` (index 0, index 1, no index).
	* L0/L1/L : :ref:`Light object <trafficLightObject>` (index 0, index 1, no index).

Unselect:
	* H- : unselect :ref:`TrafficLightHandler <trafficLightHandler>`.
	* T- : unselect :ref:`TrafficNode <trafficNode>`.
	* P- : unselect :ref:`PedestrianNode <pedestrianNode>`.
	* L- : unselect :ref:`Light object <trafficLightObject>`.

	.. image:: /images/road/trafficLight/GlobalSemaphoreAllConnections.png
	`All connection types and -1 :ref:`semaphore index <trafficLightSemaphoreIndex>` are enabled example.`

.. _trafficLightState:

Light States
------------

* Green : car only drives on a green lights.
* Red
* Yellow
* Red Yellow : red and yellow lights at the same time, shown as orange in the inspector.

.. _trafficLightHandler:

Traffic Light Handler
----------------

`Traffic Light Handler` is an entity for handling the state of a traffic light. Is part of :ref:`TrafficLightCrossroad <trafficLightCrossroad>`.

Settings
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/TrafficLightHandler.png
	
| **Traffic light crossroad** : reference to :ref:`TrafficLightCrossroad <trafficLightCrossroad>`.
| **Triggers** : nodes that relate to the handler.
| **Traffic light parent** : parent to which the :ref:`light objects <trafficLightObject>` will be added.
| **Pedestrian light parent** : parent to which the :ref:`light objects <trafficLightObject>` will be added.

.. _trafficLightSemaphoreIndex:

| **Related semaphore index** : linked traffic light traffic index.
| **Child lights** : list of attached child :ref:`light objects <trafficLightObject>`.
| **Custom lights** : list of attached custom :ref:`light objects <trafficLightObject>`.
| **Show world traffic lights** :
| **Show light connection** :
| **Visible light connection** :
| **Semaphore states** : :ref:`light state of handler <trafficLightState>`.

Components
~~~~~~~~~~~~

Authoring
~~~~~~~~~~~~ 

.. _trafficLightObject:

Traffic Light Object
------------

Main Component
~~~~~~~~~~~~ 

Traffic light object on the scene.

Contains data on the :ref:`light frames <trafficLightFrame>` and linked :ref:`semaphore light indexes <trafficLightSemaphoreIndex>`.

	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectComponents.png
	
	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectExample.png
	`Traffic light object example.`

.. _trafficLightFrame:

Light Frame
~~~~~~~~~~~~ 

Contains data on traffic light indicators.

	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectFrameAssignExample.png

| **Traffic light object** : reference to :ref:`light frames <trafficLightObject>`.
| **Red light** : red light :ref:`state <trafficLightState>` entity.
| **Yellow light** : yellow light :ref:`state <trafficLightState>` entity.
| **Green light** : green light :ref:`state <trafficLightState>` entity.
| **Initial semaphore index** : initial :ref:`semaphore index <trafficLightSemaphoreIndex>`.
| **Index direction** : direction in which the :ref:`semaphore index <trafficLightSemaphoreIndex>` is displayed on the scene.