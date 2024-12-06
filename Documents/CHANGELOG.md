# Changelog

## v0.1.2
Day 1 Patch

### Features
* Auto-walk is now auto-run

### Fixes
Flight Animation:
* Fix a bug where when the distance on the geodesic could not be calculated, the animation would blend to default orientation
* The helicopter animation now hovers above the target location until the target position is known precisely

Backend and Analytics:
* Fix curl tasks being reused whilst being executed on the worker thread
* Retry authentication/connection to the waypoint server every 30 seconds, don't just give up at start time
* Avoid truncating crash logs for GPU crashes 

Crashes:
* Fix a crash when changing borderless → full-screen and using Alt+Tab

UX:
* Fix main display screen being saved as screen mode
* Fix some UI elements calculating scaling incorrectly
* Adjust UI element positions
* Improve user messaging when (failing to) use integrated graphics cards

Assets:
* Improve UV seams on the Beech Tree

Performance:
* Optimize GPU vertex cache usage with indexed buffers for some object types

Audio:
* Play correct sound effect when creating a postcard with periscope view active

## v0.1.1

Day 0 Hotfix

* Taking a postcard now registers as a screenshot in Steam
* Fixed some asset issues with the Beech Tree and Birch Bush
* Fixed an issue where failing to connect to the backend whilst loading caused loading to take longer

## v0.1.0

First Release!
