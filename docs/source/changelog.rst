.. _changeLog:

Change Log
************

[1.1.0] - 05-08-2024
------------

Added
~~~~~~~~~~~~

* Full `Hybrid mode` support:
	* New monobehaviour compatible traffic.
	* New hybrid NPCs compatible with any custom character controller.
	* New hybrid traffic lights.
* New `EasyRoads3D <https://assetstore.unity.com/packages/tools/terrain/easyroads3d-pro-v3-469>`_ integration.
* New `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ integration.
* New `API` for custom spline roads generation.
* New `EntityWeakRef` class to link Monobehaviour script & traffic & pedestrian node entities.
* New player traffic control feature.
* New runtime entity hybrid workflow for runtime gameobjects.
* New hybrid GPU mode that allows you to mix hybrid animator models for near and GPU animation for far at the same time.
* Limit texture baking for :ref:`Animation Baker <animationBaker>`.
* Multi texture container for :ref:`Animation Baker <animationBaker>`.
* Path Waypoints can be traffic node functionality.
* Added endless streaming for :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road.
* Added `Auto-crossroad` option for :ref:`Custom segment <roadSegmentCreatorCustomSegment>` for custom shape crossroads.
* Pedestrian node generation along :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road.
* :ref:`Custom straight <roadSegmentCreatorCustomStraight>` can be converted into the :ref:`Custom segment <roadSegmentCreatorCustomSegment>` road.
* Crosswalk connection for :ref:`Custom segment <roadSegmentCreatorCustomSegment>`.
* Added left-hand traffic option.
* Custom cull state config calculation for specific entities.
* New camera view based culling calculation method.
* New spawn culling layer adjustment for traffic & pedestrians.
* New traffic node display for right, left lanes in segments & path spawn nodes.
* Traffic & pedestrian node debug in `Editor` mode.
* New project initialization window.
* Added support for Unity's built-in audio engine.
* Added :ref:`HDRP <hdrp>` support.

Fixed
~~~~~~~~~~~~

* Fixed traffic spawning in culled areas.
* Fixed custom physics vehicle could jump after restoring physics at runtime in some cases.
* Fixed a potential crash when user undoing changes :ref:`Custom straight <roadSegmentCreatorCustomStraight>` roads.
* Fixed obstacle detection for neighbouring paths.
* Fixed `Player spawner` not spawning in some cases when adding the new `ID` for player NPCs. 
* Player spawn no longer throws an exception if it doesn't exist.
* Fixed `Input` for `Player car` in `Editor` when `Android` build is selected.
* Fixed road segment merge.

Changed
~~~~~~~~~~~~

* Major refactoring of the project to make it more modular. 
* Now the project can be used for traffic simulation only, without player & extra features.
* Project no longer overwrites the settings by default.
* FMOD no longer required package.
* Removed `Naughty attributes` dependency.
* `Zenject` can be an optional dependency.
* Now all sound data is stored in `SoundDataContainer` scriptable object.
* Min `Burst` version 1.8.16 for `Unity` 2022.3.31 or higher.

[1.0.7d] - 06-06-2024
------------

Added
~~~~~~~~~~~~

* Create & connect :ref:`Pedestrian nodes <pedestrianNode>` in the prefab scene.
* Added gradle config for Android for Unity 6.
* Added support `Cinemachine 3.0+ <https://docs.unity3d.com/Packages/com.unity.cinemachine@3.0/manual/index.html>`_.

Fixed
~~~~~~~~~~~~

* Fixed Unity package dependency resolving for the first time can cause endless script compilation.
* :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road may have null traffic nodes due to initial creation in some cases.
* Fixed :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road oneway path generation with multiple lanes.
* Fixed :ref:`Custom segment <roadSegmentCreatorCustomSegment>` path surface snapping.
* Fixed :ref:`Pedestrian node creator <pedestrianNodeCreator>` losing sceneview focus, causing the hotkey for it to be disabled.
* Animation baker minor UI fixes & improvements.

[1.0.7c] - 31-05-2024
------------

Fixed
~~~~~~~~~~~~

* Fixed package initilization window doesn't load in some cases.
* Fixed package initilization window appears randomly on Mac OS.

[1.0.7b] - 29-05-2024
------------

Added
~~~~~~~~~~~~

* Auto bootstrap option for single scene.
* Bootstrap logging.
* Entity road drawer for the editor time.

Fixed
~~~~~~~~~~~~

* Car prefab creator ID duplicate error.
* Script defines after the project update.
* Input in the custom vehicle test scene.

[1.0.7] - 24-05-2024
------------

Added
~~~~~~~~~~~~
 
* New auto-spline option for `Bezier` curves in the :ref:`Path Creator <pathCreator>`
* New :ref:`extrude lane <extrudeLane>` option for :ref:`Custom segment <roadSegmentCreatorCustomSegment>` road in the :ref:`RoadSegmentCreator <roadSegmentCreator>`
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