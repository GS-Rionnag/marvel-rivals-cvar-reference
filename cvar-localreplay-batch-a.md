# localReplay CVar batch A

This guide documents all seven exact-case `localReplay.*` entries classified as variables. They appear to concern replay recording, buffering, caching, and loading, but five have no supplied help text. Interpret those names as hints only: the registry does not define file format, unit, capacity, persistence, or networking behavior for undocumented settings.

Captured values are observations, not recommended or verified defaults. No Epic UE 5.9 reference values were recorded for these entries. The scanned Shipping build 1.1.4042190 has static object-address candidates for each name; these do not prove live replay activity, runtime reads/writes, or startup `.ini` acceptance.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `localReplay.AllowLiveStreamDelete` | `int32` (`var`) | `1` | No help supplied. The name suggests control over deleting a live stream, but the object, conditions, and value semantics are unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.ChunkUploadDelayInSeconds` | `float` (`var`) | `20` | No help supplied. The name suggests a delay in seconds before uploading a chunk; it does not define when the delay starts or which upload path is involved. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.MaxBufferedStreamChunks` | `int32` (`var`) | `10` | No help supplied. The name suggests a maximum count of buffered stream chunks, but eviction and overflow behavior are unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.MaxCacheSize` | `int32` (`var`) | `10485760` | No help supplied. The name suggests a maximum cache size; the unit, cache type, and enforcement behavior are unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.MaxFriendlySerializeBytes` | `int32` (`var`) | `65536` | Maximum allowed serialized bytes when reading the friendly name from a file header. The help describes a parsing limit, not the maximum size of the whole replay file. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.MinLoadNextChunkDelaySeconds` | `float` (`var`) | `3` | Minimum time to wait between conditional chunk loads. The help does not say what makes a load conditional or how the minimum affects playback timing. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `localReplay.ReplayRecordingMinSpace` | `int32` (`var`) | `20971520` | Minimum space needed to start recording a replay. The help does not state units or whether space is checked again during recording. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |

## Interpretation and limits

- The two supplied descriptions and the `localReplay` prefix point to replay-related settings. They do not prove that replay recording or streaming is enabled or used in the live game.
- Name-based readings for rows without help are hypotheses, not documented semantics.
- Snapshot values are not recommendations or confirmed defaults for the current game build.
- Static address matches can reflect initialization or address passing; they are not proof of executed runtime code, effects, or override acceptance.

## Sources

Names, types, help, and snapshot observations are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner limitations are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
