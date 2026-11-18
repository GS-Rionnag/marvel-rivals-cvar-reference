# Snapshot-only HeroAssetLoader and HeroAssetManifest candidates

This guide covers the 19 remaining snapshot-only names in the `Marvel.HeroAssetLoader.*` and `Marvel.HeroAssetManifest.*` families. Each name and captured value comes from the community `CVarDump.txt`; none has a `var`/`ref` row in `console_vars.tsv` or a `console_objects.tsv` row with help text. Only `Marvel.HeroAssetLoader.AbandonedIdleSeconds` has an exact printable-name match in the scanned Shipping executables. The family grouping and likely roles below are inferred from names alone.

| Snapshot name | Captured value (not default) | Conservative name-based reading | Exact Shipping string candidate |
| --- | --- | --- | --- |
| `Marvel.HeroAssetLoader.AbandonedIdleSeconds` | `0` | Possible idle-time threshold for abandoned hero assets. | yes |
| `Marvel.HeroAssetLoader.AbilityPresentation.AcquireOrderLRU` | `1` | Possible acquisition-order policy for cached ability-presentation assets; `LRU` appears in the name, but selection behavior is unknown. | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.IdleSeconds` | `30` | Possible idle retention duration for ability-presentation assets; units are suggested by the `Seconds` suffix only. | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.MaintenanceInterval` | `1` | Possible maintenance cadence for ability-presentation asset entries; unit is not stated. | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.MaxIdleEntries` | `32` | Possible maximum number of idle ability-presentation entries. | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.PreferLargeIdleEntries` | `0` | Possible preference affecting which larger idle ability-presentation entries are retained; exact policy is unknown. | no |
| `Marvel.HeroAssetLoader.Bond.AcquireOrderLRU` | `0` | Possible acquisition-order policy for cached Bond assets; exact behavior is unknown. | no |
| `Marvel.HeroAssetLoader.Bond.IdleSeconds` | `30` | Possible idle retention duration for Bond assets; units are suggested by the name only. | no |
| `Marvel.HeroAssetLoader.Bond.MaintenanceInterval` | `1` | Possible maintenance cadence for Bond asset entries; unit is not stated. | no |
| `Marvel.HeroAssetLoader.Bond.MaxIdleEntries` | `16` | Possible maximum number of idle Bond asset entries. | no |
| `Marvel.HeroAssetLoader.Bond.PreferLargeIdleEntries` | `0` | Possible preference affecting retention of larger idle Bond entries; exact policy is unknown. | no |
| `Marvel.HeroAssetLoader.Hero.AcquireOrderLRU` | `0` | Possible acquisition-order policy for cached Hero assets; exact behavior is unknown. | no |
| `Marvel.HeroAssetLoader.Hero.IdleSeconds` | `30` | Possible idle retention duration for Hero assets; units are suggested by the name only. | no |
| `Marvel.HeroAssetLoader.Hero.MaintenanceInterval` | `1` | Possible maintenance cadence for Hero asset entries; unit is not stated. | no |
| `Marvel.HeroAssetLoader.Hero.MaxIdleEntries` | `16` | Possible maximum number of idle Hero asset entries. | no |
| `Marvel.HeroAssetLoader.Hero.PreferLargeIdleEntries` | `0` | Possible preference affecting retention of larger idle Hero entries; exact policy is unknown. | no |
| `Marvel.HeroAssetLoader.ProfileRequests` | `false` | Possible profiling or request-tracking switch for the hero asset loader; precise meaning is unknown. | no |
| `Marvel.HeroAssetManifest.RuntimeMode` | `0` | Possible runtime-mode selector for an asset manifest; valid modes are unknown. | no |
| `Marvel.HeroAssetManifest.ShadowMaxSamples` | `8` | Possible cap for shadow or comparison samples associated with an asset manifest; exact meaning of “shadow” and sample unit are unknown. | no |

## Interpretation and limits

- The repeated `Hero`, `Bond`, and `AbilityPresentation` groups suggest per-category idle-entry policies. That pattern is an inference from the names and snapshots, not a confirmed cache design.
- `AcquireOrderLRU`, `IdleSeconds`, `MaintenanceInterval`, `MaxIdleEntries`, and `PreferLargeIdleEntries` are not accompanied by supplied help, type metadata, or accepted ranges. Do not assume a unit for `MaintenanceInterval` or interpret `0`/`1` as a confirmed boolean for integer-like names.
- Snapshot presence records only that the community dump contained these `name=value` rows. It does not prove registration, build compatibility, runtime use, or that the captured values are defaults.
- The single `AbandonedIdleSeconds` printable-string match is static evidence of a literal in the scanned binary set, not proof of execution. No exact-name match was found for the other 18 in the preserved scan inventory.
- These entries are deliberately treated as low-confidence snapshot candidates; none is promoted to a confirmed game CVar or a recommended override.

Sources: [community snapshot and registry attachments](EVIDENCE.md#community-sources), [snapshot-only candidate inventory](cvar-snapshot-only.md), and [build 1.1.4042190 binary inventory](EVIDENCE.md#build-specific-static-analysis).
