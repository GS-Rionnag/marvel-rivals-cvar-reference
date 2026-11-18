# Additional I-P engine and rendering CVars, batch B

This guide covers 28 registry variables for input and replay display, engine and asset management, and rendering diagnostics. The snapshot values are observations from an unspecified capture build. A dash indicates no value or matching evidence in the relevant source.

The build string column reports exact names in the build 1.1.4042190 inventory. The object and ref columns report x64 address scan counts as direct-memory candidates / address-taking instructions. Static hits leave runtime registration, effects, and startup override support unverified.

## Input and replay display

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `JarvisReplay.bShowPlay` | `bool` / `ref` | `false` | Controls whether key input is shown during playback. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `JarvisReplay.bShowRecordAxisKey` | `bool` / `ref` | `false` | Controls whether axis keys are shown while recording. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `JarvisReplay.bShowRecordKey` | `bool` / `ref` | `false` | Controls whether input keys are shown while recording. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `JoyStick.Debug` | `bool` / `var` | `false` | Joystick debugging. The help leaves the output and value mapping unspecified. | x64, ARM64EC | 3 / 1 | — |
| `input.DisableHaptics` | `int32` / `var` | `0` | Positive values disable processing of haptic feedback. | x64, ARM64EC | 3 / 1 | — |
| `input.GlobalAxisConfigMode` | `int32` / `ref` | `0` | Selects where global axis settings apply. The help maps 0 to mouse only (default), 1 to all, and 2 to none. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `input.ResetActiveActionsWhenFlushingInput` | `bool` / `ref` | `true` | Translated help describes temporarily treating active action keys as released during flush-triggered InputReleased dispatch, including saving the trigger event and restoring state after dispatch. The help says the behavior is enabled by default. | x64, ARM64EC | 3 / 1 | 1 / 1 |

## Engine diagnostics and asset management

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `MarvelAssetManager.EnableHeroAssetPackCache` | `bool` / `ref` | `true` | The name suggests a switch for the hero asset pack cache. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `MarvelAssetManager.RecursivelyExpandHardReferences` | `bool` / `ref` | `false` | The name suggests recursively expanding hard asset references. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `MarvelAssetManager.SkipStateAndHitAnimLoad` | `bool` / `ref` | `false` | Controls loading of HeroStateAnimData and HitReactAnimData in the hero asset pack. The help maps 0 to load (default) and 1 to skip. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MarvelBaseCharacter.CameraShake.MaxPerFrame` | `int32` / `ref` | `0` | Caps stacked camera-shake instances per frame. The help describes 0 as unlimited and a positive N as a cap of N. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `Pool.Capacity` | `int32` / `ref` | `63` | The name suggests a pool capacity. The registry supplies no help on the pool or unit. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `Pool.ClearPoolWhenSlowMotionStart` | `bool` / `ref` | `false` | The name suggests clearing a pool when slow motion starts. The registry supplies no help on the pool or value mapping. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Pool.EnablePool` | `bool` / `ref` | `true` | The name suggests a pool switch. The registry supplies no help on which pool. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Python.SetPythonGCQuotaAfterUnrealGC` | `bool` / `ref` | `false` | The name suggests setting a Python garbage-collection quota after Unreal garbage collection. The registry supplies no help on its units or schedule. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `marvelstats.HitchCountingThresholdInSeconds` | `float` / `ref` | `0.1` | The name suggests a hitch-counting threshold in seconds. The registry supplies no help on how it is applied. | x64, ARM64EC | 3 / 1 | 1 / 1 |

## Rendering and debug visualization

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `Mass.CrowdTurnOffVisualization` | `int32` / `ref` | `0` | Turns off crowd visualization. The help leaves the affected render systems unspecified. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `Monster.CombineNiagara.SkipFlushAnimCollection` | `bool` / `var` | `true` | The name suggests skipping an animation-collection flush in combined Niagara work. The registry supplies no help. | x64, ARM64EC | 3 / 1 | — |
| `m2208.EnableUltronFormationGlowParallelAlphaWrites` | `bool` / `var` | `false` | Controls formation-glow Skelot alpha writes for 407549. The help gives 0 as serial (default) and 1 as synchronous ParallelFor. | x64, ARM64EC | 3 / 1 | — |
| `n.EnableDrawVoxelCach` | `bool` / `ref` | `false` | Enables drawing the voxel cache. The exact registry spelling ends in Cach. | x64, ARM64EC | 2 / 1 | 0 / 1 |
| `n.EnableVoxelCache` | `bool` / `ref` | `true` | Enables the voxel cache. The scope and prerequisites are unspecified. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `n.GDrawNewAddedDirtyArea` | `int32` / `ref` | `0` | Draws newly added dirty areas. The help leaves the drawing details unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `n.GDrawNewAddedDirtyAreaDuration` | `float` / `ref` | `3` | Sets how long newly added dirty areas are drawn. The help gives no unit. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `n.GForceDebugAllTiles` | `int32` / `ref` | `0` | The name suggests forcing tile debugging. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `n.GNavmeshDisplayNewTileBound` | `int32` / `ref` | `0` | The name suggests displaying bounds for new navigation mesh tiles. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `portal.phantom.debug` | `bool` / `ref` | `false` | The name suggests portal phantom debugging. The registry supplies no help on the output. | x64, ARM64EC | 3 / 1 | 5 / 1 |
| `portal.phantom.enable_niagara_copy` | `bool` / `ref` | — | The help maps 0 to disabling Niagara phantom cloning and portal material clipping and 1 to enabling them. It says existing phantoms must be recreated after a change. | x64, ARM64EC | 3 / 1 | 13 / 1 |
| `portal.phantom.refresh_on_mesh_attach` | `bool` / `ref` | — | Controls whether newly attached mesh components trigger phantom reconstruction. | x64, ARM64EC | 3 / 1 | 1 / 1 |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Help translations](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
