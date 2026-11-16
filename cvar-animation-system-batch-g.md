# Animation system CVar batch G

This page documents the 22 remaining `a.*` variable rows in this coverage pass. They include update-rate optimization (URO), streamed-animation diagnostics, skeletal-mesh LOD visualization, a curve-evaluation switch, and game-specific SpiderDes settings. The table uses the community registry's descriptions and captured `CVarDump.txt` values. The snapshot build and collection method are unknown, so captured values are observations, not verified defaults or recommendations.

The build-specific scan targets Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate against `ref_rva` means an instruction accesses the stored value; it does not reveal the entire branch or prove that a startup `.ini` override is accepted. Object-address/setup matches for `var` entries do not establish that runtime code reads the current value.

## Subgraph, pose, and streamed-animation controls

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `a.SkipSubGraph.Enable` | bool (`ref`) | `true` | When true, `SubAnimInstances` are skipped according to conditions. The conditions and fallback evaluation are not specified. | One direct comparison candidate reads the value at `0x14376BC01`; the qualifying conditions and affected graphs were not traced. |
| `a.SlotEvaluatePoseOptimize.Enable` | int32 (`var`) | `1` | Help only says it is used in `AnimNode_Slot`. It does not describe the optimization, integer modes, or pose differences. | Name/help are present in the build's nearby-text inventory, and the registry supplies only an object address. No direct value read was established. |
| `a.Streaming.SpoofFailedChunkLoad` | int32 (`ref`) | `0` | Forces streamed animation chunks to fail loading; help maps `0` to disabled and `1` to enabled. This is a failure-injection control, not a quality setting. | One comparison candidate reads the value at `0x14371A01E`. The chunk-loading branch was not traced; enabling it may deliberately break animation chunk loading. |
| `a.StripAdditiveRefPose` | int32 (`ref`) | `0` | Help says `1` strips additive reference poses during cooking and `0` leaves this off. | Three comparison candidates read the reference (`0x1437B4B30`, `0x1437B4B4F`, `0x1437BEB29`). The help describes a cook-time operation; those static references do not establish that a runtime override can change already cooked game assets. |
| `a.UseNewMethodForCurveEvaluation` | bool (`ref`) | `true` | Selects between old (`0`) and new (`1`) curve-evaluation methods. The registry does not describe the implementations, affected curves, or compatibility differences. | Twelve comparison/load candidates read the value. This supports that the binary consults it, but the two evaluation algorithms and their effects were not reconstructed. |

## SpiderDes and locomotion

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `a.SpiderDes.EnableBoneAsyncCalculate` | int32 (`var`) | `1` | No help is supplied. “Bone async calculate” is only a name-based hint; scheduling, bones, and enable modes are unknown. | The game build contains the name, but the saved scan found no direct value read. Nearby string ordering is not a verified reference or explanation. |
| `a.SpiderDes.EnableIKBoneOffsetCache` | int32 (`var`) | `1` | No help is supplied. The name suggests an IK bone-offset cache, but does not define what is cached, its lifetime, or invalidation. | No direct value read was matched; no cache implementation was recovered. |
| `a.SpiderDes.IKBoneOffsetCachePlayTimeTolerance` | float (`var`) | `0.033333` | No help is supplied. The name suggests a play-time tolerance for an IK bone-offset cache; units and comparison direction are unknown. | No direct value read was matched. Do not assume the captured value represents seconds or a frame interval. |
| `a.SpiderDes.UpdateIKEveryFrameWhenStartSpike` | int32 (`var`) | `0` | No help is supplied. The name alone does not define “StartSpike,” the IK update interval, or the integer mode map. | No direct value read was matched; the feature and trigger conditions remain unresolved. |
| `a.UseSimplifiedLocomotion` | bool (`ref`) | `false` | When true, uses simplified locomotion without `MeleeTwist`, with blend thresholds described as larger. The help does not define the blend rules or which characters/states use this path. | Two direct comparison candidates read the value at `0x1455B424B` and `0x1455B7FDB`. The locomotion selection and visual/gameplay consequences were not traced. |

## Update-rate optimization (URO) and LOD

