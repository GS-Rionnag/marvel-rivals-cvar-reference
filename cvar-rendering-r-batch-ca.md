# Vulkan and water rendering CVars (batch CA)

The next 35 uncovered exact `r.*` names after [batch BZ](cvar-rendering-r-batch-bz.md) cover Vulkan command submission and diagnostics, renderer diagnostics and warp culling, and water rendering. The snapshot column records observed values. The Epic column gives exact-name UE 5.9 reference defaults from the local catalog. A dash means the corresponding source has no entry.

| Exact CVar | Kind / type | Snapshot | Epic 5.9 | Meaning from supplied help | `ref_rva` / `obj_rva` memory candidates |
| --- | --- | ---: | ---: | --- | ---: |
| `r.Vulkan.SubmitOcclusionBatchCmdBuffer` | `var` / `int32` | `1` | — | `1` submits the command buffer after an occlusion query batch ends. Help labels `1` the default. | 0 / 2 |
| `r.Vulkan.SubmitOnDispatch` | `var` / `int32` | `0` | — | `1` submits the command buffer after each dispatch. Help labels the ordinary dispatch behavior `0` the default. | 0 / 3 |
| `r.Vulkan.SubmitOnTextureUnlock` | `ref` / `int32` | `1` | — | `1` submits the upload command buffer at each texture unlock and is the help-stated default. `0` disables that submission. | 1 / 3 |
| `r.Vulkan.SwapChainIgnoreExtraImages` | `ref` / `int32` | `0` | — | Whether to use only the requested number of images when the swap chain creates extras. | 1 / 3 |
| `r.Vulkan.TimestampQueryStage` | `var` / `int32` | `0` | — | `0` timestamps at the top of the pipeline and is the help-stated default. `1` timestamps at the bottom. Help describes the latter as more precise and more likely to affect performance on some platforms. | 0 / 2 |
| `r.Vulkan.UniqueValidationMessages` | `var` / `int32` | `1` | — | Filters repeated validation errors by error code when `r.Vulkan.EnableValidation` is nonzero. | 0 / 3 |
| `r.Vulkan.UploadCmdBufferSemaphore` | `ref` / `int32` | `0` | — | `0` submits upload and graphics buffers without synchronizing them to each other and is the help-stated default. `1` prevents graphics command buffers from overlapping upload command buffers. | 8 / 3 |
| `r.Vulkan.UseBufferBinning` | `ref` / `int32` | `0` | — | Bins suballocations within buffers to reduce fragmentation, potentially raising peak allocation. Help marks the setting read-only. | 1 / 3 |
| `r.Vulkan.UseCmdBufferTimingForGPUTime` | `ref` / `int32` | `0` | — | Uses profiling command-buffer timings to measure GPU time. | 4 / 3 |
| `r.Vulkan.UseMemoryBarrierOpt` | `ref` / `int32` | `1` | — | `1` combines eligible buffer barriers and image barriers without layout transitions into a memory barrier. Help labels it the default. `0` preserves individual barriers for resource tracking in external tools. | 1 / 3 |
| `r.Vulkan.UseProfileCheck` | `var` / `int32` | `1` | — | `1` verifies requested feature-level support with a profile check and is the help-stated default. `0` assumes support. | 0 / 3 |
| `r.Vulkan.UseSingleQueue` | `ref` / `int32` | `0` | — | `1` always submits uploads and graphics work to the graphics queue. Help labels the multiple-queue mode `0` the default. | 0 / 3 |
| `r.Vulkan.VRSFormat` | `var` / `int32` | `0` | — | Variable rate shading selection. `0` prefers Fragment Shading Rate when both formats are available. `1` uses it if available and reports its absence. `2` requires it and errors if unavailable. `3` prefers Fragment Density Map when both are available. `4` uses Fragment Density Map if available. Both registry help fields truncate the description of mode `4`. | 0 / 2 |
| `r.Vulkan.WaitForIdleOnSubmit` | `ref` / `int32` | `0` | — | GPU hang diagnostic. `0` skips the idle wait and is the help-stated default. `1` waits on every submit, `2` on upload-buffer submits, and `3` on active graphics-buffer submits. | 3 / 2 |
| `r.VulkanNVAfterMathDumpWaitTime` | `ref` / `float` | `10` | — | Time to wait for NVIDIA Aftermath to finish processing GPU crash dumps. The help leaves the unit unspecified. | 1 / 3 |
| `r.WarningOnRedundantTransformUpdate` | `ref` / `int32` | `0` | `0` | Warns when `UpdatePrimitiveTransform` is called redundantly. | 1 / 3 |
| `r.WarpCulling` | `var` / `int32` | `0` | `0` | Enables warp culling on supported platforms at `1`. Help labels `0` disabled by default. | 0 / 3 |
| `r.Water.SingleLayer` | `var` / `int32` | `1` | `1` | Enables the Single Layer Water rendering system. | 0 / 3 |
| `r.Water.SingleLayer.DepthPrepass` | `var` / `int32` | `1` | `1` | Enables the water depth prepass. Help describes it as required for proper Virtual Shadow Map (VSM) support. | 0 / 3 |
| `r.Water.SingleLayer.DistanceFieldShadow` | `var` / `int32` | `1` | `1` | Toggles distance-field shadow tracing for Single Layer Water at runtime under deferred shading, according to the help. | 0 / 3 |
| `r.Water.SingleLayer.OptimizedClear` | `var` / `int32` | `1` | `1` | Toggles optimized depth clearing. | 0 / 3 |
| `r.Water.SingleLayer.Reflection` | `var` / `int32` | `1` | `1` | `0` disables water reflections, `1` uses the scene's reflection technique, `2` forces reflection captures and sky, and `3` forces screen-space reflections (SSR). | 0 / 3 |
| `r.Water.SingleLayer.RefractionDownsampleFactor` | `ref` / `int32` | `1` | `1` | Resolution divisor for the water refraction buffer. | 5 / 3 |
| `r.Water.SingleLayer.RestoreSceneDepthBeforeSmoothOutline` | `var` / `int32` | `1` | — | `0` keeps water-inclusive scene depth for downstream passes. `1` restores the pre-water depth in `SceneTextures.Depth` when the effective PostProcessVolume setting `RestoreSceneDepthAfterWater` is also enabled. | 0 / 3 |
| `r.Water.SingleLayer.SSRTAA` | `var` / `int32` | `1` | `1` | Denoises Single Layer Water screen-space reflections using temporal antialiasing. | 0 / 3 |
| `r.Water.SingleLayer.ShadersSupportDistanceFieldShadow` | `var` / `int32` | `0` | `1` | Compiles Single Layer Water material shaders with distance-field shadow support and outputs the main directional light's luminance to a separate render target. Help requires deferred shading and project distance-field support. | 0 / 3 |
| `r.Water.SingleLayer.ShadersSupportVSMFiltering` | `var` / `int32` | `0` | `0` | Compiles Single Layer Water material shaders with VSM filtering support and outputs the main directional light's luminance to a separate render target. Help requires deferred shading and project VSM support. | 0 / 3 |
| `r.Water.SingleLayer.TiledComposite` | `var` / `int32` | `1` | `1` | Enables tiled compositing for Single Layer Water reflections. | 0 / 3 |
| `r.Water.SingleLayer.UnderwaterFogWhenCameraIsAboveWater` | `var` / `bool` | `false` | `false` | Renders height fog behind the surface from above water. Help describes fewer artifacts when crossing the surface in strong height fog and more artifacts when viewing it from afar. | 0 / 3 |
| `r.Water.SingleLayer.VSMFiltering` | `var` / `int32` | `0` | `0` | Toggles VSM filtering for Single Layer Water at runtime under deferred shading, according to the help. | 0 / 3 |
| `r.Water.SingleLayerWater.SupportCloudShadow` | `var` / `int32` | `0` | — | Enables cloud shadows on SingleLayerWater materials. | 0 / 3 |
| `r.Water.WaterInfo.DilationOverwriteMinimumDistance` | `var` / `float` | `128` | `128` | Help describes a minimum below-ground distance for dilation to overwrite water. Its wording matches the depth-offset entry below, leaving their distinction and units unresolved. | 0 / 3 |
| `r.Water.WaterInfo.RenderCaptureNextWaterInfoDraws` | `var` / `int32` | `0` | `0` | Captures the water info texture for the next specified number of draws. | 0 / 3 |
| `r.Water.WaterInfo.UndergroundDilationDepthOffset` | `var` / `float` | `64` | `64` | Help repeats the minimum below-ground distance description from the overwrite setting. It gives no separate depth-offset semantics or unit. | 0 / 3 |
| `r.WaterWave.AsyncQualityLoad` | `var` / `int32` | — | — | Loads Enhanced Water Wave quality render targets synchronously at `0` and asynchronously at `1`. Help labels `0` the default. | 0 / 3 |

The Shipping 1.1.4042190 static scan counts direct-memory candidates in the final column. It additionally found one address-taking instruction per listed `obj_rva` and one per `ref` entry's `ref_rva`. Direct-memory candidates may represent initialization, reads, or writes. This evidence leaves backend activation, `.ini` acceptance, and visible effects unverified. The captured `0` for `r.Water.SingleLayer.ShadersSupportDistanceFieldShadow` differs from Epic's UE 5.9 default of `1`. The captured value alone gives no game default.

Registry help and snapshot values come from the [preserved community sources](EVIDENCE.md#community-sources). Epic comparisons use the [community registry catalog](EVIDENCE.md#community-sources). The [address-match TSV](EVIDENCE.md#build-specific-static-analysis) and [build analysis](EVIDENCE.md#build-specific-static-analysis) describe the scan.
