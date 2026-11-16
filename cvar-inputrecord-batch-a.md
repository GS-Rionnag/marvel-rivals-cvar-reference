# InputRecord CVar batch A

This guide covers all seven currently uncovered exact-case `InputRecord.*` registry entries. Three supplied descriptions refer to showing input keys or axis keys while recording or playing. Four `Change*DeltaTime` entries have no supplied help; their names suggest timing adjustments, but the registry does not explain the units, affected subsystem, or behavior. Avoid treating that name-based interpretation as confirmed functionality.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help or name | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `InputRecord.ChangeActorTickDeltaTime` | `float` (`var`) | `0` | No help supplied. The name suggests changing an actor tick delta time, but what changes and how the value is applied are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InputRecord.ChangeCodeTickerDeltaTime` | `float` (`var`) | `0` | No help supplied. The name suggests a code-ticker delta time; the affected ticker and units are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InputRecord.ChangeCompTickDeltaTime` | `float` (`var`) | `0` | No help supplied. The name suggests a component tick delta time; the affected component(s) and application are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InputRecord.ChangeInputDeltaTime` | `float` (`var`) | `0` | No help supplied. The name suggests an input delta-time value, but the registry does not explain what consumes it or its units. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InputRecord.bShowPlay` | `bool` (`ref`) | `false` | Enables or disables showing keys during playback. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `InputRecord.bShowRecordAxisKey` | `bool` (`ref`) | `false` | Enables or disables showing axis keys during recording. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `InputRecord.bShowRecordKey` | `bool` (`ref`) | `false` | Enables or disables showing input keys during recording. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- The key-display help points to recording/playback presentation. It does not establish that the settings are exposed in ordinary matches or that they affect gameplay input handling.
- The four timing entries have blank help. Their names alone cannot establish whether they are multipliers, replacement delta times, profiling controls, or something else.
- Snapshot values are observations, not verified defaults or recommendations. `0` on the timing entries does not establish that the controls are disabled or inert.
- Build scan matches are static candidates only. They do not prove runtime reads/writes, execution, a visible effect, or that Marvel Rivals accepts startup `.ini` overrides for these entries.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
