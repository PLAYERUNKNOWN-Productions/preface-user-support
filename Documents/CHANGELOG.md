# Changelog

## v0.3.0

### Upgrade notes

* If you see odd visual behavior after updating (e.g., eye adaptation overcorrecting in the dark), run `reset_preface.bat`.
    * This is required if you participated in the Discord-only `beta` program.

### Known Issues

* Some leaking DX12 resources
* Ray tracing has some issues - especially with night-time lighting
* Flying close to the ocean can occasionally cull an ocean tile, revealing terrain underneath

### Features

* New Worlds to Explore!
  * [Mars](https://preface.pp.studio/bookmarks?longitude=1.697918&latitude=1.233565&altitude=4904896.146613&rotation=-1.046682,1.229226,-1.350954&name=copy_paste&planet_name=mars)
  * [Anesidora](https://preface.pp.studio/bookmarks?longitude=1.025059&latitude=0.589193&altitude=1307462.748291&rotation=0.494822,1.025310,-0.436434&name=copy_paste&planet_name=anesidora)
  * [Dractun](https://preface.pp.studio/bookmarks?longitude=1.218139&latitude=0.296138&altitude=654587.519777&rotation=-0.023325,1.094185,-1.146599&name=copy_paste&planet_name=Dractun)
  * [Zihan](https://preface.pp.studio/bookmarks?longitude=-0.681305&latitude=0.094576&altitude=325984.006943&rotation=1.184866,1.166104,1.806963&name=copy_paste&planet_name=Zihan)
  * [Blondewalnut](https://preface.pp.studio/bookmarks?longitude=1.612719&latitude=0.435415&altitude=333011.867676&rotation=-0.219122,-0.395727,-1.070052&name=copy_paste&planet_name=blondewalnut)
  * You can also navigate to all planets available [here](https://playerunknown-productions.github.io/preface-globe-navigator/)
  * Note: Run the updated app once to enable the feature and close it every time you want to switch planet
  * Deeplinks: you can jump straight to a planet via the `planet_name` url parameter (works with bookmarks)
* Oceans
  * We’ve added our first iteration of planet-scale water – oceans now appear on planets, bringing us one step closer to a living Earth-like world
  * This works on any size of planet
  * In User Mode, the ocean will prevent the user from flying into it with a minimum altitude
* Upscalers updated:
  * AMD FSR 2.0.0
  * NVIDIA DLSS 310.4.0
* Frame-rate control
  * Simulation frame-rate is no longer locked to 60FPS
  * New maximum frame rate option in Settings - with the possibility to uncap
* Biome audio
  * We now have biome-specific environmental audio
* Planets of very different sizes now behave consistently (terrain, population density, grass, shadows, ocean rendering)
* Visual fidelity
  * Better-looking impostors (Night/dusk lighting on impostors is more correct)
  * LOD cross-fading: smoother transitions between LODs
* Ray tracing: no longer experimental

### Fixes

* Quad-tree splitting heuristics: more consistent LOD, fewer stalls; neighboring tiles won’t block splits
* General stability: fewer resource stalls during tile/asset updates
* Crash reports include more relevant log files
* Asset pipeline fixes & improvements

### Stability & Diagnostics

* GPU crash dumps enabled only on NVIDIA cards (no more bad captures on unsupported GPUs)
* BugSplat reports now auto-attach shader PDB/CSO/NVDBG—helps pinpoint shader-line crashes

### Invisible and Upcoming Work

* Large CMake & folder restructure
    * "More Modern CMake" layout, public/private headers, MSVC/Clang support, C++20 default
    * Third-party libraries integrated via CPM and built locally
    * Project split into clearer layers to enable game team & future modders
    * CI moved to GitLab from Jenkins
* Replace Boost usage in preparation of Boost removal
    * Filesystem / path
    * Program options
    * String view
* Replace SQLite config files with JSON-based text files
* Tag-based procedural population (WIP)
    * Tag assets with meta-data such as elevation, precipitation, etc. and see them spawn in the game!
    * Blender plugin for importing and exporting gltf files with tags
    * Asset pipeline support for cooking and validating assets with tags
    * In-game asset previewer that includes tag data
    * Loading & spawning available tagged assets in the world (WIP)
* Networking (WIP)
    * Tooling to measure latency and packet loss
    * Fix various connection issues
    * Support for Steam callbacks and network events
    * State replication for remote agents
    * RPCs to issue commands to remote agents
    * Entity ownership
    * Demos for the above

## v0.2.2

### Features

* Population (trees/rocks/etc.) rendering has had its limit greatly increased - leading to a great improvement in vista rendering.
  * Note: there should only be a minor decrease in performance. If you notice a big regression, please file a bug.

### Fixes

* Various developer tool fixes for working with FSR/DLSS upscaling enabled.
* Asset factory - moved importing to async jobs to retain GUI responsiveness.
* Fixes with ML generating textures that are "out of range" causing "stripy" terrain.
* Fix for clients generating a "null" ID from an empty string hash for analytics.
* Optimisations for instancing cameras to share defines in a better way.
* Avoid converting to wstring for debug names alongside the D3D12 API border - leading to a slight perf bump.
* Don't allow our time devgui to select a time before Midnight, January 1st, 1970 - the world did not exist before that.
* Imposter rendering now uses the correct shadow filtering - avoiding a harsh contrast with fully instanced assets.

### Invisible and Upcoming Work

* Restructuring the entire project to use "more modern CMake" - WIP.
* Various Ocean Rendering improvements - unreleased.
* Steam-based matchmaking for connecting to peers.

## v0.2.1

### Fixes

* Fix for "Enabling 'Hardware Raytracing' while setting 'Hardware Raytracing Mode' to Off may cause the app to crash after some time"

## v0.2.0

### Known Issues

* The new ML model produces occasional straight-line artifacts at tile edges; a new base map is planned to fix this
* Waypoints have been reset to accommodate for changes to terrain generation
* Terrain horizontal displacement is disabled until camera system support is added, to avoid the camera going under the terrain
* Enabling 'Hardware Raytracing' while setting 'Hardware Raytracing Mode' to Off may cause the app to crash after some time

### Features

#### World

* New ML terrain model with improved mountains & elevation
* Work has been done to improve the appearance of all in-game population assets (LOD's, normals, impostors) (PST-2998)

#### Rendering

* Ray-tracing (experimental) can now be enabled via the settings menu (PST-1748)
* Added tone mapping & colour-grading to make the world look more vibrant (PST-3171)
* Added FSR & DLSS support (PST-3130)
* Added FSR & DLSS based anti-aliasing support (PST-3320)
* Added two-pass HiZ occlusion culling to increase rendering performance
* Updated SMAA to the latest version
* Lazily loaded the cloud textures to improve performance
* Impostors support cascaded shadow maps (PST-2084)

#### Gameplay

* Iterated on waypoints
    * Interact with a waypoint to get a periscope view and 'race' to visible waypoints in the distance (PST-3076/3077/3334/3335)
    * Users can now create up to 10 waypoints, up from 4
    * Created waypoints spawn in front of you (PST-3333)
    * Owned waypoints are now white, non-owned are black
    * Waypoints are now updated every 10 seconds, allowing you to see waypoints placed in near real-time (PST-2478)

#### Application

* Added a splash screen which covers up the planet until it's ready to be shown (PST-3344)
* Showing input hints for undocumented controls (Q & E - up and down) and fix conflicting inputs
* Added a setting to invert vertical mouse movement (PST-2486, https://github.com/PLAYERUNKNOWN-Productions/Preface-User-Support/issues/3)

### Fixes

* Resolved multiple existing ECS issues, uncovered by moving to a type-safe API (PST-3070/3072)
* Fixed incorrect waypoint colours and waypoint sound-streaming crash (PST-3078/3257)
* The latest notifications are now always downloaded from the server on start-up, even after reinstalling
* Fixed a crash when taking a screenshot after changing resolution
* Fixed some of the lighting on the dark side of the planet and on the GPU grass
* The title bar now stays on screen when switching to windowed mode (https://github.com/PLAYERUNKNOWN-Productions/Preface-User-Support/issues/9)
* Fixed various GPU crashes and rendering issues
* Analytics are now sent to a more appropriate back-end environment
* Stopped tracking VRAM usage each frame, increasing performance
* Time of day should match for anyone at the same location (PST-3188)
* Cleaned up and improved speed of shader cache generation
* Fixed various errors that appeared when exiting the application
* Fixed various UI scaling issues (PST-3354/3356)
* Waypoints no longer flicker briefly when refreshed (PST-3337)
* Postcards and waypoints windows can be closed by the same button that opened them (PST-2271)
* Include meta-data for postcard PNG's (PST-3395)
* Disabled horizontal displacement, to be reimplemented with CPU support (PST-3345)
* Hide terrain unloading during shutdown (PST-3209)
* Make UI elements more consistent and conforming to design style by unifying and reusing more code (PST-3279/2532)
* Stop loading screen audio when starting the game via deep link (PST-3264)
* Waypoints stream in and out at a consistent distance (PST-3339)
* Motion blur setting re-added to user menu (PST-2310)

### Invisible / Upcoming Work

#### Engine

* Rewrote ECS back-end
    * Refactored existing implementation to comply to common constraints, making it possible to switch between ECS back-ends
    * Integrated and evaluated several existing ECS back-ends (EnTT, Flecs)
    * Replaced sparse array-based storage with a sparse-set based storage to reduce memory waste and cache misses
    * Moved from a macro heavy API to a templated type-safe API to prevent accidental misuse and fixed various issues that it surfaced
    * Deferred commands that write to the ECS for safer multi-threading (PST-3363)
    * Separated API into public and private parts (implementation details)
* Worked on networking / replication fundamentals
    * Serialization
    * RPC's
    * Registry
    * Testing facilities (PST-3149)
    * Replication demo
* Iterated on asset import tools to convert assets and import them directly into a running game (PST-3440)
* Worked on tooling & workflows to more easily author data collection, processing and retrieval in-game to allow for further interactivity in the future
* Added in-game voting system to solicit user feedback
* Integrated various monitoring and profiling tools (PresentMon, GameProfiler)
* Set up the project for more robust testing (starting with Replication)
* Integrated robot-framework for more elaborate automated testing
* Tracked more relevant information when a crash occurs (unsupported hardware, assert callstacks)
* Added meta-data to the executable file
* Moved to C++17 and started using supported features
    * Nested namespaces
    * Replace boost filesystem with std::filesystem
* Adopted LLVM code guidelines
* Worked on headless mode for the app & tooling (PST-2711)
* Worked on project / solution generation to improve easy of use and maintainability (PST-2927, PST-3318)
* Add automated tests for the Data & Privacy Settings popup (PST-2923)
* Iterated on internal logging tools (PST-2849)

#### Rendering

* Implemented new GPU-profiling subsystem (PST-3190/3191/PST-2100)
    * Timestamp / statistics queries
    * Thread-safe context
    * FPS histogram & debug UI
* Integrated IMGUI multi-viewport features to support more advanced engine tooling
* Prototyped oceans

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
