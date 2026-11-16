# Scene capture, color, and tonemapper CVars: batch A

This guide covers 18 registered CVars that were not already explained in focused table guides: 11 scene-capture settings, six color/debug settings, and `r.Tonemapper.Quality`. The source registry includes community help and a captured value snapshot. That snapshot has no confirmed game build or collection method, so the values below are observations, not verified Marvel Rivals defaults or recommendations.

The registry also contains exact-name Unreal Engine 5.9 reference matches for 11 entries: four color-grade settings, six scene-capture settings, and tonemapper quality. These are upstream definitions, not proof that Marvel Rivals uses the same engine code or enables the associated rendering path.

## Scene capture

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `r.SceneCapture.AllowCustomCull` | int32 (`var`) | `1` | `0` disables and `1` enables custom scissor culling and custom frustum culling for `USceneCaptureWithScissorComponent2D`. | The build scan has object-address/setup references only. It does not prove the setting is read by a running capture component. |
| `r.SceneCapture.AlterConsoleVariables` | int32 (`var`) | `1` | `0` disables and `1` enables alteration of console variables by a scene capturer while rendering. The registry does not describe which variables are changed, when changes are restored, or how capture settings are selected. | Object-address/setup references only; no direct value read or scene-capture override behavior was traced. |
| `r.SceneCapture.CombineWithScenePostProccessVolumes` | int32 (`var`) | `0` | Controls whether scene captures combine with scene post-process volumes. Help maps `0` to disabled (stated default) and `1` to enabled. The registered spelling `PostProccess` is preserved. | Object-address/setup references only; the volume-combination path was not traced. |
| `r.SceneCapture.CullByDetailMode` | bool (`var`) | `true` | Prevents scene-capture updates according to the current detail mode. The help does not state which detail modes suppress updates. | Object-address/setup references only; no active capture or detail-mode decision was verified. |
| `r.SceneCapture.DepthPrepassOptimization` | int32 (`ref`) | `0` | Selects an experimental optimized scene-capture depth-prepass path. Help warns that enabling it ignores rendering after the depth pre-pass, such as SingleLayerWater, so the result differs from the non-optimized path. | Two direct `ref_rva` memory-access candidates occur in the scanned build. They do not establish that the optimized path executes or measure its visual/performance effect. |
| `r.SceneCapture.EnableOrthographicTiling` | bool (`var`) | `false` | Renders an orthographic scene capture across multiple frames/tiles. It is ignored in perspective mode and requires `r.SceneCapture.OverrideOrthographicTilingValues` to be enabled. | Object-address/setup references only; no tile scheduling or capture result was tested. |
| `r.SceneCapture.FixSceneCaptureStreaming` | bool (`ref`) | `false` | Help only says “Fix Scene Capture2D Streaming bug.” It does not explain the bug, the fix, or whether true enables a workaround. | One direct `ref_rva` access candidate was found. The streaming path and the branch effect remain unknown. |
| `r.SceneCapture.OrthographicNumXTiles` | int32 (`var`) | `4` | Sets the number of X tiles. It is ignored in perspective mode and works only in orthographic mode with `r.SceneCapture.OverrideOrthographicTilingValues` enabled. | Object-address/setup references only; no validation of valid counts, frame cost, or rendered output was performed. |
| `r.SceneCapture.OrthographicNumYTiles` | int32 (`var`) | `4` | Sets the number of Y tiles. It is ignored in perspective mode and works only in orthographic mode with `r.SceneCapture.OverrideOrthographicTilingValues` enabled. | Object-address/setup references only; no validation of valid counts, frame cost, or rendered output was performed. |
| `r.SceneCapture.OverrideOrthographicTilingValues` | bool (`var`) | `false` | Overrides orthographic values defined on `SceneCaptureComponent2D`; it is ignored in perspective mode. | Object-address/setup references only; which component fields are replaced was not recovered. |
| `r.SceneCapture.WithScissorMaxNumber` | int32 (`var`) | `-1` | No help is supplied. The name may indicate a maximum count related to scissored scene captures, but does not define the counted objects or `-1` behavior. | Object-address/setup references only; no value consumer or sentinel behavior was established. |

## Color grading and velocity debug

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `r.Color.Grading` | int32 (`var`) | `1` | Controls whether post-process color-grading settings are applied. | Object-address/setup references only; no active post-process configuration or image comparison was inspected. |
| `r.Color.Max` | float (`var`) | `1` | Maps input channel value `1.0` to a selected value after color grading. Help says values below 1 darken highlights, while larger values move more colors toward white; it recommends values around 1. | Object-address/setup references only; no color transform or output image was traced. |
| `r.Color.Mid` | float (`var`) | `0.5` | Maps input channel value `0.5` after color grading, described as similar to gamma correction. Help says lower values darken midtones and higher values brighten them; it recommends values around `0.5`. | Object-address/setup references only; no color transform or output image was traced. |
| `r.Color.Min` | float (`var`) | `0` | Maps input channel value `0` after color grading. Help says a positive value adds grayscale to darks, while a negative value makes more dark values become black; it recommends values around `0`. | Object-address/setup references only; no color transform or output image was traced. |
| `r.ColorDebug` | int32 (`var`) | `0` | Help says “View velocity in post overlay.” It does not define mode values, which velocity is shown, or how the overlay is activated. | Object-address/setup references only; the diagnostic overlay was not tested in-game. |
| `r.ColorDebugCrash` | int32 (`var`) | `0` | Help is the same as `r.ColorDebug`: “View velocity in post overlay.” Despite its name, the supplied help does not describe a crash action or crash trigger. | Object-address/setup references only; the diagnostic overlay and any relationship to `r.ColorDebug` were not traced. |

The four `r.Color.*` controls have exact-name Unreal 5.9 reference matches. For the three controls whose community help states mapping defaults (`Max`, `Mid`, and `Min`), the snapshot matches those values; `Grading` has a snapshot of `1`, while its registry help does not state a default. These matches do not prove which post-process settings the game applies. `r.ColorDebug` and `r.ColorDebugCrash` have no exact Unreal 5.9 reference match in the registry.

## Tonemapper quality

| Exact CVar | Type | Snapshot | What the registry says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `r.Tonemapper.Quality` | int32 (`var`) | `2` | The exact Unreal 5.9 help describes a range of `0..5`: `0` is the basic tonemapper only; `2` adds vignette; `4` adds grain; and `5` adds grain jitter and is labeled full quality/default. Values 1 and 3 are not described in the help. | Object-address/setup references only; no active tonemapper permutation or in-game image comparison was verified. The captured snapshot `2` differs from the help-stated default `5`. |

## What this says about editing

The community registry classifies 16 entries as `var` and two as `ref`. In the scanned Marvel Rivals Shipping build `1.1.4042190`, direct value-address candidates were found for the two `ref` settings (`DepthPrepassOptimization` and `FixSceneCaptureStreaming`). The `var` rows have object-address/setup matches, which are weaker evidence and do not establish that code reads their current values.

None of these registration or static-scan observations proves that the startup `.ini` loader accepts a line, that it wins over later configuration layers, or that the setting changes a live match. No controlled override, console query, capture comparison, or color/tonemapper test was performed. Scene-capture-specific settings may apply only when the game creates the relevant capture component or rendering mode.

For the source registry and snapshot limits, see [the community CVar registry](cvar-community-registry.md). For the static scan method and the distinction between registration/setup references and value reads, see [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). For broader renderer controls, see [Rendering general batch C](cvar-rendering-general-batch-c.md) and [Rendering post-processing batch A](cvar-rendering-postprocess-batch-a.md).
