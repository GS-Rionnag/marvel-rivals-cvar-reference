# Rendering shadow CVar batch C

This page documents the next 25 uncovered `r.Shadow.*` names in the community registry. The registry's help and captured values are evidence from an attachment with unknown game build and collection method; snapshot values are not verified defaults. Where an exact name appears in Epic's UE 5.9 reference, that description is upstream context, not proof that Marvel Rivals uses the same implementation.

The saved address scan targets Marvel Rivals Shipping build `1.1.4042190`. A direct `ref_rva` candidate is a static instruction-level access to the registry's recorded value address. It does not prove that the path executes in a match, that an `.ini` override is accepted, or that changing the value has the effect suggested by its help.

## Distance-fade controls

| Exact CVar | Type / kind | Snapshot | UE 5.9 reference | What the evidence supports |
| --- | --- | ---: | --- | --- |
| `r.Shadow.EnablePerObjectShadowDistanceFade` | int32 / ref | `1` | No exact match | Community help says this controls distance fading for per-object shadows. The local scan has one direct zero-comparison candidate and one address-taking reference; this supports a value check but not the fade formula or affected object classes. |
| `r.Shadow.EnablePerObjectShadowDistanceFade.Channel0` | int32 / ref | `1` | No exact match | Help applies per-object-shadow distance fading to lighting channel 0. The scan has one direct compare candidate plus an address-taking reference. The channel mask's broader semantics are not described. |
| `r.Shadow.EnablePerObjectShadowDistanceFade.Channel1` | int32 / ref | `1` | No exact match | Help applies per-object-shadow distance fading to lighting channel 1. A direct load candidate and an address-taking reference were found; how the loaded value gates rendering was not traced. |
| `r.Shadow.EnablePerObjectShadowDistanceFade.Channel2` | int32 / ref | `1` | No exact match | Help applies per-object-shadow distance fading to lighting channel 2. A direct load candidate and an address-taking reference were found; no other channel values are documented here. |
| `r.Shadow.EnableShadowDistanceFade` | int32 / ref | `1` | No exact match | Community help says this controls distance fading for whole-scene shadows. One direct zero-comparison candidate reads the registered value. The fade threshold and curve are separate controls or implementation details not established by this entry. |
| `r.Shadow.EnableShadowDistanceFade.Channel0` | int32 / ref | `1` | No exact match | Help scopes whole-scene-shadow distance fading to lighting channel 0. One direct compare candidate and an address-taking reference were found. The interaction with the parent switch was not reconstructed. |
| `r.Shadow.EnableShadowDistanceFade.Channel1` | int32 / ref | `1` | No exact match | Help scopes whole-scene-shadow distance fading to lighting channel 1. One direct load candidate and an address-taking reference were found; downstream behavior is unknown. |
| `r.Shadow.EnableShadowDistanceFade.Channel2` | int32 / ref | `1` | No exact match | Help scopes whole-scene-shadow distance fading to lighting channel 2. One direct load candidate and an address-taking reference were found; downstream behavior is unknown. |
| `r.Shadow.FadeDistance` | float / var | `0` | No exact match | Registry help says whole-scene shadows are faded below this distance. It gives no units, curve, or special meaning for the captured `0`; the saved scan has no direct value-read candidate. |
| `r.Shadow.FadeResolution` | int32 / var | `64` | Default `64` | Help says shadows are faded out below this resolution in texels. The exact boundary rule and whether this is resolution before or after scaling are unspecified. No direct value-read candidate was found. |

The eight enable entries are related by their source descriptions, but the scan alone does not establish whether channel-specific values override, refine, or combine with the parent switch. Treat each as a separate candidate rather than assuming that setting all channel values has a known combined result.

## CSM, filter, and mask-box controls

| Exact CVar | Type / kind | Snapshot | UE 5.9 reference | What the evidence supports |
| --- | --- | ---: | --- | --- |
| `r.Shadow.ExtraCSMHeight` | float / var | `2000` | No exact match | No help is supplied. The name suggests additional height related to cascaded shadow maps (CSM), but does not identify the measurement, affected cascade, or effect. No direct value-read candidate was found. |
| `r.Shadow.FilterMethod` | int32 / var | `0` | No exact match | Help maps `0` to Uniform PCF (stated default) and `1` to experimental PCSS. Other values and whether both implementations are present in the shipping build are unspecified. No direct value-read candidate was found. |
| `r.Shadow.FixMaskBoxShadowBug` | bool / ref | `true` | No exact match | Help describes removing stencil clears between shadow projections by zeroing stencil during testing. The local scan contains one byte-comparison candidate and one address-taking reference. This shows a value check in the binary, not that the stated fix is active or visually beneficial. |
| `r.Shadow.ForceSerialSingleRenderPass` | int32 / var | `0` | Default `0` | Registry help says it forces serial shadow passes to render in one pass. The help does not explain which pass sequence is changed or what zero does. No direct value-read candidate was found. |
| `r.Shadow.ForceSingleSampleShadowingFromStationary` | int32 / var | `0` | Default `0` | Help says it makes components behave as though `bSingleSampleShadowFromStationaryLights` were enabled, and calls this useful for scalability when dynamic shadows are disabled. It does not describe the visual tradeoff or component filtering. No direct value-read candidate was found. |
| `r.Shadow.IgnoreNaniteShadowByLightChannels` | int32 / ref | `2` | No exact match | Registry help expresses a three-channel bit mask: `(Channel0 ? 1 : 0) | (Channel1 << 1) | (Channel2 << 2)`. The name suggests which channels are ignored for Nanite shadows, but the mask's behavior and accepted bits are not independently confirmed. One direct compare candidate and one address-taking reference were found. |
| `r.Shadow.MaskBoxShadowMapRange` | float / ref | `8000` | No exact match | Help is only “MaskBox ShadowMap Range before sdf-shadow”; it does not define units, what “before” means, or the SDF path. The scan has one direct float-load candidate and one address-taking reference, confirming a value access candidate but not its role. |

