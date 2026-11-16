.. _changeLog:

Change Log
**********

[1.9.6] - 15-11-2026
--------------------

Added
~~~~~

* Added new CrowdAvoidanceNavMeshPath navigation mode combining full NavMesh pathfinding with OBB-based vehicle & pedestrian crowd avoidance.
* ArcadeVehicleController: Added PerWheel and PerAxle transient anti-slip modes to fix idle yaw drift on uneven slopes, with fast-path optimizations for flat surfaces.
* Added Entities 7.0+ (Unity 7 alpha 16+) support.

Changed
~~~~~~~

* Renamed CrowdAvoidance NavMesh to CrowdAvoidance NavMesh Raycast avoidance type.

Fixed
~~~~~

* Fixed Multimesh combining for Bone skinning (remap bone weights, per-bone bindpose alignment).

[1.9.5] - 02-11-2026
--------------------

Added
~~~~~

* Added Unity 6.7 & Unity 7 support.
* Added Domain Reload Disabled support.
* Added preset caching to Car Prefab Creator.

Changed
~~~~~~~

* Renamed TransformRef to HybridTransformRef to prevent name collisions in Unity 7.

Fixed
~~~~~

* Fixed range attribute for SimpleVehicleController.

[1.9.4] - 18-10-2026
--------------------

Fixed
~~~~~

* Fixed hybrid mono traffic jitter/stutter when switching from culled to active physics state.
* Fixed culling state list attribute.
* Fixed missing asmdef reference for Netcode.

[1.9.3] - 14-10-2026
--------------------

Fixed
~~~~~

* Fixed potential jittering for Mono vehicles on flat surfaces.
* Fixed incorrect overtaking in the oncoming lane when it is occupied or lacks space to merge back.
* Fixed missing scripting directives when using only hybrid Mono simulation packages.
* Fixed incorrect offsetting during creation for non-default scale vehicles.
* Fixed obsolete API/warning messages in the Navigation package for Unity 6.3.
* Fixed Netcode compatibility regression from v1.9.2.

[1.9.2] - 05-10-2026
--------------------

Changed
~~~~~~~

* Removed `Preinit` culling layer. Use the `CullStateEntityAuthoring` (or `CullStateConfigEntityAuthoring`) component to override culling layer distances instead.

[1.9.1] - 03-10-2026
--------------------

Added
~~~~~

* Added Netcode for GameObjects support.
* Added emergency vehicle system support.
* Added ability to overtake in oncoming/opposite lanes.
* Added random horn sounding while overtaking.
* Added the ability to override traffic vehicle priority at intersections.

Fixed
~~~~~

* Fixed sorting of intersecting paths relative to the current path.

[1.9.0] - 05-09-2026
--------------------

Added
~~~~~

* Added universal networking sample for Mono networking.
* Added FishNet networking implementation sample for Mono vehicles.
* Added TrafficCustomBehaviorAuthoring component to allow per-entity driving behavior customization during vehicle spawn.
* Added gear sound simulation for traffic vehicles.

Fixed
~~~~~

* Fixed Netcode for Entities compatibility.
* Fixed weight on pedestrian sub-nodes causing incorrect navigation.
* Fixed hybrid attachment for Rukhanka for Unity 6.3+.

[1.8.5] - 14-08-2026
--------------------

Added
~~~~~

* Added new Crowd Avoidance NavMesh feature to bypass NavMesh obstacles and maintain correct Y-axis snapping along the NavMesh surface.

Changed
~~~~~~~

* Removed Reese Path Navigation package and replaced it with a built-in package.
* Renamed `Calc Nav Path` avoidance method to `Simple NavMesh`.
* Reduced oscillation issues for crowd avoidance method.

Fixed
~~~~~

* Fixed an exception when using Train Mono.

[1.8.4] - 10-08-2026
--------------------

Added
~~~~~

* Added motorcycle & three-wheeler templates for the Car Prefab Creator.

Fixed
~~~~~

* Fixed generation of sub-nodes for pedestrians if the starting node has a non-default type.

[1.8.3] - 09-08-2026
--------------------

Added
~~~~~

* Added truck with trailer support.
* Added compatibility to split long vehicles (e.g. buses) into multiple sub-entities for better obstacle detection at intersections.
* Added custom pedestrian groups for spawning and filtering group-specific node access.
* Added Spawn Weight field to PedestrianAuthoring to control individual prefab spawn probabilities.
* Updated crowd avoidance to merge multiple obstacles into a single one and avoid them correctly.
* Added pedestrian death after falling a certain distance during temporary ragdoll state.

Fixed
~~~~~

* Fixed NavMesh obstacle loading for vehicles [1.8.1 regression fix].
* Fixed potential X-axis rotation for pedestrians during crowd avoidance.

[1.8.2] - 26-07-2026
--------------------

Changed
~~~~~~~

* Improved physics for the simple mono vehicle controller.

Fixed
~~~~~

* Fixed a rare issue where traffic cars unexpectedly reversed due to a gas input delay.
* Fixed a rare issue where traffic with a passive driving style performed unexpected reverse avoidance maneuvers.

[1.8.1] - 24-07-2026
--------------------

Added
~~~~~

* Added new runtime generation sample scene demonstrating dynamic road segment generation from raw data.
* Added GameObjectRef entity component to reference a GameObject from an entity.

Changed
~~~~~~~

* TransformRef now uses TransformHandle for Unity 6.3+.
* Improved performance of entity synchronization between GameObjects and entities in Unity 6.3+.
* Improved performance of hybrid Mono traffic.
* Optimized the Arcade Vehicle Controller.
* Smoother transition from No Physics to DOTS traffic vehicle mode after disabling physics culling.
* Tweaked crowd avoidance configuration for better vehicle avoidance.

