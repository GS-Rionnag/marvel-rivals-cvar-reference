# Foliage console variables in build 4042190

This guide follows the community registry author's suggestion to search the attached registry for “foliage.” It covers the 22 `foliage.*` variables and six `foliage.*` console commands. All 28 names occur as printable strings in the installed x64 and ARM64EC Shipping executables, and the 22 variables match Epic's UE 5.9 reference table. A string match and upstream description are good leads, but do not prove the Marvel fork's exact runtime behavior or that override loader permits a particular override.

The Discord registry attachment has a `var` row and type for each variable. `CVarDump.txt` contains captured values for all 22; its source does not say whether they were live values, defaults, or overrides. They are listed as a snapshot only. In particular, `foliage.CullDistanceScale` and `foliage.DensityScale` are `0` in the snapshot while Epic UE 5.9 lists `1` as the reference default. Do not treat that mismatch as proof that Marvel's default is zero.

## Variables

| CVar | Type | Snapshot value | Meaning from registry / UE 5.9 reference |
| --- | --- | ---: | --- |
| `foliage.CullAll` | int32 | `0` | Above zero, treat all foliage as culled. |
| `foliage.CullAllInVertexShader` | int32 | `0` | Debug switch that culls all instances in the vertex shader when above zero. |
| `foliage.CullDistanceScale` | float | `0` | Scales foliage cull distance; only applies to foliage types that opt in. Epic reference default: `1`. |
| `foliage.DensityScale` | float | `0` | Scales the amount rendered; only applies to foliage types that opt in. Epic reference default: `1`. |
| `foliage.DisableCull` | int32 | `0` | Above zero, disables frustum-based culling. |
| `foliage.DiscardDataOnLoad` | int32 | `0` | With `1`, discard foliage data on load when the foliage type enables that behavior; requires reloading the level. |
| `foliage.DitheredLOD` | int32 | `1` | Above zero uses dithered LOD transitions; otherwise LODs pop. |
| `foliage.ForceLOD` | int32 | `-1` | A value at least zero forces that foliage LOD. Epic reference default: `-1`. |
| `foliage.InstanceRuns` | int32 | `0` | Enables InstanceRuns compression for foliage draw-call data; unsupported by the Mesh Draw Command pipeline. |
| `foliage.LODDistanceScale` | float | `1` | Scales distance used to choose foliage LOD. |
| `foliage.MaxEndCullDistance` | int32 | `0` | Maximum end-culling distance; zero disables this limit. |
| `foliage.MaxOcclusionQueriesPerComponent` | int32 | `16` | Upper bound controlling occlusion-query granularity; registry says 16–128 is a reasonable range. |
| `foliage.MaxTrianglesToRender` | int32 | `100000000` | Absolute foliage-triangle limit per traversal, intended to protect against extreme LOD settings. |
| `foliage.MinInstancesPerOcclusionQuery` | int32 | `256` | Controls occlusion-query granularity; registry suggests 1,024–65,536, with an approximate boundary. |
| `foliage.MinLOD` | int32 | `-1` | Discards top LODs for performance evaluation; `-1` disables this CVar's effects. |
| `foliage.MinOcclusionQueriesPerComponent` | int32 | `6` | Controls occlusion-query granularity; registry says 2 is the minimum. |
| `foliage.MinVertsToSplitNode` | int32 | `8192` | Tunes the accuracy/performance tradeoff for foliage culling and LOD. |
| `foliage.MinimumScreenSize` | float | `5e-06` | Screen-size threshold below which foliage instances are culled entirely. |
| `foliage.OnlyLOD` | int32 | `-1` | A value at least zero renders only that foliage LOD. |
| `foliage.OverestimateLOD` | int32 | `0` | When positive and dithered LOD is off, uses an overestimate instead of an underestimate for LOD. |
| `foliage.RandomLODRange` | float | `0` | Adds a random distance offset per instance when computing LOD. |
| `foliage.SplitFactor` | int32 | `16` | Controls the branching factor of the foliage tree. |

The likely foliage-removal controls from their descriptions are `foliage.CullAll` and `foliage.CullAllInVertexShader`; `foliage.DensityScale` may reduce rendered foliage where the foliage type opts in. The registry does not show whether Marvel Rivals' map vegetation uses these foliage paths, whether non-foliage static meshes are affected, or whether the loader accepts them. The supplied loader notes that settings capable of removing smoke or other effects are ignored, so loader acceptance and in-game effect remain unverified. This guide does not recommend values based on the snapshot.

## What the local build confirms

The installed 1.1.4042190 Shipping executable has exact-name strings for all 22 variables, and all 22 `obj_rva` values match direct RIP-relative code references in the address-reference scan. Those hits establish that the community object addresses overlap code references in this build; they do not by themselves show the render-side read. For example, the `foliage.CullAll` hits at `0x140A50AB3` and `0x140A50B24` initialize its object slot and take that object's address for an internal list path. That sequence is registration scaffolding, not evidence of the cull decision itself. The full scan is in [the preserved address-hit table](EVIDENCE.md#evidence-artifacts-not-included). No user-visible game test is recorded here, so whether Marvel Rivals maps actually render through these foliage systems and whether override loader accepts the removal controls remain open.

## Related console commands

These six entries have `kind=cmd`, not `kind=var`; they are not persistent `[Overrides]` assignments:

| Command | Registry help |
| --- | --- |
| `foliage.Freeze` | Freezes foliage culling and LOD for debugging. |
| `foliage.LogFoliageFrame` | Logs all foliage rendered in a frame. |
| `foliage.RebuildFoliageTrees` | Rebuilds trees for non-grass foliage. |
| `foliage.Test` | Marked useful for debugging; no further description. |
| `foliage.ToggleVectorCull` | Toggles the optimized cull for debugging. |
| `foliage.UnFreeze` | Registry repeats the `Freeze` help (“Freezes the foliage culling and LOD”), which conflicts with this command's name; behavior is not confirmed here. |

## Evidence and limits

- The [registry attachment](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) classifies the 22 variables and provides the quoted help; the [object table](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) repeats help for most entries.
- The [snapshot attachment](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452) contains the values in the table, but its capture procedure and provenance are unknown.
- The [build string inventory](EVIDENCE.md#build-specific-static-analysis) records exact name strings in both local Shipping executables and matching UE 5.9 reference descriptions/defaults. It does not establish runtime registration or effect.
- In the user's override loader config format, ordinary `[Overrides]` entries are applied by the loader according to the supplied loader notes; its policy excludes settings that can remove smoke or other effects. Whether that policy blocks these foliage controls has not been tested.

Related guides: [CVar registration evidence](cvar-registration-evidence-4042190.md), [community CVar registry](cvar-community-registry.md), [CVar overrides and loader syntax](cvar-overrides.md), and [preserved source attachments](EVIDENCE.md#build-specific-static-analysis).
