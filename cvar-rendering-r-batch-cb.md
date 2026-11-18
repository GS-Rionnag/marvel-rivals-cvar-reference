# Water, display, and Intel Xe rendering CVars (batch CB)

The next 45 uncovered exact `r.*` variables after [batch CA](cvar-rendering-r-batch-ca.md) cover water waves, display modes, shader compilation, Intel Xe frame generation, latency and upscaling, and other renderer controls. The snapshot column records observed values. Epic values are exact-name UE 5.9 defaults from the local catalog. A dash indicates an absent source value.

| Exact CVar | Kind / type | Snapshot | Epic 5.9 | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | ---: | --- | ---: | ---: |
| `r.WaterWave.Quality` | `var` / `int32` | `1` | — | Selects Enhanced Water Wave quality. 0 selects low and 1 selects high. | 0 / 3 | 0 / 1 |
| `r.WaterWaveUpdateDistEveryFrame` | `var` / `float` | `0.001` | — | The help repeats the name and leaves the distance, unit, and precise per-frame behavior unspecified. | 0 / 3 | 0 / 1 |
| `r.WideCustomResolve` | `var` / `int32` | `0` | `0` | Selects the multisample antialiasing resolve filter. 0 selects the hardware box filter. 1, 2, and 3 use custom radii of 1.25, 1.4, and 1.5 with 12, 16, and 20 samples respectively. | 0 / 3 | 0 / 1 |
| `r.Windows.EnableTrueFullScreenUseNearestMonitorResolution` | `ref` / `int32` | `0` | — | Allows true fullscreen to use the nearest monitor resolution. Help leaves the monitor or mode selection rule unspecified. | 3 / 3 | 1 / 1 |
| `r.Windows.ReshapeAllWhenSwitchToFullScreen` | `ref` / `int32` | `1` | — | Forces window rectangle reshaping when resizing to fullscreen on Windows. Help gives no further scope for the reshape. | 1 / 3 | 1 / 1 |
| `r.WireframeCullThreshold` | `ref` / `float` | `5` | `5` | Culls objects below a threshold in orthographic wireframe views. Help leaves the measurement and units unspecified. | 0 / 3 | 1 / 1 |
| `r.XGEShaderCompile.MinBatchSize` | `ref` / `int32` | `50` | `50` | Deprecated shader-compile batch-size setting. Help points to r.ShaderCompiler.DistributedMinBatchSize. | 0 / 2 | 2 / 1 |
| `r.XeFG.ClearSceneColorAlpha` | `var` / `int32` | `1` | — | Whether to clear the scene-color alpha channel. Help gives 1 as the default. | 0 / 3 | 0 / 1 |
| `r.XeFG.Enabled` | `var` / `int32` | `0` | — | Set to 1 to enable XeFG frame generation. Help gives 0 as the default. | 0 / 3 | 0 / 1 |
| `r.XeFG.LogLevel` | `var` / `int32` | `2` | — | XeFG SDK minimum log level. 0 is Debug, 1 Info, 2 Warning, 3 Error, and 4 Off. Help names 1 as the default and lists -XeFGLogLevel= as a command-line input. | 0 / 3 | 0 / 1 |
| `r.XeFG.MaxInterpolatedFrames` | `var` / `int32` | `1` | — | Caps interpolated frames. The default 0 selects the supported maximum automatically. Explicit values range from 1 to r.XeFG.MaxInterpolatedFramesSupported. | 0 / 3 | 0 / 1 |
| `r.XeFG.MaxInterpolatedFramesSupported` | `ref` / `int32` | `1` | — | Reports the maximum number of interpolated frames XeFG supports. | 3 / 3 | 1 / 1 |
| `r.XeFG.ModuleDisabled` | `var` / `bool` | `false` | — | Indicates whether the -XeFGDisabled command-line option disabled XeFG modules. | 0 / 3 | 0 / 1 |
| `r.XeFG.MotionVectorScale` | `var` / `float` | `1` | — | Scales motion vectors. Help gives 1.0 as the default. | 0 / 3 | 0 / 1 |
| `r.XeFG.OverrideSwapChain` | `var` / `bool` | `true` | — | Whether to override the swap chain. Help gives true as the default and mentions reducing conflicts with similar plugins. | 0 / 3 | 0 / 1 |
| `r.XeFG.ResourceValidity` | `var` / `int32` | `1` | — | Selects XeFG input-resource validity. 0 is XEFG_SWAPCHAIN_RV_UNTIL_NEXT_PRESENT and 1 is XEFG_SWAPCHAIN_RV_ONLY_NOW. Help gives 1 as the default and lists -XeFGResourceValidity= as a command-line input. | 0 / 3 | 0 / 1 |
| `r.XeFG.Supported` | `var` / `bool` | `true` | — | Indicates whether XeFG is supported. | 0 / 3 | 0 / 1 |
| `r.XeFG.TagUI` | `var` / `int32` | `1` | — | Tags UI color and alpha. Help gives 1 as the default. | 0 / 3 | 0 / 1 |
| `r.XeFG.TagUIAlphaThreshold` | `var` / `float` | `0` | — | Alpha threshold for the UI extraction pass. Help gives 0.0 as the default. | 0 / 3 | 0 / 1 |
| `r.XeFG.UICompositionState` | `var` / `int32` | `0` | — | Toggles UI composition. Help gives 0 as the disabled default and 1 as enabled. | 0 / 3 | 0 / 1 |
| `r.XeFG.UIMode` | `var` / `int32` | `5` | — | Selects frame-generation UI handling. 0 selects automatically from the inputs. 1 interpolates the back buffer directly. 2 also refines UI with its texture and alpha. 3 interpolates HUD-free color and blends UI from its texture and alpha. 4 interpolates HUD-free color and extracts UI from the back buffer. 5 combines the blend and extraction approaches on HUD-free color and is the help-stated default. | 0 / 3 | 0 / 1 |
| `r.XeFG.Version` | `var` / `FString` | — | — | Displays the XeFG SDK version. | 0 / 3 | 0 / 1 |
| `r.XeLL.AllowRepeatedMarkers` | `ref` / `int32` | `0` | — | Allows sending repeated markers to the XeLL SDK. | 8 / 3 | 1 / 1 |
| `r.XeLL.DisableLatencyMarkers` | `ref` / `int32` | `0` | — | Disables XeLL latency markers. | 3 / 3 | 1 / 1 |
| `r.XeLL.DisableTickRateHandler` | `ref` / `int32` | `1` | — | Disables the XeLL tick-rate handler. | 2 / 3 | 1 / 1 |
| `r.XeLL.EnableLatencyResult` | `ref` / `int32` | `0` | — | Refers to enabling the XeLL latency result. Help marks the result unavailable. | 0 / 3 | 1 / 1 |
| `r.XeLL.Enabled` | `var` / `int32` | `0` | — | 0 turns XeLL off and 1 enables low latency. | 0 / 3 | 0 / 1 |
| `r.XeLL.LogLevel` | `var` / `int32` | `2` | — | XeLL SDK minimum log level. 0 is Debug, 1 Info, 2 Warning, 3 Error, and 4 Off. Help gives 1 as the default and lists -XeLLLogLevel= as a command-line input. | 0 / 3 | 0 / 1 |
| `r.XeLL.MinIntervalUS` | `var` / `int32` | `-1` | — | Minimum XeLL interval in microseconds. -1 uses the engine default. A positive value overrides it. Help leaves 0 unspecified. | 0 / 3 | 0 / 1 |
| `r.XeLL.ModuleDisabled` | `var` / `bool` | `false` | — | Indicates whether the -XeLLDisabled command-line option disabled XeLL modules. | 0 / 3 | 0 / 1 |
| `r.XeLL.Supported` | `var` / `bool` | `true` | — | Indicates whether XeLL is supported. | 0 / 3 | 0 / 1 |
| `r.XeLL.Version` | `var` / `FString` | — | — | Displays the XeLL SDK version. | 0 / 3 | 0 / 1 |
| `r.XeSS.AutoExposure` | `var` / `int32` | `1` | — | Uses XeSS internal auto exposure. Help gives 1 as the default. | 0 / 3 | 0 / 1 |
| `r.XeSS.EagerResolutionFractions` | `var` / `int32` | — | — | 1 restores eager population of the resolution-fraction table during startup probing. Help estimates about 22 MiB in additional startup allocation and gives 0 as the default. | 0 / 3 | 0 / 1 |
| `r.XeSS.Enabled` | `var` / `int32` | `0` | — | 1 selects XeSS upscaling in place of TAAU or another upscaling method. Help gives 0 as the default. | 0 / 3 | 0 / 1 |
| `r.XeSS.Experimental.PreExposure` | `var` / `int32` | `1` | — | Controls pre-exposure across Unreal versions. Help gives 1 as the default. | 0 / 3 | 0 / 1 |
| `r.XeSS.LogLevel` | `var` / `int32` | `2` | — | XeSS SDK minimum log level. 0 is Debug, 1 Info, 2 Warning, 3 Error, and 4 Off. Help gives 1 as the default and lists -XeSSLogLevel= as a command-line input. | 0 / 3 | 0 / 1 |
| `r.XeSS.ModuleDisabled` | `var` / `bool` | `false` | — | Indicates whether the -XeSSDisabled command-line option disabled XeSS modules. | 0 / 3 | 0 / 1 |
| `r.XeSS.OptimalScreenPercentage` | `var` / `float` | `50` | — | Optimal screen percentage for the current XeSS quality setting. | 0 / 3 | 0 / 1 |
| `r.XeSS.Quality` | `var` / `int32` | `2` | — | XeSS quality modes are 0 Ultra Performance, 1 Performance, 2 Balanced (help default), 3 Quality, 4 Ultra Quality, 5 Ultra Quality Plus, and 6 Anti-Aliasing. | 0 / 3 | 0 / 1 |
| `r.XeSS.Supported` | `var` / `bool` | `true` | — | Indicates whether XeSS is supported. | 0 / 3 | 0 / 1 |
| `r.XeSS.Version` | `var` / `FString` | — | — | Displays the XeSS SDK version. | 0 / 3 | 0 / 1 |
| `r.openheroskincustombyskinid` | `var` / `int32` | `1` | — | 0 always uses legacy SculptID customization. 1 uses the SkinID chain when configured and otherwise falls back to legacy lookup. | 0 / 3 | 0 / 1 |
| `r.portal.PS4UseSceneDepthInstead` | `var` / `int32` | `0` | — | Help mentions incorrect PS4 depth copying and ends mid-sentence. The exact workaround and mode values are unresolved. | 0 / 3 | 0 / 1 |
| `r.postprocessing.EnableBloom` | `ref` / `bool` | `true` | — | Global bloom rendering switch. Help gives no mode values. | 1 / 3 | 1 / 1 |

The scan columns count direct-memory and address-taking candidates for `ref_rva` and `obj_rva` in the Shipping 1.1.4042190 scan. Direct-memory candidates may include initialization, reads, and writes. The scan and captured values leave feature support, startup override acceptance, and visible effects unverified.

Registry help and snapshots come from the [preserved sources](EVIDENCE.md#community-sources). Epic defaults appear in the [community registry catalog](EVIDENCE.md#community-sources). See the [address-match TSV](EVIDENCE.md#build-specific-static-analysis) and [build notes](EVIDENCE.md#build-specific-static-analysis) for scan evidence.
