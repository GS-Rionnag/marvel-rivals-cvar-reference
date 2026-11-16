# HitRepFrame CVar batch B

This guide documents the remaining ten registered names whose exact, case-sensitive first dotted component is `HitRepFrame`. Together with batch A, this closes the supplied registry family: 35 of 35 unique `HitRepFrame.*` `var`/`ref` names are covered. Nine entries in this batch have no explanatory help, so their descriptions below are explicitly limited to tentative name-based hints.

“Snapshot” is the captured value in the supplied registry catalog, not a recommendation or proven default. The Epic UE 5.9 column contains exact-name upstream reference defaults; `—` means no matching value was recorded. Static scan counts are instruction-reference classifications, not runtime traces.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help or name-only hint | Build 1.1.4042190 static address evidence |
| --- | --- | ---: | ---: | --- | --- |
| `HitRepFrame.Move.UpdateEqualsTolerance` | float (`var`) | `0.0001` | — | No help is supplied. The identifier suggests a tolerance for treating movement updates as equal; application and units are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.Move.UpdateMaxTime` | float (`var`) | `0.2` | — | No help is supplied. The identifier suggests a maximum time associated with movement updates; what is bounded and the units are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.NAC.Debug` | int32 (`var`) | `0` | — | No help is supplied. The identifier suggests a debug setting in a subsystem labeled `NAC`; the acronym and behavior are unresolved. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.NAC.Enable` | int32 (`var`) | `1` | — | No help is supplied. The identifier suggests an enable setting for the `NAC` area, but the acronym, scope, and value mapping are unresolved. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.NAC.FrameCount` | int32 (`var`) | `3` | — | No help is supplied. The identifier suggests a frame-count parameter in the `NAC` area; what it counts is unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.NAC.OffsetTolerant` | float (`var`) | `200` | — | No help is supplied. The identifier suggests offset tolerance in the `NAC` area; units and interpretation are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.Projectile.Opt` | int32 (`var`) | `1` | — | No help is supplied. The identifier suggests a projectile-related optimization setting; the optimization and value mapping are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.Rollback.DebugLocation` | FString (`var`) | — | — | No help is supplied. The identifier suggests a rollback debug location parameter; its expected string format and effect are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.Rollback.HistoricalFilter` | int32 (`var`) | `1` | — | Community help: `0=off, 1=TracedSpec+Tags historical filtering in rollback`. The supplied text gives these two values but does not further define the filter implementation. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `HitRepFrame.Rollback.Opt` | int32 (`var`) | `1` | — | No help is supplied. The identifier suggests a rollback-related optimization setting; the optimization and value mapping are unknown. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |

## Evidence limits and coverage audit

- All ten entries have one consistent registry row and kind `var`: six int32, three float, and one FString. Nine captured snapshot values are present; `HitRepFrame.Rollback.DebugLocation` has no captured value. No exact-name Epic UE 5.9 default is recorded for any of the ten.
- The build scan reports 20 `direct-memory-candidate` hits and 10 `address-taken` hits, all against `obj_rva`; these rows have no `ref_rva` matches. Direct-memory candidates do not identify read/write direction or prove execution; address-taking hits are not value accesses. The scan does not show that startup overrides or `.ini` edits are accepted.
- This batch contains exactly the ten names remaining after batch A, with no overlap. Combined coverage is 35/35 registered `HitRepFrame.*` names, with zero remaining in the supplied family.

Sources: [community CVar registry](cvar-community-registry.md), [preserved registry and snapshot attachments](EVIDENCE.md#community-sources), and [build address-reference scan](EVIDENCE.md#build-specific-static-analysis).
