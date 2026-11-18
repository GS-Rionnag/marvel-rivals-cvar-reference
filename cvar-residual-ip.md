# Additional I-P engine and rendering CVars

These 55 registry variables cover image writes, diagnostics, editor and UI settings, mesh materials, movie rendering, level of detail, audio loopback, packaging, and portal rendering. The snapshot column reports captured observations. A dash indicates no recorded value.

The build string column lists exact names in the build 1.1.4042190 inventory. CRC denotes Crash Report Client. The object and ref columns give x64 scan counts as direct-memory candidates / address-taking instructions. A dash indicates zero hits of either class. The scan alone leaves registration, execution, and startup override support unverified.

## Engine, editor, and media

| Exact name | Type / kind | Snapshot | Supplied help or evidence limit | Epic 5.9 match | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `ImageWriteQueue.MaxConcurrency` | `int32` / `var` | `-1` | Maximum concurrent asynchronous image writes. The help gives the number of available cores as the default. | Yes | x64, ARM64EC | 3 / 1 | — |
| `ImageWriteQueue.MaxQueueSize` | `int32` / `var` | `-1` | Maximum queued image write tasks before adding a task blocks. The help gives four times the available core count as the default, or 16 when multithreading is disabled on the command line. | Yes | x64, ARM64EC | 3 / 1 | — |
| `InGamePerformanceTracking.Enabled` | `int32` / `var` | `0` | Controls in-game performance tracking. | — | — | 1 / 0 | — |
| `InGamePerformanceTracking.HistorySize` | `int32` / `var` | `30` | Number of frames stored in the in-game performance tracking history. | — | — | 3 / 0 | — |
| `LWI.Editor.GridSize` | `int32` / `ref` | `-1` | Sets the size of a grid that LWI managers will be generated with. | Yes | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `LoadingPanel.DebugInfoEnable` | `bool` / `var` | `false` | Translated help gives 0 to hide debug information and 1 to show it. | — | x64, ARM64EC | 3 / 1 | — |
| `Mass.CallUpdateInstances` | `int32` / `ref` | `1` | Toggle between UpdateInstances and BatchUpdateTransform. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `MeshComponent.EnableAsyncSet` | `bool` / `ref` | `true` | Set 0 to disable asynchronous material assignment on mesh components. | — | x64, ARM64EC | 2 / 1 | 12 / 1 |
| `MeshComponent.EnableMaterialParameterCaching` | `bool` / `var` | `false` | Enables material parameter caching for UMeshComponent. This can improve performance when setting material parameters on multiple materials at once. | — | x64, ARM64EC | 3 / 1 | — |
| `MeshComponent.OptimizeMIDCreation` | `bool` / `var` | `true` | No supplied help. The name suggests an optimization for material instance creation. The affected path and value semantics are unspecified. | — | x64, ARM64EC | 3 / 1 | — |
| `MovieRenderPipeline.FrameStepDebug` | `int32` / `var` | `-1` | How many frames should the Movie Render Pipeline produce before pausing. Set to zero on launch to stall at the first frame. Debug tool. -1: Don't pause after each frame (default) 0: Process engine ticks but don't progress in the movie rendering pipeline. 1+: Run this many loops of the movie rendering pipeline before pausing again. | — | x64, ARM64EC | 3 / 1 | — |
| `MovieRenderPipeline.MotionBlurAmount` | `float` / `var` | `-1` | Override the MotionBlurAmount obtained by PostProcessSettings while rendering in MRQ -1.0: Don't override (default) 0.1: Really small motion blur (recommanded, because MotionBlurAmount=0 will cause many troubles.) | — | x64, ARM64EC | 3 / 1 | — |
| `MovieRenderPipeline.WaveOutput.WriteDelay` | `float` / `var` | `0.5` | How long (in seconds) should the .wav writer stall the main thread to wait for the async write to finish before moving on? If your .wav files take a long time to write and they're not finished by the time the encoder runs, the encoder may fail. | — | x64, ARM64EC | 3 / 2 | — |
| `MovieScene.EnableCachingSchedulerTasks` | `bool` / `ref` | `false` | Whether to enable caching SchedulerTasks. | — | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `MovieScene.ForceMovieScenePreviewAnimationCustomMode` | `bool` / `ref` | `true` | When true, forces custom-mode evaluation for Movie Scene preview animations. The help lists true as the default. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MovieScene.LegacyConversionFrameRate` | `FString` / `var` | — | Specifies default tick resolution for UMovieScene data saved before 4.20 (default: 60000fps). Examples: 60000 fps, 120/1 (120 fps), 30000/1001 (29.97), 0.01s (10ms). | Yes | x64, ARM64EC | 2 / 1 | — |
| `MovieScene.RemoveMutedTracksOnCook` | `int32` / `ref` | `0` | If 1 remove muted tracks on cook, otherwise leave as is. | Yes | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `OSS.VoiceLoopback` | `int32` / `var` | `0` | Voice loopback. The help maps 1 to enabled and 0 to disabled. | Yes | x64, ARM64EC | 2 / 1 | — |
| `Package.Relocation` | `int32` / `var` | `0` | Define when we should run the relocation logic for the dependencies of a package. Note changing this value at runtime won't update the cached depencencies in the asset registry. 0: Off (never apply relocation. References to other relocated packages will give errors and fail to resolve.) 1: Relocate any asset saved after EUnrealEngineObjectUE5Version::ADD_SOFTOBJECTPATH_LIST (5.1). Default value for the new projects. | Yes | x64, ARM64EC, CRC | 3 / 1 | — |
| `PackageName.PackageExistResultCacheForStringTable` | `bool` / `ref` | `true` | Cache FPackageName::DoesPackageExist for StringTable. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `lod.EnableDistance` | `bool` / `var` | `true` | This enables lod to switch by view distance. | — | x64, ARM64EC | 3 / 1 | — |
| `lod.EnableScreenSize` | `bool` / `var` | `false` | This enables lod to switch by screen size. | — | x64, ARM64EC | 3 / 1 | — |
| `lod.TemporalLag` | `float` / `var` | `0.5` | This controls the the time lag for temporal LOD, in seconds. | Yes | x64, ARM64EC | 3 / 1 | — |
| `log.Category` | `int32` / `var` | `1` | Defines if the categoy is included in each line in the log file and in what form. 0 = Do not log category 2 = Log the category (default) | Yes | x64, ARM64EC, CRC | 3 / 1 | — |
| `log.Timestamp` | `int32` / `var` | `5` | No supplied help. The name suggests a log timestamp setting. The formatting and value semantics are unspecified. | Yes | x64, ARM64EC, CRC | 3 / 1 | — |
| `log.flushInterval` | `float` / `ref` | `0.2` | Logging interval in seconds | Yes | x64, ARM64EC, CRC | 3 / 1 | 3 / 1 |
| `log.flushInterval.Shipping` | `float` / `ref` | `0` | Logging interval in shipping. If set, this overrides archive.FlushInterval | — | x64, ARM64EC, CRC | 3 / 1 | 2 / 1 |
| `memory.MemoryPressureCriticalThresholdMB` | `float` / `ref` | `0` | When the available physical memory drops below this threshold memory stats will consider this to be at critical pressure. Where a platform can specifically state it's memory pressure this test maybe ignored. 0 (default) critical pressure will not use the threshold. | Yes | x64, ARM64EC, CRC | 2 / 1 | 1 / 1 |
| `memory.WindowsPlatformMemoryGetStatsLimitTotalGB` | `int32` / `ref` | `0` | Set a synthetic platform total memory size (in GB) which will be returned as Total and Available memory from GetStats | Yes | x64, ARM64EC, CRC | 3 / 1 | 1 / 1 |
| `memory.logGenericPlatformMemoryStats` | `int32` / `ref` | `1` | Report Platform Memory Stats) | Yes | x64, ARM64EC, CRC | 2 / 1 | 1 / 1 |
| `niagara.CreateShadersOnLoad` | `int32` / `ref` | `0` | Whether to create Niagara's simulation shaders on load, which can reduce hitching, but use more memory. Otherwise they will be created as needed. | Yes | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `niagara.ShowShaderCompilerWarnings` | `int32` / `ref` | `0` | When set to 1, will display all warnings from Niagara shader compiles. | Yes | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `pak.CompactDeleteRecords` | `int32` / `ref` | — | Store pak delete-record path hashes in a compact runtime table. Startup only; 0 retains the original index. | — | x64, ARM64EC, CRC | 3 / 1 | 1 / 1 |
| `pak.OptionalHLQRedirect` | `int32` / `ref` | `1` | Enable optional HQ/LQ package redirects for iostore. | — | x64, ARM64EC, CRC | 3 / 1 | 1 / 1 |
| `pak.ReaderReleaseDelay` | `float` / `ref` | `5` | If > 0, then synchronous pak readers older than this will be deleted. | Yes | x64, ARM64EC, CRC | 3 / 1 | 2 / 1 |

## Portal rendering

| Exact name | Type / kind | Snapshot | Supplied help or evidence limit | Epic 5.9 match | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `m.Portal.ClipPlaneCulling` | `bool` / `ref` | `true` | Enable portal clip plane culling or not. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.CrossFrameBudget.GlobalDistanceField` | `int32` / `ref` | `0` | Global distance field start render time. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.CrossFrameBudget.Lumen` | `int32` / `ref` | `3` | Lumen start render time. | — | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `m.Portal.CrossFrameBudget.Shadow` | `int32` / `ref` | `6` | Shadow start render time. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.CrossFrameBudget.TranslucentVolume` | `int32` / `ref` | `10` | Translucent volume start render time. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.CrossFrameBudget.ViewDistanceScale` | `float` / `ref` | `1` | Portal view distance scale by frame count, > 1.0f. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.CrossFrameBudget.VolumetricFog` | `int32` / `ref` | `8` | Volumetric fog start render time. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.DisableDistanceFieldShadow` | `int32` / `ref` | `0` | Disable portal distance field shadow or not. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.EnableSkyPassStencil` | `int32` / `ref` | `0` | Whther to enable sky pass stencil test for portals. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.GlobalDistanceFieldUseLumenParam` | `int32` / `ref` | `1` | Use portal view lumen param for global distance field. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.DiffuseIndirect` | `int32` / `ref` | `0` | Enable or disable lumen diffuse indirect in portal, 0 still lumen, 1 ssgi, 2 none. | — | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlow` | `int32` / `ref` | `1` | Controls the slower portal radiance cache update mode. The help leaves the update policy unspecified. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowDistance` | `float` / `ref` | `1000` | Portal whether to update radiance slow distance. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowDistanceFalloff` | `float` / `ref` | `100` | Portal whether to update radiance slow distance falloff. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowEnd` | `int32` / `ref` | `360` | Portal whether to update radiance slow end. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowPeriod` | `int32` / `ref` | `8` | Portal whether to update radiance slow period. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowPeriodMin` | `int32` / `ref` | `2` | Portal whether to update radiance slow period min. | — | x64, ARM64EC | 2 / 1 | 2 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowSize` | `float` / `ref` | `0.25` | Portal whether to update radiance slow size. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowSizeFalloff` | `float` / `ref` | `0.125` | Portal whether to update radiance slow size falloff. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `m.Portal.Lumen.RadianceCache.UpdateSlowStart` | `int32` / `ref` | `60` | Portal whether to update radiance slow start. | — | x64, ARM64EC | 2 / 1 | 1 / 1 |

## Sources

The capture build for the community registry and snapshot is unspecified. The Epic match column reports the existing local exact-name comparison. The ranges, defaults, and examples in the help column are claims from the registry help. For the two missing descriptions, the names supply only a tentative interpretation.

[Raw registry](EVIDENCE.md#community-sources) · [Snapshot](EVIDENCE.md#community-sources) · [Community registry](EVIDENCE.md#community-sources) · [Help translations](EVIDENCE.md#community-sources) · [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Address scan](EVIDENCE.md#build-specific-static-analysis)
