# Chaos collision feature and pruning CVars

This guide covers several remaining `p.Chaos.Collision.*` controls with direct code references in local Shipping build `1.1.4042190`. Captured values are community snapshot values, not verified defaults or recommendations.

| CVar | Type | Snapshot | Help / local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.EnableShapePairs` | bool | `true` | No registry help. At `0x142822A7B`, zero skips the shape-pair eligibility routine and returns false. With it enabled, the routine reads two shape counts, checks the count product against `MaxShapePairs`, and returns false when the threshold or other count checks fail. Exact caller semantics are not named. |
| `p.Chaos.Collision.MaxShapePairs` | int32 | `100` | No registry help. At `0x142822B34`, a positive value is compared with the product of two computed shape counts; when the product exceeds it, the helper returns false. This appears to cap candidate pair combinations in this path. |
| `p.Chaos.Collision.MaxShapePairsPerCollisionTask` | int32 | `40` | No registry help. The saved complete `.text` scan has no direct RIP-relative `ref_rva` memory-access candidate for this value. Its local build effect remains unknown; indirect reads are outside this scan's proof. |
| `p.Chaos.Collision.EnableEdgePrune` | bool | `true` | No registry help. At `0x142829BE6`, zero jumps around a loop over entries; nonzero enters the loop and runs per-entry checks. The exact data structure and meaning of a pruned entry are not identified. |
| `p.Chaos.Collision.EdgePrunePlaneDistance` | float | `3` | No registry help. At `0x1427E5ADD`, the float is loaded and converted to double precision, multiplied with a computed scalar, and placed in local data passed to a helper called once per loop entry. The threshold's units and the helper's final accept/reject meaning remain unknown. |
| `p.Chaos.Collision.CapsuleTriMeshSATCull` | bool | `false` | Registry help says it enables the SAT cull check in capsule-triangle collision. At `0x1427E0DBD`, zero branches around an alternate processing path; nonzero enters it. The code path is consistent with the help, but the exact SAT predicate and rejected cases were not recovered. |
| `p.Chaos.Collision.EnableCollisionManager` | bool | `true` | Registry help describes Chaos's collision manager as enabling ignored collisions between rigid bodies and gives default `1`. At `0x142B9B364`, zero skips a substantial processing path; nonzero enters it. This is consistent with the help but does not identify the manager's full policy. |
| `p.Chaos.Collision.EnableSubSurfaceCollisionPruning` | bool | `false` | No registry help. At `0x14292483B`, zero skips a subsequent block of scalar/vector processing; nonzero continues through it. The CVar name suggests a pruning feature, but the target data and effect are not recovered. |
| `p.Chaos.Collision.OneSidedTriangleMesh` | bool | `true` | No registry help. Two related compiled routines load this byte at `0x1427525A7` and `0x142753365` and copy it into local data passed onward. This supports that it configures triangle-mesh processing; its exact effect is unresolved. |

## Evidence and limits

- Types, help, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- The direct-reference scan is preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), and the [source notes](EVIDENCE.md#build-specific-static-analysis) record the local build identity/hash and scanner limitations.
- `EnableCollisionManager`, `EnableSubSurfaceCollisionPruning`, and `OneSidedTriangleMesh` references were inspected at the instruction addresses above; the final effect of the latter two paths remains unknown.
- The code proves local branches, threshold comparisons, and parameter reads. It does not show all indirect consumers, runtime settings, map coverage, or safe override ranges. No in-game test is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md), [Chaos CCD CVars](cvar-chaos-ccd.md), and [CVar overrides and loader syntax](cvar-overrides.md).
