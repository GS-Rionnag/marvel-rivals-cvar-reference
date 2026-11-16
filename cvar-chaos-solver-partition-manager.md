# Chaos solver partition-manager CVars

This page covers the four `p.Chaos.SolverPartitionManager.*` variables in the registry. Their help text is checked against direct reads in Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommended overrides.

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.SolverPartitionManager.Partitioning` | int32 | `0` | Registry help maps `0` to no partitions and `1` to greedy graph coloring. Code compares the setting with zero in partitioned-solver paths, including `0x14286AE0B` and `0x14286E224`; the value also gates the default-parallel decision for `ParallelSolve`. Other strategy values are not defined by the help or recovered here. |
| `p.Chaos.SolverPartitionManager.ParallelSolve` | int32 | `-1` | Registry help maps `0` to off, `1` to task-graph parallel, and `-1` to off without partitioning / on with partitioning. At `0x14286ADF3` and `0x14286E203`, value `1` selects the parallel path. When the value is `-1`, the code checks `Partitioning` and selects parallel only when partitioning is positive. This corroborates the documented default rule. |
| `p.Chaos.SolverPartitionManager.BatchSize` | int32 | `200` | Registry help says this is the number of constraints per solver batch. The build loads it in partition-processing routines at `0x14286DE61`, `0x14286E271`, and `0x14287D9E1`, where it becomes a local batch-processing input. Exact batch boundaries and clamping are inside surrounding helper logic. |
| `p.Chaos.SolverPartitionManager.MinConstraintsForColoring` | int32 | `1000` | Registry help says coloring activates only when a constraint type reaches this minimum. At `0x14287916D`, the code compares a constraint count against the CVar and skips the following coloring work when the count is lower. |

Names, help, and reference RVAs come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Direct instruction candidates are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The helper internals and runtime performance impact are not measured here.

Related guides: [Chaos solver collision CVars](cvar-chaos-solver-collision.md), [Chaos solver island, iteration, and inertia-conditioning CVars](cvar-chaos-solver-islands-iterations.md), and [CVar overrides and loader syntax](cvar-overrides.md).
