.. _trafficLight:

*************
Traffic Light
*************

`YouTube tutorial. <https://youtu.be/0L84dkGqCCE?si=NhYzMJcyJ5RoJxoS&t=1379>`_

.. _trafficLightGlobalLightHowToUse:

How To Customize City Crossroads
--------------------------------
	
#. Open :ref:`Global Light Settings <trafficLightGlobalLight>`.

	`Spirit604/CityEditor/Window/Global Traffic Light Settings`
	
	.. image:: /images/road/trafficLight/GlobalLightConnectionSettingsOpen.png
	
#. Enable :ref:`Show world info <trafficLightGlobalLightCommonSettings>`.

	.. image:: /images/road/trafficLight/GlobalLightViewExample1.png
	
#. Adjust the timelines for city crossroads as needed.
#. Enable :ref:`Show disabled Lights <trafficLightGlobalLightCommonSettings>` to display crossroads with deactivated signals.

	.. image:: /images/road/trafficLight/GlobalLightViewExample2.png
	
#. Select the desired crossroad and click `Select`.
#. In the :ref:`TrafficLightCrossroad <trafficLightCrossroad>` component, configure state timings.

.. _trafficLightAutoConnection:

How To Auto Connect Lights
--------------------------

Automatically reconnects traffic and pedestrian lights to the closest road nodes using the built-in connector tool.

Requirements for Light Objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The root GameObject of the traffic light must contain both the **TrafficLightObjectAuthoring** and :ref:`TrafficLightObject <trafficLightObject>` components.
* Each child :ref:`TrafficLightFrame <trafficLightFrame>` must have its **Index direction** aligned with the physical visor/lens facing vector. **A guide ray is displayed in the Scene view to visualize this direction.**

Execution Steps
~~~~~~~~~~~~~~~

#. Open :ref:`Global Light Settings <trafficLightGlobalLight>`.
#. Expand the **Auto Light Connector** foldout.
#. Configure search parameters:
   
   * **Raycast Distance**: Search radius for finding adjacent road nodes.
   * **Connect Only Missing**: Skips lights already connected to a crossroad.
   * **Traffic Lights**: Processes vehicle traffic signals.
   * **Pedestrian Lights**: Processes pedestrian traffic signals.
   * **Pedestrian Name Pattern**: Substring used to identify pedestrian signal GameObjects (e.g., ``Pedestrian``).

#. Click **Reconnect Lights**.

.. note::
   Vehicle lights link to the nearest aligned :ref:`TrafficNode <trafficNode>`, while pedestrian lights match crosswalk nodes based on name filters.
   
.. important::
   If **DOTS Simulation** is enabled, ensure the **Is Active** toggle on the **TrafficLightHybridService** component is enabled. Otherwise, scene traffic lights will not receive state updates from ECS. *(Mono simulation enables this by default).*

How To Assign Light
-------------------

#. Open :ref:`Global Light Settings <trafficLightGlobalLightHowToUse>`.
#. Enable :ref:`Show light connections <trafficLightGlobalLightConnectionSettings>`.

	.. image:: /images/road/trafficLight/GlobalLightConnectionSettings.png
	
#. Set :ref:`Light connection type <trafficLightGlobalLightConnectionSettings>` (e.g., :ref:`Traffic node <trafficNode>`).

	.. image:: /images/road/trafficLight/GlobalLightViewTrafficNodeConnection.png
	
#. Select :ref:`H0 <trafficLightSceneViewObjectDescription>` or :ref:`H1 <trafficLightSceneViewObjectDescription>` according to the desired light handler.
#. Select the target :ref:`T <trafficLightSceneViewObjectDescription>` (:ref:`TrafficNode <trafficNode>`).
#. The selected :ref:`TrafficNode <trafficNode>` is now linked to the :ref:`TrafficLightHandler <trafficLightHandler>`.
#. Repeat to bind :ref:`PedestrianNodes <pedestrianNode>` and :ref:`Light objects <trafficLightObject>` by changing the connection type.

	.. image:: /images/road/trafficLight/GlobalLightViewPedestrianConnection.png
	`Pedestrian node connection example.`
	
	.. image:: /images/road/trafficLight/GlobalLightViewLightConnection2.png
	`Light object connection example.`