Fixed
~~~~~

* Fixed endless forward-and-back jitter near targets in crowd avoidance when close to a vehicle.
* Fixed pedestrian cornering generation for runtime segments created via auto crossroad generation.

[1.8.0] - 17-07-2026
--------------------

Added
~~~~~

* Added support for Unity 6.6+.
* Added Floating Origin system for DOTS & Mono with seamless hybrid synchronization for jitter-free massive maps.
* Added new `Traffic Demo` and `Traffic Demo Mobile` scenes.
* Added presets for the `Path Creator` to quickly save, reuse, and switch between path generation settings.
* Added road reuse protection for `Road Constructor`: automatically binds and reuses existing road segments during regeneration to prevent losing custom modifications.
* Added manual node overrides for `Road Constructor`: introduced an inspector panel to force crosswalks at road ends, configure custom offsets, and easily manage saved overrides.
* Added snapping for pedestrian nodes on road segments.

Changed
~~~~~~~

* Replaced all `managed components` with `UnityObjectRef` to reduce chunk fragmentation and speed up structural changes.
* Updated the position handle of road segments with a sphere to distinguish it from other handles.
* Tab selection index is now shared between road segment creators.

Fixed
~~~~~

* Fixed traffic cars potentially getting permanently stuck on pedestrians in a temporary ragdoll state.
* Fixed crowd avoidance for pedestrians on different floors.
* Fixed pedestrian node corners for one-way roads.
* Fixed the pedestrian animation stress scene.

[1.7.6] - 09-07-2026
--------------------

Added
~~~~~

* Added a new method to RuntimeSegmentCustom for directly adding runtime road data without needing RoadSceneUtils data containers.
* Added new dedicated pedestrian crosswalk creation methods to `RuntimeSegmentCustom`.

Changed
~~~~~~~

* The road segment placer has been removed for public use.

Fixed
~~~~~

* Fixed project update for some versions.
* Fixed a race condition issue for car sound systems.
* Fixed temporary ragdoll disappearance in some corner cases.
* Fixed the raycasting issue for mono vehicles when the Unity Physics package is removed.
* Fixed compilation when the Unity Physics or Entities Graphics package is removed.
* Fixed Rukhanka animation system when custom animation is in use.
* Fixed road segment generation from Unity splines.
* Fixed exception in Animation Baker when the animation collection is null.
* Fixed an exception that occurred during initial serialization of the dictionary when adding a component in the inspector.

[1.7.5] - 27-06-2026
--------------------

Changed
~~~~~~~

* Added updating from DOTS Traffic Core.
* RuntimeGenerationUtils uses a separate runtime pool.
* Moved subscene save path from the Hub prefab to EditorPrefs.
* Changed empty & idle input systems to run on the main thread.

Fixed
~~~~~

* Fixed potential issue with vehicle navigation breaking after avoidance.
* Improved avoidance of vehicles for the crowd avoidance method.
* Fixed pedestrian state when running through a crosswalk with a wait light state due to a fear trigger point.
* Fixed issue of losing focus in the inspector when entering the first digit for the speed limit.

[1.7.4] - 18-06-2026
--------------------

Added
~~~~~

* Added an additional safe distance parameter for lane-changing vehicles to prevent them from hitting the vehicle ahead.
* Added custom scaling support for Road Constructor roads.
* Added Unity 6.5 support.

Changed
~~~~~~~

* Improved global traffic light window for connecting merged traffic nodes with traffic lights.
* Improved path creator workflow with one-way roads to prevent incorrect connection side selection.

Fixed
~~~~~

* Fixed a potential endless stuck state during reverse avoidance.
* Fixed potential wrong raycast detection when many mono cars are in use with physics enabled.
* Fixed a warning message for the roundabout.

[1.7.3] - 12-06-2026
--------------------

Added
~~~~~

* Added transient forces for Arcade Vehicle Controller to prevent slipping on inclined surfaces.
* Added support for motorcycles & three-wheelers in Arcade Vehicle Controller.
* Added configurable boundary constraints for pedestrians on paths for the crowd avoidance method.

Changed
~~~~~~~

* Improved EasyRoads3D road generation depending on the prefabs used.
* Improved traffic light auto-reconnecting with the global traffic light tool for merged traffic nodes.

Fixed
~~~~~

* Fixed warning message for ReactionCollisionSystem.
* Fixed warning messages for Unity 6.4.

[1.7.2] - 15-05-2026
--------------------

Added
~~~~~

* New crowd avoidance navigation method [beta].
* Added a new feature: the temporary ragdoll will now get up after being hit by a car.
* New ability to link custom user runtime NPCs with the pedestrian system.
* Added pathfinding support for parking nodes.
* Added ability to turn on ignoring traffic lights for traffic.

[1.7.1] - 28-03-2026
--------------------

Changed
~~~~~~~

* Added a new clear job for hashmap systems.

Fixed
~~~~~

* Fixed physics culling for DOTS physics cars.
* Fixed baking order for simple physics cars to avoid a potential exception.

[1.7.0] - 25-03-2026
--------------------

Added
~~~~~

