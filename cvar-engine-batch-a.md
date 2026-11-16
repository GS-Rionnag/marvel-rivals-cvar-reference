# Engine CVar batch A

This guide documents the eight exact-case `Engine.*` entries in the current uncovered registry slice. Their supplied help covers map-load memory trimming, overlap deduplication, scene-query timing, leaked-world diagnostics, and on-screen warning filtering. The supplied names `SeceneQuery` and `SupressWarnings` are preserved exactly as registered (including apparent spelling errors).

Snapshot values are observations from a console dump, not proof of defaults. The Epic UE 5.9 registry cross-reference provides direct help/default evidence for the two rows marked below; similar game-build help is kept distinct from an Epic reference. Static scan hits are compiled-code candidates, not runtime tests.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 help/default | Supported interpretation | Static scan evidence |
| --- | --- | --- | --- | --- | --- |
| `Engine.DelayTrimMemoryDuringMapLoadMode` | `int32` (`ref`) | `0` | `0`: trim during `LoadMap` normally; `1`: defer until end of initial boot `LoadMap`; `2`: defer in every `LoadMap` call | Selects when the engine performs its memory trimming relative to map loading. No evidence here that changing it improves frame rate or reduces total memory use. | Static reference and object-address candidates |
| `Engine.MinNumOverlapsToUseTMap` | `int32` (`ref`) | `3` | `3`; minimum overlaps required before using a `TMap` for deduplication | An internal threshold for choosing a map-based deduplication path. The help does not say which overlap workload, performance tradeoff, or valid range applies. | Static reference and object-address candidates |
| `Engine.SeceneQuery.RecordTime` | `bool` (`ref`) | `false` | No Epic help/default supplied; game-build help repeats the exact name only | Likely related to timing scene queries from its name, but this remains an inference; exact behavior is undocumented in gathered help. | Static reference and object-address candidates |
| `Engine.SeceneQuery.Threshold` | `float` (`ref`) | `0.8` | No Epic help/default supplied; game-build help repeats the exact name only | “Threshold” has no identified unit, comparison, or subsystem semantics in gathered evidence. | Static reference and object-address candidates |
| `Engine.ShouldLogReferencesToLeakedWorldObjects` | `bool` (`ref`) | `false` | No Epic help/default supplied; game-build help: enables logging references preventing previous world objects from being cleaned up during map load | Diagnostic logging for references keeping old world objects alive during map loading. It is not evidence that it fixes a leak. | Static reference and object-address candidates |
| `Engine.SupressWarningsInOnScreenDisplay` | `int32` (`ref`) | `0` | `0`: show errors and warnings; `1`: show errors only, subject to the HUD duration setting | Filters warnings from the on-screen display at value `1`; help does not say it suppresses logging, notifications, or warnings elsewhere. | Static reference and object-address candidates |
| `Engine.VerifyLoadMapWorldCleanup.Severity.Shipping` | `int32` (`ref`) | `2` | No Epic help/default supplied; game-build help: leaked-world cleanup diagnostic severity; `0` disables tracing/logging, `1` logs an error, `2` raises an ensure, and `3` raises a fatal error | Controls diagnostics when a `UWorld` is detected as leaked during `LoadMap`. Exact meanings beyond the displayed levels should be checked against the full build help; it is not a cleanup behavior switch. | Static reference and object-address candidates |
| `Engine.VerifyLoadMapWorldCleanup.TraceMode.Shipping` | `int32` (`ref`) | `0` | No Epic help/default supplied; game-build help: trace detail; `0` direct references only, `1` full reference chains | Selects reference-tracing detail for leaked-world diagnostics. More detailed tracing may add diagnostic work; gathered sources do not quantify a cost. | Static reference and object-address candidates |

## Evidence limits

- The registry classifies these as `ref` entries. That does not prove that Marvel Rivals accepts them from an `.ini`, allows them to be changed at runtime, or uses the same implementation as the engine version documented by Epic.
- Snapshot values are not guaranteed defaults and may reflect the capture environment or later configuration.
- Static address/reference hits from Shipping build 1.1.4042190 show that corresponding data or references appear in the binary scan. They do not prove call frequency, reachable behavior, config loading, or user-visible effect.
- No live `.ini` or runtime experiment was performed for these entries. Editability and in-game impact remain unverified.

## Sources

Exact names, types, snapshots, and Epic cross-reference fields are in the [community registry](cvar-community-registry.md) and [`console_vars.tsv`](EVIDENCE.md#community-sources). Captured values are in [`CVarDump.txt`](EVIDENCE.md#community-sources). Game-build text and binary-scan context are documented in [build 1.1.4042190 context](EVIDENCE.md#build-specific-static-analysis), [build inventory](EVIDENCE.md#build-specific-static-analysis), and [research-source notes](EVIDENCE.md#community-sources).
