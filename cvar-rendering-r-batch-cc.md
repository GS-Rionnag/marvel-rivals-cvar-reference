# Post-processing and pipeline state CVars (batch CC)

The final 51 uncovered exact `r.*` registry names after [batch CB](cvar-rendering-r-batch-cb.md) cover post-processing, pipeline state object (PSO) compilation and caching, render scheduling, and diagnostics. The snapshot column records observed values. Epic values are exact-name UE 5.9 reference defaults from the local catalog. A dash indicates an absent source value.

| Exact CVar | Kind / type | Snapshot | Epic 5.9 | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | ---: | --- | ---: | ---: |
| `r.postprocessing.EnableCAS` | `ref` / `bool` | `true` | — | Global rendering switch for CAS. Help leaves the implementation and mode values unspecified. | 1 / 3 | 1 / 1 |
| `r.postprocessing.EnableEyeAdaptation` | `ref` / `bool` | `true` | — | Global eye-adaptation rendering switch. | 1 / 3 | 1 / 1 |
| `r.postprocessing.EnableHeroOutline` | `ref` / `bool` | `true` | — | Rendering switch for hero outlines and team outlines. | 2 / 2 | 1 / 1 |
| `r.postprocessing.EnableSkipPPByName` | `ref` / `bool` | `false` | — | Skips a post-process by name. Help leaves the name source and matching behavior unspecified. | 1 / 3 | 1 / 1 |
| `r.pso.AllowComputePSODelete` | `ref` / `bool` | `false` | — | Allows deletion of compute pipeline state objects (PSOs). Help leaves the deletion timing unspecified. | 6 / 3 | 1 / 1 |
| `r.pso.ComputeCommandLifetimeRef` | `ref` / `bool` | — | — | Keeps compute pipeline state wrappers alive while queued Render Hardware Interface (RHI) commands reference them. | 2 / 3 | 1 / 1 |
| `r.pso.ComputeResidentMode` | `ref` / `int32` | `0` | — | Selects compute preload and legacy residency through ReservePSOUsage. 0 retains global and Niagara compute PSOs and is the help-stated default. 1 retains global compute PSOs and still bakes base and hero PSOs into DXCache. 2 reserves none. Help says LRU ignores the reserve policy and skips startup preload when both compile phases are complete. | 2 / 2 | 1 / 1 |
| `r.pso.CreateOnRHIThread` | `ref` / `bool` | `false` | `false` | 0 creates PSOs on task threads. 1 creates them on the RHI thread. | 1 / 3 | 1 / 1 |
| `r.pso.DXCacheWithDelPSO` | `ref` / `bool` | `true` | — | Help mentions creating file-cache PSOs with deleted PSOs. The exact file-cache operation and relationship to deletion are unclear. | 1 / 2 | 1 / 1 |
| `r.pso.EnableHeroSkillPSOMask` | `ref` / `bool` | `true` | — | Enables a hero-skill PSO mask. Help leaves mask contents and selection unspecified. | 1 / 2 | 1 / 1 |
| `r.pso.EnableReloadPSOMask` | `ref` / `bool` | `true` | — | Enables a reload PSO mask. Help leaves mask contents and reload triggers unspecified. | 4 / 2 | 1 / 1 |
| `r.pso.FixGraphicsCompileTaskRefLeak` | `var` / `int32` | `1` | — | 0 restores legacy asynchronous graphics PSO compile task reference counting, including duplicate state refs and the Pipeline guard. 1 retains each resource once and releases task-held refs after compilation clears Pipeline. Help confines changes to newly created tasks. | 0 / 3 | 0 / 1 |
| `r.pso.FixLowlevelCacheLeak` | `ref` / `bool` | `true` | — | Help describes allowing graphics PSO deletion. It gives no additional low-level cache or leak details. | 2 / 3 | 1 / 1 |
| `r.pso.FixPSOCompileWait` | `ref` / `bool` | `true` | — | Help describes a PSO compile wait fix. It gives no wait conditions or mode values. | 2 / 2 | 1 / 1 |
| `r.pso.GlobalPSOUseDefaultLoad` | `ref` / `bool` | `true` | — | Help mentions skipping general PSO loading while still loading some required PSOs. The selection criteria are unspecified. | 0 / 2 | 1 / 1 |
| `r.pso.GlobalPSOUseThreadPool` | `ref` / `bool` | `true` | — | Selects use of a thread pool for global PSOs. Help leaves the scheduling details unspecified. | 1 / 2 | 1 / 1 |
| `r.pso.LowLevelLRU.AsyncRelease` | `var` / `int32` | — | — | 0 releases detached PSOs on the RHI thread. 1 transfers detached PSOs to one background batch per adapter and queues new releases while that batch is active. Requires LowLevelLRU. ReleasePerFrame caps batches per pool. On disabling, the active batch finishes before synchronous releases resume, without an RHI wait according to the help. | 0 / 3 | 0 / 1 |
| `r.pso.LowLevelLRU.Enable` | `var` / `int32` | — | — | Startup-only D3D12 low-level LRU for runtime PSOs. Help lists -PSOLowLevelLRU as an enable option and says 0 keeps legacy behavior. | 0 / 3 | 0 / 1 |
| `r.pso.LowLevelLRU.LogInterval` | `var` / `float` | — | — | Seconds between per-pool count and cumulative activity logs. 0 disables logging. | 0 / 3 | 0 / 1 |
| `r.pso.LowLevelLRU.MaxComputeCount` | `var` / `int32` | — | — | Compute PSOs deliberately retained per adapter. 0 retains none, -1 is unlimited, and other negatives act as 0. | 0 / 3 | 0 / 1 |
| `r.pso.LowLevelLRU.MaxGraphicsCount` | `var` / `int32` | — | — | Graphics PSOs deliberately retained per adapter. 0 retains none, -1 is unlimited, and other negatives act as 0. | 0 / 3 | 0 / 1 |
| `r.pso.LowLevelLRU.ReleasePerFrame` | `var` / `int32` | — | — | Maximum detached PSO references released per pool per RHI frame. Help gives a minimum of 1. | 0 / 3 | 0 / 1 |
| `r.pso.MaxBatchSize` | `ref` / `int32` | `300` | — | PSO batch-size maximum. Help leaves the batch stage unspecified. | 2 / 2 | 1 / 1 |
| `r.pso.NewPSOMaterialTrack` | `ref` / `int32` | `0` | — | Tracks material information for newly encountered PSOs. 0 disables and 1 enables. | 3 / 3 | 1 / 1 |
| `r.pso.NonPSOCompileThreadReserveSize` | `ref` / `int32` | `3` | — | Number of threads reserved for work other than PSO compilation. | 1 / 3 | 1 / 1 |
| `r.pso.OpenPSODebugLog` | `ref` / `bool` | `false` | — | Enables PSO debug log output. Help leaves the content and categories unspecified. | 1 / 2 | 1 / 1 |
| `r.pso.OpenPSOLog` | `ref` / `bool` | `false` | — | Enables PSO log output. Help leaves the content and categories unspecified. | 2 / 2 | 1 / 1 |
| `r.pso.PSOMtlNameRecord` | `ref` / `bool` | `false` | — | Enables recording material names in PSO tracking. Help leaves the output format unspecified. | 2 / 2 | 1 / 1 |
| `r.pso.PSOPriority` | `ref` / `int32` | `1` | — | PSO priority setting. Help gives no priority scale or scheduling scope. | 1 / 3 | 1 / 1 |
| `r.pso.PSOUseNewTickFunc` | `ref` / `bool` | `true` | — | Selects a new PSO tick function. Help gives no details about its behavior. | 1 / 2 | 1 / 1 |
| `r.pso.PreLoadPSOCostPerFrame` | `ref` / `float` | `10` | — | Per-frame PSO preload cost setting. Help leaves the cost unit unspecified. | 2 / 2 | 1 / 1 |
| `r.pso.PreLoadPSONumPerFrame` | `ref` / `int32` | `20` | — | Per-frame PSO preload count setting. | 3 / 2 | 1 / 1 |
| `r.pso.PreLoadPSOusage` | `ref` / `int32` | `251` | — | Help mentions skipping general PSO loading and loading a preload PSO usage mask. It leaves the mask values unspecified. | 3 / 2 | 1 / 1 |
| `r.pso.PrecompileThreadPoolPercentOfHardwareThreads` | `ref` / `int32` | `0` | `75` | A positive percentage selects the precompile pool size as a share of hardware threads, rounded up, as an alternative to r.pso.PrecompileThreadPoolSize. Help gives 0 as the default and describes it as disabling precompile pool usage. | 2 / 3 | 1 / 1 |
| `r.pso.PrecompileThreadPoolSize` | `ref` / `int32` | `0` | `0` | Fixed thread count available for concurrent PSO precompilation. Help gives 0 as the default and describes it as disabling precompile pool usage. | 1 / 3 | 1 / 1 |
| `r.pso.PrecompileThreadPoolSizeMax` | `ref` / `int32` | `2147483647` | `2147483647` | Maximum thread count for percentage-based PSO precompilation. Applies when r.pso.PrecompileThreadPoolPercentOfHardwareThreads selects the size. Help gives INT_MAX as the uncapped default. | 1 / 3 | 1 / 1 |
| `r.pso.PrecompileThreadPoolSizeMin` | `ref` / `int32` | `0` | `2` | Minimum thread count when r.pso.PrecompileThreadPoolPercentOfHardwareThreads selects the size. Help gives 0 as the default with no minimum. | 1 / 3 | 1 / 1 |
| `r.pso.PrecompileThreadPoolThreadPriority` | `ref` / `int32` | `2` | `2` | Sets PSO precompile pool thread priority. Help gives no numeric mapping. | 5 / 3 | 1 / 1 |
| `r.pso.SkipDirverInstallTimeCheck` | `ref` / `bool` | `false` | — | Skips the driver installation-time process according to the help. Dirver is the registry spelling. | 1 / 2 | 1 / 1 |
| `r.pso.ThreadPoolPercentOfHardwareThreads` | `ref` / `int32` | `100` | — | A positive percentage selects a thread pool size as a share of hardware threads, rounded up. Help calls it an alternative to r.pso.ThreadPoolSize and refers to precompilation, while the associated bounds refer to compilation. | 2 / 3 | 1 / 1 |
| `r.pso.ThreadPoolSizeMax` | `ref` / `int32` | `2147483647` | — | Maximum thread count for concurrent PSO compilation when r.pso.ThreadPoolPercentOfHardwareThreads selects pool size. Help gives INT_MAX as the uncapped default. | 1 / 3 | 1 / 1 |
| `r.pso.ThreadPoolSizeMin` | `ref` / `int32` | `2` | — | Minimum thread count for concurrent PSO compilation when r.pso.ThreadPoolPercentOfHardwareThreads selects pool size. | 1 / 3 | 1 / 1 |
| `r.pso.UseBackgroundThread` | `ref` / `bool` | `true` | — | Uses background threads for PSO work. Help leaves scope and priority unspecified. | 1 / 2 | 1 / 1 |
| `r.pso.UseNewDelayedCleanupFunc` | `ref` / `bool` | `true` | — | Selects the new delayed PSO cleanup function. Help leaves cleanup scheduling unspecified. | 2 / 2 | 1 / 1 |
| `r.pso.UsePSOCompileThreadPool` | `ref` / `bool` | `true` | — | Uses a compile thread pool to create PSOs. | 2 / 2 | 1 / 1 |
| `r.pso.evictiontime` | `var` / `int32` | `60` | `60` | Interval between checks for stale cached objects. Help leaves the unit unspecified and says 0 disables eviction, allowing memory use to grow. | 0 / 3 | 0 / 1 |
| `r.shadow.ShadowMapsRenderEarly` | `var` / `int32` | `0` | `0` | Renders shadow maps earlier in the frame to help asynchronous compute scheduling on some platforms. Help marks it incompatible with Virtual Shadow Maps. | 0 / 3 | 0 / 1 |
| `r.slate3d.SkipMaterialUpdate` | `ref` / `int32` | `1` | — | Avoids a full material uniform-buffer update during a Slate 3D update. | 2 / 2 | 1 / 1 |
| `r.velocity.visualization` | `var` / `int32` | `0` | — | Displays velocity in a post-process overlay. | 0 / 3 | 0 / 1 |
| `r.vt.FeedbackFactor` | `ref` / `int32` | `16` | `16` | Divides render resolution by the factor to size the virtual-texture feedback buffer. The factor rounds up to the next power of two when necessary. | 1 / 3 | 1 / 1 |
| `r.vulkan.LogDefrag` | `ref` / `int32` | `0` | — | Logs all Vulkan defragmentation moves and evictions. `0` disables logging and `1` enables it. The registry spells `vulkan` in lowercase. | 5 / 3 | 1 / 1 |

The scan columns count direct-memory and address-taking candidates for `ref_rva` and `obj_rva` in the Shipping 1.1.4042190 scan. Direct-memory candidates may include initialization, reads, and writes. Feature activation, startup override acceptance, and runtime effects remain unverified.

Registry help and snapshots come from the [preserved community sources](EVIDENCE.md#community-sources). Epic defaults appear in the [community registry catalog](EVIDENCE.md#community-sources). See the [address-match TSV](EVIDENCE.md#build-specific-static-analysis) and [build notes](EVIDENCE.md#build-specific-static-analysis) for scan evidence.