* Added support for `NetCode for Entities`.
* Added support for multiple cull points for local split-screen multiplayer.
* Reworked the GPU animation engine, which reduces the overall number of draw calls, adds custom timings for each animation, and provides a more convenient workflow.
* Added support for runtime attachments & animation events for GPU animations.
* Added custom animation speed for walking animations for each entity across all animation engines (`Unity Animator`, `Built-In GPU Engine`, `Rukhanka`, and `Animatron`).
* Added ability to add runtime pedestrian nodes for custom pedestrian routes or buildings.
* Added methods for adding runtime custom roads by custom chunks to reduce frame overhead during the creation of large maps at runtime.
* Added a new parameter to reduce or prevent overtaking from the road side.
* Added checking the opposite lane for obstacles during avoidance on straight roads.
* Added a new option for adding different wagons to trains at runtime.
* Improved precision for obstacle detection on narrow roads.
* Added position handles for the default type of segments.
* Added mono vehicles to the `Polygon City` template.
* Added choice for entity types in the `Hub` selection window.
* Added 3 new weapons to the `Demo Mono` scene.
* Added `Roundabout` support for the `Road Constructor` editor scene.
* Added Unity 6.4 support.

Changed
~~~~~~~

* Improved the performance of some high-load systems.
* Improved parking navigation for traffic.
* Improved `EasyRoads3D` generation.
* Significantly improved performance of adding runtime roads for giant maps.
* All of the demo city scene prefabs have been moved to separate presets.
* Improved `Roundabout` template workflow.

Fixed
~~~~~

* Fixed the build size for giant entity scenes.
* Fixed a potential exception in the avoidance system.
* Fixed avoidance at intersections in some cases.
* Fixed jittering for no-physics cars during avoidance.
* Fixed speeding of approaching vehicles with custom behavior.
* Fixed the roundabout template when the entrance traffic node has a different lane count than the inner traffic nodes.
* Fixed compatibility with the latest `Polygon City` template.
* Fixed collision avoidance for DOTS vehicles in traffic areas.
* Fixed `Trigger and Destroy` type for `Traffic node`.

[1.6.5] - 08-01-2026
--------------------

Added
~~~~~

* Added custom post-processing for mono cars during car creation in the Car Prefab Creator.

Fixed
~~~~~

* Fixed targeting for custom physics vehicles in some corner cases.
* Fixed weight parameter for mono cars in the Car Prefab Creator.
* Fixed navigation for a parking segment when merged with another segment.
* Fixed lane changing during A* navigation in some corner cases.

[1.6.4] - 31-12-2025
--------------------

Added
~~~~~

* Added Unity vehicle support.
* Added a `CarPlayerBlocker` component for mono traffic to prevent the player from pushing the car when using a custom controller.

Changed
~~~~~~~

* 2 unused layers were removed from the demo scene.

Fixed
~~~~~

* Removed scheduling from Begin Simulation Systems to prevent potential structural changes during jobs.
* Fixed Road Constructor generation in some cases.
* Fixed the demo's mono bullet collision with pedestrians.
* Fixed the player demo's shooting on non-flat surfaces.

[1.6.3] - 28-11-2025
--------------------

Fixed
~~~~~

* Fixed the missing driving sound for cars.
* Fixed player interaction with cars in Demo scenes.

[1.6.2] - 24-11-2025
--------------------

Fixed
~~~~~

* Fixed compatibility with Unity 2022.3.
* Fixed PathHashMapSystem Burst error message.

[1.6.1] - 21-11-2025
--------------------

Added
~~~~~

* Added the ability to change lanes during built-in A* navigation for traffic.
* Added the ability to route traffic to a user-defined point.
* Added new events for spawning and reaching the target for pedestrians.

Changed
~~~~~~~

* The project no longer overrides constant scripts and enums during version updates.

Fixed
~~~~~

* Fixed unexpected acceleration beyond the maximum speed for mono cars.
* Fixed an issue where traffic lights failed to link with the crossroad when placed in an arbitrary hierarchy while moving the entity root back to the main scene.
* Fixed potential warning messages after subscene generation.
* Fixed Road Constructor traffic lights integration.
* Fixed Road Constructor setting the wrong speed limit for the runtime scene.
* Fixed auto-crossroad generation for left-hand driving.
* Fixed a minor memory leak in the traffic test scene.

[1.6.0] - 09-11-2025
--------------------

Added
~~~~~

* Added `Animatron` support.
* Added a new `API` & `Runtime RawData Demo` scene that demonstrates the generation of a road from raw data at runtime.
* Added a new obstacle detection method for traffic at intersections to improve accuracy in some corner cases.
* Added tools to the `Road Segment Creator` for quickly merging `Traffic nodes`, creating new `Traffic nodes`, and creating a new `Road segment` from an existing one.
* Added auto-crossroad recalculation during editing.
* Added support for single or multi-container splines in the `Road Segment Creator`.
* Added smooth corners of pedestrian nodes for `Custom road segment`.
* Added validation for traffic lights.
* Added auto-connect for custom segments that are added during runtime.
* Added U-turn support for runtime roads.
* Added `RuntimeSegmentCustomView` helper scene component to view `RuntimeSegmentCustom` data.
* Added support for custom lane counts for the forward & backward directions of traffic nodes for custom runtime roads.
* Added support for merged roads in custom runtime roads.

Changed
~~~~~~~

* Improved along-path generation of pedestrian nodes for `Custom straight road segment`.
* `MonoBehaviour` inheritance was removed from the `RuntimeSegmentCustom` script to reduce overhead.
* Editor metadata was removed from the serializable dictionary.

Fixed
~~~~~

