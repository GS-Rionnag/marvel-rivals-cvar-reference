# Static value reads for unresolved `demo.*` CVars

All 103 lower-case `demo.*` entries in the [CVar definition gaps](cvar-unresolved-definitions.md) already have rows in the replay guides. Both community help columns are empty for these names, and the pinned community config has no exact-name matches. The archived Epic UE 5.9 comparison supplied no definitions for this set. [Evidence and sources](EVIDENCE.md) describes the local evidence scope. Epic's [replay architecture overview](https://dev.epicgames.com/documentation/unreal-engine/demonetdriver-and-streamers-in-unreal-engine) describes the upstream `DemoNetDriver` and its streamers.

## Build 1.1.4042190 reads

Filtering the saved Shipping-build scan to exact names and `target_field=ref_rva` gives 44 matches for the 18 community `ref` entries. The 18 `lea` instructions take the address. In the other 26 instructions, the matching address supplies a value to a compare, load, or multiply. The count below excludes object-field matches. The 85 community `var` entries lack a backing `ref_rva` in the source, so this method cannot establish value use for those entries. See the [build-specific scan scope and limitations](EVIDENCE.md#build-specific-static-analysis).

| CVar | Reads | Operation at the matched backing address |
| --- | ---: | --- |
| `demo.CleanupOutstandingRewindComponents` | 2 | Compares a 32-bit value with zero and, separately, with a register. |
| `demo.DebugCameraAngleThreshold` | 1 | Compares a single-precision float with another float. The instruction does not identify the quantity or angular unit. |
| `demo.DebugReplayNotFound` | 1 | Compares a byte with a register. The comparison does not supply a constant. |
| `demo.DoNotCreateReplayWidget` | 1 | Loads a byte and zero-extends it to a 32-bit register. |
| `demo.HologramReplay.DisableLight` | 1 | Compares a 32-bit value with zero. |
| `demo.HologramReplay.Enable` | 4 | Two comparisons with zero and two with registers, all 32-bit. |
| `demo.HologramReplay.FakePersistent` | 1 | Compares a 32-bit value with zero. |
| `demo.HologramReplay.OpenAudio` | 1 | Compares a 32-bit value with zero. |
| `demo.HologramReplay.PlaybackCompleteStop` | 5 | Three 32-bit loads and two 32-bit comparisons with zero. |
| `demo.HologramReplay.UpdateLocalPlayerState` | 1 | Compares a byte with zero. |
| `demo.Playback.AutonomousView.FreeReset` | 1 | Compares a 32-bit value with a register. |
| `demo.Playback.AutonomousView.Opt` | 1 | Compares a 32-bit value with zero. |
| `demo.Playback.AutonomousView.PauseFreeReset` | 1 | Compares a 32-bit value with a register. |
| `demo.Playback.AutonomousView.PingRate` | 1 | Supplies a single-precision multiplier. The scan leaves the scaled quantity and units unresolved. |
| `demo.ProcessPacketTimeLimit` | 3 | Three single-precision loads. The scan leaves the time unit and enforcement point unresolved. |
| `demo.SkipMulticastRPC` | 1 | Compares a 32-bit value with zero. The instruction does not distinguish the semantics of positive values. |

The two names with address-taking matches only are `demo.CustomData.Test` and `demo.HologramReplay.InitVisable`. The address association comes from the community table. The saved instructions alone leave name-to-storage registration, execution conditions, branch outcomes, runtime availability, and loader acceptance unverified.

## Nearby text checks

Some text windows in the local scan of neighboring binary text match exact help for a different entry in the community variable table. For example, the gRPC/HTTP selector beside `demo.AutoCycle.DelayTime` matches `demo.LowDelayMode.UseGRPC`, the deferred-close rule beside `demo.Playback.AutonomousView.PingRate` matches `demo.Playback.AutonomousView.DrainBeforeOpen`, and the three replay data formats beside `demo.TimeoutReplayNetConnection` match `demo.DeathReplay.ServerDataVersion`. Those windows cannot establish definitions for the unresolved names.
