# Network CVar batch E: RPC rate limits and transport limits

This page documents 25 networking entries present in the preserved community `var`/`ref` registry. The attachment does not identify its game build or capture method. Snapshot values below are observations, not defaults. The installed executable scan is for Marvel Rivals Shipping build `1.1.4042190`; a local address match does not alone show that a user override is accepted or that the path executes in normal play.

## Marvel RPC rate-limit configuration

All twelve variables in this subsection are `var` rows with an object RVA but no `ref_rva`. The local scanner therefore found no direct `ref_rva` value reads for these entries. Their help describes a CVar-to-INI precedence interface, but the preserved attachments do not establish that a client-side override can change server policy or that these paths are active in this build. These settings appear relevant to server RPC governance; don't infer client authority from their presence in the registry.

| Exact name | Type | Snapshot | What the registry help establishes |
| --- | --- | --- | --- |
| `net.Marvel.RPCRateLimit.Allowlist` | FString | — | Empty defers to INI `Allowlist`; otherwise a comma-separated list of RPC names/keys replaces it. Escaping, whitespace handling, and matching rules are unspecified. |
| `net.Marvel.RPCRateLimit.DefaultBurst` | int32 | — | `-1` defers to INI `DefaultBurst`; any other value overrides the burst count. Valid range and how tokens are consumed are unspecified. |
| `net.Marvel.RPCRateLimit.DefaultQPS` | float | — | `-1` defers to INI `DefaultQPS`; `0` disables the default limit; otherwise the value overrides default queries-per-second. Whether the implementation uses a rolling window or token bucket is not documented here. |
| `net.Marvel.RPCRateLimit.Enable` | int32 | — | `-1` follows `[Marvel.RPCRateLimit] bEnable`; `0` disables, `1` enables. The local scan does not establish the owning subsystem or whether a client can set its effective policy. |
| `net.Marvel.RPCRateLimit.Enforce` | int32 | — | `-1` follows INI `bEnforce`; `0` observes, `1` drops RPCs that exceed limits. The help doesn't specify what an observed violation records. |
| `net.Marvel.RPCRateLimit.EnsureOnMissingQPS` | int32 | — | `-1` follows INI `bEnsureOnMissingQPS`; `0` disables and `1` enables a development-governance ensure when an RPC lacks a QPS value. Exact ensure behavior is not described. |
| `net.Marvel.RPCRateLimit.HitchBurstScale` | float | — | `-1` follows INI `HitchBurstScale`; otherwise overrides the hitch burst multiplier. The help doesn't give a default, clamp, or formula. |
| `net.Marvel.RPCRateLimit.HitchSuspendMs` | int32 | — | `-1` follows INI `HitchSuspendTimeMS`; otherwise overrides how long in milliseconds the hitch burst relaxation lasts. The exact start/end conditions are unknown. |
| `net.Marvel.RPCRateLimit.HitchThresholdMs` | int32 | — | `-1` follows INI `HitchThresholdMS`; otherwise overrides the hitch threshold in milliseconds. The measured frame/time source is unspecified. |
| `net.Marvel.RPCRateLimit.NoRateLimit` | FString | — | Empty defers to INI `NoRateLimit`; otherwise a comma-separated RPC-name/key list replaces the INI value. The relationship with `Allowlist` is not defined by the help. |
| `net.Marvel.RPCRateLimit.PerRPC` | FString | — | Empty defers to INI `PerRPC`; otherwise pipe-separated entries use `Key=Class.Func;QPS=N;Burst=N;Enforce=0|1`. The help does not specify key matching, parsing failures, or whether per-RPC values supersede all defaults. |
| `net.Marvel.RPCRateLimit.ViolationLog` | int32 | — | `-1` follows INI `bViolationLog`; `0` disables VIO logs and `1` enables them. Log destination, contents, and whether they are client-visible are unknown. |

The lack of snapshot values for these FString/int/float settings means only that `CVarDump.txt` has no matching rows. It does not mean that the variables are unset or disabled. Their names and help do not match entries in the preserved exact-name Epic 5.9 column.

## Connection, packet, and server sizing