* Fixed deprecation messages for `Entities 1.4.2` & `Unity 6.3`.
* Fixed compatibility with Rukhanka 2.5.0+.
* Fixed a potential NaN destination for traffic in rare cases.
* Fixed raycast for DOTS cars & obstacle detection outside their path.
* Fixed unexpected avoidance activation for traffic on long roads in some cases.
* Fixed the path drawer exception at the start of the scene if it was initially enabled.
* Fixed simple mono preset.
* Fixed cyclic obstacle avoidance case.
* Fixed `Road Constructor` generation in some cases.

[1.5.0] - 30-09-2025
--------------------

Added
~~~~~

* Added new option to enable different driving styles for traffic.
* Added random lateral offset for traffic.
* Added ability for traffic to avoid player & custom obstacles.
* Added `GPU` skinning bone animation method to significantly reduce texture memory usage.
* Added new lightweight simple vehicle controller for mono cars.
* Added new sample for Arcade Vehicle Controller with heavy mass.
* Demo project importing according to user choice at start.
* Added ability to choose which toolbar path to use for a project in the editor.
* Added an option to cull vehicle sounds based on distance.
* Added spawn weights for pedestrian NPCs.
* Hybrid shape factory can override hybrid shapes for certain pedestrians.
* Added `Static transform hybrid component` for static runtime entities.
* Added capability to select unique car models for each lane in the `Traffic road debugger` component.
* Added new API to find the closest traffic path or pedestrian node entity to a given point in the scene.
* Added validation for Traffic Area authoring.

Changed
~~~~~~~

* `Entities.Graphics` package is no longer required if Mono physics cars & Hybrid Legacy pedestrians are in use.
* `Unity.Physics` package is no longer required if NoPhysics or Mono physics cars are in use.
* `Cinemachine` package is no longer required.
* Polygon City sample updated with new GPU animations.
* City Pack sample updated with new GPU animations.
* Improved path recalculation during parking builder mode.

Fixed
~~~~~

* Fixed `RaycastCommand` for Arcade vehicles for Unity 6.2.
* Fixed potential vehicle rollover for simple physics cars.
* Fixed pedestrians getting stuck in cars due to car movement during local avoidance.
* Fixed an issue with invalid input for mono traffic cars when reversing in rare cases.
* Fixed an issue with obstacle detection at intersections when both vehicles were targeting the same destination.
* Fixed compatibility with Road Constructor 1.7.0+.

[1.4.4] - 29-08-2025
--------------------

Changed
~~~~~~~

* Added traffic light cloning for traffic lights that are part of a road prefab.

Fixed
~~~~~

* Fixed installation on Unity 6.2.
* Fixed a potential jitter for Arcade Vehicle Controller on Unity 6+.
* Fixed compatibility with Agents Navigation 4.2.0+.
* Fixed disappearing traffic lights during subscene generation in some corner cases.
* Fixed movement for simple DOTS vehicles.
* Fixed truncation warning for animation shader.

[1.4.3] - 01-07-2025
--------------------

Added
~~~~~

* A crosswalk node type has been added for crosswalks without traffic nodes.
* Added crosswalk system for pedestrians crossing the road at the crosswalk node type.
* Added NPC obstacle with a flexible detection area based on vehicle speed.
* NPC obstacle offset authoring has been added for certain vehicles that require a custom offset for NPC obstacle detection.

Fixed
~~~~~

* Fixed Road Constructor compatibility.
* Fixed A* compatibility.
* Fixed rotation of attachments for Rukhanka hybrid pedestrians.
* Fixed Rukhanka hybrid animation event registration.
* Fixed chaser controller spawn.
* Fixed Car Prefab Creator in some corner cases.

[1.4.2b] - 08-05-2025
---------------------

Fixed
~~~~~

* Fixed ragdoll system exception for Hybrid pedestrians.
* Fixed sound looping for custom user sounds.

[1.4.2] - 05-05-2025
--------------------

Added
~~~~~

* Added support for parking & one-way roads for the runtime tile sample.
* Added support for custom pedestrian node types for the runtime tile sample.
* Added support for `Rukhanka Animation System` ragdoll.
* Added new player-interactive car system for mono players.
* Added ability to invoke a callback for user-spawned entities.
* Added ability to merge `Traffic nodes` with `Road parent`.
* Added support for manual user connection of merged nodes in `Path creator` & `Pedestrian node` connection.
* Added talk animation config.
* Added ragdoll syncing with GPU animations.
* Added ability to use `Mesh Collider` in `Car Prefab Creator` for mono cars.

Changed
~~~~~~~

* Improved MicroVerse Roads workflow.

Fixed
~~~~~

* Fixed speed limit setting for custom straight roads.
* Fixed rare wrong obstacle calculation on intersecting roads.
* Fixed car system order for DOTS cars which could cause an initial jump.
* Fixed traffic path service registration when not all sample services are in the scene.
* Fixed talk area NPC randomization.
* Fixed parking for Toon City template.
* Fixed sound tracking for built-in sound engine for DOTS cars.
* Fixed rail movement for DOTS cars.
* Fixed player interaction with cars when the car ignition option is disabled.
* Fixed starting shooting before reload finished for the built-in controller in the sample scene.

[1.4.1] - 17-03-2025
--------------------

Added
~~~~~

* Added new `Runtime CustomRoad Demo` scene to demonstrate the use of the `API` to generate runtime roads from `Unity` spline roads or from custom data.
* Added support for priority intersections without traffic lights for custom runtime roads.
* Added gizmos for RuntimeRoadManagerCustom for nodes.

Fixed
~~~~~

* Fixed drawing of road segment paths after segment rotation.
* Fixed position handle when moving multiple road segments at the same time.
* Fixed root detection when different projects have different path roots.
* Fixed external connection path if the source lane index is different from the connected lane index.

