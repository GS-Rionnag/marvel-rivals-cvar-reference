# AudioPerf, Localization, CullDistance, and TimerManager CVars

This guide covers 20 variable rows in four exact-case namespaces. The snapshot column gives captured values. A dash means the snapshot has no entry for that name.

## AudioPerf

The registry provides Chinese help for all five variables. The meanings below use the repository's English translations. The help gives no integer value mapping for the three history variables. [Help translation catalog](cvar-chinese-help-translations.md)

| Exact name | Type / kind | Snapshot | Meaning from translated help |
| --- | --- | --- | --- |
| `AudioPerf.History.Components` | `int32` / `var` | — | Records detailed component state on demand. The record does not measure actual tick duration. |
| `AudioPerf.History.Events` | `int32` / `var` | — | Records playback counts per Event ID on demand. The counts provide no voice or CPU attribution. |
| `AudioPerf.History.Wwise` | `int32` / `var` | — | Queries Playing IDs and SDK memory categories for selected components on demand. Event CPU cost is unavailable. |
| `AudioPerf.PostEvent.WindowSeconds` | `float` / `var` | — | Sets the PostEvent statistics window from 0.05 to 1 second. Changing the value starts a new segment. |
| `AudioPerf.Record.MaxMB` | `int32` / `var` | — | Sets the trace-file recording stop threshold from 1 to 1000 decimal MB. Async writes can slightly overshoot the threshold. |

## Localization

| Exact name | Type / kind | Snapshot | Meaning from supplied help |
| --- | --- | --- | --- |
| `Localization.AsyncLoadLocalizationData` | `bool` / `ref` | `true` | `true` selects asynchronous loading of localization data. `false` selects synchronous loading. |
| `Localization.AsyncLoadLocalizationDataOnLanguageChange` | `bool` / `ref` | `false` | Selects asynchronous loading when switching languages with `true`, or synchronous loading with `false`. The interaction with the general loading flag is unspecified. |
| `Localization.HangulTextWrappingMethod` | `int32` / `var` | `1` | Selects wrapping per syllable at `0` or per word at `1`. The help lists per-word wrapping as the default. |
| `Localization.SpanishUsesMinTwoGrouping` | `bool` / `var` | `true` | For the example value 1234, `false` uses a grouping separator and `true` omits it. The help lists `true` as the default. |
| `Localization.SpanishUsesRAENumberFormat` | `bool` / `var` | `true` | Selects Spanish number formatting according to RAE when `true`, or CLDR when `false`. The help lists RAE formatting as the default. |

## CullDistance

The registry and upstream cross-check provide no help for these five names. The table describes only what the identifiers suggest. Units, culling criteria, affected effects, and the interpretation of zero remain unverified.

| Exact name | Type / kind | Snapshot | Name-based reading |
| --- | --- | --- | --- |
| `CullDistance.GameplayEffect.AlwaysSource` | `int32` / `ref` | `1` | Suggests special treatment of an effect source. The name leaves the rule and value mapping unclear. |
| `CullDistance.GameplayEffect.Distance` | `int32` / `ref` | `10` | Suggests a distance setting for gameplay-effect culling. |
| `CullDistance.GameplayEffect.Replay.Distance` | `int32` / `ref` | `0` | Suggests a replay-specific gameplay-effect culling distance. |
| `CullDistance.GameplayEffect.Replay.ViewFrustumDistance` | `int32` / `ref` | `100` | Suggests a replay-specific view-frustum distance for gameplay effects. |
| `CullDistance.GameplayEffect.ViewFrustumDistance` | `int32` / `ref` | `100` | Suggests a view-frustum distance for gameplay effects. |

## TimerManager

| Exact name | Type / kind | Snapshot | Meaning from supplied help |
| --- | --- | --- | --- |
| `TimerManager.DumpTimerLogResolveVirtualFunctions` | `int32` / `ref` | `1` | Resolves virtual functions when logging timer information, where possible. The help gives no explicit value mapping. |
| `TimerManager.DumpTimerLogSymbolNames` | `int32` / `ref` | `1` | Includes symbol names in timer diagnostic logs at `1`. |
| `TimerManager.DumpTimerLogsThreshold` | `float` / `ref` | `0` | Timer diagnostic logging threshold in milliseconds. `0` disables threshold-triggered logging. |
| `TimerManager.FastPathRecyclePendingAdd` | `int32` / `ref` | `1` | At `1`, the stated default, `RemoveTimer` can use `TryWriteLock` to recycle pending-add timer indices synchronously, limiting timer array growth during same-frame add/remove churn. Set `0` to always defer recycling. |
| `TimerManager.MaxExpiredTimersToLog` | `int32` / `ref` | `30` | Caps the number of timer records above the log threshold reported in a single frame. |

## Build and source evidence

- All 20 names appear in the x64 and ARM64EC Shipping string inventories for build 1.1.4042190. The five Localization names also appear in the Crash Report Client inventory. The local Epic UE 5.9 cross-check matches all five Localization names and the four timer logging controls. [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Community registry](EVIDENCE.md#community-sources)
- In the x64 address scan, every variable has three direct-memory candidates and one address-taking instruction against `obj_rva`. Each `ref` has one address-taking instruction against `ref_rva`. At that field, the CullDistance variables have one direct-memory candidate each, with three for `CullDistance.GameplayEffect.Distance` and four for `CullDistance.GameplayEffect.ViewFrustumDistance`. The two Localization refs each have one. In table order, the TimerManager refs have 0, 1, 2, 1, and 1. [Address-reference scan](EVIDENCE.md#build-specific-static-analysis)
- The capture build of the community attachments is unspecified. The static evidence leaves runtime registration, call-path behavior, and startup override support unverified. [Raw registry](EVIDENCE.md#community-sources) · [Raw snapshot](EVIDENCE.md#community-sources) · [Source notes](EVIDENCE.md#community-sources)
