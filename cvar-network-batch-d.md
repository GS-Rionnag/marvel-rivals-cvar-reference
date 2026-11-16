# Network CVar batch D: duplicate-send, handshake, and IP transport

This guide covers 25 entries from the preserved community `var`/`ref` registry. Its attachment does not identify the capture build or method; `CVarDump.txt` values are recorded as snapshots, not defaults. Local executable evidence is from Marvel Rivals Shipping build `1.1.4042190`.

## Evidence limits

Twenty-one entries are `var` rows with no `ref_rva` in the registry. The local address scan has some `obj_rva` matches, but those can reflect registration/storage and do not establish a feature-code value read. Four entries have a `ref` row: `net.GVarNetBunchDebugFlag2` has only an address-taking match; `net.GVarUseAckOpt`, `net.HandshakeEnforceNetworkCLVersion`, and `net.HandshakeResendInterval` have direct memory-instruction candidates. The listed instructions support that local code consults the latter three values, but without control-flow tracing they do not prove a user override reaches them or that the path runs during normal play.

All entries are syntactically representable using the supplied `name=value` `[Overrides]` format. No runtime application or behavior test was performed. A registry row or captured value does not by itself show that the Shipping game accepts a startup override.

## Opaque duplicate-send and ACK parameters

The first nine entries below have no community help or Epic 5.9 description in the registry. Their names cluster around duplicate-send behavior, and the first batch C guide documents a related `net.DuplicateSend*` family, but neither naming similarity nor snapshot values establish the exact mapping, units, valid ranges, or which code consumes them.

| Exact name | Type | Captured value | What can be concluded |
| --- | --- | ---: | --- |
| `net.GDuplicateParam2` | int32 (`var`) | `100` | No help or direct value-read evidence. Meaning, units, valid range, and relation to other `GDuplicate` names are unknown. |
| `net.GDuplicateParam3` | int32 (`var`) | `150` | No help or direct value-read evidence. The snapshot is not a threshold/default definition. |
| `net.GDuplicateParam4` | int32 (`var`) | `200` | No help or direct value-read evidence; exact function is unknown. |
| `net.GDuplicateParam5` | float (`var`) | `0.1` | No help or direct value-read evidence. Do not infer that this is a time interval or percentage from its type/value. |
| `net.GDuplicateParam6` | float (`var`) | `0.2` | No help or direct value-read evidence; exact function and units are unknown. |
| `net.GDuplicateParam7` | float (`var`) | `0.05` | No help or direct value-read evidence; exact function and units are unknown. |
| `net.GDuplicateParam8` | int32 (`var`) | `30` | No help or direct value-read evidence; exact function and valid range are unknown. |
| `net.GDuplicateRedundancy` | int32 (`var`) | `1` | No help or direct value-read evidence. The name does not establish what data, if any, is made redundant. |
| `net.GDuplicateSendMode` | int32 (`var`) | `2` | No help or direct value-read evidence. No mode labels are available, so `2` cannot be decoded. |
| `net.GEnableBunchPing` | int32 (`var`) | `1` | No help or direct value-read evidence. The name does not establish how a bunch ping is generated or used. |
| `net.GFastNakCount` | int32 (`var`) | `3` | No help or direct value-read evidence. Its relation to the maximum-count entry below is unverified. |
| `net.GMaxFastNakCount` | int32 (`var`) | `3` | No help or direct value-read evidence. The apparent cap implied by the name is not independently confirmed. |
| `net.GOptimizeFastNak` | bool (`var`) | `false` | No help or direct value-read evidence. The behavior or effect of enabling it is unknown. |
| `net.GVarNetBunchDebugFlag2` | int32 (`ref`) | `0` | Object reference is address-taken in the local scan, but no direct value read was found. The only help is “debug flag2”; it does not define flag bits or output. |
| `net.GVarUseAckOpt` | int32 (`ref`) | `1` | Help says `0` does not use ACK optimization and `1` uses it. A local integer comparison reads the reference at `0x143B2BBD5`, consistent with a boolean-like gate; no ACK behavior or performance effect was traced. |

## Handshake and consistency

| Exact name | Type | Captured value | Meaning and local evidence |
| --- | --- | ---: | --- |
| `net.HandshakeEnforceNetworkCLVersion` | int32 (`ref`) | `0` | Help says whether the stateless handshake enforces the Network CL version instead of leaving that to higher-level netcode. Local comparisons at `0x143EE572E` and `0x143EE5772` read the referenced value. The snapshot `0` is a captured value, not a recommendation; compatibility behavior was not tested. |
| `net.HandshakeResendInterval` | float (`ref`) | `1` | Help defines the delay between resending handshake packets without a received response. A local floating-point load at `0x143EF5B2E` reads the reference. Units are described by the source as delay but not explicitly named; packet timing and retry limits were not traced. |
| `net.IgnoreNetworkChecksumMismatch` | int32 (`var`) | `0` | Help says a true value ignores integrity checksums on package-map objects and warns this can cause issues with out-of-sync data. The local registry row has no `ref_rva`; no code read was established in the saved scan. This is a consistency-check bypass with a stated data-synchronization risk, not a performance recommendation. |

## Instant replay and IP transport

| Exact name | Type | Captured value | Meaning and limits |
| --- | --- | ---: | --- |
| `net.InstantReplayProcessQueuedBunchesMillisecondLimit` | int32 (`var`) | `8` | Help sets a per-frame time threshold for processing queued bunches during instant replay; if work exceeds it, processing continues in a later frame. Help says `0` means unlimited time. Local row has no `ref_rva`; use in live matches is not established. |
| `net.IpConnectionDisableResolution` | int32 (`var`) | `0` | Help says enabling it prevents future IP connections from using “resolution methods”; the type of resolution is not further defined. No local value-read evidence or connection-path trace. |
| `net.IpConnectionUseSendTasks` | int32 (`var`) | `0` | Help says the `IpConnection` schedules socket `SendTo` in a task-graph task so it can run off the game thread. This does not establish which socket backends, connections, or conditions use the path. |
| `net.IpNetDriverReceiveThreadMaxFrameRate` | int32 (`var`) | `240` | When `net.IpNetDriverUseReceiveThread` is true, this limits receive-thread frame rate. Help says lowering it increases sleeping and reduces CPU use but also increases latency. The receive-thread prerequisite is part of the help; whether the game enables that path is unverified. |
| `net.IpNetDriverReceiveThreadPollTimeMS` | int32 (`var`) | `250` | With the receive thread enabled, this is the millisecond timeout for `FSocket::Wait`; a negative value waits indefinitely, with socket shutdown expected to cancel it. No game-specific valid range or runtime use is established. |
| `net.IpNetDriverReceiveThreadQueueMaxPackets` | int32 (`var`) | `4096` | With the receive thread enabled, this caps packets waiting in its queue; extra arrivals are dropped. The help lists `1024` as the default, while the snapshot is `4096`; this is a source discrepancy, not proof of the game's default. |
| `net.IpNetDriverUseNetSmoothOpt` | int32 (`var`) | `1` | Help says it enables optimizations for `NetSmooth` clients. The local row has no `ref_rva`; optimization details and effects are unknown. |

## Sources

- Exact names, registration kind, type, help, and RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Local address matches: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Object-RVA registration/storage hits are not equivalent to feature reads.
- Related variables: [Network CVar batch C](cvar-network-batch-c.md), [Fast Array networking CVars](cvar-fast-array-sharing.md), and [the consolidated community registry](cvar-community-registry.md).
- Loader syntax and editability caveats: [CVar override research](cvar-overrides.md#how-to-read-these-in-the-users-loader).
