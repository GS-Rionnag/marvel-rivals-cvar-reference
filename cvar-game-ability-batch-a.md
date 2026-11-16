# Game-specific visual ability CVars: batch A

This page covers the 15 remaining `m.ability.*` entries in the supplied community registry. They cluster around a shared visual-mesh-clone path and afterimage effects. Registry help gives a concrete shared-path requirement and partial descriptions for the afterimage controls; it does not establish the full rendering implementation or identify most numeric IDs with a hero. `m.ability.106172` is explicitly labeled as Black Cat in the registry. Do not infer mappings for the other IDs from these names alone.

Snapshot values below are observations from an attachment with unknown build and collection method. They are not confirmed defaults. Three `CaptainShadow` settings are absent from that snapshot.

## Per-ability visual mesh clone opt-ins

The shared registry help says these ability-specific booleans opt into a shared visual mesh-clone layer and require the global `m.VisualMeshClone.Enable` switch. The broader override notes describe the global switch as gating the shared layer and say ability paths fall back to legacy behavior while it is disabled. That relationship comes from embedded help and is not an in-game test. The saved address scan found each name and an object/setup reference, but no direct value-read candidate for these `var` entries.

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `m.ability.101871.UseVisualMeshCloneLayer` | bool (`var`) | `true` | Ability-level opt-in for the shared visual mesh-clone layer; requires `m.VisualMeshClone.Enable`. No hero mapping is stated in this source row. | The name is present in the build's string inventory and has object-address setup matches. There is no matched `ref_rva` read showing the opt-in being consumed. |
| `m.ability.102181.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.102251.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.103651.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.104321.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.104931.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.104981.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.105071.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.105461.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Same opt-in and global prerequisite. | String and object-address setup matches only; no direct value-read candidate. |
| `m.ability.106172.UseVisualMeshCloneLayer` | bool (`var`) | `false` | Ability-level opt-in for Black Cat 106172 to use the shared visual mesh-clone layer; requires the global switch. | Black Cat is identified in the registry help. The build scan has string and object-address setup matches, but no direct value-read candidate for this `var` entry. |
| `m.ability.102181.DebugAfterImageLog` | bool (`ref`) | `false` | Unreviewed translation of registry help: when enabled, prints debug information such as skeletal positions used to fit an afterimage capsule and its `SpawnLocation`; source says off by default. It does not identify the output destination or logging frequency. | Two direct byte-comparison candidates read the reference in build 4042190. These show value checks, not the complete logging path or whether the output is reachable in normal play. |
| `m.ability.102181.DebugCapsuleDrawTime` | float (`ref`) | `5` | Unreviewed translation: lifetime, in seconds, for drawing the debug afterimage capsule; source help states `5.0` as default. | One direct float-load candidate reads the reference. The drawing API, accepted range, and visible lifetime were not tested. |

## CaptainShadow afterimage update controls

The three Chinese descriptions were translated for the research catalog and have not been independently reviewed. They describe reducing repeated material-parameter writes by comparing new values with prior values and, when the tick optimization is enabled, caching material-instance targets instead of traversing every slot each frame. This is a coherent reading of the supplied help, but the precise cache lifecycle and material-update implementation have not been independently reconstructed.

| Exact CVar | Type | Snapshot | What the translated registry help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `m.ability.CaptainShadow.MovePosTolerance` | float (`ref`) | — (not in snapshot) | Change-detection tolerance in centimeters for afterimage movement-position material parameters; a smaller difference skips that material write. The exact vector comparison rule is unspecified. | One direct float-load candidate reads the reference in build 4042190. The consuming comparison and its relation to visible movement were not traced. |
| `m.ability.CaptainShadow.OpacityTolerance` | float (`ref`) | — (not in snapshot) | Change-detection tolerance for afterimage opacity material parameters; a smaller difference skips that write. Units and comparison/clamping behavior are not stated. | One direct float-comparison candidate reads the reference. It does not establish the parameter's range or appearance change. |
| `m.ability.CaptainShadow.OptimizeTick` | bool (`ref`) | — (not in snapshot) | Translated help says `1` (stated default) caches direct writes to target material instances and applies change detection; `0` restores traversal and writing of every slot each frame. | Two direct byte-comparison candidates read the reference. The toggle's full branch behavior and performance effect were not measured. |

## What the evidence establishes

- The community registry classifies all 15 names as `var` or `ref`. Its snapshot contains values for the 12 visual-mesh and `102181` entries; it has no captured values for the three `CaptainShadow` entries.
- The build 1.1.4042190 scan has direct reference-value candidates for the two `102181` debug controls and all three `CaptainShadow` controls. It has only object/setup-address matches for the ten visual-mesh `var` entries. String presence and object setup do not prove a CVar's current value is read by the runtime feature.
- The Chinese descriptions are assistant translations marked unreviewed in the research catalog. Treat the translated details as provisional until checked against a fluent source review or the implementation.
- None of this proves that a particular startup `.ini` override is accepted, that values survive other config layers, or that a visible change occurs in a live match. No controlled override comparison was run for this batch.

For the global visual-mesh-clone prerequisite and other embedded name/help candidates, see [CVar override research](cvar-overrides.md). For the address-scan method and its limitations, see [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis) and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). The registry and snapshot provenance are summarized in [community registry and snapshot sources](EVIDENCE.md).
