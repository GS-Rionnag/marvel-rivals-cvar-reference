# Snapshot-only CVar candidates

These names have `name=value` rows in the community `CVarDump.txt` but no `var` or `ref` row in `console_vars.tsv`. The dump header calls the file re-importable, so values are preserved as a snapshot, not as defaults. A snapshot row is strong evidence that the community source treated the key as a setting, but its registration, type, build, and runtime effect are not confirmed by these attachments alone.

- Source: [CVar snapshot message](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); file preserved as [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Names: 67; also present in `console_objects.tsv`: 40; not found there: 27.
- Exact names present in the local dotted-string candidate index: 30; not present in that index: 37 (2 undotted and 35 dotted).
- Local game presence is an exact printable-string comparison, not runtime registration.

| Name | Snapshot value (not default) | `console_objects.tsv` flags | Object-table help | Exact Epic 5.9 entry | Local build string candidate |
|---|---|---|---|---|---|
| `102451.UseAverageNormal` | false | 0 | 102451 UseAverageNormal | — | no |
| `103711.ScopeRadius.UseFlyTime` | true | 0 | — | — | no |
| `104971.PinIgnoreSourceLandBeforeLaunched` | true | 0 | — | — | no |
| `1055.fix105542telelport` | true | 0 | 0: Disable, 1: Enable | — | no |
| `a.ForceUseAnimNotifyFilters` | false | — | — | — | no |
| `a.Streaming.ChunkSizeSeconds` | 4 | 0 | Size of streaming animation chunk in seconds, 0 or negative signifies only have 1 chunk | `4` — Size of streaming animation chunk in seconds, 0 or negative signifies only have 1 chunk | yes |
| `a.StripFramesOnCompression` | 0 | 0 | 1 = Strip every other frame on animations that have an even number of frames. 0 = off | `0` — 1 = Strip every other frame on animations that have an even number of frames. 0 = off | yes |
| `a.StripOddFramesWhenFrameStripping` | 0 | 0 | 1 = When frame stripping apply to animations with an odd number of frames too. 0 = only even framed animations | `0` — 1 = When frame stripping apply to animations with an odd number of frames too. 0 = only even framed animations | yes |
| `ability.101662.EnablePreSpawnAI` | true | — | — | — | no |
| `au.ThreadedSwapDebugExtraTime` | 0 | 0 | Simulate a slow device swap by adding addional time to the swap task | `0` — Simulate a slow device swap by adding addional time to the swap task | yes |
| `buildidoverride` | 0 | 0 | Sets build id used for matchmaking | — | no |
| `fx.Niagara.PruneEmittersOnCook` | 1 | 320 | If > 0 this platform will prune disabled emitters during cook. | `1` — If > 0 this platform will prune disabled emitters during cook. | yes |
| `fx.Niagara.QualityLevel` | 2 | 16777536 | The quality level for Niagara Effects. | `3` — The quality level for Niagara Effects. | yes |
| `fx.Niagara.QualityLevel.Max` | -1 | 4 | The Maximum quality level for Niagara Effects. | `-1` — The Maximum quality level for Niagara Effects. | yes |
| `fx.Niagara.QualityLevel.Min` | -1 | 4 | The minimum quality level for Niagara Effects. | `-1` — The minimum quality level for Niagara Effects. | yes |
| `fx.NiagaraAllowRuntimeScalabilityChanges` | 1 | 67109184 | If > 0 this platform allows niagara scalability settings changes at runtime. | `1` — If > 0 this platform allows niagara scalability settings changes at runtime. | yes |
| `GameplayCue.DisableBuffCueRecycle` | false | — | — | — | no |
| `GameplayCue.DisableTargetActorCueRecycle` | false | — | — | — | no |
| `GameplayCue.EnableCueActorCache` | false | — | — | — | no |
| `Marvel.Feedback.DiagnoseAllowEditor` | 0 | 0 | — | — | no |
| `Marvel.Feedback.DiagnoseForceOff` | 0 | 0 | — | — | no |
| `Marvel.Feedback.DiagnoseForceOn` | 0 | 0 | — | — | no |
| `Marvel.HeroAssetLoader.AbandonedIdleSeconds` | 0 | — | — | — | yes |
| `Marvel.HeroAssetLoader.AbilityPresentation.AcquireOrderLRU` | 1 | — | — | — | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.IdleSeconds` | 30 | — | — | — | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.MaintenanceInterval` | 1 | — | — | — | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.MaxIdleEntries` | 32 | — | — | — | no |
| `Marvel.HeroAssetLoader.AbilityPresentation.PreferLargeIdleEntries` | 0 | — | — | — | no |
| `Marvel.HeroAssetLoader.Bond.AcquireOrderLRU` | 0 | — | — | — | no |
| `Marvel.HeroAssetLoader.Bond.IdleSeconds` | 30 | — | — | — | no |
| `Marvel.HeroAssetLoader.Bond.MaintenanceInterval` | 1 | — | — | — | no |
| `Marvel.HeroAssetLoader.Bond.MaxIdleEntries` | 16 | — | — | — | no |
| `Marvel.HeroAssetLoader.Bond.PreferLargeIdleEntries` | 0 | — | — | — | no |
| `Marvel.HeroAssetLoader.Hero.AcquireOrderLRU` | 0 | — | — | — | no |
| `Marvel.HeroAssetLoader.Hero.IdleSeconds` | 30 | — | — | — | no |
| `Marvel.HeroAssetLoader.Hero.MaintenanceInterval` | 1 | — | — | — | no |
| `Marvel.HeroAssetLoader.Hero.MaxIdleEntries` | 16 | — | — | — | no |
| `Marvel.HeroAssetLoader.Hero.PreferLargeIdleEntries` | 0 | — | — | — | no |
| `Marvel.HeroAssetLoader.ProfileRequests` | false | — | — | — | no |
| `Marvel.HeroAssetManifest.RuntimeMode` | 0 | — | — | — | no |
| `Marvel.HeroAssetManifest.ShadowMaxSamples` | 8 | — | — | — | no |
| `mass.EnableMassCMCParallelUpdate` | false | — | — | — | no |
| `networkversionoverride` | 1 | 0 | Sets network version used for multiplayer | — | no |
| `pve.SkipZeroLevelReplicatedApply` | false | — | — | — | no |
| `r.BatchedElementUsePoolResource` | 1 | — | — | — | no |
| `r.Composure.CompositingElements.Editor.WarnWhenSceneCaptureIsMissingCamera` | true | 0 | By default, scene capture (CG) elements rely on a camera to position themselves. To catch when one isn't set up, the editor displays a warning image. Disable this CVar to allow the capture from the element's position & orientation. | — | yes |
| `r.DebugActionZone.ActionRatio` | 1 | 0 | The action zone ratio that will be returned by FDisplayMetrics::GetDisplayMetrics on platforms that don't have a defined safe zone (0..1)  default: 1.0 | `1` — The action zone ratio that will be returned by FDisplayMetrics::GetDisplayMetrics on platforms that don't have a defined safe zone (0..1)   default: 1.0 | yes |
| `r.DebugSafeZone.TitleRatio` | 1 | 0 | The safe zone ratio that will be returned by FDisplayMetrics::GetDisplayMetrics on platforms that don't have a defined safe zone (0..1)  default: 1.0 | `1` — The safe zone ratio that will be returned by FDisplayMetrics::GetDisplayMetrics on platforms that don't have a defined safe zone (0..1)   default: 1.0 | yes |
| `r.DumpingMovie` | 0 | 1 | Allows to dump each rendered frame to disk (slow fps, names MovieFrame..). <=0:off (default), <0:remains on, >0:remains on for n frames (n is the number specified) | `0` — Allows to dump each rendered frame to disk (slow fps, names MovieFrame..).  <=0:off (default), <0:remains on, >0:remains on for n frames (n is the number specified) | yes |
| `r.EnableStereoEmulation` | 0 | 4 | Emulate stereo rendering | `0` — Emulate stereo rendering | yes |
| `r.grass.DensityQualityLevel` | -1 | 320 | The quality level for grass (low, medium, high, epic). | `-1` — The quality level for grass (low, medium, high, epic). | yes |
| `r.Shadow.Virtual.Cache.AllocateViaLRU` | 0 | 32 | Prioritizes keeping more recently requested cached physical pages when allocating for new requests. | `0` — Prioritizes keeping more recently requested cached physical pages when allocating for new requests. | yes |
| `r.SkeletalMesh.MinLodQualityLevel` | -1 | 320 | The quality level for the Min stripping LOD. | `-1` — The quality level for the Min stripping LOD. | yes |
| `r.StaticMesh.MinLodQualityLevel` | -1 | 320 | The quality level for the Min stripping LOD. | `-1` — The quality level for the Min stripping LOD. | yes |
| `r.StaticMesh.SimplifyWithTargetPlatform` | -1 | 0 | 1 = Simplify static meshes based on target platform lod settings. 0 = off | — | yes |
| `r.StaticMesh.SimplifyWithWorldSetting` | -1 | 0 | 1 = Simplify static meshes based on world settings. 0 = off | — | yes |
| `r.Streaming.NoRefLODBiasQualityLevel` | -1 | 320 | The quality level for the no-ref mesh streaming LOD bias | `-1` — The quality level for the no-ref mesh streaming LOD bias | yes |
| `r.Streamline.Load.DeepDVC` | true | 36 | Determines whether feature DeepDVC is loaded. This can be useful to resolve conflicts where multiple SL features are incompatible with each other. | — | yes |
| `r.Streamline.Load.DLSSG` | true | 36 | Determines whether feature DLSS-FG is loaded. This can be useful to resolve conflicts where multiple SL features are incompatible with each other. | — | yes |
| `r.Streamline.Load.Reflex` | true | 36 | Determines whether feature Reflex is loaded. This can be useful to resolve conflicts where multiple SL features are incompatible with each other. | — | yes |
| `ShowFlag.SmartObjects` | 2 | 0 | Allows to override a specific showflag (works in editor and game, "show" only works in game and UI only in editor) Useful to run a build many time with the same showflags (when put in consolevariables.ini like "showflag.abc=0")  0: force the showflag to be OFF  1: force the showflag to be ON  2: do not override this showflag (default) | — | no |
| `Slate.bAllowNotifications` | true | 0 | If false, then notifications will not be displayed to the user. | `true` — If false, then notifications will not be displayed to the user. | yes |
| `Slate.bAllowThrottling` | 1 | 0 | Allow Slate to throttle parts of the engine to ensure the UI is responsive | `1` — Allow Slate to throttle parts of the engine to ensure the UI is responsive | yes |
| `Slate.DeferWindowsMessageProcessing` | 1 | 0 | Whether windows message processing is deferred until tick or if they are processed immediately | `1` — Whether windows message processing is deferred until tick or if they are processed immediately | yes |
| `sony.NumMissedMotionUpdatesToCombine` | 0 | 0 | How many missed motion updates to combine into the latest one when sending motion events from a PS controller. No more than 64 missed updates will be stored. | — | yes |
| `sony.UnifyMotionSpace` | 0 | 0 | If set to non-zero, acceleration and rotation rate will all be in the same coordinate space. 0 for legacy behaviour. 1 will match Unreal's coordinate space (left-handed, z-up, etc). 2 will be right-handed by swapping x and y. Non-zero also forces rotation rate units to be radians/s and acceleration units to be g. | — | yes |
| `System30104.CheckPhotoSourceSignature` | 1 | 0 | 1=     0= | — | no |