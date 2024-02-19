.. _trafficPublic:

Traffic Public
=====

Traffic vehicles following public transport :ref:`routes <trafficPublicRoute>` and picking up passengers at :ref:`stop station nodes <pedestrianNodeStopStation>`.

`Youtube tutorial. <https://youtu.be/7z9frpVcYpA>`_

How To Create
------------

#. Create a vehicle by following these :ref:`steps <trafficCar>`.
#. Set :ref:`traffic group <pathTrafficGroup>` to `Public Transport` in the :ref:`TrafficCarEntityAuthoring <trafficCarEntityAuthoring>` component.
#. Add :ref:`TrafficPublicAuthoring <trafficPublicAuthoring>` and :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>` to the created vehicle.
#. Tick on :ref:`Predefined Road <trafficPublicAuthoring>` if public transport is to be routed via :ref:`TrafficPublicRoute <trafficPublicRoute>`. **[Optional step]**
#. Create an empty child `GameObject`, add the :ref:`VehicleEntryAuthoring <vehicleEntryAuthoring>` component and assign it to the :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>` component.
#. Position the created Entry `GameObject` where the pedestrian entrances/exits will be.
#. Create the :ref:`TrafficPublicRoute <trafficPublicRoute>` entity and set the :ref:`CarModel <carModel>` according to created public transport vehicle. **[Optional step]**

Components
------------

.. _trafficPublicAuthoring

TrafficPublicAuthoring
~~~~~~~~~~~~ 

Authoring component that contains settings for public transport.

	.. image:: /images/entities/trafficCar/TrafficPublicAuthoring.png

| **Predefined Road** : the vehicle will only be spawned on :ref:`TrafficPublicRoute <trafficPublicRoute>` paths.
| **Min/Max idle time** : min/max idle time at the public stop station.
| **Min/Max pedestrian exit count** : min/max number of pedestrians that can exit the station at a time
| **Enter/exit delay duration** : min/max delay between entrances to public transport.

.. _trafficPublicCarCapacity:

Car capacity authoring
~~~~~~~~~~~~ 

Authoring component that contains capacity settings of the vehicle.

	.. image:: /images/entities/trafficCar/CarCapacityComponent.png
	
| **Max capacity** : max capacity of the vehicle.
| **Entry point** : any `GameObject` that contain :ref:`VehicleEntryAuthoring <vehicleEntryAuthoring>` component.
| **Show entry point** : on/off display entry point.

	.. image:: /images/entities/trafficCar/TrafficPublicTramExample.png
	`Public tram example (white box - entry point).`

	.. note:: At the moment the component is only used for :ref:`TrafficPublic <trafficPublic>` vehicles.
	
.. _vehicleEntryAuthoring:

VehicleEntryAuthoring
~~~~~~~~~~~~ 

	.. image:: /images/entities/trafficCar/VehicleEntryAuthoring.png

Entrance point for pedestrians to public transport.
