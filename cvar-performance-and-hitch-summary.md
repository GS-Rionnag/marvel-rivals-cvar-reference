# Hitch collection and runtime performance CVars

These eight exact registry entries cover hitch diagnostics, Fast Array comparison work, and per-frame object processing. The Fast Array and actor-frame rows summarize the existing focused traces. Snapshot values are observations from an unspecified capture build.

Build strings are exact names in the build 1.1.4042190 inventory. The address columns give x64 direct-memory candidates / address-taking instructions. A dash means no matching evidence. Static matches leave runtime effects and startup override support unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `marvelstats.EnableOnlineHitchCounting` | `bool` / `ref` | `true` | No supplied help. The name suggests enabling online hitch counting. What online denotes and which samples count are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `marvelstats.HitchCollectDelayInSeconds` | `float` / `ref` | `0.5` | No supplied help. The name suggests a collection delay in seconds. The trigger, timing reference, and effect are unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `marvelstats.HitchCountingThresholdInSeconds` | `float` / `ref` | `0.1` | No supplied help. The name suggests a counting threshold in seconds. Its relationship to detection and collection is unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `marvelstats.HitchDetectThresholdInSeconds` | `float` / `ref` | `0.1` | The supplied help says a frame time strictly above this threshold is detected as a hitch. The unit is seconds. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `marvelstats.MaxRingBufferSizeMB` | `int32` / `ref` | `64` | The supplied help gives the maximum expanded ring-buffer size when collecting hitches and says the value cannot exceed 256 MB. Allocation and out-of-range behavior are unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `net.FastArrayIgnoreLocalID` | `bool` / `ref` | `true` | The focused static trace shows a per-entry ID-like comparison that can avoid a helper call under an additional condition. Source field names and runtime effects remain unresolved. [Fast Array trace](cvar-fast-array-sharing.md) | x64, ARM64EC | 2 / 1 | 32 / 1 |
| `net.ShareFastArrayCompare` | `bool` / `ref` | `false` | The focused static trace shows a gated alternate comparison path using stored state and a hash lookup. Cache scope, validity rules, and performance remain unresolved. [Fast Array trace](cvar-fast-array-sharing.md) | x64, ARM64EC | 2 / 1 | 96 / 1 |
| `Performance.DestroyActorFrame.Enable` | `bool` / `ref` | `false` | The focused static trace shows a branch to a helper that can append eligible objects to a list. The consumer, actor-destruction timing, and performance effect remain unresolved. [Actor-frame trace](cvar-performance-destroy-actor-frame.md) | x64, ARM64EC | 3 / 1 | 9 / 1 |

The adjacent binary strings place the hitch collection delay near the ring-buffer size help. That help belongs to the ring-buffer name in the registry. [Nearby binary-string inventory](EVIDENCE.md#build-specific-static-analysis) | [CVar override guide](cvar-overrides.md)

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
