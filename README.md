# crazyhorse-gaming-engine
High-precision native C++20 core framework with unified asset pipelines, multi-genre kernel support, and a decoupled DOM/SVG web runtime utilizing WebGL 2 and Three.js.

CRAZY HORSE GAMING ENGINE
Xaida Insignia Productions
SemVer 0.1.0  --  7 September 2026
PROJECT MAP  (every component)
"This is not a toy."  
Credit
  Daniel Scribe
  X:           https://x.com/danRydr
  GitHub:      https://github.com/dmscribe
  Site:        https://xaelserpent.com
  Studio:      Xaida Insignia Productions
===========================================
0.  PURPOSE
===========================================
Crazy Horse is a small, named C++20 game engine.  It exists so one
core developer can clone the tree, open it in an IDE, and author
playable worlds without forking the engine per genre or per GPU API.
It is built to run, over time:
  - 3D RPGs and action-RPGs
  - 2D and 3D platformers
  - First-person shooters
  - Third-person shooters
  - Later MMORPG worlds (data model reserved; no netcode in 0.1.0)
One ECS, one scene IR, one RHI, one asset pipeline. Genre lives in
gameplay/kernel_* (platformer, shooter, RPG; MMO reserved). A later
WebGPU or "Web 3GL" path is one more RHI backend -- not a new engine
and not a new Greasy Grass.
The default download proves those kernels compose on one battlefield
cell: Greasy Grass / Little Bighorn, 25-26 June 1876. Adults-only
tactical documentary. Outcome locked. Local agency only. That slice
is a capability demo, not the product ceiling.
Crazy Horse is never editor chrome. On the field he appears only as
Shadow (unlit black + cyan rim). The locked mark at
engine/assets/brand/logo.png is used on splash, titlebar, and About.
Do not invent mark art.
C++ is source of truth. Three.js r0.185.1 is a browser preview RHI
adapter for the slice, not the engine. Launch and Editor are DOM and
must boot with no GPU.
============================================
1.  ONE-LINE ANSWER
============================================
Is this a Three.js project?
  PARTLY -- only the browser preview of the Greasy Grass slice.
  The product is Crazy Horse: a C++20 engine (one ECS, one scene IR,
  one RHI, one asset pipeline, genre kernels). Native RHI is sokol
  (GL / D3D11 / wasm WGPU) with a Vulkan hello-triangle stub.
  The live web preview draws the same kernels through Three.js
  r0.185.1 (imperative WebGL 2, not React-Three-Fiber for the field).
  Launch and Editor are DOM. They do not load Three.js.
  Three.js is a preview RHI. It is not the engine.
============================================
2.  TWO TREES  (same kernels, two hosts)
============================================
  crazy-horse/     C++20  CMake 3.28+  native + wasm + tests
  src/             TypeScript peer for the browser workbench
                   (TanStack Start + React 19 overlays)
  Genre differences live in gameplay/kernel_* -- not forked engines.
============================================
3.  C++ ENGINE  (crazy-horse/)
============================================
ROOT
  CMakeLists.txt          Build graph. C++20. FetchContent sokol.
  CMakePresets.json       Presets: native, wasm, tests, native-vk.
  VERSION                 SemVer 0.1.0
  LICENSE                 MIT, Copyright 2026 Xaida Insignia Productions
  README.md               Worker start (cmake --preset native ...)
DOCS
  docs/architecture.md    Loop, RHI, Shadow, AdultsOnly, leftover tasks
  docs/book-map.md        Lengyel / Rendering Cookbook / Chiu / Bourg
  docs/genre-kernels.md   How A+B+C compose; MMO reserved
  docs/project-map.md     Two sentences per path
  docs/slice-greasy-grass.md   Beat sheet, sockets, historical lock
ENGINE MATH  (Lengyel FGED Vol.1 ch.1-3)
  engine/math/math.h      Umbrella
  engine/math/math.cpp
  engine/math/vec2.h
  engine/math/vec3.h
  engine/math/vec4.h
  engine/math/mat3.h
  engine/math/mat4.h
  engine/math/quat.h
  engine/math/ray.h
  engine/math/plane.h
  engine/math/aabb.h
  engine/math/frustum.h
ENGINE CORE  (Lengyel FGED Vol.2)
  engine/core/core.h      Identity
  engine/core/core.cpp
  engine/core/log.h       Log
  engine/core/log.cpp
  engine/core/tick.h      Fixed 30 Hz + interpolate
  engine/core/tick.cpp
  engine/core/version.h   From VERSION
  engine/core/version.h.in
ENGINE OS
  engine/os/os.h          Clock, sleep, display probe
  engine/os/os.cpp
