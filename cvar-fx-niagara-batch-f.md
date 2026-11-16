# Niagara GPU, grid, pool, and validation CVars: batch F

This page documents the next 25 uncovered `fx.Niagara.*` variables in the supplied community registry. The captured values are from a snapshot with unknown build and collection method; they are observations, not confirmed defaults or recommendations. Several names also have exact-name entries in the Unreal Engine 5.9 reference, but that does not establish that Marvel Rivals uses the same engine implementation.

The build-specific scan is for Marvel Rivals Shipping build `1.1.4042190`. A read-like `ref_rva` instruction means code in that binary accesses the registered value's storage; it does not identify every caller, prove the branch runs in a live match, or show that a startup `.ini` can change the value. The scanner's address-taking matches are registration/setup evidence only.

## GPU-compute debug and profiling

| Exact CVar | Type | Snapshot | What the supplied help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.GpuComputeDebug.MaxLineInstances` | int32 (`ref`) | `4096` | Maximum number of line draws supported in one frame. It does not define which GPU-compute visualizations generate lines or what happens when the cap is reached. | No read-like reference access was found; the scan only records an address-taking match. The line cap's consumer was not established in this build. |
| `fx.Niagara.GpuComputeDebug.MaxTextureHeight` | int32 (`ref`) | `128` | Maximum height used when visualizing a texture, to keep it from becoming too large on screen. Width handling and behavior above the cap are unspecified. | No read-like reference access was found; only an address-taking match appears in the scan. |
| `fx.Niagara.GpuComputeDebug.MinTextureHeight` | int32 (`ref`) | `128` | Minimum visualization height; smaller textures are scaled up to this height. The scaling method and interaction with the maximum are not described. | No read-like reference access was found; only an address-taking match appears in the scan. |
| `fx.Niagara.GpuComputeDebug.OccludedLineColorScale` | float (`ref`) | `0.05` | Scales occluded debug-line color/opacity: help maps `0` to transparent and `1` to opaque, and states `0.05` (5%) as the default. | No read-like reference access was found; only an address-taking match appears in the scan. The snapshot happens to equal the help-stated default, but is not independently verified as the game's default. |
| `fx.Niagara.GpuComputeDebug.ShowNaNInf` | int32 (`ref`) | `1` | When enabled, shows NaNs as flashing colors. The help does not say whether the `Inf` part of the name is also visualized or how data is selected. | No read-like reference access was found; only an address-taking match appears in the scan. A captured `1` does not prove this debug view is active or visible in the shipped game. |
| `fx.Niagara.GpuProfiling.Enabled` | bool (`ref`) | `true` | Primary switch allowing Niagara to use GPU profiling. The help does not name the profiler, output path, sampling method, or overhead. | No read-like reference access was found; only an address-taking match appears in the scan. The help does not establish whether profiling is enabled in a normal client session. |

These are described as instrumentation or visualization controls. They do not, from this evidence, establish a general reduction in gameplay effects or a performance improvement when changed.

## Niagara grid formats and resolution

| Exact CVar | Type | Snapshot | What the supplied help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.Grid2D.OverrideFormat` | int32 (`ref`) | `-1` | Optional format override for Grid2D grids. The integer-to-format mapping and the meaning of `-1` are not stated in the supplied help. | Three read-like loads from the `ref_rva` were found. They establish value accesses, not the chosen format or its effects on memory, quality, or compatibility. |
| `fx.Niagara.Grid2D.ResolutionMultiplier` | float (`ref`) | `1` | Optional global modifier for grid resolution. The help does not give the resolution formula, supported range, or scaling direction. | Four read-like operations (`movss`/`mulss`) access the value. The calculations and affected grids were not traced to their results. |
| `fx.Niagara.Grid3D.OverrideFormat` | int32 (`ref`) | `-1` | Optional format override for Grid3D grids. No mapping or sentinel behavior is specified. | Two read-like loads access the value; the format choice and fallback remain unknown. |
| `fx.Niagara.Grid3D.ResolutionMultiplier` | float (`ref`) | `1` | Optional global modifier for grid resolution. No formula, range, or effect on cell count is described. | Six read-like operations access the value. The full resolution path and any downstream memory/performance effect were not reconstructed. |
| `fx.Niagara.Grid3D.UseRGBAGrid` | int32 (`ref`) | `1` | Uses RGBA textures when possible. The help does not define “possible,” the alternative format, or the channel data. | Three comparisons read the value. The format-selection branch and resource consequences were not traced. |

The `-1` format snapshots are consistent with an optional override being unset, but the text does not define `-1`; treat that interpretation as a hypothesis rather than a confirmed mode. The resolution snapshots of `1` likewise do not prove a neutral multiplier is the game's runtime default.

## Tick-group selection and indirect-argument pool

