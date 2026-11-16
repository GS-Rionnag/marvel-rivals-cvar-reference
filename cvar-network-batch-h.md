# Network CVar batch H: RPC diagnostics, actor quantization, and socket recovery

This page covers 25 network variables from the community `var`/`ref` registry. The community attachment does not identify its game build or capture procedure. `CVarDump.txt` values below are observed snapshot values, not assumed defaults. Local instruction evidence comes from the saved address-reference scan for Marvel Rivals Shipping build `1.1.4042190`; address matches are candidates, not proof that a setting is accepted from startup config or that its path runs in a match.

## Quantization of newly spawned actors

| Exact name | Type | Snapshot | Meaning from the registry | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.QuantizeActorLocationOnSpawn` | bool (`ref`) | `false` | When enabled, quantizes the location of newly spawned actors to one decimal place, according to registry help. | One direct `ref_rva` value-read candidate plus address-taking. This is static use evidence; precision units and replication consequences were not independently measured. |
| `net.QuantizeActorRotationOnSpawn` | bool (`ref`) | `true` | When enabled, quantizes the rotation of newly spawned actors to one decimal place. | One direct comparison candidate plus address-taking. The rotation representation and angular units are not specified. |
| `net.QuantizeActorScaleOnSpawn` | bool (`ref`) | `false` | When enabled, quantizes the scale of newly spawned actors to one decimal place. | One direct comparison and one byte-load candidate plus address-taking. Scale component representation and visual/replication impact are not tested. |
| `net.QuantizeActorVelocityOnSpawn` | bool (`ref`) | `true` | When enabled, quantizes the velocity of newly spawned actors to one decimal place. | One direct comparison and one byte-load candidate plus address-taking. Velocity units and any error bound are not given. |

The captured states are mixed: rotation and velocity are true, while location and scale are false. These are snapshot observations, not proof of engine defaults or that the four settings share a common registration source in this build.

## Queued bunches and replication controls

| Exact name | Type | Snapshot | Meaning from the registry | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.QueueBunchesForLevelCollection` | int32 (`var`) | `1` | Any nonzero value queues bunches while a level collection is invisible. The help does not specify when the queue drains or which level-collection states qualify. | `ref_rva=0`; the scan found object-address setup candidates only, not a consumer reading the CVar value. |
| `net.QueuedBunchTimeoutSeconds` | float (`ref`) | `30` | Time in seconds to wait for queued bunches on a channel to flush before logging a warning. The help describes a warning threshold, not a disconnect or forced flush. | A direct float-load candidate reads `ref_rva`; warning behavior and queue path were not traced. |
| `net.QuitShareParam` | int32 (`ref`) | `2867` | The help says that when the count of unacknowledged reliable bunches in a single frame reaches this buffer size, the connection “will quit share replication.” That final phrase is ambiguous in the source text; do not silently reinterpret it as disconnecting the connection. | One direct comparison candidate reads `ref_rva`. The compared counter, response path, and exact meaning of “quit share replication” remain unresolved. |
| `net.REP.NeedSkipOpt` | bool (`ref`) | `true` | Changes the test for whether a `RemoteFunction` is queued: true requires actual bits (`> 0`); false uses the legacy always-true `>= 0` check. This documents a queue-eligibility condition, not a general RPC skip switch. | One direct comparison candidate reads `ref_rva`. The full queue path and runtime consequences were not followed. |

## RPC logging and DoS diagnostics

| Exact name | Type | Snapshot | Meaning from the registry | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.RPC.Debug` | int32 (`ref`) | `0` | Prints RPC bunches as they are sent: 0 disables printing, 1 enables it. The help does not say which log or whether both directions are included. | Four direct comparison candidates read `ref_rva`. Logging volume and performance cost were not measured. |
| `net.RPCDoSAnalyticsMaxRPCs` | int32 (`var`) | `20` | The top N RPCs, ranked by rate per second, to include in RPC DoS analytics. The help does not define the analysis window or treatment of ties. | `ref_rva=0`; object-address setup hits do not prove a direct value read in this scan. |
| `net.RPCDoSDetectionOverride` | FString (`var`) | unreadable | Registry help says it overrides RPC DoS detection per `NetDriver`, with `0` disabling and `1` enabling; example syntax names a `NetDriver` followed by a value. The captured FString bytes are not readable as text, so no snapshot setting can be reported. | `ref_rva=0`; only object-address setup candidates. The setting's server/client authority, accepted string grammar, and effect on any online server are not established. |
| `net.RPCDoSForcedRPCTracking` | FString (`var`) | unreadable | Help says one named RPC can force tracking; optional comma-separated chance and duration parameters are described, with a sample in the source help. The captured FString bytes are not readable as text. | `ref_rva=0`; object-address setup only. The actual parser, tracking scope, and server authority were not traced. The help suggests a diagnostic trigger, not a way to bypass a protection. |
| `net.RPCDoSScopeDebugging` | int32 (`ref`) | `0` | Toggles debugging/ensure behavior for RPC DoS Tick/Packet scopes. The help does not define which events produce output. | The scan found address-taking for `ref_rva` and object-address setup candidates, but no direct value read. |

The `RPCDoS*` names do not prove that a client-side override controls server-side detection. These entries may be meaningful only in a process that owns the relevant `NetDriver`; client authority and online behavior remain unverified. Do not treat the strings, analytics limits, or debug flags as evidence that protection is enabled or disabled on a remote server.

## RPC send-alarm settings

| Exact name | Type | Snapshot | What the sources establish | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.RPCSendAlarm.BufferCount` | int32 (`ref`) | `64` | No help text was supplied. The name suggests a buffer count, but the counted item and threshold semantics are unknown. | The scan found an address-taking reference and object-address setup candidates, but no direct `ref_rva` value read. |
| `net.RPCSendAlarm.Enable` | int32 (`ref`) | `3` | Object-table help maps 0 to None, 1 to Client, 2 to Server, and 3 to Both. It does not describe the alarm condition or message. | The scan found address-taking and object setup references only, not a direct value read. |
| `net.RPCSendAlarm.ErrorCount` | int32 (`ref`) | `60` | No help text; the name alone does not show whether this is a threshold, counter, or limit. | Address-taking and object-address setup candidates only; no direct `ref_rva` value read was found. |
| `net.RPCSendAlarm.OnlyOnce` | int32 (`ref`) | `0` | Object-table help maps 0 to None, 1 to Warning, 2 to Error, and 3 to Both. This code list appears severity-like, but its association with a variable named `OnlyOnce` is unclear. | Address-taking and object-address setup candidates only. Nearby strings associate other RPCSendAlarm names with this address, but do not resolve this metadata/name mismatch. |
| `net.RPCSendAlarm.ShowError` | int32 (`ref`) | `1` | No help text; the name does not establish whether it prints errors, controls a UI, or selects a severity. | Address-taking and object-address setup candidates only; no direct value read was found. |
| `net.RPCSendAlarm.WarningCount` | int32 (`ref`) | `40` | No help text; do not infer warning thresholds or counting units from the name. | Address-taking and object-address setup candidates only; no direct value read was found. |