ENGINE RHI  (Rendering Cookbook -- pass / buffer / pipeline)
  engine/rhi/rhi.h
  engine/rhi/caps.h             RasterWebGL2, RasterWebGPU, Compute, Bindless
  engine/rhi/rhi_sokol.cpp      Fast path
  engine/rhi/vulkan_stub.cpp    native-vk hello-triangle stub only
  engine/rhi/README.md          Fork table. WebGPU is not a new engine.
ENGINE RENDER
  engine/render/draw_list.h     Mesh handle + material id + TEMP + Shadow
  engine/render/render.h        Frame encodes to DrawList
  engine/render/render.cpp
  engine/render/shadow.h        Shadow permutation: unlit black + cyan rim
ENGINE ECS
  engine/ecs/ecs.h              Entity ids, sparse sets
  engine/ecs/ecs.cpp
  engine/ecs/components.h       Transform, Velocity, Health, Stamina,
                                Faction, AdultTag, Mount, Weapon,
                                SenseCone, CoverVolume
ENGINE SCENE IR
  engine/scene/scene.h          Hierarchy
  engine/scene/scene.cpp
  engine/scene/sockets.h        Ten Greasy Grass sockets (snake_case ids)
  engine/scene/cell.h           420 m cell, 128x128 heightfield
ENGINE CONTRACTS
  engine/contracts/shared.h     Umbrella: tick, AdultsOnly, sockets, draw list, caps
ENGINE ASSETS
  engine/assets/assets.h        PNG / glTF ingest stubs
  engine/assets/assets.cpp
  engine/assets/character_policy.h   AdultsOnly (age, tags, proportions)
