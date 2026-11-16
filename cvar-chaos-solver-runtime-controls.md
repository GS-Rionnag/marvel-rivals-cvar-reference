# Chaos solver runtime and lifecycle controls

This guide covers twelve remaining `p.Chaos.Solver.*` controls: determinism, CCD, sleeping, particle-array/pool behavior, test/debug switches, cleanup, probe narrow phase, and constraint priority. It distinguishes registry help from direct reads observed in the local Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommendations.

## Variables

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Solver.Deterministic` | int32 | `1` | Registry help maps `0` to disabled, `1` to enabled, and `-1` to configuration. The value is read at `0x142AE46C8` and `0x142AEF7F0`. Negative values skip an explicit update in one path; another path compares with `1` and uses a helper for the lower-value case. The mapping from those branches to the final deterministic state is not fully recovered. |
| `p.Chaos.Solver.UseCCD` | bool | `true` | Registry help describes a global CCD on/off flag. Setup reads the byte at `0x142AE43A9` and copies it into the scene collision-settings data. |
| `p.Chaos.Solver.SleepEnabled` | bool | `true` | No registry help is supplied. At `0x1428E9396`, zero branches around the subsequent body of a sleep-related routine; the exact behavior of the enabled path is not recovered. |
| `p.Chaos.Solver.ShrinkArrays` | bool | `false` | Registry help says it enables or disables particle-array shrinking in the main scene. The byte is checked at `0x142ADE44B`; zero skips the following array-processing block, consistent with the help. |
| `p.Chaos.Solver.UseParticlePool` | bool | `true` | Registry help describes using a dirty particle pool for optimization. No direct RIP-relative value-read candidate was found in the saved scan, so this local build's runtime gate remains unconfirmed. |
| `p.Chaos.Solver.ParticlePoolNumFrameUntilShrink` | int32 | `30` | Registry help describes the number of frames before the pool can potentially shrink. The scan found no direct value-read candidate; pool timing logic is not independently traced. |
| `p.Chaos.Solver.CleanupCommandsOnDestruction` | int32 | `1` | Registry help says `0` disables internal command-queue cleanup on solver destruction and values greater than `0` clean all commands. The scan found no direct value-read candidate for this setting. |
| `p.Chaos.Solver.DoFinalProbeNarrowPhase` | bool | `true` | No registry help is supplied. At `0x142988D7B`, a nonzero byte calls helper `0x1429218B0`; zero skips that call. The name indicates final probe narrow-phase work, but the helper's effects are not recovered. |
| `p.Chaos.Solver.TestMode` | bool | `false` | No registry help is supplied. At `0x142987E01` and `0x142988D6A`, zero skips a helper call and nonzero allows it. The helper is the same in both observed paths; what test mode changes is unresolved. |
| `p.Chaos.Solver.Debugkkk` | int32 | `0` | Registry help says it colors shapes red for server and blue for client. The saved scan has no direct value-read candidate; rendering behavior in this build remains unverified. The unusual spelling is preserved from the registry. |
| `p.Chaos.Solver.CharacterGroundConstraint.Priority` | int32 | `0` | Registry help says larger constraint-priority values are evaluated later. The value is passed to a constraint helper at `0x14297BA40`; exact sorting/order details are not traced. |
| `p.Chaos.Solver.Suspension.Priority` | int32 | `0` | Registry help likewise says larger values are evaluated later. The value is passed to a constraint helper at `0x14297BA02`; the exact suspension ordering behavior is not recovered. |

## Evidence and limits

- Names, types, help, and reference RVAs come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); the values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Direct and registration address candidates are kept separately in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). A missing direct candidate does not prove a setting is unused: indirect or non-RIP-relative access can be missed.
- The observed branches and helper calls do not establish all downstream behavior. No in-game test is recorded.

Related guides: [Chaos solver collision CVars](cvar-chaos-solver-collision.md), [Chaos solver joint CVars](cvar-chaos-solver-joint.md), and [Chaos solver island, iteration, and inertia-conditioning CVars](cvar-chaos-solver-islands-iterations.md).
