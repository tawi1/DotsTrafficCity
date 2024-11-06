.. _changeLog:

Change Log
************

[1.2.1b] - 06-11-2024
------------

Added
~~~~~~~~~~~~

* Added support for lane changing on run-time roads.
* Added a helper button for traffic lights that have lost their reference to a traffic light crossroad. 
* Added support for `Odin Inspector`.

Fixed
~~~~~~~~~~~~

* Fixed intersection conversion for run-time road chunks.

[1.2.1] - 04-11-2024
------------

Added
~~~~~~~~~~~~

* Added support for `Multi-road segments` by adding 1 `RuntimeSegment` at a time in `Runtime Road mode`.
* Added new `RuntimeTile Chunk Road demo` to demonstrate the road chunks added at runtime.
* Added a new option to leave the car idle for a certain amount of time when parking if pedestrian is disabled for the scene.
* Parking can be used on sloping surfaces.
* Added auto-curve type detection for :ref:`Path creator <pathCreator>`.

Fixed
~~~~~~~~~~~~

* Fixed :ref:`path <path>` intersection calculation for custom shape surface.
* Minor fix `Car prefab creator` text pattern search for wheels.
* Fixed :ref:`Animation Baker <animationBaker>` baking with single texture atlas for multi-mesh characters.
* Fixed a problem with the `Local Avoidance` switch multi-targeting in a short amount of time.

Changed
~~~~~~~~~~~~

* Improved obstacle detection in intersecting & neighbouring cases.

[1.2.0] - 28-10-2024
------------

Added
~~~~~~~~~~~~

* Runtime graph creation.
* Added new `RuntimeTile Demo` scene.
* Traffic light `API` to get traffic light state from monobehaviour script.
* Added option to manually handle traffic light state.
* New train system.
* Custom train system support.
* Custom train demo scene.
* Added the ability to split :ref:`external traffic routes <trafficNodeConnectionInfo>` into smaller ones to better balance spawning.
* Added custom settings for pedestrian nodes for selected routes.
* Added the ability to split pedestrian routes into smaller ones to better balance spawning.
* New `TriggerLight` type for :ref:`TrafficNode <trafficNode>`, which triggers selected traffic light when traffic car enters this node.
* The :ref:`Traffic Road Debugger <testSceneTrafficCarRoadDebugger>` can be used at runtime to manually spawn vehicles in custom scenarios.
* Added saving of :ref:`Road Segment Creator <roadSegmentCreator>` settings so that a new road segment is created using the previously saved settings.
* Added a handy duplicate feature for existing connected :ref:`Road Segment Creator <roadSegmentCreator>` to create clean duplicates without existing connected paths.
* Added a sample custom player to interact with the custom car & pedestrian.
* Added one-way roads for pedestrian nodes.
* Added manual sync button for all configs.

Fixed
~~~~~~~~~~~~

* Fixed car creation offset for car parts when the car parts are not the parent of the car body.
* Fixed wheel detection during car creation in some cases.
* Fixed adding trigger area tag to non-pedestrian entities.
* Fixed :ref:`Auto-crossroad <roadSegmentCreatorAuto>` generation when the custom segment contains one-way paths.
* Fixed Path creator detects wrong connection sides in some cases.
* Fixed steering input can be incorrectly calculated in some cases.

Changed
~~~~~~~~~~~~

* Now the road `Graph` is created at runtime when the scene starts.
* `Cinemachine v3` used by default.
* Traffic light states for each traffic light handler are now stored in the dynamic buffer.
* Improved randomization of initial pedestrian spawn.
* Added traffic light debugging for paths with custom lights.

[1.1.0g] - 19-09-2024
------------

Fixed
~~~~~~~~~~~~

* Crossroad jam obstacle fix.
* Fixed sound pooling when vehicle is destroyed.
* Fixed lane change potential obstacle stuck when multiple cars are changing to the same lane.
* Fixed avoidance of mono cars when trying to change lanes.
* Fixed custom traffic light for specific path.
* Fixed initial `HDRP` installation conflict with `Cinemachine v3` package.

