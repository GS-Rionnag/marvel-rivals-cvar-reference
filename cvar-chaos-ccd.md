# Chaos CCD CVars

This guide covers the six `p.Chaos.Collision.CCD.*` variables in the community registry and the references found in Marvel Rivals Shipping build `1.1.4042190`. Community help and the CVar snapshot are reported separately from what the local code scan establishes.

| CVar | Type | Snapshot | Community help / local evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.CCD.AllowClipping` | bool | `true` | Help says CCD clips the object at colliding positions when computation budgets run out, and warns disabling it might cause tunneling. The build reads the bool in CCD processing at `0x1426A2991` and branches on it again at `0x1426A38AC`; the local names of the clipping state are unresolved. The help's default is `true`. |
| `p.Chaos.Collision.CCD.ConstraintMaxProcessCount` | int32 | `1` | Help describes the maximum number of times a constraint may be resolved while applying CCD constraints, and says larger values resolve them more fully. In code, a per-constraint counter is incremented at `0x1426A39D7`, the CVar is loaded at `0x1426A39F4`, and the values are compared at `0x1426A39FA`; processing loops while the counter is below the limit. Help states default `2`, while the attached snapshot is `1`; neither should be used as a recommendation. |
| `p.Chaos.Collision.CCD.CorrectionIterations` | int32 | `4` | Help describes the number of post-solve CCD correction iterations. At `0x1426A1B7A` the value is loaded into a loop bound; nearby code starts a counter at zero and exits when it reaches the bound. Early exits elsewhere in the routine may shorten work. |
| `p.Chaos.Collision.CCD.CorrectionPhiToleranceScale` | float | `0.02` | Help says this controls allowed penetration during the correction phase as a multiplier on shape size. The build loads it at `0x1426A1B70` and converts it to double precision at `0x1426A1BA8`; exact downstream units are not recovered here. |
| `p.Chaos.Collision.CCD.EnableResweep` | bool | `true` | Help says resweeping can detect more secondary collisions at additional cost, with help default `true`. The local build contains the name and registration, but the complete direct `ref_rva` scan found no RIP-relative memory-access candidate for its value. This bounded negative result does not rule out indirect reads, so build-specific resweep behavior remains unverified. |
| `p.Chaos.Collision.CCD.UseTightBoundingBox` | bool | `true` | No community help. At `0x14297FE33` the value gates an adjustment: nonzero skips a block that, when `ConstraintMaxProcessCount > 1`, adds the largest absolute component of a vector to a local scalar. This is consistent with a tighter versus expanded bound, though the exact bound and collision consequence are not identified. |

## Evidence and limits

- Types, help, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Direct-reference rows and the scan boundary are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Build identity and hash are recorded in the [source notes](EVIDENCE.md#build-specific-static-analysis).
- Several code paths support the registry descriptions, but the static trace does not show runtime settings, map coverage, or safe override ranges. No in-game test is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md), [Chaos collision UnionBVH CVars](cvar-chaos-union-bvh.md), and [CVar overrides and loader syntax](cvar-overrides.md).