[1.4.0b] - 07-03-2025
---------------------

Fixed
~~~~~

* Fixed initial installation for Unity 2022.3.
* Fixed wrong skin index selection for Hybrid Shape GPU.

[1.4.0] - 05-03-2025
--------------------

Added
~~~~~

* Added support for `MicroVerse Roads`.
* Added support for `CityGen3D`.
* Added support for Aron's A* Pathfinding Project (point graph for traffic & pedestrians).
* Added multithreaded raycasting for `Arcade Car Controller` to improve overall performance.
* Added `Roundabout` template for `Road Segment Creator`.
* Added a new option for non-physics pedestrians to precisely follow tilted surfaces.
* Added new external runtime connection for runtime segments for custom solutions.

Changed
~~~~~~~

* All presets & prefabs are packed in separate packages so the project can be updated seamlessly without overwriting edited presets.
* Significantly improved performance of built-in A* pathing for large numbers of entities searching for a path simultaneously.

[1.3.2] - 21-02-2025
--------------------

Fixed
~~~~~

* Fixed `Pedestrian node creator` attachment to surface when attach to mesh is selected.
* Fixed road segment creator drag position handle for the new gizmos system.
* Fixed inspector for traffic light converter for `Road Constructor` if a custom inspector is used.
* Fixed `Path data viewer` for the new gizmos system.

[1.3.1] - 31-01-2025
--------------------

Added
~~~~~

* Added new trigger node type for traffic and pedestrian nodes to invoke a callback when an entity reaches the node.
* Added compatibility to auto-generate intersections between selected straight roads.
* Traffic nodes can now hold different lane counts for forward and backward lanes.
* Added input limit steering based on vehicle speed to stabilize when FPS drops below 30 in `Editor` or at high speeds.
* Added pre-built template roads for `Fantastic City Generator`.
* Added `TrafficIdleStateDebugger` for a handy display of all the reasons why a car is idling.
* `Traffic Object Finder` & `Path Data Viewer` can be used in `Prefab Stage`.
* Added hotkeys for `Path Creator`.
* Added `UGizmos` plugin to improve the performance of gizmos.

Fixed
~~~~~

* Fixed potential exceptions in `Runtime Tile Road Demo`.
* Fixed auto-crossroad generation causing incorrect connection paths.
* Fixed `ID` not being generated for `TrafficLightCrossroad`.
* Fixed editor performance leak caused by frequent loading of editor settings.
* Fixed recalculation of connected paths for custom straight one-way roads in the `Prefab Stage`.

Changed
~~~~~~~

* Improved editor performance of gizmos.
* Now the project can be used completely without the old input system.

[1.3.0] - 15-01-2025
--------------------

Added
~~~~~

* Added support for `Road Constructor` for editor & runtime.
* Added support for `Fantastic City Generator` for editor & runtime generation.
* Added support for `Rukhanka Animation System` for pure & hybrid modes.
* New A* Traffic & Pedestrian navigation added to user-selected nodes.
* Added `API` for runtime pedestrian node paths.
* Added `API` to generate road segments from custom user code or Unity splines.
* Added runtime buildings for the runtime demo scene.
* New ability to create U-turns with `Path Creator` & `Road Segment Creator`.
* New utility buttons for disconnecting automatically connected pedestrian & traffic nodes.
* Added car lights for hybrid mono cars.
* Added new options to change lanes based on the speed of the car in front or randomly.
* Added a new `CustomAreaTriggerCreatorSystem` to create fear triggers from custom user code.
* Added priority-to-right option at intersections for cars with the same priority.

Fixed
~~~~~

* Fixed potential crash on some devices.
* Fixed bounds calculation in some cases that could cause incorrect avoidance or obstacle detection.
* Fixed Traffic Change Lane Config enable option not being enabled in some cases.
* Fixed incorrect removal index for connected paths for runtime roads.
* Fixed potential exception when using auto-sync config in `Editor`.
* Fixed ID reset when spawning built-in NPC player.
* Fixed path index debugger not being initialized.
* Fixed editor memory leak caused by `TrafficNpcCalculateObstacleSystem`.

Changed
~~~~~~~

* By default, a clean scene is created with a clean `HubBase` without any extra dependencies.
* Improved `ArcadeVehicleController` braking & suspension.
* Improved some corner cases of generation for different types of crossroads.
* Now runtime segments are connected with the raycast method.

[1.2.2] - 27-11-2024
--------------------

Added
~~~~~

* Added new `Hybrid On Request And GPU` pedestrian type for manual control handling transitions between Hybrid & GPU pedestrians.
* Added entity selection example script.
* Added `Hybrid` pedestrian support with a Rigidbody that is affected by gravity.
* Added mobile version of `RuntimeTile Road demo`.
* Node navigation example for traffic.
* Added ability to temporarily disable & enable traffic simulation in `Runtime Road Manager`.
* Added an API to get road entities in `Runtime Road Manager` using road scene objects.

Fixed
~~~~~

* Fixed potential incorrect init for mono trains.
* Fixed potential lane change issue when the route is not on a flat surface.

Changed
~~~~~~~

* Major refactoring of the system order & system registration to significantly reduce the number of sync points.
* `Traffic Car` will by default take the path with the fewest cars in `RuntimeRoad mode`.
* `Runtime tile demo scene` now has 3 traffic lights at each intersection.
* Removed `Dummy` skin.

[1.2.1c] - 08-11-2024
---------------------

Fixed
~~~~~

* Fixed rare endless stuck state for traffic cars when using raycast.
* Fixed collision system calculation.
* Fixed tile chunk prefab example.

