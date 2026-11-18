# View, projectile diagnostics, and test CVars beginning N–Z

This guide documents 15 exact registry names that have limited or no help. A dash means the preserved snapshot has no value. Meanings are limited to registry or console-object help.

| Exact CVar | Kind / type | Snapshot | Supplied meaning or unresolved detail | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `PlayerView.GetViewSideOptimize` | `var` / `bool` | `true` | Enables the optimized GetViewSide implementation using TeamComponent. | 0 / 3 | 0 / 1 |
| `ProjectileHit.AutoRecalcBarrierImpactPoint` | `ref` / `bool` | `true` | Help is absent. The trigger, affected impact location, and value semantics are unknown. | 1 / 3 | 1 / 1 |
| `ProjectileHit.EnableRecalcSceneImpactPoint` | `ref` / `bool` | `true` | Help is absent. The recalculation algorithm and affected impact contexts are unknown. | 2 / 3 | 1 / 1 |
| `Server.Pose.FlushSize` | `var` / `int32` | `32` | Help is absent. The buffered data, units, and threshold behavior are unknown. | 0 / 3 | 0 / 1 |
| `SpiderManager.GTargetTraceInterval` | `ref` / `float` | — | Help is absent. The trace scope, timing unit, and valid values are unknown. | 1 / 3 | 1 / 1 |
| `Tag.Crash` | `var` / `int32` | `1` | Help says 1 triggers a crash when tags are inconsistent. | 0 / 3 | 0 / 1 |
| `TraceMgr.CVar_OptimizeAngleSort` | `ref` / `bool` | `false` | Uses ImpactPoint in place of GetClosestPointOnCollision for angle sorting. | 1 / 3 | 1 / 1 |
| `TraceMgr.DrawTargetShape` | `ref` / `bool` | `false` | The only object help is a period. Target shape, drawing scope, and mode semantics are unknown. | 1 / 3 | 1 / 1 |
| `VirtualProjectile.FindRecordTolerance` | `ref` / `float` | `1e-05` | Help is absent. The compared quantities and tolerance unit are unknown. | 1 / 3 | 1 / 1 |
| `VirtualProjectile.GetRecordDeltaTime` | `ref` / `float` | `0.02` | Help is absent. The time unit and which records it applies to are unknown. | 0 / 3 | 1 / 1 |
| `VirtualProjectile.LogigValueStepMaxCount` | `ref` / `int32` | `1000` | Maximum number of stored movement-parameter steps. Values at or below zero disable the limit. Logig is the registry spelling. | 2 / 3 | 1 / 1 |
| `pm.CVarProjectileMovementComponentAlternate` | `ref` / `bool` | `false` | Help is absent. The alternative behavior and selection conditions are unknown. | 2 / 3 | 1 / 1 |
| `pv.debug.msg` | `var` / `int32` | `0` | Help is absent. The messages, output destination, and supported modes are unknown. | 0 / 3 | 0 / 1 |
| `summoner.DrawLevelPenetrationBound` | `var` / `int32` | `0` | Help gives 1 for drawing and says other values leave drawing disabled. Shape and coordinate space are unspecified. | 0 / 3 | 0 / 1 |
| `test.launchkey` | `var` / `bool` | `true` | The help names CVarLaunchKey and lists 0 disabled and 1 enabled. The key and test scope are unspecified. | 0 / 2 | 0 / 1 |

Address counts are compiled from the Shipping 1.1.4042190 static scan. They can include initialization, reads, writes, and address passing. Runtime behavior and override acceptance remain unverified.

See the [preserved source notes](EVIDENCE.md#community-sources) and the [address-match TSV](EVIDENCE.md#build-specific-static-analysis).
