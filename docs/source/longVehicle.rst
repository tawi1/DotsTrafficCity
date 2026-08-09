.. _longVehicle:

Long Vehicle
============

This feature is used to split long single vehicles (e.g., buses or long trucks without a trailer) into multiple sub-entities to improve obstacle detection and prevent collisions at intersections and road transitions.

It is recommended to use this feature for any single vehicle with a length exceeding **7–8 meters**.

Why Is This Needed?
-------------------

When a long vehicle moves through intersections or between road segments, its pivot point or front section may register as having entered a new road segment while its rear section is still trailing behind in the previous segment or intersection. 

Without sub-entities, traffic systems relying on spatial queries or segment-based vehicle registration would no longer see the vehicle occupying the previous road section. As a result, oncoming or crossing vehicles might start moving prematurely and collide with the tail of the long vehicle.

Splitting the vehicle into sub-entities solves this issue: the additional sub-entities extend backward along the vehicle's body, ensuring that the previous road segment remains marked as occupied until the entire vehicle has completely cleared it.

How to Create
-------------

1. Select the entity prefab for your vehicle.
2. Add the ``TrafficLongVehicleAuthoring`` component to it.
3. Adjust **Sub entities count** and **Sub entity length** to create additional sub-entities, which will be generated starting from the rear side of the vehicle.

.. note:: 
   For long vehicles, both the main entity and its sub-entities are registered in the obstacle detection system. However, the parent entity will ignore its own sub-entities during collision and obstacle processing.