| Exact name | Type | Snapshot | Meaning and build-specific evidence |
| --- | --- | --- | --- |
| `net.Iris.SaturateBandwidth` | bool | `false` | Registry/Epic 5.9 help says whether to saturate bandwidth, default false. The ref address was only address-taken in the saved scan; no value-read candidate was found. The name doesn't specify the transport or how saturation is generated. |
| `net.KeepAliveTime` | float | `0.2` | Community help says the effective value is `max(GNetKeepAliveTime, Driver->KeepAliveTime)`. A local `maxss` at `0x143E7FBF8` reads the referenced float, consistent with a maximum operation. The peer/global field and call context weren't traced, so this doesn't prove which driver or connection uses it. |
| `net.LogUnhandledFaults` | int32 | `1` | Help says `0` off, `1` log once, `2` log always; it warns unhandled faults may be deliberate depending on implementation. No direct `ref_rva` read was found; the object-RVA hits are setup/storage candidates. |
| `net.MagicHeader` | FString | — | Help describes a string of binary bits prepended to every game packet, with a maximum length of 32 bits. It is a packet-format setting, not a CVar for bandwidth or latency. No snapshot value or direct CVar value-read was found. |
| `net.MaxAggregateIPLogs` | int32 | `16` | Limits unique IPs included in aggregated pre-connection logging before that logging is disabled; documented range is 1–128. Local instructions read the `ref_rva` in comparisons, clamps, and moves around `0x144DB249A`–`0x144DD5428`, consistent with use in a logging cap. The surrounding path was not fully reconstructed. |
| `net.MaxChannelSize` | int32 | `0` | Exact Epic 5.9 help says this caps network channels across the server; values `<=0` defer to each connection's `DefaultMaxChannelSize`. Local scan found object-address setup matches only, not a direct value read. |
| `net.MaxClientGuidRemaps` | int32 | `100` | Registry help says maximum client resolutions of unmapped network GUIDs per tick. No direct `ref_rva` read was found; local object matches don't verify the per-tick loop or behavior at the threshold. |
| `net.MaxConnectionsToTickPerServerFrame` | int32 | `0` | Exact Epic 5.9 help describes a nonzero maximum number of channels with changed state replicated to them per server update. The local scan found object-address matches only. Snapshot `0` is a captured value; the source help does not state explicitly what zero means beyond saying “when non-zero.” |
| `net.MaxConstructedPartialBunchSizeBytes` | int32 | `65536` | Exact Epic 5.9 help says this is the maximum allowed size for partial bunches. Local code loads the referenced integer at `0x143B2F1A3`, `0x143B2F1F4`, `0x143B36524`, and `0x143B36580`, supporting local value-read evidence. The exact send/receive failure behavior wasn't traced here. |
| `net.MaxIPHitLogs` | int32 | `4` | Caps individual pre-connection log messages for one IP before further messages are aggregated. Local code compares/loads the referenced integer in the `0x144DB2325`–`0x144DD5410` region, consistent with thresholds used by the IP-log aggregation path. |
| `net.MaxNetStringSize` | int32 | `16777216` | Exact Epic 5.9 help says maximum size, in bytes, for strings sent or received by the netcode. No direct `ref_rva` read was found; the object-address match does not show which serialization path enforces the limit. |
| `net.MaxPlayersOverride` | int32 | `0` | Exact Epic 5.9 help says a value greater than zero overrides the standard max player count, useful for testing full servers. The local scan found object-address setup matches only. A client-side setting should not be assumed to alter server capacity. |
| `net.MaxRPCPerNetUpdate` | int32 | `2` | Exact Epic 5.9 help says this limits unreliable multicast RPC calls per network update and drops additional calls. The local scan found object-address matches only; it did not confirm whether the counter is per actor, connection, or server update in this fork. |

## Sources and limits

- Names, types, help, and reference metadata: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), summarized in the [community registry](cvar-community-registry.md).
- Snapshot values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); the capture build, method, and whether values were overridden are unknown.
- Build-specific references: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). `obj_rva` matches often reflect registration or storage; they are not proof of a runtime value read. `ref_rva` direct-memory candidates still need control-flow interpretation.
- Loader syntax is documented in [CVar override research](cvar-overrides.md#how-to-read-these-in-the-users-loader). No test here verified startup application, authority over a remote server, or gameplay effects.
