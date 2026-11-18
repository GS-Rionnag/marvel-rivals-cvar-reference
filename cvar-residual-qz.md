# Residual Q–Z engine, graphics, UI, and audio CVars

This batch records 54 unique, currently uncovered `var`/`ref` names beginning Q–Z (case-insensitive), excluding names with the exact lowercase `r.` prefix. It prioritizes engine, rendering, animation, UI/window/input, audio, media, and runtime-support settings. It is a focused subset, not a claim that every Q–Z registry name has been documented.

Descriptions reproduce supplied help or use the preserved assistant translation where the help is Chinese; those translations have not been independently reviewed. Rows with blank help are labeled unresolved rather than guessed from their names. Snapshot values are captured observations, not verified defaults or recommendations. Build scan counts refer to static address-reference candidates: they do not establish execution, runtime registration, config acceptance, or in-game effect.

## Graphics, rendering, and animation
| Exact CVar | Type / kind | Snapshot | Supplied help / conservative meaning | Build 1.1.4042190 scan candidates |
| --- | --- | --- | --- | --- |
| `RHIPoolAllocator.DefragMaxPoolsToClear` | int32 (`ref`) | 1 | Maximum amount of pools to try and clear during a single alloctor defrag call (default: 1 - negative then all pools will be tried and no timeslicing) | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `RHIPoolAllocator.DefragSizeFraction` | float (`ref`) | 0.9 | Skip defrag of pool if usage is more than given fraction (default: 0.9f). | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `RHIPoolAllocator.ValidateLinkedList` | int32 (`ref`) | 0 | Validate all the internal linked list data of all the RHIPoolAllocators during every operation. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `RigVM.DisableExecutionAll` | int32 (`var`) | 0 | if nonzero we disable all execution of rigvms. | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `RigVM.DisableNativizedVMs` | int32 (`var`) | 1 | if nonzero we disable swapping to nativized VMs. | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `RigVM.EnableDrawInterfaceInShipping` | int32 (`var`) | 0 | Set to 1 to enable control rig draw interface in shipping | obj: 2 direct candidate(s), 1 address-taking reference(s). |
| `RigVM.UInterfaceSupport` | bool (`var`) | true | When true the RigVMCompiler will allow UInterfaces. | obj: 2 direct candidate(s), 1 address-taking reference(s). |
| `SkeletalMesh.FollowerCurveDoubleBuffered` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 3 direct candidate(s), 1 address-taking reference(s). |
| `SkeletalMesh.OnPostLoadToCDO` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `SkeletalMesh.OnRegisterLoad` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `SkeletalMesh.OnRegisterLoadToCDO` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 4 direct candidate(s), 1 address-taking reference(s). |
| `Skelot.GlobalTransitionBudgetLimit` | int32 (`ref`) | 300 | Global transition budget limit per frame across all SkelotComponents. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 5 direct candidate(s), 1 address-taking reference(s). |
| `Skelot.LocalBoundUpdateInterval` | float (`ref`) | 0.04 | No supplied help. Name alone is insufficient to establish behavior. | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `Skelot.QueryTransform.SkipFlushDeferredTransitions` | bool (`ref`) | true | Skip ConditionalFlushDeferredTransitions in transform query paths and read cached pose data only. true: never trigger deferred flush from query functions (default, safer for worker threads). false: fallback to the legacy behavior and allow query-triggered flush. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 3 direct candidate(s), 1 address-taking reference(s). |
| `SkelotAnimCollection.AllowAsyncFlushDeferredTransitions` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `VA.DisableSystem` | bool (`var`) | false | When true the VA system will be disabled as though 'SystemName' was 'None' | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `VA.LazyInitSystem` | bool (`var`) | false | When true the VA system will be lazy initialized on first use | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `xr.VRS.DynamicFoveation` | int32 (`var`) | 0 | Whether foveation level should adjust based on GPU utilization<br> 0: Disabled (default);<br> 1: Enabled | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `xr.VRS.FoveationLevel` | int32 (`var`) | 0 | Level of foveated VRS to apply (when Variable Rate Shading is available)<br> 0: Disabled (default);<br> 1: Low;<br> 2: Medium;<br> 3: High;<br> 4: High Top; | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `xr.VRS.FoveationPreview` | int32 (`var`) | 1 | Include foveated VRS in the VRS debug overlay. 0: Disabled;<br> 1: Enabled (default) | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `xr.VRS.GazeTrackedFoveation` | int32 (`var`) | 0 | Enable gaze-tracking for foveated VRS<br> 0: Disabled (default);<br> 1: Enabled | obj: 3 direct candidate(s), 1 address-taking reference(s). |

