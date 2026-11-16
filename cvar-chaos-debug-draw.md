# Chaos debug-draw CVars

This note covers the five `p.Chaos.DebugDraw.*` boolean entries in the preserved community registry. The descriptions below tell us what each toggle is intended to visualize; they do not establish that the Shipping client exposes the visualization in normal matches or that enabling it works through the override loader loader.

## Findings

| CVar | Registry type / help | Captured snapshot | What the available evidence supports |
| --- | --- | --- | --- |
| `p.Chaos.DebugDraw.Deformable.KinematicParticle` | `bool` / “Debug draw the deformables kinematic particles.” Help says default `false`. | `false` | A diagnostic visualization toggle for deformable kinematic particles. The exact marker, color, lifetime, and qualifying particle states are not documented. |
| `p.Chaos.DebugDraw.Deformable.RigidCollisionGeometry` | `bool` / “Debug draw the deformable solvers rigid collision geometry.” Help says default `false`. | `false` | A diagnostic visualization toggle for rigid collision geometry used by deformable solvers. The help does not say which geometry representation is drawn or where it appears. |
| `p.Chaos.DebugDraw.Deformable.TetrahedralParticle` | `bool` / “Debug draw the deformable solvers tetrahedron.” Help says default `false`. | `false` | A diagnostic visualization toggle for tetrahedral particles in deformable solvers. The wording does not specify whether it draws vertices, edges, faces, or all three. |
| `p.Chaos.DebugDraw.Deformable.TransientKinematicParticle` | `bool` / “Debug draw the deformables transient kinematic particles.” Help says default `false`. | `false` | A diagnostic visualization toggle for transient kinematic particles in deformable systems. “Transient” is part of the setting’s label; its lifetime or internal definition is not recovered here. |
| `p.Chaos.DebugDraw.GeometryCollectionReplication` | `bool` / “If true debug draw deltas and corrections for geometry collection replication.” | `false` | When enabled, intended to visualize replication deltas and corrections for Geometry Collections. The help does not define the displayed quantities, colors, coordinate space, or network conditions. |

The snapshot values are captured values, not proven defaults. Only the four deformable entries have `[def: false]` in the community help. Public Unreal CVar listings repeat these descriptions and classify them as variables; they do not add implementation details ([KinematicParticle](https://unrealdirective.com/resources/console-variables/p-chaos-debugdraw-deformable-kinematicparticle/), [RigidCollisionGeometry](https://unrealdirective.com/resources/console-variables/p-chaos-debugdraw-deformable-rigidcollisiongeometry/), [TetrahedralParticle](https://unrealdirective.com/resources/console-variables/p-chaos-debugdraw-deformable-tetrahedralparticle/), [TransientKinematicParticle](https://unrealdirective.com/resources/console-variables/p-chaos-debugdraw-deformable-transientkinematicparticle/), [GeometryCollectionReplication](https://unrealdirective.com/resources/console-variables/p-chaos-debugdraw-geometrycollectionreplication/)). These pages are secondary indexes, not Marvel Rivals implementation evidence.

## Build 1.1.4042190 inspection

The installed Shipping executable is identified in the local build inventory as `Marvel Rivals Shipping executable`, build `1.1.4042190`, SHA-256 `omitted from this documentation-only project`. The saved full-`.text` RIP-relative address scan has two address-taking (`lea`) matches and two direct-memory candidates for each of the five names. The address-taking rows only take addresses. Each direct-memory candidate is `mov QWORD PTR [rip+...],rax`, a memory write to an `obj_rva` target; none is a direct read of the CVar's `ref_rva`. Thus this scan did **not** yield a direct value read for any of these five toggles.

This negative result is scoped to the scanner's direct RIP-relative references in the scanned `.text`. It does not prove the variables are unused: an indirect pointer, a non-RIP-relative access, or code outside that scanned executable can evade this scan. The local executable's exact consumer/visualization routines and controlled in-game effects remain unverified. The installed executable was not separately opened in REA for this focused note; the binary evidence here is the saved scan and its instruction text.

## Loader use

If experimenting, these are the boolean override forms for the documented `[Overrides]` section:

```ini
p.Chaos.DebugDraw.Deformable.KinematicParticle=true
p.Chaos.DebugDraw.Deformable.RigidCollisionGeometry=true
p.Chaos.DebugDraw.Deformable.TetrahedralParticle=true
p.Chaos.DebugDraw.Deformable.TransientKinematicParticle=true
p.Chaos.DebugDraw.GeometryCollectionReplication=true
```

These lines express the registry type and intended toggle operation; they are not a tested recommendation. The current evidence does not show whether the release build's relevant debug-draw branches execute, whether the rendering is visible to a player, or what performance cost enabling them has.

## Evidence and scope

- Community registry attachment and provenance: [community research-source notes](EVIDENCE.md#community-sources), [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Snapshot values are not defaults unless the help explicitly says so.
- Local direct-reference rows: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Scanner limits and build identity are documented in the source README.
- Local build inventory: [`cvar-game-build-4042190.md`](EVIDENCE.md#build-specific-static-analysis).
- Related physics research: [Chaos scene-query CVars](cvar-chaos-scene-queries.md), [Chaos collision CVars](cvar-chaos-collision-tolerances.md), and [Chaos solver runtime controls](cvar-chaos-solver-runtime-controls.md).
