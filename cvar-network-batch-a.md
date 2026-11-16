# Network CVar batch A

This page covers 25 exact `net.*` names from the community registry. The source attachment does not identify its game build or capture procedure. Its help text describes intended meanings; it does not prove the local Shipping build accepts overrides or follows every described path.

## Registry entries

| Exact name | Kind / type | Captured value | Help-based meaning and limits |
| --- | --- | ---: | --- |
| `net.ABSCUseRpcReplicate` | `ref` / bool | `false` | Source help says “If true, ABSReplicationSkipOther,” but does not explain the flag or replication behavior. Treat as unresolved. |
| `net.ActorChannelPool` | `var` / int32 | `1` | Nonzero enables actor-channel pooling to reduce memory use and object-creation work. |
| `net.AllowAsyncLoading` | `var` / int32 | `1` | Controls asynchronous loading of assets referenced by packets. Help says disabling it synchronously loads and may hitch; enabling it can defer packet processing until async loading completes. It mentions `net.DelayUnmappedRPCs` as a related control. |
| `net.AllowClientRemapCacheObject` | `ref` / bool | `false` | When enabled, clients may remap read-only cache objects while retaining the same NetGUID. Exact Marvel-specific applicability is unverified. |
| `net.AllowEncryption` | `var` / int32 | `1` | Help describes loading an encryption PacketHandler and using an `EncryptionToken`: `0` disables, `1` allows, and `2` requires it (the required mode is enforced server-side). This is connection/security configuration, not a graphics tweak. |
| `net.AllowPIESeamlessTravel` | `ref` / bool | `false` | Allows seamless travel in single-process Play-In-Editor (PIE). PIE is an editor context; the help does not suggest a normal retail-match setting. |
| `net.AllowReliableMulticastToNonRelevantChannels` | `var` / int32 | `1` | Allows reliable server multicast to non-relevant actors when an ActorChannel already exists. This describes server-side networking behavior. |
| `net.AllowRPCDoSDetectionBlocking` | `ref` / int32 | `1` | Overrides whether RPC denial-of-service detection may block RPCs (`0` off, `1` on). The registry help does not describe thresholds or policy. |
| `net.AllowRPCDoSDetectionKicking` | `var` / int32 | `1` | Overrides whether RPC denial-of-service detection may kick (`0` off, `1` on). The registry help does not describe thresholds or policy. |
| `net.AlwaysUpdateGuidReferenceMapForNetSerializeObjectStruct` | `ref` / bool | `false` | Requires `net.TrackNetSerializeObjectReferences`. When true, updates object-reference entries for NetSerialize struct properties continuously, rather than only when a GUID changes or becomes null; help says this should prevent stale property data when an actor reference becomes mapped. |
| `net.AOI.ClearNetGUIDMaped` | `ref` / bool | `false` | No help text. The AOI/NetGUID meaning cannot be safely inferred from the name alone. |
| `net.AOI.DestroySubObjects` | `ref` / bool | `false` | No help text. The exact AOI subobject-destruction behavior is unknown. |
| `net.AOI.EnableClear` | `ref` / bool | `true` | No help text. The setting's name suggests an AOI clear operation, but its condition and effect are unverified. |
| `net.AsyncAck.Enable` | `ref` / int32 | *(not in snapshot)* | Marvel-specific help says `1` defers the heavy part of `UNetConnection::ReceivedAck` to worker threads in the `UIpNetDriver::TickDispatch` async-ack phase; `0` flushes inline using the legacy path. Other values are not defined. |
| `net.bDebugChecksum` | `ref` / bool | `true` | No help text. Whether this enables a checksum diagnostic, and which data it covers, remains unknown. |
| `net.bEnableBunchCompress` | `ref` / bool | `true` | Help says it enables “special bunch compress,” without defining the compression format or its conditions. |
| `net.BitReader.EnsureOnOverflow` | `ref` / int32 | `1` | Ensures on BitReader overflow. Help says `net.BitReader.LogFatalOnOverflow`, if set, takes precedence. It does not specify the consequence of the ensure in this build. |
| `net.Bunch.DebugOpen` | `ref` / int32 | `0` | No help text; the debug behavior and accepted values are unknown. |
| `net.Bunch.TestPrint` | `ref` / int32 | `0` | No help text; what is printed and under what conditions are unknown. |
| `net.ChangeListMgrAcrossNetDrivers` | `ref` / bool | `false` | No help text. Sharing or changing a change-list manager across network drivers is only a name-based interpretation. |
| `net.Channel.SuppressUnopenedClose` | `var` / int32 | *(not in snapshot)* | Help says to suppress an unopened Cache/Destroyed Close. `0` is diagnostic-only until receive/ACK validation, including auxiliary data, completes. The accepted nonzero behavior is not further specified. |
| `net.CheckArchetypeBeforeActorCreation` | `var` / int32 | `0` | No help text. Its check point, values, and consequence are unknown. |
| `net.CheckNoLoadPackages` | `ref` / bool | `true` | When enabled, checks the no-load flag in `GetObjectFromNetGUID` before forcing a synchronous load for packages not marked fully loaded. |
| `net.ClientConnectionCleanupTimeLimitMS` | `var` / float | *(not in snapshot)* | Marvel-specific help calls this a shared soft time budget, in milliseconds, for pre-cleaning closed dedicated-server game connections' channels per `TickDispatch`. Nonpositive or nonfinite values retain synchronous cleanup. |
| `net.ClientUseOodleCompress` | `ref` / bool | `false` | Help names client-side Oodle compression but does not specify the negotiated conditions or which traffic is compressed. |

