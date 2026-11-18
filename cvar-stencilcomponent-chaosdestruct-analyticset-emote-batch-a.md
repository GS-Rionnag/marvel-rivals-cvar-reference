# StencilComponent, ChaosDestruct, AnalyticsET, and Emote CVars

This guide covers all 21 exact-case registry variables in these four namespaces. Snapshot values are observations from an unspecified capture build. A dash means the snapshot has no entry for the variable.

## StencilComponent

| Exact name | Type / kind | Snapshot | Meaning and limits |
| --- | --- | --- | --- |
| `StencilComponent.DebugEnable` | `bool` / `var` | `false` | No help. The name suggests a debug switch with unspecified output. |
| `StencilComponent.EnableOutline` | `bool` / `var` | `true` | Enables outlines. The help leaves the affected objects unspecified. |
| `StencilComponent.EnemyOnly` | `bool` / `ref` | — | The help lists `0` as the original mode and stated default and `1` as enemy-only outlines and fills. It describes skipping non-enemy visibility traces and transparent outline placeholders while preserving other CustomDepth users. It specifies selection before match entry and says live switching is unsupported. |
| `StencilComponent.OptimizeFillColorPass` | `bool` / `var` | `true` | Translated help says it disables the fill placeholder when no fill effect is active. |
| `StencilComponent.OverrideDitheringSortIndex` | `int32` / `var` | `0` | No help. The name suggests a dithering sort-index override with unspecified range and zero behavior. |
| `StencilComponent.PixelationPPThreshold` | `float` / `ref` | `1` | Translated help says pixelation post-processing is disabled when the nearest stencil component's `DitheringOpacity` exceeds this threshold. |

The two translated descriptions use the repository's English renderings of the supplied Chinese help. [Help translation catalog](EVIDENCE.md#community-sources)

## ChaosDestruct

| Exact name | Type / kind | Snapshot | Meaning and limits |
| --- | --- | --- | --- |
| `ChaosDestruct.BanLoopFieldActor` | `bool` / `ref` | `false` | Help says “ban loop field.” The scope and affected actors are unspecified. |
| `ChaosDestruct.ForceBanApplyField` | `bool` / `ref` | `false` | No help. The name suggests a forced block on field application. |
| `ChaosDestruct.bCanBeatClientGC` | `bool` / `var` | `true` | Help is the fragment `ForceEnablePerfor`. The name suggests a client GC setting with unspecified behavior. |
| `ChaosDestruct.bEnableAliveStage` | `bool` / `var` | `false` | Help says `EnableAliveStage`, without defining that stage. |
| `ChaosDestruct.bForceOpenDamage` | `bool` / `var` | `false` | The name mentions damage and the help says `ForceEnableAlive`. The relationship between these terms is unclear. |
| `ChaosDestruct.bOpenOneBeatGC` | `bool` / `var` | `true` | Help is the fragment `ForceEnablePerfor`. The name suggests a GC setting with unspecified behavior. |

## AnalyticsET

| Exact name | Type / kind | Snapshot | Meaning from supplied help |
| --- | --- | --- | --- |
| `AnalyticsET.PayloadFlushTimeSecForWarning` | `float` / `ref` | `0.001` | EventCache flush-duration warning threshold in seconds. The warning lists events in the payload. |
| `AnalyticsET.PayloadPercentageOfMaxForWarning` | `float` / `ref` | `1` | Warns and lists payload events when the payload reaches a threshold relative to the EventCache maximum size. The help describes a percentage and leaves the numeric scale unspecified. |
| `AnalyticsET.PreventMultipleFlushesInOneFrame` | `bool` / `ref` | `true` | When enabled, lets at most one AnalyticsProviderET instance flush in a frame to spread flush and HTTP work. |
| `AnalyticsET.UserAgentCommentsEnabled` | `bool` / `var` | `true` | Controls support for comments in the analytics user-agent string. |

## Emote

| Exact name | Type / kind | Snapshot | Meaning and limits |
| --- | --- | --- | --- |
| `Emote.Cache.MaxCount` | `int32` / `var` | `16` | Maximum resident emote cache entries when on-demand loading is enabled. `0` disables the resident cache. |
| `Emote.LoadAssetsOnDemand` | `int32` / `var` | `1` | A positive value excludes emote assets from hero packs and loads them just before play. The help lists startup arguments `-EmoteLoadAssetsOnDemand`, `-EmoteLoadAssetsOnDemand=0/1`, and `-NoEmoteLoadAssetsOnDemand`. Their behavior in the scanned build remains unverified. |
| `Emote.PreservePresentationOnFreeze` | `int32` / `var` | — | Preserves the presentation of an interrupted emote while frozen at `1`, the stated default. `0` selects legacy behavior. The help says the value is sampled on freeze entry, existing captures are cleaned up on thaw, and server-side disablement applies to all clients. |
| `Emote.PrewarmEquipped` | `int32` / `var` | `0` | With on-demand loading enabled, a positive value prewarms locally equipped emotes after begin play. |
| `Emote.VolleyBall.CheckDistance` | `int32` / `var` | `1` | No help. The name suggests a volleyball-emote distance check with unverified value semantics. |

## Build and source evidence

- All 21 names appear in both Shipping string inventories for build 1.1.4042190. The four AnalyticsET names also appear in Crash Report Client and have exact-name UE 5.9 reference matches in the community catalog. [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Community registry](EVIDENCE.md#community-sources)
- Each name has one address-taking instruction against `obj_rva` in the x64 scan. The same field has three direct-memory candidates per variable, with two for each AnalyticsET variable, `Emote.VolleyBall.CheckDistance`, and `StencilComponent.PixelationPPThreshold`, and four for `StencilComponent.EnableOutline`. Each `ref` has one address-taking instruction and one direct-memory candidate against `ref_rva`, with five direct-memory candidates for `StencilComponent.EnemyOnly`. [Address-reference scan](EVIDENCE.md#build-specific-static-analysis)
- The snapshot observations, stated defaults, and static hits leave installed-build behavior and startup override support unverified. [Raw registry](EVIDENCE.md#community-sources) · [Raw snapshot](EVIDENCE.md#community-sources) · [Source notes](EVIDENCE.md#community-sources)