[1.1.0f] - 10-09-2024
------------

Changed
~~~~~~~~~~~~

* Improved `NPC` obstacle detection.

Fixed
~~~~~~~~~~~~

* `TrafficNpcCalculateObstacleSystem` debug race condition fixed.
* Anti-roll fix for `Arcade Vehicle Controller`.
* Fixed warning messages.
* Fixed potential config sync failure in some cases.
* Fixed missing reference in the `PolygonCity`.
* Fixed `EasyRoads3D` exception when crossing has 1 connecting road.

[1.1.0e] - 16-08-2024
------------

Added
~~~~~~~~~~~~

* Auto-crosswalk connection in the :ref:`Road Parent <roadParentInfo>`.
* Auto-connection distance in the :ref:`Road Parent <roadParentInfo>`.
* Added new road warning messages.
* New `Agents Navigation` config.
* New agent hybrid component.

Fixed
~~~~~~~~~~~~

* Fixed move handle for moving two or more road segments.
* Crowd sound system dependency fix.
* Fixed `Ragdoll` not being pooled.

Changed
~~~~~~~~~~~~

* Improved :ref:`Road Parent <roadParentInfo>` UI.

[1.1.0d] - 12-08-2024
------------

Added
~~~~~~~~~~~~

* Interpolation of the car view for culled mono physics cars.
* New collision stuck avoidance system for :ref:`Hybrid mono <hybridMonoVehicle>` cars.

Fixed
~~~~~~~~~~~~

* Agents Navigation integration editor error fix.
* Minor player arcade car prefab fix.
* Traffic node viewer fix.

Changed
~~~~~~~~~~~~

* Improved transition between physics & no physics arcade cars.

[1.1.0c] - 09-08-2024
------------

Added
~~~~~~~~~~~~

* New auto-sync config option between MainScene & Subscene.
* Traffic node gizmos settings.
* New pure city stress scene.

Fixed
~~~~~~~~~~~~

* Minor script fix for Unity 2023.2.
* Fixed potential config corruption for builds.
* Fixed stress scene demo exit error.
* Arcade vehicle controller wheel position fix.

Changed
~~~~~~~~~~~~

* Minimum `Unity` version 2022.3.21.
* Improved arcade sample cars.

[1.1.0b] - 06-08-2024
------------

Added
~~~~~~~~~~~~

* Added `CarModelRuntimeAuthoring`, `BoundsRuntimeAuthoring`, `VelocityRuntimeAuthoring` entity runtime components.

Fixed
~~~~~~~~~~~~

* Fixed compatibility with Entities 1.3.0.
* Fixed initial entity scale for runtime entities with `CopyTransformFromGameObject` component.
* Fixed bootstrap if user tries to start bootstrap twice.
* FMOD minor script fix.
* Nav agents dependency fix.

[1.1.0] - 05-08-2024
------------

Added
~~~~~~~~~~~~

* Full `Hybrid mode` support:
	* New :ref:`monobehaviour compatible <hybridMonoVehicle>` traffic.
	* New hybrid NPCs compatible with any custom character controller.
	* New hybrid traffic lights.
* New `EasyRoads3D <https://assetstore.unity.com/packages/tools/terrain/easyroads3d-pro-v3-469>`_ integration.
* New `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ integration.
* New `API` for custom spline roads generation.
* New `EntityWeakRef` class to link Monobehaviour script & traffic & pedestrian node entities.
* New player traffic control feature.
* New runtime entity hybrid workflow for runtime gameobjects.
* New hybrid GPU mode that allows you to mix hybrid animator models for near and GPU animation for far at the same time.
* New universal animation handling API for GPU & hybrid animator entities.
* Limit texture baking for :ref:`Animation Baker <animationBaker>`.
* Multi texture container for :ref:`Animation Baker <animationBaker>`.
* Added chasing cars feature.
* Path Waypoints can be traffic node functionality.
* Added endless streaming for :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road.
* Added :ref:`Auto-crossroad <roadSegmentCreatorAuto>` option for :ref:`Custom segment <roadSegmentCreatorCustomSegment>` for custom shape crossroads.
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