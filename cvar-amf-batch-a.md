# AMF CVar batch A

This note documents the currently uncovered `AMF.KeyframeInterval` registry entry. The supplied help describes the interval for sending IDR frames: every N frames, with values less than or equal to zero disabling interval-based IDR sending. The `AMF` prefix may refer to an encoder integration, but the registry alone does not establish which subsystem consumes this setting or whether it affects gameplay capture, replay, streaming, or another media path.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `AMF.KeyframeInterval` | `int32` (`var`) | `300` | — | Send an IDR frame every N frames. A value `<= 0` disables interval-based IDR sending. The help does not specify the consumer, other keyframe triggers, or whether the count is tied to encoded or source frames. | Name appears in both scanned Shipping executable string inventories; 0 `ref_rva` and 3 `obj_rva` matches (2 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- “IDR frame” is retained from the supplied help. The exact media pipeline and purpose are not identified by the registry.
- The snapshot value `300` is an observed value, not a guaranteed default or recommendation.
- The three address matches are static candidates. They do not establish runtime reads, writes, code execution, whether the setting is registered in the running build, or whether a startup `.ini` override is accepted.
- The `AMF` name may suggest an AMD media component, but that is a naming inference only; it is not evidence that this CVar controls a particular hardware encoder.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
