# Additional A-M feature CVars

These 35 exact registry names cover gameplay cues, diagnostics, event processing, and engine settings. Snapshot values are observations from an unspecified capture build. A dash indicates no value or matching evidence in that column.

The build string column lists names found in build 1.1.4042190. CRC denotes Crash Report Client. The two address columns give x64 direct-memory candidates / address-taking instructions. These matches leave runtime effects and startup override support unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `ABS.EnableHittedDisplay` | `bool` / `ref` | `true` | Name suggests a display toggle for hit feedback. The affected display is unspecified. | x64, ARM64EC | 3 / 1 | 10 / 1 |
| `ABS.GTickClearSessionDataRate` | `float` / `ref` | `5` | Name suggests a rate for clearing session data during ticks. Units are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `ABS.TagUpdateFuncOptimize` | `bool` / `ref` | `false` | Name suggests optimizing tag updates. The affected function and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `AOI.Enter.Delay` | `float` / `ref` | `0.2` | Name suggests a delay associated with AOI entry. The trigger and unit are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `AOI.Enter.TickRate` | `int32` / `ref` | `30` | Name suggests a rate for processing AOI entry. The unit and scheduling behavior are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Aero.DisableNoCrookedInputRemaining` | `bool` / `ref` | `true` | Help gives 0 as disable and 1 as enable but leaves the named input behavior undefined. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `BirthBase.EnableBoundsTestBeforeOverlap` | `bool` / `ref` | `true` | Name suggests a bounds test before an overlap check. The affected objects and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `BitReader.LogFatalOnOverflow` | `bool` / `ref` | `false` | The help describes issuing a fatal log if BitReader overflows. | x64, ARM64EC, CRC | 3 / 1 | 1 / 1 |
| `Bond.EnableRegister` | `bool` / `ref` | `true` | Translated help describes controlling registration of linked characters. At 0, OnRegisterCharacter returns immediately. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Bond.UseRepBondState` | `bool` / `ref` | `true` | Name suggests using replicated bond state. The affected scope and alternative are unspecified. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `ChildActor.EnableNetAddressable` | `bool` / `ref` | `false` | Name suggests a setting for making child actors network-addressable. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `ClientCommunication.EnableAsync` | `int32` / `var` | `1` | Name suggests controlling asynchronous client communication. The affected work is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `CombatExp.Open` | `bool` / `ref` | `false` | Name suggests enabling a combat experience feature. The registry supplies no help on the feature or values. | x64, ARM64EC | 3 / 1 | 4 / 1 |
| `Cue.BuffMaterialCull.DistanceCM` | `int32` / `ref` | — | The help gives a maximum application distance in centimeters from the local camera for BuffCue materials when culling is enabled. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `CueDeath.ExecuteEndOfFrame` | `bool` / `ref` | `false` | Name suggests executing death cue work at the end of the frame. The work affected is unspecified. | x64, ARM64EC | 3 / 1 | 3 / 1 |
| `CueDeath.HideMesh.AllowVisibilityOpimization` | `bool` / `ref` | `true` | Name suggests allowing a visibility optimization on the hide-mesh death-cue path. The exact spelling is preserved. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `CueDeath.Normal.AllowVisibilityOpimization` | `bool` / `ref` | `false` | Name suggests allowing a visibility optimization on the normal death-cue path. The exact spelling is preserved. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `CueDeath.ReplaceRagdollWithHideMesh` | `bool` / `ref` | `false` | Name suggests hiding the mesh in place of a death ragdoll. The applicable cases are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `DataCollection.EnableMoveLogicValueDataCollection` | `bool` / `ref` | `false` | Name suggests enabling movement-logic value data collection. The registry supplies no help on collected fields. The registry has 642 rows under this exact name. Scan counts here count distinct instruction, target, and field combinations across those rows. | x64, ARM64EC | 1926 / 642 | 0 / 642 |
| `Event.MergeDamge` | `int32` / `var` | `1` | Name suggests merging damage events. The registry supplies no help on merge criteria. | x64, ARM64EC | 2 / 1 | — |
| `Event.MergeDeathEvent` | `int32` / `ref` | `0` | The help says eligible Mass monster death events are bucketed by killer, target class, and ability ID only in the DataBase merged dispatcher. It maps 0 to off (default) and 1 to on. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `FireTask.NewDelayEndTask` | `bool` / `ref` | `true` | Name suggests an alternate delayed end-task path. The registry supplies no help. | x64, ARM64EC | 2 / 1 | 3 / 1 |
| `Gameplay.AllowDamgeEventMergeByClass` | `bool` / `ref` | `true` | The help describes allowing damage events to merge into other actors of the same class. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Gameplay.GForceEnableBuffOpt` | `int32` / `ref` | — | Name suggests forcing a buff optimization. The optimization is unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `GameplayCueSet.FailedWhenTryLoadCue` | `bool` / `ref` | `true` | Name associates the setting with a failure during a cue load attempt. The registry supplies no help. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `GameplayTags.UseIntPacked` | `int32` / `var` | `1` | Name suggests a packed integer representation for gameplay tags. The serialized data and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | — |
| `Hero_1062.Ability_106241.DebugDrawBitePath` | `int32` / `ref` | `0` | Translated help describes debug drawing for the capsule trajectory of a character caught in the bite ability. It maps 0 to off and 1 to on and limits drawing to the controlling side. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Hero_1062.Ability_106241.DebugDrawBitePathLifeTime` | `float` / `ref` | `5` | Translated help gives the bite-path debug drawing lifetime in seconds. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `HiddenSubsystem.Enable` | `bool` / `var` | `true` | The help describes a toggle for HiddenSubsystem. Its role is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `MarvelAILibrary.AIShippingTestEnabled` | `bool` / `ref` | `false` | Name suggests a switch for AI testing in Shipping. Test behavior is unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `angela.WingThresholdToForceReplayEffect` | `float` / `ref` | `0.9` | The help gives 0 as disable and 1 as enable and leaves the wing threshold behavior undefined. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `battlerule.DefaultPVE.AbilityInitFallbackTime` | `float` / `var` | `5` | Fallback delay in seconds before Default PVE applies effects when ability initialization never finishes. The help says 0 applies immediately. | x64, ARM64EC | 3 / 1 | — |
| `battlerule.DefaultPVE.SkipAIControlled` | `bool` / `var` | — | When true, the Default PVE effects rule skips AI-controlled characters. | x64, ARM64EC | 3 / 1 | — |
| `clusterunion.callflushnetdormancy` | `bool` / `ref` | `true` | Controls whether the cluster-union path calls FlushNetDormancy, according to the help. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `http.DefaultUserAgentCommentsEnabled` | `bool` / `var` | `true` | Controls whether comments are supported in the default HTTP user-agent string. | x64, ARM64EC, CRC | 2 / 1 | — |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Help translations](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
