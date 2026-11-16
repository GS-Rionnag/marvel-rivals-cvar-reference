# MessageBus CVar batch A

This is the next uncovered namespace batch: seven exact-case `MessageBus.UDP.*` entries. Their supplied help describes endpoint failure handling, a socket-error injection facility, and segmented-message resend limits. The names and help are consistent with transport diagnostics, but do not establish that these affect Marvel Rivals gameplay networking or player traffic.

Snapshot values are captured observations, not guaranteed defaults. The registry has no Epic UE 5.9 reference defaults for these rows. All seven have static address/reference candidates in the Shipping 1.1.4042190 scan; this does not show config loading or runtime behavior.

| Exact CVar | Type / kind | Snapshot | Supplied help and practical meaning | Static scan |
| --- | --- | --- | --- | --- |
| `MessageBus.UDP.BadEndpointPeriod` | `int32` (`var`) | `60` | Time in seconds between endpoint socket errors used to consider an endpoint bad. It describes a classification interval, not a retry delay. | 3 candidate hits |
| `MessageBus.UDP.ConnectionsToError` | `FString` (`var`) | Not present | When `MessageBus.UDP.InduceSocketError` is enabled, selects connections to fail; help says it may be a comma-separated list of `IP:port` entries. Exact parsing and whether an empty value disables matching are undocumented. | 3 candidate hits |
| `MessageBus.UDP.EndpointDenyListEnabled` | `bool` (`var`) | `true` | Enables an endpoint deny-list mechanism. A problematic endpoint may be tagged for exclusion; maximum attempts are governed by `MessageBus.UDP.MaxRetriesForBadEndpoint`. The help does not define when an endpoint is removed from the list. | 3 candidate hits |
| `MessageBus.UDP.InduceSocketError` | `int32` (`var`) | `0` | Any nonzero value forces outbound socket failure when the target IP matches `ConnectionsToError`; `MessageBus.UDP.ClearDenyList` can clear the list. This is explicitly a failure-induction control, not a performance optimization. | 3 candidate hits |
| `MessageBus.UDP.MaxRetriesForBadEndpoint` | `int32` (`var`) | `5` | Maximum retry attempts when a socket connection fails to reach an endpoint. The help does not describe backoff timing or whether retries are per message or connection. | 3 candidate hits |
| `MessageBus.UDP.SegmenterMaxResends` | `int32` (`var`) | `16` | Maximum attempts to resend data to an endpoint; values are clamped from 1 to 100 according to supplied help. | 3 candidate hits |
| `MessageBus.UDP.SegmenterTimeout` | `int32` (`var`) | `100` | Milliseconds to wait for a segment acknowledgment before retrying; values are clamped from 10 to 1000. | 3 candidate hits |

## Interpretation and limits

- The help uses “endpoint,” “socket,” “segment,” and “MessageBus.” It does not identify which Rivals subsystem consumes these controls. Do not assume they govern game-server connections, matchmaking, replication, or ordinary gameplay packets.
- `InduceSocketError` and `ConnectionsToError` are test/failure-injection controls by their own descriptions. The docs do not establish what endpoint values are safe or whether these are active in Shipping.
- The `var` registration class and snapshot values do not prove that `.ini` overrides are accepted, that changing values at runtime works, or that the setting is exposed in the retail build. No live override experiment was performed.
- Static scan hit counts are candidate references from the supplied binary scan, not proof of reachable code paths, successful writes, or runtime effects.

## Sources

Exact names, types, help and snapshots are in the [community registry](EVIDENCE.md#community-sources) and [community source notes](EVIDENCE.md#community-sources); captured values also appear in [community source notes](EVIDENCE.md#community-sources). Build-specific strings and scan provenance are documented in [build 1.1.4042190 context](EVIDENCE.md#build-specific-static-analysis), [build inventory](EVIDENCE.md#build-specific-static-analysis), and [research-source notes](EVIDENCE.md#community-sources).
