# Object-table-only CVar-like candidates

This guide identifies plausible settings among the 427 unique names present in the community `console_objects.tsv` table but absent from its `console_vars.tsv` table. It does not treat all console objects as CVars: command-like entries, mode/data labels, and objects explicitly marked `IAmNoRealVariable` are left in the [complete object catalog](cvar-community-console-objects.md) without being promoted here.

**Candidate count: 247 names** — 223 previously unlisted `ShowFlag.*` entries and 24 additional object-only names. Two related show flags already have focused notes: [`ShowFlag.AntiAliasing`](cvar-object-graphics-candidates.md) and [`ShowFlag.SmartObjects`](cvar-object-engine-candidates.md).

An object-table row alone does not identify the object as a writable console variable. Snapshot membership is only a captured `name=value` observation, and an embedded Shipping string is only literal presence. The exact type, current registration, startup-config acceptance, and runtime effect remain unverified for every candidate below unless another guide provides stronger evidence.

## Show-flag family

The object table gives these names the same generic help: each is associated with overriding a specific rendering show flag. The suffix identifies the named render feature; the supplied text does not establish that any particular flag is registered or effective in the current Shipping build. The two names already covered elsewhere are not repeated here.

| Exact object name | Source-supported interpretation |
| --- | --- |
| `ShowFlag.AllowPrePass` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.AmbientCubemap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.AmbientOcclusion` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Atmosphere` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.AudioRadius` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.BSP` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.BSPSplit` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.BSPTriangles` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.BillboardSprites` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Bloom` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Bones` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Bounds` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Brushes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.BuilderBrush` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CameraAspectRatioBars` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CameraFrustums` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CameraImperfections` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CameraInterpolation` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CameraSafeFrames` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CapsuleShadows` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CastShadowLightOverlap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Cloud` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Collision` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CollisionPawn` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CollisionVisibility` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ColorDebug` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ColorGrading` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ColorHeatMap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CombineLUT` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.CompositeEditorPrimitives` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Constraints` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ContactShadows` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Cover` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DebugAI` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DebugDrawDistantVirtualSMLights` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Decals` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DeferredLighting` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DepthOfField` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Diffuse` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DirectLighting` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DirectionalLights` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DisableOcclusionQueries` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DistanceCulledPrimitives` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DistanceFieldAO` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DrawOnlyVSMInvalidatingGeo` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.DynamicShadows` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.EditingLevelInstance` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Editor` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ExternalResHighlight` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.EyeAdaptation` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Fog` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ForceFeedbackRadius` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.GBufferHints` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Game` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.GameplayDebug` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.GlobalIllumination` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Grain` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Grid` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HISMCClusterTree` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HISMCOcclusionBounds` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HLODColoration` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HMDDistortion` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HeterogeneousVolumes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HighResScreenshotMask` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.HitProxies` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.IndirectLightingCache` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.InputDebugVisualizer` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.InstancedFoliage` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.InstancedGrass` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.InstancedStaticMeshes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LOD` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LODColoration` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Landscape` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LargeVertices` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LensFlares` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LevelColoration` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightComplexity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightDebugMode0` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightDebugMode1` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightDebugMode2` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightFunctions` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightInfluences` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightMapDensity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightRadius` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightShafts` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Lighting` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LightingOnlyOverride` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LocalExposure` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LocalHeightFog` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenDetailTraces` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenFarFieldTraces` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenGlobalIllumination` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenGlobalTraces` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenReflections` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenScreenTraces` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenSecondaryBounces` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.LumenShortRangeAmbientOcclusion` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MassProperties` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MaterialLayersComplexity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MaterialTextureScaleAccuracy` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Materials` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MediaPlanes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MeshEdges` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MeshMaterialsNum` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MeshTriangleDensity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MeshUVDensityAccuracy` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MeshWPO` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ModeWidgets` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.MotionBlur` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.NaniteMeshes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.NaniteStreamingGeometry` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Navigation` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Niagara` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OcclusionMeshes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OnScreenDebug` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OnlyMaterialAO` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OpaqueCompositeEditorPrimitives` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OutputMaterialTextureScales` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.OverrideDiffuseAndSpecular` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Paper2DSprites` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Particles` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PathTracing` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PhysicalMaterialMasks` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PhysicsField` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Pivot` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PointLights` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PostProcessMaterial` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PostProcessing` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PrecomputedVisibility` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PrecomputedVisibilityCells` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PreviewShadowsIndicator` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PrimitiveDistanceAccuracy` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.PropertyColoration` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.QuadOverdraw` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.QuadOverdrawWithMaskOverdraw` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.RayTracedDistanceFieldShadows` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.RayTracingDebug` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.RectLights` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ReflectionEnvironment` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ReflectionOverride` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Refraction` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Rendering` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.RequiredTextureResolution` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SceneColorFringe` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ScreenPercentage` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ScreenSpaceAO` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ScreenSpaceReflections` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Selection` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SelectionOutline` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SeparateTranslucency` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ServerDrawDebug` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ShaderComplexity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ShaderComplexityWithQuadOverdraw` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ShaderPrint` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ShadowFrustums` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SkeletalMeshes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SkyLighting` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Snap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Specular` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Splines` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SpotLights` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.StaticMeshes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.StationaryLightOverlap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.StereoRendering` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.StreamingBounds` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.SubsurfaceScattering` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.TemporalAA` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.TestImage` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.TexLODColoration` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.TextRender` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.TexturedLightProfiles` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.ToneCurve` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Tonemapper` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Translucency` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VREditing` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VectorFields` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VertexColors` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Vignette` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VirtualShadowMapCaching` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VirtualTexturePendingMips` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VirtualTexturePrimitives` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VirtualTextureResidency` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisLog` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeBuffer` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeCalibrationColor` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeCalibrationCustom` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeCalibrationGrayscale` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeDOF` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeDistanceFieldAO` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeGPUSkinCache` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeGlobalDistanceField` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeGroom` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeHDR` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeInstanceUpdates` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeLevelInstanceEditing` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeLightCulling` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeLightingOnProbes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeLocalExposure` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeLumen` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeMeshDistanceFields` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeMotionBlur` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeMotionVectors` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeNanite` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeOutOfBoundsPixels` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizePostProcessStack` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeReprojection` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeSSR` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeSSS` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeSenses` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeShadingModels` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeSkyAtmosphere` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeSubstrate` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeTemporalUpscaler` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeVirtualShadowMap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeVolumetricCloudConservativeDensity` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeVolumetricCloudEmptySpaceSkipping` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VisualizeVolumetricLightmap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VolumeLightingSamples` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Volumes` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VolumetricFog` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.VolumetricLightmap` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.WidgetComponents` | Named rendering show-flag candidate; per-name runtime effect is unverified. |
| `ShowFlag.Wireframe` | Named rendering show-flag candidate; per-name runtime effect is unverified. |

