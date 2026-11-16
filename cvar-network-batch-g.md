# Network CVar batch G: transport, packet ordering, and replication

This guide covers 25 registered network variables that were not covered by the earlier focused network pages. Types, help, and snapshots come from the preserved community attachments. Their capture build and method are unknown; a snapshot value is not assumed to be a default. Build-specific evidence is from the Marvel Rivals Shipping 1.1.4042190 address-reference scan. A direct memory instruction is a candidate read, not proof that an override is accepted or that the path runs in a match.

## Oodle packet compression

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.OodleSmallPacketDictThreshold` | int32 (`ref`) | `128` | When size-routed dictionaries are enabled, outgoing packets whose uncompressed size is strictly less than this many bytes use the small-packet dictionary. | One direct comparison candidate reads `ref_rva`; an address-taking match also exists. This supports a value-read candidate, but not the dictionary algorithm or compression benefit. |
| `net.OodleUseCrcCheck` | bool (`ref`) | `false` | Help is only “if use crc check.” It suggests a CRC-check toggle; which buffer is checked and what happens on a mismatch are undocumented here. | Seven direct load/compare candidates read `ref_rva`, plus address-taking. The scan does not identify the checked data or failure handling. |
| `net.OodleUseSizeRoutedDict` | bool (`ref`) | `true` | If true, route outgoing packets with `UncompressedBytes < net.OodleSmallPacketDictThreshold` to the small-packet dictionary. The strict less-than matters at the threshold boundary. | Three direct comparisons read `ref_rva`, plus address-taking. The related threshold is also read in the Oodle path. No runtime compression test was performed. |

## Pacing, object serialization, and packet collection

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.PacingTargetFps` | int32 (`ref`) | `30` | Phase-2 pacing fallback target used to calculate minimum per-frame byte replenishment as `BytesPerSecond / TargetFps`; intended to handle a zero-delta-time clock anomaly. Help states a default of 30. | Two direct integer-load candidates read `ref_rva`; the pacing formula itself was not traced here. |
| `net.PackageMap.DebugAll` | int32 (`var`) | `0` | Debugs PackageMap serialization for all objects. | The `ref_rva` is zero. The scan only has object-address setup candidates, not evidence of a consumer reading the value. |
| `net.PackageMap.DebugObject` | FString (`var`) | unreadable | Debugs serialization of an object whose partial name matches the configured string. The dump's non-text snapshot cannot be decoded reliably. | The `ref_rva` is zero; object-address setup candidates do not establish a value read or which serialization messages are logged. |
| `net.PackageMap.LongLoadThreshhold` | float (`var`) | `0.02` | Threshold in seconds for printing long-load warnings during object serialization. Preserve the registry's spelling `Threshhold`. | The `ref_rva` is zero; only object-address setup candidates were found. |
| `net.PacketCollect.Enable` | int32 (`ref`) | `0` | No help text was supplied. The name suggests a packet-collection switch, but what is collected, saved, or triggered is unknown. | One direct integer comparison candidate reads `ref_rva`; this establishes a value-check candidate only, not capture behavior or output. |
| `net.PacketCollect.MaxDurationTime` | float (`ref`) | `180` | No help text. The name suggests a duration limit for packet collection; units and whether it is a maximum capture length are unverified. | `ref_rva` has no direct value-read candidate in the saved scan; object-address matches are setup evidence only. |
| `net.PacketCollect.MaxWaitTime` | float (`ref`) | `5` | No help text. The name suggests a wait-time limit associated with packet collection, but the starting event, units, and timeout behavior are not established. | One direct float-load candidate reads `ref_rva`; surrounding collection logic was not traced. |
| `net.PacketCollect.UnreliableBunch` | int32 (`ref`) | `1` | No help text. The name may select unreliable bunches for a collection operation; the exact polarity and behavior are unresolved. | One direct comparison candidate reads `ref_rva`; it does not establish what is collected. |

