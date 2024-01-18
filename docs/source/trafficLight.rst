.. _trafficLight:

************
Traffic Light
************

`Youtube tutorial. <https://youtu.be/r85kMJ4BL5E&t=49>`_

.. _trafficLightGlobalLightHowToUse:

How To Customize City Crossroads
------------
	
#. Open :ref:`Global Light Settings <trafficLightGlobalLight>`.

	`Spirit604/CityEditor/Window/Global Traffic Light Settings`
	
	.. image:: /images/road/trafficLight/GlobalLightConnectionSettingsOpen.png
	
#. Enable :ref:`Show world info <trafficLightGlobalLightCommonSettings>`.

	.. image:: /images/road/trafficLight/GlobalLightViewExample1.png
	
#. You can now quickly see and adjust the timelines of all the crossroads.
#. Enable :ref:`Show disabled lights <trafficLightGlobalLightCommonSettings>` to see crossroads with traffic lights off.

	.. image:: /images/road/trafficLight/GlobalLightViewExample2.png
	
#. Select the desired crossroad and press `Select`.
#. Now in the :ref:`TrafficLightCrossroad <trafficLightCrossroad>` component you can adjust timings.

How To Assign Light
------------

#. Open :ref:`Global Light Settings <trafficLightGlobalLightHowToUse>`.
#. Enable :ref:`Show light connections <trafficLightGlobalLightConnectionSettings>`.

	.. image:: /images/road/trafficLight/GlobalLightConnectionSettings.png
	
#. Select :ref:`Light connection type <trafficLightGlobalLightConnectionSettings>` for example :ref:`traffic node <trafficNode>`.

	.. image:: /images/road/trafficLight/GlobalLightViewTrafficNodeConnection.png
	
#. Select :ref:`H0 <trafficLightGlobalLightObjectDescription>` or :ref:`H1 <trafficLightGlobalLightObjectDescription>` depending on the desired light index.
#. Next, select desired :ref:`T <trafficLightGlobalLightObjectDescription>` (:ref:`TrafficNode <trafficNode>`).
#. Now, the selected :ref:`TrafficNode <trafficNode>` will have the selected  :ref:`TrafficLightHandler <trafficLightHandler>`.
#. In the same way, you can assign :ref:`PedestrianNodes <pedestrianNode>` and :ref:`Light objects <trafficLightObject>` by changing :ref:`Light connection type <trafficLightGlobalLightConnectionSettings>`.

	.. image:: /images/road/trafficLight/GlobalLightViewPedestrianConnection.png
	`Pedestrian node connection example.`
	
	.. image:: /images/road/trafficLight/GlobalLightViewLightConnection2.png
	`Light object connection example.`

.. _trafficLightGlobalLight:

Global Lights Settings 
------------

Window for quick display of crossroad timings and for connecting the traffic lights to different entities.

How To Use
~~~~~~~~~~~~

Read more :ref:`here <trafficLightGlobalLightHowToUse>`.

Settings
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/GlobalLightSettings.png

.. _trafficLightGlobalLightCommonSettings:

Common Settings
~~~~~~~~~~~~

| **Focus on select** : move the `SceneView` camera to the selected traffic light crossroad when you select.
| **Show world info** : show enabled traffic light data on the scene (:ref:`example <trafficLightSceneInfo>`).
| **Show disabled lights** : show all traffic light data (include disabled) on the scene (:ref:`example <trafficLightSceneInfo2>`).

.. _trafficLightSceneInfo:

	.. image:: /images/road/trafficLight/GlobalLightViewExample1.png
	`Scene light info example.`
	
.. _trafficLightSceneInfo2:

	.. image:: /images/road/trafficLight/GlobalLightViewExample2.png
	`Scene light info (include disabled) example.`

.. _trafficLightGlobalLightObjectDescription:

Connection Settings
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/GlobalLightConnectionSettings.png
	
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
| **Lights index** : objects with a selected :ref:`light index <trafficLightIndex>` are displayed (-1 value - all indexes are displayed).
	
	.. image:: /images/road/trafficLight/GlobalLightViewTrafficNodeConnection2.png
	`Selected Light connection type : [TrafficNode] and Lights index : [0] example.`
		
World Lights
~~~~~~~~~~~~

| **Custom settings** : on/off custom timeline settings for selected crossroad.
**Timeline:** shows :ref:`light states <trafficLightState>` of crossroad and total duration.
	* **TrafficLight [0]** : :ref:`TrafficLightHandler <trafficLightHandler>` with :ref:`light index <trafficLightIndex>` 0.
	* **TrafficLight [1]** : :ref:`TrafficLightHandler <trafficLightHandler>` with :ref:`light index <trafficLightIndex>` 1.
	
.. _trafficLightGlobalLightObjectDescription:
	
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

	.. image:: /images/road/trafficLight/GlobalLightAllConnections.png
	`All connection types and -1` :ref:`light index <trafficLightIndex>` `are enabled example.`

.. _sharedLightStateReplace:

How To Replace Global Light States
~~~~~~~~~~~~

#. Open :ref:`Global Light Settings <trafficLightGlobalLight>` window.
#. Click the `*` button to expand the `Replace settings`.

	.. image:: /images/road/trafficLight/replaceShared0.png
	
#. Select the source :ref:`state container <sharedLightStates>` you want to replace.


	.. image:: /images/road/trafficLight/replaceShared1.png
	
#. Select your new desired :ref:`state container <sharedLightStates>`.
	
	.. image:: /images/road/trafficLight/replaceShared2.png
	
#. Click `Replace` button.
#. As a result, all the source :ref:`state container <sharedLightStates>` are replaced.

	.. image:: /images/road/trafficLight/replaceShared3.png

.. _sharedLightStates:

Shared Light State Container
------------

Contains common timings of :ref:`light states <trafficLightState>` that are shared between :ref:`traffic light crossroads <trafficLightCrossroad>`. You can easily replace shared container using the :ref:`Global Light Settings <sharedLightStateReplace>` tool.

How To Create
~~~~~~~~~~~~

In the project context menu:

	.. image:: /images/road/trafficLight/sharedLightStatesPath.png
	
Default Container Path
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/sharedLightStatesProjectPath.png
	`Project path example.`
	
Settings
~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/sharedLightStates.png
	`Example.`

.. _trafficLightState:

Light States
------------

* Green : car only drives on a green lights.
* Red
* Yellow
* Red Yellow : red and yellow lights at the same time, shown as orange in the inspector.

.. _trafficLightIndex:

Light Index
------------

Unique traffic light ID in :ref:`TrafficLightCrossroad <trafficLightCrossroad>` defined in :ref:`TrafficLightHandler <trafficLightHandler>` used to link :ref:`TrafficLightHandlers <trafficLightHandler>` and :ref:`traffic lights <trafficLightFrame>`.

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
| **Related light index** : linked traffic :ref:`light traffic index <trafficLightIndex>`.
| **Child lights** : list of attached child :ref:`light objects <trafficLightObject>`.
| **Custom lights** : list of attached custom :ref:`light objects <trafficLightObject>`.
| **Show world traffic lights** :
| **Show light connection** :
| **Visible light connection** :
| **Light states** : :ref:`light state of handler <trafficLightState>`.

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

Contains data on the :ref:`light frames <trafficLightFrame>` and linked :ref:`light indexes <trafficLightIndex>`.

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
| **Initial light index** : initial :ref:`light index <trafficLightIndex>`.
| **Index direction** : direction in which the :ref:`light index <trafficLightIndex>` is displayed on the scene.