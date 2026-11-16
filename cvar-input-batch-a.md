# Input CVar batch A

This guide covers the nine exact-case `Input.*` registry entries found in the current research catalog. They concern input-event bookkeeping, axis consumption, chord mappings, force-feedback duration, and two opaque upload-related globals. The registry establishes presence and metadata; it does not establish that the game accepts these as `.ini` overrides.

The “snapshot” column records values observed in the supplied console dump, not guaranteed defaults. Epic UE 5.9 help/defaults are reproduced where available through the registry cross-reference. The build scan is static evidence from Shipping build 1.1.4042190, not a runtime behavior test.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 reference | What the evidence supports | Static scan |
| --- | --- | --- | --- | --- | --- |
| `Input.AutoReconcilePressedEventsOnFirstRepeat` | `bool` (`ref`) | `true` | `true`; synthesizes a pressed event when a repeat arrives first; help says this option will be removed in a future update | Repairs an input-event sequence where repeat precedes press. The deprecation note is from supplied help, not a promise about Marvel Rivals’ version. | `ref` and object-address candidates; static references found |
| `Input.AxisEventsCanBeConsumed` | `bool` (`ref`) | `true` | `true`; if all keys for an axis event are consumed, the axis delegate does not fire | Controls whether consumption of every key contributing to an axis suppresses its delegate callback. | `ref` and object-address candidates; static references found |
| `Input.CVarOpenPlayerKeyStateUpload` | `int32` (`var`) | `1` | No help/default reference | Name suggests a player key-state upload switch, but that is only a naming inference. Exact data, destination, and effect are unknown. | Object-address candidates only |
| `Input.CVarUploadClientMemoryInfo` | `int32` (`var`) | `1` | No help/default reference | Name suggests client memory information upload; payload, destination, and effect are unknown. | Object-address candidates only |
| `Input.FlushPendingPressedKeys` | `bool` (`ref`) | Not present | No Epic reference in the catalog | Help says that when true, `FlushPressedKeys` balances pending non-analog press events with release events. This is event-state cleanup, not evidence of a general input reset. | `ref` and object-address candidates; static references found |
| `Input.ForceInverseGamepadAcceptAndBackKey` | `bool` (`ref`) | `false` | No help/default reference | Name indicates inverse handling of gamepad Accept and Back keys, but which mapping or condition is inverted is undocumented in the gathered sources. | `ref` and object-address candidates; static references found |
| `Input.GGlobalEnableAbilityKeyConsume` | `int32` (`var`) | `1` | No help/default reference | Name suggests a global switch related to ability-key consumption. Whether it gates input, ability dispatch, or a particular subsystem is unresolved. | Object-address candidates only |
| `Input.GGlobalProtectChordMappings` | `int32` (`var`) | `1` | No English Epic help/default; community registry contains Chinese help | Supplied Chinese description translates to “protect the priority order of chord mappings.” The English translation is machine-assisted and unreviewed; interpretation is provisional. | Object-address candidates only |
| `Input.ShouldAlwaysEvaluateForceFeedbackDuration` | `bool` (`ref`) | `true` | `true`; asks whether force-feedback duration is evaluated every time it is called | Governs repeated duration evaluation for a force-feedback effect. No evidence here connects it to haptics intensity or a user-facing setting. | `ref` and object-address candidates; static references found |

## Reading these entries safely

- The two help-backed key-event variables describe engine input plumbing. They do not imply improved responsiveness or lower latency when changed.
- The three `GGlobal*`/`CVar*Upload*` names have no gathered implementation-level explanation. Treat their names as clues only; in particular, do not assume the upload variables disclose or transmit data merely from their names.
- `FlushPendingPressedKeys` has no value in the captured snapshot. The absence is not evidence that it is disabled or unavailable.
- Registry metadata lists `var` or `ref` registration categories and captured snapshots, while static address hits indicate compiled references/candidates. Neither demonstrates `.ini` load order, override acceptance, mutability, or runtime effect in the installed build.
- No live game or config-override experiment was performed for this batch. Runtime/editability status remains unknown for all nine entries.

## Sources and scope

Exact membership and type come from [the community registry](cvar-community-registry.md), cross-checked against [`console_vars.tsv`](EVIDENCE.md#community-sources). Snapshot values are in [`CVarDump.txt`](EVIDENCE.md#community-sources). Help/context and static hit methodology are described in the [build 1.1.4042190 text context](EVIDENCE.md#build-specific-static-analysis), [build inventory](EVIDENCE.md#build-specific-static-analysis), and [research-source notes](EVIDENCE.md#community-sources). `Input.GGlobalProtectChordMappings` translation is recorded in [`cvar-help-translations.tsv`](sources/cvar-research/cvar-help-translations.tsv) and marked unreviewed there.
