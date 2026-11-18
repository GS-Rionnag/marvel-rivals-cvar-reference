# Additional CVar registry evidence

These five entries cover prediction settings, visibility update serialization, and trace processing. Snapshot values are observations from an unspecified capture build.

The build column records exact name matches in the 1.1.4042190 binary inventory. The two address columns record x64 direct-memory candidates / address-taking instructions. A dash indicates no evidence in that column. Runtime effects and startup override support remain unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `Performance.MarvelApplyCost.MaxPredict` | `int32` / `ref` | `250` | No supplied help. The name suggests a maximum value in the ApplyCost prediction path. The limit, units, and affected code are unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `Performance.MarvelApplyCost.MinPredict` | `int32` / `ref` | `50` | No supplied help. The name suggests a minimum value in the ApplyCost prediction path. The limit, units, and affected code are unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `PlayerController.LevelVisibilityDontSerializeFileName` | `bool` / `ref` | `false` | Supplied help says that when enabled, level-visibility update info omits FileName to reduce bandwidth when both identifiers are unnecessary. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `Tether.TruncateHits` | `int32` / `var` | `1` | No supplied help. The name suggests truncating tether hit results. The limit, selection criteria, and call sites are unspecified. | x64, ARM64EC | 3 / 1 | — |
| `m2212.Raccoon.TracePrefilter` | `int32` / `var` | `2` | Supplied help maps 0 to the original path, 1 to comparison only, and 2 to prefiltering predicted-empty traces. The help states 2 is the default and gives no prediction method. | x64, ARM64EC | 3 / 1 | — |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