URO here means animation-rate optimization according to the registry help. These entries are recorded as `var` objects, so the available scan can confirm their names and setup but cannot match a `ref_rva` value read. The help still gives useful descriptions, but that does not prove that each control is consumed by this Shipping build or accepted from a local config.

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `a.URO.DisableInterpolation` | int32 (`var`) | `0` | Setting `1` disables interpolation. The affected interpolation path and visual tradeoff are unspecified. | Name and nearby help occur in the build string inventory; no direct value read was established. |
| `a.URO.DisableLodMap` | int32 (`var`) | `0` | Setting `1` disables the LOD map. The map's selection role and fallback are not described. | Name and nearby help occur in the build string inventory; no direct value read was established. |
| `a.URO.Draw` | int32 (`var`) | `0` | Enables color-coded boxes for animation rate. The color mapping and drawing conditions are unspecified. | The string is present in the build inventory; its visualization path was not recovered. |
| `a.URO.Enable` | int32 (`var`) | `1` | Enables animation-rate optimization. The registry does not state how eligibility, visibility, distance, or importance determine the rate. | Name/help are present in the build string inventory; no direct value read was established. |
| `a.URO.ForceAnimRate` | int32 (`var`) | `0` | A nonzero value forces an animation rate. Help gives `10` as an example that evaluates eligible meshes every ten frames and notes that some cases count a frame as 30 FPS. The exact eligible meshes and timing rule are not specified. | No direct value read was matched. Do not assume the example value works for every mesh or maps directly to display frame rate. |
| `a.URO.ForceInterpolation` | int32 (`var`) | `0` | Setting `1` forces interpolation. The help does not explain precedence with `DisableInterpolation` or other URO conditions. | Name/help are present in the build string inventory; no direct value read was established. |
| `a.URO.GpuSkinUpdateFollowURO` | bool (`ref`) | `false` | When true, GPU skin updates follow URO's update rate. It does not define which GPU-skinning paths qualify. | One direct comparison candidate reads the value at `0x143AA123E`; GPU-skin and animation scheduling behavior was not traced together. |
| `a.URO.LODSkipFrameCount_0` | int32 (`ref`) | `-1` | Help calls this the skip-frame count for LOD 0. The meaning of `-1`, the accepted range, and how counts vary by LOD are unspecified. | No direct value-read candidate was found. The captured `-1` does not establish a sentinel meaning. |
| `a.URO.LODSkipFrameCount_1` | int32 (`ref`) | `-1` | Help calls this the skip-frame count for LOD 1. | No direct value-read candidate was found; range and scheduling effect are unknown. |
| `a.URO.LODSkipFrameCount_2` | int32 (`ref`) | `-1` | Help calls this the skip-frame count for LOD 2. | No direct value-read candidate was found; range and scheduling effect are unknown. |
| `a.URO.LODSkipFrameCount_3` | int32 (`ref`) | `-1` | Help calls this the skip-frame count for LOD 3. | No direct value-read candidate was found; range and scheduling effect are unknown. |
| `a.VisualizeLODs` | int32 (`var`) | `0` | Visualizes skeletal-mesh LODs. The display mode and how it composes with other animation-rate debug visualization are not described. | Name/help are present in the build string inventory; no direct value read or visualization path was established. |

## Override and evidence limits

- The community registry classifies 10 entries as `ref` and 12 as `var`. The saved scan has direct value-access candidates for six: `a.SkipSubGraph.Enable`, `a.Streaming.SpoofFailedChunkLoad`, `a.StripAdditiveRefPose`, `a.URO.GpuSkinUpdateFollowURO`, `a.UseNewMethodForCurveEvaluation`, and `a.UseSimplifiedLocomotion`. Four other `ref` entries have no direct candidate in this scan; absence is not proof of no indirect or out-of-scope access.
- The other 12 `var` entries have name/setup evidence only. A `var` label or embedded name does not establish that a changed startup value reaches runtime behavior.
- No controlled `.ini` override comparison, live console query, animation/LOD comparison, or in-game test was performed. Snapshot values are not canonical defaults.
- For adjacent animation controls, see [animation system batch E](cvar-animation-system-batch-e.md), [animation system batch F](cvar-animation-system-batch-f.md), [animation-node controls](cvar-animation-nodes-batch-a.md), and [animation budget controls](cvar-animation-budget-batch-a.md). For registry and build-scan methodology, see [the community registry](cvar-community-registry.md), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