Changed
~~~~~~~

* Added an option to change some general settings from the corresponding configs.
* :ref:`Path creator <pathCreator>` can be used in the `Prefab stage`.
* :ref:`Global Light Settings <trafficLightGlobalLight>` can be used in the `Prefab stage`.
* :ref:`Road segment <roadSegment>` can be created in the `Prefab stage`.

[1.2.1b] - 06-11-2024
---------------------

Added
~~~~~

* Added support for lane changing on runtime roads.
* Added a helper button for traffic lights that have lost their reference to a traffic light crossroad.
* Added support for `Odin Inspector`.

Fixed
~~~~~

* Fixed intersection conversion for runtime road chunks.

[1.2.1] - 04-11-2024
--------------------

Added
~~~~~

* Added support for `Multi-road segments` by adding 1 `RuntimeSegment` at a time in `Runtime Road mode`.
* Added new `RuntimeTile Chunk Road demo` to demonstrate road chunks added at runtime.
* Added a new option to leave the car idle for a certain amount of time when parking if pedestrians are disabled for the scene.
* Parking can be used on sloped surfaces.
* Added auto-curve type detection for :ref:`Path creator <pathCreator>`.

Fixed
~~~~~

* Fixed :ref:`path <path>` intersection calculation for custom shape surfaces.
* Minor fix in `Car prefab creator` text pattern search for wheels.
* Fixed :ref:`Animation Baker <animationBaker>` baking with a single texture atlas for multi-mesh characters.
* Fixed a problem with `Local Avoidance` switching multi-targeting in a short amount of time.

Changed
~~~~~~~

* Improved obstacle detection in intersecting & neighbouring cases.

[1.2.0] - 28-10-2024
--------------------

Added
~~~~~

* Runtime graph creation.
* Added new `RuntimeTile Demo` scene.
* Traffic light `API` to get traffic light state from a MonoBehaviour script.
* Added option to manually handle traffic light state.
* New train system.
* Custom train system support.
* Custom train demo scene.
* Added the ability to split :ref:`external traffic routes <trafficNodeConnectionInfo>` into smaller ones to better balance spawning.
* Added custom settings for pedestrian nodes for selected routes.
* Added the ability to split pedestrian routes into smaller ones to better balance spawning.
* New `TriggerLight` type for :ref:`TrafficNode <trafficNode>`, which triggers the selected traffic light when a traffic car enters this node.
* The :ref:`Traffic Road Debugger <testSceneTrafficCarRoadDebugger>` can be used at runtime to manually spawn vehicles in custom scenarios.
* Added saving of :ref:`Road Segment Creator <roadSegmentCreator>` settings so that a new road segment is created using the previously saved settings.
* Added a handy duplicate feature for existing connected :ref:`Road Segment Creator <roadSegmentCreator>` segments to create clean duplicates without existing connected paths.
* Added a sample custom player to interact with custom cars & pedestrians.
* Added one-way roads for pedestrian nodes.
* Added manual sync button for all configs.

Fixed
~~~~~

* Fixed car creation offset for car parts when the car parts are not children of the car body.
* Fixed wheel detection during car creation in some cases.
* Fixed adding trigger area tag to non-pedestrian entities.
* Fixed :ref:`Auto-crossroad <roadSegmentCreatorAuto>` generation when the custom segment contains one-way paths.
* Fixed Path Creator detecting wrong connection sides in some cases.
* Fixed steering input being incorrectly calculated in some cases.

Changed
~~~~~~~

* Now the road `Graph` is created at runtime when the scene starts.
* `Cinemachine v3` is used by default.
* Traffic light states for each traffic light handler are now stored in a dynamic buffer.
* Improved randomization of initial pedestrian spawn.
* Added traffic light debugging for paths with custom lights.

[1.1.0g] - 19-09-2024
---------------------

Fixed
~~~~~

* Crossroad jam obstacle fix.
* Fixed sound pooling when a vehicle is destroyed.
* Fixed lane change potential obstacle stuck state when multiple cars are changing to the same lane.
* Fixed avoidance of mono cars when trying to change lanes.
* Fixed custom traffic light for a specific path.
* Fixed initial `HDRP` installation conflict with `Cinemachine v3` package.

[1.1.0f] - 10-09-2024
---------------------

Changed
~~~~~~~

* Improved `NPC` obstacle detection.

Fixed
~~~~~

* `TrafficNpcCalculateObstacleSystem` debug race condition fixed.
* Anti-roll fix for `Arcade Vehicle Controller`.
* Fixed warning messages.
* Fixed potential config sync failure in some cases.
* Fixed missing reference in `PolygonCity`.
* Fixed `EasyRoads3D` exception when a crossing has 1 connecting road.

[1.1.0e] - 16-08-2024
---------------------

Added
~~~~~

* Auto-crosswalk connection in the :ref:`Road Parent <roadParentInfo>`.
* Auto-connection distance in the :ref:`Road Parent <roadParentInfo>`.
* Added new road warning messages.
* New `Agents Navigation` config.
* New agent hybrid component.

Fixed
~~~~~

* Fixed move handle for moving two or more road segments.
* Crowd sound system dependency fix.
* Fixed `Ragdoll` not being pooled.

Changed
~~~~~~~

* Improved :ref:`Road Parent <roadParentInfo>` UI.

[1.1.0d] - 12-08-2024
---------------------

Added
~~~~~

* Interpolation of the car view for culled mono physics cars.
* New collision stuck avoidance system for :ref:`Hybrid mono <hybridMonoVehicle>` cars.

