# Demo and replay CVar batch G

This guide covers 23 currently undocumented registered `demo.*` variables. Community help is source-provided intent; snapshot values and Epic UE 5.9 defaults are separate evidence. They do not establish the game build’s active path.

Static address references are from Marvel Rivals Shipping build `1.1.4042190`; direct-memory candidates are not full read/write or execution traces. No controlled startup config or live gameplay test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `demo.SkipMulticastRPC` | int32 (`ref`) | `2` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.SkipTickInFastForwarding` | int32 (`ref`) | `2` | `—` | 如果大于0，快速追帧时忽略level的更新，只处理数据包 *(assistant translation, unreviewed: If greater than 0, skip level updates during fast-forward catch-up and process packets only.)* | `ref_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.SkipTime` | float (`var`) | `0` | `0` | Skip fixed amount of network replay time (in seconds) *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.SourceLevelsTickInterval` | int32 (`ref`) | `100000` | `—` | 如果大于0，在死亡回放期间，主世界按给定帧间隔进行更新 *(assistant translation, unreviewed: If greater than 0, update the main world at the specified frame interval during death replay.)* | `ref_rva`: 10 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.SplitDuplicateTimeLimit` | int32 (`var`) | `5` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.Streaming.CompareCompressType` | int32 (`var`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.Streaming.CompressType` | int32 (`var`) | `4` | `—` | 0: NoCompress, 1: ZLib, 2: GZip, 3: LZ4, 4: ZSTD *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.Streaming.EnableServerCheckPointCompress` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.Streaming.ZSTDCompressLevel` | int32 (`var`) | `3` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.TickSendStreamingDataTime` | float (`var`) | `4` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.TimeDilation` | float (`var`) | `-1` | `-1` | Override time dilation during demo playback (-1 = don't override) *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.TimeoutReplayNetConnection` | float (`var`) | `15` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.UseAdaptiveReplayUpdateFrequency` | int32 (`var`) | `1` | `1` | If 1, NetUpdateFrequency will be calculated based on how often actors actually write something when recording to a replay *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.UseCustomDuplicationForReplay` | bool (`var`) | `true` | `—` | if true, enable custom duplication for replay. *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.UseNetRelevancy` | int32 (`var`) | `0` | `0` | If 1, will enable relevancy checks and distance culling, using all connected clients as reference. *(community registry help)* | `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.ViewTargetPriorityScale` | float (`var`) | `3` | `3` | Scale view target priority by this value when prioritization is enabled. *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.WithDeltaCheckpoints` | int32 (`var`) | `0` | `0` | If true, record checkpoints as a delta from the previous checkpoint. *(community registry help)* | `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.WithGameSpecificFrameData` | int32 (`var`) | `0` | `0` | If true, allow game specific data to be recorded with each demo frame. *(community registry help)* | `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.WithLevelStreamingFixes` | int32 (`var`) | `0` | `0` | If 1, provides fixes for level streaming (but breaks backwards compatibility). *(community registry help)* | `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.WithTimeBurnIn` | int32 (`var`) | `0` | `0` | If true, adds an on screen message with the current DemoTime and Changelist. *(community registry help)* | `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.checkpointready` | float (`var`) | `1` | `—` | loadcheckpoint延迟改时间后可以保证安全处理逻辑，单位秒 *(assistant translation, unreviewed: Delay after LoadCheckpoint so the safe-processing logic can run. Unit: seconds.)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.pctick` | int32 (`var`) | `1` | `—` | if 1, open game world player input tick, else close *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `demo.replayTask.TimeoutOpt` | int32 (`var`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- Untranslated or empty registry help remains unresolved rather than guessed from the name.
- Exact-name upstream defaults are references, not verified game defaults.
- Registry entries and scan matches do not prove `.ini` acceptance, player editability, or an in-game effect.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
