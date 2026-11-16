# SharedRep CVar batch B

This page covers 25 uncovered `Net.SharedRep.*` entries from the community registry. Snapshot values are observations from an attachment with unknown build and capture method, not verified defaults or recommendations. The static scan targets Marvel Rivals Shipping build `1.1.4042190`; a `ref_rva` memory-access match shows that the instruction touches the stored value, but does not recover the complete branch or prove that an INI override is honored.

## Scheduling, consideration counts, and actor-channel frames

| Exact CVar | Type | Snapshot | What the evidence supports | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `Net.SharedRep.ActorChannelFrameTimeout` | int32 (`ref`) | `0` | A nonzero value enables updates to a frame-like field in several replication-related paths. The observed code treats it as a zero/nonzero gate; it does not use the integer as a timeout count. | Seven direct reads are detailed in [SharedRep traffic control and actor-channel frame timeout](cvar-shared-rep-traffic-and-timeout.md). The field's source type, units, and timeout semantics remain unknown. |
| `Net.SharedRep.ClearPreSaveData` | int32 (`var`) | `1` | No registry help is supplied. The name alone does not establish which data is cleared or when. | The scan found object/setup references only, not a direct value read. No behavior or effect of the captured `1` is established. |
| `Net.SharedRep.ConsiderDormantCount` | int32 (`ref`) | `60` | No help is supplied. The name suggests a count associated with dormant actors, but does not say whether it is a per-frame budget, list size, or another limit. | Two direct accesses occur in shared-replication code: a comparison at `0x145202F45` and a load at `0x1452076D2`. The surrounding selection loop was not reconstructed. |
| `Net.SharedRep.ConsiderDormantGlobalCount` | int32 (`ref`) | `60` | No help is supplied. The name suggests a dormant-actor count tied to a global consideration path; scope and enforcement are unknown. | One direct load at `0x1451F9365` was found. The value's downstream use and whether it is a cap were not traced. |
| `Net.SharedRep.ConsiderGlobalCount` | int32 (`ref`) | `200` | No help is supplied. The name suggests a count for a global consideration list, but its unit and scheduling meaning are not defined. | Two direct loads at `0x1451F9BBF` and `0x1452076DA` appear in the saved scan. Their consumers were not traced. |
| `Net.SharedRep.ConsiderReconnectCount` | int32 (`ref`) | `50` | No help is supplied. The name suggests a reconnect-related count, but does not identify whether it is a limit or how often it is applied. | Three direct loads at `0x1451FA321`, `0x145203469`, and `0x1452076CA` were found. No reconnect scheduling or authority path was reconstructed. |

These four `Consider*Count` values are read by the Shipping binary, but the name and reads do not prove a “maximum actors per frame” interpretation. The captured values are not tested performance settings.

## Logging and diagnostics

| Exact CVar | Type | Snapshot | What the evidence supports | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `Net.SharedRep.Log.DormantInfo` | int32 (`ref`) | `0` | No registry help is supplied. The name suggests dormant-object logging, but output and levels are undefined. | The scan found no direct value-access candidate, only registration/object-address matches. A logging consumer was not confirmed. |
| `Net.SharedRep.Log.LimitGlobal` | int32 (`ref`) | `0` | No registry help is supplied. The name suggests logging related to a global limit, but does not identify the event or format. | No direct value-access candidate was found. The name alone is not evidence that setting it produces output. |
| `Net.SharedRep.Log.LimitReconnect` | int32 (`ref`) | `0` | No registry help is supplied. The name suggests logging related to reconnect limits; the exact condition and output are unknown. | No direct value-access candidate was found in the scan. |
| `Net.SharedRep.LogMacros.Net` | FString (`var`) | — (not in snapshot) | Registry help says “Set Net's Verbosity to VeryVerbose.” It does not explain the accepted string, logging categories, or how this shared-rep macro setting is applied. | No direct value consumer was matched. |
| `Net.SharedRep.LogMacros.Rep` | FString (`var`) | — (not in snapshot) | Registry help also says “Set Net's Verbosity to VeryVerbose.” The help does not define whether this changes a distinct category or shares the `Net` setting. | No direct value consumer was matched. |

## Serialization, reconnect, and RPC-related names

