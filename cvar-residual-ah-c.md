# Cue handling, engine diagnostics, and profile CVars beginning A–H

This guide adds 37 exact registry names to [batch B](cvar-residual-ah-b.md). A dash means the observed snapshot omits that value. The descriptions summarize registry help. Rows marked as translated use the preserved English translations.

| Exact CVar | Kind / type | Snapshot | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `AI.AILab.DisableUIDCache` | `var` / `bool` | `false` | Bypasses the cached actor UID lookup. Help names the M2207 mode, where PlayerState may change. | 0 / 3 | 0 / 1 |
| `AI.AILab.EnableRuntimeSlotMapping` | `var` / `bool` | `true` | Controls sending runtime slot mappings to AILab. Help gives 0 off and 1 on by default. | 0 / 3 | 0 / 1 |
| `AI.BondUsage.AIAddBondUsage` | `var` / `bool` | `true` | Adds bond usage to AdditionalUsages when the bond state changes. | 0 / 3 | 0 / 1 |
| `AI.HeroTagLogic.ProcessOnInit` | `var` / `bool` | `false` | Executes tag logic for already-active tags during the initial binding. | 0 / 3 | 0 / 1 |
| `AbilityContext.Enable` | `var` / `int32` | `1` | Enables AbilityContext. Help gives no details about its data or lifecycle. | 0 / 2 | 0 / 1 |
| `AbilityContext.EnableDebug` | `var` / `int32` | `0` | Enables debugging of AbilityContext information. Help gives no output format. | 0 / 2 | 0 / 1 |
| `Chaos.Debug.StrainModifier` | `ref` / `float` | `200` | Multiplier applied to strain. Help does not identify the affected strain calculations. | 1 / 3 | 1 / 1 |
| `ClusterUnion.UseAccelerationStructure` | `ref` / `bool` | `false` | Selects an acceleration structure for component-level sweeps and overlaps against cluster unions. | 1 / 3 | 1 / 1 |
| `Cue.LocalRelevanceCull.Categories` | `ref` / `int32` | — | Bitmask for local cue culling. 0 is off, bit 1 applies to buff and effect cues, and bit 2 applies to hit-impact cues. The help tracks whether the corresponding add event was culled before culling a remove event. | 2 / 3 | 1 / 1 |
| `CueFuncLibrary.EnableAutonomousCueDataMap` | `ref` / `bool` | `true` | Builds the hero autonomous cue map. Help says cues in AutonomousOnly load on the autonomous proxy. Translated help. | 2 / 3 | 1 / 1 |
| `Damage.HighDamageLogThreshold` | `var` / `float` | `0` | Logs damage above the threshold. Values at or below zero disable the log. | 0 / 3 | 0 / 1 |
| `EffectComp.EnableSummonedTriggerNoActorCue` | `ref` / `bool` | `true` | Allows a summoned entity to trigger the cue presentation for a spell field without an actor that it created. Help describes the setting as temporary. Translated help. | 1 / 3 | 1 / 1 |
| `GE.SyncStats.Enable` | `var` / `int32` | `0` | Toggles GameplayEffect synchronization statistics. 0 disables and 1 enables. | 0 / 3 | 0 / 1 |
| `GE.SyncStats.SimulateConnectionCount` | `var` / `int32` | `12` | Uses a simulated client count to estimate property replication. 0 uses the actual count. Help limits this setting to property replication estimates and leaves RPC statistics unaffected. | 0 / 3 | 0 / 1 |
| `GameplayCue.AddToGlobalSet.DebugTag` | `var` / `FString` | — | Debug tag for cue registration in the global set. Help leaves the selection format unspecified. | 0 / 3 | 0 / 1 |
| `GameplayCue.EnableCountCue` | `ref` / `bool` | `false` | Counts cue calls by type. Translated help. | 0 / 3 | 1 / 1 |
| `GameplayCue.ForceUnloadGameplayCue` | `ref` / `bool` | `false` | Forces cue cache cleanup after a period with no cues entering the cache. Help supplies no duration. Translated help. | 2 / 3 | 1 / 1 |
| `GameplayCue.OptBuffCueMultiActive` | `ref` / `bool` | `true` | Help describes distance culling for blacklisted cues. It gives no filter details. Translated help. | 1 / 3 | 1 / 1 |
| `GameplayCue.OptCueFrustum` | `ref` / `bool` | `true` | Help describes distance culling for blacklisted cues. The same text appears for OptBuffCueMultiActive and leaves the frustum behavior unconfirmed. Translated help. | 1 / 3 | 1 / 1 |
| `GetLokiPhantoms.CacheEnable` | `var` / `bool` | `true` | Enables the cached GetLokiPhantoms lookup. | 0 / 3 | 0 / 1 |
| `GetTeamComponent.CacheEnable` | `var` / `bool` | `true` | Enables the LRU-cached team component lookup. | 0 / 3 | 0 / 1 |
| `GetTeamComponent.CacheMode` | `ref` / `int32` | `1` | 0 selects an LRU cache for all actors. 1 uses a per-frame TMap cache for Mass projectiles and keeps the LRU cache for other actors. | 2 / 3 | 1 / 1 |
| `HeartBeat.Enable` | `ref` / `bool` | `false` | Enables heartbeat checks at runtime. 0 disables and 1 enables. | 3 / 3 | 1 / 1 |
| `HeartBeat.HangDuration` | `ref` / `float` | `-1` | Hang detection duration in seconds. -1 uses the config value and 0 disables this check. | 1 / 3 | 1 / 1 |
| `HeartBeat.HangsAreFatal` | `ref` / `bool` | `false` | Selects nonfatal handling at 0 or fatal handling at 1 when a hang is detected. | 2 / 3 | 1 / 1 |
| `HeartBeat.PresentDuration` | `ref` / `float` | `-1` | Presentation hang detection duration in seconds. -1 uses the config value and 0 disables this check. | 1 / 3 | 1 / 1 |
| `HeartBeat.StuckDuration` | `ref` / `float` | `-1` | Stuck thread detection duration in seconds. -1 uses the config value and 0 disables this check. | 1 / 3 | 1 / 1 |
| `charmove.EnableLODBasedTickInterval` | `ref` / `bool` | `false` | Uses an LOD-based tick interval for character movement. | 3 / 3 | 1 / 1 |
| `charmove.EnableSkipUpdateOptimization` | `ref` / `bool` | `true` | Enables the ShouldSkipUpdate check. Help gives no skip criteria. | 1 / 3 | 1 / 1 |
| `charmove.UseSkipUpdateNewMethod` | `ref` / `bool` | `true` | Selects the newer ShouldSkipUpdate implementation. Help gives no implementation details. | 3 / 3 | 1 / 1 |
| `cpfuo.AuditAggressiveReferenceReplacment` | `var` / `bool` | `true` | Audits and reports aggressive-path reference replacements. Replacment is the registry spelling. | 0 / 2 | 0 / 1 |
| `cpfuo.UseAggressiveReferenceReplacment` | `var` / `bool` | `false` | Toggles the deprecated aggressive reference replacement path. Replacment is the registry spelling. | 0 / 2 | 0 / 1 |
| `debug.EnableAlternateFunctionDebug` | `ref` / `bool` | `false` | Enables alternate-function debugging. Help gives no output details. | 0 / 3 | 1 / 1 |
| `debug.EnableBarrierDebug` | `ref` / `bool` | `false` | Enables FTaskBarrier debugging. Help gives no output details. | 0 / 3 | 1 / 1 |
| `dp.AllowScalabilityGroupsToChangeAtRuntime` | `var` / `int32` | `0` | Gives device-profile scalability groups scalability priority so they can change at runtime. Help gives off as the default. | 0 / 3 | 0 / 1 |
| `dp.Override` | `var` / `FString` | — | Selects a named device profile and restores any previous override first. Help describes the dp command-line option as taking precedence at startup. | 0 / 3 | 0 / 1 |
| `health.logHealthSnapshot` | `ref` / `int32` | `1` | Logs a health snapshot. Help leaves the trigger and contents unspecified. | 2 / 3 | 1 / 1 |

The scan columns count address matches in Shipping 1.1.4042190. Direct-memory candidates may include writes, reads, or initialization. Runtime effects and override acceptance remain unverified.

See the [preserved source notes](EVIDENCE.md#community-sources) for the registry, translated help, and snapshot, and the [address scan](EVIDENCE.md#build-specific-static-analysis) for match details.
