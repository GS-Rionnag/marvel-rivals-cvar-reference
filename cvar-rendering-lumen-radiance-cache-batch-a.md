# Lumen radiance-cache CVars: batch A

This page documents the 18 currently uncovered registered `r.Lumen.RadianceCache.*` variables. Registry help and captured values come from community attachments whose game build and capture method are unknown. The community registry also records exact-name matches to Epic's Unreal Engine 5.9 CVar reference for 17 of these names; upstream defaults and descriptions are comparison context, not proof of Marvel Rivals' live values or exact engine revision.

The build-specific evidence below comes from a static address scan of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate at a registered `ref_rva` shows an instruction reading or comparing the CVar storage. It does not establish that an override changes that storage, that a gated renderer path runs in a normal match, or that an observed visual effect follows.

## Cache update and trace selection

| Exact CVar | Type | Snapshot | UE 5.9 default | What the evidence supports | Build-specific evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.RadianceCache.ForceUniformTraceTileLevel` | int32 (`ref`) | `-1` | `-1` | For debugging, values `0`–`2` force a uniform trace-tile level and override BRDF-importance sampling: `0` half resolution, `1` full resolution, `2` supersampled. Negative values do not force a level according to the help; other negative values are unspecified. | A compare at `0x141D7D480` and integer load at `0x141D7E180` read the value. The mode branches and visual results were not traced. |
| `r.Lumen.RadianceCache.SortTraceTiles` | int32 (`ref`) | `0` | `0` | Help says whether trace tiles are sorted by direction before tracing to extract coherency. It does not define the sort key or quantify performance impact. | One direct comparison at `0x141D7ECC4` reads the value; the sorting routine and resulting work order were not reconstructed. |
| `r.Lumen.RadianceCache.Update` | int32 (`ref`) | `1` | `1` | Help describes whether the radiance cache is updated every frame. It does not describe behavior when disabled, deferred-update rules, or whether all cache work is affected. | One comparison at `0x141D797CE` checks the value against zero. The update loop and skipped work were not traced end to end. |

## Hardware ray tracing and temporary buffers

| Exact CVar | Type | Snapshot | UE 5.9 default | What the evidence supports | Build-specific evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.RadianceCache.HardwareRayTracing` | int32 (`var`) | `1` | `1` | Registry help says this enables hardware ray tracing for the Lumen radiance cache. The entry is a generic variable registration. Whether the game activates this path depends on renderer/platform conditions not established by the name or help. | `ref_rva` is absent; the saved scan found object/setup references only, not a direct read of the current value. No game-specific consumer was verified. |
| `r.Lumen.RadianceCache.HardwareRayTracing.Retrace.FarField` | int32 (`var`) | `1` | `1` | Help says this controls whether a second trace is fired for far-field contribution. It does not define distance, eligibility, or how far-field radiance is accumulated. | `ref_rva` is absent; setup/object-address matches do not demonstrate that the renderer reads this variable. |
| `r.Lumen.RadianceCache.HardwareRayTracing.TemporaryBufferAllocationDownsampleFactor` | int32 (`var`) | `8` | `8` | Help describes a downsample factor for the temporary buffer used by the hardware-ray-traced radiance cache. Higher values save transient allocator memory but may cause overflow and artifacts. The accepted range and buffer dimensions are not provided. | `ref_rva` is absent; no direct value read was matched. The memory-saving and artifact statements are community help, not a measurement in Rivals. |
| `r.Lumen.RadianceCache.TemporaryAtlasDownsampleFactor` | int32 (`var`) | — (not in snapshot) | — (no exact UE 5.9 match) | Help describes a downsample factor for the temporary buffer used for probe updates; higher factors may save transient allocator memory but risk overflow and artifacts. The help does not specify accepted values or how this atlas differs from the hardware-ray-tracing temporary buffer above. | `ref_rva` is absent and the address scan found setup/object references only. Runtime consumption is unconfirmed. |

## Probe retention, filtering, and supersampling

