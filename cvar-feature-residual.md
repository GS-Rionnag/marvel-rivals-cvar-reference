# Additional feature and diagnostic CVars

These 30 registry variables cover presentation, asset loading, diagnostics, and runtime housekeeping. Snapshot values are observations from an unspecified capture build. A dash marks the absence of a value or match in that source.

The build string column lists exact names found in the build 1.1.4042190 inventory. CRC denotes Crash Report Client. The two address columns report x64 scan counts as direct-memory candidates / address-taking instructions. These observations leave runtime effects and startup override support unverified.

## Presentation and assets

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `BigHead.GFixBigHeadRedirectionTable` | `bool` / `ref` | `true` | The name suggests a fix for the Big Head redirection table. The registry supplies no help. | x64, ARM64EC | 2 / 1 | 3 / 1 |
| `CharacterMaterialComponent.CacheDefaultMaterials` | `bool` / `var` | `false` | The name suggests caching default character materials. The cache scope is unspecified. | — | 3 / 1 | — |
| `CurveTable.RemoveRedundantKeys` | `int32` / `ref` | `1` | The name suggests removing redundant curve table keys. Selection and timing are unspecified. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `GP.CustomSplitLayout` | `bool` / `var` | `true` | The name suggests a custom split layout. The registry supplies no help on scope or format. | x64, ARM64EC | 3 / 1 | — |
| `HeadWidget.DebugEnable` | `bool` / `var` | `false` | The name suggests enabling head-widget diagnostics. Output is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `Skin.SkinLoadControl` | `int32` / `var` | `1` | Supplied help maps 0 to no limit and 1 to loading only the default skin. | x64, ARM64EC | 2 / 1 | — |
| `Skin.SkinLoadPerformControl` | `int32` / `var` | `1` | Supplied help maps 0 to no limit and describes 1 as limiting server loading to one skin. It limits the scope to the skin asset loading path that uses SkinID. | x64, ARM64EC | 2 / 1 | — |
| `angela.UseNewMethodForMaterialParam` | `bool` / `ref` | `true` | Selects the new material-parameter method for Angela at 1. The help maps 0 to disabled. | x64, ARM64EC | 3 / 1 | 5 / 1 |
| `anim.AnimNotifyUpdateMaterialParams` | `bool` / `ref` | `false` | The name suggests updating material parameters through an animation notify. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `Zombie.CombineNiagara.SkipFlushAnimCollection` | `bool` / `var` | `true` | The name suggests skipping an animation-collection flush in combined Niagara work for zombies. The registry supplies no help. | x64, ARM64EC | 3 / 1 | — |
| `Venom.ShouldForceDisableTentacleURO` | `bool` / `ref` | `true` | The name suggests suppressing URO for Venom's tentacles. The registry supplies no help on scope or value mapping. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `skin.EnablePerSculptDefaultSkinResourceControl` | `bool` / `ref` | `false` | Controls whether the per-sculpt bAppendDefaultSkinResources setting governs default-skin resource inheritance. The help says 0 preserves legacy selected-skin and default-skin resource loading. | x64, ARM64EC | 3 / 1 | 9 / 1 |

### BigHead redirection-table flag: scan detail

The saved build 1.1.4042190 address scan shows three direct references to `BigHead.GFixBigHeadRedirectionTable` as `cmp BYTE PTR [rip+...],0x0`, at instruction RVAs `0x6BDEEC2`, `0x6BDF2F2`, and `0x6BDF722`. These are byte comparisons against zero, consistent with the registry's `bool` type. The scan table does not include the following conditional branches, so it does not show which path is taken for zero versus nonzero or what “fix” changes. The registry and companion object row have no supplied help; the snapshot value `true` is not a documented default.

## Diagnostics

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `GameplayTags.PrintNetIndiceAssignment` | `int32` / `ref` | `0` | Logs gameplay tag network index assignments. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `Hero.LogMacros` | `FString` / `ref` | — | Sets Hero module log verbosity to Warning, according to the help. | x64, ARM64EC | 2 / 1 | 1 / 2 |
| `HitStat.FlushSize` | `int32` / `var` | `5` | The name suggests a hit-statistics flush size. The registry supplies no help on units or trigger. | x64, ARM64EC | 3 / 1 | — |
| `HitStat.Open` | `int32` / `var` | `0` | The help maps 1 to client, 2 to server, and 3 to both. | x64, ARM64EC | 3 / 1 | — |
| `HitStat.ScreenShot` | `int32` / `var` | `0` | The name suggests a hit-statistics screenshot setting. The trigger is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `HitStat.ServerRawHit` | `int32` / `var` | `0` | For hit statistics, the help maps 0 to the final result and 1 to the raw hit. | x64, ARM64EC | 3 / 1 | — |
| `HitStat.Total` | `int32` / `var` | `1000` | The name suggests a hit-statistics total. What it counts is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `SigMan.FilterTag` | `FString` / `var` | — | Filters the Significance Manager debug display by tag. The help says None shows objects with any tag. | x64, ARM64EC | 3 / 1 | — |
| `SigMan.ObjectsToShow` | `int32` / `ref` | `15` | Controls how many objects the Significance Manager debug display shows. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `SwingingComponent.DebugCamera` | `bool` / `ref` | `false` | Toggles swinging camera debugging. The help maps 0 to no and 1 to yes. | x64, ARM64EC | 2 / 1 | 0 / 1 |
| `TestStake.PointLifeTime` | `float` / `ref` | `-1` | The name suggests a TestStake point lifetime. The registry supplies no help on units or trigger. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `TestStake.PointSize` | `float` / `ref` | `10` | The name suggests a TestStake point size. The registry supplies no help on units or rendering. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Tether.DebugParticle` | `int32` / `var` | `-1` | Selects a simulation particle by unique ID for verbose diagnostics. | x64, ARM64EC | 3 / 1 | — |
| `Tether.DebugSubstep` | `int32` / `var` | `-1` | Selects a simulation substep number for verbose diagnostics. | x64, ARM64EC | 3 / 1 | — |

## Runtime housekeeping

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `AbilityActorPool.CheckRecycleInterval` | `float` / `ref` | `15` | The name suggests the ability-actor pool's recycle-check interval. Timing units are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `AbilityActorPool.LimitTime` | `int32` / `ref` | `0` | The name suggests a time limit for the ability-actor pool. The registry supplies no help on units or what the limit covers. | x64, ARM64EC | 3 / 1 | 5 / 1 |
| `AbilityActorPool.TickPoolRecycle.Enable` | `bool` / `ref` | `false` | The name suggests toggling tick-based recycling for the ability-actor pool. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `grpc.nexting.threads` | `int32` / `var` | `16` | Supplied help identifies the number of threads for gRPC Next processing. Thread ownership and when the value is read are unspecified. | x64, ARM64EC | 3 / 1 | — |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
