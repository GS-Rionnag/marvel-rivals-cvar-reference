# Third-party engine.ini setting cross-check

This cross-check extracts dotted `name=value` assignments from the public `engine.ini` in [Natram1zh/Marvel-Rivals-Config](https://github.com/Natram1zh/Marvel-Rivals-Config/blob/c5f0a51a44efc954d533287fa72f8919c2c20e32/engine.ini). The source commit is `c5f0a51a44efc954d533287fa72f8919c2c20e32` (2025-01-18 UTC); its values are community settings, not game defaults or tested recommendations. It is older than the local build 1.1.4042190. The extraction is preserved as [`community-engine-config-extract.tsv`](EVIDENCE.md#evidence-artifacts-not-included).

The source file has 160 dotted assignments across sections, representing 132 unique dotted names. Exact comparison finds 96 names in the community `var`/`ref` registry, 2 additional dotted strings in local binaries, and 34 names absent from the registry, current CVar snapshot, Epic 5.9 reference, and local dotted-string scan. Some keys may be config properties, old-engine names, misspellings, or ineffective settings; this source alone cannot establish their behavior.

| Name | Community value(s) and locations | Registry | Local build string | Snapshot | Assessment |
|---|---|---|---|---|---|
| `FX.MaxCPUParticlesPerEmitter` | `20` ([SystemSettings] line 145) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `FX.MaxGPUParticlesSpawnedPerFrame` | `0` ([SystemSettings] line 146) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.AllowAsyncRenderThreadUpdates` | `1` ([SystemSettings] line 55) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.AllowAsyncRenderThreadUpdatesDuringGamethreadUpdates` | `1` ([SystemSettings] line 56) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.AllowAsyncRenderThreadUpdatesEditor` | `1` ([SystemSettings] line 57) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.AllowLandscapeShadows` | `0` ([SystemSettings] line 124) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.AllowStaticLighting` | `0` ([SystemSettings] line 112) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.AmbientOcclusionLevels` | `0` ([SystemSettings] line 82) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.AmbientOcclusionRadiusScale` | `0` ([/script/engine.renderersettings] line 188) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.AOApplyToStaticIndirect` | `0` ([SystemSettings] line 140) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Atmosphere` | `0` ([SystemSettings] line 98, [/script/engine.renderersettings] line 175) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.BloomQuality` | `0` ([SystemSettings] line 84) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.BlurGBuffer` | `0` ([SystemSettings] line 103) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.CapsuleDirectShadows` | `0` ([/script/engine.renderersettings] line 201) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.CapsuleIndirectShadows` | `0` ([/script/engine.renderersettings] line 202) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.CapsuleMaxDirectOcclusionDistance` | `0` ([/script/engine.renderersettings] line 203) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.CapsuleMaxIndirectOcclusionDistance` | `0` ([/script/engine.renderersettings] line 204) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.CapsuleShadows` | `0` ([/script/engine.renderersettings] line 205) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.ContactShadows` | `0` ([SystemSettings] line 125, [SystemSettings] line 142) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.D3D11.UseAllowTearing` | `1` ([SystemSettings] line 63) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.D3D12.UseAllowTearing` | `1` ([SystemSettings] line 64) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DefaultFeature.AmbientOcclusion` | `False` ([SystemSettings] line 81, [/script/engine.renderersettings] line 168) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DefaultFeature.AntiAliasing` | `0` ([/script/engine.renderersettings] line 165) | no | yes | no | Embedded string only; registration/meaning unconfirmed |
| `r.DefaultFeature.Bloom` | `False` ([SystemSettings] line 83, [/script/engine.renderersettings] line 170) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DefaultFeature.DepthOfField` | `False` ([/script/engine.renderersettings] line 167) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.DefaultFeature.LensFlare` | `False` ([SystemSettings] line 85, [/script/engine.renderersettings] line 166) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DefaultFeature.MotionBlur` | `False` ([SystemSettings] line 87, [/script/engine.renderersettings] line 169) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DepthOfField.MaxSize` | `0` ([SystemSettings] line 22) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DepthOfFieldQuality` | `0` ([SystemSettings] line 89) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DetailMode` | `1` ([SystemSettings] line 105) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DFShadowScatterTileCulling` | `0` ([/script/engine.renderersettings] line 198) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DistanceFieldAO` | `0` ([SystemSettings] line 40, [ConsoleVariables] line 160) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DistanceFields.MaxPerObjectResolution` | `0` ([SystemSettings] line 39, [ConsoleVariables] line 159) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.DistanceFieldShadowing` | `0` ([/script/engine.renderersettings] line 189) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.DynamicShadows` | `0` ([SystemSettings] line 110) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.EmitterSpawnRateScale` | `0` ([SystemSettings] line 16) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.EyeAdaptationQuality` | `1` ([SystemSettings] line 108) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.FastBlurThreshold` | `0` ([SystemSettings] line 91) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Fog` | `0` ([SystemSettings] line 96, [/script/engine.renderersettings] line 174) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.GenerateMeshDistanceFields` | `0` ([SystemSettings] line 38, [ConsoleVariables] line 158) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.GTSyncType` | `1` ([SystemSettings] line 62) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.IndirectLightingCache` | `0` ([/script/engine.renderersettings] line 196) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LandscapeLOD0DistributionScale` | `1` ([SystemSettings] line 70) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LandscapeLODBias` | `0` ([SystemSettings] line 68) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.LandscapeLODDistributionScale` | `1` ([SystemSettings] line 69) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LensFlareQuality` | `0` ([SystemSettings] line 86) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LevelStreamingDistanceScale` | `1` ([SystemSettings] line 13) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.LightFunction` | `0` ([SystemSettings] line 99) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.LightFunctionQuality` | `0` ([/script/engine.renderersettings] line 179) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LightMaxDrawDistanceScale` | `0.01` ([SystemSettings] line 126) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LightShaftQuality` | `0` ([/script/engine.renderersettings] line 191) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.LightShafts` | `0` ([/script/engine.renderersettings] line 180) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.LODFadeTime` | `2` ([SystemSettings] line 71) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Lumen.GlobalIllumination` | `0` ([SystemSettings] line 26, [ConsoleVariables] line 153) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.Lumen.Reflections.Enable` | `0` ([SystemSettings] line 25, [ConsoleVariables] line 152) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.Lumen.ScreenProbeGather.DownsampleFactor` | `4` ([SystemSettings] line 28, [ConsoleVariables] line 154) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MaterialQuality` | `1` ([SystemSettings] line 21) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.MaterialQualityLevel` | `1` ([SystemSettings] line 17) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MaxAnisotropy` | `0` ([SystemSettings] line 104) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MaxCSMRadiusToAllowPerObjectShadows` | `0.01` ([SystemSettings] line 130) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MipMapLODBias` | `1` ([SystemSettings] line 109) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MobileHDR` | `False` ([SystemSettings] line 111, [/script/engine.renderersettings] line 171) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.MotionBlurQuality` | `0` ([SystemSettings] line 88) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Nanite` | `0` ([SystemSettings] line 31, [ConsoleVariables] line 155) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.OnlyStreamInTextures` | `True` ([SystemSettings] line 77) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.OptimizeForUAVPerformance` | `0` ([/script/engine.renderersettings] line 197) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.ParallelShadows` | `0` ([/script/engine.renderersettings] line 199) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.ParticleLightQuality` | `0` ([SystemSettings] line 148) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.ParticleLODBias` | `3` ([SystemSettings] line 147) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.PostProcessAAQuality` | `0` ([SystemSettings] line 102, [/script/engine.renderersettings] line 181) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.RayTracing` | `0` ([SystemSettings] line 50) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.RayTracing.ForceAllRayTracingEffectsOff` | `1` ([SystemSettings] line 49, [ConsoleVariables] line 151) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.RayTracing.Translucency.Shadows` | `0` ([SystemSettings] line 132) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.ReduceThreadLatency` | `1` ([SystemSettings] line 58) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.ReflectionEnvironment` | `0` ([SystemSettings] line 127, [/script/engine.renderersettings] line 176) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.RefractionQuality` | `0` ([SystemSettings] line 92) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.RHICmdAsyncCompute` | `1` ([SystemSettings] line 54) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.RHICmdUseParallelAlgorithms` | `1` ([SystemSettings] line 53) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.SceneColorFormat` | `3` ([SystemSettings] line 93) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SceneColorFringeQuality` | `0` ([SystemSettings] line 90) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SeparateTranslucency` | `True` ([SystemSettings] line 95) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shaders.Optimize` | `1` ([SystemSettings] line 61) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.CachedShadowsCastFromMovablePrimitives` | `0` ([SystemSettings] line 134) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.CachePreshadow` | `1` ([SystemSettings] line 133) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.CSM.MaxCascades` | `1` ([SystemSettings] line 117) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.CSM.TransitionScale` | `0` ([SystemSettings] line 118) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.DistanceScale` | `0` ([SystemSettings] line 119) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.FadeExponent` | `1` ([SystemSettings] line 137) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.LightViewConvexHullCull` | `0` ([SystemSettings] line 135) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.MaxCSMResolution` | `0` ([SystemSettings] line 121, [/script/engine.renderersettings] line 173) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.MaxResolution` | `64; 0` ([SystemSettings] line 116, [SystemSettings] line 122, [/script/engine.renderersettings] line 172) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.PerObject` | `1` ([SystemSettings] line 123) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.PerObjectCastDistanceRadiusScale` | `0.001` ([SystemSettings] line 141) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.PreshadowExpand` | `-1` ([SystemSettings] line 138) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.Preshadows` | `0` ([SystemSettings] line 139) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.RadiusThreshold` | `0` ([SystemSettings] line 120) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.RectLightReceiverBias` | `0` ([/script/engine.renderersettings] line 206) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.TransitionScale` | `9` ([SystemSettings] line 136) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadow.Virtual.Disable` | `1` ([SystemSettings] line 34, [ConsoleVariables] line 156) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.Shadow.Virtual.SMRT` | `0` ([SystemSettings] line 35, [ConsoleVariables] line 157) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.ShadowQuality` | `0` ([SystemSettings] line 115) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Shadows.SpotLightTransitionScale` | `1` ([/script/engine.renderersettings] line 194) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.SimpleDynamicLighting` | `0` ([SystemSettings] line 131) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.SkeletalMeshLODBias` | `3` ([SystemSettings] line 15) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SkeletalMeshLODRadiusScale` | `0.25` ([/script/engine.renderersettings] line 200) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SSR` | `0` ([SystemSettings] line 101, [/script/engine.renderersettings] line 182) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.SSR.Quality` | `0` ([SystemSettings] line 100) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SSS.SampleSet` | `0` ([SystemSettings] line 18) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.SSS.Scale` | `0` ([SystemSettings] line 19) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.StaticMeshLODDistanceScale` | `0.10` ([SystemSettings] line 14) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Strata` | `0` ([SystemSettings] line 46, [ConsoleVariables] line 162) | no | yes | no | Embedded string only; registration/meaning unconfirmed |
| `r.Streaming.Boost` | `0.1` ([SystemSettings] line 73, [/script/engine.renderersettings] line 183) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Streaming.LimitPoolSizeToVRAM` | `0` ([SystemSettings] line 76) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Streaming.MipBias` | `3` ([/script/engine.renderersettings] line 193) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Streaming.PoolSize` | `0` ([SystemSettings] line 78) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Streaming.ScaleTexturesByGlobalMyBias` | `1` ([SystemSettings] line 75) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.SwitchGridShadow` | `0` ([SystemSettings] line 20) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.TextureStreaming` | `1` ([SystemSettings] line 74) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Tonemapper.GrainQuantization` | `0` ([/script/engine.renderersettings] line 177) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.Tonemapper.Sharpen` | `0.0` ([SystemSettings] line 107) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.TonemapperGamma` | `3` ([/script/engine.renderersettings] line 178) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.TonemapperQuality` | `0` ([SystemSettings] line 106) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.TranslucencyLightingVolumeDim` | `24` ([/script/engine.renderersettings] line 192) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.TranslucencyVolumeBlur` | `0` ([SystemSettings] line 94) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.TranslucentLightingVolume` | `0` ([/script/engine.renderersettings] line 195) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.TriangleOrderOptimization` | `1` ([/script/engine.renderersettings] line 184) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.UITextureLODBias` | `-1` ([SystemSettings] line 72) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.Upscale.Quality` | `0` ([/script/engine.renderersettings] line 190) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.ViewDistanceScale` | `0.6666; 0.5` ([SystemSettings] line 67, [/script/engine.renderersettings] line 185) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `r.VirtualHeightfieldMesh` | `0` ([SystemSettings] line 43, [ConsoleVariables] line 161) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |
| `r.VolumetricFog` | `0` ([SystemSettings] line 97) | yes | yes | yes | Listed as var/ref; definition in registry catalog |
| `rhi.DefaultRHI` | `D3D12` ([SystemSettings] line 10) | no | no | no | No exact registry or local binary match; likely stale, unsupported, or misspelled |

## Additional public user configuration: uncorroborated names

A separate public [`userengine.ini`](https://github.com/RitzDaCat/MarvelRivalsConfig/blob/26cf358988f2d74004544ca128fd3a3ae1a3aa79/userengine.ini) presents itself as a UE5 performance configuration; its header says it was last updated in December 2024. This file is a community claim, not a tested Marvel Rivals config. Seven dotted names in it have no exact match in the preserved `var`/`ref`/command registry, console-object table, value snapshot, UE 5.9 comparison, or scanned 1.1.4042190 executable inventory:

| Exact name | Evidence in this project |
| --- | --- |
| `D3D12.MaximumFrameLatency` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.Lumen.Enabled` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.Nanite.Enable` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.LightPropagationVolume` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.SSGI.Enable` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.SSR.Enable` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |
| `r.AmbientOcclusion.Quality` | Source-only key. No independent registration, upstream-reference, or local-build match was found. |

These are retained as unverified CVar-shaped config candidates, not counted as confirmed variables. The source's performance and latency claims are not repeated here because this pass found no corroborating game or engine definition for these exact names.

## Other public community configs: additional unverified names

The following public sources contain CVar-shaped names that did not exactly match the preserved community registry, console-object table, snapshot, Epic UE 5.9 reference, the extracted third-party engine config, or the local 1.1.4042190 build inventories. They are recorded only as search leads. Appearance in a config file does not show that Marvel Rivals registers the name, accepts it at startup, or changes behavior.

### RoboMWM Scalability.ini gist

The [RoboMWM gist](https://gist.github.com/RoboMWM/ae6fd0689c949322ba973322cada2888) contains these ten additional exact names:

| Exact name | Evidence status |
| --- | --- |
| `r.Distortion` | Gist-only candidate; no independent exact match found. |
| `r.FogDensity` | Gist-only candidate; no independent exact match found. |
| `r.GlobalIllumination` | Gist-only candidate; no independent exact match found. |
| `r.Lumen.Reflections.EnableHWRT` | Gist-only candidate; no independent exact match found. |
| `r.Lumen.Reflections.HighQuality` | Gist-only candidate; no independent exact match found. |
| `r.Reflections` | Gist-only candidate; no independent exact match found. |
| `r.TemporalAA` | Gist-only candidate; no independent exact match found. |
| `r.TemporalAASharpness` | Gist-only candidate; no independent exact match found. |
| `r.Tessellation` | Gist-only candidate; no independent exact match found. |
| `r.TiledDeferredShading.MinimumCount` | Gist-only candidate; no independent exact match found. |

### Marvel Rivals FPS Booster

The pinned [`MarvelRivalsFPSBooster.hta`](https://github.com/n0tmar/Marvel-Rivals-FPS-Booster/blob/0eee0d36c0775fca09b8ae7fb30537c2d6e562a3/MarvelRivalsFPSBooster.hta) embeds a generated Scalability.ini template. Four names in that template had no independent exact match:

| Exact name | Evidence status |
| --- | --- |
| `PM.CaptiveMode` | Template-only candidate; no independent exact match found. |
| `r.ActiveProjectPackageManager` | Template-only candidate; no independent exact match found. |
| `r.HairStrands.CamByVTPipe` | Template-only candidate; no independent exact match found. |
| `r.Streaming.IPV` | Template-only candidate; no independent exact match found. |

### Two Pastebin configs linked by Odyi's guide

The [Odyi config guide](https://github.com/Odyi/Config-settings-for-marvel-rivals/blob/main/Instructions.md) links two community config snippets ([first](https://pastebin.com/DGiLxGgp), [second](https://pastebin.com/GpwmPxpc)). Together they contain six names below without independent exact matches. `r.Distortion` is already listed in the gist section above, so the distinct-name total increases by five here.

| Exact name | Evidence status |
| --- | --- |
| `r.DefaultFeature.Fog` | Pastebin-only candidate; no independent exact match found. |
| `r.DefaultFeature.Reflections` | Pastebin-only candidate; no independent exact match found. |
| `r.DefaultFeature.Translucency` | Pastebin-only candidate; no independent exact match found. |
| `r.PoolSize` | Pastebin-only candidate; no independent exact match found. |
| `r.TSR.Sharpen` | Pastebin-only candidate; no independent exact match found. |
| `r.UseVSync` | Pastebin-only candidate; no independent exact match found. |

The three sources add 19 distinct unverified names (10 gist, 4 template, and 5 new names from the Pastebins after deduplication). They do not change the registry count or establish that any of these names are editable in Marvel Rivals.
