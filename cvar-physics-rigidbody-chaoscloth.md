# Rigid Body Node and Chaos Cloth CVars

This guide documents all 17 currently uncovered registered `p.RigidBodyNode.*` names and all 8 uncovered `p.ChaosCloth.*` names in the community registry. It focuses on animation physics simulation, cloth interaction, update timing, and debug drawing. Community help and snapshot values remain distinct from exact-name Epic UE 5.9 matches; neither source establishes Marvel Rivals’ engine revision or live behavior.

Build evidence comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may be a read, comparison, or write; a `var` object reference may be registration/setup. Static references do not show the path executes for a particular character or match. No `.ini` override, live query, or gameplay comparison was performed.

## Rigid Body Node simulation and space

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.RigidBodyNode.DebugDraw` | bool (`ref`) | `false` | `false` | Whether to debug draw the rigid body simulation state. Requires p.Chaos.DebugDraw.Enabled 1 to function as well. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.DeferredSimulationDefault` | bool (`ref`) | `false` | `false` | Whether rigid body simulations are deferred one frame for assets that don't opt into a specific simulation timing *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.EnableComponentAcceleration` | bool (`ref`) | `true` | `true` | Enable/Disable the simple acceleration transfer system for component- or bone-space simulation *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.EnableSimulation` | int32 (`var`) | `1` | `1` | Runtime Enable/Disable RB Node Simulation for debugging and testing (node is initialized and bodies and constraints are created, even when disabled.) *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value use was not established. |
| `p.RigidBodyNode.EnableTimeBasedReset` | bool (`ref`) | `true` | `true` | If true, Rigid Body nodes are reset when they have not been updated for a while (default true) *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.IncludeClothColliders` | bool (`ref`) | `true` | `true` | Include cloth colliders as kinematic bodies in the immediate physics simulation. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.InitializeBoneReferencesRangeCheckEnabled` | bool (`ref`) | `true` | `true` | No explanatory help was supplied; exact behavior remains unresolved. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.MaxSubSteps` | int32 (`ref`) | `4` | `4` | Set the maximum number of simulation steps in the update loop *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.MaxAngularAcceleration` | float (`ref`) | `10000` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.MaxAngularVelocity` | float (`ref`) | `10000` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.MaxLinearAcceleration` | float (`ref`) | `10000` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.MaxLinearVelocity` | float (`ref`) | `10000` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.Override` | bool (`ref`) | `false` | `false` | Force-enable the advanced simulation space movement forces *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.VelocityScaleZ` | float (`ref`) | `1` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.Space.WorldAlpha` | float (`ref`) | `0` | `-1` | RBAN SimSpaceSettings overrides *(source: community help)* | 2 direct-memory candidate(s), 3 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.TaskPriority.Simulation` | int32 (`ref`) | `0` | `0` | Task priority for running the rigid body node simulation task (0 = foreground/high, 1 = foreground/normal, 2 = background/high, 3 = background/normal, 4 = background/low). *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.RigidBodyNode.WorldObjectExpiry` | int32 (`ref`) | `4` | `4` | World objects are removed from the simulation if not detected after this many tests *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |

## Chaos Cloth simulation and solver

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.ChaosCloth.CanBeAffectedByFields` | bool (`ref`) | `false` | `—` | Chaos Cloth can be affected by fields *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.ChaosCloth.DebugDraw.Enabled` | bool (`ref`) | `false` | `—` | Enable Cloth Debug Draw *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.ChaosCloth.LegacyDisablesAccurateWind` | bool (`var`) | `true` | `true` | Whether using the Legacy wind model switches off the accurate wind model, or adds up to it *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value use was not established. |
| `p.ChaosCloth.SkipUpdateBounds` | bool (`ref`) | `true` | `—` | No explanatory help was supplied; exact behavior remains unresolved. *(source: not described)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.ChaosCloth.Solver.DisableTimeDependentNumIterations` | bool (`ref`) | `false` | `false` | Make the number of iterations independent from the time step. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.ChaosCloth.Solver.UseVelocityScale` | bool (`ref`) | `true` | `true` | Use the velocity scale to compensate for clamping to MaxPhysicsDelta, in order to avoid miscalculating velocities during hitches. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |
| `p.ChaosCloth.UseOptimizedTaperedCapsule` | bool (`var`) | `true` | `true` | Use the optimized TaperedCapsule code instead of using a tapered cylinder and two spheres *(source: community help)* | CVar-object setup/address references only; this `var` lacks a `ref_rva`, so runtime value use was not established. |
| `p.ChaosCloth.UseTimeStepSmoothing` | bool (`ref`) | `true` | `true` | Use time step smoothing to avoid jitter during drastic changes in time steps. *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and the consuming path were not traced. |

## Scope and limitations

- Help text describes simulation toggles, step limits, resets, space settings, cloth collider participation, wind models, solver iteration behavior, and debug visualization. It does not reveal which character assets use each setting or whether the game reads the override at startup.
- Captured values are not recommendations. Epic 5.9 defaults appear only when the registry has an exact upstream name match; an em dash means no exact match was recorded.
- The `var`/`ref` labels and binary address matches are static registry evidence. They do not establish that a CVar is runtime-editable or accepted by the loader.

For broader coverage, see the [CVar docs index](README.md), the [community registry](cvar-community-registry.md), and the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).


