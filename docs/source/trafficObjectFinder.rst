.. _trafficObjectFinder:

Traffic Object Finder
============

.. contents::
   :local:

Tool for finding traffic objects in the scene by `InstanceID` for troubleshooting.

.. _trafficObjectFinderTypes:

Available Types
------------

* :ref:`Traffic nodes <trafficNode>`.
* :ref:`Path <path>`.
* :ref:`Pedestrian Node <pedestrianNode>`.
* :ref:`Traffic Light Object <trafficLightObject>`.
* :ref:`Traffic Light Handler <trafficLightHandler>`.
* :ref:`Traffic Light Crossroad <trafficLightCrossroad>`.

How To Open
------------

In the `Unity` toolbar:

	`Spirit604/CityEditor/Window/Traffic Object Finder`

	.. image:: /images/debuggers/other/trafficObjectFinderOpen.png		
	
How To Use
------------

#. Select :ref:`type <trafficObjectFinderTypes>` of traffic object.
#. Copy & paste `InstanceID` from the error message into the window.

	.. image:: /images/debuggers/other/trafficObjectFinderExample1.png		
	`Message example.`
	
#. In the example, the type is :ref:`path <trafficObjectFinderTypes>` and the `InstanceId` is `372130`.
	
	.. image:: /images/debuggers/other/trafficObjectFinderExample2.png		
	
#. Press `Find` & `Focus` buttons.