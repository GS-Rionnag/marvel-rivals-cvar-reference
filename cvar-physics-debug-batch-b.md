# Physics debug CVar batch B

This guide records the 40 remaining registered `p.debug.*` names after batch A, in the source registry's order. The supplied help strings are often only terse labels or mode descriptions. They indicate intended topics, but do not identify the code path, activation conditions, side effects, or whether a setting is suitable for a player override. No exact-name UE 5.9 default is listed for these entries.

The table separates the community snapshot from Epic reference data. Snapshot values are merely captured values, not defaults. Each row's build column counts address-scan matches separately for `ref_rva` and `obj_rva`; a direct-memory candidate may be a read, write, or initialization operation. Address-taking is not a value access. These counts do not establish an executed branch, runtime effect, or `.ini` editability.

## Registry entries

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help | Build 1.1.4042190 static address candidates |
| --- | --- | ---: | ---: | --- | --- |
| `p.debug.MoreFieldInsightData` | bool (`ref`) | `false` | — | insight get more field command data | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.RemoveClientGCEvent` | bool (`ref`) | `false` | — | Remove Client GC Event | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.RemoveClientGCEventNew` | bool (`ref`) | `false` | — | Remove Client GC Event | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.SmallIgnoreBounds` | bool (`ref`) | `false` | — | small particle ignore bounds | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.SphereToNoneCollisionRate` | float (`ref`) | `-1` | — | Born Sphere to Set None Collision, [0,1] is set rate, -1 reset | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseChunkDebugLog` | bool (`ref`) | `false` | — | Enable Debug Log | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseColLog` | bool (`ref`) | `false` | — | No help supplied; meaning unresolved. | ref_rva: 4 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseDefaultReplication` | bool (`ref`) | `true` | — | Use Default Replication | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseDesChannelFunc` | int32 (`ref`) | `1` | — | Use Channel Func, 0:Use SmallChunk Setting, 1:Ignore, 2:Overlap, 3:Blocking | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseDumpInfo` | bool (`ref`) | `false` | — | No help supplied; meaning unresolved. | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseDumpSPInfo` | bool (`ref`) | `false` | — | No help supplied; meaning unresolved. | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseFlipResultLog` | bool (`ref`) | `false` | — | use flip result log | ref_rva: 6 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseHeroFlipResultLog` | bool (`ref`) | `false` | — | print Hero FlipResultLog | ref_rva: 4 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseIdentityRotation` | bool (`ref`) | `true` | — | fUse Identity Rotation | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseInfluences` | bool (`ref`) | `true` | — | use influence process | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseKinematicUpdateInsight` | bool (`ref`) | `false` | — | Use Kinematic Update Insight Data | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseMidNoneCollision` | bool (`ref`) | `true` | — | Mid Part has no collision | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseMod` | bool (`ref`) | `false` | — | Enable Use Mod RestCollection | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseModNanite` | bool (`ref`) | `false` | — | Enable Generate Nanite Data | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseMoreInsightData` | bool (`ref`) | `false` | — | No help supplied; meaning unresolved. | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseNewDirtyParticle` | bool (`ref`) | `true` | — | Enable the new DirtyParticle | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseNewMethod` | bool (`ref`) | `true` | — | Use New Method | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseNoneCollision` | bool (`ref`) | `false` | — | When enabled, none collision will not add to spatial ac | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseOptBatchDes` | bool (`ref`) | `true` | — | Batch Release Particle Optimized Des | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UsePhysicalBlendLog` | bool (`ref`) | `false` | — | print Physical Blend Log | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UsePhysicsOnly` | int32 (`ref`) | `0` | — | Whether to use physics only. | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 3 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSPLog` | bool (`ref`) | `false` | — | No help supplied; meaning unresolved. | ref_rva: 3 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseServerSimpleCollection` | bool (`ref`) | `false` | — | Server Use Simple Collection | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSimpleCollection` | bool (`ref`) | `false` | — | Use Simple Collection | ref_rva: 2 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSimpleRemap` | bool (`ref`) | `false` | — | Use Simple Collection Remap | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSkipBoneKinematic` | bool (`ref`) | `false` | — | skip the bone kinematic dirty particle | ref_rva: 3 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSkipHitShapeBoneUpdateSolverAC` | bool (`ref`) | `false` | — | HitShape Skip Bone Rigid Update Solver AC | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSkipPhysAnimBoneUpdateSolverAC` | bool (`ref`) | `false` | — | PhysAnim Skip Bone Rigid Update Solver AC | ref_rva: 4 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSkipSyncBodyBoneUpdateSolverAC` | bool (`ref`) | `false` | — | Syncbodies Skip Bone Rigid Update Solver AC | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSmallInsightPoint` | bool (`ref`) | `true` | — | use Small Point for insight | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSmallInsightPoint1` | bool (`ref`) | `true` | — | use Small Point for insight | ref_rva: 0 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSmallNoneCollision` | bool (`ref`) | `true` | — | Small Part has no collision | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSmallNoneCollisionRate` | float (`ref`) | `0` | — | Small Part Rate Has no collision | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.UseSubLevel` | bool (`ref`) | `false` | — | Set Level One Node to Ignore Parent List | ref_rva: 1 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |
| `p.debug.bUseClientGCInstance` | bool (`ref`) | `true` | — | Only Use StaticMesh | ref_rva: 3 direct-memory candidate(s), 1 address-taking; obj_rva: 2 direct-memory candidate(s), 1 address-taking. |

## Evidence and interpretation limits

- `console_vars.tsv` supplies exact names, `kind`, `vtype`, `help`, `obj_rva`, and `ref_rva`. All entries in this batch are registered as `ref`. Registration as `ref` documents a reference-style registry row; it does not show that the game accepts an override from an `.ini` or that the setting changes an in-match client.
- `CVarDump.txt` supplies the snapshot column. Its capture procedure, game build, and whether each value was a default or an override are unspecified.
- Epic 5.9 values are exact-name reference matches in the generated community catalog. `—` means no exact-name UE 5.9 entry was found in that comparison, not that the game lacks a default.
- Address counts are from the saved `.text` scan of the installed Shipping executable for build `1.1.4042190`. `ref_rva` and `obj_rva` are kept distinct. The scan did not decode surrounding functions or determine whether candidates read or write the value. There was no runtime test.
- Labels about destruction collections, insight/debug logs, collision filtering, and physics-only behavior should be read as the registry's supplied descriptions. Names and help alone do not prove the effect in Marvel Rivals.

Sources: [community source notes](EVIDENCE.md#community-sources), [community registry attachments](EVIDENCE.md#community-sources), [community snapshot attachment](EVIDENCE.md#community-sources), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), and [registry catalog with Epic 5.9 cross-check](cvar-community-registry.md).