| Exact CVar | Type | Snapshot | What the supplied help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.IgnoreParentTickGroup` | int32 (`ref`) | `1` | Help says not to use the parent component's tick group. It gives no value map or alternative scheduling rule. | One comparison reads the value. The branch's scheduling result and interaction with component/renderer tick groups were not recovered. |
| `fx.Niagara.IndirectArgsPool.AllowShrinking` | int32 (`ref`) | `1` | Allows the indirect-arguments pool to shrink after it remains below a low-water mark for a number of frames. | Two comparisons read the value. The pool lifecycle and the exact gate were not traced end to end. |
| `fx.Niagara.IndirectArgsPool.BlockSizeFactor` | float (`ref`) | `2` | Multiplier used to grow the pool when it runs out of space; help states `2.0` as the default. It does not define rounding or whether the factor applies to the whole pool or an allocation block. | Two floating-point operations read the value. The growth formula and allocation consequences were not reconstructed. |
| `fx.Niagara.IndirectArgsPool.LowWaterAmount` | float (`ref`) | `0.5` | Fraction from `0` to `1` used to decide when pool usage is low enough to warrant shrinking. The exact numerator/denominator and comparison are unspecified. | One floating-point multiplication reads the value. It does not show the complete shrink condition. |
| `fx.Niagara.IndirectArgsPool.LowWaterFrames` | int32 (`ref`) | `150` | Number of frames to wait while below the low-water mark before shrinking; help states `150` as the default. | One integer load reads the value. The frame counter, reset conditions, and shrink action were not traced. |
| `fx.Niagara.IndirectArgsPool.MinSize` | int32 (`ref`) | `256` | Minimum number of draw-indirect arguments allocated in the pool; help states `256` as the default. | Four read-like operations access the value, including loads and comparisons. The allocation units and behavior below the minimum were not reconstructed. |

These pool settings describe capacity and reclamation policy for indirect draw arguments, not particle count directly. The game-specific scan confirms value accesses for this build, but no pool memory measurements or GPU workload tests were performed.

## LOD, Level Sequencer, Curve LUT, and leakage checks

| Exact CVar | Type | Snapshot | What the supplied help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `fx.Niagara.LOD.EnableLODDistance` | int32 (`ref`) | `1` | Nonzero enables `LODDistance`. Which LOD-distance source is enabled and its relationship to `SetLODDistance` are not further described. | No read-like reference access was found; only an address-taking match appears in the scan. |
| `fx.Niagara.LOD.SetLODDistance` | float (`ref`) | `-1` | Sets LOD distance manually; help says this requires `fx.Niagara.LOD.EnableLODDistance = 0`. It does not give units, a valid range, or the meaning of snapshot `-1`. | No read-like reference access was found; only an address-taking match appears in the scan. The manual-distance mode was not observed in the scanned code. |
| `fx.Niagara.LSTickAgeThreshold` | float (`ref`) | `0.05` | Names a Niagara Level Sequencer tick-age threshold and states `0.05f` as the default. The age unit, comparison, and behavior on either side of the threshold are not given. | No read-like reference access was found; only an address-taking match appears in the scan. The help-stated default is not runtime-verified for Marvel Rivals. |
| `fx.Niagara.LUT.OptimizeThreshold` | float (`ref`) | `0.01` | Error threshold for optimizing curve lookup tables; values at or below `0.0` disable optimization. The error metric and resulting approximation are unspecified. | No read-like reference access was found; only an address-taking match appears in the scan. Curve conversion behavior was not traced in this build. |
| `fx.Niagara.LUT.VerifyPostLoad` | int32 (`ref`) | `0` | Enables verification that LUTs after `PostLoad` match the loaded data. It does not describe mismatch handling or reporting. | No read-like reference access was found; only an address-taking match appears in the scan. A captured `0` does not establish the Shipping default. |
| `fx.Niagara.Leakage.EnableCheckParticleLeakage` | bool (`ref`) | `true` | Enables a particle-leakage check. Help gives no specific validation procedure or response. | No read-like reference access was found; only an address-taking match appears in the scan. The check and its execution conditions were not recovered. |
| `fx.Niagara.Leakage.MaxNoParticleCheckLeakageTime` | float (`ref`) | `30` | If an instance has remained without particles for longer than this threshold, it is considered at leakage risk. The time unit and follow-up action are not stated. | No read-like reference access was found; only an address-taking match appears in the scan. The threshold's unit and comparison path remain unverified. |
| `fx.Niagara.Leakage.MaxNoParticlesInstancesCount` | int32 (`ref`) | `8` | Help describes leakage risk when no-particle simulation instances consume more than a configured memory threshold **or** their count exceeds a configured count threshold. The raw help for this count CVar refers to both symbolic thresholds, so it does not isolate this variable's exact comparison by itself. | No read-like reference access was found; only an address-taking match appears in the scan. The paired memory threshold is a separate CVar and neither condition was traced here. |

## Evidence and editability limits

- All 25 names are `ref` entries in the community registry. Their types, help text, and captured values come from the registry and companion snapshot; that snapshot's game build and capture method are unknown.
- Eleven of the 25 names have read-like `ref_rva` candidates in the saved scan: the five grid controls, `IgnoreParentTickGroup`, and the five indirect-argument pool controls. The other 14 have only address-taking/setup references in this scan. A missing direct match does not prove the setting is unused; indirect or out-of-scope accesses can be missed.
- Read-like candidates prove only that instructions access the value storage in build `1.1.4042190`. No consumer path was reconstructed to prove an in-match outcome. No controlled `.ini` override, live console query, GPU profiling session, grid-format comparison, or pool-memory measurement was performed.
- Exact-name help/default matches in the Unreal Engine 5.9 reference are upstream context only. They do not prove Marvel Rivals uses that engine revision or that its startup configuration honors the CVar.

See the [community CVar registry](cvar-community-registry.md) for source help and exact upstream-name matches, [Niagara batch E](cvar-fx-niagara-batch-e.md) and [Niagara batch D](cvar-fx-niagara-batch-d.md) for adjacent settings, and the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis) for how to read the static scan.
