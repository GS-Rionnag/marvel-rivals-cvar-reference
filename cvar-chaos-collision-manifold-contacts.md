# Chaos collision manifold and contact CVars

This page covers twenty `p.Chaos.Collision.*` settings that were not in the focused collision guides. It uses the community registry/snapshot and static disassembly of the installed Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommendations.

## Variables

| CVar | Type | Snapshot | What the evidence supports |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.AllowLevelsetManifolds` | bool | `true` | Registry help says it enables incremental manifolds for levelset-levelset collisions and warns that rotation in small pieces makes the feature work poorly. The local scan finds registration references but no direct RIP-relative value-read candidate; the runtime gate is not independently confirmed. |
| `p.Chaos.Collision.AllowParticleTracking` | bool | `true` | Registry help says particles can track collision constraints when `DoBufferCollisions` is enabled. No direct value-read candidate was found in the saved scan, so treat this as the registry's description rather than a verified local runtime path. |
| `p.Chaos.Collision.DebugDrawProbeDetection` | bool | `false` | Registry help describes drawing probe-constraint detection. The scan found registration references but no direct value-read candidate; whether this draw path is reachable in this Shipping build is unresolved. |
| `p.Chaos.Collision.GBFCharacteristicTimeRatio` | float | `1` | Registry help calls it the ratio between characteristic time and `Dt`. The saved scan found registration references but no direct value read, so its runtime formula is not established. |
| `p.Chaos.Collision.Manifold.CapsuleAxisAlignedThreshold` | float | `0.8` | A capsule contact path compares a computed scalar against this value. When the comparison does not take the axis-aligned branch, it proceeds to a separate deep-penetration check. The compared scalar's geometric definition is not recovered. |
| `p.Chaos.Collision.Manifold.CapsuleDeepPenetrationFraction` | float | `0.05` | The capsule path multiplies the smaller of two shape-related values by this fraction, takes an absolute value, and compares the result with another geometry-derived scalar. A failed comparison exits that contact path. Exact units and intended penetration interpretation are unknown. |
| `p.Chaos.Collision.Manifold.CapsuleMinContactDistanceFraction` | float | `0.1` | The value is loaded into solver-local data in four repeated collision routines. This shows it is an input to those paths; its exact downstream formula is unresolved. |
| `p.Chaos.Collision.Manifold.CapsuleRadialContactFraction` | float | `0.25` | The value is loaded in a capsule/triangle contact path and enters its floating-point calculations. The remaining data flow does not establish the resulting contact geometry, so the radial-fraction interpretation remains based on the name. |
| `p.Chaos.Collision.Manifold.CullDistanceMarginMultiplier` | float | `1` | The registry row has an object/registration reference, but the saved direct-reference scan found no RIP-relative value-read candidate. Its effect on cull distance is not verified locally. |
| `p.Chaos.Collision.Manifold.EdgeNormalThreshold` | float | `0.9` | In a triangle-contact routine, a computed weighted scalar is made absolute and compared with this value. The result selects between later contact-processing paths. This is consistent with a normal threshold, but the compared vector's exact construction is unresolved. |
| `p.Chaos.Collision.Manifold.EnableFrictionRestore` | bool | `true` | A contact-processing path checks this flag before a loop. If it is zero, or earlier checks succeed, the routine skips the later friction-position path. This supports a gate on friction restoration work; the restored state and helper semantics are unknown. |
| `p.Chaos.Collision.Manifold.EnableGjkWarmStart` | bool | `true` | The registry row has registration references but no direct RIP-relative value-read candidate in the saved scan. The name suggests reuse of prior GJK solver state, but that behavior is not established by this build trace. |
| `p.Chaos.Collision.Manifold.FrictionPositionTolerance` | float | `1` | After the friction-restore gate, this value is squared and converted to double precision before comparisons in a contact-count loop. This confirms it supplies a distance-like tolerance to that path; the compared quantities and output are not fully mapped. |
| `p.Chaos.Collision.Manifold.MatchNormalTolerance` | float | `0.02` | Registry help says it is a tolerance on the normal dot product for deciding whether contact points match. The local routine loads it alongside `MatchPositionTolerance` and uses it in the normal-comparison arithmetic, consistent with that description. |
| `p.Chaos.Collision.Manifold.MatchPositionTolerance` | float | `0.3` | Registry help says this is a fraction of object size. The local routine finds the maximum of three bounds dimensions, scales it by this value, squares the result, and compares it against a squared three-axis point separation. This directly supports a size-relative point-match distance. |
| `p.Chaos.Collision.Manifold.MinFaceSearchDistance` | float | `1e-06` | The value is loaded in multiple manifold/face-search routines; one observed site applies a `maxss` with it. The data flow confirms a lower-bound input to those calculations, but not which geometric distance is bounded. |
| `p.Chaos.Collision.Manifold.SphereCapsuleSizeThreshold` | float | `0.5` | A sphere/capsule path multiplies the sum of two shape-related dimensions by this value and compares it with another size-like value. One comparison result exits the path. The exact size fields and boundary meaning are unresolved. |
| `p.Chaos.Collision.Manifold.TriangleConvexMarginMultiplier` | float | `0.5` | A triangle/convex path multiplies a shape-related scalar by this CVar and stores the result in local solver data. This supports a margin multiplier in that path, but the input scalar and resulting margin units are not identified. |
| `p.Chaos.Collision.Manifold.TriangleNormalThreshold` | float | `0.75` | In a triangle-contact routine, a computed scalar is compared with this threshold; the result changes a local iteration count from three to one. The scalar's geometric derivation and the iteration purpose are not recovered. |
| `p.Chaos.Collision.ShapesArrayMode` | bool | `true` | The registry row has registration references, but the saved direct-reference scan found no RIP-relative value read. The mode's behavior is unknown. |
| `p.Chaos.Collision.Stiffness` | float | `-1` | Registry help says this overrides collision solver stiffness when the value is `>= 0`. The build compares the value with zero and stores it into solver state only on the nonnegative branch, corroborating the override rule. The solver's stiffness units and effect on convergence or contacts are not determined here. |

## Build evidence

Direct runtime reads were checked at these sites in the local build:

- Capsule contact: `CapsuleRadialContactFraction` at `0x1427E07A1`, `CapsuleAxisAlignedThreshold` at `0x1427E0814`, and `CapsuleDeepPenetrationFraction` at `0x1427E082A`; `SphereCapsuleSizeThreshold` at `0x1427E2605`; and `CapsuleMinContactDistanceFraction` at `0x1426CF0E1`, `0x1426D019A`, `0x1426D11EA`, and `0x1426D226C`.
- Triangle and convex contact: `TriangleConvexMarginMultiplier` at `0x1426E69A4` and `TriangleNormalThreshold` at `0x1426E71E6`; `EdgeNormalThreshold` at `0x1426E70BA`.
- Contact-point matching: `MatchPositionTolerance` at `0x142821CD3` and `0x142821D70`; `MatchNormalTolerance` at `0x142821D85`. The routine compares the squared point separation with a squared size-scaled threshold and also applies the normal tolerance to its normal-comparison path.
- Friction-position processing: `EnableFrictionRestore` at `0x142825246` and `FrictionPositionTolerance` at `0x14282526E`.
- Solver-state override: `Stiffness` at `0x142829713`; negative skips the store and nonnegative stores the value.
- `CullDistanceMarginMultiplier`, `EnableGjkWarmStart`, `AllowLevelsetManifolds`, `AllowParticleTracking`, `DebugDrawProbeDetection`, `GBFCharacteristicTimeRatio`, and `ShapesArrayMode` have registry/object references in the scan but no direct RIP-relative value-read candidate there. This does not prove they are unused: indirect access, non-RIP-relative reads, or scan limitations may hide a use.

## Evidence and limits

- Names, types, help, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Address candidates are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). `ref_rva` direct-memory candidates and `obj_rva` registration references are kept distinct; object references alone are not runtime-use evidence.
- The routine interpretations above are static traces from the installed Shipping executable. The scan can miss indirect or non-RIP-relative access. No in-game test of these settings is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md), [Chaos collision margins and triangle-mesh tolerances](cvar-chaos-collision-margins-tolerances.md), and [CVar overrides and loader syntax](cvar-overrides.md).
