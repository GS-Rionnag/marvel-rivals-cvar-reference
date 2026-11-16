# Marvel Rivals CVar overrides: research notes

Started 2026-11-15. This guide catalogs the 89 setting lines (85 distinct keys) in the original [community Discord thread](https://discord.com/channels/1452445537298022637/1556428197820633269), including 83 ordinary lines and six `!` reset lines. Four ordinary keys appear to be input config properties rather than CVars. The notes separate upstream engine facts and community claims from verified game behavior.

## Evidence and scope

The community thread is a list of proposed settings, not a controlled benchmark of each variable. A name in an Unreal reference or community registry does not prove that the game build registers it or accepts a startup override. See [Evidence and scope](EVIDENCE.md) for how the documentation treats community metadata, snapshots, and build-specific static analysis.

## Epic reference and community benchmark

For standard Unreal variables, this guide uses Epic's public [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference) and [Texture Streaming Configuration](https://dev.epicgames.com/documentation/unreal-engine/texture-streaming-configuration-in-unreal-engine). Marvel Rivals' precise Unreal fork/version can differ. A variable appearing in Epic's reference is evidence of its meaning in that engine version, not proof that Marvel Rivals registers it or honors runtime changes. `Not located` means it was not present in the Epic 5.9 reference during this review; it may still be a Marvel-specific, plugin-specific, older-version, or fork-only variable. Verify registration/effect in the current game before relying on it.

The thread's author says the list was assembled from things other people used and that they had **not individually benchmarked** each entry. Three screenshots attached to the original post show different Practice Range views with FPS counters, but no matched scene/config pair. A later chart in the thread compares “1600x1200 w/ CMDS @ 100% AA” with “1600x1200 Mid No CMDS 100% AA”: it reports 253.3 average / 111.6 1st-percentile / 86.4 0.1-percentile FPS for the first row and 199.6 / 103.7 / 81 for the second. The chart does not identify the exact override set, test hardware, benchmark method, or repetitions; these figures are a community-reported comparison, not causal proof that the posted CVars produced the average-FPS difference.

## How to read an example `[Overrides]` loader format

According to the example loader instructions:

- Lines beginning with `;` are comments and do nothing. The example block must be copied below the actual `[Overrides]` marker and uncommented before it takes effect.
- An ordinary `name=value` line under `[Overrides]` is a CVar override. The loader says these merge above existing configuration and take precedence, including switches.
- In this loader, `!name=` removes the configured value so the game's own value applies. Keep the `=`. This is the loader's behavior; it is not a general Unreal CVar reset syntax.
- The loader's own instructions say settings that can remove smoke or other effects are ignored. This is a loader policy statement; it does not identify every protected setting or promise that all visual changes are detected the same way.
- The `[Section]` format is for non-CVar config properties. In the thread, `bDisableMouseAcceleration`, `bEnableMouseSmoothing`, `bViewAccelerationEnabled`, and `RawMouseInputEnabled` look like config properties, not console variables. They should only be used in the setting's real config section if the game defines them there; putting them under `[Overrides]` does not make them CVars.
- The thread's `!r.SkeletalMeshLODBias=15` and `=16` are two alternative reset lines, not a way to set a range. Under the example loader semantics both remove the configured value; neither requests LOD 15 or 16.



The six reset lines and the status of the variable each names are:

| Exact line | What this loader does / CVar status |
| --- | --- |
| `!r.Streaming.UsePerMeshBias=0` | Removes the configured value for this key; `0` is not applied. Not located in Epic 5.9, and the name must be treated as possibly game/fork-specific or misspelled. |
| `!r.SkeletalMeshLODBias=15` | Removes the configured value. Epic documents the underlying LOD-bias CVar, but this line does not set bias 15. |
| `!r.SkeletalMeshLODBias=16` | Same reset operation for the same key; the `15` and `16` versions are redundant alternatives. |
| `!r.SkeletalMeshLODRadiusScale=0.25` | Removes the configured value. The number does not apply; Epic documents the underlying screen-radius scale separately. |
| `!r.FreeSkeletalMeshBuffers=1` | Removes the configured value; `1` is not applied. Epic documents this CVar as controlling whether skeletal-mesh buffers stay in CPU memory to support skeletal-mesh merging (`0` keeps them, `1` frees them). |
| `!r.Streaming.PoolSizeForMeshes=0` | Removes the configured value; zero is not applied. Epic documents the underlying mesh-pool CVar separately. |

## Does a CVar actually change in Marvel Rivals?

“Editable” has several separate meanings. The supplied loader instructions say that a syntactically valid line below `[Overrides]` is merged over the config and wins over its existing values. That establishes what the loader intends to do with the line; by itself it does **not** establish that the game accepts the setting or that gameplay/rendering changes.

For this research, use these evidence levels and do not collapse them into a single yes/no label:

| Evidence level | What it establishes | What it does not establish |
| --- | --- | --- |
| Loader syntax | The line is uncommented, in the right section, and uses the loader's documented `name=value` form (or its documented `!name=` reset form). | That the key is a CVar, recognized by this build, or read by active code. |
| Name/registration evidence | The name occurs in a community registry attachment, a local binary string, or stronger registration-like binary evidence. | That the current game build exposes it to config loading, permits this source's priority, or applies its value. The registry attachment's exact game build is unknown. |
| Config application evidence | A startup log, in-game query, or comparable runtime check shows the requested value was applied and not rejected/overridden. | That any live feature reads the value or changes because of it. |
| Local code-use evidence | The Shipping build contains a direct value read or a registration/callback path tied to the setting. | That the path executes in a normal match, that the requested config value reaches it, or that the visible effect is beneficial. Address-taking alone is not a value read. |
| Controlled behavior evidence | A repeatable in-game A/B change, with other settings and the scene controlled, demonstrates an observable effect. | Effects in modes, maps, patches, or hardware not covered by the test. |

Unreal's public documentation says CVars may be set from config files and that different sources have priorities; a higher-priority value can prevent a lower-priority source from setting the CVar. It also documents special config sections for some engine CVar namespaces. Those are Unreal-engine rules, not proof that Marvel Rivals uses the same fork behavior, loads the mod loader at the same priority, or accepts a particular custom CVar. See Epic's [configuration-file guidance](https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#SetConsoleVariablesinConfigurationFiles) and [C++ CVar priority guidance](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine#priority).

Some CVar families documented below were analyzed only from registry metadata and static executable references. For those, say “loader-configurable by syntax; game acceptance/effect unverified” unless there is specific runtime evidence. The loader also explicitly says it ignores settings that can remove smoke or other effects; this can veto an otherwise valid line, and the rule should be checked before testing any effect-removal proposal. A variable can therefore be syntactically editable without being accepted, behaviorally active, or allowed by the loader.

## Can a packaged asset mod list the live CVar registry?

An Unreal asset package or INI override can carry predetermined values when a compatible loader reads them. That alone does not expose the live `IConsoleManager` registry or write its state to a file. A true runtime enumerator requires a supported game command or code that queries the live registry. Epic documents `DumpCVars` and `DumpConsoleCommands`, but their availability in Marvel Rivals Shipping is unverified. Static name presence does not prove a command is available. See [Evidence and scope](EVIDENCE.md#method-and-reproducibility) for what the build-specific analysis included.


## Current Marvel Rivals policy on injected mods and config changes

Marvel Rivals' official [Use of Mods and Violation Management notice (2026-10-15)](https://www.marvelrivals.com/20261015/41525_1316797.html) says that certain mods using memory-injection and modification behaviors trigger anti-cheat detection and that prohibited mods can receive disciplinary action. Its official [Prohibited Software & Hardware List](https://www.marvelrivals.com/guide/20250226/41348_1214569.html) also lists unauthorized client-config changes, graphics-rendering `.ini` modifications, third-party plugins, and unfair mod resources as prohibited while the game runs. These notices do not establish whether community's reported startup-time method is the same as the memory-injection methods called out in the newer notice, but they do mean we cannot verify that an injected or config-loading CVar dumper is safe or authorized for online use. This project will use the supplied dumps and static/offline analysis rather than build or run a dumper in the live client.

## Thread entries

“Epic 5.9” means Epic's reference describes the CVar. “Not located” means current status is unconfirmed for Marvel Rivals. Values in the first column are exactly what the author posted; they are not recommended defaults.

For the static scan, an embedded name is only a literal-presence fact. In particular, `r.TextureStreaming.DiscardUnusedMips`, `r.VirtualTextureReducedMemory`, `TaskGraph.MaxWorkerThreads`, `TaskGraph.MaxTaskThreadsPerGroup`, `r.DirectX.UsePerQueueFence`, `r.ParallelInitDynamicRHI`, `r.RHICmdUseThread`, `r.TaskGraph.TasksPerThread`, `a.ParallelSkeletalMeshUpdate`, `au.DisableParallelAudioProcessing`, `gc.AssetClusteringEnabled`, `gc.CreateGarbageCollectorUObjectClusters`, `gc.MinDesiredObjectsPerSubTask`, `p.AsyncSceneEnabled`, and `s.LevelStreamingActorsPerPage` were not found as exact strings in this executable. The three absent input keys are `bDisableMouseAcceleration`, `bViewAccelerationEnabled`, and `RawMouseInputEnabled`.

### Texture and mesh streaming

| Posted override | Meaning / evidence |
| --- | --- |
| `r.Streaming.MipBias=0` | Global streaming mip bias. Zero requests no extra mip reduction; positive values drop detail levels to reduce memory demand. Epic documents this. |
| `r.Streaming.MaxNumTexturesToStreamPerFrame=32` | Limits texture uploads from CPU memory to GPU memory per frame; non-positive means unlimited in Epic's reference. Epic notes it only has an effect with `r.Streaming.AmortizeCPUToGPUCopy` enabled. |
| `r.Streaming.DelayProcessPendingMipCopyRequests=1` | Not located in Epic 5.9. Name suggests scheduling pending mip-copy work, but exact semantics and validity in Marvel Rivals are unknown. |
| `r.Streaming.FramesForFullUpdate=30` | Frames between full texture-streamer updates. Higher values reduce update work but make the streamer react more slowly to viewpoint/visibility changes. |
| `r.TextureStreaming.DiscardUnusedMips=1` | Not located as written. Epic documents `r.TextureStreaming` and the separate `r.Streaming.*` family, but not this exact name. Do not assume it is accepted or that it means “free unused mips.” |
| `r.VirtualTextureReducedMemory=0` | Epic documents this as reducing virtual-texture cost through a more packed layout when enabled. The posted zero leaves that optimization disabled in the documented engine. |
| `r.MeshStreaming=1` | Epic labels mesh streaming experimental and says nonzero enables it. This may depend on game asset support and build-time setup; enabling it does not create missing mesh LOD data. |
| `r.Streaming.PoolSize=12288` | Texture streamer pool target in MB in the Epic reference. The pool can include UI, non-streaming textures, cubemaps, and platform-dependent resources. A larger number reserves/allows more budget; it is not a guarantee that 12 GB is available or safe. |
| `r.Streaming.PoolSizeForMeshes=512` | Epic: negative shares texture/mesh pools; nonnegative sets a dedicated mesh pool size. The thread's 512 is a 512 MB mesh-pool target in the referenced implementation. |
| `r.Streaming.PoolSizeForGCs=256` | Not located in Epic 5.9. Exact owner, units, and whether “GCs” means geometry collections or garbage collection are unconfirmed. Do not infer its behavior from the name. |
| `r.Streaming.LimitPoolSizeToVRAM=1` | Epic: limits texture pool size to available GPU memory when enabled. It is not a VRAM allocator and cannot make an oversized pool safe; combined pool accounting may differ by platform/game fork. |
| `r.Streaming.AmortizeCPUToGPUCopy=1` | Epic: when enabled, `MaxNumTexturesToStreamPerFrame` limits the number of 2D textures copied from CPU to GPU per frame. It spreads streaming work out; the direct benefit is smoother upload workload, not necessarily a higher average frame rate. |
| `r.Streaming.NumStaticComponentsProcessedPerFrame=50` | Epic: number of static components incrementally processed per frame before a level is visible (in the streaming setup described by the reference). It is not a general per-frame texture count. |
| `r.Streaming.MaxEffectiveScreenSize=0` | Zero means use actual vertical screen size in Epic's reference; a positive value clamps the screen-size input used to calculate wanted texture mips. |

### GPU, render thread, and latency

| Posted override | Meaning / evidence |
| --- | --- |
| `r.ParallelInitDynamicRHI=1` | Not located in Epic 5.9. The name implies parallel initialization of the Render Hardware Interface, but whether this CVar exists or has any effect in the Marvel build is unknown. |
| `r.RHICmdUseThread=1` | Not located in Epic 5.9. Likely related to dispatching RHI commands from a dedicated thread based on the name; do not treat that guess as a verified description. |
| `r.DirectX.UsePerQueueFence=1` | Not located in Epic 5.9. Likely a DirectX queue/fence synchronization switch; exact behavior, supported queues, and safety are unverified. |
| `r.D3D12.GPUTimeout=0` | Epic's reference says zero disables GPU timeout and explicitly warns that a GPU stall can freeze the PC. This is a watchdog/debugging behavior change, not a latency optimization. Avoid recommending it as a routine setting. |
| `r.OneFrameThreadLag=1` | Epic CVar reference describes the engine's one-frame render-thread lag behavior. This setting can affect CPU/GPU pipelining and latency; its name alone does not tell whether enabling or disabling is preferable for a given bottleneck. |
| `RHI.MaximumFrameLatency=1` | RHI frame-latency limit. Lower queued frames can reduce input-to-display delay but may reduce throughput or cause uneven frame pacing. Exact behavior depends on the RHI/driver and game integration; verify in-game. |
| `r.GTSyncType=2` | Not located in Epic 5.9 reference. The poster says “try 1 or 2”; exact modes and behavior in this game are unverified. The number cannot be assumed to mean a universal sync policy. |
| `r.MeshCardRepresentation.Async=1` | Epic reference lists the CVar, but its description is just “.”; the adjacent `r.MeshCardRepresentation` family concerns mesh cards (used by rendering features such as Lumen in UE). The exact async operation/effect in Marvel Rivals is not documented by Epic's entry. |
| `r.SkinCache.CompileShaders=1` | Epic: controls whether to compile GPU compute skin-cache shaders. The documented default is 0. Epic notes changing it requires touching a shader source file to cause a recompile, so forcing `1` in a shipping config is not evidence that it compiles anything or switches meshes to compute skinning. |
| `r.TeamOutline.LineWidth=2` | Not located in Epic 5.9. Likely game-specific outline width from the name, but this has not been verified in the Marvel build. Do not assume its units or allowed range. |

### Task graph, animation, physics, and audio

| Posted override | Meaning / evidence |
| --- | --- |
| `TaskGraph.MaxWorkerThreads=8` | Not located in Epic 5.9. Name suggests a cap for Task Graph worker threads; exact semantics and whether the game uses this legacy/custom variable are unknown. |
| `TaskGraph.MaxTaskThreadsPerGroup=8` | Not located in Epic 5.9. Exact scheduling behavior is unknown; do not assume it simply adds eight threads. |
| `r.TaskGraph.TasksPerThread=2` | Not located in Epic 5.9. Could be fork-specific scheduler tuning; runtime registration and interpretation unknown. |
| `r.ForceAllCoresForShaderCompiling=1` | Not located in Epic 5.9. Shader compilation is mostly a startup/build-time concern; a shipping client may not expose this or recompile shaders due to this setting. |
| `a.EnableVisibilityBasedTickOptimization=1` | Not located in Epic 5.9. Name suggests suppressing/tuning actor or animation updates when not visible; precise scope and gameplay consequences unknown. |
| `a.ParallelAnimUpdate=1` | Epic: permits animation blend-tree/native update, asset player, and montage update work on worker threads where possible. |
| `a.ParallelAnimEvaluation=1` | Epic: evaluates animation across the Task Graph instead of purely on the game thread. |
| `a.ParallelAnimInterpolation=1` | Epic: runs animation interpolation across the Task Graph instead of purely on the game thread. |
| `a.ParallelSkeletalMeshUpdate=1` | Not located in Epic 5.9. Likely a Marvel/engine-fork switch for parallel skeletal-mesh component updates; exact implementation and safety are unknown. |
| `spine.MaxSkeletonFrameRate=0` | Not located in Epic 5.9. Likely belongs to a Spine runtime/plugin, but the meaning of zero (unlimited, disabled cap, or default) is unknown. |
| `p.AsyncSceneEnabled=1` | Not located in Epic 5.9. Appears to be a physics async-scene switch from its name; modern Chaos physics configuration may not use it. Exact game behavior is unknown. |
| `tick.AllowAsyncProjectileComponent=1` | Not located in Epic 5.9. Likely game-specific asynchronous projectile component ticking. Potentially gameplay-sensitive; no implementation evidence yet. |
| `tick.AllowAsyncNetTicks=1` | Not located in Epic 5.9. Likely asynchronous network-related ticking; exact scope, compatibility, and effect on authoritative gameplay are unknown. |
| `tick.AllowAsyncSummonedComponent=1` | Not located in Epic 5.9. Likely game-specific ticking for summoned components; exact behavior is unknown. |
| `au.DisableParallelAudioProcessing=0` | Not located in Epic 5.9. Name implies `1` disables parallel audio processing, so the posted `0` would leave it enabled if the CVar exists; exact game implementation is unverified. |

### Chaos geometry collections (physics effects)

These names use `GC` in the Chaos/physics section and should not be conflated with `gc.*` Unreal UObject garbage-collection variables below.

| Posted override | Meaning / evidence |
| --- | --- |
| `p.Chaos.GCRemoveInternalfaceFaceRender=0` | Not located in Epic 5.9. The spelling is exactly as posted. It appears to concern internal-face removal/rendering for Chaos Geometry Collections, but exact semantics are unknown. |
| `p.Chaos.GGCRemoveInternalfaceFaceInShadow=0` | Not located in Epic 5.9. Spelling includes `GGC`; do not silently “correct” it. Likely geometry-collection shadow handling, but unverified. |
| `p.chaos.ChoseGCLOD=1` | Not located in Epic 5.9. Likely a game-specific Geometry Collection LOD selector. The misspelling/casing is preserved from the post; effect and valid values unknown. |
| `p.chaos.ChoseGCSecondaryLOD=1` | Not located in Epic 5.9. Likely a secondary Geometry Collection LOD selector; exact behavior and valid values unknown. |
| `p.Chaos.ClientGCMaxRenderNum=64` | Not located in Epic 5.9. Likely a client-side rendering cap/count for Geometry Collections. Whether `64` counts objects, pieces, or something else is unknown. |
| `p.Chaos.PerformGeometryReduction=1` | Not located in Epic 5.9. Name suggests reducing Geometry Collection geometry, but whether this is runtime, cooking, or game-specific is unknown. |

### UObject garbage collection and loading

| Posted override | Meaning / evidence |
| --- | --- |
| `gc.MultithreadedDestructionEnabled=1` | Epic: frees object memory from a worker thread. It is about UObject destruction, not Chaos Geometry Collections. |
| `gc.CreateGCClusters=1` | Epic: attempts object clusters for more efficient garbage collection. |
| `gc.AllowParallelGC=1` | Epic: controls parallel garbage collection. |
| `gc.MinDesiredObjectsPerSubTask=120` | Not located in Epic 5.9. Likely a game-fork threshold for dividing GC work among subtasks; exact units/meaning unknown. |
| `gc.AssetClusteringEnabled=True` | Not located with this exact spelling. Epic's reference instead lists `gc.AssetClustreringEnabled` (misspelled) for asset-file clusters. Do not assume this thread spelling maps to that CVar. |
| `gc.ActorClusteringEnabled=True` | Epic documents `gc.ActorClusteringEnabled` as controlling actor clusters. Its reference default is `0`; setting it to true enables the feature in builds that support it. |
| `gc.CreateGarbageCollectorUObjectClusters=True` | Not located in Epic 5.9. Likely a game-specific cluster switch; do not confuse it with the documented `gc.CreateGCClusters`. |
| `gc.LowMemory.MemoryThresholdMB=2048` | Epic: threshold in MB for low-memory GC mode. Setting 2048 means the threshold is 2 GiB in the documented version, though the game may define what memory measurement triggers it. |
| `gc.LowMemory.TimeBetweenPurgingPendingKillObjects=10.0` | Epic: seconds between purges of pending-kill objects in low-memory mode. Lower values may reclaim sooner but can increase GC work/hitches. |
| `gc.TimeBetweenPurgingPendingKillObjects=60` | Epic: interval in seconds between purging references to pending-kill objects. This is not a fixed 60-second full-GC cadence. |
| `gc.IncrementalBeginDestroyEnabled=1` | Epic: spreads object destruction over frames using a per-frame time limit. This can trade a long destruction spike for work across multiple frames. |
| `s.IoDispatcherDecompressionWorkerCount=6` | Epic: number of IoDispatcher decompression workers. More workers may increase parallel decompression throughput while also consuming CPU and memory bandwidth. |
| `s.IoDispatcherBufferMemoryMB=1024` | Epic: IoDispatcher buffer memory size in MB. The reference default is 8 MB; a 1024 MB override is a large memory budget change, not automatically faster. |
| `s.IoDispatcherCacheSizeMB=2048` | Epic: IoDispatcher cache memory size in MB. The reference default is 0; a nonzero cache can consume substantial memory. Whether it helps Marvel Rivals' asset access is unbenchmarked. |
| `s.MaxPrecacheRequestsInFlight=32` | Epic: maximum number of in-flight precache requests. Higher concurrency can raise CPU/storage pressure and does not guarantee faster loading. |
| `s.MinBulkDataSizeForAsyncLoading=0` | The Epic 5.9 row's description appears inconsistent with its name (“Minimum time the time limit exceeded warning will be triggered by”). Treat intended threshold/units and the effect of zero as unresolved until checked against Marvel's exact source/build. |
| `s.ProcessPrestreamingRequests=1` | Epic: when nonzero, processes prestreaming requests in cooked builds. This controls request processing, not a general “load everything earlier” toggle. |
| `s.IoDispatcherTocsEnablePerfectHashing=1` | Epic: enables perfect hashmap lookups for IoStore TOCs. This is a lookup implementation detail; runtime/build support is required. |
| `s.AsyncLoadingThreadEnabled=1` | Epic labels this a placeholder CVar that is currently not used at runtime. Do not count on the `1` enabling a loading thread. |
| `s.AsyncLoadingTimeLimit=2.0` | Epic documents milliseconds per frame spent on async loading. The reference's default is 5; the community post's 2.0 is a smaller budget and may defer load work rather than speed it up. |
| `s.ForceGCAfterLevelStreamedOut=0` | Epic: whether to force GC after levels stream out, reclaiming memory at the cost of a hitch. Zero avoids forcing that GC through this mechanism. |
| `s.LevelStreamingActorsPerPage=1000` | Not located in Epic 5.9. Likely a game-specific level-streaming actor batch/page setting; meaning, units, and effect unknown. |
| `s.AdaptiveAddToWorld.Enabled=1` | Epic: enables adaptive AddToWorld time slicing, replacing `s.LevelStreamingActorsUpdateTimeLimit` in the documented version. The default is off. |

### Visual detail and model LODs

| Posted override | Meaning / evidence |
| --- | --- |
| `skelot.ForceLOD=0` | Not located in Epic 5.9. Likely belongs to a project/plugin named Skelot. Zero may mean “do not force” but that is only a naming guess; plugin code/game runtime is needed. |
| `r.SkeletalMeshLODRadiusScale=1.0` | Epic: scales the screen radius used to compute skeletal-mesh discrete LOD; documented range is 0.25–1. A lower value can make LOD selection behave as if the mesh were smaller on screen, leading to earlier lower-detail LODs. |
| `r.SkeletalMeshLODBias=0` | Epic's scalability reference says this globally biases skeletal-mesh LOD selection. Zero adds no global bias; positive/negative direction should be checked against the specific engine version and mesh LOD setup before use. |
| `r.EnableMorphTargets=1` | Epic: enables morph targets. This does not make morph data appear on a mesh that was cooked without the needed morph targets. |
| `r.StaticMeshLODBias=0` | Not located in Epic 5.9 reference. It may be fork-specific; Epic documents `r.StaticMeshLODDistanceScale`, which is a different CVar and must not be substituted by name. |
| `r.ViewDistanceScale=1` | Epic CVar reference describes a global multiplier for view distance. Increasing it can retain/draw more objects farther away, with CPU/GPU cost. |
| `r.StaticMeshLODDistanceScale=1` | Epic: scales distance for static-mesh discrete LOD selection. Higher values make LOD transitions earlier (for example, 2 means twice as quickly/half the distance); 1 is the reference default. |
| `r.DetailMode=2` | Epic: detail mode determines which components are updated/ticked; 0 low, 1 medium, 2 high, 3 epic in the reference. It can suppress detail-tagged content; it is not simply texture quality. |

### Image effects

| Posted override | Meaning / evidence |
| --- | --- |
| `r.PostProcessing.DisableMaterials=1` | Not located in Epic 5.9. Likely disables post-process materials in this game/fork; possible visual/gameplay/UI side effects unknown. The thread's “disable Chronovision” label is an author claim, not verified causation. |
| `r.LightTile.Enable=0` | Not located in Epic 5.9. Name suggests a tiled-lighting feature; exact feature and visual/performance consequences unknown. |
| `r.CustomDepth=0` | Epic: controls custom depth rendering (the reference discusses the CVar family). Disabling it can break outlines, occlusion effects, and other materials that depend on the custom-depth buffer. It may affect character visibility cues, so do not present this as a harmless performance switch. |

### Input settings copied from the post (not established as CVars)

| Posted line | Status |
| --- | --- |
| `bDisableMouseAcceleration=1` | Looks like a boolean config property, not a CVar. Its owning config section and whether Marvel Rivals reads it are not established. |
| `bEnableMouseSmoothing=0` | Looks like a boolean config property, not a CVar. Do not assume Unreal's generic input option uses this exact key. |
| `bViewAccelerationEnabled=0` | Looks like a boolean config property, not a CVar. Game-specific registration/section unknown. |
| `RawMouseInputEnabled=1` | Looks like a boolean config property, not a CVar. Game-specific registration/section unknown. |

## Additional related CVars found in Epic's reference

These are useful research leads beyond the original post, not confirmed Marvel Rivals overrides:

| CVar | Documented role |
| --- | --- |
| `r.Streaming.UsePerTextureBias` | Lets the streamer assign individual mip bias values to fit the texture pool; it changes how global mip bias is applied. |
| `r.Streaming.FullyLoadUsedTextures` | Streams used textures to their highest available resolution and keeps them resident. Epic describes it as an alternative to disabling texture streaming entirely; it can use much more memory. |
| `r.Streaming.UseAllMips` | Removes mip-resolution limits in the documented streamer. Epic recommends it for showcases/promotional rendering, not as a general low-risk optimization. |
| `r.Streaming.UseFixedPoolSize` | Prevents the pool size from changing at runtime when nonzero. |
| `r.Streaming.MaxTempMemoryAllowed` | Caps temporary memory used to update streamed texture mips; too low can limit streaming speed. |
| `r.Streaming.UseMaterialData` | Uses material texture scale/coordinate data when calculating texture streaming requirements. |
| `s.LevelStreamingActorsUpdateTimeLimit` | Per-frame time limit for actor registration during level streaming. `s.AdaptiveAddToWorld.Enabled` replaces this mechanism in the documented configuration. |
| `gc.IncrementalGCTimePerFrame` | Time budget per frame for incremental garbage collection. This is distinct from `gc.IncrementalBeginDestroyEnabled`. |
| `TaskGraph.NumForegroundWorkers` | Number of foreground Task Graph worker threads (Epic 5.9 default: 2). Epic says the scheduler must be restarted for a change to take effect. The name is also embedded in this Marvel build. |
| `TaskGraph.ForkedProcessMaxWorkerThreads` | Worker-thread count for forked child processes that allow Task Graph multithreading (Epic default: 2); it does not mean “set the whole game's worker pool to this many.” Embedded in the Marvel build. |
| `TaskGraph.UseBackgroundThreads` | When positive, allows background tasks to use background-priority threads; zero routes them to normal-priority Task Graph threads (Epic default: 1). Embedded in the Marvel build. |
| `TaskGraph.UseHiPriThreads` | When positive, enables high-priority Task Graph worker threads; zero routes background tasks to normal-priority workers (Epic default: 1). Embedded in the Marvel build. |
| `TaskGraph.UseDynamicPrioritization` | Adjusts thread priority per task so high-priority work on background threads is less likely to be preempted (Epic default: true). Embedded in the Marvel build. |
| `tick.AllowAsyncComponentTicks` | General Unreal control for asynchronous component ticks (Epic default: 1). This is a different, broader variable than Marvel's `tick.AllowAsyncProjectileComponent`, `tick.AllowAsyncNetTicks`, and `tick.AllowAsyncSummonedComponent`, whose individual effects remain undocumented. Embedded in the Marvel build. |

Before adding any of these, confirm the current game's registry and compare behavior with the setting absent. A generic Unreal reference is not a Marvel Rivals compatibility list.

## Registry definitions for the posted CVar keys

The following cross-check uses exact CVar names from the posted override list, including keys that appear only in the reset block. Registry help text is copied from the preserved community attachment; it is a direct static definition when present, but still does not prove runtime behavior in build 1.1.4042190. The source does not include 15 of these names.

| CVar | Registry status | Type(s) | Help text |
|---|---|---|---|
| `a.EnableVisibilityBasedTickOptimization` | Registered in attachment | int32 | When enabled, skeletalmeshcomponent will stop tick when bVisible == false or bHiddenInGame == true |
| `a.ParallelAnimEvaluation` | Registered in attachment | int32 | If 1, animation evaluation will be run across the task graph system. If 0, evaluation will run purely on the game thread |
| `a.ParallelAnimInterpolation` | Registered in attachment | int32 | If 1, animation interpolation will be run across the task graph system. If 0, interpolation will run purely on the game thread |
| `a.ParallelAnimUpdate` | Registered in attachment | int32 | If != 0, then we update animation blend tree, native update, asset players and montages (is possible) on worker threads. |
| `a.ParallelSkeletalMeshUpdate` | No exact registry entry | — | — |
| `au.DisableParallelAudioProcessing` | No exact registry entry | — | — |
| `gc.ActorClusteringEnabled` | Registered in attachment | int32 | Whether to allow levels to create actor clusters for GC. |
| `gc.AllowParallelGC` | Registered in attachment | int32 | Used to control parallel GC. |
| `gc.AssetClusteringEnabled` | No exact registry entry | — | — |
| `gc.CreateGarbageCollectorUObjectClusters` | No exact registry entry | — | — |
| `gc.CreateGCClusters` | Registered in attachment | int32 | If true, the engine will attempt to create clusters of objects for better garbage collection performance. |
| `gc.IncrementalBeginDestroyEnabled` | Registered in attachment | int32 | If true, the engine will destroy objects incrementally using time limit each frame |
| `gc.LowMemory.MemoryThresholdMB` | Registered in attachment | float | Memory threshold for low memory GC mode, in MB |
| `gc.LowMemory.TimeBetweenPurgingPendingKillObjects` | Registered in attachment | float | Time in seconds (game time) we should wait between purging object references to objects that are pending kill when we're low on memory |
| `gc.MinDesiredObjectsPerSubTask` | No exact registry entry | — | — |
| `gc.MultithreadedDestructionEnabled` | Registered in attachment | int32 | If true, the engine will free objects' memory from a worker thread |
| `gc.TimeBetweenPurgingPendingKillObjects` | Registered in attachment | float | Time in seconds (game time) we should wait between purging object references to objects that are pending kill. |
| `p.AsyncSceneEnabled` | No exact registry entry | — | — |
| `p.chaos.ChoseGCLOD` | Registered in attachment | int32 | warning, for low memory machine, we choose the lod level, and discards other lod resources |
| `p.chaos.ChoseGCSecondaryLOD` | Registered in attachment | int32 | warning, for low memory machine, we choose the lod level for secondary fragment, and discards other lod resources |
| `p.Chaos.ClientGCMaxRenderNum` | Registered in attachment | int32 | Define the max number of client gc to render |
| `p.Chaos.GCRemoveInternalfaceFaceRender` | Registered in attachment | int32 | Disable rendering of internal face in geometry collection |
| `p.Chaos.GGCRemoveInternalfaceFaceInShadow` | Registered in attachment | int32 | Disable shadow rendering of internal face in geometry collection |
| `p.Chaos.PerformGeometryReduction` | Registered in attachment | int32 | Perform convex geometry simplification to increase performance in Chaos physics. |
| `r.CustomDepth` | Registered in attachment | int32 | 0: feature is disabled<br>1: feature is enabled, texture is created on demand<br>2: feature is enabled, texture is not released until required (should be the project setting if the feature should not stall)<br>3: feature is enabled, stencil writes are enabled, texture is not released until required (should be the project setting if the feature should not stall) |
| `r.D3D12.GPUTimeout` | Registered in attachment | int32 | 0: Disable GPU Timeout; use with care as it could freeze your PC!<br>1: Enable GPU Timeout; operation taking long on the GPU will fail(default) |
| `r.DetailMode` | Registered in attachment | int32 | Current detail mode; determines whether components of actors should be updated/ ticked.<br> 0: low, show only object with DetailMode low or higher<br> 1: medium, show all object with DetailMode medium or higher<br> 2: high, show all objects (default) |
| `r.DirectX.UsePerQueueFence` | No exact registry entry | — | — |
| `r.EnableMorphTargets` | Registered in attachment | int32 | Enable Morph Targets |
| `r.ForceAllCoresForShaderCompiling` | Registered in attachment | int32 | When set to 1, it will ignore INI settings and launch as many ShaderCompileWorker instances as cores are available.<br>Improves shader throughput but for big projects it can make the machine run OOM |
| `r.FreeSkeletalMeshBuffers` | Registered in attachment | int32 | Controls whether skeletal mesh buffers are kept in CPU memory to support merging of skeletal meshes.<br>0: Keep buffers(default)<br>1: Free buffers |
| `r.GTSyncType` | Registered in attachment | int32 | Determines how the game thread syncs with the render thread, RHI thread and GPU.<br>Syncing to the GPU swap chain flip allows for lower frame latency.<br> 0 - Sync the game thread with the render thread (default).<br> 1 - Sync the game thread with the RHI thread.<br> 2 - Sync the game thread with the GPU swap chain flip (only on supported platforms). |
| `r.LightTile.Enable` | Registered in attachment | int32 | — |
| `r.MeshCardRepresentation.Async` | Registered in attachment | int32 | — |
| `r.MeshStreaming` | Registered in attachment | int32 | Experimental - When non zero, enables mesh stremaing. |
| `r.OneFrameThreadLag` | Registered in attachment | int32 | Whether to allow the rendering thread to lag one frame behind the game thread (0: disabled, otherwise enabled) |
| `r.ParallelInitDynamicRHI` | No exact registry entry | — | — |
| `r.PostProcessing.DisableMaterials` | Registered in attachment | int32 | Allows to disable post process materials. |
| `r.RHICmdUseThread` | No exact registry entry | — | — |
| `r.SkeletalMeshLODBias` | Registered in attachment | int32 | LOD bias for skeletal meshes (does not affect animation editor viewports). |
| `r.SkeletalMeshLODRadiusScale` | Registered in attachment | float | Scale factor for the screen radius used in computing discrete LOD for skeletal meshes. (0.25-1) |
| `r.SkinCache.CompileShaders` | Registered in attachment | int32 | Whether or not to compile the GPU compute skinning cache shaders.<br>This will compile the shaders for skinning on a compute job and not skin on the vertex shader.<br>GPUSkinVertexFactory.usf needs to be touched to cause a recompile if this changes.<br>0 is off(default), 1 is on |
| `r.StaticMeshLODBias` | Registered in attachment | int32 | Static Mesh LOD Bias |
| `r.StaticMeshLODDistanceScale` | Registered in attachment | float | Scale factor for the distance used in computing discrete LOD for static meshes. (defaults to 1)<br>(higher values make LODs transition earlier, e.g., 2 is twice as fast / half the distance) |
| `r.Streaming.AmortizeCPUToGPUCopy` | Registered in attachment | int32 | If set and r.Streaming.MaxNumTexturesToStreamPerFrame > 0, limit the number of 2D textures streamed from CPU memory to GPU memory each frame |
| `r.Streaming.DelayProcessPendingMipCopyRequests` | Registered in attachment | bool | If true, call ProcessPendingMipCopyRequests at the beginning of UpdateResourceStreaming.This means the process is delay until the next frame, but it can optimize the time spent on waiting FUpdateStreamingRenderAssetsTask. |
| `r.Streaming.FramesForFullUpdate` | Registered in attachment | int32 | Texture streaming is time sliced per frame. This values gives the number of frames to visit all textures. |
| `r.Streaming.LimitPoolSizeToVRAM` | Registered in attachment | int32 | If non-zero, texture pool size with be limited to how much GPU mem is available. |
| `r.Streaming.MaxEffectiveScreenSize` | Registered in attachment | float | 0: Use current actual vertical screen size<br>> 0: Clamp wanted mip size calculation to this value for the vertical screen size component. |
| `r.Streaming.MaxNumTexturesToStreamPerFrame` | Registered in attachment | int32 | Maximum number of 2D textures allowed to stream from CPU memory to GPU memory each frame. <= 0 means no limit. This has no effect if r.Streaming.AmortizeCPUToGPUCopy is not set |
| `r.Streaming.MipBias` | Registered in attachment | float | 0..x reduce texture quality for streaming by a floating point number.<br>0: use full resolution (default)<br>1: drop one mip<br>2: drop two mips |
| `r.Streaming.NumStaticComponentsProcessedPerFrame` | Registered in attachment | int32 | If non-zero, the engine will incrementaly inserting levels by processing this amount of components per frame before they become visible |
| `r.Streaming.PoolSize` | Registered in attachment | int32 | -1: Default texture pool size, otherwise the size in MB |
| `r.Streaming.PoolSizeForGCs` | Registered in attachment | int32 | < 0: GeometryCollection and texture share the same pool, otherwise the size of pool dedicated to GeometryCollections. |
| `r.Streaming.PoolSizeForMeshes` | Registered in attachment | int32 | < 0: Mesh and texture share the same pool, otherwise the size of pool dedicated to meshes. |
| `r.Streaming.UsePerMeshBias` | Registered in attachment | int32 | If non-zero, each mesh will be assigned a mip bias between 0 and MipBias as required to fit in budget. |
| `r.TaskGraph.TasksPerThread` | No exact registry entry | — | — |
| `r.TeamOutline.LineWidth` | Registered in attachment | int32 | Team outline line width (only 1 or 2 width avaliable now).Not working for LineMode 0, only LineMode 1 and 2Exterior line mode : skip internal pixels;Internal line mode : True/1 -> 4 samples, False/0 ->8 samples |
| `r.TextureStreaming.DiscardUnusedMips` | No exact registry entry | — | — |
| `r.ViewDistanceScale` | Registered in attachment | float | Controls the view distance scale. A primitive's MaxDrawDistance is scaled by this value.<br>Higher values will increase view distance but at a performance cost.<br>Default = 1. |
| `r.VirtualTextureReducedMemory` | No exact registry entry | — | — |
| `RHI.MaximumFrameLatency` | Registered in attachment | int32 | Number of frames that can be queued for render. |
| `s.AdaptiveAddToWorld.Enabled` | Registered in attachment | int32 | Enables the adaptive AddToWorld timeslice (replaces s.LevelStreamingActorsUpdateTimeLimit) (default: off) |
| `s.AsyncLoadingThreadEnabled` | Registered in attachment | int32 | Placeholder console variable, currently not used in runtime. |
| `s.AsyncLoadingTimeLimit` | Registered in attachment | float | Maximum amount of time to spend doing asynchronous loading (ms per frame). |
| `s.ForceGCAfterLevelStreamedOut` | Registered in attachment | int32 | Whether to force a GC after levels are streamed out to instantly reclaim the memory at the expensive of a hitch. |
| `s.IoDispatcherBufferMemoryMB` | Registered in attachment | int32 | IoDispatcher buffer memory size (in megabytes). |
| `s.IoDispatcherCacheSizeMB` | Registered in attachment | int32 | IoDispatcher cache memory size (in megabytes). |
| `s.IoDispatcherDecompressionWorkerCount` | Registered in attachment | int32 | IoDispatcher decompression worker count. |
| `s.IoDispatcherTocsEnablePerfectHashing` | Registered in attachment | int32 | Enable perfect hashmap lookups for iostore tocs |
| `s.LevelStreamingActorsPerPage` | No exact registry entry | — | — |
| `s.MaxPrecacheRequestsInFlight` | Registered in attachment | int32 | Controls the maximum amount of precache requests to have in flight. |
| `s.MinBulkDataSizeForAsyncLoading` | Registered in attachment | int32 | Minimum time the time limit exceeded warning will be triggered by. |
| `s.ProcessPrestreamingRequests` | Registered in attachment | int32 | If non-zero, then we process prestreaming requests in cooked builds. |
| `skelot.ForceLOD` | Registered in attachment | int32 | similar to r.ForceLOD, -1 to disable |
| `spine.MaxSkeletonFrameRate` | Registered in attachment | int32 | If 0 (default), no limit is enforced. If greater than 0, the maximum frame rate for a skeleton is limited to this value. |
| `TaskGraph.MaxTaskThreadsPerGroup` | No exact registry entry | — | — |
| `TaskGraph.MaxWorkerThreads` | No exact registry entry | — | — |
| `tick.AllowAsyncNetTicks` | Registered in attachment | int32 | Set 0 for disable parallel optimation for net tick. |
| `tick.AllowAsyncProjectileComponent` | Registered in attachment | bool | Set 0 for disable parallel optimation of projectile movement component. |
| `tick.AllowAsyncSummonedComponent` | Registered in attachment | bool | Set 0 for disable parallel optimation for components of Summoners. |

## Important corrections and risks in the community bundle

- `r.D3D12.GPUTimeout=0` removes the GPU timeout guard in Epic's documented implementation and can freeze the machine if the GPU hangs.
- `s.IoDispatcherBufferMemoryMB=1024` and `s.IoDispatcherCacheSizeMB=2048` reserve large memory budgets. Larger buffers/caches can crowd out other game/system memory and are not proof of higher throughput.
- Some variables are spelling-sensitive. Preserve exact names, including `gc.AssetClusteringEnabled` vs Epic's differently spelled `gc.AssetClustreringEnabled`, and the thread's `GGC`, `Chose`, and `InternalfaceFace` names, until the game's own registration confirms the intended spelling.
- The `!` lines under “Fix Broken Retexture Mods” use this loader's reset-to-game-value behavior. They do not force high LODs. The section also contains duplicate resets of the same `r.SkeletalMeshLODBias` key.
- Turning off custom depth or post-process material paths can remove visual information, not just cosmetic effects.
- Parallel/tick/physics/network variables may affect timing or gameplay correctness. Names imply intent but do not prove thread safety in the game's fork.

## Follow-up research needed

1. Confirm exact CVar registration and startup values from the running Marvel Rivals build (console query, engine log, or sufficiently complete binary/runtime inspection). A config line being accepted by the loader is not proof the engine recognized it.
2. Inspect the thread's four attached screenshots for their actual benchmark setup/results and determine whether there is a usable controlled pair; the post's text alone does not attribute gains to any particular setting.
3. Find the code or reliable build-specific evidence for the names marked “Not located,” especially task graph, `tick.*`, `p.Chaos.*`, `spine.*`, the outline variable, and the alleged input keys.
4. Once registration is confirmed, run controlled one-variable comparisons per engine/build and record frame-time distributions, memory use, visual differences, and crash/stability outcomes. Do not use a single FPS average as the only success measure.
5. Expand this catalog with newly found Marvel-specific CVars and refresh evidence after game patches. Epic's reference will continue to be a useful index of upstream UE variables, but cannot define the entire game fork.

## References

- [Original community Discord thread](https://discord.com/channels/1452445537298022637/1556428197820633269).
- [Community CVar registry attachment](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- [Community CVar snapshot attachment](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference).
- [Unreal Engine 5.9 Texture Streaming Configuration](https://dev.epicgames.com/documentation/unreal-engine/texture-streaming-configuration-in-unreal-engine).
- [Official Marvel Rivals use-of-mods notice](https://www.marvelrivals.com/20261015/41525_1316797.html) and [prohibited software list](https://www.marvelrivals.com/guide/20250226/41348_1214569.html).
