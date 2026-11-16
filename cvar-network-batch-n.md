# Lower-case network CVar batch N

This guide records the next 25 registered lower-case `net.*` CVars left uncovered by the preceding network batches and focused guides. The order follows the community registry. “Snapshot” is the value captured in that dump; the Unreal Engine 5.9 value is an upstream reference match, not a verified Marvel Rivals default. The dump does not identify its game build or capture method.

Build evidence below comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may represent a read, comparison, or write; it does not establish an executed path. For a `var` entry, the scan found CVar-object setup/address references, not a `ref_rva` showing where its runtime value is consumed. Registration and an address hit do not prove that an `.ini` override is accepted or that a setting changes a live match. No runtime query or controlled gameplay test was performed.

## Dormancy tracking and replication diagnostics

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `net.TrackFlushedDormantObjects` | int32 (`ref`) | `1` | `1` | Tracks dormant subobjects when dormancy is flushed so they can be deleted if destroyed before the next `ReplicateActor`. *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TrackDormantObjectsByLevel` | bool (`ref`) | `false` | `false` | When true, the network object list maintains a set of dormant actors per connection per level. *(source: community help)* | 12 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TrackNetSerializeObjectReferences` | bool (`ref`) | `false` | `false` | Creates small layouts for Net Serialize structs with object properties; the supplied help says this can prevent some Shadow State garbage-collection crashes. *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.VerifyShareSerializedData` | int32 (`ref`) | `0` | `0` | Debug option to verify shared serialization data during replication. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.SupportFastArrayDelta` | int32 (`ref`) | `1` | `1` | Whether Fast Array Struct Delta Serialization is enabled. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TaskLogRepFunc` | bool (`ref`) | `false` | `—` | “Spew rep functions for debugging”; the dump does not explain the output destination, volume, or activation conditions. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TaskLogRepFuncPrerequistes` | bool (`ref`) | `false` | `—` | “Spew rep function prerequistes for debugging”; spelling is preserved from the registered CVar. The dump does not explain the output destination or activation conditions. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.ValidateReplicatedPropertyRegistration` | int32 (`var`) | `0` | `1` | Warns when replicated properties were not registered in `GetLifetimeReplicatedProps`. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. |
| `net.UseAdaptiveNetUpdateFrequency` | int32 (`var`) | `0` | `0` | If 1, calculates `NetUpdateFrequency` based on how often actors actually send something while replicating. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. |

## Queued bunches and asynchronous loads

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `net.TrackQueuedActorThreshold` | float (`ref`) | `0` | `0` | When greater than zero, tracks actors that spend longer than the threshold with queued bunches. The help gives seconds as the unit and describes this as debugging/analytics. *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TrackQueuedActorThresholdOwner` | float (`ref`) | `0` | `0` | When greater than zero, if the connection’s owning Controller or Pawn has queued bunches longer than the threshold, fires a CSV event to track it; described as debugging/profiling. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.TrackAsyncLoadingGUIDThresholdOwner` | float (`ref`) | `0` | `0` | When greater than zero, if the connection’s owning Controller or Pawn waits on async loads longer than the threshold, fires a CSV event; described as debugging/profiling. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |

## Packet verification and socket receive path

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `net.VerifyNetSessionID` | int32 (`ref`) | `1` | `1` | Controls verification of the packet SessionID value. *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.VerifyNetClientID` | int32 (`ref`) | `1` | `1` | Controls verification of the packet ClientID value. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.VerifyMagicHeader` | int32 (`ref`) | `0` | `0` | Controls verification of the packet magic header before processing. The supplied help describes disabling it during a magic-header transition while retaining temporary support for the old header. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.IpNetDriverUseReceiveThread` | int32 (`var`) | `1` | `0` | If true, the IpNetDriver calls the socket’s `RecvFrom` on a separate thread rather than the game thread. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. The registered snapshot differs from the UE 5.9 reference default. |
| `net.UseRecvMulti` | int32 (`var`) | `0` | `0` | Help says that on Unix/Linux, multiple packets can be retrieved per socket syscall, improving performance and allowing timestamp retrieval. The platform qualifier means this description does not establish an effect on the Windows game build. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. |
| `net.UseRecvTimestamps` | int32 (`var`) | `1` | `0` | Help says that with `net.UseRecvMulti` enabled on Unix/Linux, the kernel timestamp is retrieved per packet for more accurate ping calculations. The platform qualifier means this description does not establish an effect on the Windows game build. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. The registered snapshot differs from the UE 5.9 reference default. |
| `net.UseSocketsAdaptor` | bool (`ref`) | `false` | `—` | If true, the IpNetDriver uses the SocketsAdaptor. The dump does not specify implementation or compatibility requirements. *(source: community help)* | 10 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and control flow were not distinguished. |
| `net.UseInitialConnectMultiplier` | bool (`ref`) | `false` | `—` | If enabled, the first socket-recreation cooldown is doubled from `GNetRecreateSocketCooldown`. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |

## Other network and replay entries

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `net.TickAllOpenChannels` | int32 (`var`) | `0` | `0` | If nonzero, each net connection ticks all open channels every tick; the supplied help says leaving this off improves performance. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. |
| `net.UOpenReplayNetOpt` | int32 (`var`) | `1` | `—` | The help says “pause packet loss in replay connections” when true; the dump does not further explain the replay optimization. *(source: community help)* | CVar-object setup/address references only; no `ref_rva`, so runtime value consumption was not established. |
| `net.netease_protocol_log` | bool (`ref`) | `false` | `—` | If true, opens the Netease protocol log. The dump does not identify where it is written or its contents. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.rpc.CullDistance` | int32 (`ref`) | `2` | `—` | No explanatory help or upstream default was supplied in the available registry. The meaning and unit are unresolved. *(source: not described)* | 5 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |
| `net.UseLastOutRec` | int32 (`ref`) | `1` | `—` | No explanatory help or upstream default was supplied in the available registry. The behavior is unresolved. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); direction and execution path were not traced. |

## Interpretation and limits

- The descriptions above are registration help, not proof that these settings are exposed to the user or accepted from a config override in Marvel Rivals. This guide does not establish which of these CVars are safe, effective, or supported to change.
- Snapshot values and UE 5.9 reference defaults are recorded separately because they disagree for `net.IpNetDriverUseReceiveThread`, `net.UseRecvTimestamps`, and `net.ValidateReplicatedPropertyRegistration`.
- Several receive-path descriptions explicitly name Unix/Linux. They should not be generalized to the Windows Shipping build without code-path or runtime evidence.
- Static address-reference counts do not reveal whether a reference reads, writes, validates, or initializes a setting. No recommendation to change a network CVar follows from these counts.

Sources: [community CVar registry](cvar-community-registry.md), [community registry attachments](EVIDENCE.md#community-sources), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). See also [network batch M](cvar-network-batch-m.md) and [fast-array sharing notes](cvar-fast-array-sharing.md).