## User interface, windowing, and input
| Exact CVar | Type / kind | Snapshot | Supplied help / conservative meaning | Build 1.1.4042190 scan candidates |
| --- | --- | --- | --- | --- |
| `SafeZone.EnableScale` | bool (`ref`) | false | IS the safe zone scale enabled? | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `SafeZone.Scale` | float (`ref`) | 1 | The safezone scale. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `Show.ObTick.Ray` | int32 (`var`) | 0 | No supplied help. Name alone is insufficient to establish behavior. | obj: 2 direct candidate(s), 1 address-taking reference(s). |
| `TypedElements.EnableElementsCopyAndPaste` | int32 (`ref`) | 0 | Is support for elements copy and paste enabled? | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `TypedElements.EnableFoliageInstanceElements` | int32 (`ref`) | 0 | Is support for static mesh instance elements enabled for foliage owned instances? | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `TypedElements.EnableSMInstanceElements` | int32 (`ref`) | 1 | Is support for static mesh instance elements enabled? | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `Widget.DisablePreConstructInRuntime` | bool (`var`) | true | Disable PreConstruct at runtime. (assistant translation; not independently reviewed) | obj: 2 direct candidate(s), 1 address-taking reference(s). |
| `Widget.MaxAnimationLatentActions` | int32 (`var`) | 100 | Defines the maximum number of latent actions that can be run in one frame. | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `Widget.UseParallelAnimation` | bool (`var`) | true | Use multi-threaded evaluation for widget animations. | obj: 2 direct candidate(s), 1 address-taking reference(s). |
| `Widget3D.AllowToSetVisibleNextFrame` | bool (`ref`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `Widget3D.DebugDrawInteraction` | bool (`var`) | — | Draw the hit surface of interactive 3D UI on screen to check whether the hit box aligns with the rendered image. (assistant translation; not independently reviewed) | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `Widget3D.DisablePixelSnapping` | bool (`var`) | true | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `Widget3D.InputEnabled` | bool (`var`) | — | 3D UI input channel (enabled by default): 1 uses the new proxy input; 0 clears proxy input and restores the component’s original input rules. Widgets with EnableInput(true) switch on the manager’s next update; reopening restores their request. (assistant translation; not independently reviewed) | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `WidgetAnimationProfiler.CountRedundant` | bool (`ref`) | true | Whether to count redundant MarvelSetAnimationTime calls within the same frame. (Default: 1) | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `WidgetAnimationProfiler.DelayCalling` | bool (`ref`) | false | Whether to delay all MarvelSetAnimationTime calls to end of frame. Only the last call per Widget+Animation will be executed. (Default: 0) | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `WindowsApplication.EnableFirstTouchEvent` | bool (`ref`) | false | Enable FirstTouch Event which prevents small pop on some touch input devices | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `WindowsApplication.UseWorkerThreadForRawInput` | bool (`ref`) | false | Use a worker thread for raw input messages to remove processing from game thread. Mice with high polling rates can take multiple milliseconds per frame even on fast CPUs. When the cvar is changed a CVarSinkHandler will attempt to switch the thread used for handling inputs. | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 4 direct candidate(s), 1 address-taking reference(s). |
| `WindowTitleBar.ForceWindowButtonsHidden` | bool (`var`) | false | If true, force the window title bar buttons to be hidden. | obj: 3 direct candidate(s), 1 address-taking reference(s). |

## Runtime, scheduling, and diagnostics
| Exact CVar | Type / kind | Snapshot | Supplied help / conservative meaning | Build 1.1.4042190 scan candidates |
| --- | --- | --- | --- | --- |
| `shaderpipeline.MinPrecompileTasksInFlight` | int32 (`ref`) | 10 | Note: Only used when threadpool PSO precompiling is active.<br>The number of active PSO precompile jobs in flight before we will submit another batch of jobs. <br>i.e. when the number of inflight precompile tasks drops below this threshold we can add the next batch of precompile tasks. <br>This is to prevent bubbles between precompile batches but also to avoid saturating dispatch. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `slate.ForbidLineBreakerUpdateTextLayout` | bool (`ref`) | false | For slate perf, prevent updating TextLayout every frame. | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `StateMachine.Transition.Opt` | int32 (`ref`) | 1 | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 3 direct candidate(s), 1 address-taking reference(s). |
| `stats.AutoEnableNamedEventsWhenProfiling` | bool (`ref`) | false | If 1, toggles named events on when a profiler is detected and capturing. Toggles named events off if 0 or when profiling stops. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 0 direct candidate(s), 1 address-taking reference(s). |
| `Throttle.Enable` | bool (`ref`) | false | Global toggle for adaptive tick throttling. 0=disabled (all intervals return 1), 1=enabled. Default 0. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `Throttle.Enable.PinnedMotion` | bool (`ref`) | false | Enable adaptive tick throttling for PinnedMotion PinOther tasks (0=off, 1=on). Default 0.<br>Enable adaptive tick throttling for PinnedMotion V2 tasks (0=off, 1=on). Default 0. | obj: 6 direct candidate(s), 2 address-taking reference(s); ref: 1 direct candidate(s), 2 address-taking reference(s). |
| `TickingGroup.AbilitySystem.Enable` | bool (`ref`) | true | Whether move abilitysystem's TickingGroup | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 5 direct candidate(s), 1 address-taking reference(s). |
| `TickingGroup.AnimTimeline.Enable` | bool (`ref`) | true | Whether move AnimTimeline's TickingGroup | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 6 direct candidate(s), 1 address-taking reference(s). |
| `WindowsPlatformCrashContext.ForceCrashReportDialogOff` | bool (`var`) | false | If true, force the crash report dialog to not be displayed in the event of a crash. | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `world.EnableGCPhysicsObjectLoadHelper` | int32 (`ref`) | 1 | if true, finish adding level to world when all gc actors have created physics object. | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 3 direct candidate(s), 1 address-taking reference(s). |
| `world.EnableLevelCollectionTimerManager` | bool (`ref`) | true | if true, use each level collection uses its own TimerManager | obj: 2 direct candidate(s), 1 address-taking reference(s); ref: 2 direct candidate(s), 1 address-taking reference(s). |
| `world.PhysicsObjectLoadHelper.TimeOut` | float (`ref`) | 15 | No supplied help. Name alone is insufficient to establish behavior. | obj: 3 direct candidate(s), 1 address-taking reference(s); ref: 1 direct candidate(s), 1 address-taking reference(s). |
| `world.ShouldDuplicateLevelByDefault` | bool (`var`) | false | if true, duplicate level by defalut | obj: 3 direct candidate(s), 1 address-taking reference(s). |

## Audio and media timing
| Exact CVar | Type / kind | Snapshot | Supplied help / conservative meaning | Build 1.1.4042190 scan candidates |
| --- | --- | --- | --- | --- |
| `sound.MuteClientSetting` | FString (`var`) | — | 0 means unmuted; 1 means muted. Each character in the string specifies the initial mute state of the corresponding client. (assistant translation; not independently reviewed) | obj: 3 direct candidate(s), 1 address-taking reference(s). |
| `timecode.UseDropFormatTimecodeByDefaultWhenSupported` | bool (`var`) | true | By default, should we generate a timecode in drop frame format when the frame rate does support it. | obj: 3 direct candidate(s), 1 address-taking reference(s). |

## Scope and limitations

- There are 54 unique names here. `Throttle.Enable.PinnedMotion` occurs more than once in the registry with two different help strings referring to PinnedMotion PinOther and V2 tasks; both descriptions are preserved in the table. Duplicate rows are counted once by exact name.
- `modeling`-adjacent/editor-like controls, RigVM, typed elements, VR/XR, and crash-report settings may belong to tooling or platform-specific paths. Their presence in a Shipping binary does not show they are active in ordinary matches.
- No row should be treated as an optimization recommendation. The source values are snapshots; ranges and documented semantics are only those stated in supplied help.
- Even `var`/`ref` registry classification plus static candidates does not prove that a startup `.ini` override is accepted by the game.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), [translated help notes](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
