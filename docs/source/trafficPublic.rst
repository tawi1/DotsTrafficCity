.. _trafficPublic:

Traffic Public
=====

Traffic vehicles following public transport :ref:`routes <trafficPublicRoute>`.

How To Create
------------

#. Create a vehicle by following these :ref:`steps <trafficCar>`.
#. Add :ref:`TrafficPublicAuthoring <trafficPublicAuthoring>` and :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>` to the created vehicle.
#. Select :ref:`Traffic public type <trafficPublicType>` in the :ref:`TrafficPublicAuthoring <trafficPublicAuthoring>` component.
#. Create empty child `GameObject`, add :ref:`TrafficPublicEntryAuthoring <trafficPublicEntryAuthoring>` component and assign it to :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>` component.
#. Position the created `GameObject` where the pedestrian entrances/exits will be.
#. Create :ref:`TrafficPublicRoute <trafficPublicRoute>` entity for the public transport route.

.. _trafficPublicAuthoring:

TrafficPublic Components
------------

.. _trafficPublicAuthoring

TrafficPublicAuthoring component
~~~~~~~~~~~~ 

Authoring component that contains settings for public transport.

	.. image:: /images/entities/trafficCar/TrafficPublicAuthoring.png

.. _trafficPublicType:

**Traffic public type** :
	* **Bus** : for the default path.
	* **Tram** : for the rail path.
| **Min/Max idle time** : min/max idle time at the public stop station.
| **Min/Max pedestrian exit count** : min/max number of pedestrians that can exit the station at a time
| **Enter/exit delay duration** : min/max delay between entrances to public transport.

.. _trafficPublicCarCapacity:

Car capacity component
~~~~~~~~~~~~ 

Authoring component that contains capacity settings of the vehicle.

	.. image:: /images/entities/trafficCar/CarCapacityComponent.png
	
| **Max capacity** : max capacity of the vehicle.
| **Entry point** : any `GameObject` that contain :ref:`TrafficPublicEntryAuthoring <trafficPublicEntryAuthoring>` component.
| **Show entry point** : on/off display entry point.

	.. image:: /images/entities/trafficCar/TrafficPublicTramExample.png
	`Public tram example (white box - entry point).`

	.. note:: At the moment the component is only used for :ref:`TrafficPublic <trafficPublic>` vehicles.
	
.. _trafficPublicEntryAuthoring:

TrafficPublicEntryAuthoring component
~~~~~~~~~~~~ 

Entrance point for pedestrians to public transport.