ENGINE AUDIO
  engine/audio/audio.h          Event table + buses
  engine/audio/audio.cpp
  engine/assets/audio/events.json
  engine/assets/audio/*.wav     amb, carbine, pistol, bow, hit, hoof,
                                foley, vo_hau, vo_hello
ENGINE PHYSICS
  engine/physics/physics.h      Swept AABB/OBB, heightfield sample
  engine/physics/physics.cpp
ENGINE BRAND
  engine/brand/brand.h          Wordmark, studio, logo path
  engine/brand/brand.cpp        Never invent mark art
  engine/assets/brand/logo.png  Locked mark. Splash / titlebar / About only.
ENGINE TEXTURES
  engine/assets/textures/grass.jpg
  engine/assets/textures/gravel.jpg
  engine/assets/textures/sage.jpg
  engine/assets/textures/water.jpg
  engine/assets/textures/dust.png
GAMEPLAY KERNELS
  gameplay/kernel_platformer/   A  coyote, jump buffer, slopes, mount
  gameplay/kernel_shooter/      B  hitscan, bow projectile, cover, cameras
  gameplay/kernel_rpg/          C  attributes, stamina, groups, greet
  gameplay/kernel_mmo/          RESERVED  AoI / shard / dedicated server
                                (comments only -- no netcode)
  gameplay/shared/              pawn, camera, interact, AdultsOnly hook
    pawn.h  camera.h  interact.h  ai.h  shared.cpp
SAMPLES
  samples/00_triangle/          Sokol hello triangle or software "ok"
  samples/slice_greasy_grass/   Showcase: director, pawns, mount, hitscan
    beat_director.h
    slice.h
    main.cpp
  samples/slice_2d_platformer/  kernel A + empty scene
  samples/slice_2d_shooter/     kernel B + empty scene
  samples/slice_3d_platformer/  kernel A in 3D + empty scene
  samples/slice_fps/            kernels B + A + empty scene
  samples/slice_rpg_village/    kernel C + empty scene
EDITOR (C++)
  editor/app/main.cpp           Overlay notes
  editor/app/overlay.h          pause, beat skip, camera debug, About
  editor/about/about.cpp        Product + studio + version
  editor/preview_web/           wasm HTML shell stub
RUNTIME
  runtime/client_native/main.cpp
  runtime/client_web/README.md
TESTS
  tests/math_test.cpp
  tests/adults_only_test.cpp
  tests/beat_director_test.cpp
  tests/hitscan_cover_test.cpp
  tests/contracts_test.cpp
  tests/CMakeLists.txt
===========================================
4.  TYPESCRIPT PEER  (src/)  -- browser workbench
===========================================
ROUTES  (TanStack Start, file-based)
  routes/__root.tsx             Shell, fonts, theme
  routes/index.tsx              Launch (DOM, no GPU)
  routes/editor.tsx             Editor GUI (DOM + SVG map, no GPU)
  routes/slice.tsx              Lazy-loads Three.js slice
LAUNCH
  components/launch-screen.tsx  Logo, Editor card, Greasy Grass card
EDITOR GUI  (no Three.js)
  editor/store.ts               Selection, tabs, console, AdultsOnly probe
  components/editor/EditorApp.tsx
      Topbar, outliner, inspector, bottom dock, About
  components/editor/ViewportMap.tsx
      SVG tactical map of sockets + river, pan/zoom
SLICE OVERLAY  (DOM over canvas)
  components/slice-overlay.tsx  Role select, HUD, pause, end card, GlFail
  samples/slice-greasy-grass/hud-store.ts   Zustand HUD
SLICE RUNTIME  (Three.js r0.185.1, imperative)
  samples/slice-greasy-grass/SliceApp.tsx   Host + GL retry
  samples/slice-greasy-grass/runtime.ts     Sim loop, AI, weapons, camera
  samples/slice-greasy-grass/world-build.ts Terrain, river, grass, sage, dust
  samples/slice-greasy-grass/meshes.ts      TEMP pawn / horse / Shadow
ENGINE PEER  (mirrors C++ namespaces)
  engine/version.ts
  engine/math.ts                vec, ray-AABB, ray-sphere, damp
  engine/tick.ts                Fixed 30 Hz
  engine/contracts.ts           Shared numbers (C++ is source of truth)
  engine/rhi.ts                 Cap bits + feature detect. No THREE.
  engine/assets.ts              AdultsOnlyPolicy
  engine/audio.ts               Web Audio event table
  engine/input.ts               WASD, pointer lock, fire, mount, irons
PREVIEW ADAPTER  (not the engine)
  preview/README.md             Fork rules. Wasm of kernels preferred over JS sim.
  preview/webgl2-adapter.ts     0.1.0 default field. Imperative Three.js WebGL 2.
  preview/webgpu-adapter.ts     Empty hook. Do not default the field here.
GAMEPLAY PEER
  gameplay/battlefield.ts       Heightfield + 10 sockets + cover volumes
  gameplay/beat-director.ts     5 beats, 600s, outcome locked
  gameplay/kernels/platformer.ts
  gameplay/kernels/shooter.ts
  gameplay/kernels/rpg.ts
  gameplay/kernels/mmo.ts       Reserved
  gameplay/shared.ts
HOST SCAFFOLD  (App Builder, not engine)
  lib/auth/*                    Session gates (unused by the slice)
  lib/app-data/*
  lib/db.ts  lib/env.server.ts
  lib/error-component.tsx
  lib/multiplayer/*             Unused. MMO not shipped.
  components/preview-host-bridge.tsx
  styles.css                    Tokens: ink, gunmetal, steel, cyan
  router.tsx  routeTree.gen.ts
PUBLIC ASSETS
  public/brand/logo.png         Locked mark
  public/logo.png
  public/textures/*             grass, gravel, sage, water, dust
  public/audio/*                Same event table as C++
  public/favicon.svg  og.jpg  x-banner.jpg
===========================================
5.  NAMED CONTENT  (Greasy Grass cell)
===========================================
SOCKETS (scene IR)
  ridge_approach          Eastern ridge
  medicine_tail_coulee    Medicine Tail Coulee
  deep_coulee             Deep Coulee
  calhoun_hill            Calhoun Hill
  battle_ridge            Battle Ridge
  last_stand_hill         Last Stand Hill
  deep_ravine             Deep Ravine
  river_terrace           River terrace
  distant_bluffs          Eastern bluffs
  river                   Little Bighorn
BEATS  (scripted, 600 seconds)
  0:00-0:45    Ridge approach
  0:45-4:00    Coulee skirmish
  4:00-7:30    Horses and dust
  7:30-9:30    Last Stand Hill (pocket)
  9:30-10:00   Fade to stamp  (25-26 June 1876)
WEAPONS
  Springfield carbine     hitscan
  Colt revolver           hitscan
  Bow                     slow projectile + gravity
AUDIO BUSES
  amb_loop  sfx_weapon  sfx_horse  sfx_foley  vo_interact
  Events: amb_wind, sfx_carbine, sfx_pistol, sfx_bow, sfx_hit,
          sfx_hoof, sfx_foley, vo_hau, vo_hello
  Policy: AdultsOnly. No child voices.
ROLES
  Adult Lakota / allied warrior
  7th Cavalry trooper
  No named Custer player. Crazy Horse is Shadow only, never chrome.
POLICY
  AdultsOnly: reject age < 18, banned tags (child/minor/underage/...),
  child proportions (head/body > 0.28), height < 1.5 m.
===========================================
6.  PUBLIC STATS  (release sheet)
===========================================
IDENTITY
  Product          Crazy Horse Gaming Engine
  Studio           Xaida Insignia Productions
  Author           Daniel Scribe  (x.com/danRydr, github.com/dmscribe)
  Site             xaelserpent.com
  Version          0.1.0
  License          MIT
  Slice            Greasy Grass / Little Bighorn  25-26 June 1876
  Classification   Adults only. Tactical documentary. Outcome locked.
STACK
  Language (engine)     C++20
  Language (preview)    TypeScript (strict) + React 19 overlays
  Build (engine)        CMake 3.28+, Ninja, 4 presets
  Build (preview)       Vite 8 + TanStack Start
  Native / wasm RHI     sokol_gfx / sokol_app
  Browser preview RHI   Three.js 0.185.1  WebGL 2
  Vulkan                hello-triangle stub only
  UI chrome             DOM (Cinzel + IBM Plex, gunmetal / steel / cyan)
  State                 Zustand
  Tick                  Fixed 30 Hz + render interpolate
SIZE  (authored, excluding node_modules)
  C++ headers + sources              ~3,100+ lines  ~70 translation units
  C++ docs                           architecture, book map, genre kernels
  TypeScript engine + slice + editor core gameplay + DOM workbench
  CMake presets                      4  (native, wasm, tests, native-vk)
  Automated tests                    5  (math, AdultsOnly, beats, hitscan, contracts)
FIELD
  World cell                         420 x 420 units
  Heightfield                        128 x 128  (~16.6k verts)
  Named sockets                      10
  Cover volumes                      16  (12 rock + 4 empty tipi frames)
  Scripted beats                     5
  Field clock                        600 s  (~8-10 min play)
  Playable factions                  2
  AI groups                          4  (cavA, cavB, lakA, lakB)
  Typical spawn                      1 player + 8 cavalry + 12 Lakota
                                     + 8 adult horses  = 29 units
  Grass instances (desktop)          1,600
  Sage instances (desktop)           220
  Dust particles (desktop)           420
  Tracer pool                        8
  Bow projectile pool                12
  Cameras                            TPS / irons / rider
  Kernels live                       3  (platformer, shooter, rpg)
  Kernels reserved                   1  (mmo -- no netcode)
BOOKS MAPPED TO CODE  (not to a black-box generator)
  Lengyel, FGED Vol.1            math, rays, AABB, frustum, physics
  Lengyel, FGED Vol.2            tick, OS port, draw list
  Kosarevsky, Rendering Cookbook RHI pass/buffer/pipeline, assets
  Chiu, UE5 RPG                  attributes, groups, greet, ECS-as-data
  Bourg & Seemann, AI for Games  beat FSM, cones, steering, morale
WHAT IS NOT SHIPPED
  MMO netcode / listen-server / shards
  Child content or child-proportion meshes
  Named Custer as a playable
  Crazy Horse as a textured hero or editor chrome
  Hand-written Vulkan swapchain
  Full glTF/PNG decode (stubs)
  Dear ImGui docking (C++ overlay notes; web editor is the GUI)
===========================================
7.  HOW THIS WAS BUILT WITHOUT ASTRA 6
===========================================
GPT-6 Astra (OpenAI, September 2026) is the current public story for
one-shot 3D: Unreal Manhattan flythroughs, a Hangzhou city in Three.js
in 24 minutes, Unity prototypes from a grey box. This tree was not
authored that way.
  1. Engine first, renderer second.
     Kernels, scene IR, AdultsOnly, and the beat director exist in C++
     with tests that compile without a GPU. If the slice were only a
     pretty Three.js scene, the C++ tree would be empty. It is not.
  2. Textbooks, not a vibe dump.
     Every subsystem header cites Lengyel, the Rendering Cookbook,
     Chiu, or Bourg & Seemann. The map from book to file is
     crazy-horse/docs/book-map.md. Astra 6 does not replace that map.
  3. Dual host, one data model.
     Native sokol and browser Three.js both consume the same sockets,
     beats, weapons, and policy. Preview RHI can be swapped; the IR
     cannot. That is the opposite of a single-canvas prototype.
  4. Constraints over spectacle.
     Historical outcome locked. Local agency only. AdultsOnly at
     import. Shadow is a shader permutation, not a celebrity mesh.
     kernel_mmo is two sentences on purpose. These are production
     rules, not "make it look like a AAA trailer."
  5. Editor without a GPU.
     Launch and the workbench are DOM + SVG. They boot when WebGL
     does not. Astra-style city demos die with the context. This
     workbench does not.
  6. No Unreal, no Unity, no Playbot, no Astra IDE.
     No generated Manhattan. No 24-minute city. TEMP capsules and an
     authored heightfield on one battlefield cell, with a 10-minute
     director you can skip, pause, and inspect.
What we are claiming: a small, named engine with tests, kernels, a
policy, a documentary slice, and a workbench a stranger can open.
What we are not claiming: Astra-scale world gen, photogrammetry, or
a week of Unreal street-by-street mesh.
==========================================
8.  WORKER START
==========================================
  cmake --preset native
  cmake --build --preset native
  ctest --preset native
  ./build/native/samples/slice_greasy_grass
  cmake --preset wasm
  cmake --build --preset wasm
  Browser workbench: open Launch -> Editor (no GPU) or Greasy Grass
  (Three.js preview of the same cell).
END OF MAP
