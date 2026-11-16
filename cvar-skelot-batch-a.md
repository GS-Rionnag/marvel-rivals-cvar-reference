# Skelot CVar batch A

This guide documents the 12 currently uncovered, exact-case lower-case `skelot.*` `var`/`ref` entries. Their supplied help covers shadow suppression, distance-based LOD, animation frame selection, bone-influence and triangle-count limits; several culling and drawing names lack usable descriptions. One other registry entry in this family is covered elsewhere and is not repeated here.

No exact-name Epic UE 5.9 CVar entry was found for these 12 names. Snapshot values are observations, not defaults. The local Shipping-build scan matches address fields from the community registry; direct-memory candidates do not prove a value read, write, or runtime effect. No `.ini` override or in-game behavior was tested.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `skelot.DisableFrustumCull` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 4 direct-memory candidates and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.DisableGridCull` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.DisableSectionsUnification` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.DisableShadow` | `int32` (`var`) | — | — | Supplied help: disable shadow casting for all Skelot components across all worlds. `0` preserves component and mesh shadow settings; `1` disables shadow casting. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `skelot.DistanceScale` | `float` (`ref`) | `1` | — | Supplied help: scale used for distance-based LOD; a higher value results in a “higher LOD.” The help does not clarify the detail convention or affected distance calculation. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.DrawCells` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; the exact display and scope remain unresolved. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.DrawInstanceBounds` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; the exact display and scope remain unresolved. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.ForcedAnimFrameIndex` | `int32` (`ref`) | `-1` | — | Supplied help: force all instances to use the specified animation frame index; `-1` disables the override. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.FroceMaxBoneInfluence` | `int32` (`ref`) | `-1` | — | Supplied help: limit `MaxBoneInfluence` for all instances; `-1` disables the limit. The spelling `Froce` is preserved exactly from the registry. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.MaxTrianglePerInstance` | `int32` (`ref`) | `-1` | — | Supplied help: limit triangles per instance for debug/profile purposes; values at or below `0` disable the limit. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.NumInstancePerGridCell` | `int32` (`ref`) | `256` | — | No useful supplied help or exact-name Epic description; the name does not establish cell sizing or behavior. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `skelot.ShadowForceLOD` | `int32` (`ref`) | `-1` | — | No useful supplied help or exact-name Epic description; the meaning of `-1` and the LOD selection behavior remain unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The documented shadow, animation-frame, bone-influence, and triangle-limit descriptions are supplied help, not verification that the installed game registers or honors the settings.
- `DisableFrustumCull` and `DisableGridCull` suggest broad changes to visibility/selection work by name, but no supplied description defines their relationship to instance rendering or performance.
- `DrawCells` and `DrawInstanceBounds` look like visualization controls by name, but their draw target, timing, and shipping behavior are not described.
- `DistanceScale` says higher values give “higher LOD,” without defining whether that means more detail or a larger LOD index.
- Static address candidates are not function-level proof. Registry presence and snapshot values do not establish that the mod loader accepts these entries in startup `.ini` overrides.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), and [snapshot and address-reference scan provenance](EVIDENCE.md#community-sources).
