# Niagara CVars: batch D

This batch covers the next 25 uncovered `fx.Niagara.*` entries in the community registry, in alphabetical order. All are typed `ref` there. Snapshot values are observations from a separate attachment with unknown build and capture method; they are not verified defaults or recommendations.

## Automation, component pools, and diagnostics

| Exact CVar | Type | Snapshot | What the registry help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.CompileWaitLoggingCap` | int32 (`ref`) | `3` | During automation, sets how many times to log before failing compilation. The help does not say what event is counted or whether the cap is per script, emitter, or run. | No read-like `ref_rva` instruction was found. The scan matches registration/setup only; it does not establish whether the automation path is active in Shipping. |
| `fx.Niagara.CompileWaitLoggingThreshold` | float (`ref`) | `30` | During automation, sets how long to wait for a compile result before logging. The help does not specify a time unit. | No read-like `ref_rva` instruction was found. The wait/log path and unit were not recovered. |
| `fx.Niagara.ComponentRenderComponentCountWarning` | float (`ref`) | `50` | Sets the maximum allowed component count before the component renderer shows a UI warning. The help does not define the warning UI, scope, or whether a fractional value is meaningful. | No read-like `ref_rva` instruction was found. The warning path was not traced. |
| `fx.Niagara.ComponentRenderPoolInactiveTimeLimit` | float (`ref`) | `5` | Sets, in seconds, how long an inactive component may remain in the pool before destruction. The component type and pool policy are not detailed. | One `movss` load candidate reads `ref_rva` in build 4042190. The scan does not identify the pool cleanup branch or establish that it runs in this game. |
| `fx.Niagara.ComponentWarnAsleepCullReaction` | int32 (`ref`) | `1` | When enabled, warns if a `NiagaraComponent` completes naturally while its cull reaction is set to `Asleep`. The help describes a diagnostic warning, not a change to the cull reaction. | One comparison candidate reads `ref_rva`. Its warning path and Shipping availability are unverified. |
| `fx.Niagara.ComponentWarnNullAsset` | int32 (`ref`) | `0` | When enabled, warns when a `NiagaraComponent` is activated with a null asset; help says this can help find components that could be removed. | One comparison candidate reads `ref_rva`. The warning path and output are unverified. |
| `fx.Niagara.CompressScriptByteCode` | bool (`ref`) | `false` | Compresses script bytecode to save memory, with decompression on demand. The help does not specify compression format or memory/CPU tradeoffs. | No read-like `ref_rva` instruction was found. The runtime compression path was not observed. |
| `fx.Niagara.ConcurrentDoAsyncQuery` | int32 (`ref`) | `1` | Handles asynchronous query logic concurrently. The help does not identify the query type, concurrency mechanism, or behavior when disabled. | Two comparison candidates read `ref_rva`. The query path and concurrency effects were not traced. |
| `fx.Niagara.CullDisabledEmittersOnLoad` | int32 (`ref`) | `0` | In cooked builds with a fixed quality level, a nonzero value discards emitters and renderers disabled for that quality level during `PostLoad`, allowing garbage collection to reclaim them. Help states default `0`. | One comparison candidate reads `ref_rva`. The saved value is also `0`; neither establishes the Shipping default or confirms the load-time cull path runs here. |

## Data Channels and skeletal-mesh data interfaces

| Exact CVar | Type | Snapshot | What the registry help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.DataChannels.DebugDumpWriterDI` | int32 (`ref`) | `0` | No help is supplied. The name suggests a debug control related to a Data Channel writer data interface, but the name alone does not establish what it dumps or where. | One comparison candidate reads `ref_rva`; no dump behavior was recovered. |
| `fx.Niagara.DataChannels.DumpHandlerTick` | int32 (`ref`) | `0` | No help is supplied. The name suggests a Data Channel handler tick diagnostic, but does not define the handler, output, or value mapping. | No read-like `ref_rva` instruction was found. No behavior was recovered. |
| `fx.Niagara.DataChannels.Enabled` | bool (`ref`) | `true` | Enables Niagara Data Channels. Help does not state which systems use them or what fallback applies when disabled. | Twenty-three comparison candidates read `ref_rva` across the scanned executable. They show the value is checked in this build, but not the full effect or feature coverage. |
| `fx.Niagara.DataChannels.ForceReadPrevFrame` | bool (`ref`) | `false` | Forces Niagara systems with Niagara Data Channel read data interfaces to read from the previous frame. The scope and synchronization effects are not detailed. | Six comparison candidates read `ref_rva`. The read timing behavior was not traced. |
| `fx.Niagara.DataChannels.ForceReadTickGroup` | int32 (`ref`) | `-1` | At values `>= 0`, forces Niagara systems with Data Channel read data interfaces to tick in the given tick group. The mapping from integers to groups and invalid-value handling are not stated. | Two comparisons and one conditional-move load candidate read `ref_rva`. No complete tick-group selection path was recovered. |
| `fx.Niagara.DataInterfaceSkeletalMeshLODBias` | int32 (`ref`) | `0` | Adds a bias to `WholeMeshLOD` for the skeletal-mesh data interface. Help says `-1` means never select the last LOD and `+1` means never select the first; stated default is `0`. The exact selection rule and behavior outside these values are not explained. | No `ref_rva` access candidate was found; only setup/object evidence appears in the saved scan. The LOD-selection code was not verified in this build. |

