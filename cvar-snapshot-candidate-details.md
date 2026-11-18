# Snapshot-only candidates with converging engine evidence

This guide compares 15 benign graphics, animation, and UI names that appear in all four supplied/local evidence sources: the community value snapshot, the separate community `console_objects.tsv` table, an exact-name Epic Unreal Engine 5.9 CVar-reference entry, and printable strings in both Shipping executables for Marvel Rivals build 1.1.4042190. Each is absent from the community `var`/`ref` registry. The overlap makes these high-evidence *candidates*, not confirmed Marvel Rivals runtime CVars.

The community snapshot records captured values, not defaults. Console-object flags are reproduced as raw metadata; their meaning is not established. Epic 5.9 is upstream comparison material and does not establish the game’s exact engine version or runtime behavior.

| Exact name | Community snapshot / object flags | Supplied object-table help | Exact Epic UE 5.9 entry | Shipping binary string |
| --- | --- | --- | --- | --- |
| `a.Streaming.ChunkSizeSeconds` | `4` / `0` | Size of a streaming animation chunk in seconds; zero or negative means only one chunk. | Default `4`; matching description. | x64 + ARM64EC |
| `a.StripFramesOnCompression` | `0` / `0` | `1` strips every other frame on animations with an even number of frames; `0` disables stripping. | Default `0`; matching description. | x64 + ARM64EC |
| `a.StripOddFramesWhenFrameStripping` | `0` / `0` | `1` also applies frame stripping to animations with an odd frame count; `0` limits it to even-frame animations. | Default `0`; matching description. | x64 + ARM64EC |
| `fx.Niagara.PruneEmittersOnCook` | `1` / `320` | If greater than zero, the platform prunes disabled Niagara emitters during cook. | Default `1`; matching description. | x64 + ARM64EC |
| `fx.Niagara.QualityLevel` | `2` / `16777536` | Niagara Effects quality level. | Default `3`; same short description, but the captured value differs (`2` vs `3`). | x64 + ARM64EC |
| `fx.Niagara.QualityLevel.Max` | `-1` / `4` | Maximum Niagara Effects quality level. | Default `-1`; matching description. | x64 + ARM64EC |
| `fx.Niagara.QualityLevel.Min` | `-1` / `4` | Minimum Niagara Effects quality level. | Default `-1`; matching description. | x64 + ARM64EC |
| `fx.NiagaraAllowRuntimeScalabilityChanges` | `1` / `67109184` | If greater than zero, allows Niagara scalability settings to change at runtime. | Default `1`; matching description. | x64 + ARM64EC |
| `r.DebugActionZone.ActionRatio` | `1` / `0` | Action-zone ratio returned by `FDisplayMetrics::GetDisplayMetrics` on platforms without a defined safe zone; help gives range `0..1` and default `1.0`. | Default `1`; matching description. | x64 + ARM64EC |
| `r.DebugSafeZone.TitleRatio` | `1` / `0` | Safe-zone ratio returned by `FDisplayMetrics::GetDisplayMetrics` on platforms without a defined safe zone; help gives default `1.0`. | Default `1`; matching description. | x64 + ARM64EC |
| `r.Shadow.Virtual.Cache.AllocateViaLRU` | `0` / `32` | Prioritizes keeping more recently requested cached physical pages when allocating new pages. | Default `0`; matching description. | x64 + ARM64EC |
| `r.grass.DensityQualityLevel` | `-1` / `320` | Grass density quality level; help lists low, medium, high, and epic. | Default `-1`; matching description. | x64 + ARM64EC |
| `Slate.bAllowNotifications` | `true` / `0` | If false, notifications are not displayed to the user. | Default `true`; matching description. | x64 + ARM64EC |
| `Slate.bAllowThrottling` | `1` / `0` | Allows Slate to throttle parts of the engine to help keep the UI responsive. | Default `1`; matching description. | x64 + ARM64EC |
| `Slate.DeferWindowsMessageProcessing` | `1` / `0` | Controls whether Windows message processing is deferred until tick or handled immediately. | Default `1`; matching description. | x64 + ARM64EC |

## What this evidence does and does not establish

- The community snapshot and object table independently contain the same exact names and help for all 15 candidates. The object flags vary widely, but the available sources do not define those numbers, so no type, priority, or mutability meaning is assigned to them.
- The exact Epic UE 5.9 name and description matches strengthen the interpretation of each string as an Unreal CVar-shaped control. They do not prove Marvel Rivals uses the same code path or version.
- The local build inventory finds each literal in both the x64 and ARM64EC Shipping executables. Printable strings establish binary presence only; they do not prove registration, execution, or that an override is read.
- None of these names has a `var` or `ref` row in the preserved community registry. The snapshot’s re-importable header indicates how that source treats the dump, but it does not prove the game accepts these names from an `.ini` file.
- `fx.Niagara.QualityLevel` is a concrete source discrepancy: snapshot `2`, Epic 5.9 reference default `3`. The evidence cannot determine whether that reflects a deliberate captured setting, game-specific default, engine-version difference, or another source difference.
- `fx.Niagara.PruneEmittersOnCook` explicitly concerns cooking assets. It should not be read as a runtime visual-quality control merely because its name and binary string are present.

Sources: [community snapshot and object-table attachments](EVIDENCE.md#community-sources), [Epic 5.9 and Shipping-string cross-reference](cvar-snapshot-only.md), [engine-reference-only entries](cvar-engine-reference-only.md), and [build 1.1.4042190 binary inventory](EVIDENCE.md#build-specific-static-analysis).