## Directional and local-light limits

| Exact CVar | Type / kind | Snapshot | UE 5.9 reference | What the evidence supports |
| --- | --- | ---: | --- | --- |
| `r.Shadow.FarShadowDistanceOverride` | float / var | `0` | Default `0` | Help describes an override of the far-shadow distance for all directional lights. The zero value's exact sentinel behavior is not stated. No direct value-read candidate was found. |
| `r.Shadow.FarShadowStaticMeshLODBias` | int32 / ref | `0` | Default `0` | Help warns that only selected geometry types—static meshes and landscapes—respect this bias. Five direct memory candidates and one address-taking reference target its registered value. The LOD arithmetic and visible result were not traced. |
| `r.Shadow.MaxCSMScrollingStaticShadowSubjects` | int32 / var | `5` | Default `5` | Help calls this the maximum number of extra static shadow subjects drawn when scrolling CSM. No direct value-read candidate was found; the scheduling path and behavior at the limit remain unverified. |
| `r.Shadow.MaxDistance` | float / var | `0` | No exact match | Help says this is the maximum distance for rendering whole-scene shadow depths. Units, zero behavior, light types, and clamping are not given. No direct value-read candidate was found. |
| `r.Shadow.MaxLightRadiusForScalableLocalLightShadow` | float / ref | `1` | No exact match | The registry's help is `None`. The name hints at a light-radius threshold for scalable local-light shadows, but that is not a confirmed definition. The scan found an address-taking reference but no direct value-read candidate. |
| `r.Shadow.MaxNumFarShadowCascades` | int32 / var | `10` | Default `10` | Help sets the maximum number of far-shadow cascades a directional light can cast. The local scan found no direct value-read candidate; the relationship to other cascade limits is not described. |
| `r.Shadow.MaxNumPointShadowCacheUpdatesPerFrame` | int32 / ref | `-1` | Default `-1` | Help limits per-frame point-light shadow-cache updates caused by resolution changes; `-1` means no limit. Two direct load candidates and one address-taking reference were found. The policy for other update causes was not recovered. |
| `r.Shadow.MaxNumSpotShadowCacheUpdatesPerFrame` | int32 / ref | `-1` | Default `-1` | Help gives the corresponding per-frame limit for spot-light shadow-cache updates caused by resolution changes; `-1` means no limit. Two direct load candidates and one address-taking reference were found. The update queue and behavior for other causes were not traced. |

## What this establishes about overrides

The community registry labels these rows `var` or `ref`, and its snapshot records the values shown above. Those labels and values do not prove that a startup `.ini` line is accepted, survives later configuration layers, or changes a live renderer path. The eight channel fade controls, the mask-box bug switch, the Nanite-channel mask, the mask-box range, the static-mesh LOD bias, and the point/spot cache limits have direct value-access candidates in the scanned build. The other names have no direct `ref_rva` candidate in this scan; that absence does not prove they are unused because indirect accesses or other modules may be out of scope.

No controlled override or in-game visual/performance comparison was performed for this batch. The snapshot is not a preset. In particular, `FadeDistance=0` and `MaxDistance=0` have no established zero semantics here, while the two cache-update values of `-1` are described by source help as unlimited.

## Sources and related guides

- Registry type, help, and reference addresses: [community registry attachment](EVIDENCE.md); captured values: [community snapshot attachment](EVIDENCE.md).
- Exact-name UE 5.9 matches and descriptions: [community registry](cvar-community-registry.md) and [Epic's Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference).
- Static value-address candidates: [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis). See [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis) for scanner semantics and limitations.
- Related shadow controls: [shadow batch A](cvar-rendering-shadow-batch-a.md), [shadow batch B](cvar-rendering-shadow-batch-b.md), [dynamic-page VSM controls](cvar-dynamic-page-vsm.md), [bone-reduction controls](cvar-bone-reduction.md), and [CVar override research](cvar-overrides.md).