## Packet ordering and partial bunches

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.PacketOrderCorrectionEnableThreshold` | int32 (`var`) | `1` | Number of out-of-order packet sequences required before packet-order correction is enabled. | `ref_rva` is zero; the scan found object-address setup candidates only. The correction algorithm was not reconstructed. |
| `net.PacketOrderMaxCachedPackets` | int32 (`var`) | `32` | Maximum number of packets cached while waiting for missing sequences before the missing packets are treated as lost. Help requires a power-of-two value. | `ref_rva` is zero; no value read was established by the object-address matches. |
| `net.PacketOrderMaxMissingPackets` | int32 (`var`) | `3` | Maximum number of missing packet sequences allowed before they are treated as lost. | `ref_rva` is zero; no value read was established by the object-address matches. |
| `net.PacketsLost.Connection` | int32 (`var`) | `1` | No help text. The name alone does not establish whether this toggles a statistic, loss simulation, or connection policy. | `ref_rva` is zero; only object-address setup candidates were found. |
| `net.PartialBunchReliableThreshold` | int32 (`ref`) | `0` | Help says that when a non-reliable bunch is split into this many or more partial bunches, it is sent reliably because every partial must arrive. The snapshot is `0`, while the Epic-reference default shown in the registry catalog is `8`; this is a snapshot/default discrepancy, not proof of effective runtime behavior. Zero-boundary handling is unknown. | Two direct integer loads read `ref_rva`. The reliable-send decision and zero case were not followed through control flow. |

## GUID remapping

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.OptimizedRemapping` | int32 (`var`) | `1` | Uses an optimized path to remap unmapped network GUIDs. The description does not define the algorithm, compatibility conditions, or the meaning of zero. | `ref_rva` is zero; only object-address setup candidates were found, so this scan does not establish a direct value read. |

## Dormancy, ping calculation, and queued bunch work

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.PendingDormant` | int32 (`ref`) | `1` | No help text; the name may relate to pending network dormancy, but that interpretation is not confirmed. | One direct integer comparison reads `ref_rva`. Its branch meaning is not identified. |
| `net.PingExcludeFrameTime` | int32 (`var`) | `0` | If true, subtracts game-frame time from calculated ping to approximate network-only ping. | `ref_rva` is zero; only object-address setup candidates were found. |
| `net.PingUsePacketRecvTime` | int32 (`var`) | `0` | Uses OS or receive-thread packet receive time for ping calculation, excluding time spent waiting for frame processing, according to help. | `ref_rva` is zero; only object-address setup candidates were found. Do not assume it is interchangeable with `net.PingExcludeFrameTime`. |
| `net.ProcessQueuedBunchesMillisecondLimit` | int32 (`var`) | `20` | Time limit for processing queued bunches in one frame; if processing exceeds the limit, continue on a later frame. `0` means unlimited. The registry's Epic-reference default is `30`, different from this captured value. | `ref_rva` is zero; no direct consumer read was identified by this scan. Actual scheduling and gameplay impact are unverified. |
| `net.ProfileReceive` | int32 (`ref`) | `0` | If `1`, include receive RPCs in NetProfile. | The `ref_rva` is address-taken but has no direct value-read candidate. Object setup writes are not evidence that receive profiling consumes it. |

## Push-model replication

| Exact name | Type | Snapshot | What the help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `net.PushModelSkipUndirtiedFastArrays` | bool (`ref`) | `true` | When true, include Fast Arrays when skipping objects that can safely be identified as not dirty. The registry catalog's Epic-reference default is `false`, unlike the snapshot. | One direct byte comparison reads `ref_rva`; the surrounding skip predicate and Fast Array dirty-state checks are not reconstructed. |
| `net.PushModelSkipUndirtiedReplication` | bool (`ref`) | `true` | When true, skip replicating objects that can safely be identified as not dirty. The registry catalog's Epic-reference default is `false`, unlike the snapshot. | Two direct byte comparisons read `ref_rva`; code still determines whether each object can safely be skipped. The snapshot alone does not prove the setting was active. |
| `net.PushModelValidateSkipUpdate` | bool (`ref`) | `false` | Enables detection when push-model state says an object can be skipped, but data is sent anyway. Help describes validation/diagnostics, not a way to force replication. | Two direct byte comparisons read `ref_rva`. The emitted diagnostic and validation path were not traced. |

## What these scans do and do not establish

- All 25 names have exact `var` or `ref` rows in [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). Captured values are from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452), whose build and capture method are unknown.
- The local address evidence is indexed in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Direct reads listed above are instruction candidates at `ref_rva`; the scanner does not establish full call paths or whether each path runs in a normal match. Entries with `ref_rva=0` are supported only by object-address setup candidates in this pass.
- The sample values and upstream defaults differ for `net.PartialBunchReliableThreshold`, `net.ProcessQueuedBunchesMillisecondLimit`, `net.PushModelSkipUndirtiedFastArrays`, and `net.PushModelSkipUndirtiedReplication`. This does not tell which source wins in the game or whether an override was applied.
- A syntactically valid startup override is not proof of registration, priority, server authority, or an in-game effect. No runtime override or network benchmark was performed.
- Source evidence and scanner limits: [`cvar-community-registry.md`](cvar-community-registry.md), [`cvar-registration-evidence-4042190.md`](cvar-registration-evidence-4042190.md), and [`sources/cvar-research/README.md`](EVIDENCE.md#build-specific-static-analysis).
