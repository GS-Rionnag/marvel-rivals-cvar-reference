# FX budget and Cascade CVars

This page covers the ten `fx.Budget.*` entries and seven `fx.Cascade.*` entries in the supplied community variable registry. Their help text describes a global FX budget tracker and Cascade particle-system controls. The numeric values below are observations from the attached CVar snapshot, not verified game defaults or recommendations.

## FX budget tracking

The registry describes a shared budget tracker across game-thread, concurrent game-thread, and render-thread FX work. As a budget is approached or exceeded, participating FX systems may scale down. The help does not identify which systems respond, the scaling policy, or how the three thread budgets interact.

| Exact CVar | Type | Snapshot | What the registry help says | Interpretation and limits |
| --- | --- | ---: | --- | --- |
| `fx.Budget.Enabled` | bool (`ref`) | `false` | Controls whether global FX budgets are tracked. | The snapshot is off. The registry does not establish which other systems depend on tracking or whether enabling it changes visible effects in this game build. |
| `fx.Budget.GameThread` | float (`ref`) | `2` | Millisecond budget for combined FX work running only on the game thread; systems may scale down more aggressively as the budget is approached or exceeded. | This is a time budget, not a frame-rate target. The exact accounting window and participating FX systems are unspecified. |
| `fx.Budget.GameThreadConcurrent` | float (`ref`) | `2` | Millisecond budget for combined FX work on the game thread or a concurrent task spawned from it. | The help does not say whether work counted here is also counted by `GameThread`, or how a concurrent task's time is measured. |
| `fx.Budget.RenderThread` | float (`ref`) | `2` | Millisecond budget for combined FX work on the render thread; systems may scale down as the budget is approached or exceeded. | The help describes FX work, not the whole render-thread frame. It does not identify affected render systems or their quality tradeoffs. |
| `fx.Budget.HistoryFrames` | int32 (`ref`) | `60` | Number of frames retained to calculate average frame time for the global FX budget tracker. | This suggests a rolling history, but the averaging method, minimum/maximum accepted values, and update cadence are not given. |
| `fx.Budget.AdjustedUsageDecayRate` | float (`ref`) | `0.1` | Rate at which adjusted budget usage is allowed to decay; intended to reduce FX switching on and off when usage oscillates around a culling threshold. | This is a smoothing/stability control by description. Units, formula, and relation to each thread's budget are unspecified. |
| `fx.Budget.AdjustedUsageMax` | float (`ref`) | `2` | Maximum adjusted usage; intended to stop one very long frame from keeping usage above `1.0` for an extended period. | The help identifies a cap and an example failure mode, but does not define the usage scale or whether `1.0` is the only threshold used. |
| `fx.Budget.Debug.GameThreadTimeOverride` | float (`ref`) | `-1` | When at least `0.0`, overrides the reported FX time for the game thread; described as useful for observing/debugging impact on other systems. | The snapshot's `-1` is outside the documented override range. The help does not say whether the value simulates reported cost, feeds budget decisions, or only affects diagnostics. |
| `fx.Budget.Debug.GameThreadConcurrentTimeOverride` | float (`ref`) | `-1` | When at least `0.0`, overrides the reported FX time for game-thread concurrent work. | Same caveat as the game-thread override: the precise reporting and budget-consumer path is not documented. |
| `fx.Budget.Debug.RenderThreadTimeOverride` | float (`ref`) | `-1` | When at least `0.0`, overrides the reported FX time for render-thread work. | The help does not establish whether this changes measured cost, a reported statistic, or both. |

## Cascade particle controls

Cascade is Unreal Engine's older particle-system framework; these names target Cascade-specific rendering/update behavior according to their help. They do not establish controls over Niagara or every visual effect in Marvel Rivals.

| Exact CVar | Type | Snapshot | What the registry help says | Interpretation and limits |
| --- | --- | ---: | --- | --- |
| `fx.Cascade.BeamRenderingEnabled` | bool (`ref`) | `true` | Enables or disables beam rendering for Cascade. | This names one Cascade renderer type. The help does not say how many game effects use it or what fallback is shown when disabled. |
| `fx.Cascade.GpuSpriteRenderingEnabled` | bool (`ref`) | `true` | Enables or disables GPU sprite rendering for Cascade. | This is specific to the GPU-sprite path; it does not claim to disable CPU sprites or Niagara sprites. |
| `fx.Cascade.MeshRenderingEnabled` | bool (`ref`) | `true` | Enables or disables mesh rendering for Cascade. | It identifies a renderer path, but not whether affected systems switch to another renderer or simply lose those particles. |
| `fx.Cascade.SpriteRenderingEnabled` | bool (`ref`) | `true` | Enables or disables sprite rendering for Cascade. | Scope is Cascade sprite rendering. The help does not identify whether it includes GPU sprites or how that setting composes with `GpuSpriteRenderingEnabled`. |
| `fx.Cascade.TrailRenderingEnabled` | bool (`ref`) | `true` | Enables or disables trail rendering for Cascade. | The help does not describe trail simulation, update, or fallback behavior when rendering is disabled. |
| `fx.Cascade.SkipZeroDeltaTime` | bool (`ref`) | `true` | When enabled, a delta tick time close to zero skips the component update. The help says this fixes issues such as velocity-aligned sprites, but can affect systems that need accurate velocities, including TSR. | The exact near-zero threshold and affected components are unspecified. The source help warns that disabling the update can have visual consequences. |
| `fx.Cascade.UseVelocityForMotionBlur` | bool (`var`) | `true` | When enabled, velocity is used to approximate velocity for vertex factories that support it. | This is limited by vertex-factory support. The help does not specify which factories Marvel Rivals uses or how the approximation changes the final blur. |

## Evidence and editability limits

- The supplied registry classifies these names as `var` or `ref` and supplies the help and captured values. Its build identity and capture method are unknown; the values should not be treated as defaults.
- All 17 exact names also appear in the static nearby-text inventory for Marvel Rivals build `1.1.4042190`. That inventory associates help-like strings by proximity in the executable; the association is not a verified code reference or runtime registration trace.
- No consumer call path, live console query, config override, or visual test was performed for this batch. The `ref`/`var` label and an embedded name do not by themselves prove that a startup `.ini` override is accepted or that changing a value affects a live match.
- For the broader static-scan method and version caveats, see [the build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis), [the build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis), and [the community registry](cvar-community-registry.md).
