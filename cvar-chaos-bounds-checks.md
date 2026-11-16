# Chaos collision bounds-check CVars

This guide covers four bounds-related `p.Chaos.Collision.*` entries. The snapshot values are community captures, not verified defaults or recommendations. Static code observations refer to local Shipping build `1.1.4042190`.

| CVar | Type | Snapshot | Local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.EnableBoundsCheckInMidPhases` | bool | `true` | At `0x1428200C9`, zero takes a path that clears bit 0 in a local flag byte. When nonzero, the code also requires two local state bytes to be set before it sets that bit. The later consumer of the flag and the precise mid-phase check are not identified. |
| `p.Chaos.Collision.EnableBoundsChecksInBroadPhase` | bool | `true` | At `0x14282E3F4`, zero branches around a block of floating-point calculations; nonzero continues through it. The compared values are loaded from a caller-provided structure, but this trace does not map them to a specific bound representation. The CVar name points to a broad-phase bounds check. |
| `p.Chaos.Collision.AABBBoundsCheck` | bool | `true` | The saved direct `ref_rva` scan contains no RIP-relative memory-access candidate for this value. Its local read/effect remains unknown; indirect use is not excluded. |
| `p.Chaos.Collision.SphereBoundsCheck` | bool | `true` | The saved direct `ref_rva` scan contains no RIP-relative memory-access candidate for this value. Its local read/effect remains unknown; indirect use is not excluded. |

## Evidence and limits

- Types, reference addresses, and captured values come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- The full direct-reference scan is in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); its method and limitations are documented in the [source notes](EVIDENCE.md#build-specific-static-analysis).
- Only the broad-/mid-phase branches have direct local code observations here. The four names do not establish map coverage, runtime values, or safe overrides. No in-game test is recorded.

Related guides: [Chaos scene-query CVars](cvar-chaos-scene-queries.md), [Chaos collision feature and pruning CVars](cvar-chaos-shape-pairs-pruning.md), and [CVar overrides and loader syntax](cvar-overrides.md).