Fixed
~~~~~

* Agents Navigation integration editor error fix.
* Minor player arcade car prefab fix.
* Traffic node viewer fix.

Changed
~~~~~~~

* Improved transition between physics & no-physics arcade cars.

[1.1.0c] - 09-08-2024
---------------------

Added
~~~~~

* New auto-sync config option between MainScene & Subscene.
* Traffic node gizmos settings.
* New pure city stress scene.

Fixed
~~~~~

* Minor script fix for Unity 2023.2.
* Fixed potential config corruption for builds.
* Fixed stress scene demo exit error.
* Arcade vehicle controller wheel position fix.

Changed
~~~~~~~

* Minimum `Unity` version 2022.3.21.
* Improved arcade sample cars.

[1.1.0b] - 06-08-2024
---------------------

Added
~~~~~

* Added `CarModelRuntimeAuthoring`, `BoundsRuntimeAuthoring`, `VelocityRuntimeAuthoring` entity runtime components.

Fixed
~~~~~

* Fixed compatibility with Entities 1.3.0.
* Fixed initial entity scale for runtime entities with `CopyTransformFromGameObject` component.
* Fixed bootstrap if user tries to start bootstrap twice.
* FMOD minor script fix.
* Nav agents dependency fix.

[1.1.0] - 05-08-2024
--------------------

Added
~~~~~

* Full `Hybrid mode` support:
	* New :ref:`monobehaviour compatible <hybridMonoVehicle>` traffic.
	* New hybrid NPCs compatible with any custom character controller.
	* New hybrid traffic lights.
* New `EasyRoads3D <https://assetstore.unity.com/packages/tools/terrain/easyroads3d-pro-v3-469>`_ integration.
* New `Agents Navigation <https://assetstore.unity.com/packages/tools/behavior-ai/agents-navigation-239233>`_ integration.
* New `API` for custom spline road generation.
* New `EntityWeakRef` class to link MonoBehaviour scripts with traffic & pedestrian node entities.
* New player traffic control feature.
* New runtime entity hybrid workflow for runtime GameObjects.
* New hybrid GPU mode that allows you to mix hybrid animator models for near view and GPU animation for far view at the same time.
* New universal animation handling API for GPU & hybrid animator entities.
* Limit texture baking for :ref:`Animation Baker <animationBaker>`.
* Multi-texture container for :ref:`Animation Baker <animationBaker>`.
* Added chasing cars feature.
* Path waypoints can use traffic node functionality.
* Added endless streaming for :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road.
* Added :ref:`Auto-crossroad <roadSegmentCreatorAuto>` option for :ref:`Custom segment <roadSegmentCreatorCustomSegment>` for custom shape crossroads.
* Pedestrian node generation along :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road.
* :ref:`Custom straight <roadSegmentCreatorCustomStraight>` can be converted into a :ref:`Custom segment <roadSegmentCreatorCustomSegment>` road.
* Crosswalk connection for :ref:`Custom segment <roadSegmentCreatorCustomSegment>`.
* Added left-hand traffic option.
* Custom cull state config calculation for specific entities.
* New camera-view-based culling calculation method.
* New spawn culling layer adjustment for traffic & pedestrians.
* New traffic node display for right & left lanes in segments & path spawn nodes.
* Traffic & pedestrian node debug in `Editor` mode.
* New project initialization window.
* Added support for Unity's built-in audio engine.
* Added :ref:`HDRP <hdrp>` support.

Fixed
~~~~~

* Fixed traffic spawning in culled areas.
* Fixed custom physics vehicles jumping after restoring physics at runtime in some cases.
* Fixed a potential crash when undoing changes on :ref:`Custom straight <roadSegmentCreatorCustomStraight>` roads.
* Fixed obstacle detection for neighbouring paths.
* Fixed `Player spawner` not spawning in some cases when adding a new `ID` for player NPCs.
* Player spawner no longer throws an exception if the player doesn't exist.
* Fixed `Input` for `Player car` in `Editor` when `Android` build is selected.
* Fixed road segment merge.

Changed
~~~~~~~

* Major refactoring of the project to make it more modular.
* Now the project can be used for traffic simulation only, without player & extra features.
* Project no longer overwrites settings by default.
* FMOD is no longer a required package.
* Removed `NaughtyAttributes` dependency.
* `Zenject` is now an optional dependency.
* Now all sound data is stored in the `SoundDataContainer` ScriptableObject.
* Min `Burst` version 1.8.16 for `Unity` 2022.3.31 or higher.

[1.0.7d] - 06-06-2024
---------------------

Added
~~~~~

* Create & connect :ref:`Pedestrian nodes <pedestrianNode>` in the prefab stage.
* Added Gradle config for Android for Unity 6.
* Added support for `Cinemachine 3.0+ <https://docs.unity3d.com/Packages/com.unity.cinemachine@3.0/manual/index.html>`_.

Fixed
~~~~~

* Fixed Unity package dependency resolving for the first time causing endless script compilation.
* Fixed :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road having null traffic nodes during initial creation in some cases.
* Fixed :ref:`Custom straight <roadSegmentCreatorCustomStraight>` road one-way path generation with multiple lanes.
* Fixed :ref:`Custom segment <roadSegmentCreatorCustomSegment>` path surface snapping.
* Fixed :ref:`Pedestrian node creator <pedestrianNodeCreator>` losing SceneView focus, causing its hotkey to be disabled.
* Animation Baker minor UI fixes & improvements.

[1.0.7c] - 31-05-2024
---------------------

Fixed
~~~~~

