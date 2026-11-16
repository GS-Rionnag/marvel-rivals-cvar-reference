# AudioThread CVar batch A

This guide covers the eight currently uncovered exact-case `AudioThread.*` registry entries. Seven rows are CVar references/variables; `AudioThread.TaskPriority` is classified as a command and takes a named argument. Keep that distinction: the command is not a CVar override. Supplied help concerns audio-thread priority, command batching, waits, logging, suspension, and realtime decompression.

| Exact name | Type / kind | Snapshot | Epic UE 5.9 | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- | --- |
| `AudioThread.AboveNormalPriority` | `int32` (`ref`) | 0 | 0 | 0=Normal, 1=AboveNormal | Name appears in both scanned Shipping executable string inventories; `1` `ref_rva` and `3` `obj_rva` scan hits (2 direct-memory candidates, 2 address-taken), unvalidated. |
| `AudioThread.BatchAsyncBatchSize` | `int32` (`ref`) | 128 | 128 | When AudioThread.EnableBatchProcessing = 1, controls the number of audio commands grouped together for threading. | Name appears in both scanned Shipping executable string inventories; `2` `ref_rva` and `4` `obj_rva` scan hits (4 direct-memory candidates, 2 address-taken), unvalidated. |
| `AudioThread.EnableAudioCommandLogging` | `int32` (`ref`) | 0 | 0 | 0=Disbaled, 1=Enabled | Name appears in both scanned Shipping executable string inventories; `2` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 2 address-taken), unvalidated. |
| `AudioThread.EnableAudioThreadWait` | `int32` (`var`) | 1 | 1 | Enables waiting on the audio thread to finish its commands. 0: Not Enabled, 1: Enabled | Name appears in both scanned Shipping executable string inventories; `0` `ref_rva` and `3` `obj_rva` scan hits (2 direct-memory candidates, 1 address-taken), unvalidated. |
| `AudioThread.EnableBatchProcessing` | `int32` (`ref`) | 1 | 1 | Enables batch processing audio thread commands. 0: Not Enabled, 1: Enabled | Name appears in both scanned Shipping executable string inventories; `2` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 2 address-taken), unvalidated. |
| `AudioThread.SuspendAudioThread` | `int32` (`ref`) | 0 | 0 | 0=Resume, 1=Suspend | Name appears in both scanned Shipping executable string inventories; `2` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 2 address-taken), unvalidated. |
| `AudioThread.TaskPriority` | `—` (`cmd`) | — | — | Takes a single parameter of value `High`, `Normal`, `BackgroundHigh`, `BackgroundNormal` or `BackgroundLow`. This is a command signature, not a tunable CVar value. | Name appears in both scanned Shipping executable string inventories; `0` `ref_rva` and `4` `obj_rva` scan hits (3 direct-memory candidates, 1 address-taken), unvalidated. |
| `AudioThread.UseBackgroundThreadPool` | `int32` (`var`) | 1 | 1 | If true, use the background thread pool for realtime audio decompression. | Name appears in both scanned Shipping executable string inventories; `0` `ref_rva` and `4` `obj_rva` scan hits (3 direct-memory candidates, 1 address-taken), unvalidated. |

## Evidence limits

- The registry distinguishes `ref`, `var`, and `cmd`: references are not proof of registration, variables are registered-value candidates, and `AudioThread.TaskPriority` is a command. Neither the registry nor static scanning establishes loader support.
- Snapshot values are observations from `CVarDump.txt`, not recommended or guaranteed defaults. The command has no snapshot value.
- Epic UE 5.9 matches provide a comparison reference. They do not establish the game’s engine version or prove the same settings are active in Marvel Rivals.
- Printable strings and static address-reference hits do not establish execution, runtime mutability, or safe value ranges.
- `SuspendAudioThread` help explicitly allows suspending the thread; the effects on live audio are not tested here. Do not infer the game remains usable for all values.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [preserved source attachments](EVIDENCE.md#community-sources), [raw registry](EVIDENCE.md#community-sources), [snapshot](EVIDENCE.md#community-sources), [build CVar string inventory](EVIDENCE.md#build-specific-static-analysis), and [static address-reference scan](EVIDENCE.md#community-sources).
