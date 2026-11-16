# Network CVar batch F: bunch limits, ping, replication, and compression

This page covers 25 additional networking variables from the community `var`/`ref` registry. The registry and `CVarDump.txt` do not identify the capture build or method. Snapshot values below are observations, not defaults or recommendations. Static references are from Marvel Rivals Shipping build `1.1.4042190`; an instruction that reads a registered value shows a local code read, not that a startup override is accepted or that the code runs on every connection.

## Serialized network-export limits

| Exact name | Type | Snapshot | Meaning from help | Local read evidence |
| --- | --- | ---: | --- | --- |
| `net.MaxSerializedNetExportGroups` | int32 (`ref`) | `65536` | Maximum number of network export groups expected in a received bunch. The help does not state whether this is a clamp, allocation limit, or validation threshold. | Four direct `ref_rva` memory candidates, including three loads into `r9d` and one comparison. Exact use is not reconstructed. |
| `net.MaxSerializedNetExportsPerGroup` | int32 (`ref`) | `131072` | Maximum number of network exports expected in each group in a received bunch. No validation/failure response or supported range is specified. | Three direct `ref_rva` load candidates (`mov r9d,...`). |
| `net.MaxSerializedNetGuids` | int32 (`ref`) | `2048` | Maximum number of network GUIDs expected in a received bunch. The help does not define whether the value rejects, caps, or preallocates data. | One direct `ref_rva` load candidate (`mov r9d,...`). |
| `net.MaxSerializedReplayNetGuids` | int32 (`ref`) | `32768` | Maximum number of network GUIDs expected in replay export data, distinct from the regular bunch limit above. | One direct `ref_rva` load candidate (`mov r9d,...`). |

These are receive/serialization resource bounds by their descriptions. Do not raise them based only on the unusually high snapshot values; the dump is not a default manifest, and the code path's handling of malformed or oversized input was not traced.

## RPC size thresholds and connection settings

| Exact name | Type | Snapshot | Meaning from help | Local read evidence |
| --- | --- | ---: | --- | --- |
| `net.MaxSizePerRpc` | float (`ref`) | `2097150` | Maximum RPC size in bytes according to help. The help says exceeding the threshold logs an error and explicitly labels that behavior “not shipping.” | No direct `ref_rva` value-load candidate in the saved scan; one reference was address-taken only. |
| `net.MaxSizePerRpcClient2ServerCrash` | float (`ref`) | `524288` | Client-to-server RPC size threshold whose help says an oversized RPC would crash; the same help labels this behavior “not shipping.” | No direct value-load candidate; one address-taking reference only. |
| `net.MaxSizePerRpcClient2ServerWarning` | float (`ref`) | `1024` | Client-to-server RPC size threshold whose help says an oversized RPC logs an error; help labels the behavior “not shipping.” | No direct value-load candidate; one address-taking reference only. |
| `net.MinHandshakeVersion` | int32 (`ref`) | `3` | Minimum numeric stateless-handshake protocol version supported. It does not document the meaning of version numbers or negotiation behavior. | Seven direct memory candidates include byte/int loads and comparisons against the value. The minimum-version decision path was not followed. |
| `net.MinSingleTimeOut` | int32 (`ref`) | `10` | Help only says “Min Timeout for one connection.” Units, which timeout, and whether the value is a minimum duration or retry threshold are unspecified. | One direct `ref_rva` floating-register transfer candidate (`movd`); no surrounding timeout path was traced. |

## NAK queue and replication behavior

| Exact name | Type | Snapshot | Meaning from help | Local read evidence |
| --- | --- | ---: | --- | --- |
| `net.NakCountPerTime` | int32 (`ref`) | `20` | Help says values at or below zero stop use of the NAK queue. The name suggests a count over time, but the time window and effect of positive values are not described. | Two direct comparison candidates read the value. |
| `net.NakQueueForLos` | int32 (`ref`) | `500` | Help says the NAK queue begins to be used after a connection's total lost-packet count exceeds this value. The counter scope/reset behavior is unspecified. | One direct load candidate reads the value; the threshold comparison path was not reconstructed. |
| `net.OnlyRepAnimMontageWhenChanged` | int32 (`ref`) | `1` | Enables replicating an animation montage only when it has changed. Help does not define the change test or initial-send behavior. | Two direct comparisons read the value. This supports local branch use, but not the network-visible result of changing it. |
| `net.OnlyRepMoveWhenChanged` | int32 (`ref`) | `1` | Enables replicating movement only when it has changed. Help does not define the movement fields, tolerance, or scheduling. | One direct comparison candidate reads the value. |
| `net.Montage.Debug` | int32 (`var`) | `0` | Help: 0 prints nothing; 1 prints AnimMontage replication information client-side as montages play. | `ref_rva` is zero; this saved reference scan does not show the CVar value being consumed. Treat as a registry/help-only diagnostic setting. |

