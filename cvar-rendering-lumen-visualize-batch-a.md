# Lumen visualization CVar batch I

This batch documents the first 25 uncovered registered `r.Lumen.Visualize.*` variables in registry order. It includes surface-cache/card placement diagnostics and hardware-ray-tracing visualization controls. The community dump is not build-tagged; exact Epic UE 5.9 name matches are upstream references, not proof of the game’s engine version, active path, or runtime values.

Build evidence comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may be a read, comparison, or write. A `var` address match can be registration/setup rather than a value read. No instruction trace, override test, live query, or gameplay A/B was performed.

## Card, cone, and surface visualization

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.Visualize.CardGenerationCluster` | int32 (`ref`) | `0` | `0` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 5 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardGenerationClusterScale` | float (`ref`) | `1` | `1` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardGenerationMaxSurfel` | int32 (`ref`) | `-1` | `-1` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 4 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardGenerationSurfelScale` | float (`ref`) | `1` | `1` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardGenerationSurfels` | int32 (`ref`) | `0` | `0` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 6 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardInterpolateInfluenceRadius` | float (`ref`) | `10` | `10` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacement` | int32 (`ref`) | `0` | `0` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 4 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacementDirection` | int32 (`ref`) | `-1` | `-1` | Visualize only a single card direction. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacementDistance` | float (`ref`) | `5000` | `5000` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 5 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacementIndex` | int32 (`ref`) | `-1` | `-1` | Visualize only a single card per mesh. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacementLOD` | int32 (`ref`) | `0` | `0` | 0 - all 1 - only primitives 2 - only merged instances 3 - only merged components 4 - only far field *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.CardPlacementPrimitives` | int32 (`ref`) | `0` | `0` | Whether to visualize primitive bounding boxes. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.ConeAngle` | float (`ref`) | `0` | `0` | Visualize cone angle, in degrees. *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.ConeStepFactor` | float (`ref`) | `2` | `2` | Cone step scale on sphere radius step size. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.GridPixelSize` | int32 (`ref`) | `32` | `32` | No explanatory help was supplied; exact effect remains undocumented in the available references. *(source: not described)* | 4 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |
| `r.Lumen.Visualize.HiResSurface` | int32 (`ref`) | `1` | `1` | Whether visualization should sample highest available surface data or use lowest res always resident pages. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); read/write direction and control flow were not traced. |

## Hardware ray-tracing visualization controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.Lumen.Visualize.HardwareRayTracing` | int32 (`var`) | `1` | `1` | Enables visualization of hardware ray tracing (Default = 1) *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.BucketMaterials` | int32 (`var`) | `1` | `1` | Determines whether a secondary traces will be bucketed for coherent material access (default = 1 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.Compact` | int32 (`var`) | `1` | `1` | Determines whether a second trace will be compacted before traversal (default = 1 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.DeferredMaterial` | int32 (`var`) | `1` | `1` | Enables deferred material pipeline (Default = 1) *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.DeferredMaterial.TileDimension` | int32 (`var`) | `64` | `64` | Determines the tile dimension for material sorting (Default = 64) *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.GroupCount` | int32 (`var`) | `4096` | `4096` | Determines the active group count when dispatching raygen shader (default = 4096 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.Retrace.FarField` | int32 (`var`) | `1` | `1` | Determines whether a second trace will be fired for far-field contribution (default = 1 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.Retrace.HitLighting` | int32 (`var`) | `0` | `0` | Determines whether a second trace will be fired for hit-lighting for invalid surface-cache hits (default = 1 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |
| `r.Lumen.Visualize.HardwareRayTracing.ThreadCount` | int32 (`var`) | `64` | `64` | Determines the active group count when dispatching raygen shader (default = 64 *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value consumption was not established. |

## Practical scope

- These names and descriptions are for Lumen visualization/debug controls. Their presence in the registry does not show that a visualization mode is enabled or reachable in the retail client.
- Several rows have no help text in either supplied community help or the Epic 5.9 reference. Those are explicitly marked as undocumented; the name alone is not treated as proof of a setting’s exact behavior.
- Snapshot values are captured values, not recommendations. Epic 5.9 defaults appear separately when there is an exact upstream match.
- Static reference counts do not measure runtime execution or whether the mod loader honors a `.ini` override.

For neighboring controls, see the [Lumen guide index](README.md) and [community CVar registry](cvar-community-registry.md). The raw build scan is summarized in the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
