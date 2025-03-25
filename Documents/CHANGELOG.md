# Changelog

## v0.1.6

### Known Issues

* Switching to Windowed mode from Borderless Fullscreen can cause the title bar to be out of your monitor's resolution
    * This is already fixed internally and will be fixed with the next patch
* The current texture upsampling model generates some artifacts, rainbow-coloured areas. This will be fixed next model updates.
* There are noticeable seams along the quadtree borders at large scale. This is caused by the basemaps currently not being seamless. There will be a new update of the basemap with seamless borders.
 
### Features

* Added a fixed altitude flying camera mode (Q/E keys and gamepad)
    * Prevent waypoint requests whilst above a certain altitude to avoid network saturation
* LOD/Impostor transition
    * Impostors now consistently appear once you exceed the farthest geometric LOD, avoiding sudden disappearances in distant scenery.
* Log Driver Version
    * We now log the user's driver version on startup, as this information can help us understand and fix bugs
      
### Fixes

* Addressed several shutdown, invalid-entity, and concurrency edge cases
* Rendering
    * Fixed motion vectors and perspective-correct velocity calculations
    * Motion Blur: Correctly handles colour and velocity buffers of different sizes
    * Correctly clears and updates sorted instance counters for occlusion
    * Improved performance of Atmospheric Scattering by slightly reducing sample counts
* Planet
    * Properly applies configured planet radius (removes hard-coded Earth radius)
        * Resolved far-plane NaN issues at small planet sizes
        * There are still a lot of known issues for non-earth sized planets
          
### Invisible/Upcoming Work

* ECS Concurrency & Refactoring
    * Introduced automatic deferral of ECS modifications, thread-local recorders, and concurrency detection
    * Removed or refactored deprecated systems (e.g. old texture load, physics, sim-state)
    * Consolidated typed entity-access APIs for simpler and safer ECS usage
* Prototypes
    * Note: some prototypes require compile-time changes and cannot be enabled through SQL configuration - but others can.
    * Oceans
    * Height and Distance Fog
    * Using the Docking branch for Dear ImGui - allowing developer UI to be moved outside the main window


## v0.1.5

### Known Issues

* Multi monitor setups may show the window on the wrong monitor.
* Windowed mode allows setting a too large resolution, which does not fit on screen. Use alt-enter to fix it.
* Sometimes when switching display mode and resolution simultaneously, the resolution will not be applied.

### Features

* Added LUT-based color correction, allowing custom color grading based on screenshots in the future. (PST-2131)
* Added a new API for logging and asserts which should improve detection of issues (PST-2006)

### Fixes

* Rendering Improvements
    * Instancing & occlusion optimizations
    * Optimized atmospheric scattering, reducing render time by up to 0.5ms (PST-1890)
* Stability Improvements
    * Fixed incorrect handling of resource counts in the rendering abstraction layer
    * Early exit mechanism added to prevent crashes when the GPU device is unavailable
    * Improved handling of minimum VRAM requirements to ensure compatibility with lower-end hardware.

### Invisible Work

* More work has been done to reduce tech debt following the first release and help prepare for future work.

## v0.1.4

### Known Issues

* Multi monitor setups may show the window on the wrong monitor.
* Windowed mode allows setting a too large resolution, which does not fit on screen. Use alt-enter to fix it.
* Sometimes when switching display mode and resolution simultaneously, the resolution will not be applied.

### Features

* You can now set resolution in borderless fullscreen.
* You can now opt in or out of sending analytics data from the settings menu.

### Fixes

* Performance:
  * Improved Atmospheric Scattering frametime by 33% by using float16 for the LUT format.
* Logging:
  * Fix a bug where long messages are truncated.
  * Redesigned and simplified a bunch of internal APIs around logging which should improve quality of logs.
* UI:
  * Scale the "Confirm" button in the postcard interface with the resolution.
* Crashes:
  * Avoid a highly annoying crash where we can set the screenshot readback buffer to not match the swapchain size.
    * This one was tricky to hunt down because many graphics cards don't crash, despite it being clearly wrong.
  * Improved unsupported hardware detection to use hardware features instead of names.
  
### Invisible Work

* A large amount of work has been done to reduce tech debt following the first release and help prepare for future work.

## v0.1.3

### Features

* Provide a more click-able format for deeplinks
  * [See the new deeplink documentation](https://github.com/PLAYERUNKNOWN-Productions/Preface-User-Support/wiki/A-Guide-to-DeepLink-(Fast-Travelling-in-Preface))
* PST-2504 - Improve unsupported hardware and OS detection and user-facing messaging

### Fixes

* Windowing
  * PST-2461 - Prevent mouse being captured in full screen mode with DPI scaling
  * PST-2462 - Handle updating UI hitboxes when switching to Borderless Fullscreen from Exclusive Fullscreen with a non-desktop resolution
  * PST-2440 - Fix Preface logo getting drawn before ui scaling is calculated
* Logging
  * Ensure the last line of logs is always added to output
* Performance
  * Fix memory leak in and optimize `string_builder`
  * PST-2470 - Prevent new waypoints requests during flight and ensure they are streamed in when landing
* Crashes
  * PST-2447 - Fix render model load crash
    * When a model is no longer used, don't destroy its resources if an async job is working on processing textures for it
* Troubleshooting
  * `reset_preface.bat` now also deletes the shader cache
    * This works around an issue where occasionally the cache could be corrupted

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
