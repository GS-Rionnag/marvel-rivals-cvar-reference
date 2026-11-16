# Tick CVar batch B: final registered entries

This batch documents the final 3 currently uncovered exact lowercase `tick.*` names. Together with the previously covered entries and batch A, it closes the 31-name `tick.*` `var`/`ref` registry inventory.

Community help records the source author’s stated purpose; it does not confirm active game behavior. Snapshot values come from `CVarDump.txt`; Epic UE 5.9 defaults are exact-name upstream references, not confirmed game-build defaults. Static address candidates come from Shipping build `1.1.4042190`; direct-memory matches do not distinguish reads, writes, comparisons, or initialization, and address-taking matches alone do not establish value use. No runtime or startup override test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help and separate upstream explanation | Static scan evidence |
| --- | --- | ---: | ---: | --- | --- |
| `tick.ParallelSimulatedTickMovement` | int32 (`ref`) | `0` | `—` | 0: Disable, 1: Enable *(community registry help)* | `ref_rva`: 5 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `tick.SecondsBeforeEmbeddedAppSleeps` | float (`var`) | `1` | `1` | When built as embedded, how many ticks to perform before sleeping *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `tick.ShowPrerequistes` | int32 (`var`) | `1` | `1` | When logging ticks, show the prerequistes; debugging. *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- Registry membership and snapshot presence do not establish startup `.ini` acceptance, player editability, or a live game effect.
- Epic references are upstream exact-name matches; version alignment with the game build is unconfirmed.
- Static address matches are not complete value-use traces. Missing scan hits do not prove a CVar is unused.

Sources: [community CVar registry](cvar-community-registry.md), [preserved research attachments](EVIDENCE.md#community-sources), and [build-specific CVar inventory](EVIDENCE.md#build-specific-static-analysis).
