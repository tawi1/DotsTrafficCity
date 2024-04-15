.. _changeLog:

Change Log
************

[1.0.5] - 15-04-2024
------------

Added
~~~~~~~~~~~~

* New :ref:`multi-mesh <animationBakerHowToMulti>` customization support for GPU animations. 
* New custom :ref:`attachments <animationBakerHowToMulti>` support for GPU animations. 
* New custom GPU animation :ref:`option <crowdSkinFactory>` for selected pedestrians . 
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