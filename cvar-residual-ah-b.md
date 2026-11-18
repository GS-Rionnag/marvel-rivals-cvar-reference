# Asset loading, presentation, and diagnostics CVars beginning A–H

This guide follows [the first A–H batch](cvar-residual-ah.md) with 38 more exact registry names. The snapshot records observed values. A dash means the snapshot lacks a value. Defaults and setting lifecycle details in the descriptions come from the supplied help.

| Exact CVar | Kind / type | Snapshot | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `AssetRegistry.LoadDependencies` | `var` / `int32` | — | Loads dependency data from premade registries in cooked Windows processes. Help describes a startup setting in Engine.ini [SystemSettings] that requires restarting. | 0 / 3 | 0 / 1 |
| `AssetRegistry.LoadPackageData` | `var` / `int32` | — | Loads package data from premade registries in cooked Windows processes. Help describes a startup setting in Engine.ini [SystemSettings] that requires restarting. | 0 / 3 | 0 / 1 |
| `Async.ParallelFor.YieldingTimeout` | `ref` / `int32` | `8` | Milliseconds before background-priority ParallelFor work yields to higher-priority tasks. | 22 / 3 | 1 / 1 |
| `AutoTest.LogMacros` | `ref` / `FString` | — | Sets all log-category verbosity to Warning according to the test help. | 1 / 2 | 2 / 1 |
| `Automation.CaptureLogEvents` | `ref` / `bool` | `true` | Treats warning and error log events during automation tests as affecting the test result. | 1 / 3 | 1 / 1 |
| `Automation.LogBPTestMetadata` | `ref` / `bool` | `false` | Writes Blueprint functional-test metadata to the log during testing. | 0 / 3 | 1 / 1 |
| `Automation.SkipStackWalk` | `ref` / `bool` | `false` | Controls skipping stack walks in the automation test framework. Help gives no finer scope. | 1 / 3 | 1 / 1 |
| `BehaviorTree.RecordFrameSearchTimes` | `var` / `int32` | `0` | Records per-frame behavior tree search times for performance statistics. | 0 / 3 | 0 / 1 |
| `BuildPatchFileConstructor.SleepTimeWhenFileSystemThrottledSeconds` | `ref` / `int32` | `15` | Seconds to sleep when the destination filesystem is throttled. | 2 / 3 | 1 / 1 |
| `BuildPatchFileConstructor.bStallWhenFileSystemThrottled` | `ref` / `bool` | `false` | Controls stalling when the filesystem is throttled. | 1 / 3 | 1 / 1 |
| `Career.PreloadAlignWithCharacter` | `var` / `bool` | `true` | Aligns career hero asset preload bundles with the local-client bundle set used by ProcessHeroAssetParams. | 0 / 3 | 0 / 1 |
| `Config.ShareValues` | `ref` / `int32` | — | Startup-only sharing for identical long config values until a string reference is requested. Help gives 0 as the original-storage default and 1 as shared storage, and says the LowMemory startup option enables sharing. | 11 / 3 | 1 / 1 |
| `Core.bFastDecimalFormatLargeFloatSupport` | `ref` / `int32` | `1` | Processes floating-point values above 9223372036854775807 to avoid clipping them to that limit during decimal formatting. | 2 / 3 | 1 / 1 |
| `CriticalPathStall.TickStartFrame` | `var` / `float` | `0` | Adds a debug sleep at frame start, in milliseconds, for critical-path analysis. | 0 / 3 | 0 / 1 |
| `CueFuncLibrary.OnlyPreloadMarvelGASInstantCue` | `ref` / `bool` | `false` | Preloads only instant-effect cues without components, leaving persistent cues outside this preload. | 2 / 3 | 1 / 1 |
| `CueFuncLibrary.SkipMarvelGASCuePreload` | `ref` / `bool` | `true` | Skips MarvelGAS character cue preload and loads those cues asynchronously on demand. | 3 / 3 | 1 / 1 |
| `DefaultPakFileRules.AsyncLoading.Enable` | `var` / `int32` | `0` | Test setting for DefaultPakFileRules. Help does not describe the asynchronous test scope. | 0 / 3 | 0 / 1 |
| `DefaultPakFileRules.SyncLoading.Enable` | `var` / `int32` | `0` | Test setting for DefaultPakFileRules. Help does not describe the synchronous test scope. | 0 / 3 | 0 / 1 |
| `GameplayTags.EnableDetailedStats` | `ref` / `bool` | `false` | Runtime switch for verbose CPU profiling statistics. | 0 / 3 | 1 / 1 |
| `Gliding.UseMeshRotationInterp` | `ref` / `bool` | `false` | Controls mesh rotation interpolation. Help gives 0 disabled and 1 enabled. | 7 / 2 | 1 / 1 |
| `Hero.1047.RestoreDivingMaterialSectionState` | `ref` / `bool` | `true` | When enabled, restores Jeff's material section visibility from before diving. | 1 / 3 | 1 / 1 |
| `benchmark.GameThreadTimeMode` | `var` / `int32` | — | Game-thread benchmark timing. 0 excludes idle waits and 1 retains task dependency waits. | 0 / 3 | 0 / 1 |
| `blink.debug.UseGPUMode` | `ref` / `bool` | `false` | Enables Blink GPU assist. Help gives no GPU assist algorithm or mode details. | 1 / 2 | 1 / 1 |
| `bp.BlamePrintString` | `ref` / `bool` | `false` | Logs the Blueprint asset and function responsible for Print String calls to help trace screen-message spam. | 0 / 2 | 1 / 1 |
| `bp.ComponentInstancingFastPathDisabled` | `ref` / `int32` | `0` | Disables the Blueprint component instancing fast path. | 1 / 3 | 1 / 1 |
| `bp.NativePropertyInitFastPathDisabled` | `ref` / `int32` | `0` | Disables the Blueprint native property initialization fast path. | 1 / 3 | 1 / 1 |
| `bp.ScriptRecurseLimit` | `ref` / `int32` | `120` | Sets the recursion limit before script execution is treated as an infinite loop. | 0 / 3 | 1 / 1 |
| `bp.ShortScriptWarnings` | `ref` / `int32` | `0` | Shortens Blueprint exception messages in the log. | 0 / 3 | 1 / 1 |
| `bp.VerboseStats` | `ref` / `int32` | `0` | Creates more Blueprint execution statistics. | 0 / 3 | 1 / 1 |
| `cac.ExperimentalAllowPerInstanceChildActorProperties` | `ref` / `int32` | `0` | Experimental switch allowing child actor properties to be modified per instance. | 2 / 3 | 1 / 1 |
| `cook.AllowCookedDataInEditorBuilds` | `ref` / `int32` | `0` | Allows loading cooked assets in editor builds. | 0 / 3 | 1 / 2 |
| `cook.SkipAsyncLoaderForCookedData` | `ref` / `int32` | `0` | Loads the cooked package header synchronously to reduce cross-thread handoffs. | 1 / 3 | 1 / 1 |
| `core.EnsuresAreErrors` | `ref` / `int32` | `1` | Logs failed ensures as errors when true and as warnings when false. | 0 / 2 | 1 / 1 |
| `dt.ValidateMigration` | `ref` / `bool` | `false` | Validates migrated DataTable fields by comparing them with SparseConfig or OptionalConfig values. Translated help. | 0 / 3 | 1 / 1 |
| `fc.BlockSize` | `ref` / `int32` | `64` | Block size in KB for the global file cache. Help associates matching the package compression block size with optimal reads. | 6 / 3 | 1 / 1 |
| `fc.NumBlocks` | `ref` / `int32` | `256` | Number of blocks in the global file cache. | 1 / 3 | 1 / 1 |
| `frametask.budget` | `ref` / `float` | `0.005` | Per-frame FrameTaskManager budget, in seconds. Translated help. | 2 / 2 | 1 / 1 |
| `g.bEnablePendingCleanupObjectsCommandBatching` | `ref` / `bool` | `true` | Batches destruction of PendingCleanupObjects. | 2 / 3 | 1 / 1 |

Scan counts are from Shipping 1.1.4042190. Direct-memory candidates can include initialization, reads, or writes. Availability and runtime behavior remain unverified.

Sources include the [preserved registry, snapshot, and translated help](EVIDENCE.md#community-sources) and the [static address scan](EVIDENCE.md#build-specific-static-analysis).