## NetPing controls

| Exact name | Type | Snapshot | Meaning from help | Local read evidence |
| --- | --- | ---: | --- | --- |
| `net.NetPingEnabled` | int32 (`var`) | `0` | Mode selector: 0 off, 1 client, 2 server and client, 3 server only. Help describes centralized ping tracking plus ICMP/UDP ping handling. | `ref_rva` is zero; the scan does not establish a read or that the ping interface is enabled in this build. |
| `net.NetPingICMPInterval` | int32 (`ref`) | `5` | ICMP ping interval in seconds. | Two direct `ref_rva` loads. |
| `net.NetPingTimeoutDisableThreshold` | int32 (`var`) | `15` | Number of ICMP/UDP ping attempts at a 100% failure/timeout rate before the system gives up and disables pings. The help does not explain how the rate is calculated or when the count resets. | `ref_rva` is zero; no direct value read was found in this scan. |
| `net.NetPingTypes` | FString (`var`) | Not reliably decoded | Comma-delimited list of `EPingType` pings, optionally paired with an `EPingAverageType`; help gives examples such as `RoundTrip=None` and `ICMP=MovingAverage`. Parsing and accepted enum values are not specified. | `ref_rva` is zero; no read candidate was found. The snapshot contains a non-text replacement character, so it is not quoted as a value. |
| `net.NetPingUDPInterval` | int32 (`ref`) | `5` | UDP ping interval in seconds. | Two direct `ref_rva` loads. |
| `net.NetPingUDPPort` | int32 (`ref`) | `22222` | Port used for the `UDPQoS` ping type. The help does not describe port validation or server requirements. | One direct `ref_rva` load. |

All these entries describe a ping measurement/tracking subsystem. The static evidence does not show a match-telemetry or latency benefit, nor does it establish which ping modes the game exposes to a client.

## Server rate and Oodle compression

| Exact name | Type | Snapshot | Meaning from help | Local read evidence |
| --- | --- | ---: | --- | --- |
| `net.NetSpeedLimit` | int32 (`ref`) | `0` | Limits packet send speed on the server. The help provides no units or special meaning for zero. This is server-side policy by its own description; client authority is not established. | Four direct `ref_rva` load candidates. The packet-scheduling path and units are not recovered. |
| `net.OodleClientEnableMode` | FString (`var`) | Not reliably decoded | Selects when to enable Oodle compression on the client and overrides the `.ini` `ClientEnableMode` setting. Accepted mode strings and parsing are not included in registry help. | `ref_rva` is zero; no direct value read found. |
| `net.OodleClientLazyDictLoad` | bool (`ref`) | `true` | When true, the client defers loading the Oodle compression dictionary until first use. Help says it affects only the client. | Four direct `ref_rva` comparisons read the bool; dictionary-loading behavior was not traced. |
| `net.OodleMinSizeForCompression` | int32 (`ref`) | `0` | Minimum outgoing packet size considered for compression, excluding overhead from later packet-handler components. Help does not define zero's behavior. | One direct `ref_rva` load candidate. Compression threshold behavior was not traced. |
| `net.OodleServerEnableMode` | FString (`var`) | Not reliably decoded | Selects when to enable Oodle compression on the server and overrides the `.ini` `ServerEnableMode` setting. The accepted strings and authority path are unknown. | `ref_rva` is zero; no direct value read found. |

The two `EnableMode` FString snapshots are not reliably decoded from the preserved text dump. Do not infer their selected modes from replacement characters or infer that a client-side config can change server compression policy.

## Sources and limits

- Registry kinds, types, help, and reference RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); consolidated upstream descriptions/defaults are in the [community registry](cvar-community-registry.md).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The file's build, capture method, and whether values are defaults are unknown.
- Local instruction candidates: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), matched by the documented [address-reference scanner](EVIDENCE.md#method-and-reproducibility). A direct-memory candidate can be a load, comparison, or write; the operations noted above support read candidates where identified, not complete control-flow semantics.
- The supplied `[Overrides]` syntax can express a `name=value` line. Nothing in this static review proves the game accepts a particular value, that a client can affect server policy, or that an observed branch changes normal gameplay. No runtime test was performed.
