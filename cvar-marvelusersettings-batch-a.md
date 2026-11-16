# MarvelUserSettings CVar batch A

This guide covers all 10 currently uncovered exact-case `MarvelUserSettings.*` `var`/`ref` entries. The supplied text points to game-settings UI, performance collection, scalability, an FPS/network information panel, and an RHI-optimization menu entry. Several help strings merely repeat the variable name, so their exact role is unknown. The registry does not identify its capture build.

None has an exact-name Epic UE 5.9 CVar reference match. Snapshot values are observations, not defaults. Every entry is a `var` row; the local scan found three direct-memory candidates and one address-taking reference for each `obj_rva`, but no `ref_rva` field. These scan results are not proof of reads/writes, execution, or `.ini` acceptance. No runtime override test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `MarvelUserSettings.EnabledPIE` | `bool` (`var`) | `false` | — | Supplied help repeats `MarvelUserSettings.EnabledPIE`; behavior and any PIE meaning remain unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.EnabledPerformanceCollect` | `bool` (`var`) | `false` | — | Supplied help says only “EnabledPerformanceCollect in game settings.” Whether this is a menu visibility flag, a collection toggle, or both is unspecified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.EnabledScalability` | `bool` (`var`) | `true` | — | Supplied help repeats `MarvelUserSettings.EnabledScalability`; exact behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.ForceShowFPSWidget` | `bool` (`var`) | `false` | — | Supplied help repeats `MarvelUserSettings.ForceShowFPSWidget`; the widget's display conditions are not documented by this row. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.IntervalToUpdateFPSInfoPanel` | `float` (`var`) | `0.1` | — | Community help (translated, unreviewed): update interval in seconds for the overall information panel, including FPS, network information, and network status. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.Level` | `int32` (`var`) | `-1` | — | Supplied help repeats `MarvelUserSettings.Level`; its range and meaning are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.PlatformName` | `FString` (`var`) | — | — | Supplied help repeats `MarvelUserSettings.PlatformName`; expected platform identifiers and use are not documented. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.ShowRHIOptimization` | `bool` (`var`) | `false` | — | Supplied help: show the RHI Optimization setting entry in game settings. This describes showing a setting entry, not applying or enabling an RHI optimization. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.SkipFGBeforeLobby` | `bool` (`var`) | `false` | — | Supplied help repeats `SkipFGBeforeLobby`; the meaning of `FG`, timing, and skipped operation are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `MarvelUserSettings.Version` | `int32` (`var`) | `22` | — | Supplied help repeats `MarvelUserSettings.Version`; the name does not establish whether this is a settings schema version or another version value. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- `MarvelUserSettings.*` and the two help strings referring to “game settings” point toward settings-related data, but do not prove that these variables map directly to visible UI controls or user preferences.
- The FPS information-panel interval has an unreviewed translation and a `0.1` snapshot; neither establishes a runtime default or refresh cadence in the installed game.
- The `ShowRHIOptimization` help says to show a menu entry. It does not say that this CVar applies the optimization itself.
- Nearby build strings do not connect these names to a specific code path. The table's address candidates are not call-flow or runtime evidence.
- Whether these variables are accepted through startup `.ini` overrides in the mod loader remains unverified.

Sources: [community registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
