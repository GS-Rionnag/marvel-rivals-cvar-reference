# Replay CVar batch A

This guide covers the first 25 alphabetically sorted currently undocumented registered `replay.*` variables. The registry help describes intended controls, while captured snapshots and exact-name Epic UE 5.9 values remain separate references.

Static references are from Marvel Rivals Shipping build `1.1.4042190`. Direct-memory candidates are not complete read/write or execution traces. No controlled replay session or startup override test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `replay.MontageErrorThreshold` | float (`ref`) | `0.1` | `—` | Tolerance level for when montage playback position correction occurs in replays *(community registry help)* | `ref_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.AddCache` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.BatchLoad` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.BlockRequest` | int32 (`var`) | `0` | `—` | server: >= 1, client: >= 2 *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.CancelRequestCount` | int32 (`ref`) | `0` | `—` | Real failed. To cancel request. *(community registry help)* | `ref_rva`: 0 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.ChunkDownloadTime` | float (`var`) | `0.2` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.ChunkQuickDownloadTime` | float (`var`) | `0.1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.ChunkUploadTime` | float (`var`) | `0.4` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.ClientPort` | int32 (`var`) | `9999` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.DownloadAllData` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnableBatchDownload` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnableIpv6` | int32 (`var`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnableStreaming` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnableTimeoutCompatible` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnableTls` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.EnterStreamingTimes` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.FailedCount` | int32 (`ref`) | `0` | `—` | Fake failed. *(community registry help)* | `ref_rva`: 0 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.HighPriorityDownloadNextChunkTime` | float (`var`) | `0.001` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.LimitUpdateEventMetaLen` | int32 (`var`) | `2000` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.LogClient` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.LogServer` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.MaxBatchDownloadChunk` | int32 (`var`) | `30` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.MaxChunkBuffTime` | float (`var`) | `5` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.MaxChunkFailedCount` | int32 (`var`) | `20` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `replay.grpc.MaxRetries` | int32 (`var`) | `10` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- Replay-related names do not by themselves show whether the setting affects recording, playback, networking, or a specific replay transport.
- Missing help and upstream matches are left unresolved.
- Registration and static references do not establish `.ini` acceptance, editability, or behavior in the live game.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
