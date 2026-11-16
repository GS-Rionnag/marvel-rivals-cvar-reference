# Chaos solver joint CVars

This page covers the twenty `p.Chaos.Solver.Joint.*` registry entries. It uses their community help and captured snapshot values, then distinguishes settings read by the local Marvel Rivals Shipping build `1.1.4042190` from those for which the saved static scan found no direct read. Snapshot values are not verified defaults or recommendations.

## Variables

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Solver.Joint.AngleTolerance` | float | `0.001` | Registry help labels the setting `AngleTolerance`. The scene setup routine reads it at `0x142AE44FE` and copies the converted value into local solver settings; the angle comparison that consumes it is not traced. |
| `p.Chaos.Solver.Joint.PositionTolerance` | float | `0.025` | Registry help labels this `PositionTolerance`. The value is loaded at `0x142AE44ED` and copied into local solver settings; the exact convergence or error test is not recovered. |
| `p.Chaos.Solver.Joint.MinParentMassRatio` | float | `0.2` | Registry help says this 6DOF-joint ratio applies when greater than zero. It is read at `0x142AE4512` and copied into the setup data. |
| `p.Chaos.Solver.Joint.MaxInertiaRatio` | float | `5` | Registry help says this is the 6DOF-joint maximum inertia ratio, used when greater than zero. It is read at `0x142AE4520` and copied into setup data. |
| `p.Chaos.Solver.Joint.MinSolverStiffness` | float | `1` | Registry help says stiffness starts at this value on the first iteration and rises toward `MaxSolverStiffness`. It is read at `0x142AE449F` and copied into local solver settings. The iteration math is not traced. |
| `p.Chaos.Solver.Joint.MaxSolverStiffness` | float | `1` | Registry help says this is the stiffness on the last iteration, approached from `MinSolverStiffness`. It is read at `0x142AE448C` and copied into local solver settings. |
| `p.Chaos.Solver.Joint.NumIterationsAtMaxSolverStiffness` | int32 | `1` | Registry help says it controls how many iterations use maximum stiffness. It is read at `0x142AE44AB` and copied into setup data. |
| `p.Chaos.Solver.Joint.NumShockPropagationIterations` | int32 | `0` | Registry help says it controls how many iterations enable shock propagation. It is read at `0x142AE44D7` and passed with the joint settings to a helper. |
| `p.Chaos.Solver.Joint.ShockPropagation` | float | `-1` | Registry help says a nonnegative value overrides 6DOF joint shock propagation. The value is read at `0x142AE4534` and passed into the scene setup helper. The helper's application logic is not traced. |
| `p.Chaos.Solver.Joint.Priority` | int32 | `0` | Registry help says larger constraint-priority values are evaluated later. A value is passed to a joint-related helper at `0x14297BA2A`; exact ordering behavior beyond the help is unknown. |
| `p.Chaos.Solver.Joint.RemoveKeepOrder` | bool | `true` | No registry help is supplied. During a removal path, the byte at `0x142940C0C` gates a helper call that shifts array elements; enabled takes the helper path, while disabled skips it. This is consistent with preserving element order during removal, though the collection's identity is not recovered. |
| `p.Chaos.Solver.Joint.SolvePositionLast` | bool | `true` | Registry help says `false` solves position then rotation, while `true` solves rotation then position. It is read at `0x142AE44BB` and copied into local joint settings. |
| `p.Chaos.Solver.Joint.UsePBDDrives` | bool | `true` | Registry help says it selects the position or velocity phase for drive solving; the default is true. The byte is read at `0x142AE44C9` and copied into local settings. |
| `p.Chaos.Solver.Joint.UseLinearSolver` | bool | `true` | Registry help says it selects the linear joint solver and defaults to true. The byte is read at `0x142AE454E`, copied into local settings, and passed to a helper. |
| `p.Chaos.Solver.Joint.UseSimd` | bool | `true` | Registry help says it enables SIMD on the linear joint solver. The byte is read at `0x14297B884` and copied to a solver-state field at `0x14297B88B`. |
| `p.Chaos.Solver.Joint.TransferCollisions` | bool | `true` | Registry help says child collisions can transfer to the parent when `Joints.TransferCollisionScale` is nonzero. The saved scan has no direct RIP-relative value-read candidate for this setting. |
| `p.Chaos.Solver.Joint.TransferCollisionsDebugTestAgainstMaxClamp` | bool | `false` | Registry help says it forces transferred joint-collision constraint settings to the maximum clamp for stability testing. No direct read candidate was found in the saved scan. |
| `p.Chaos.Solver.Joint.TransferCollisionsKinematicScale` | float | `1` | Registry help says it scales collision transfers between kinematic bodies. No direct read candidate was found in the saved scan. |
| `p.Chaos.Solver.Joint.TransferCollisionsLimit` | int32 | `2147483647` | Registry help describes the maximum constraints transferred to the parent and says lowering it can improve performance at an accuracy cost. No direct read candidate was found in the saved scan. |
| `p.Chaos.Solver.Joint.TransferCollisionsStiffnessClamp` | float | `1` | Registry help describes a clamp on maximum stiffness for collision transfer. No direct read candidate was found in the saved scan. |

## Scene setup and evidence limits

The angle/position tolerance, inertia/mass ratios, stiffness ramp, iteration count, shock-propagation controls, solve order, drive phase, and linear-solver selection are loaded into a local joint-settings structure around `0x142AE448C`–`0x142AE454E` and passed to a helper. This confirms they reach the setup path but not how the helper uses each field. Priority, removal ordering, and SIMD are read in separate paths. The five collision-transfer settings have registry help but no direct RIP-relative read candidate in the saved scan; this does not rule out indirect or non-RIP-relative use.

Names, types, help, and reference RVAs come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Direct and registration address candidates are preserved separately in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). No in-game tests of these settings are recorded.

Related guides: [Chaos solver collision CVars](cvar-chaos-solver-collision.md), [Chaos collision manifold and contact CVars](cvar-chaos-collision-manifold-contacts.md), and [CVar overrides and loader syntax](cvar-overrides.md).
