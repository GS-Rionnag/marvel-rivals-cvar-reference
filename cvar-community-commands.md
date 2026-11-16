# Console commands in the community registry

Commands are listed separately because they are not CVar settings and should not be treated as `name=value` overrides.

- Source: [original Discord message](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); preserved as [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Unique command names: 395.

| Command | Source rows | Help text(s) |
|---|---:|---|
| `a.AuditLoadedAnimGraphs` | 1 | Audit memory breakdown of currently loaded anim graphs. Writes results to the log. |
| `a.Sharing.Enabled` | 1 | Arguments: 0/1<br>Controls whether the animation sharing is enabled. |
| `AbilitySystem.Ability.Activate` | 1 | <TagName/ClassName/AssetName>. Activate a Gameplay Ability.<br>Substring name matching works for Activation Tags (on already granted abilities), Asset Paths (on non-granted abilities), or Class Names on both. |
| `AbilitySystem.Ability.Cancel` | 1 | <Name>. Cancels (prematurely Ends) a currently executing Gameplay Ability |
| `AbilitySystem.Ability.Grant` | 1 | Include a param [ClassName/AssetName] to Grant an Ability to the Player.  Omit parameters to lists all of the Gameplay Abilities currently granted to the Player. |
| `AbilitySystem.AbilityTask.Debug.PrintCounts` | 1 | Print out the current AbilityTask counts by class. 'AbilitySystem.AbilityTask.Debug.RecordingEnabled' must be turned on for this to function. |
| `AbilitySystem.DamageRpcOptimizationParams1` | 1 | AbilitySystem.DamageRpcOptimizationParams1 |
| `AbilitySystem.Debug.NextCategory` | 1 | Switches to the next ShowDebug AbilitySystem category |
| `AbilitySystem.Debug.SetCategory` | 1 | Sets the ShowDebug AbilitySystem category. Usage: AbilitySystem.Debug.SetCategory <CategoryName> |
| `AbilitySystem.DisplayDebug` | 1 | Display AbilitySystem Debug |
| `AbilitySystem.Effect.Apply` | 1 | <Class/AssetName> [Level]. Apply a Gameplay Effect on the Player.  Substring name matching works for Asset Tags, Asset Paths, or Class Names. |
| `AbilitySystem.Effect.ListActive` | 1 | Lists all of the Gameplay Effects currently active on the Player |
| `AbilitySystem.Effect.Remove` | 1 | <Handle/Name>. Remove a Gameplay Effect that is currently active on the Player |
| `AbilitySystem.EffectTemplate` | 1 | EffectTemplate Drawing |
| `AbilitySystem.GameplayCue.ClearIgnoredCueTags` | 1 | Clear global GIgnoredCueTags |
| `AbilitySystem.GameplayCue.DumpIgnoredCueTags` | 1 | Output GIgnoredCueTags |
| `AbilitySystem.HistogramMetric.Send` | 1 | AbilitySystem.HistogramMetric.SendAbilitySystem.HistogramMetric.Send |
| `AbilitySystem.Log` | 1 | Show AbilitySystem Logs |
| `AbilitySystem.MergeContainerSpec` | 1 | Register/Unregister ContainerSpecLock. Usage: AbilitySystem.MergeContainerSpec [0\|1] |
| `AbilitySystem.MergeDamageEffects` | 1 | — |
| `AbilitySystem.MergeDurationEffects` | 1 | — |
| `AbilitySystem.MergeProjectileActors` | 1 | Toggle projectile merging. Usage: AbilitySystem.MergeProjectileActors <0\|1> [ProjectileId] |
| `AbilitySystem.MergeProjectileEffectiveScope` | 1 | — |
| `AbilitySystem.MergeScopeActors` | 1 | Toggle scope merging. Usage: AbilitySystem.MergeScopeActors <0\|1> [ScopeId] |
| `AbilitySystem.MergeTreatEffects` | 1 | Merge compatible one-shot treatments. 0=off, 1=on; requires AbilitySystem.MergeGameplayEffects. |
| `AbilitySystem.OptimizeAttributeModifierRPCBatch` | 1 | — |
| `AbilitySystem.PeriodicDamageManagerCmd` | 1 | Toggle PeriodicDamageManager. Usage: 0=off, 1=on |
| `AbilitySystem.PrintLog` | 1 | Show AbilitySystem PrintLog |
| `ActiveChaosField` | 1 | Active Chaos FieldActiveChaosField field01, field02, field03 |
| `AssetManager.DumpAssetRegistryInfo` | 1 | Dumps extended info about asset registry to log |
| `AssetManager.DumpBundlesForAsset` | 1 | Shows a list of all bundles for the specified primary asset by primary asset id (i.e. Map:Entry) |
| `AssetManager.DumpLoadedAssets` | 1 | Shows a list of all loaded primary assets and bundles |
| `AssetManager.DumpReferencersForPackage` | 1 | Generates a graph viz and log file of all references to a specified package |
| `AssetManager.DumpTypeSummary` | 1 | Shows a summary of types known about by the asset manager |
| `AssetPool.CueActorExpiry.Enable` | 1 | — |
| `au.capture.start` | 1 | Start audio capture on all PIE clients. Usage: au.capture.start [tag] [categories] [duration_seconds] [output_path]<br>  categories: all \| events,rtpc,states,switches,banks (default: all)<br>  duration_seconds: auto-stop after N seconds, 0 = manual stop only (default: 0)<br>  output_path: relative to Saved/AudioCapture/ or absolute path for JSON file |
| `au.capture.stop` | 1 | Stop audio capture on all PIE clients, dump log and JSON report. Usage: au.capture.stop [output_path]<br>  output_path: relative to Saved/AudioCapture/ or absolute path for JSON file (overrides start-time path) |
| `au.Modulation.SetPitchRange` | 1 | Sets max final modulation range of pitch (in semitones). Default: 96 semitones (+/- 4 octaves) |
| `au.ReportAudioDevices` | 1 | This will log any active audio devices (instances of the audio engine) alive right now. |
| `au.SourceFadeMin` | 1 | Sets the length (in samples) of minimum fade when a sound source is stopped. Must be divisible by 4 (vectorization requirement). Ignored for some procedural source types. (Default: 512, Min: 4). |
| `au.spatialization.ListAvailableSpatialPlugins` | 1 | This will output a list of currently available/active spatialization plugins |
| `au.spatialization.SetCurrentSpatialPlugin` | 1 | Attempt to swap to the named spatialization plugin (au.spatialization.ListAvailableSpatialPlugins to see what is availible) |
| `au.streamcaching.FlushAudioCache` | 1 | This will flush any non retained audio from the cache when Stream Caching is enabled. |
| `au.streamcaching.ResizeAudioCacheTo` | 1 | This will try to cull enough audio chunks to shrink the audio stream cache to the new size if neccessary, and keep the cache at that size. |
| `au.streamcaching.StartProfiling` | 1 | This will start a performance-intensive profiling mode for this streaming manager. Profile stats can be output with audiomemreport. |
| `au.streamcaching.StopProfiling` | 1 | This will start a performance-intensive profiling mode for this streaming manager. Profile stats can be output with audiomemreport. |
| `AudioAmmoTrajectoryAudioOpt` | 1 | enable or disable ammo trajectory audio post optimization |
| `AudioAutoShowLogRecording` | 1 | start recording info |
| `AudioAutoUnregister` | 1 | Auto unregister emitter when no active events |
| `AudioDebugPanel` | 1 | Toggle show Debug Audio Panel |
| `AudioEnableDoppler` | 1 | Toggle set doppler effect enable or disable |
| `AudioEnableOccObs` | 1 | toggle enable occlusion and obstruction service |
| `AudioEnableSpatialListener` | 1 | enable current client spatial listener, this command will mute other client(because there can only be one spatial listener at the same time) |
| `AudioMakeUpLandAudio` | 1 | Toggle set makeup land audio enable or not |
| `AudioRoomReverbInterval` | 1 | enable or disable room/reverb update interval |
| `AudioShowEmitter` | 1 | Show audio emitter |
| `AudioShowEmitterName` | 1 | Toggle show name of each akcomponent |
| `AudioShowEventName` | 1 | Show Event Name |
| `AudioShowListener` | 1 | Draw a arrow from listener position |
| `AudioShowOccObs` | 1 | Debug Audio Occlusion Obstruction trace |
| `AudioShowRtpc` | 1 | Toggle show rtpc state of each akcomponent |
| `AudioShowSwitch` | 1 | Toggle show switch state of each akcomponent |
| `AudioShowThreatValue` | 1 | Show Threat Value |
| `AudioThread.TaskPriority` | 1 | Takes a single parameter of value `High`, `Normal`, `BackgroundHigh`, `BackgroundNormal` or `BackgroundLow`. |
| `AudioToggleAkReflect` | 1 | Toggle set marvel reflect enable or not |
| `bink.List` | 1 | Display all Bink Media Player objects and their current state |
| `c.ToggleGPUCrashedFlagDbg` | 1 | Forcibly toggles the 'GPU Crashed' flag for testing crash analytics. |
| `Cache.Pool.Print` | 1 | — |
| `char.skin_fx_visibility_mode` | 1 | 0/1/2: invisible to all / visible to all / visible to ViewTarget only |
| `clientmass.Remote.NpcGateStatus` | 1 | Logs the remote NPC gate per world: clientmass.Remote.NpcGate, tag lookups, refusals, attackers cached allowed / refused. |
| `CommonUI.DumpActivatableTree` | 1 | Outputs the current state of the activatable tree. 4 args: bIncludeActions, bIncludeChildren, bIncludeInactive, LocalPlayerId (optional, defaults to -1 or all) |
| `CommonUI.DumpInputConfig` | 1 | Outputs the current Input Config for each player |
| `Config.DumpSharedValueStats` | 1 | Print live shared config value storage and gross string savings. |
| `CPUTime.Dump` | 1 | Usage -Delay=[NumSeconds=30]<br>If Delay==0, disables printing the CPU usage to the log<br>If Delay>0, starts printing the average CPU usage from the last n frames, clamps between 10 and 300 |
| `CsvCategory` | 1 | Changes whether a CSV category is included in captures. |
| `CsvProfile` | 1 | Starts or stops Csv Profiles |
| `CustomTimeStep.reset` | 1 | Resets the current custom step. |
| `CVarDefaultPakFileRules_Packages` | 1 | PakFileMounted2 Packages |
| `DataRegistry.DumpCachedItems` | 1 | Shows a list of every item available cached for the specified registry type. Add All as second parameter to also print value as text |
| `DataRegistry.DumpTypeSummary` | 1 | Shows a summary of types known about by the Data Registry system |
| `DefaultPakFileRules_ReloadMissing` | 1 | DefaultPakFileRules_ReloadMissing |
| `Demo.ActorPrioritizationEnabled` | 1 | Set whether or not actor prioritization is enabled on demo driver of the current world. |
| `demo.ChangeLevelCollection` | 1 | 如果大于0，显示死亡回放世界的场景；反之，显示主世界的场景 |
| `Demo.CheckpointSaveMaxMSPerFrame` | 1 | Set max checkpoint record time in MS on demo driver of the current world. |
| `demo.DebugCameraAccuracy` | 1 | — |
| `demo.DrawCheckpointEvents` | 1 | — |
| `demo.GotoInstantReplay` | 1 | jump to a particular time (arg0: rewind time, arg1: spectator uid). |
| `demo.HologramReplay.ToggleDynamicsVisible` | 1 | Toggle DynamicDuplicatedLevels collection visible. arg0: 0=hide, 1=show (default toggle). arg1: LCIndex (optional, V2 per-session) |
| `demo.HologramReplay.ToggleSourceVisible` | 1 | Toggle source hologram levels visible. arg0: 0=hide, 1=show (default toggle) |
| `Demo.MaxDesiredRecordTimeMS` | 1 | Set max desired record time in MS on demo driver of the current world. |
| `Demo.SetLocalViewerOverride` | 1 | Set first local player controller as the viewer override on demo driver of the current world. |
| `demo.StopInstantReplay` | 1 | stop instant replay. |
| `DumpLevelCollections` | 1 | Dump level collections in the current world. |
| `DumpNiagaraWorldManager` | 1 | Dump Information About the Niagara World Manager Contents |
| `DumpVisibleActors` | 1 | Dump visible actors in current world. |
| `EnhancedInput.DumpKeyProfileToLog` | 1 | — |
| `EnhancedInput.SaveKeyProfilesToSlot` | 1 | Save the user input settings object with the Save Game to slot system |
| `FlushAsyncLoading` | 1 | — |
| `FlushAsyncLoadingInQueue` | 1 | — |
| `FName.Dump` | 1 | Dump all base FName strings to a file. Pass -num=n to dump the most recent n names. |
| `FName.DumpNumbered` | 1 | Dump all numbered FNames to a file (only when UE_FNAME_OUTLINE_NUMBER is set). Pass -num=n to dump the most recent n names. |
| `FName.HashCsv` | 1 | Write FName hash stats to a csv file. |
| `FName.List` | 1 | List all base FName strings to the output device. Pass -num=n to list the most recent n names. |
| `FName.ListNumbered` | 1 | List all numbered FNames to the output devicce (only when UE_FNAME_OUTLINE_NUMBER is set). Pass -num=n to list the most recent n names. |
| `FName.Stats` | 1 | Write FName stats to the output device. |
| `foliage.Freeze` | 1 | Useful for debugging. Freezes the foliage culling and LOD. |
| `foliage.LogFoliageFrame` | 1 | Useful for debugging. Logs all foliage rendered in a frame. |
| `foliage.RebuildFoliageTrees` | 1 | Rebuild the trees for non-grass foliage. |
| `foliage.Test` | 1 | Useful for debugging. |
| `foliage.ToggleVectorCull` | 1 | Useful for debugging. Toggles the optimized cull. |
| `foliage.UnFreeze` | 1 | Useful for debugging. Freezes the foliage culling and LOD. |
| `ForceBuildStreamingData` | 1 | Forces streaming data to be rebuilt for the current world. |
| `FuncTests_InputRecord` | 1 | get all player controller to input record (arg : init, start, stop, save, load, play)Args[0] : init, start, stop, save, load, play; Args[1] : recordname; Args[2] : recordpath |
| `FuncTests_SlateInputRecord` | 1 | slate input record (arg : init, start, stop, save, load, play)Args[0] : init, start, stop, save, load, play; Args[1] : recordname; Args[2] : recordpath |
| `FX.AutoTrajectory.FlushCache` | 1 | — |
| `FX.DumpNCPoolInfo` | 1 | Dump Niagara System Pooling Info |
| `fx.DumpPSCPoolInfo` | 1 | Dump Particle System Pooling Info |
| `fx.DumpPSCTickStateInfo` | 1 | Dumps state information for all current Particle System Components. |
| `fx.Niagara.DataChannels.ResetLayoutInfo` | 1 | Resets all data channel layout info used by data interfaces to access data channels. |
| `fx.Niagara.Debug.PlaybackMode` | 1 | Set playback mode<br>0 - Play<br>1 - Paused<br>2 - Step |
| `fx.Niagara.Debug.PlaybackRate` | 1 | Set playback rate |
| `fx.Niagara.DumpComponents` | 1 | Dump Information about all Niagara Components |
| `fx.Niagara.RenderTarget.OverrideFormat` | 1 | Optional global format override for all Niagara render targets |
| `fx.Niagara.Scalability.CullingMode` | 1 | Set scalability culling mode<br>0 - Enabled. Culling is enabled as normal.<br>1 - Paused. No culling will occur but FX will still be tracked internally so culling can be resumed correctly later.<br>2 - Disabled. No culling will occur and no FX will be tracked. Culling may not work correctly for some FX if enabled again after this. |
| `fx.Niagara.SetOverridePlatformName` | 1 | Sets which platform we should override with, no args means reset to default |
| `fx.Niagara.SetOverrideQualityLevel` | 1 | Sets which quality level we should override with, no args means clear the override and return to non overriden quality level). Valid levels are 0-4 (Low-Cinematic) |
| `fx.Niagara.SetOverrideQualityLevelToMin` | 1 | Overrides Niagara quality with Low (0) on Windows or Lowest (5) on other platforms if in the platform Min/Max range, otherwise Min (0 if unset). Clear with fx.Niagara.SetOverrideQualityLevel without arguments. |
| `fx.Niagara.TaskPriorities.Dump` | 1 | Dump currently set priorities |
| `fx.Niagara.TaskPriorities.RunTest` | 1 | Run a test set of priorites |
| `fx.ParticlePerfStats.RunTest` | 1 | Runs for a number of frames then logs out the results.<br>Arg0 = NumFrames.<br>Arg1 = Gather World Stats (default 0).<br>Arg2 = Gather System Stats (default 1).<br>Arg3 = Gather Component Stats (default 0). |
| `fx.PSCMan.Dump` | 1 | Dumps state information for all current Particle System Managers. |
| `FX.RestartAll` | 1 | Restarts all particle system components |
| `GameplayCue.BuildGameplayCueTranslator` | 1 | Displays GameplayCue notify map |
| `GameplayCue.FilterCuesByTag` | 1 | Adds or removes a GameplayCue tag to the debug filter list. If the filter is populated, only GameplayCues with tags in the filter will be invoked. |
| `GameplayCue.PrintGameplayCueNotifyMap` | 1 | Displays GameplayCue notify map |
| `GameplayCue.PrintGameplayCueTranslator` | 1 | Displays GameplayCue notify map |
| `GameplayCue.PrintLoadedGameplayCueNotifyClasses` | 1 | Displays GameplayCue Notify classes that are loaded |
| `GameplayMediaEncoder.Initialize` | 1 | Constructs the audio/video encoding objects. Does not start encoding |
| `GameplayMediaEncoder.Shutdown` | 1 | Releases all systems. |
| `GameplayMediaEncoder.Start` | 1 | Starts encoding |
| `GameplayMediaEncoder.Stop` | 1 | Stops encoding |
| `gc.DebugGraphHide` | 1 | Hide GC debug graph. |
| `gc.DebugGraphShow` | 1 | Show GC debug graph. (See also: DebugGraphSafeDurationThresholdMs) |
| `gc.GenerateReachabilityStressData` | 1 | Allocate deeply-nested UObject tree to stress test reachability analysis. |
| `gc.UnlinkReachabilityStressData` | 1 | Unlink previously-generated reachability analysis stress test data for collection in the next cycle. |
| `GE.SyncStats.Export` | 1 | Export GameplayEffect sync statistics to CSV. Usage: GE.SyncStats.Export [optional_path] |
| `GE.SyncStats.Print` | 1 | Print GameplayEffect sync statistics report |
| `GE.SyncStats.Reset` | 1 | Reset GameplayEffect sync statistics |
| `GE.SyncStats.Snapshot` | 1 | Create a statistics snapshot |
| `geometry.DynamicMesh.ClearDebugMeshes` | 1 | Discard all debug meshes currently stored in the FDynamicMesh3 Global Debug Mesh set. This command only works in the Editor. |
| `grass.DumpExclusionBoxes` | 1 | Print the exclusion boxes, debugging. |
| `grass.DumpGrassData` | 1 | — |
| `grass.FlushCache` | 1 | Flush the grass cache, debugging. |
| `grass.FlushCachePIE` | 1 | Flush the grass cache, debugging. |
| `Hero.AssetDumpLoaded` | 1 | Dump currently loaded asset-pack assets for a hero+skin to a CSV file. Usage: Hero.AssetDumpLoaded hero=<HeroID> skin=<SkinID> |
| `HeroAccessory.SpawnHomingFX` | 1 | Spawn configured accessory FX and home them to accessory SK sockets. Usage: HeroAccessory.SpawnHomingFX <X> <Y> <Z> [VX VY VZ] [ConfigIndex] [AccessoryActorNameFilter] |
| `HighlightRecorder.Pause` | 1 | Pauses recording of highlight clip |
| `HighlightRecorder.Resume` | 1 | Resumes recording of highlight clip |
| `HighlightRecorder.Save` | 1 | Saves highlight clip, optional parameters: filename ("test.mp4" by default) and max duration (float, secs, duration of ring buffer by default) |
| `HighlightRecorder.Start` | 1 | Starts recording of highlight clip, optional parameter: max duration (float, 30 seconds by default) |
| `HighlightRecorder.Stop` | 1 | Stops recording of highlight clip |
| `HighlightRecorderX.Pause` | 1 | Pauses recording of highlight clip |
| `HighlightRecorderX.Resume` | 1 | Resumes recording of highlight clip |
| `HighlightRecorderX.Save` | 1 | Saves highlight clip, optional parameters: filename ("test.mp4" by default) and max duration (float, secs, duration of ring buffer by default) |
| `HighlightRecorderX.Start` | 1 | Starts recording of highlight clip, optional parameter: max duration (float, 30 seconds by default) |
| `HighlightRecorderX.Stop` | 1 | Stops recording of highlight clip |
| `HitStat.Clear` | 1 | Clear HitStat cache |
| `Jarvis.Demo.Disable` | 1 | Disable JarvisDemo |
| `Jarvis.Demo.Enable` | 1 | Enable JarvisDemo |
| `Jarvis.Demo.IsEnabled` | 1 | Is JarvisDemo Enabled |
| `Level.DisableFoliageWind` | 1 | Modify parameter b to 0 for all material instances with base material A |
| `ListAllCullDistanceVolumes` | 1 | List informations of all CullDistanceVolumes in console. |
| `ListShaderLibraries` | 1 | Spits out a csv table containing stats of all shader libraries |
| `ListTimers` | 1 | — |
| `LiveLink.Log.DisableMessage` | 1 | Disable a LiveLink Message ID.Use: "LiveLink.Log.DisableMessage MessageID" |
| `LiveLink.Log.EnableMessage` | 1 | Enable a LiveLink Message ID that was previously disabled.Use: "LiveLink.Log.EnableMessage MessageID" |
| `LiveLink.Log.LogRepeated` | 1 | Log all messages event if they are not log for the first time.To log: "LiveLink.Log.LogRepeated"To set: "LiveLink.Log.LogRepeated TRUE\|FALSE" |
| `LiveLink.Log.SilentMode` | 1 | Silent all log from LiveLink.To silent: "LiveLink.Log.SilentMode"To set: "LiveLink.Log.SilentMode TRUE\|FALSE" |
| `LiveLink.Preset.Add` | 1 | Add a LiveLinkPreset. Use: LiveLink.Preset.Add Preset=/Game/Folder/MyLiveLinkPreset.MyLiveLinkPreset |
| `LiveLink.Preset.Apply` | 1 | Apply a LiveLinkPreset. Use: LiveLink.Preset.Apply Preset=/Game/Folder/MyLiveLinkPreset.MyLiveLinkPreset |
| `LoadPkg.DumpProcessing` | 1 | Dump processing packages info being tracked |
| `LoadPkg.DumpTracking` | 1 | — |
| `LoadTimes.DumpTracking` | 1 | Dump high level load times being tracked |
| `LoadTimes.DumpTrackingLow` | 1 | Dump low level load times being tracked |
| `LoadTimes.ResetTracking` | 1 | Reset load time tracking |
| `LoadTimes.StartAccumulating` | 1 | Starts capturing fine-grained accumulated load time data |
| `LoadTimes.StopAccumulating` | 1 | Stops capturing fine-grained accumulated load time data and dump the results |
| `LogCountedInstances` | 1 | Dumps count of all tracked FInstanceCountingObject's |
| `ls.PrintNumLandscapeShadows` | 1 | Prints the number of landscape components that cast shadows. |
| `mallocleak.clear` | 1 | Clears recorded allocation info |
| `mallocleak.report` | 1 | Writes malloc leak reports |
| `mallocleak.start` | 1 | Starts tracking allocations. Args -report=[secs] -size=[filter] |
| `mallocleak.stop` | 1 | Stops tracking allocations |
| `marvel.AOIRelevantCache.Benchmark` | 1 | Benchmark GetRelevantCharacters: old traversal vs cached lookup.<br>Usage: marvel.AOIRelevantCache.Benchmark [iterations] (default 10000) |
| `marvel.audio.FinalEventNameCacheStats` | 1 | Print the resolved event name cache stats (hits/misses/entries) of every audio world subsystem. |
| `marvel.AudioMemory` | 1 | Dumps Wwise audio memory snapshot (env/global/categories/banks/crossref). |
| `marvel.Bink.DumpAudioStats` | 1 | Dumps cumulative Bink/Wwise bridge underflow, overflow, and buffer occupancy statistics. |
| `marvel.Bink.ResetAudioStats` | 1 | Resets cumulative Bink/Wwise bridge audio statistics without clearing queued PCM. |
| `Marvel.ProjectileRoute.SetOverride` | 1 | Set one BattleRule projectile route. Usage: <AbilityID\|ProjectileID\|all> <0\|1>. Exact ProjectileID takes precedence over AbilityID; all sets the default state and clears individual states. This command does not change the master gate. |
| `MarvelGameData.DamageRpcOptimizationParams` | 1 | MarvelGameData.DamageRpcOptimizationParams |
| `MarvelGlobals.DumpHeroAssetPack` | 1 | Dump hero asset pack |
| `MarvelGlobals.ReloadGameData` | 1 | Reload game data |
| `MarvelStats.SendSnapshotTraceToServer` | 1 | [ServerIP]，for example, 127.0.0.1, or other remote ip addresses. |
| `MarvelStats.SnapshotTrace` | 1 | — |
| `MarvelStats.StartOnlineHitchCollecting` | 1 | 0/1: Stop/Start |
| `MarvelZombie.Occlusion` | 1 | — |
| `mass.MonsterMove.DS.Dump` | 1 | Print requested DS movement CVars and the last accepted per-world configuration and counters. |
| `MediaEncoderX.Initialize` | 1 | Constructs the audio/video encoding objects. Does not start encoding |
| `MediaEncoderX.Shutdown` | 1 | Releases all systems. |
| `MediaEncoderX.Start` | 1 | Starts encoding |
| `MediaEncoderX.Stop` | 1 | Stops encoding |
| `MediaIO.HideInputTimecode` | 1 | All media player will stop logging the frame timecode when a new frame is captured. |
| `MediaIO.ShowInputTimecode` | 1 | All media player will log the frame timecode when a new frame is captured. |
| `MemoryTest.CaptureTopImage` | 1 | Capture an image of current level |
| `MeshDiff.StartCapture` | 1 | Start capturing mesh diff data to CSV. Usage: MeshDiff.StartCapture [SamplingInterval] |
| `MeshDiff.StopCapture` | 1 | End capturing mesh diff data and close CSV files |
| `MessageBus.UDP.ClearDenyList` | 1 | Clear the UDP socket deny list. |
| `MonsterCharacter.Occlusion` | 1 | — |
| `net.ActorReport` | 1 | — |
| `Net.AsyncRep.RepBodyOffGT.Debug` | 1 | 无参数或 1 开启 RepBodyOffGT 诊断日志，0 关闭；不修改复制行为开关。 |
| `Net.CharMove.Sync.Debug` | 1 | 0/1。1 打开 MoveSync 相关调试指令，0 关闭。只修改已有调试 CVar，不改变 Enable、ForceNetUpdateInterval、AllowAOIWithUIDKey、AOI 等行为开关。 |
| `Net.CreateBandwidthGenerator` | 1 | — |
| `net.DeleteDormantActor` | 1 | Lists open actor channels |
| `net.DisconnectSimulatedConnections` | 1 | Disconnects some simulated connections (0 = all) |
| `net.EnableSharedRepECS` | 1 | Enable/disable SharedRep ECS mode. 0=disabled (use traditional per-channel storage), 1=enabled (use global ECS storage) |
| `net.ForceOnePacketPerBunch` | 1 | When set to true it will enable AutoFlush on all connections and force a packet to be sent for every bunch we create. This forces one packet per replicated actor and can help find rare ordering bugs |
| `Net.GenerateConstantBandwidth` | 1 | Deliver a constant throughput every tick to generate the specified Kilobytes per sec.<br>Usage:<br>Net.GenerateBandwidth KilobytesPerSecond |
| `Net.GeneratePeriodicBandwidthSpike` | 1 | Generates a spike of bandwidth every X milliseconds.<br>Usage:<br>Net.GeneratePeriodicBandwidthSpike SpikeInKb PeriodInMS |
| `net.ListActorChannels` | 1 | Lists open actor channels |
| `net.ListNetGUIDExports` | 1 | Lists open actor channels |
| `net.ListNetGUIDs` | 1 | Lists NetGUIDs for actors |
| `net.Marvel.RPCRateLimit.Reload` | 1 | Reload [Marvel.RPCRateLimit] ini section and atomically swap the rate-limit config snapshot. |
| `Net.MarvelRepGraph.SetAOI` | 1 | — |
| `Net.MarvelRepGraph.SetNetSpeed` | 1 | — |
| `Net.RepGraph.ActorDiscoveryBudget` | 1 | Set a separate network traffic budget for data sent when opening a new actor channel. Value in kilobytes per second |
| `Net.RepGraph.Debug.Start` | 1 | — |
| `Net.RepGraph.DrawGraph` | 1 | — |
| `Net.RepGraph.DyanmicSpatialization.Reinit` | 1 | — |
| `Net.RepGraph.Lists.Stats` | 1 | — |
| `Net.RepGraph.PrintActorChannelCounters` | 1 | — |
| `Net.RepGraph.PrintAll` | 1 | — |
| `Net.RepGraph.PrintAllActorInfo` | 1 | — |
| `Net.RepGraph.PrintCullDistances` | 1 | Print the cull distances of RepGraph actors on the server. |
| `Net.RepGraph.PrintCullDistancesForConnection` | 1 | Print the cull distances via the ReplicationDebugActor to add the connection cull distances. |
| `Net.RepGraph.PrintGraph` | 1 | — |
| `Net.RepGraph.PrioritizedLists.Draw` | 1 | — |
| `Net.RepGraph.PrioritizedLists.Print` | 1 | — |
| `Net.RepGraph.SetClassCullDistance` | 1 | — |
| `Net.RepGraph.SetDebugActor` | 1 | Set DebugActorConnectionPair on server, from client. Specify |
| `Net.RepGraph.SetPeriodFrame` | 1 | — |
| `Net.RepGraph.Spatial.CellInfo` | 1 | — |
| `Net.RepGraph.StarvedList` | 1 | — |
| `Net.SharedRep.Check` | 1 | — |
| `Net.SharedRep.Log.ChannelIndex` | 1 | — |
| `Net.SharedRep.Log.NetGuid` | 1 | — |
| `Net.SharedRep.Tool` | 1 | — |
| `net.SharedRepECS.Reset` | 1 | Reset all SharedRep ECS storage (clears all entities and indices) |
| `net.SharedRepECS.Stats` | 1 | Display statistics about SharedRep ECS storage usage |
| `net.SimulateConnections` | 1 | Starts a Simulated Net Driver |
| `NiagaraReportSystemMemory` | 1 | Dumps some rough information about system memory breakdown |
| `osc.client.connect` | 1 | Connects (or reconnects) the osc mix client with the provided name<br>(see "osc.clients" for a list of available clients and their respective ids). Args:<br>Name - Object name of client to (re)connect<br>Address - IP Address to (re)connect to (default: LocalHost)<br>Port - Port to (re)connect to (default: 8094) |
| `osc.client.connectById` | 1 | Connects (or reconnects) the osc mix client with the provided object id<br>(see "osc.clients" for a list of available clients and their respective ids). Args:<br>Id - Object Id of client to (re)connect<br>Address - IP Address to (re)connect to (default: LocalHost)<br>Port - Port to (re)connect to (default: 8094) |
| `osc.clients` | 1 | Prints diagnostic information pertaining to the currently initialized OSC client objects to the output log. |
| `osc.server.connect` | 1 | Connects or reconnects the osc mix server with the provided name<br>(see "osc.servers" for a list of available servers and their respective names). Args:<br>Name - Object name of server to (re)connect<br>Address - IP Address to connect to (default: LocalHost)<br>Port - Port to connect to (default: 8095) |
| `osc.server.connectById` | 1 | Connects or reconnects the osc mix server with the provided object id<br>(see "osc.servers" for a list of available servers and their respective ids). Args:<br>Id - Object Id of client to (re)connect<br>Address - IP Address to (re)connect to (default: LocalHost)<br>Port - Port to (re)connect to (default: 8095) |
| `osc.servers` | 1 | Prints diagnostic information pertaining to the currently initialized OSC servers objects to the output log. |
| `p.chaos.dumphierarcystats` | 1 | Outputs current collision hierarchy stats to the output log |
| `p.Vehicle.NextDebugPage` | 1 | Display the next page of vehicle debug data. |
| `p.Vehicle.PrevDebugPage` | 1 | Display the previous page of vehicle debug data. |
| `pak.DumpBlocks` | 1 | Debug command to spew the outstanding blocks. |
| `pak.WaitPrecache` | 1 | Debug command to wait on the pak precache. |
| `Python.ResetTraceFunc` | 1 | — |
| `Python.StartProfile` | 1 | Send python profile to stats system |
| `Python.StopProfile` | 1 | Stop python profile |
| `r.AOListMemory` | 1 | — |
| `r.AOListMeshDistanceFields` | 1 | — |
| `r.Composure.CompositingElements.Debug.LogSharedTargetsCount` | 1 | Dumps the count of all target currently allocated for the shared target compositing target pool. |
| `r.ComputeFramework.RebuildComputeGraphs` | 1 | Force all loaded UComputeGraph objects to rebuild. |
| `r.CopyLockedViews` | 1 | Copies all locked views in to a string that r.LockView will accept to reload them. |
| `r.d3d11.dumpliveobjects` | 1 | When using -d3ddebug will dump a list of live d3d objects.  Mostly for finding leaks. |
| `r.debug.ClearPendingPrecompileTask` | 1 | Clear pending Precompile Task |
| `r.debug.DumpNewPSOMaterial` | 1 | Dump all tracked NewPSO->Material mappings to a CSV file in Saved directory |
| `r.debug.DumpPSORecord` | 1 | Dump PSO Record |
| `r.debug.DumpSkelotPool` | 1 | Dump Skelot Pool |
| `r.debug.LoadPSOByFilter` | 1 | load pso by filter |
| `r.debug.PausePSOCompile` | 1 | Pause PSO Compile |
| `r.debug.PrintPSOConfigInfo` | 1 | print PSO Config to log |
| `r.debug.ReleasePSO` | 1 | Release PSO |
| `r.debug.ResumePSOCompile` | 1 | Resume PSO Compile |
| `r.debug.SavePSOConfigInfo` | 1 | Save PSO Config |
| `r.debug.SetBatchTime` | 1 | runtime Set Batch Time |
| `r.DumpBufferPoolMemory` | 1 | Dump allocation information for the buffer pool. |
| `r.DumpPipelineCache` | 1 | Dump current cache stats. |
| `r.DumpRenderTargetPoolMemory` | 1 | Dump allocation information for the render target pool. |
| `r.DumpShaderFrozenContentCache` | 1 | Dumps information about all evicted shader map frozen content entries. |
| `r.FlushMaterialUniforms` | 1 | — |
| `r.ListSceneColorMaterials` | 1 | Lists all materials that read from scene color. |
| `r.OpenGL.PrintProgramStats` | 1 | Print to log current program binary stats |
| `r.pso.ResetPSORuntimeMask` | 1 | Reset PSO RuntimeMask |
| `r.pso.SetPSORuntimeMask` | 1 | Set PSO Runtime Mask |
| `r.RecompileRenderer` | 1 | Recompiles the renderer module on the fly. |
| `r.RHISetGPUCaptureOptions` | 1 | Utility function to change multiple CVARs useful when profiling or debugging GPU rendering. Setting to 1 or 0 will guarantee all options are in the appropriate state.<br>r.rhithread.enable, r.rhicmdbypass, r.showmaterialdrawevents, toggledrawevents<br>Platform RHI's may implement more feature toggles. |
| `r.RHIThread.Enable` | 1 | Enables/disabled the RHI Thread and determine if the RHI work runs on a dedicated thread or not. |
| `r.SetFramePace` | 1 | Set a target frame rate for the frame pacer.To set 30fps: "r.SetFramePace 30" |
| `r.SetNearClipPlane` | 1 | Set the near clipping plane (in cm) |
| `r.ShaderPipelineCache.Close` | 1 | Close the current pipeline file cache. |
| `r.ShaderPipelineCache.DumpPSOHashMap` | 1 | dumo pso hash map to log |
| `r.ShaderPipelineCache.DumpPSOTypeCount` | 1 | dumo pso type count to log |
| `r.ShaderPipelineCache.DumpShaderHashMap` | 1 | dumo shader hash map to log |
| `r.ShaderPipelineCache.Open` | 1 | Close and reopen the user cache. |
| `r.ShaderPipelineCache.Save` | 1 | Save the current pipeline file cache. |
| `r.ShaderPipelineCache.SetBatchMode` | 1 | Sets the compilation batch mode, which should be one of:<br>	Pause: Suspend precompilation.<br>	Background: Low priority precompilation.<br>	Fast: High priority precompilation. |
| `r.SkylightRecapture` | 1 | Updates all stationary and movable skylights, useful for debugging the capture pipeline |
| `r.TogglePreCulledIndexBuffers` | 1 | Toggles use of preculled index buffers from the command 'PreCullIndexBuffers' |
| `r.UITextureResidency.DumpThreadDiagnostics` | 1 | Print bounded residency compatibility counters; valid worker calls are not errors. |
| `r.VT.FlushAndEvictFileCache` | 1 | Flush both the virtual texture physcial page cache and disk file cache |
| `r.VT.ShowDecodeErrors` | 1 | Highlight virtual textures with decode errors in hot pink. |
| `ReloadGlobalShaders` | 1 | Reloads the global shaders file |
| `RepBodyOffGT.DumpStaleActors` | 1 | [Marvel-RepBodyOffGT] Dump destroyed actors lingering in replication containers (OFFGTSTALE lines) for R1 comparative forensics. Diagnostic only; avoid spamming on production frames. |
| `RepBodyOffGT.KickClient` | 1 | [Marvel-RepBodyOffGT] Close the first client connection on GT to deterministically trigger logout teardown (Mass SynchronizeClients -> RemoveClient -> DestroyActor bubble info off-GT) for M1/R1 repro. |
| `Replay.NetworkTool.Stat` | 1 | — |
| `ReplicationGraph.Reload` | 1 | — |
| `rhi.DumpWorldsWithRendererInfos` | 1 | Dumps all worlds with renderer infos |
| `sc.DumpSceneComponentUpdateStats` | 1 | — |
| `sc.ResetSceneComponentUpdateStats` | 1 | — |
| `SetGlobalShaderCacheOverrideDirectory` | 1 | Set the directory to read the override global shader map file from. |
| `SetThreadConfig` | 1 | Sets a thread Priority and/or Affinity. A single arg of default resets all the thread Priorities and Affinities, otherwise [GT\|RT\|RHI\|Task\|TaskBP] both/either [TPri_type] [0x] sets the Priority and/or Affinity. |
| `ShowMontageName` | 1 | Show Montage Name |
| `ShrinkUObjectHashTables` | 1 | Shrinks all of the UObject hash tables. |
| `Slate.StopUIAutoTest` | 1 | Stop UI Auto Test |
| `slate.UserWidgetMemory` | 1 | Dumps all user widget memory infos. |
| `SparseDelegateReport` | 1 | Outputs a report of what sparse delegates are bound. SparseDelegateReport [name=<ObjectName>] [delegate=<DelegateName>] [class=<ClassName>] -details |
| `stats.NamedEvents` | 1 | <on/off> Enables or disables the Named Events. |
| `stats.VerboseNamedEvents` | 1 | <on/off> Enables or disables the Verbose Named Events. |
| `StuckDetect.ForceOn` | 1 | Force StuckDetector open/closed |
| `Swift.Log.All` | 1 | Print Swift Projectile Spec Info |
| `SynthBenchmark` | 1 | Run simple benchmark to get some metrics to find reasonable game settings automatically<br>Optional (float) parameter allows to scale with work amount to trade time or precision (default: 10). |
| `TaskGraph.ABTestThreads` | 1 | Takes two 0/1 arguments. Equivalent to setting TaskGraph.UseHiPriThreads and TaskGraph.UseBackgroundThreads, respectively. Packages as one command for use with the abtest command. |
| `TaskGraph.NumWorkerThreadsToIgnore` | 1 | Used to tune the number of task threads. Generally once you have found the right value, PlatformMisc::NumberOfWorkerThreadsToSpawn() should be hardcoded. |
| `TaskGraph.TaskThreadPriority` | 1 | Sets the priority of the task threads. Argument is one of belownormal, normal or abovenormal. |
| `TestStake.FlushHitPoints` | 1 | — |
| `TestStake.ToggleHitPoint` | 1 | — |
| `Throttle.SetConfig` | 1 | Throttle.SetConfig <Channel> <Tier1> <Tier2> <Tier3> |
| `Throttle.Status` | 1 | Throttle.Status - Print active count and interval for all channels |
| `tick.AddIndirectTestTickFunctions` | 1 | Add no-op ticks to test performance of ticking infrastructure. |
| `tick.AddTestTickFunctions` | 1 | Add no-op ticks to test performance of ticking infrastructure. |
| `tick.RemoveTestTickFunctions` | 1 | Remove no-op ticks to test performance of ticking infrastructure. |
| `TimecodeProvider.reset` | 1 | Resets the current timecode provider. |
| `ToggleAnonymousMode` | 1 | 开关匿名模式 |
| `ToggleEnableCullDistanceVolume` | 1 | Toggle whether all CullDistanceVolume is enabled. |
| `ToggleForceDefaultMaterial` | 1 | Render all meshes with the default material. |
| `ToggleLight` | 1 | Toggles all lights whose name contains the specified string |
| `ToggleReversedIndexBuffers` | 1 | Render static meshes with negative transform determinants using a reversed index buffer. |
| `ToggleShadowIndexBuffers` | 1 | Render static meshes with an optimized shadow index buffer that minimizes unique vertices. |
| `ToggleSocialFeatureRestriction` | 1 | 开关社交功能限制 |
| `Trace.Bookmark` | 1 | [Name] - Emits a TRACE_BOOKMARK() event with the given string name. |
| `Trace.Disable` | 1 | [ChannelSet] - Disables a set of channels. ChannelSet is comma-separated list of trace channels/presets to be disabled. If no channel is specified, it disables all channels. |
| `Trace.Enable` | 1 | [ChannelSet] - Enables a set of channels. ChannelSet is comma-separated list of trace channels/presets to be enabled. |
| `Trace.File` | 1 | [Path] [ChannelSet] - Starts tracing to a file. ChannelSet is comma-separated list of trace channels/presets to be enabled. Either Path or ChannelSet can be excluded. |
| `Trace.Pause` | 1 | Pauses all trace channels currently sending events. |
| `Trace.Resume` | 1 | Resumes tracing that was previously paused (re-enables the paused channels). |
| `Trace.Screenshot` | 1 | [Name] [ShowUI] Takes a screenshot and saves it in the trace. Ex: Trace.Screenshot ScreenshotName true |
| `Trace.Send` | 1 | <Host> [ChannelSet] - Starts tracing to a trace store. <Host> is the IP address or hostname of the trace store. ChannelSet is comma-separated list of trace channels/presets to be enabled. |
| `Trace.SnapshotFile` | 1 | [Path] - Writes a snapshot of the current in-memory trace buffer to a file. |
| `Trace.SnapshotSend` | 1 | <Host> <Port> - Sends a snapshot of the current in-memory trace buffer to a server. If no host is specified 'localhost' is used. |
| `Trace.Start` | 1 | [ChannelSet] - (Deprecated: Use Trace.File instead.) Starts tracing to a file. ChannelSet is comma-separated list of trace channels/presets to be enabled. |
| `Trace.Status` | 1 | Prints Trace status to console. |
| `Trace.Stop` | 1 | Stops tracing profiling events. |
| `UI.DebugProfileWidget` | 1 | UI.DebugProfileWidget idx |
| `UI.WidgetPresentationPool.Dump` | 1 | Dump requests, resident slots and RT identities without creating a pool. |
| `UMG.DebugPrintPreAnimatedStorage` | 1 | Print the PreAnimatedStorage info. |
| `UpdateCullDistanceVolume` | 1 | UpdateCullDistanceVolListAllCullDistanceVolumesume [INDEX] [ENABLE: 0 \| 1] [PAIR0: [SIZE],[DISTANCE]] [PAIR1: [SIZE],[DISTANCE]] ...<br>eg. UpdateCullDistanceVolume 0 0<br>eg. UpdateCullDistanceVolume 1 1 100,2000 200,3000 |
| `voice.sendLocalTalkersToEndpoint` | 1 | This will send audio output for all outgoing voip audio to the named endpoint. if given no arguments, this will disconnect all external endpoints. |
| `voice.sendRemoteTalkersToEndpoint` | 1 | This will send audio output for all incoming voip audio to the named endpoint. if given no arguments, this will route voice output through the game engine. |
| `Widget.DumpTemplateSizes` | 1 | Dump the sizes of all widget class templates in memory |
| `wp.DumpstreamingSources` | 1 | Dumps active streaming sources to the log |
| `wp.Editor.WorldPartitionRuntimeHashSet.Enable` | 1 | Enable experimental runtime hash set class. |
| `wp.Runtime.DebugFilterByCellName` | 1 | Filter debug diplay of world partition streaming by full or partial cell name. Args [cell name] |
| `wp.Runtime.DebugFilterByDataLayer` | 1 | Filter debug diplay of world partition streaming by data layer. Args [datalayer labels] |
| `wp.Runtime.DebugFilterByRuntimeHashGridName` | 1 | Filter debug diplay of world partition streaming by grid name. Args [grid names] |
| `wp.Runtime.DebugFilterByStreamingStatus` | 1 | Filter debug diplay of world partition streaming by streaming status. Args [streaming status] |
| `wp.Runtime.DrawWorldPartitionIndex` | 1 | Sets the index of the wanted partitioned world to display debug draw.<br>Sets < 0 to display debug draw all registered partitioned worlds. |
| `wp.Runtime.DumpDataLayers` | 1 | Dumps data layers to the log |
| `wp.Runtime.HLOD` | 1 | Turn on/off loading & rendering of world partition HLODs. |
| `wp.Runtime.OverrideRuntimeSpatialHashLoadingRange` | 1 | Sets runtime loading range. Args -grid=[index] -range=[override_loading_range] |
| `wp.Runtime.SetDataLayerRuntimeState` | 1 | Sets Runtime DataLayers state. Args [State = Unloaded, Loaded, Activated] [DataLayerNames] |
| `wp.Runtime.ToggleDataLayerActivation` | 1 | Toggles DataLayers active state. Args [DataLayerNames] |
| `wp.Runtime.ToggleDrawDataLayers` | 1 | Toggles debug display of active data layers. |
| `wp.Runtime.ToggleDrawDataLayersLoadTime` | 1 | Toggles debug display of active data layers load time. |
| `wp.Runtime.ToggleDrawLegends` | 1 | Toggles debug display of world partition legends. |
| `wp.Runtime.ToggleDrawRuntimeCellsDetails` | 1 | Toggles debug display of world partition runtime streaming cells. |
| `wp.Runtime.ToggleDrawRuntimeHash2D` | 1 | Toggles 2D debug display of world partition runtime hash. |
| `wp.Runtime.ToggleDrawRuntimeHash3D` | 1 | Toggles 3D debug display of world partition runtime hash. |
| `wp.Runtime.ToggleDrawStreamingPerfs` | 1 | Toggles debug display of world partition streaming perfs. |
| `wp.Runtime.ToggleDrawStreamingSources` | 1 | Toggles debug display of world partition streaming sources. |