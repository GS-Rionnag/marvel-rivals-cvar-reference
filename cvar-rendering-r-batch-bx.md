# GPU rendering CVars: volumetric clouds and fog (batch BX)

This guide documents the next 25 currently uncovered unique `r.*` registry names after batch BW: ten cloud controls and 15 volumetric-fog controls. Duplicate source rows are counted once by exact CVar name. Supplied community help is summarized below; blank or vague descriptions remain limited to what the text actually says.

Community help and captured values do not prove live-game implementation or `.ini` acceptance. Snapshot values are observations, not defaults or recommendations. Epic UE 5.9 reference values were not supplied for this batch. Static address-reference hits in Shipping build 1.1.4042190 are candidates only, not proof of runtime reads, writes, execution, or visible effects.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build scan evidence and limits |
| --- | --- | --- | --- | --- |
| `r.VolumetricCloud.ShadowMap.TemporalFiltering.NewFrameWeight` | `float` (`var`) | `1` | Experimental temporal-filter contribution weight from the current frame, described as a value from 0 to 1. The help warns that low values can impair depth convergence and says the feature is disabled at 1. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO` | `int32` (`var`) | `1` | Enables cloud sky ambient occlusion; requires a Skylight with Cloud Ambient Occlusion enabled. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO.Debug` | `int32` (`var`) | `0` | Prints information about the cloud sky-AO map. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO.Filtering` | `int32` (`var`) | `1` | Enables or disables the sky-AO dilation/smoothing filter. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO.MaxResolution` | `int32` (`var`) | `2048` | Maximum texture resolution for sky-light ambient-occlusion data. The active resolution is also controlled by the Skylight component's `CloudAmbientOcclusionMapResolutionScale` property. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO.SnapLength` | `float` (`var`) | `20` | Cloud sky-AO texture-position snapping size, in kilometers, intended to avoid flicker. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SkyAO.TraceSampleCount` | `int32` (`var`) | `10` | Number of samples used to evaluate ground-lighting occlusion. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.SoftBlendingDistanceOnTranslucent` | `float` (`var`) | `0.5` | Distance in kilometers used to soften cloud blending over translucent objects, measured from the evaluated start depth. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.StepSizeOnZeroConservativeDensity` | `int32` (`var`) | `1` | Ray-march step size used after a sample has zero conservative density. The help says values above 1 may improve performance but can cause banding when too large. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricCloud.ViewRaySampleMaxCount` | `float` (`var`) | `768` | Maximum samples taken while ray marching primary view rays. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `r.VolumetricFog.AllowSDFMultiView` | `int32` (`ref`) | `1` | Whether volumetric-fog SDF features are allowed with multiple views; 0 retains the legacy single-view restriction. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.ConservativeDepth` | `int32` (`ref`) | `0` | Experimental option to allow conservative depth for accelerating volumetric computations. The exact acceleration path is unspecified. | 5 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.DepthDistributionScale` | `float` (`ref`) | `32` | Scales the depth distribution of volumetric-fog slices. | 3 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.Emissive` | `int32` (`ref`) | `1` | Whether volumetric fog's emissive component is allowed. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.EnableDirectionalLight` | `int32` (`ref`) | `0` | Whether a directional light can affect volumetric fog. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.GridPixelSize` | `int32` (`ref`) | `16` | XY size of a volumetric-fog voxel-grid cell, in pixels. | 8 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.GridSizeZ` | `int32` (`ref`) | `32` | Number of volumetric-fog grid cells along Z. | 5 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.HistoryMissSupersampleCount` | `int32` (`ref`) | `4` | Lighting samples used for voxels without a history value. Help gives range 1–16, says it can reduce noise during panning or camera cuts, and notes variable computation cost. | 10 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.HistoryWeight` | `float` (`ref`) | `0.9` | Weight applied to the previous history value each frame; help describes a tradeoff between visible jitter and responsiveness. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.IgnoreMaskBox` | `bool` (`ref`) | `false` | Help only says “VolumetricFog Ignore MaskBox”; it does not define the mask-box behavior. | 2 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.InjectRaytracedLights` | `int32` (`ref`) | `0` | Whether lights with ray-traced shadows are injected into volumetric fog. | 5 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.InjectShadowedLightsSeparately` | `int32` (`ref`) | `1` | Help says “whether to allow the volumetric fog feature,” but does not explain what is injected separately. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.InverseSquaredLightDistanceBiasScale` | `float` (`ref`) | `1` | Scales the bias added to an inverse-square falloff denominator; help says this can remove a spike that causes extreme aliasing. | 2 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.Jitter` | `int32` (`ref`) | `1` | Whether to jitter volumetric-fog computation each frame for temporal supersampling. | 3 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `r.VolumetricFog.LightFunction` | `int32` (`ref`) | `1` | Whether light functions are generated for sampling during volumetric-fog rendering. | 5 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |

## Interpretation and limits

- These names describe renderer settings and do not establish that every path is active in Marvel Rivals or that a player-facing option controls them.
- Values shown are captured snapshot values, not recommendations or verified defaults for the current game build.
- `var`/`ref` classifications and static scanner matches are not evidence that a startup `[Overrides]` line changes the running game.
- Scanner address candidates can include initialization and address passing. They do not establish executed runtime reads/writes or visible effect.

## Sources

Names, types, supplied help, and snapshots are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner methodology are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
