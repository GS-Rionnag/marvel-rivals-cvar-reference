# Lumen Screen Probe filtering and AO CVar batch G

This guide covers the next 25 uncovered registered `r.Lumen.ScreenProbeGather.*` names in source-registry order. Community help and snapshot values are reproduced as evidence, not recommendations. The registry does not identify its game build or capture method. An exact-name Epic 5.9 match provides upstream context; it does not prove Marvel Rivals uses that engine revision or default.

Build evidence is from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate points at a registered reference address but can be a read, comparison, or write; a CVar-object reference can be setup code. Neither proves the path executes in a match. No controlled `.ini` override, live CVar query, or in-game A/B test was performed.

## Short-range AO and hair tracing

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.DownsampleFactor` | int32 (`var`) | `1` | `—` | Downsampling factor for ShortRangeAO. | The scan found CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value reads were not established. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.HairScreenTrace` | int32 (`ref`) | `0` | `0` | Whether to trace against hair depth for hair casting shadow onto opaques. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.HairVoxelTrace` | int32 (`ref`) | `1` | `1` | Whether to trace against hair voxel structure for hair casting shadow onto opaques. | 4 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.HardwareRayTracing` | int32 (`var`) | `0` | `0` | 0. Screen space tracing for the full resolution Bent Normal (directional occlusion).1. Enable hardware ray tracing of the full resolution Bent Normal (directional occlusion). (Default) | The scan found CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value reads were not established. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.HardwareRayTracing.NormalBias` | float (`var`) | `0.1` | `0.1` | Bias for HWRT Bent Normal to avoid self intersection | The scan found CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value reads were not established. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.MaxMultibounceAlbedo` | float (`ref`) | `0.5` | `0.5` | Maximum albedo used for the AO multi-bounce approximation.  Useful for forcing near-white albedo to have some occlusion. | 5 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.ScreenSpace.FoliageOcclusionStrength` | float (`ref`) | `0.7` | `0.7` | Maximum strength of ScreenSpaceBentNormal occlusion on foliage and subsurface pixels.  Useful for reducing max occlusion to simulate subsurface scattering. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.ScreenSpace.SlopeCompareToleranceScale` | float (`ref`) | `0.5` | `0.5` | Scales the slope threshold that screen space traces use to determine whether there was a hit. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.Temporal` | int32 (`var`) | `1` | `—` | Whether to run temporal accumulation on Short Range AO | The scan found CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value reads were not established. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO.Temporal.NeighborhoodClampScale` | float (`var`) | `1` | `—` | Scales how permissive is neighborhood clamp. Higher values increase ghosting, but reduce noise and instability. Values <= 0 will disable neighborhood clamp. | The scan found CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value reads were not established. |

## Spatial filtering and probe interpolation

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.ScreenProbeGather.SpatialFilterHalfKernelSize` | int32 (`ref`) | `1` | `1` | Experimental | 4 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.SpatialFilterMaxRadianceHitAngle` | float (`ref`) | `10` | `10` | In Degrees.  Larger angles allow more filtering but lose contact shadows. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.SpatialFilterNumPasses` | int32 (`ref`) | `3` | `3` | Number of spatial filter passes | 4 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.SpatialFilterPositionWeightScale` | float (`ref`) | `1000` | `1000` | Determines how far probes can be in world space while still filtering lighting | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.SpatialFilterProbes` | int32 (`ref`) | `1` | `1` | Whether to spatially filter probe traces to reduce noise. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.StochasticInterpolation` | int32 (`ref`) | `0` | `0` | Where to interpolate screen probes stochastically (1 sample) or bilinearly (4 samples) | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |

## Temporal filtering and history rejection

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.ScreenProbeGather.Temporal` | int32 (`ref`) | `1` | `1` | Whether to use a temporal filter | 4 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.ClearHistoryEveryFrame` | int32 (`ref`) | `0` | `0` | Whether to clear the history every frame for debugging | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.DebugForceTracesMoving` | int32 (`ref`) | `0` | `0` | No help text was supplied. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.DistanceThreshold` | float (`ref`) | `0.005` | `0.005` | Relative distance threshold needed to discard last frame's lighting results.  Lower values reduce ghosting from characters when near a wall but increase flickering artifacts. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.FastUpdateModeUseNeighborhoodClamp` | int32 (`ref`) | `0` | `0` | Whether to clamp history values to the current frame's screen space neighborhood, in areas around moving objects. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.FractionOfLightingMovingForFastUpdateMode` | float (`ref`) | `0.1` | `0.1` | No help text was supplied. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.MaxFastUpdateModeAmount` | float (`ref`) | `0.9` | `0.9` | Maximum amount of fast-responding temporal filter to use when traces hit a moving object.  Values closer to 1 cause more noise, but also faster reaction to scene changes. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.MaxFramesAccumulated` | float (`ref`) | `30` | `10` | Lower values cause the temporal filter to propagate lighting changes faster, but also increase flickering from noise. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |
| `r.Lumen.ScreenProbeGather.Temporal.NormalThreshold` | float (`ref`) | `45` | `45` | Maximum angle that the history texel's normal can be from the current pixel to accept it's history lighting, in degrees. | 3 direct-memory candidate(s) and 2 address-taken reference(s); instruction context and runtime use were not traced. |

## Reading the values

- Snapshot numbers are values from the community capture; they are not guaranteed defaults or safe recommendations. This batch includes an upstream/snapshot difference for `r.Lumen.ScreenProbeGather.Temporal.MaxFramesAccumulated` (snapshot `30`, Epic 5.9 default `10`).
- Rows without an Epic 5.9 match show `—`; their explanations come from supplied community help only.
- The help describes intended effects and tradeoffs for AO, hair visibility in traces, spatial denoising, interpolation, and temporal history. It does not establish the game’s active rendering path, accepted runtime ranges, performance costs, or whether this mod loader applies a given override.
- Address-scan counts are static references, not measured runtime reads. Values were not changed in a controlled match.

For adjacent settings, see [Lumen batches A–F](cvar-rendering-lumen-batch-a.md), [Lumen Radiance Cache](cvar-rendering-lumen-radiance-cache-batch-a.md), and [Lumen reflections](cvar-rendering-lumen-reflections-batch-a.md). The registry method is in the [community CVar registry](cvar-community-registry.md); build scan scope is summarized in [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).

