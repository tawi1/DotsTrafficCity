.. _changeLog:

Change Log
************

[1.0.7] - 24-05-2024
------------

Added
~~~~~~~~~~~~
 
* New auto-spline option for `Bezier` curves in the :ref:`Path Creator <pathCreator>`
* New extrude lane option :ref:`Custom segment <roadSegmentCreatorCustomSegment>` road in the :ref:`RoadSegmentCreator <roadSegmentCreator>`
* New divider line for :ref:`Traffic nodes <trafficNode>` & :ref:`Custom straight <roadSegmentCreatorCustomStraight>` roads.
* New components to interact with :ref:`Hybrid pedestrians <pedestrianHybridLegacy>` from `MonoBehaviour's`.
* Custom ragdoll user's support for :ref:`Hybrid pedestrians <pedestrianHybridLegacy>`.
* New custom IDs for vehicles in the :ref:`Car Prefab Creator <carPrefabCreator>`.
* New car model selection list for the :ref:`player spawner <playerSpawner>` when the player is spawned in the car.
* User's :ref:`custom camera <customCamera>` integration.

Fixed
~~~~~~~~~~~~

* Fixed :ref:`Pedestrian node <pedestrianNode>` connection on custom terrain shapes in the :ref:`Pedestrian node creator <pedestrianNodeCreator>`.
* Fixed auto-switch type for oneway paths in the :ref:`Path Creator <pathCreator>`.
* Player spawn, if the player originally spawned in the car.
* Fixed a potential `Type mismatch` error for animation clips in :ref:`Animation Baker <animationBaker>` which could cause the UI to break.
* Fixed a potential `NaN` position for pedestrian in the `Antistuck system`.
* Fixed traffic spawner for the path with `0` index.
* Fixed compatibility with Unity 2023.2.

Changed
~~~~~~~~~~~~

* :ref:`Pedestrian node <pedestrianNode>` scene filtering updates when node settings are changed in the :ref:`Pedestrian node creator <pedestrianNodeCreator>`.
* `PedestrianReferences` component renamed to `PedestrianEntityRef`.

[1.0.6] - 22-04-2024
------------

Added
~~~~~~~~~~~~

* New connection type for :ref:`Path Creator <pathCreator>`.
* New :ref:`traffic light <roadSegmentCreatorLightSettings>` customizations for Road Segment Creator tool.
* New :ref:`crosswalk node shape <pedestrianNodeSettings>` option for :ref:`Road Segment Creator <roadSegmentCreator>`.
* New state utils methods for pedestrian.

Fixed
~~~~~~~~~~~~

* Fixed path connection for Path Creator in some cases
* Fix for traffic light duplication when editing a road segment in the subscene.

Changed
~~~~~~~~~~~~

* UX improvement for Path Creator.

[1.0.5] - 15-04-2024
------------

Added
~~~~~~~~~~~~

* New :ref:`multi-mesh <animationBakerHowToMulti>` customization support for GPU animations. 
* New custom :ref:`attachments <animationBakerHowToMulti>` support for GPU animations. 
* New custom GPU animation :ref:`option <animationGPUAnimationCollection>` for selected pedestrians. 
* Integration for custom  :ref:`player vehicle controller <playerHybridMono>` plugin which controlled by MonoBehaviour script **[experimental]**. 

Fixed
~~~~~~~~~~~~

* Animation GPU baking with animated parent.
* Fixed physics surface cloning tool in some cases.
* Traffic spawn fix in some cases.
* Fixed obstacle detection for reverse or arc paths.
* Static physics culling.

Changed
~~~~~~~~~~~~

* Traffic lights are disabled by default for straight road templates.
* Removed obsolete options for Car Prefab Creator.

[1.0.4] - 04-04-2024
------------

Added
~~~~~~~~~~~~

* New align custom straight road feature :ref:`along the surface <snapLine>`. 
* New animation baker clip :ref:`binding <animationBakerBind>`. 

Fixed
~~~~~~~~~~~~

* Path recalculation for custom straight roads.
* Re-creation of the road segment with custom user orientation.
* Fix waypoint info display for road segment in some cases.

Changed
~~~~~~~~~~~~

* Improved :ref:`snapping <roadSegmentCreatorCustomSnapNodeSettings>` for custom road segments.

[1.0.3b] - 01-04-2024
------------

Fixed
~~~~~~~~~~~~

* First init editor hotfix.
* Path baking validation fix.

[1.0.3] - 29-03-2024
------------

Added
~~~~~~~~~~~~

* Added GPU animation :ref:`transition preview <animationTransitionEditor>`.
* New optimized shaders for crowds.
* GPU data preparation for LODs.
* New user-friendly animation shader control.

Changed
~~~~~~~~~~~~

* Update to entities 1.2.0
* GPU animation baking and playback algorithm for better memory texture layout.
* Improved GPU transition animations.

[1.0.2] - 25-03-2024
------------

Added
~~~~~~~~~~~~

* New movement randomization speed for pedestrians.

Fixed
~~~~~~~~~~~~

* A rare build crash caused by the area trigger system.
* Fixed the pedestrian physics runtime option in the build.
* Mobile input for build.

[1.0.1b] - 22-03-2024
------------

Fixed
~~~~~~~~~~~~

* Traffic mask settings editor fix.
* Script refactoring.
	
[1.0.1] - 20-03-2024
------------

Fixed
~~~~~~~~~~~~

* Missing script hotfix.

[1.0.0] - 19-03-2024
------------

* Initial release.