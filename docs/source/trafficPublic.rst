.. _trafficPublic:

Traffic Public
=====

How To Create
------------

#. Create a vehicle by following these :ref:`steps <trafficCar>`.
#. Add :ref:`TrafficPublicAuthoring <trafficPublicAuthoring>` and :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>` to the created vehicle.
#. Select `Traffic public type` in the :ref:`TrafficPublicAuthoring <trafficPublicAuthoring>` component.
#. Create child `gameobject`, add :ref:`trafficPublicEntryAuthoring <trafficPublicEntryAuthoring>` component and assign to :ref:`TrafficPublicCarCapacity <trafficPublicCarCapacity>`.
#. Create :ref:`TrafficPublicRoute <trafficPublicRoute>` for the public transport route.

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
| **Entry point** : any `gameobject` that contain :ref:`TrafficPublicEntryAuthoring <trafficPublicEntryAuthoring>` component.
| **Show entry point** : on/off display entry point.

	.. image:: /images/entities/trafficCar/TrafficPublicTramExample.png
	`Tram example (white box - entry point).`

.. _trafficPublicEntryAuthoring:

TrafficPublicEntryAuthoring component
~~~~~~~~~~~~ 

Entrance point for pedestrians to public transport.