## Debug and rendering controls

| Exact CVar | Type | Snapshot | What the registry help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.Debug.GlobalLoopTime` | float (`ref`) | `0` | If greater than zero, resets all Niagara effects every `N` seconds. The reset trigger and whether `N` is measured from startup or per-system state are unspecified. | One `movss` load candidate reads `ref_rva`; the reset path and scheduling were not recovered. |
| `fx.Niagara.DebugDraw.Enabled` | int32 (`ref`) | `1` | Enables or disables the Debug Draw data interface; help warns that disabling it does not remove all overhead. It does not identify the remaining overhead. | No read-like `ref_rva` instruction was found. The debug draw implementation was not traced. |
| `fx.Niagara.DecalRenderer.Enabled` | bool (`ref`) | `true` | A value of `0` disables Niagara decal renderers. Help does not describe whether affected systems omit decals or use another renderer. | No read-like `ref_rva` instruction was found. The renderer gate was not recovered. |
| `fx.Niagara.DelayScriptAsyncOptimization` | bool (`ref`) | `false` | Controls whether asynchronous optimization is delayed until an emitter is activated. The optimization and its cost/benefit are not specified. | One comparison candidate reads `ref_rva`. No optimization scheduling path was recovered. |
| `fx.Niagara.DumpNans` | int32 (`ref`) | `0` | Any nonzero value dumps NaNs whenever they are encountered. The output destination and data included are unspecified. | No read-like `ref_rva` instruction was found. The dump path and runtime cost are unverified. |
| `fx.Niagara.DumpNansOnce` | int32 (`ref`) | `0` | Any nonzero value dumps NaNs for the first emitter that encounters them. The help does not state whether “once” is per emitter, system, or process. | No read-like `ref_rva` instruction was found. The once-only state and output path were not traced. |
| `fx.Niagara.EableDynamicFragment` | int32 (`ref`) | `1` | The name is spelled `Eable` in the registry. Help says that a value greater than zero lets Chaos enable dynamic fragments; it does not define the fragment type or relation to Niagara. | No read-like `ref_rva` instruction was found. The unusual spelling is preserved exactly; the Chaos/Niagara path was not recovered. |

## Emitter PSO and GPU-buffer controls

| Exact CVar | Type | Snapshot | What the registry help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.Emitter.ComputePSOPrecacheMode` | int32 (`ref`) | `1` | Help maps `0` to disabled (stated default); `1` enables when `r.PSOPrecaching` is enabled; `2` forces it; `3` forces it and prevents emitters running until precaching completes. For mode `1`, emitter waiting also depends on `r.PSOPrecache.ProxyCreationWhenPSOReady=1`. | Four comparison candidates read `ref_rva`. Mode handling, cross-CVar gates, and startup stalls were not traced end to end. |
| `fx.Niagara.Emitter.MaxGPUBufferElements` | int32 (`ref`) | `0` | Sets the maximum elements per GPU buffer. Help says requests below the size needed for a unit of work are raised to that size, and `0` allows the maximum supported by the RHI. It gives an example that 4k elements would restrict a float buffer to 16k, but does not clarify the element/byte relationship further. | One signed-integer load candidate reads `ref_rva`. The allocation limits, RHI-specific maximum, and exact size units were not recovered. |
| `fx.Niagara.EmitterBounds.DynamicExpandMultiplier` | float (`ref`) | `1.1` | Multiplies dynamically gathered bounds after dynamic bounds snapping; help says `1` makes no change and `1.1` increases them by 10%. It does not state clamping or effects on culling. | Two `movss` load candidates read `ref_rva`. Bounds and culling behavior were not traced. |

## What this establishes about overrides

The community registry labels these as references and supplies the help text; the companion snapshot supplies the observed values. The saved scan output's broad `direct-memory-candidate` class includes stores as well as reads, so this page counts only read-like instruction operands that target a `ref_rva` (for example, comparisons or loads from the memory operand). It found such candidates for 14 entries. The other 11 have no read-like `ref_rva` instruction in this scan; their matches are setup/address evidence, not proof that runtime code reads the current value. A missing direct match is also not proof that a setting is unused; indirect or out-of-scan accesses may be missed. Even a read-like match does not reconstruct the full behavior or prove that the setting can be changed through startup configuration.

Accordingly, this batch does not establish that a startup `.ini` override is accepted or that a changed value affects the live game. No controlled override or in-game comparison was performed. Several descriptions concern automation, editor-style component rendering, or data-interface features; names/help alone do not prove those paths are enabled in Marvel Rivals Shipping.

## Sources and related notes

- Registry help/types: [community registry attachment](EVIDENCE.md), summarized in the [community registry guide](cvar-community-registry.md).
- Captured values: [community snapshot attachment](EVIDENCE.md); snapshot build and capture method are unknown.
- Address matches: [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). Read the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis) for scan semantics and limits.
- Nearby upstream families: [Niagara batch C](cvar-fx-niagara-batch-c.md) and [FX budget/Cascade controls](cvar-fx-budget-batch-a.md).