## Other plausible setting candidates

| Exact object name | Supplied clue and limit | Additional evidence |
| --- | --- | --- |
| `102451.UseAverageNormal` | Snapshot name=value entry; object help only echoes the name. The name suggests an average-normal option, but its target and behavior are unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `103711.ScopeRadius.UseFlyTime` | Object help is blank. The name suggests a relationship between scope radius and flight time; the calculation is unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `104971.PinIgnoreSourceLandBeforeLaunched` | Object help is blank. The name suggests a pin/launch condition, but the behavior is unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `1055.SkipInhibitedSpeedUpdate` | Help associates it with ability 105502 speed-modifier updates while a buff is inhibited. The precise runtime conditions are not established. | Help only; no snapshot or matching CVar-shaped Shipping candidate. |
| `1055.fix105542telelport` | Help labels it as an enable/disable fix, but does not define what is corrected. | Help and snapshot; no matching CVar-shaped Shipping candidate. |
| `M2215.BombardDebugLog` | Help identifies detailed Fleet Bombard logging and says the setting is separated between server and client. Runtime scope is unverified. | Help only; no snapshot or matching CVar-shaped Shipping candidate. |
| `Marvel.Feedback.DiagnoseAllowEditor` | No help. The name suggests an editor-related diagnostic control; exact meaning is unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `Marvel.Feedback.DiagnoseForceOff` | No help. The name suggests a force-off diagnostic control; exact target and behavior are unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `Marvel.Feedback.DiagnoseForceOn` | No help. The name suggests a force-on diagnostic control; exact target and behavior are unknown. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `System30104.CheckPhotoSourceSignature` | The name suggests a photo-source signature check. The object help contains only an incomplete value label, so behavior is unresolved. | Snapshot; no matching CVar-shaped Shipping candidate. |
| `TaskGraph.TaskPriorities.AsyncIOCPUWork` | Help associates it with task/thread scheduling for asynchronous I/O decompression, decryption, and signature-check work. Its registered type and current value are unknown. | Object help and a matching Shipping string; no snapshot. |
| `TaskGraph.TaskPriorities.ClearDynamicPageVSM` | Help associates it with task/thread scheduling for Dynamic Page VSM clearing work. Its registered type and current value are unknown. | Object help and a matching Shipping string; no snapshot. |
| `au.AudioSourceManager.HangDiagnostics` | No help. The name suggests audio-source hang diagnostics; the behavior is unknown. | Object-table name and matching Shipping string; no snapshot. |
| `buildidoverride` | Help says it sets the build ID used for matchmaking. Snapshot presence makes it a plausible setting candidate, but does not resolve whether the object is a variable or command. | Object help and snapshot; no matching CVar-shaped Shipping candidate. |
| `networkversionoverride` | Help says it sets the network version used for multiplayer. Snapshot presence makes it a plausible setting candidate, but does not resolve whether the object is a variable or command. | Object help and snapshot; no matching CVar-shaped Shipping candidate. |
| `marvel.AudioGT.AkTick.Enable` | The name and neighboring object help associate it with AudioGT tick diagnostics. The exact switch semantics are not supplied. | Object help and a matching Shipping string; no snapshot. |
| `marvel.AudioGT.AkTick.Interval` | Object help associates it with AudioGT tick interval output; units and the setting’s effect are unknown. | Object help and a matching Shipping string; no snapshot. |
| `marvel.AudioGT.Enable` | The name and object help associate it with AudioGT diagnostics. The controlled feature and effect are not defined. | Object help and a matching Shipping string; no snapshot. |
| `marvel.AudioGT.RoomQuery.Enable` | The name and object help associate it with AudioGT room-query diagnostics. Exact behavior is unknown. | Object help and a matching Shipping string; no snapshot. |
| `marvel.AudioGT.StackStats.Enable` | The name and object help associate it with AudioGT stack statistics. Exact behavior is unknown. | Object help and a matching Shipping string; no snapshot. |
| `marvel.banrecord` | Help associates the name with capture restrictions in a non-disclosure context. Its actual scope and variable-versus-command status are unverified. | Object help and a matching Shipping string; no snapshot. |
| `Landscape.Combine` | Help describes a landscape-component combining mode. The object table does not establish whether this is a variable or a command. | Object help only; no snapshot or matching CVar-shaped Shipping candidate. |
| `Landscape.Patches` | Help describes showing or hiding landscape patches. The object table does not establish whether this is a variable or a command. | Object help only; no snapshot or matching CVar-shaped Shipping candidate. |
| `Landscape.Static` | Help describes enabling or disabling landscape static drawlists. The object table does not establish whether this is a variable or a command. | Object help only; no snapshot or matching CVar-shaped Shipping candidate. |

## Classification and limits

- The 427-name source set contains a mixture of variables, commands, and other console objects. This guide promotes only names whose namespace, help, or captured snapshot makes a setting interpretation plausible; ambiguous cases are labeled as such.
- Command-like entries with explicit operation syntax or action help (for example, asset-registry queries, debug launches/stops, dump/flush operations, and input-forcing commands) remain classified in the [command catalog](cvar-community-commands.md) or the full object catalog.
- Names carrying the object-help sentinel `IAmNoRealVariable` and bare `Level.Mode.*` labels are not counted as candidates.
- The community source does not identify its game build or capture procedure. The Shipping comparison is static and does not prove registration, mutability, or that an `.ini` override is honored.

Sources: [community console-object catalog](cvar-community-console-objects.md) · [community variable registry](cvar-community-registry.md) · [source and build-evidence limits](EVIDENCE.md#build-specific-static-analysis).
