.. _changeLog:

Change Log
**********

[1.8.3] - 09-08-2026
--------------------

Added
~~~~~

* Added truck with trailer support.
* Added compatibility to split long vehicles (e.g. buses) into multiple sub-entities for better obstacle detection at intersections.

Fixed
~~~~~

* Fixed navmesh obstacle loading for vehicles [1.8.1 regression fix].

[1.8.2] - 26-07-2026
--------------------

Changed
~~~~~~~

* Improved physics for the simple mono vehicle controller.

Fixed
~~~~~

* Fixed a rare issue where traffic cars unexpectedly reversed due to a gas input delay.
* Fixed a rare issue where traffic with a passive driving style performed unexpected reverse avoidance maneuvers.

[1.8.1] - 23-07-2026
--------------------

Added
~~~~~

* Added GameObjectRef entity component to reference a GameObject from an entity.

Changed
~~~~~~~

* TransformRef now uses TransformHandle for Unity 6.3+.
* Improved performance of entity synchronization between GameObjects and entities in Unity 6.3+.
* Improved performance of hybrid Mono traffic.
* Optimized the Arcade Vehicle Controller.
* Smoother transition from No physics to DOTS traffic vehicle mode after disabling physics culling.

[1.8.0] - 16-07-2026
--------------------

Release.