| Exact CVar | Type | Snapshot | What the evidence supports | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `Net.SharedRep.NetGUIDExport` | int32 (`var`) | `1` | No help is supplied. Do not infer whether it enables NetGUID export, records a state, or selects an export path. | Object/setup references only; no direct read of a `ref_rva` exists for this `var`. The consumer and server/client scope remain unknown. |
| `Net.SharedRep.OnlyShareGlobalConsider` | int32 (`ref`) | `1` | Registry help maps `1` to allowing shared serialization only for actors in that frame's `GlobalConsiderList`; off-cadence reconnect/dormant actors then do not advance the shared channel frame. `0` selects legacy behavior. | A comparison at `0x1451F7F2D` reads the value. This confirms a mode check, not the full serialization policy or match behavior. |
| `Net.SharedRep.Opt` | int32 (`var`) | `1` | No help is supplied. “Opt” is ambiguous and does not establish an optimization or its effect. | The scan found only object/setup references; it does not establish a runtime read. |
| `Net.SharedRep.PriorityDelta` | float (`ref`) | `0.2` | Static code shows this value scales several floating-point adjustments associated with shared-replication priority. Some uses add and others subtract, so the net effect on a score is condition-dependent. | Nine direct reads were traced in [the dedicated priority analysis](cvar-shared-rep-priority.md); the complete scoring model and runtime effect remain unresolved. |
| `Net.SharedRep.PropertyEnsure` | int32 (`var`) | `0` | No help is supplied. The name does not identify which property is ensured or what a value changes. | Object/setup references only; no consumer behavior was established. |
| `Net.SharedRep.RPC` | int32 (`var`) | `1` | No help is supplied. The name is insufficient to determine whether this controls RPC replication, diagnostics, or a feature state. | Object/setup references only. No direct read or RPC path was confirmed. |
| `Net.SharedRep.RPCChannelCreateRate` | float (`ref`) | `0.3` | No help is supplied. The name suggests a rate associated with RPC channel creation, but units, scale, and whether it is a limit or multiplier are unknown. | No direct `ref_rva` value access was found in the saved scan. Its name and snapshot do not establish runtime effect. |
| `Net.SharedRep.Replay` | int32 (`var`) | `1` | No help is supplied. The name does not identify a replay system, what is replayed, or whether this is a feature toggle. | Object/setup references only; no value consumer was identified. |
| `Net.SharedRep.ReplayVerifyRPC` | int32 (`var`) | `0` | No help is supplied. The name suggests RPC verification in some replay context, but that relationship and the verification behavior are unconfirmed. | Object/setup references only. No replay or RPC verification code path was traced. |

## Reconnect and tooling entries

| Exact CVar | Type | Snapshot | What the evidence supports | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `Net.SharedRep.Reconnect.ForceOnResume` | int32 (`ref`) | `1` | No help is supplied. The name suggests a force option when a connection resumes; it does not say what is forced. | A zero/nonzero comparison at `0x14520BF9A` reads the value. The branch effect and reconnect lifecycle were not recovered. |
| `Net.SharedRep.Reconnect.FrameInterval` | int32 (`ref`) | `10` | No help is supplied. The name suggests a frame interval in reconnect processing, but the interval's unit and exact action are unverified. | A load at `0x1452033CD` reads the value. The update loop and interval calculation were not reconstructed. |
| `Net.SharedRep.Reconnect.LogicPriority` | int32 (`ref`) | `0` | No help is supplied. The name suggests a priority mode or level for reconnect logic, but no value mapping is known. | A comparison at `0x14521B082` reads the value. This establishes a check, not the meaning of its branch. |
| `Net.SharedRep.Tool.Inherit.Connection` | int32 (`var`) | `1` | No help is supplied. The name may refer to inheritance by a tool from a connection, but the tool and inherited state are unidentified. | Object/setup references only; no value consumer was established. |
| `Net.SharedRep.Tool.Inherit.Demo` | int32 (`var`) | `1` | No help is supplied. The name may refer to inheritance from a demo/replay context, but that interpretation is not confirmed. | Object/setup references only; no value consumer was established. |

## What this says about changing them

The direct-read rows show that some values are consulted by this one Shipping build; they do not prove that a client startup `.ini` can change the value. Shared replication and reconnect behavior may be server-side or connection-specific. A local client setting cannot be assumed to control a remote server's actor selection, RPC, reconnect, or serialization decisions. None of these entries was tested with a controlled config change in a live match.

For more complete code observations on `ActorChannelFrameTimeout`, see [the existing frame-timeout analysis](cvar-shared-rep-traffic-and-timeout.md). For the other SharedRep families with traced branches, see [AOI](cvar-shared-rep-aoi.md), [priority adjustment](cvar-shared-rep-priority.md), and [traffic control](cvar-shared-rep-traffic-and-timeout.md). Registry help and captured values come from the preserved [CVar research attachments](EVIDENCE.md); address-scan coverage and limitations are described in [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
