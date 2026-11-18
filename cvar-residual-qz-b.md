# Residual Q–Z engine, UI, replay-export, and diagnostic CVars (batch B)

This follow-up records 12 additional exact-case `var`/`ref` names beginning Q–Z (case-insensitive), excluding names with the exact lowercase `r.` prefix. Names were checked against the public focused documentation and the earlier local Q–Z batch. This is a focused benign subset; it does not claim that all remaining Q–Z entries are covered.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help or conservative name reading | Build 1.1.4042190 scan candidates |
| --- | --- | --- | --- | --- |
| `ReplayDataExport.CompressJson` | `bool` (`var`) | `false` | Gzip the exported JSON output. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ReplayDataExport.Enable` | `bool` (`var`) | `false` | Master switch for replay data export; the help does not specify output contents or when export runs. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ReplayDataExport.PlayTimeRate` | `float` (`var`) | `8` | Playback speed for the replay-data export path. The help does not define units or a supported range. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ReplayDataExport.PositionInterval` | `float` (`var`) | `0.25` | Position sampling interval in seconds. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `SVON.DebugDrawPath` | `int32` (`var`) | `0` | Enables debug drawing of SVON navigation paths: `0` disabled, `1` enabled. The source does not expand “SVON.” | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `Select.AllowToLimitMaxSelectNum` | `bool` (`ref`) | `false` | No supplied help. The name suggests permitting a maximum-selection limit, but the affected selection system and behavior are unknown. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `SpineWidget.AllowBatchTickInParallel` | `bool` (`ref`) | `true` | No supplied help. The name suggests allowing batched SpineWidget ticking to run in parallel; scheduling and compatibility details are unknown. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `ref.AllowParallelCollection` | `int32` (`ref`) | `1` | Controls parallel reference collection. Help does not define the integer modes or collection scope. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `save.FixupStandaloneFlags` | `int32` (`ref`) | `0` | If nonzero, adds `RF_Standalone` to a package UAsset missing the flag. If zero, flags remain unchanged and saving fails. The description concerns a package-save path. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `umg.enable_sequence_player_pool` | `bool` (`ref`) | `true` | Enables the `UMGSequencePlayerPool`. The help does not describe pooling behavior or limits. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `upload.show.drawtimerinterval` | `float` (`ref`) | `0.5` | No supplied help. The name suggests a timer interval for a display associated with upload; its function and units are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `UserSetting.RebuildInputOnlyIfHeroChanged` | `bool` (`ref`) | `true` | No supplied help. The name suggests rebuilding input settings only when the selected hero changes; exact scope and effect are unknown. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- Snapshot values are observations, not verified defaults or recommendations. For fields with only name-based readings, the names do not establish actual implementation behavior.
- The described replay export, debug drawing, parallel collection, package saving, and UI paths may belong to diagnostics, tooling, or internal runtime paths. Their presence in the community registry does not show they are player-facing or active in ordinary matches.
- Build scan matches are static address-reference candidates, not proof of execution, runtime registration, config loading, or visible effect. `var`/`ref` classification also does not prove that startup `.ini` overrides are accepted.
- Selection, animation scheduling, and other gameplay-adjacent mechanics are deliberately not inferred beyond the supplied help; names alone are insufficient to establish safe or intended usage.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