* Fixed package initialization window not loading in some cases.
* Fixed package initialization window appearing randomly on macOS.

[1.0.7b] - 29-05-2024
---------------------

Added
~~~~~

* Auto-bootstrap option for a single scene.
* Bootstrap logging.
* Entity road drawer for editor time.

Fixed
~~~~~

* Car Prefab Creator ID duplicate error.
* Script defines after project update.
* Input in the custom vehicle test scene.

[1.0.7] - 24-05-2024
--------------------

Added
~~~~~

* New auto-spline option for `Bezier` curves in the :ref:`Path Creator <pathCreator>`.
* New :ref:`extrude lane <extrudeLane>` option for :ref:`Custom segment <roadSegmentCreatorCustomSegment>` road in the :ref:`RoadSegmentCreator <roadSegmentCreator>`.
* New divider line for :ref:`Traffic nodes <trafficNode>` & :ref:`Custom straight <roadSegmentCreatorCustomStraight>` roads.
* New components to interact with :ref:`Hybrid pedestrians <pedestrianHybridLegacy>` from `MonoBehaviours`.
* Custom user ragdoll support for :ref:`Hybrid pedestrians <pedestrianHybridLegacy>`.
* New custom IDs for vehicles in the :ref:`Car Prefab Creator <carPrefabCreator>`.
* New car model selection list for the :ref:`player spawner <playerSpawner>` when the player is spawned in a car.
* User :ref:`custom camera <customCamera>` integration.

Fixed
~~~~~

* Fixed :ref:`Pedestrian node <pedestrianNode>` connection on custom terrain shapes in the :ref:`Pedestrian node creator <pedestrianNodeCreator>`.
* Fixed auto-switch type for one-way paths in the :ref:`Path Creator <pathCreator>`.
* Fixed player spawn when the player originally spawned in a car.
* Fixed a potential `Type mismatch` error for animation clips in :ref:`Animation Baker <animationBaker>` which could cause the UI to break.
* Fixed a potential `NaN` position for pedestrians in the `Antistuck system`.
* Fixed traffic spawner for the path with `0` index.
* Fixed compatibility with Unity 2023.2.

Changed
~~~~~~~

* :ref:`Pedestrian node <pedestrianNode>` scene filtering updates when node settings are changed in the :ref:`Pedestrian node creator <pedestrianNodeCreator>`.
* `PedestrianReferences` component renamed to `PedestrianEntityRef`.

[1.0.6] - 22-04-2024
--------------------

Added
~~~~~

* New connection type for :ref:`Path Creator <pathCreator>`.
* New :ref:`traffic light <roadSegmentCreatorLightSettings>` customizations for Road Segment Creator tool.
* New :ref:`crosswalk node shape <pedestrianNodeSettings>` option for :ref:`Road Segment Creator <roadSegmentCreator>`.
* New state utility methods for pedestrians.

Fixed
~~~~~

* Fixed path connection for Path Creator in some cases.
* Fix for traffic light duplication when editing a road segment in the subscene.

Changed
~~~~~~~

* UX improvement for Path Creator.

[1.0.5] - 15-04-2024
--------------------

Added
~~~~~

* New :ref:`multi-mesh <animationBakerHowToMulti>` customization support for GPU animations.
* New custom :ref:`attachments <animationBakerHowToMulti>` support for GPU animations.
* New custom GPU animation :ref:`option <animationGPUAnimationCollection>` for selected pedestrians.
* Integration for custom :ref:`player vehicle controller <playerHybridMono>` plugins controlled by MonoBehaviour scripts **[experimental]**.

Fixed
~~~~~

* Animation GPU baking with animated parent.
* Fixed physics surface cloning tool in some cases.
* Traffic spawn fix in some cases.
* Fixed obstacle detection for reverse or arc paths.
* Static physics culling.

Changed
~~~~~~~

* Traffic lights are disabled by default for straight road templates.
* Removed obsolete options for Car Prefab Creator.

[1.0.4] - 04-04-2024
--------------------

Added
~~~~~

* New align custom straight road feature :ref:`along the surface <snapLine>`.
* New animation baker clip binding.

Fixed
~~~~~

* Path recalculation for custom straight roads.
* Re-creation of the road segment with custom user orientation.
* Fixed waypoint info display for road segments in some cases.

Changed
~~~~~~~

* Improved :ref:`snapping <roadSegmentCreatorCustomSnapNodeSettings>` for custom road segments.

[1.0.3b] - 01-04-2024
---------------------

Fixed
~~~~~

* First init editor hotfix.
* Path baking validation fix.

[1.0.3] - 29-03-2024
--------------------

Added
~~~~~

* Added GPU animation :ref:`transition preview <animationTransitionEditor>`.
* New optimized shaders for crowds.
* GPU data preparation for LODs.
* New user-friendly animation shader control.

Changed
~~~~~~~

* Updated to Entities 1.2.0.
* GPU animation baking and playback algorithm for better memory texture layout.
* Improved GPU transition animations.

[1.0.2] - 25-03-2024
--------------------

Added
~~~~~

* New movement speed randomization for pedestrians.

Fixed
~~~~~

* A rare build crash caused by the area trigger system.
* Fixed the pedestrian physics runtime option in the build.
* Mobile input for build.

[1.0.1b] - 22-03-2024
---------------------

Fixed
~~~~~

* Traffic mask settings editor fix.
* Script refactoring.

[1.0.1] - 20-03-2024
--------------------

Fixed
~~~~~

* Missing script hotfix.

[1.0.0] - 19-03-2024
--------------------

* Initial release.