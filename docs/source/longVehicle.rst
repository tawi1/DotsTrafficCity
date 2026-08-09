.. _longVehicle:

Long Vehicle
============

This feature is used to split long single vehicles (e.g., buses or long trucks without a trailer) into multiple sub-entities for improved obstacle detection and accurate bounds processing at intersections.

How to Create
-------------

1. Select the entity prefab for your vehicle.
2. Add the ``TrafficLongVehicleAuthoring`` component to it.
3. Adjust **Sub entities count** and **Sub entity length** to create additional sub-entities, which will be generated starting from the rear side of the vehicle.

.. note:: 
   For long vehicles, both the main entity and its sub-entities are registered in the obstacle detection system. However, the parent entity will ignore its own sub-entities during collision and obstacle processing.