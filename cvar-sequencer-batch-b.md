# Sequencer CVar batch B

This guide documents the final five currently uncovered registered names whose exact, case-sensitive first dotted component is `Sequencer`. Together with batch A, it closes the supplied registry family at 30 of 30 unique `Sequencer.*` `var`/`ref` names.

“Snapshot” is the captured value in the supplied registry catalog, not a recommendation. The Epic UE 5.9 default is an exact-name upstream reference value; it is recorded separately from the snapshot and community help. The descriptions below summarize supplied help and do not establish behavior in the shipped game.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Meaning from supplied help | Build 1.1.4042190 static address evidence |
| --- | --- | ---: | ---: | --- | --- |
| `Sequencer.StartTransformOffsetInBoneSpace` | bool (`var`) | `true` | `true` | For skeletal-animation matching, `true` applies start offsets in bone space and `false` in root space; help gives `true` as the default. | `obj_rva`: 2 direct-memory candidates, 1 address-taking hit; no `ref_rva` match. |
| `Sequencer.ThreadedEvaluation.AllocationThreshold` | int32 (`ref`) | `32` | `32` | Entity-allocation fragmentation threshold above which threaded evaluation will be used; help gives a default of 32. | `ref_rva`: 1 direct-memory candidate, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. |
| `Sequencer.ThreadedEvaluation.EntityThreshold` | int32 (`ref`) | `256` | `256` | Number of entities that need to exist to justify threaded evaluation; help gives a default of 256. | `ref_rva`: 1 direct-memory candidate, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. |
| `Sequencer.TickIntervalGroupingResolutionMs` | int32 (`ref`) | `50` | `50` | Maximum resolution for actor tick-interval groupings. Larger values group more actors with custom tick intervals but make those intervals less accurate. | `ref_rva`: 3 direct-memory candidates, 1 address-taking hit; `obj_rva`: 3 direct-memory candidates, 1 address-taking hit. |
| `Sequencer.UseSoftObjectPtrsForPreAnimatedMaterial` | bool (`ref`) | `true` | `true` | Selects soft-object pointers (the help’s stated default) rather than strong `TObjectPtr`s when referencing pre-animated state. | `ref_rva`: 3 direct-memory candidates, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. |

## Evidence limits and coverage audit

- Each entry has one consistent registry row and a captured snapshot. The batch contains one bool `var`, one bool `ref`, and three int32 `ref` entries. All five have exact-name Epic UE 5.9 reference defaults, matching their captured snapshots.
- Static scan totals are 19 `direct-memory-candidate` hits and 9 `address-taken` hits. Candidate instructions do not establish read/write direction or prove execution; address-taking is not a value access. The scan does not establish runtime behavior or whether startup overrides or `.ini` edits are accepted.
- These are the five names remaining after batch A, with no overlap. Batches A and B now cover all 30 unique exact-case `Sequencer.*` registered `var`/`ref` names.

Sources: [community CVar registry](cvar-community-registry.md), [preserved registry and snapshot attachments](EVIDENCE.md#community-sources), and [build address-reference scan](EVIDENCE.md#build-specific-static-analysis).