.. _trafficLightGlobalLight:

Global Lights Settings 
----------------------

Window for crossroad signal timing adjustments and entity linking.

Settings
~~~~~~~~

	.. image:: /images/road/trafficLight/GlobalLightSettings.png

.. _trafficLightGlobalLightCommonSettings:

Common Settings
~~~~~~~~~~~~~~~

| **Focus on select** : frames the `SceneView` camera onto the selected crossroad.
| **Show world info** : displays active traffic signal data in the scene (:ref:`example <trafficLightSceneInfo>`).
| **Show disabled lights** : displays all traffic light data, including inactive ones (:ref:`example <trafficLightSceneInfo2>`).

.. _trafficLightSceneInfo:

	.. image:: /images/road/trafficLight/GlobalLightViewExample1.png
	`Scene light info example.`
	
.. _trafficLightSceneInfo2:

	.. image:: /images/road/trafficLight/GlobalLightViewExample2.png
	`Scene light info (including disabled) example.`

.. _trafficLightGlobalLightConnectionSettings:

Connection Settings
~~~~~~~~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/GlobalLightConnectionSettings.png
	
| **Show light connections** : toggles visible connection lines in the scene.
| **Auto unselect handler** : automatically deselects the current handler after linking.
| **Allow override light index** : allows overriding light indices on assigned signal objects.
| **Reparent light** : reparents the light GameObject under the connected crossroad.
**Light connection type** : 
	* **All** : displays all connection types.
	* **Traffic node** : displays :ref:`traffic node <trafficNode>` connections only.
	* **Pedestrian node** : displays :ref:`pedestrian node <pedestrianNode>` connections only.
	* **Light** : displays light object connections only.
| **Show connection buttons** : displays linking buttons for the selected connection type.
| **Lights index** : filters displayed objects by :ref:`light index <trafficLightIndex>` (-1 displays all).
	
	.. image:: /images/road/trafficLight/GlobalLightViewTrafficNodeConnection2.png
	`Selected Light connection type : [TrafficNode] and Lights index : [0] example.`
		
World Lights
~~~~~~~~~~~~

| **Custom settings** : enables/disables custom timeline settings for the selected crossroad.
**Timeline:** displays :ref:`light states <trafficLightState>` and phase durations.
	* **TrafficLight [0]** : :ref:`TrafficLightHandler <trafficLightHandler>` with index 0.
	* **TrafficLight [1]** : :ref:`TrafficLightHandler <trafficLightHandler>` with index 1.
	
.. _trafficLightSceneViewObjectDescription:
	
SceneView Light Objects Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selection icons:
	* **H0 / H1** : :ref:`TrafficLightHandler <trafficLightHandler>` (index 0, index 1).
	* **T0 / T1 / T** : :ref:`TrafficNode <trafficNode>` (index 0, index 1, unassigned).
	* **P0 / P1 / P** : :ref:`PedestrianNode <pedestrianNode>` (index 0, index 1, unassigned).
	* **L0 / L1 / L** : :ref:`Light object <trafficLightObject>` (index 0, index 1, unassigned).

Deselect icons:
	* **H-** : deselects :ref:`TrafficLightHandler <trafficLightHandler>`.
	* **T-** : deselects :ref:`TrafficNode <trafficNode>`.
	* **P-** : deselects :ref:`PedestrianNode <pedestrianNode>`.
	* **L-** : deselects :ref:`Light object <trafficLightObject>`.

	.. image:: /images/road/trafficLight/GlobalLightAllConnections.png
	`All connection types with -1 light index filter enabled.`

.. _sharedLightStateReplace:

How To Replace Global Light States
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the :ref:`Global Light Settings <trafficLightGlobalLight>` window.
#. Click the `*` button to expand `Replace settings`.

	.. image:: /images/road/trafficLight/replaceShared0.png
	
