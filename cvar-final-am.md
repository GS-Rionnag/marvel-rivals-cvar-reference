# Additional A-M gameplay and engine controls

These 28 exact registry names cover gameplay cues, movement, replication, and HTTP or network diagnostics. Snapshot values are observations from an unspecified capture build. A dash indicates no recorded value or matching evidence in that column.

Build strings are exact names found in build 1.1.4042190. CRC denotes Crash Report Client. The address columns give x64 direct-memory candidates / address-taking instructions. These static observations leave runtime effects and startup override support unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `AI.bForceUseNewAbilityConfig` | `bool` / `var` | `true` | Translated help describes forcing the new AI ability configuration in place of the table setting. | x64, ARM64EC | 3 / 1 | — |
| `Ability134.EnterDeathCheckSimulatedAlive` | `int32` / `var` | `1` | Name suggests a simulated-alive check on entering death handling. No supplied help. | x64, ARM64EC | 3 / 1 | — |
| `Ability231.CVarEnableBuffIdRangeCheck` | `FString` / `ref` | — | Name suggests enabling a buff ID range check. No supplied help on the range or check location. | x64, ARM64EC | 3 / 1 | 1 / 3 |
| `BlockFly.RemoveBuffWhenForbidFlyFailed` | `bool` / `ref` | `true` | The help describes removing the BlockFly buff if forbidding flight fails. It maps 0 to disable and 1 to enable. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `Char.DelayUpdateSimulationLocation` | `bool` / `ref` | `true` | Controls whether a replicated simulation location update is delayed. The help maps 0 to disable and 1 to enable. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `Char.GUseTickDesPenetration` | `bool` / `ref` | `false` | Name suggests a tick-based penetration-resolution option. No supplied help. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `ExecuteScopeNoActorHitCue.Disable` | `int32` / `ref` | `0` | Supplied help links the entry to a server-side per-frame hit-cue limit. The name and help leave the numeric polarity unclear. | — | 3 / 1 | 2 / 1 |
| `ExecuteScopeNoActorHitCue.Suppression.Distance` | `int32` / `ref` | `0` | Supplied help links the entry to a per-frame server hit-cue distance limit. No units or values are described. | — | 3 / 1 | 7 / 1 |
| `ExecuteScopeNoActorHitCue.Suppression.Num` | `int32` / `ref` | `0` | Supplied help links the entry to a per-frame server hit-cue count limit. | — | 3 / 1 | 8 / 1 |
| `Gameplay.Optimize.NetCamUpdateBoostTimeOverride` | `float` / `ref` | `0` | Name suggests an override for network camera update boost duration. No supplied help on units or fallback. | x64, ARM64EC | 2 / 1 | 2 / 1 |
| `Gameplay.Optimize.NetCamUpdateDeltaTimeOverride` | `float` / `ref` | `0` | Name suggests an override for network camera update interval. No supplied help on units or fallback. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `JoyStick.XIMRecord` | `bool` / `ref` | `false` | Name suggests a joystick recording setting. No supplied help on the capture format or trigger. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MarvelBaseCharacter.ReplicatedCameraRotByRPC` | `bool` / `var` | `true` | The help describes camera updates through RPC at 1 and through replicated variables at 0. | x64, ARM64EC | 2 / 1 | — |
| `MarvelRepGraph.CellSize` | `float` / `ref` | `5000` | Name suggests a replication graph cell size. No supplied help on units or indexing. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MarvelRepGraph.SpatialBiasX` | `float` / `ref` | `-25000` | Name suggests an X-axis spatial bias for the replication graph. No supplied help on units or origin. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MarvelRepGraph.SpatialBiasY` | `float` / `ref` | `-25000` | Name suggests a Y-axis spatial bias for the replication graph. No supplied help on units or origin. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `MisterFantastic.EnableSyncTolerance` | `int32` / `var` | `1` | The help maps 1 to enabling network sync tolerance for Mister Fantastic's energy threshold detection and 0 to disabling it. | x64, ARM64EC | 2 / 1 | — |
| `Movement.Stat.Record` | `bool` / `ref` | `false` | The help describes recording movement statistics and sending them to the server. Fields and frequency are unspecified. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `ability_136.EnableAddInputPreConsume` | `bool` / `ref` | `true` | Translated help maps 0 to the original AddMoveInput call in Tick and 1 to processing input before Consume. | x64, ARM64EC | 3 / 1 | 8 / 1 |
| `backchannel.logerrors` | `int32` / `ref` | `1` | Logs packet errors. The help leaves the destination and verbosity unspecified. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `backchannel.logpackets` | `int32` / `ref` | `0` | Logs incoming packets. The help leaves the captured fields and destination unspecified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `cb.debug.msg` | `int32` / `var` | `0` | Name suggests debugging messages. No supplied help on the subsystem or output. | x64, ARM64EC | 3 / 1 | — |
| `http.CurlEventLoopEnableChance` | `int32` / `var` | `100` | Supplied help gives a 0 to 100 chance of enabling the cURL event loop. Sampling behavior is unspecified. | x64, ARM64EC, CRC | 2 / 1 | — |
| `http.EnableChannel` | `int32` / `var` | `1` | The help maps 0 to disabled and 1 to enabled and describes a fix for HTTP resource occupancy. Channel semantics are unspecified. | x64, ARM64EC, CRC | 3 / 1 | — |
| `http.LogQueueUrl` | `int32` / `var` | `1` | The help describes URL-limit debugging. The exact log contents are unspecified. | x64, ARM64EC, CRC | 3 / 1 | — |
| `http.SetRunningThreadedRequestLimit` | `int32` / `var` | `0` | Name suggests a limit on running threaded HTTP requests. No supplied help on scope or boundary behavior. | x64, ARM64EC, CRC | 3 / 1 | — |
| `m2207.ability_136.BindControllerChanged` | `bool` / `ref` | `false` | Name suggests binding to controller-change notifications for ability 136. No supplied help. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `mass.UpdateVisibleAfterRep` | `bool` / `ref` | `true` | Name suggests updating Mass visibility after replication. No supplied help. The registry contains 2 rows under this exact name. Address counts combine the rows. | x64, ARM64EC | 6 / 2 | 2 / 2 |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Help translations](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
