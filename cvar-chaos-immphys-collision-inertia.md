# Chaos immediate-physics collision and inertia CVars

This guide covers the eight `p.Chaos.ImmPhys.Collision.*` and five `p.Chaos.ImmPhys.InertiaConditioning.*` settings. It combines the community registry with direct code reads in Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommended overrides.

## Collision settings

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.ImmPhys.Collision.Enabled` | int32 | `1` | Registry help says this enables or disables collisions in Immediate Physics. The code compares it with zero and stores the result as a boolean scene setting at `0x143FFE7B0`–`0x143FFE7BD`. |
| `p.Chaos.ImmPhys.Collision.DeferNarrowPhase` | int32 | `1` | Help says the legacy solver can create contacts for all broad-phase pairs and run narrow phase later. The value is converted from zero/nonzero to a local boolean at `0x143FDF7A5` and copied into a local settings structure; another direct read occurs at `0x143FFE7E2`. |
| `p.Chaos.ImmPhys.Collision.UseManifolds` | int32 | `0` | Help says this enables or disables manifolds in the legacy collision solver. The value is converted to a local boolean at `0x143FDF7E7` and copied into setup data; another read occurs at `0x143FFE80B`. |
| `p.Chaos.ImmPhys.Collision.CullDistance` | float | `-1` | Registry help says a nonnegative value sets collision cull distance. The value is read at `0x143FFE355` while the scene's collision/time-step settings are being assembled; the exact downstream cull comparison is not isolated in this trace. |
| `p.Chaos.ImmPhys.Collision.MaxDepenetrationVelocity` | float | `-1` | Registry help says a nonnegative value sets maximum depenetration velocity. The value is loaded at `0x143FFE395` in the same setup routine; the final clamp and contact effect are not recovered. |
| `p.Chaos.ImmPhys.Collision.Priority` | int32 | `1` | Help says this sets collision-constraint sort order and that joints have priority `0`. The value is passed to a helper at `0x143FFE7C6`; another path reads it at `0x143FDE284`. The helper's exact ordering implementation is not traced. |
| `p.Chaos.ImmPhys.Collision.RestitutionEnabled` | int32 | `1` | Registry help says this enables or disables collision restitution. The zero/nonzero result is stored as a scene setting at `0x143FFE757`–`0x143FFE764`. |
| `p.Chaos.ImmPhys.Collision.RestitutionThresholdMultiplier` | float | `1.5` | Help defines the restitution threshold acceleration as this multiplier times gravity. The local path squares and sums the three components of a gravity-like vector, takes its square root, multiplies by the CVar, and stores the result at `0x143FFE791`–`0x143FFE7A8`. This directly supports the documented magnitude-times-multiplier formula. |

## Inertia-conditioning settings

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.ImmPhys.InertiaConditioning.LinearEnabled` | bool | `true` | Registry help says it enables constraint stabilization through inertia conditioning for the linear joint solver. At `0x144001B62`, this byte is selected when the solver-mode field indicates a linear-solver path. |
| `p.Chaos.ImmPhys.InertiaConditioning.NonlinearEnabled` | bool | `false` | Registry help says it enables the same stabilization for the nonlinear joint solver. At `0x144001B5A`, this byte is read and selected when the mode field does not indicate the linear path. If the selected enable is zero, the routine skips the following conditioning work. |
| `p.Chaos.ImmPhys.InertiaConditioning.RotationRatio` | float | `2` | Registry help defines the maximum ratio of joint correction from rotation versus translation. The value is read at `0x144001BA3` and copied into local inputs for the conditioning routine. |
| `p.Chaos.ImmPhys.InertiaConditioning.Distance` | float | `10` | Registry help describes the joint-distance error that must be stable to generate low rotation. The value is read at `0x144001BB4` and copied into local inputs; the helper's exact distance test is not recovered. |
| `p.Chaos.ImmPhys.InertiaConditioning.MaxInvInertiaComponentRatio` | float | `0` | Registry help describes a ratio involving the largest and smallest inertia components. The value is read at `0x144001BCE` and copied into local inputs. The helper's comparison direction and threshold formula remain unknown. |

## Evidence and limits

- Names, types, help, and reference RVAs come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Direct reference candidates are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Reads into scene or helper settings prove the values reach the path, but do not establish every downstream solver effect.
- No in-game test of these settings is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md), [Chaos solver collision CVars](cvar-chaos-solver-collision.md), and [CVar overrides and loader syntax](cvar-overrides.md).