Captured values are from `CVarDump.txt`; except where source help explicitly labels a default, they are observations, not defaults or recommendations. Rows marked `ref` are reference entries in the source schema; `var` rows are variable entries. Neither category alone proves that the current game build registers the setting or that the loader can change its live value.

## Local Shipping-build scan

All 25 names have at least one reference in the saved address scan for build `1.1.4042190`. For entries with a nonzero `ref_rva`, the scan found direct-memory instruction candidates for most values: comparisons for `net.ABSCUseRpcReplicate`, `net.AllowClientRemapCacheObject`, `net.AllowPIESeamlessTravel`, `net.AllowRPCDoSDetectionBlocking`, `net.AlwaysUpdateGuidReferenceMapForNetSerializeObjectStruct`, `net.AOI.EnableClear`, `net.AsyncAck.Enable`, `net.bEnableBunchCompress`, `net.BitReader.EnsureOnOverflow`, `net.Bunch.DebugOpen`, `net.ChangeListMgrAcrossNetDrivers`, `net.CheckNoLoadPackages`, and `net.ClientUseOodleCompress`; `movzx` candidates for the `net.AOI.ClearNetGUIDMaped` and `net.AOI.DestroySubObjects` references; and `mov` candidates for `net.Bunch.TestPrint`. `net.bDebugChecksum` had an address-taking candidate but no direct value-read candidate in this scan.

The `var` entries in this batch have `ref_rva=0`; they have `obj_rva` address/write candidates, which do not establish a consumer reading the variable's value. Direct-reference candidates can also be writes or initialization, and the scan can miss indirect accesses. The instruction rows and scanner limitations are retained in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and the [source-method notes](EVIDENCE.md#build-specific-static-analysis). Name presence in the local printable-string inventory is static evidence, not proof of runtime registration.

## Override and editability status

The supplied `[Overrides]` syntax can express a line for each name, but this batch has no controlled runtime test showing that the game accepts a requested value, retains it after startup, or changes the live network path. The community snapshot and local code-reference scan cannot establish that. Use the shared [CVar editability evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) before labeling a variable editable. In particular, do not treat encryption, reliable multicast, or RPC-DoS controls as client-side performance switches based only on the values shown here.

## Sources

- Preserved community registry and snapshot: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452), and [source notes](EVIDENCE.md#build-specific-static-analysis).
- Exact Unreal Engine 5.9 name/default/help cross-check: [Community CVar registry](cvar-community-registry.md). Unreal help is upstream context, not proof of Marvel Rivals behavior.
- Local candidate names for build 1.1.4042190: [CVar executable inventory](EVIDENCE.md#build-specific-static-analysis).
- Loader behavior, runtime evidence levels, and mod-format limits: [CVar overrides](cvar-overrides.md).
