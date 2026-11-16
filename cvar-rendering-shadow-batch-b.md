# Shadow rendering CVar notes — batch B

This page covers 25 exact names from the community `var`/`ref` registry. Registry descriptions are reported as source help and interpreted conservatively; they do not establish that a setting is effective in Marvel Rivals. Each `CVarDump.txt` value below is a captured snapshot value, not a verified default or recommendation. See [the source notes](EVIDENCE.md#build-specific-static-analysis), [the generated registry](cvar-community-registry.md), and [the override research](cvar-overrides.md) for provenance and loader limits.

## Evidence and how to use the table

The local address scan is for Marvel Rivals 1.1.4042190 Shipping. All 24 rows whose registry `kind` is `var` have an `obj_rva` and `ref_rva=0`; the scan shows one address-taking `lea` and 2–3 `mov` direct-memory candidates targeting each `obj_rva`. These `mov` instructions target the CVar object address and appear to be object-pointer writes/initialization, not reads of the CVar's value. They are not runtime-use proof. `r.Shadow.Debug.SortMethod` is a `ref` row with nonzero `ref_rva`; the local scan finds only an address-taking `lea` for that reference, no value read. Thus this pass gives no confirmed local value-read evidence for any of these 25 names. This does not prove they are unused; indirect access and other code paths are outside this scan's evidence.

“UE 5.9 default” means an exact-name match in Epic's published reference. It is upstream context only: Marvel Rivals uses a fork and the current build's registration or behavior is not proven by the match. “Not located” means no exact UE 5.9 reference row was found. The loader's `[Overrides]` `name=value` syntax can express these names; syntax and merge behavior do not prove the game accepts, retains, or acts on a setting. The loader's provided policy says settings that can remove smoke or other effects are ignored; no CVar-specific policy decision is inferred here.

## Exact-name inventory

| Exact CVar | Registry type / kind | Captured snapshot | UE 5.9 reference | Registry help and conservative reading |
| --- | --- | ---: | --- | --- |
| `r.Shadow.CSMCachingRangeFactor` | float / var | `1.4` | Not located | Multiplies realtime-shadow range to derive clipmap-caching shadow range. A range factor; impact and valid bounds are not documented here. |
| `r.Shadow.CSMCachingUpdateViewTranslationThrottle` | float / var | `0.2` | Not located | Described as the length of view translation for a CSM caching update. Units and exact update rule are unspecified. |
| `r.Shadow.CSMDepthBias` | float / var | `10` | default `10` | Constant depth bias used by cascaded shadow maps (CSM). Depth bias offsets shadow depth comparisons; sign, units, and visible impact depend on the implementation. |
| `r.Shadow.CSMDepthBoundsTest` | int32 / var | `1` | default `1` | Chooses depth-bounds tests instead of stencil tests for CSM bounds, according to help. No guarantee either path is supported by the active renderer. |
| `r.Shadow.CSMReceiverBias` | float / var | `0.9` | default `0.9` | Receiver bias for CSM; help says range 0–1. The help does not define a curve or effect size. |
| `r.Shadow.CSMScissorOptim` | bool / var | `false` | default `false` | Computes an optimized scissor rectangle to exclude CSM slice portions outside the view frustum; describes a rendering optimization. |
| `r.Shadow.CSMScrollingOverlapAreaThrottle` | float / var | `0.75` | default `0.75` | Minimum overlap-area ratio for CSM scrolling. Exact units/algorithm are not specified. |
| `r.Shadow.CSMShadowDistanceFadeoutMultiplier` | float / var | `1` | default `1` | Multiplier for CSM distance fade. A value's visual effect is not established in this game. |
| `r.Shadow.CSMSlopeScaleDepthBias` | float / var | `3` | default `3` | Slope-scaled depth bias used by CSM. Exact scale and artifacts are implementation-dependent. |
| `r.Shadow.CSMSplitPenumbraScale` | float / var | `0.5` | default `0.5` | Scales penumbra size for CSM splits; upstream help says this can help minimize transitions between splits. It does not document a safe range. |
| `r.Shadow.Debug.SortMethod` | int32 / ref | `3` | Not located | Enum in registry help: `0` Number, `1` Memory, `2` Size, `3` DynamicMesh, `4` StaticMesh. The name/help imply a shadow-debug sorting mode, but the exact display it sorts is not stated. |
| `r.Shadow.Denoiser` | int32 / var | `2` | default `2` | Selects denoising algorithm: help lists `0` disabled, `1` renderer default, `2` `GScreenSpaceDenoiser` (possibly overridden by a third-party plugin). These choices are registry help, not proof that the selected denoiser exists in the game build. |
| `r.Shadow.Denoiser.HistoryConvolutionSamples` | int32 / var | `1` | default `1` | Number of samples used to convolve history over time. The exact denoiser stage and quality/performance curve are not specified in the help. |
| `r.Shadow.Denoiser.MaxBatchSize` | int32 / var | `4` | default `4` | Maximum number of shadows denoised at the same time, per registry help. |
| `r.Shadow.Denoiser.PreConvolution` | int32 / var | `1` | default `1` | Number of pre-convolution passes; registry help explicitly says default 1. |
| `r.Shadow.Denoiser.ReconstructionSamples` | int32 / var | `8` | default `8` | Maximum reconstruction-pass samples; registry help says default 16, which differs from the UE 5.9 reference and snapshot value 8. Treat the help's stated default as text from the registry, not a verified game default. |
| `r.Shadow.Denoiser.TemporalAccumulation` | int32 / var | `1` | Not located | No help text in either attachment and no exact UE 5.9 reference match. The name suggests temporal accumulation in shadow denoising, but that interpretation remains an unverified inference. |
| `r.Shadow.DetectVertexShaderLayerAtRuntime` | int32 / var | `1` | default `1` | Help says to force compilation of the vertex-shader-layer permutation even when the RHI does not declare compile-time support; it notes Windows/SM5 defaults enabled because DX11 commonly supports it at runtime. Primarily a shader capability/compilation control, not a general visual-quality slider. |
| `r.Shadow.DisableNeverDinstanceCull` | int32 / var | `1` | Not located | Registry help is blank. The misspelled `Dinstance` is part of the exact registered name; its apparent intent cannot be established from the name alone. |
| `r.Shadow.DistanceFadeExponent` | float / var | `0.25` | Not located | Controls the rate at which whole-scene shadows fade out with distance. No scale, limits, or perceptual mapping are given. |
| `r.Shadow.DistanceScale` | float / var | `1` | default `1` | Directional-light shadow-distance scalability control, clamped to a reasonable range. Registry help says below 1 shortens distance, 1 is normal, and above 1 increases it. This is the clearest documented distance/quality-versus-performance control in this set. |
| `r.Shadow.DrawPreshadowFrustums` | int32 / var | `0` | default `0` | Visualizes preshadow frustums when the `shadowfrustums` show flag is enabled; a debug visualization. |
| `r.Shadow.EnableMaskBox` | int32 / var | `1` | Not located | Help says it enables a mask box for shadow projection. Exact semantics and visual/performance effects are unspecified. |
| `r.Shadow.EnableMaskBoxCulling` | int32 / var | `1` | Not located | Help lists `0` as shadow-frustum culling only and `1` as shadow-frustum plus mask-box-frustum culling. This describes a culling-path switch; no speedup or correctness result has been measured. |
| `r.Shadow.EnableModulatedSelfShadow` | int32 / var | `0` | default `0` | Allows modulated shadows to affect the shadow caster; registry and UE help qualify it as mobile-only. Relevance on the Windows PC build is unproven. |

## Practical grouping

- **CSM bias and split appearance:** `CSMDepthBias`, `CSMReceiverBias`, `CSMSlopeScaleDepthBias`, `CSMSplitPenumbraScale`, and `CSMShadowDistanceFadeoutMultiplier` describe depth comparison, receiver, slope, split penumbra, or fade parameters. Their registry values match the published UE 5.9 defaults in this set; this is not evidence those are Marvel's live defaults.
- **CSM cache and bounds work:** `CSMCachingRangeFactor`, `CSMCachingUpdateViewTranslationThrottle`, `CSMScrollingOverlapAreaThrottle`, `CSMDepthBoundsTest`, and `CSMScissorOptim` describe cache/update or bounds/scissor behavior. Two cache-specific names are absent from the UE 5.9 reference and may be fork-specific or version-specific.
- **Denoising:** `Denoiser`, `Denoiser.HistoryConvolutionSamples`, `Denoiser.MaxBatchSize`, `Denoiser.PreConvolution`, `Denoiser.ReconstructionSamples`, and `Denoiser.TemporalAccumulation` describe denoiser selection/work parameters. No benchmark establishes that changing sample counts improves image quality or performance in Marvel Rivals. The reconstruction help/default mismatch above should be retained when evaluating proposals.
- **Distance, culling, and diagnostics:** `DistanceScale` and `DistanceFadeExponent` concern distance behavior; `EnableMaskBox` and `EnableMaskBoxCulling` concern mask-box/culling paths; `Debug.SortMethod` and `DrawPreshadowFrustums` are diagnostic by their names/help. `DetectVertexShaderLayerAtRuntime` concerns shader capability compilation. `DisableNeverDinstanceCull` remains undefined from available evidence.

## Loader and runtime status

To propose an override in the supplied loader, use an uncommented line under the real `[Overrides]` section, for example `r.Shadow.DistanceScale=0.9`. This only exercises the loader's documented config merge path. It does not demonstrate that this CVar is registered or mutable at startup, that a renderer consumes it, or that the requested value survives clamping/platform gates. None of the 25 has been experimentally changed and compared in-game as part of this page. Avoid treating the snapshot as a preset: it is a capture whose game build and capture conditions are unknown.
