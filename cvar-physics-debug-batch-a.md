# Physics debug CVar batch A

This guide covers the first 25 currently uncovered registered `p.debug.*` CVars in registry order. Their names and supplied help suggest Chaos/Geometry Collection diagnostic and workaround controls, but this does not establish that they are exposed to players, enabled in matches, or safe to override. The community registry has no exact-name Epic UE 5.9 defaults for these entries.

Build evidence comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may be a read, comparison, or write; address counts do not reveal direction or execution frequency. No code path was traced and no startup override or gameplay test was performed.

## Debug, collision, destruction, and particle controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `p.debug.AABBLog` | bool (`ref`) | `false` | `—` | Ignore AABB log | 80 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.AABBLogCount` | int32 (`ref`) | `100000` | `—` | AABBLogCount | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.AlwaysColLog` | bool (`ref`) | `false` | `—` | No explanatory help supplied; exact behavior unresolved. | 5 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.AlwaysFlipResultLog` | bool (`ref`) | `false` | `—` | always use flip result log | 6 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.AlwaysSPGCLog` | bool (`ref`) | `false` | `—` | No explanatory help supplied; exact behavior unresolved. | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.CheckFilterFlag` | bool (`ref`) | `false` | `—` | No explanatory help supplied; exact behavior unresolved. | 2 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.DumpDestructionData` | bool (`ref`) | `false` | `—` | Dump Destruction binary Data Switch | 2 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.DynamicCheckFrameNum` | int32 (`ref`) | `-1` | `—` | No explanatory help supplied; exact behavior unresolved. | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.DynamicCheckMaxLife` | int32 (`ref`) | `10` | `—` | No explanatory help supplied; exact behavior unresolved. | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.EnableChaosDesChannel` | bool (`ref`) | `true` | `—` | Enable Channel | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.EnableGCRenderLOD` | int32 (`ref`) | `1` | `—` | Enable GC Render LOD | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.FilterPairsNum` | int32 (`ref`) | `-1` | `—` | No explanatory help supplied; exact behavior unresolved. | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.FixChaosGeometryLeak` | bool (`ref`) | `true` | `—` | fix chaos Geometry leak | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.FixFieldStackOverflow` | bool (`ref`) | `false` | `—` | fix the X20 Field Stack Overflow | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.FixKinematicRoot` | bool (`ref`) | `true` | `—` | fix the kinematic Root problem,kinematic particle will in ActiveParticlesMapArray | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.FixMassComputeByMesh` | bool (`ref`) | `true` | `—` | fix the Mass To Local Compute | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.ForceParticlePath` | int32 (`ref`) | `2` | `—` | =0 will choose the min particle,=1 force sleeping particle,=2 force Moving Kinematic Particle | 10 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.HideClientSMBP` | bool (`ref`) | `false` | `—` | HideClientSMBP | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.IgnoreAABBNoneCollision` | bool (`ref`) | `true` | `—` | Ignore AABB NoneCollision | 7 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.IgnoreBroadPhaseNoneCollision` | bool (`ref`) | `true` | `—` | Braod Phase filter no collision | 26 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.MassToLocalTolerance` | float (`ref`) | `1` | `—` | CheckMassToLocal Function Use Tolerance | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.MaxBreakEventNum` | int32 (`ref`) | `-1` | `—` | Set Max Break Event Num, -1 reset | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.MaxCollisionEventNum` | int32 (`ref`) | `-1` | `—` | Set Max Collision Event Num, -1 reset | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.MaxDynamicDestructionForCrumble` | int32 (`ref`) | `-1` | `—` | max small dynamic destruction for one frame,if exceed then remain middle block will disappear, -1 will reset | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |
| `p.debug.MaxSmallNumPerFrame` | int32 (`ref`) | `-1` | `—` | max small num for one frame,if exceed then remain middle block will disappear, -1 will reset | 2 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime execution were not traced. |

## Reading the evidence

- Help such as `ForceParticlePath` values or per-frame destruction-event limits gives a direct description of intent, but not the caller, timing, or runtime conditions.
- Several entries have only a short label or no help at all. Their exact behavior remains unresolved; the name alone is not treated as a definition.
- Snapshot values are captured values, not defaults or recommendations. A missing Epic 5.9 match means this registry does not provide an upstream default for the exact name.
- These entries are registered as `ref` in the community dump. Registration plus static address references do not prove the CVar accepts an `.ini` override or affects a live match.

For additional physics families, see the [CVar documentation index](README.md), [community CVar registry](cvar-community-registry.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