| Exact CVar | Type | Snapshot | UE 5.9 default | What the evidence supports | Build-specific evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.RadianceCache.NumFramesToKeepCachedProbes` | int32 (`var`) | `8` | `8` | Help says this is how many frames unused probes remain in the cache. More retention may increase reuse between frames; too much can leave stale probes that filter into lighting. The cache eviction policy and effective range are unspecified. | `ref_rva` is absent; setup/object-address matches do not prove a value read in the current build. |
| `r.Lumen.RadianceCache.SpatialFilterMaxRadianceHitAngle` | float (`ref`) | `0.2` | `0.2` | Help gives degrees and says larger angles allow filtering nearby features but increase leaking. The compared direction vectors and exact filter formula are not described. | A scalar load at `0x141D7FBE6` reads the value. The filter math and resulting light leak were not tested. |
| `r.Lumen.RadianceCache.SpatialFilterProbes` | int32 (`ref`) | `1` | `1` | Help says whether probe radiance is filtered between neighbors. It does not define the neighborhood, filter kernel, or disabled-path fallback. | A direct compare at `0x141D798AB` reads the value; no filter implementation was reconstructed from that site. |
| `r.Lumen.RadianceCache.SupersampleDistanceFromCamera` | float (`ref`) | `2000` | `2000` | Help says only probes closer to the camera than this distance can be supersampled. It does not define the units or whether other selection conditions also apply. | Three scalar loads at `0x141D7BC9D`, `0x141D7C645`, and `0x141D7E15E` read the value. Exact distance comparisons and selection logic were not fully traced. |
| `r.Lumen.RadianceCache.SupersampleTileBRDFThreshold` | float (`ref`) | `0.1` | `0.1` | Help says probes receive more rays for supersampling when BRDF value is above this threshold, within the stated `0`–`1` BRDF range. It does not detail clamping or material inputs. | A scalar load at `0x141D7E151` reads the value. No BRDF calculation or resulting ray count was confirmed. |

## Diagnostics and visualization

| Exact CVar | Type | Snapshot | UE 5.9 default | What the evidence supports | Build-specific evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.RadianceCache.OverrideCacheOcclusionLighting` | int32 (`ref`) | `0` | `0` | No help is supplied. The name suggests a cache-occlusion lighting override but does not reveal the selected value, visual meaning, or activation conditions. | One integer load at `0x141D5F8B4` reads the value. Its consuming path was not reconstructed, so the name-based interpretation remains unverified. |
| `r.Lumen.RadianceCache.ShowBlackRadianceCacheLighting` | int32 (`ref`) | `0` | `0` | No help is supplied. The name may refer to a diagnostic rendering mode, but it does not define what is blackened or how to enable/filter the display. | One integer load at `0x141D5F8C1` reads the value. The visual/debug branch was not traced; this does not prove a usable visualization appears in Shipping. |
| `r.Lumen.RadianceCache.Visualize` | int32 (`ref`) | `0` | `0` | No help is supplied. The name indicates a radiance-cache visualization control but does not identify what is visualized or the mode mapping. | One compare at `0x141E52E7C` reads the value. The output path and display conditions were not traced. |
| `r.Lumen.RadianceCache.VisualizeClipmapIndex` | int32 (`ref`) | `-1` | `-1` | Help says it selects which radiance-cache clipmap to visualize, with `-1` selecting all clipmaps at once. Other negative values and out-of-range indices are unspecified. | A comparison at `0x141E52F3C` and conditional move at `0x141E52F42` access the value. The selection bounds and visual result were not independently verified. |
| `r.Lumen.RadianceCache.VisualizeProbeRadius` | int32 (`ref`) | `0` | `0` | Help says this controls whether radiance-cache probe radius is visualized. It does not specify how the radius is drawn or how this switch interacts with `Visualize`. | The address scan found an address-taking reference but no direct `ref_rva` value-read candidate. The current build's consumer path is therefore unconfirmed by this scan. |
| `r.Lumen.RadianceCache.VisualizeRadiusScale` | float (`ref`) | `0.05` | `0.05` | Help says it scales the sizes of spheres used to visualize radiance-cache samples. It does not specify the base radius or accepted range. | One scalar load at `0x141E52FC4` reads the value. The draw code and visual scale were not tested. |

## What this establishes about edits

Twelve entries have at least one direct-memory candidate at their `ref_rva`. Six entries have no direct value-read match: the five `var` registrations (`HardwareRayTracing`, `HardwareRayTracing.Retrace.FarField`, `HardwareRayTracing.TemporaryBufferAllocationDownsampleFactor`, `NumFramesToKeepCachedProbes`, and `TemporaryAtlasDownsampleFactor`) and `VisualizeProbeRadius` (`ref`), which has an address-taking match only. The value-read candidates show static access in this build; they do not prove that a startup INI override is accepted, survives later config layers, or changes the visible renderer.

The community snapshot equals the listed Epic 5.9 defaults for the 17 exact-name matches, but the snapshot build is unknown. Do not treat that agreement as Marvel Rivals' live defaults. `TemporaryAtlasDownsampleFactor` is described in the community help but is absent from the snapshot and has no exact Epic 5.9 match in the registry cross-reference.

No controlled override, runtime console query, or in-game visual/performance comparison was performed for this batch. The visualization controls may be diagnostic and may not be exposed in a normal Shipping session. The hardware-ray-tracing controls also do not prove that a particular device or game configuration takes that rendering path.

## Evidence and related guides

- Registry names, types, community help, snapshot values, and exact-name Unreal 5.9 comparisons: [community CVar registry](cvar-community-registry.md) and the preserved [community registry and snapshot sources](EVIDENCE.md#community-sources).
- Direct-memory candidates and their scope: [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). Address-level matches are static evidence, not an end-to-end renderer trace.
- Related Lumen settings: [Lumen global-illumination CVars, batch A](cvar-rendering-lumen-batch-a.md), [Lumen hardware-ray-tracing and irradiance-field CVars, batch B](cvar-rendering-lumen-batch-b.md), and [CVar override/editability notes](cvar-overrides.md).
- Upstream reference: [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference). Its entries are upstream context and do not establish Marvel Rivals' Unreal revision.
