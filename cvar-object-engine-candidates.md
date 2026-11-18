# Replay and engine task candidates in the console object table

These six exact names have matching descriptions in the community console-object table and the preserved Epic UE 5.9 comparison. Each literal name also appears in both the x64 and ARM64EC Shipping executables for build 1.1.4042190. They have no `var` or `ref` registry row or captured snapshot value, so game registration, configuration acceptance, and runtime effects remain unverified.

| Exact name | Object flags | Epic 5.9 default | Meaning shared by both descriptions |
| --- | ---: | --- | --- |
| `demo.ReplayStreamerAutoDemoPrefix` | 0 | `demo` | Prefix used when generating automatic demo names. |
| `TaskGraph.TaskPriorities.HiPriAsyncTickTaskPriority` | 0 | `hnn` | Thread and task priority for high-priority asynchronous ticks. |
| `TaskGraph.TaskPriorities.IoDispatcherAsyncTasks` | 0 | `bnn` | Thread and task priority for I/O dispatcher decompression. |
| `TaskGraph.TaskPriorities.NormalAsyncTickTaskPriority` | 0 | `nnn` | Thread and task priority for asynchronous ticks outside the high-priority class. |
| `TaskGraph.TaskPriorities.TickCleanupTaskPriority` | 0 | `nnn` | Thread and task priority for tick cleanup. |
| `TaskGraph.TaskPriorities.TickDispatchTaskPriority` | 0 | `hnn` | Thread and task priority for tick-task dispatch. |

For the five task priorities, the descriptions define a three-character string. The first character is the thread priority (`h` for high, `n` for normal, or `b` for background). The second is the task priority (`h` or `n`). The third is the task priority if execution is forced onto a normal-priority thread (`h` or `n`). The recorded object flags are source metadata. Their effects on mutability and priority are unknown.

The [community object catalog](cvar-community-console-objects.md) preserves the supplied flags and help. The [Epic comparison and binary inventory](cvar-engine-reference-only.md) record the upstream defaults and executable evidence. See the [graphics companion guide](cvar-object-graphics-candidates.md) for Niagara and graphics scheduling entries.
