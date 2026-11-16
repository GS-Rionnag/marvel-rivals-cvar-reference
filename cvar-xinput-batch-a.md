# XInput CVar batch A

This guide documents the currently uncovered `XInput.ForceControllerStateUpdate` registry entry. Its supplied help describes forcing an XInput controller-state refresh on every frame and lists `0` as disabled and `1` as enabled. This wording does not establish how the game polls devices, which controllers use the path, or whether forced per-frame refresh improves input responsiveness.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `XInput.ForceControllerStateUpdate` | `int32` (`ref`) | `0` | — | Force XInput controller-state refresh on each frame. `0`: not enabled; `1`: enabled. No behavior for other values is given. | Name appears in both scanned Marvel Shipping executable inventories and CrashReportClient; 5 `ref_rva` hits (4 direct-memory candidates, 1 address-taken) and 3 `obj_rva` hits (2 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- The supplied description is about XInput state refresh, not proof of a Marvel Rivals input bug or a responsiveness optimization.
- Snapshot `0` is an observed value, not a guaranteed default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or startup `.ini` acceptance. No controller behavior has been tested with this override.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
