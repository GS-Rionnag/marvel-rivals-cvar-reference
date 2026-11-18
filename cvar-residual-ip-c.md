# Additional I-P gameplay and engine CVars, batch C

These 33 registry entries cover event settings, gameplay and physics, and networking diagnostics. Snapshots are observations from an unspecified capture build. A dash indicates no value or matching evidence in the relevant source.

Build strings are exact names recorded for 1.1.4042190. CRC denotes Crash Report Client. Object and ref hits are x64 direct-memory candidates / address-taking instructions. The static evidence leaves runtime effects and startup override support unverified.

## Event and mode settings

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `M2201.ChargeBanHeros` | `FString` / `ref` | — | The help identifies a Times Square charge-mode hero ban list. The list format is unspecified. | x64, ARM64EC | 3 / 1 | 1 / 2 |
| `M2201.NewYearFirework_CountDownStr` | `FString` / `ref` | — | New Year fireworks countdown string used in Python, according to the help. | x64, ARM64EC | 3 / 1 | 1 / 2 |
| `M2206.EnableWaveGCByTier` | `bool` / `ref` | `true` | Translated help describes whether garbage collection runs when the wave tier changes in mode M2206. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `M2208.EnableWaveGCByTier` | `bool` / `ref` | `true` | Translated help describes whether garbage collection runs when the wave tier changes in mode M2208. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `M2212.Bubble.Log` | `int32` / `var` | `0` | Translated help describes logging the original and resulting IDs and the caster for projectile-to-bubble conversions when enabled. | x64, ARM64EC | 3 / 1 | — |

## Gameplay and physics

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `Impulse.Apply.Char` | `int32` / `var` | `0` | The help describes applying an impulse to a character. The trigger and parameters are unspecified. | x64, ARM64EC | 2 / 1 | — |
| `Impulse.Print` | `int32` / `var` | `0` | Prints impulse diagnostics. Their format and logging destination are unspecified. | x64, ARM64EC | 2 / 1 | — |
| `MarvelKnockUpAbility.DelayTimeToListenMovementModeChanged` | `float` / `ref` | `0.5` | Delay before listening for movement-mode changes. The help gives no unit. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MarvelProjectile.EnableScenePenetrationOpt` | `bool` / `ref` | `false` | Name suggests a scene-penetration optimization for projectiles. No supplied help. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `MarvelProjectile.SupportHomingThroughPortal` | `bool` / `ref` | `true` | The help says setting 0 disables projectile homing through portals. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `MarvelSolvePenetrationComponent.UseNewMethod` | `bool` / `ref` | `true` | The help maps 0 to disabling the new penetration-resolution method and 1 to enabling it. | — | 3 / 1 | 2 / 1 |
| `MisterFantastic.EnableStateSwitch` | `int32` / `var` | `1` | The help repeats the identifier. The state and conditions are unspecified. | x64, ARM64EC | 2 / 1 | — |
| `MoveToAbilityEx.Debug` | `bool` / `ref` | `false` | Enables debug drawing for movement trajectories, collision, detours, and related movement information. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `MoveToAbilityEx.DebugLifetime` | `float` / `ref` | `10` | Debug line lifetime in seconds. The help gives 10 seconds as the default. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `Movement.MoveLogicFrame.Debug` | `int32` / `var` | `0` | The help maps 0 to disabling the movement logic frame log and 1 to enabling it. | x64, ARM64EC | 2 / 1 | — |
| `Movement.MultiCapsuleBottomHitMargin` | `float` / `ref` | `5` | Margin in centimeters for identifying bottom hits on an extra capsule. The help gives 5 cm as the default. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `P.Chaos.PullPhysicsStateForceUpdateBounds` | `bool` / `ref` | `false` | When enabled, updates rigid particle bounds even if X and R have not changed. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `P.Chaos.Simulation.Enable` | `int32` / `var` | `1` | Controls whether Chaos simulation runs. The help says disabling simulation stops the physics tick. | x64, ARM64EC | 2 / 1 | — |
| `P.Chaos.SyncKinematicOnGameThread` | `int32` / `ref` | `-1` | At 1, kinematic bodies send transforms back to the game thread after simulation. At 0, setting the target updates kinematics immediately. Other values use the per-object UpdateKinematicFromSimulation flag. The help cites -1 as the default. | x64, ARM64EC | 2 / 1 | 5 / 1 |
| `P.Chaos.UpdateKinematicsOnDeferredUseExternelPhysics` | `int32` / `var` | `0` | Toggles the option labeled ExternelPhysics in UpdateKinematicsOnDeferred. The help leaves this option undefined. | x64, ARM64EC | 2 / 1 | — |
| `Physics.MoveActorPerFrame` | `int32` / `var` | `30` | Translated help identifies the number of actors moved per frame. | x64, ARM64EC | 2 / 1 | — |
| `ProjectileHit.EnableCatchUpTailFX` | `bool` / `ref` | `true` | Name suggests enabling projectile catch-up trail effects. No supplied help. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Projectile_10302101.EnableStatistics` | `bool` / `ref` | `false` | Enables statistics for projectile 10302101. The metrics are unspecified. | x64, ARM64EC | 3 / 1 | 5 / 1 |
| `jeff.PassengerSkipChildTransform` | `int32` / `var` | `0` | When enabled, devoured passengers use SetAbsolute to skip UpdateChildTransforms propagation. | x64, ARM64EC | 3 / 1 | — |
| `pathfollow.LogUpdate` | `int32` / `var` | `0` | Logs path-following update data for debugging when true. | x64, ARM64EC | 3 / 1 | — |
| `pm.MaxSimulationIterations` | `int32` / `ref` | `0` | Overrides the maximum simulation iterations for ProjectileMovementComponent. The help says 0 uses the original setting. | x64, ARM64EC | 3 / 1 | 1 / 1 |

## Networking diagnostics

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `NetAnalytics.MinimumNumberOfPacketsForBurstTracking` | `int32` / `ref` | `5` | Minimum notified packet count for considering a frame under percentage-based burst tracking, for incoming or outgoing packets. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `NetAnalytics.NumberOfConsecutiveDroppedPacketsToConsiderBurst` | `int32` / `ref` | `3` | Number of consecutive lost packets required for a loss burst. The packet-count floor used by percentage-based tracking does not apply. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `NetAnalytics.PercentOfDroppedPacketsToConsiderBurst` | `float` / `ref` | `0.2` | Percentage of lost packets in a frame that qualifies as a burst. The help links it to the minimum packet-count setting. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `n.IpNetDriverMaxFrameTimeBeforeAlert` | `float` / `ref` | `1` | Per-frame network processing time in seconds before an alert. Additional processing can trigger another alert in that frame. The help gives 1 second as the default. | x64, ARM64EC | 2 / 1 | 3 / 1 |
| `n.IpNetDriverMaxFrameTimeBeforeLogging` | `float` / `ref` | `10` | Per-frame network processing time in seconds before a warning is logged. The help gives 10 seconds as the default. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `net.TrackAsyncLoadingGUIDThreshold` | `float` / `ref` | `0` | A positive value tracks objects whose asynchronous load exceeds the threshold in seconds, for diagnostics and analytics. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `net.UseRepMontageNew` | `int32` / `ref` | `1` | Enables the new animation-montage replication method. The help leaves the implementation unspecified. | x64, ARM64EC | 2 / 1 | 1 / 1 |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Help translations](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