For these six settings, the scan found address-taking references and object-pointer setup writes, but no direct `ref_rva` value-read candidates. The `Enable` and `OnlyOnce` help is the only supplied interpretation; the other captured integers are not proven defaults or effective thresholds.

## Packet sequence and receive-thread error handling

| Exact name | Type | Snapshot | Meaning from the registry | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.RandomizeSequence` | int32 (`var`) | `1` | Help says it randomizes the initial packet sequence and “can provide some obfuscation.” The text does not identify the sequence, algorithm, threat model, or cryptographic/security guarantees; this is not evidence of encryption or anti-cheat behavior. | `ref_rva=0`; the scan found object-address setup candidates only. |
| `net.RcvThreadShouldSleepForLongRecvErrors` | int32 (`var`) | `0` | Receive-thread policy for long-lasting `RecvFrom` errors: 0 do not sleep, 1 sleep, 2 exit the receive thread. The help does not define how an error becomes “long-lasting.” | `ref_rva=0`; object-address setup hits only. |
| `net.RcvThreadSleepTimeForWaitableErrorsInSeconds` | float (`var`) | `0` | Time in seconds for the receive thread to sleep when a socket operation returns a waitable error. The zero-value behavior is not explicitly documented. | `ref_rva=0`; no direct value read identified. |

## Socket recreation

| Exact name | Type | Snapshot | Meaning from the registry | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `net.RecreateSocketCheckBoth` | bool (`ref`) | `true` | When enabled, socket recreation checks both send and receive for timeout. The exact decision rule is not stated. | One direct comparison candidate reads `ref_rva`; timeout control flow was not followed. |
| `net.RecreateSocketCooldown` | int32 (`ref`) | `5` | Minimum interval in seconds between socket recreation attempts. The community registry's Epic-reference column lists 10 as an upstream default, while the snapshot is 5; this is a source/default discrepancy, not proof of an effective game value. | One direct integer-load candidate reads `ref_rva`; no retry loop was traced. |
| `net.RecreateSocketTimeoutThreshold` | float (`ref`) | `5` | Help says no received packet or send acknowledgement for this many seconds triggers socket recreation; `0.0` turns the threshold off. Epic's reference column lists upstream default 0 while the snapshot is 5. | Three direct float-load candidates read `ref_rva`; this does not establish the trigger side or that the setting can be changed through startup config. |

## Scope and editability

The `ref_rva` memory-load/comparison candidates support that many of these values are read somewhere in the Shipping binary. The scan does not recover the complete caller context, runtime `LastSetBy`, or the source that wins after startup. Entries with `ref_rva=0` have only CVar-object setup references in this saved scan; they are weaker evidence of a consuming code path. Community `var`/`ref` metadata is not a controlled confirmation that each line under `[Overrides]` is accepted. No runtime override or gameplay/network test was performed.

Captured values are observations, not recommended settings. In particular, packet sequencing, socket recovery, reliable bunch handling, or RPC processing can affect connectivity and protocol behavior; the help text and static evidence here are not a reason to change them on live servers.

## Sources

- Names, types, help, and reference RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), plus [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) for alternate RPCSendAlarm help.
- Snapshot values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); capture build and generation method are unknown.
- Build-specific instruction candidates: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), interpreted under the [scanner limitations](EVIDENCE.md#build-specific-static-analysis).
- Nearby strings: [build-specific text index](EVIDENCE.md#build-specific-static-analysis); adjacency alone does not prove which string belongs to which CVar.
