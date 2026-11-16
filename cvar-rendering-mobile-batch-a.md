# Mobile-rendering CVars batch A

This page covers 25 exact `r.Mobile.*` names in the preserved community registry. All 25 rows are `kind=var`; 23 are `int32` and two are `bool`. The community table has an exact-name Unreal Engine 5.9 reference entry for each. UE 5.9 meanings/defaults are upstream context, not proof that Marvel Rivals uses the same engine implementation or honors a value.

## Names, captured values, and meanings

The `CVarDump.txt` column is a captured value, not a verified game default or recommendation. The `UE 5.9` column comes from the exact-name match in the generated registry catalog. Community help remains the primary plain-language description for this batch.

| Exact CVar | Type | Snapshot | UE 5.9 default | Community help, summarized |
| --- | --- | ---: | ---: | --- |
| `r.Mobile.AdrenoOcclusionMode` | int32 | `0` | `0` | `0` runs occlusion queries after the base pass; `1` moves them until after translucency and a flush, which help says can help Adreno devices in GL mode. |
| `r.Mobile.AllowDeferredShadingOpenGL` | int32 | `0` | `0` | Allows mobile deferred shading on OpenGL when enabled. |
| `r.Mobile.AllowDistanceFieldShadows` | int32 | `1` | `1` | Controls shader-permutation generation for distance-field shadows from stationary directional lights. |
| `r.Mobile.AllowDitheredLODTransition` | int32 | `0` | `0` | Controls support for the material “Dithered LOD Transition” option on mobile. |
| `r.Mobile.AllowMovableDirectionalLights` | int32 | `1` | `1` | Controls shader-permutation generation for movable directional lights on mobile. |
| `r.Mobile.AllowPerPixelShadingModels` | int32 | `1` | `1` | Allows per-pixel shading models selected from a material expression at the mobile feature level. |
| `r.Mobile.AllowPixelDepthOffset` | int32 | `1` | `1` | Allows Pixel Depth Offset in mobile materials; help warns pixel-shader depth modification may reduce GPU performance. |
| `r.Mobile.AmbientOcclusion` | int32 | `0` | `0` | Enables mobile ambient occlusion. Help warns it consumes an extra sampler in the mobile base-pass pixel shader. |
| `r.Mobile.AmbientOcclusionDepthBoundsTest` | int32 | `1` | `1` | Uses depth-bounds testing to cull distant AO pixels; help says it applies only to the pixel-shader path. |
| `r.Mobile.AmbientOcclusionQuality` | int32 | `1` | `1` | Mobile screen-space AO quality: `0` disabled, `1` low, `2` medium, `3` high. |
| `r.Mobile.AmbientOcclusionShaderType` | int32 | `2` | `2` | Selects an AO shader type: `0` compute, `1` separate compute, `2` pixel. |
| `r.Mobile.AmbientOcclusionTechnique` | int32 | `0` | `0` | Selects `0` GTAO or `1` SSAO. |
| `r.Mobile.AntiAliasing` | int32 | `1` | `1` | Mobile AA method: `0` off, `1` FXAA, `2` Temporal AA (may fall back to FXAA depending on `r.Mobile.SupportsGen4TAA`), `3` MSAA. |
| `r.Mobile.CustomDepthForTranslucency` | int32 | `1` | `1` | Renders custom depth/stencil when translucency in the scene uses it. |
| `r.Mobile.DesiredResX` | int32 | `0` | `0` | Desired mobile X resolution on the longest axis; nonzero sets X and derives Y to preserve aspect ratio. |
| `r.Mobile.DesiredResY` | int32 | `0` | `0` | Desired mobile Y resolution on the shortest axis; nonzero sets Y and derives X to preserve aspect ratio. |
| `r.Mobile.DisableVertexFog` | int32 | `1` | `1` | When enabled, omits vertex fog from most mobile base-pass shaders; fog is applied in a separate pass when the scene has a fog component. |
| `r.Mobile.EarlyZPass` | int32 | `0` | `0` | Controls a depth-only pass before the mobile base pass: `0` off, `1` all opaque, `2` masked only. Help says changing it requires restarting the editor. |
| `r.Mobile.EnableCloth` | bool | `true` | `true` | Controls compiling cloth shader permutations and rendering simulated cloth on mobile and Mobile mode on PC. Help says it cannot be changed at runtime. |
| `r.Mobile.EnableMovableLightCSMShaderCulling` | int32 | `1` | `1` | `0` gives CSM to all primitives lit by a movable directional light; `1` selects the CSM shader when a primitive is determined to be within CSM range. |
| `r.Mobile.EnableMovableSpotlightsShadow` | int32 | `0` | `0` | Enables movable spotlight-shadow support when set to `1`. |
| `r.Mobile.EnableNoPrecomputedLightingCSMShader` | int32 | `0` | `1` | Controls generation of CSM shaders for scenes without precomputed lighting. The captured value differs from the UE 5.9 reference default; neither establishes the current Marvel Rivals value. |
| `r.Mobile.EnableOcclusionExtraFrame` | bool | `true` | `true` | Allows an extra frame for occlusion culling; community help says enabled by default. |
| `r.Mobile.EnableStaticAndCSMShadowReceivers` | int32 | `1` | `1` | `0` lets primitives receive only static shadowing from stationary lights; `1` allows both CSM and static shadowing. |
| `r.Mobile.EyeAdaptation` | int32 | `1` | `1` | Enables mobile eye adaptation when set to `1`; `0` disables it. |

## Installed-build evidence and limits

All 25 entries have `ref_rva=0` in the community table. The saved address scan matched `obj_rva` address/setup references for each, including address-taking (`lea`) and memory-write candidates. It found no direct CVar-value reads at a `ref_rva` for these names. This is not evidence that the variables are unused: this registry family has no `ref_rva` lead to scan, and indirect access, code in other modules, or the mobile rendering path may not be covered. The installed Windows Shipping executable is build `1.1.4042190`; the community registry's build is unknown.

These names describe mobile-renderer features. Their presence in the community table and upstream UE 5.9 does not show that the current Windows game uses the mobile renderer or executes these settings' paths. The snapshot is not a report of the current live value in build `1.1.4042190`.

## Loader syntax is not runtime editability

The supplied `[Overrides]` format can express lines such as `r.Mobile.AmbientOcclusionQuality=2`, but this establishes syntax only. There is no controlled runtime test here showing that the current game accepts these values, that their initialization timing permits changes, or that they affect a path the Windows client uses. In particular, the `EnableCloth` help explicitly says it cannot be changed at runtime; that source statement does not independently settle whether a startup config can select it in this build. Follow the shared [CVar editability evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) before treating an override as usable.

## Sources

- Names, types, community help, and RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Snapshot values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Epic 5.9 exact-name match status and defaults: [community registry](cvar-community-registry.md).
- Local address candidates and scan scope: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and [CVar source notes](EVIDENCE.md#build-specific-static-analysis).
- Official upstream reference: [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference).
