# Chaos solver island, iteration, and inertia-conditioning CVars

This guide covers thirteen `p.Chaos.Solver.*` settings for island scheduling, iteration counts, dynamic iteration-setting recomputation, and inertia conditioning. Evidence combines the community registry/snapshot with direct references in Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommendations.

## Island grouping

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Solver.IslandGroups.MaxWorkers` | int32 | `0` | Registry help says zero means unlimited workers. The build reads it at `0x1428D3301`; positive values cap a calculated worker limit, while zero or negative leaves the `INT_MAX` sentinel. |
| `p.Chaos.Solver.IslandGroups.WorkerMultiplier` | float | `1` | Registry help defines total island groups as worker-thread count times this multiplier. The build reads it at `0x1428D3309`, converts it to double precision, and multiplies it into a worker-count calculation before a later clamp. The complete formula is not recovered. |
| `p.Chaos.Solver.IslandGroups.MinBodiesPerWorker` | int32 | `50` | Registry help says it is the desired minimum bodies per worker. At `0x1428D9EB1`, the setting is compared with a derived count and the greater value is written into island-group data. |
| `p.Chaos.Solver.IslandGroups.MinConstraintsPerWorker` | int32 | `5` | Registry help says it is the desired minimum constraints per worker. At `0x1428D9EA1`, the setting is compared with a derived count and the greater value is written into island-group data. |
| `p.Chaos.Solver.IslandGroups.ParallelMode` | int32 | `2` | Registry values are `0` single-threaded, `1` parallel-for, and `2` tasks. At `0x1428E77C6`, zero exits the parallel branch, one selects a parallel-for path, and two calls a task helper. Other nonzero values reach another branch rather than either documented mode. |

## Iteration settings

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Solver.ComputeIterationSettings.Enabled` | bool | `true` | Registry help says iteration settings are recomputed whenever an island changes. The build checks this flag at `0x1428DADC2`; zero skips the following recomputation block, while nonzero permits entry when an earlier mode check also passes. |
| `p.Chaos.Solver.Iterations.Position` | int32 | `-1` | Registry help says `-1` uses configuration. In a scene-settings setup path, negative skips the override; nonnegative values are capped at `127` and stored in a byte field at `0x142AE45C3`. In an island update path, nonnegative values are combined with an existing local count using a minimum operation before a byte store at `0x1428E6F91`. The helper-level meaning of those two fields is not recovered. |
| `p.Chaos.Solver.Iterations.Velocity` | int32 | `-1` | Registry help says `-1` uses configuration. Negative skips the override; nonnegative values are capped at `127` and stored in a byte field at `0x142AE45FA`. A second path at `0x1428E6FC5` combines the value with an existing count using a minimum operation before storing a byte. |
| `p.Chaos.Solver.Iterations.Projection` | int32 | `-1` | Registry help says `-1` uses configuration. Negative skips the override; nonnegative values are capped at `127` and stored in a byte field at `0x142AE4625`. A second path at `0x1428E6FEA` combines the value with an existing count using a minimum operation before storing a byte. |

## Inertia conditioning

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Solver.InertiaConditioning.Enabled` | bool | `true` | Registry help says it enables constraint stabilization through inertia conditioning. In the local routine, the flag is checked at `0x1429B9329` after candidate type/flag filters; zero skips the later inertia-conditioning helper call. |
| `p.Chaos.Solver.InertiaConditioning.Distance` | float | `20` | Registry help describes this as the joint-distance error that needs to be stable to generate low rotation. The value is read at `0x1429B9283` and supplied to the inertia-conditioning path; the helper's distance test is not traced. |
| `p.Chaos.Solver.InertiaConditioning.RotationRatio` | float | `2` | Registry help calls this the maximum ratio of joint correction from rotation versus translation. The value is read at `0x1429B9276` and passed into the helper. The exact correction equation is not recovered. |
| `p.Chaos.Solver.InertiaConditioning.MaxInvInertiaComponentRatio` | float | `0` | Registry help describes a relation between the largest and smallest inertia components. The value is read at `0x1429B9291` and passed into the helper, but its comparison and threshold direction remain unresolved. |

## Evidence and limits

- Names, types, help, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); snapshot values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- The local instruction candidates are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Island and iteration behavior is described only through the observed branches, clamps, conversions, and stores; downstream solver semantics remain partly unknown.
- No in-game test of these settings is recorded.

Related guides: [Chaos solver collision CVars](cvar-chaos-solver-collision.md), [Chaos solver joint CVars](cvar-chaos-solver-joint.md), and [CVar overrides and loader syntax](cvar-overrides.md).
