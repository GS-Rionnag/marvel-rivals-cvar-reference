# MarvelGameplayCue CVar batch A

This guide covers the eight currently uncovered exact-case `MarvelGameplayCue.*` registry entries. Supplied help describes decal material curves and culling, melee hit-effect precision, and remote laser-effect hit prediction/audio. English explanations below are working translations of the community’s Chinese help and are not independently reviewed. They describe the stated intent, not verified in-game behavior.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 scan |
| --- | --- | --- | --- | --- |
| `MarvelGameplayCue.EnableDecalMaterialCurve` | `int32` (`ref`) | `1` | Enables material curves for some decals. Disabling may remove complex gradient effects while preserving basic fade-out. The help does not define whether every nonzero value enables it. | 6 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.LaserCue.AudioReusePredictHits` | `bool` (`ref`) | — | On remote laser cues, periodically rechecks audio timing while reusing cached predicted hits, including fake-predicted locations rotated with camera direction. If the cache is empty, it falls back to a real `ForceTraceSpec` check. `0` means the older behavior of checking independently each time. | 6 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.LocalLaserFakePredictHitNum` | `int32` (`ref`) | `0` | On the local side, how many laser-effect predicted-hit calculations occur before a real world line trace. If traces are not allowed, the next hit location is estimated from the previous result and current camera direction. | 6 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.MeleeHitEffectDetailLevel` | `int32` (`ref`) | `1` | Controls precision for melee hit-effect/decal positions: higher levels provide more precise hit positions at higher computation cost. The help does not state valid levels or boundaries. | 7 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.OtherDecalCullSize` | `float` (`ref`) | `0` | Cull an ability-hit decal on a non-viewed character when its size-to-distance ratio falls below this threshold. | 6 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.SimulateLaserFakePredictHitNum` | `int32` (`ref`) | `0` | On remote clients, how many laser-effect predicted-hit calculations occur before a real world line trace. Help states default `2`; `0` restores tracing on every calculation. When traces are disallowed, the predicted position uses the last result and current camera direction. | 7 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.UseFakeAimLocationWhenCalculateFakeLaserHit` | `int32` (`ref`) | `1` | While estimating a new laser hit from camera direction, also estimate the camera aim location from prior state instead of using a world trace. | 7 `ref_rva` candidates; no `obj_rva` hits. |
| `MarvelGameplayCue.ViewTargetDecalCullSize` | `float` (`ref`) | `0` | Cull an ability-hit decal on the viewed character when its size-to-distance ratio falls below this threshold. | 6 `ref_rva` candidates; no `obj_rva` hits. |

## Interpretation and limits

- The paired `OtherDecalCullSize` and `ViewTargetDecalCullSize` descriptions distinguish non-viewed and viewed characters. The snapshot values of `0` do not prove culling is disabled: threshold semantics, runtime clamps, and whether zero is a special value are undocumented.
- The two `*FakePredictHitNum` names distinguish local and remote behavior according to supplied help. The name and description do not prove that changing them affects authoritative hit registration; they are described as hit-position prediction for effects.
- `LaserCue.AudioReusePredictHits` is absent from the captured snapshot. Absence is not a known default.
- All eight rows are classified as `ref`, not `var`. A registry entry, snapshot value, or address-reference candidate does not prove that Marvel Rivals registers the setting at runtime or accepts a startup `.ini` override.
- Static scan counts are candidate references only. They do not prove reads, writes, execution, or visible effects. Captured values are observations, not recommendations or verified defaults.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), [Chinese help and working translations](cvar-chinese-help-translations.md), and [build 1.1.4042190 static scan and provenance](EVIDENCE.md#build-specific-static-analysis).
