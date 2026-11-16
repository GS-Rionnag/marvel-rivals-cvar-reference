# `opt.*` CVar batch A

This guide documents the seven currently uncovered exact-case `opt.*` references. The names and supplied help concern multicast RPC handling, component culling, hit-shape processing, and monster RPC merging. One help string is in Chinese; its paraphrase below is a translation of the supplied text, not independent verification. These descriptions do not establish which gameplay paths use the settings in a live match.

Captured values are observations, not recommendations or verified defaults. No Epic UE 5.9 reference values were supplied. Static address-reference candidates from Shipping build 1.1.4042190 do not prove runtime execution, an effect, or acceptance by the startup `.ini` loader.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `opt.DisableLandedMulticastRpc` | `bool` (`ref`) | `false` | No help supplied. The name suggests disabling a Landed multicast RPC; the affected actor and consequences are unknown. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.DisableMonsterLandedMulticastRpc` | `bool` (`ref`) | `false` | Translated from supplied Chinese help: disables the monster Landed multicast RPC because FallState is already synchronized through property replication and an extra RPC is considered unnecessary. The exact actors and conditions are unspecified. | 1 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.EnableComponentCullByTag` | `bool` (`ref`) | `false` | No help supplied. The name suggests component culling based on tags, but the tags, culling conditions, and effect are undocumented. | 3 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.EnableHitShapeFastForwardingOptimization` | `bool` (`ref`) | `true` | No help supplied. The name suggests a fast-forwarding optimization for hit shapes; its algorithm and tradeoffs are unknown. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.EnableHitShapeNetTickTimeOptimization` | `bool` (`ref`) | `true` | No help supplied. The name suggests optimizing hit-shape work using network tick time; the actual condition and behavior are unknown. | 3 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.EnableHitShapeVisibilityOptimization` | `bool` (`ref`) | `false` | No help supplied. The name suggests a visibility-related hit-shape optimization; its scope and correctness conditions are unknown. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `opt.MergeMonsterRpc` | `bool` (`ref`) | No snapshot row | Supplied help: “merge monster setlocation rpc.” This suggests merging monster SetLocation RPCs, but batching rules and effect are not described. | 2 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |

## Interpretation and limits

- Except for the one supplied Chinese description and the short `MergeMonsterRpc` phrase, the table's possible meanings come from names and are not confirmed definitions.
- Snapshot values are not proof of defaults for the installed game build. `opt.MergeMonsterRpc` has no captured value in the supplied snapshot.
- `ref` classification and static scan candidates do not prove that these values can be changed through `[Overrides]` or that changes are safe.
- Address candidates may reflect initialization, writes, or address passing; they do not prove a particular runtime branch or visible outcome.

## Sources

Exact names, types, supplied help, and captured values are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner limitations are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