#. Select the source :ref:`state container <sharedLightStates>` to replace.

	.. image:: /images/road/trafficLight/replaceShared1.png
	
#. Select the new target :ref:`State container <sharedLightStates>`.
	
	.. image:: /images/road/trafficLight/replaceShared2.png
	
#. Click `Replace`. All matching containers across crossroads are updated.

	.. image:: /images/road/trafficLight/replaceShared3.png

.. _sharedLightStates:

Shared Light State Container
----------------------------

ScriptableObject holding synchronized timings of :ref:`light states <trafficLightState>` shared across multiple :ref:`traffic light crossroads <trafficLightCrossroad>`.

How To Create
~~~~~~~~~~~~~

from the project context :

	.. image:: /images/road/trafficLight/sharedLightStatesPath.png
	
Default Container Path
~~~~~~~~~~~~~~~~~~~~~~

	.. image:: /images/road/trafficLight/sharedLightStatesProjectPath.png
	`Project path example.`
	
Settings
~~~~~~~~

	.. image:: /images/road/trafficLight/sharedLightStates.png
	`Example.`

.. _trafficLightState:

Light States
------------

* **Green** : traffic proceeds.
* **Red** : traffic halts.
* **Yellow** : transition state before red/green.
* **Red Yellow** : simultaneous red and yellow phase indicating an impending green signal.

.. _trafficLightIndex:

Light Index
-----------

Unique group identifier in a :ref:`TrafficLightCrossroad <trafficLightCrossroad>` assigned to a :ref:`TrafficLightHandler <trafficLightHandler>` and used to synchronize :ref:`light frames <trafficLightFrame>` with specific signal phases.

.. _trafficLightHandler:

Traffic Light Handler
---------------------

Entity representing an active traffic signal phase inside a :ref:`TrafficLightCrossroad <trafficLightCrossroad>`.

Settings
~~~~~~~~

	.. image:: /images/road/trafficLight/TrafficLightHandler.png
	
| **Traffic light crossroad** : parent :ref:`TrafficLightCrossroad <trafficLightCrossroad>`.
| **Triggers** : road nodes assigned to this handler.
| **Traffic light parent** : parent transform where vehicle :ref:`light objects <trafficLightObject>` reside.
| **Pedestrian light parent** : parent transform where pedestrian light objects reside.
| **Related light index** : associated :ref:`light index <trafficLightIndex>`.
| **Child lights** : list of attached child :ref:`light objects <trafficLightObject>`.
| **Custom lights** : list of attached custom :ref:`light objects <trafficLightObject>`.
| **Light states** : current :ref:`state <trafficLightState>` of the handler.

.. _trafficLightObject:

Traffic Light Object
--------------------

Root component for physical traffic light models in the scene.

	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectComponents.png
	
	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectExample.png

.. _trafficLightFrame:

Light Frame
~~~~~~~~~~~

Child component controlling individual lenses/indicators.

	.. image:: /images/road/trafficLight/TrafficLightObject/TrafficLightObjectFrameAssignExample.png

| **Traffic light object** : reference to the parent :ref:`traffic light object <trafficLightObject>`.
| **Red light** : mesh/light entity for the red indicator.
| **Yellow light** : mesh/light entity for the yellow indicator.
| **Green light** : mesh/light entity for the green indicator.
| **Initial light index** : initial :ref:`light index <trafficLightIndex>`.
| **Index direction** : facing vector of the lens/visor. A visual guide ray is rendered in the Scene view.

.. _trafficLightHybridService:

Traffic Light Hybrid Service
----------------------------

Synchronizes light states between the DOTS simulation world and scene `MonoBehaviour` components.

.. important::
   When **DOTS Simulation** is enabled, ensure **Is Active** is checked on the ``TrafficLightHybridService`` component in the scene. Otherwise, scene signals will not reflect DOTS simulation states.

Settings
~~~~~~~~

* **Is Active**: Main toggle to enable hybrid state synchronization.
* **Register Light States**: Enables reading crossroad light states via standard scripts using ``GetLightState(int id)``.
* **Register Light Entities**: Exposes ECS light entities for dynamic script modification.