# Chaos PBD collision-solver CVars

This guide covers all thirteen `p.Chaos.PBDCollisionSolver.*` entries in the supplied registry. Their community help strings are blank. The descriptions below therefore separate behavior visible in the local Marvel Rivals Shipping `1.1.4042190` executable from names and captured values that remain unexplained. Snapshot values are not verified defaults or recommendations.

## Per-phase solve and friction controls

| CVar | Type | Snapshot | Local-build evidence and limits |
| --- | --- | ---: | --- |
| `p.Chaos.PBDCollisionSolver.Position.SolveEnabled` | bool | `true` | The byte is checked at `0x142854234`; zero branches around the position-solver path. Nearby, the path iterates constraints and feeds the position-specific mass-scale setting to a helper. This confirms an enable gate on position-phase work, though the complete solver entry point is not named. |
| `p.Chaos.PBDCollisionSolver.Position.MinInvMassScale` | float | `0.77` | Read repeatedly in a per-item loop, including `0x142854284`, and passed as a float argument to helper `0x14285FAF0`. That helper combines the argument with constraint and mass-property data. This supports a position-solver inverse-mass scaling input; the exact minimum/clamp formula is not reconstructed. |
| `p.Chaos.PBDCollisionSolver.Position.StaticFriction.Stiffness` | float | `0.5` | Loaded at `0x142843206`, broadcast across vector lanes, and used in the position-friction calculation path. Other reads occur at `0x142843A1F` and `0x1428603B0`. The value's exact relationship to the friction correction is not fully recovered. |
| `p.Chaos.PBDCollisionSolver.Velocity.SolveEnabled` | bool | `true` | The byte is checked at `0x1428551E4`; zero branches around velocity-phase work. The path otherwise iterates solver items and passes the velocity-specific mass-scale value to a helper. |
| `p.Chaos.PBDCollisionSolver.Velocity.MinInvMassScale` | float | `0.77` | Read repeatedly in a per-item loop, including `0x142855235`, and passed to helper `0x14285FAF0` alongside solver-item data. This supports an inverse-mass scaling input for the velocity phase; the exact minimum/clamp formula remains unresolved. |
| `p.Chaos.PBDCollisionSolver.Velocity.FrictionEnabled` | bool | `true` | At `0x14284396C`, zero branches to a fallback path and skips the following velocity-friction calculation; nonzero continues into that work. Another read occurs at `0x142863A4C`. |
| `p.Chaos.PBDCollisionSolver.Velocity.StaticFriction.Stiffness` | float | `1` | Read at `0x142863D35` and multiplied by solver-local values in the velocity-friction path. This confirms it scales terms in that calculation, but not the exact physical response. |
| `p.Chaos.PBDCollisionSolver.Velocity.AveragePointEnabled` | bool | `true` | In a contact loop at `0x142863A1F`, the setting is consulted only after the contact count exceeds one. When enabled, that branch calls helper `0x142863000` before continuing, consistent with an averaging path. The helper's output layout and exact averaging formula are not mapped. |

## Jacobi and automatic-stiffness parameters

| CVar | Type | Snapshot | Local-build evidence and limits |
| --- | --- | ---: | --- |
| `p.Chaos.PBDCollisionSolver.JacobiStiffness` | float | `0.5` | Read at `0x142860FB4`, `0x142861FF3`, and `0x142862AD0`. Each observed path multiplies this value by solver-local correction data before further accumulation. This supports a Jacobi correction-strength/relaxation factor; the final update equation is not fully reconstructed. |
| `p.Chaos.PBDCollisionSolver.JacobiPositionTolerance` | float | `1e-06` | No help text and no direct `ref_rva` memory-read candidate in the saved scan. The tolerance's use and unit are unknown. |
| `p.Chaos.PBDCollisionSolver.JacobiRotationTolerance` | float | `1e-08` | No help text and no direct `ref_rva` memory-read candidate in the saved scan. The tolerance's use and unit are unknown. |
| `p.Chaos.PBDCollisionSolver.AutoStiffness.MassRatio1` | float | `0` | No help text and no direct `ref_rva` memory-read candidate in the saved scan. Its name suggests an automatic-stiffness mass-ratio parameter, but its formula and whether the local build reads it are unknown. |
| `p.Chaos.PBDCollisionSolver.AutoStiffness.MassRatio2` | float | `0` | No help text and no direct `ref_rva` memory-read candidate in the saved scan. Its name suggests a second automatic-stiffness mass-ratio parameter, but its formula and whether the local build reads it are unknown. |

## Evidence and limits

- Names, types, and reference RVAs come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Both registry-help columns are blank for this family.
- Candidate reads are retained in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The listed instruction behavior was checked in the local executable's `.text` disassembly. The scanner is limited to direct references; absence of a match does not prove absence of indirect use.
- The helper calls and solver paths are not fully symbolized. No controlled in-game overrides were tested, and no snapshot value should be treated as a default or tuning recommendation.

Related guides: [Chaos collision solver CVars](cvar-chaos-solver-collision.md), [Chaos collision manifold and contact CVars](cvar-chaos-collision-manifold-contacts.md), [Chaos joint settings](cvar-chaos-joints-and-constraint-scales.md), and [CVar overrides and loader syntax](cvar-overrides.md).
