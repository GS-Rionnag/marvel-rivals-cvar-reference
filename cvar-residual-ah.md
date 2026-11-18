# Graphics, UI, and audio CVars beginning A–H

This guide covers 55 previously uncovered graphics, UI, input presentation, and audio variables in the local community registry. The snapshot column shows observed values, with a dash when the snapshot omits the entry. Defaults mentioned in the descriptions come from the supplied help.

| Exact CVar | Kind / type | Snapshot | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `ActorSequence.DefaultDisplayRate` | `var` / `FString` | — | Default display rate for new level sequences and playback rate for frame-locked sequences. Help accepts rates such as 30 fps or 30000/1001. | 0 / 3 | 0 / 1 |
| `ActorSequence.DefaultEvaluationType` | `var` / `int32` | `0` | 0 locks evaluation to playback frames. 1 allows subframe interpolation. | 0 / 3 | 0 / 1 |
| `ActorSequence.DefaultTickResolution` | `var` / `FString` | — | Default tick resolution for new level sequences. Help gives both frame rates and a 10 ms interval as examples. | 0 / 3 | 0 / 1 |
| `AudioCommand.FenceWaitTimeMs` | `ref` / `int32` | `35` | Fence wait time in milliseconds. Help leaves the specific fence behavior unspecified. | 0 / 2 | 1 / 1 |
| `AudioCommand.WaitUntilEmptyOnEndFrame` | `ref` / `int32` | `1` | Waits for GAudioPipe to empty before the frame sync. | 1 / 2 | 1 / 1 |
| `AudioWorldSubSystem.EnableEventPostedStackDelegate` | `ref` / `bool` | `true` | Broadcasts the audio event-post stack delegate for debugging tools. | 0 / 3 | 1 / 1 |
| `AudioWorldSubSystem.FinalEventNameCache` | `ref` / `bool` | — | Caches the resolved Ak audio event name in PostGetFinalEventName. 0 selects the legacy path and 1 selects caching. | 2 / 3 | 1 / 1 |
| `AudioWorldSubSystem.FinalEventNameCache.Measure` | `ref` / `bool` | — | Measures per-call savings from the final event name cache and accumulates results on cache misses. | 4 / 3 | 1 / 1 |
| `AudioWorldSubSystem.UseDefaultAkEventName` | `var` / `bool` | `false` | Uses the original skin sound event names for every uniform when enabled. | 0 / 2 | 0 / 1 |
| `Bond.HideNonLocalBondCue` | `ref` / `bool` | — | Hides Team-Up effects for characters controlled by someone other than the local player when true. Translated help. | 1 / 3 | 1 / 1 |
| `CameraCalibration.StartupLensFile` | `var` / `FString` | — | Startup lens file. Help leaves the path format, lookup rules, and when the file is used unspecified. | 0 / 3 | 0 / 1 |
| `Canvas.DistanceFieldSmoothness` | `ref` / `float` | `4` | Global sharpness of distance-field fonts and shapes rendered by Canvas. Help does not describe units. | 1 / 2 | 2 / 1 |
| `CommonButton.EnableSimulateHoverOnTouch` | `ref` / `int32` | `1` | Allows buttons configured with SimulateHoverOnTouchInput to simulate hover on touch. Help gives 0 disabled and 1 enabled by default. | 2 / 2 | 1 / 1 |
| `CommonInput.EnableGamepadPlatformCursor` | `ref` / `bool` | `false` | Allows cursor use during gamepad input. | 1 / 3 | 1 / 1 |
| `CommonInput.ShowKeys` | `ref` / `int32` | `1` | Shows keys for the current input device. | 3 / 3 | 1 / 1 |
| `CommonRichTextBlock.CVarApplyMobileScaleOnTextRuns` | `ref` / `int32` | `0` | Controls mobile scaling when rich-text runs are created. Help gives 0 as the disabled default because scaling tagged text can apply the factor twice. | 1 / 2 | 1 / 1 |
| `Compat.MAX_GPUSKIN_BONES` | `ref` / `int32` | `65536` | Caps the per-platform project limit on bones GPU-skinned in one draw call. Help says the cap is fixed at runtime. | 4 / 3 | 1 / 1 |
| `Compat.UseDXT5NormalMaps` | `var` / `int32` | `0` | Selects DXT5 for normal maps when enabled and BC5 otherwise. Help notes that BC5 support varies across hardware. | 0 / 2 | 0 / 1 |
| `CriticalPathStall.AfterInitViews` | `var` / `float` | `0` | Adds a debug sleep after InitViews, in milliseconds, for critical-path analysis. | 0 / 3 | 0 / 1 |
| `CriticalPathStall.ParallelAnimation` | `var` / `float` | `0` | Adds a debug sleep to each parallel animation task, in milliseconds, for critical-path analysis. | 0 / 3 | 0 / 1 |
| `Cue.BuffMaterialCull.Enable` | `ref` / `int32` | — | Culls the active buff cue material by distance and local view frustum at activation. | 1 / 3 | 1 / 1 |
| `Cue.EnableNiagaraMultiPassPortal` | `ref` / `bool` | `true` | Lets Niagara effects pass through portals multiple times. Translated help. | 1 / 3 | 1 / 1 |
| `CueDeath.HideMesh.DontForceUpdateAnimation` | `ref` / `bool` | `true` | Controls whether the death dissolve effect skips a forced animation update. Translated help. | 1 / 3 | 1 / 1 |
| `Dump.IndividualOcclusionTestPrimitives` | `ref` / `int32` | `0` | Dumps individual occlusion-test primitives. Help leaves the format and destination unspecified. | 0 / 3 | 1 / 1 |
| `EOSVoiceChat.FakeAudioInputEnabled` | `var` / `bool` | `false` | Controls fake audio input for EOS voice chat. Help leaves the source and testing behavior unspecified. | 0 / 3 | 0 / 1 |
| `Electra.DX.H265.LegacyInputSampleCleanOrder` | `var` / `int32` | `0` | Controls H.265 input sample release relative to the Media Foundation Transform flush. The help-stated default `0` releases samples after the transform drops its references. `1` releases before flushing. | 0 / 3 | 0 / 1 |
| `EnhancedInput.EnableDefaultMappingContexts` | `ref` / `int32` | `1` | Applies developer-configured default mapping contexts to every UEnhancedPlayerInput. | 1 / 3 | 1 / 1 |
| `EnhancedInput.OnlyTriggerLastActionInChord` | `ref` / `int32` | `1` | Fires only the last action in a chord when enabled. Otherwise the dependent chords fire too. | 1 / 3 | 1 / 1 |
| `EnhancedInput.bShouldLogAllWorldSubsystemInputs` | `ref` / `bool` | `false` | Logs each InputKey call to the World subsystem when enabled. | 0 / 3 | 1 / 1 |
| `GPUSort.DebugOffsets` | `var` / `int32` | `0` | GPU sort offset diagnostics. Help leaves output and modes unspecified. | 0 / 3 | 0 / 1 |
| `GPUSort.DebugSort` | `var` / `int32` | `0` | GPU sorting diagnostics. Help leaves output and modes unspecified. | 0 / 3 | 0 / 1 |
| `GroomCache.EnableStreaming` | `ref` / `bool` | `true` | Enables streaming and prebuffering for groom caches. Help advises keeping the setting fixed while the caches are in use. | 7 / 3 | 1 / 1 |
| `HeadWidget.DebounceScale` | `var` / `float` | `1` | Scale factor for head-position debouncing. Smaller values follow the pelvis more closely. Translated help. | 0 / 3 | 0 / 1 |
| `HeadWidget.P` | `var` / `float` | `0.1` | Interpolation speed for the character head-position widget. Translated help. | 0 / 3 | 0 / 1 |
| `Hero.1047.DebugWaterFlow` | `ref` / `int32` | `0` | Water-flow diagnostics for Hero 1047. Help gives no diagnostic output or mode details. | 1 / 3 | 1 / 1 |
| `HeroAccessory.ReapplyNotifyVisibilityOnAttach.Enable` | `var` / `bool` | `true` | Reapplies active ANS_SetComponentsInActorVisible states after a deferred hero accessory attach. | 0 / 3 | 0 / 1 |
| `HeroAccessory.WeaponSwitchSkeletonReattach.Enable` | `var` / `bool` | `true` | Enables a hero accessory skeleton retarget attach when switching weapons. | 0 / 3 | 0 / 1 |
| `HeroAccessoryRotator.EnableRotation` | `var` / `bool` | `true` | Help repeats the variable name. The name suggests an accessory rotation switch. | 0 / 3 | 0 / 1 |
| `HeroAccessoryRotator.EnableTickRotation` | `var` / `bool` | `true` | Help repeats the variable name. The name suggests a switch for accessory rotation during ticks. | 0 / 3 | 0 / 1 |
| `HpBar.ParallelUpdateEnabled` | `ref` / `bool` | `true` | Deprecated switch for parallel updates of health-bar widgets. | 0 / 3 | 1 / 1 |
| `HpBar.SkipRedundantParamUpdate` | `ref` / `int32` | `1` | 1 skips redundant SetScalarParameterValue calls and is the help-stated default. 0 always updates. | 2 / 3 | 1 / 1 |
| `combinefx.UseSubsystemDriver` | `ref` / `bool` | `false` | 1 batches CueCombine work in parallel at TG_EndPhysics in ordinary worlds. Duplicated worlds use per-component batch ticks. 0 uses the per-component path in all worlds. Help says switches apply fully to newly created effects. Translated help. | 2 / 3 | 1 / 1 |
| `con.MinLogVerbosity` | `var` / `int32` | `0` | Controls the verbosity of logs displayed in the in-game console. Help describes 0 as showing only console responses. | 0 / 2 | 0 / 1 |
| `console.position.enable` | `var` / `int32` | `0` | Enables custom console placement. | 0 / 3 | 0 / 1 |
| `console.position.x` | `var` / `int32` | `0` | Console horizontal offset from the left border. Help gives no unit. | 0 / 3 | 0 / 1 |
| `console.position.y` | `var` / `int32` | `0` | Console vertical offset from the bottom border. Help gives no unit. | 0 / 3 | 0 / 1 |
| `console.searchmode.legacy` | `var` / `bool` | `false` | Uses legacy search for console commands. | 0 / 3 | 0 / 1 |
| `cue.UpgradeAssetExpireSeconds` | `ref` / `float` | `30` | Seconds from ConsumerCount reaching zero to releasing the cue upgrade StreamableHandle. Help gives 30 seconds as the default. Translated help. | 4 / 3 | 1 / 1 |
| `cue.UpgradeLRU.CloneTTLSeconds` | `ref` / `float` | — | Seconds before idle Clone Montage or Clone StaticCue instances are destroyed. Help gives 30 seconds as the default. Translated help. | 1 / 3 | 1 / 1 |
| `cue.UpgradeLRU.Enabled` | `ref` / `int32` | — | Runtime switch for the cosmetic cue-upgrade least-recently-used cache, alongside its compile-time guard. Help gives 1 enabled and 0 disabled during editor validation. Translated help. | 6 / 3 | 1 / 1 |
| `d3d11.ZeroBufferSizeInMB` | `var` / `int32` | `4` | D3D11 static zero allocation for asynchronous texture streaming. Help gives 4 MB as the default and relates the buffer size to the largest mipmap being streamed. | 0 / 2 | 0 / 1 |
| `decal.enable_pool` | `ref` / `bool` | `true` | Enables decal pooling. Help leaves its policy unspecified. | 5 / 2 | 1 / 1 |
| `framegrabber.framelatency` | `ref` / `int32` | `0` | Frames to wait before frame readback. Help says 0 is valid and can stall performance by synchronizing the CPU and GPU. | 4 / 3 | 1 / 1 |
| `g.TimeToBlockOnRenderFence` | `ref` / `int32` | `1` | Milliseconds the game thread blocks while waiting on a render-thread fence. | 2 / 3 | 1 / 1 |
| `g.TimeoutForBlockOnRenderFence` | `ref` / `int32` | `60000` | Milliseconds the game thread waits before failing when a render-thread fence does not complete. | 1 / 3 | 1 / 1 |

The two scan columns count candidates at the registry's reference and object addresses in Shipping build 1.1.4042190. Candidates may include initialization, reads, and writes. Runtime behavior, availability, and startup override acceptance remain unverified.

Help, translations, and snapshot values come from the [preserved community sources](EVIDENCE.md#community-sources). The [address-match TSV](EVIDENCE.md#build-specific-static-analysis) and [build analysis](EVIDENCE.md#build-specific-static-analysis) describe the static evidence.
