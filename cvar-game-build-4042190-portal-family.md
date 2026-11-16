# Marvel Rivals `m.Portal.*` candidates in build 4042190

This guide records all 74 `m.Portal.*` name candidates found in the x64 Shipping executable in build `1.1.4042190`. Descriptions below summarize printable text close to each name in the executable and, where text is absent, identify what remains unknown. The nearby-text pairing is inferred from static data layout; it has not yet been confirmed with Ghidra cross-references or a runtime CVar registry dump. The [raw nearby-text index](EVIDENCE.md#build-specific-static-analysis) preserves the offsets and strings.

These entries belong to a portal/scene-capture renderer, but some affect camera, character translation, projectiles, or portal collision. Do not treat every candidate as a rendering-only switch, and do not infer that a name is registered or accepted by the loader merely because it is embedded in the binary.

## Portal visibility, selection, and capture

| Candidate | Embedded help / current interpretation |
| --- | --- |
| `m.Portal.CVarCollisionMeshSingleSideToAbilityChannel_S3_1_0717` | No useful nearby help recovered. The name suggests an ability-channel collision-mesh rule; exact behavior is unknown. |
| `m.Portal.CVarIgnorePortalBehindActor` | No help recovered; likely a portal visibility or actor-occlusion rule based on the name. |
| `m.Portal.CVarPortalEndByLevelPenetrationRefreshCD` | No help recovered; exact meaning and units unknown. |
| `m.Portal.CVarPortalServerTranslateTolerance` | No help recovered; name suggests a server-side portal translation tolerance. Unit and behavior are unknown. |
| `m.Portal.CVarPortalTranslateBoundMeshCheck` | No help recovered; name suggests a bound-mesh check during portal translation. |
| `m.Portal.CVarTerrainDamageToEnergyChange_S2_2` | No help recovered; ability-specific name appears gameplay-related, not general rendering. |
| `m.Portal.CapsuleTraceMultiplier` | Nearby help calls this a multiplier for the character capsule trace during translation. Range/default unknown. |
| `m.Portal.Check.DeltaCount` | Nearby text associates it with a `TranslateActor` check; numeric meaning/default unknown. |
| `m.Portal.Check.Distance` | Nearby text associates it with checking the distance between an actor's location and the portal location. |
| `m.Portal.Check.Ensure` | Nearby text associates it with an ensure/check for the actor-to-portal location difference. |
| `m.Portal.Check.MinLimit` | Nearby text associates it with `TranslateActor` location checks; the threshold's unit and default are unknown. |
| `m.Portal.ClipPlaneCulling` | Enables portal clip-plane culling. |
| `m.Portal.ClipPlaneOffset` | No useful nearby help recovered; likely a clip-plane offset, but units and sign are unknown. |
| `m.Portal.ControlAimFallback` | After a local player is translated through a portal, uses control aim until the next camera update. Disabling it prevents new fallback windows. This can affect aim/camera behavior. |
| `m.Portal.CustomBlockDistanceWeight` | Scales camera-to-portal distance when custom weighting is used. |
| `m.Portal.DebugBlocked` | Shows which portal is blocked and why; debug output. |
| `m.Portal.DisableBlockTexture` | Makes a blocked portal display as black. |
| `m.Portal.EnableReplaySubsystem` | No useful nearby help recovered; exact replay behavior is unknown. |
| `m.Portal.FilterSimulatedProjectile` | Nearby help describes whether to filter simulated projectiles through portals. This can affect projectile behavior. |
| `m.Portal.HidePortalMesh` | Hides the portal mesh. |
| `m.Portal.HighRenderQuality` | No useful nearby help recovered; exact quality settings are unknown. |
| `m.Portal.LevelPortalViewDistanceExtent` | Portal-view distance extent in centimeters. |
| `m.Portal.OcclusionDrivenSceneCapture` | Enables an occlusion-test-driven scene capture. |
| `m.Portal.OcclusionDrivenSceneCaptureFrameGap` | Frame gap for the occlusion test that drives scene capture; exact default and range unknown. |
| `m.Portal.OverrideBlockByCount` | Overrides portal-block selection by count. The count and selection rule are unknown. |
| `m.Portal.OverrideBlockByDistance` | Overrides portal-block selection by distance, in meters according to nearby help. |
| `m.Portal.OverrideBlockByFacingPortal` | Overrides portal-block selection based on facing a portal. |
| `m.Portal.OverrideBlockDistanceWeight` | Custom weighted distance used for sorting. Nearby help says weights can favor the area the mouse points toward; farther weight details are not stated. |
| `m.Portal.PortalSphereTraceCheckRadius` | Custom sphere-trace check radius; unit/default unknown. |
| `m.Portal.ProjectionCulling` | Enables portal projection culling. |
| `m.Portal.RenderWithPostProcess` | Nearby text says `0` follows the SceneCapture setting and `1` keeps post-processing off. The printed help is terse, so verify behavior in the current build before overriding. |
| `m.Portal.Scalability` | Controls whether portal scalability is enabled; exact scalability levels and default unknown. |
| `m.Portal.Scissor.DrawThreshold` | No useful nearby help recovered; exact scissor draw threshold is unknown. |
| `m.Portal.ScreenPercentageAdjustEnable` | Enables portal control of screen percentage. |
| `m.Portal.ScreenPercentageLowerLimit` | Lower limit for the player-resolution change associated with portals; exact units/range unknown. |
| `m.Portal.SupportStaticLevelPortal` | No useful nearby help recovered; support conditions are unknown. |
| `m.Portal.TestBlocked` | Forces all portals to be treated as blocked; appears to be a test/debug switch. |
| `m.Portal.TwoSide` | Controls whether a portal has two-sided effects. |
| `m.Portal.UseUserOcclusionQuery` | Uses a GPU occlusion query (`bUserIssueOcclusionQuery`) instead of main-view `LastRenderTimeOnScreen` to cull portal visibility. This is a rendering/performance tradeoff. |
| `m.Portal.UseViewport` | Scene-capture post-processing policy: `0` disables all, `1` enables on demand, `2` enables all. |
| `m.Portal.ViewTemporalAAIndexOverrideByView0` | Name suggests an override of the temporal-AA index by view 0; no explanatory help or value range recovered. |

## Portal rendering quality and budgets

| Candidate | Embedded help / current interpretation |
| --- | --- |
| `m.Portal.CrossFrameBudget.GlobalDistanceField` | Nearby help identifies the Global Distance Field render start time for portal cross-frame budgeting. Time unit/default unknown. |
| `m.Portal.CrossFrameBudget.Lumen` | Nearby help identifies Lumen's render start time for portal cross-frame budgeting. |
| `m.Portal.CrossFrameBudget.Shadow` | Nearby help identifies shadow render start time for portal cross-frame budgeting. |
| `m.Portal.CrossFrameBudget.TranslucentVolume` | Nearby help identifies translucent-volume render start time for portal cross-frame budgeting. |
| `m.Portal.CrossFrameBudget.ViewDistanceScale` | Portal view-distance scale by frame count; nearby help notes values greater than `1.0`. |
| `m.Portal.CrossFrameBudget.VolumetricFog` | Nearby help identifies volumetric-fog render start time for portal cross-frame budgeting. |
| `m.Portal.DisableDistanceFieldShadow` | Disables distance-field shadows in portals. |
| `m.Portal.DisableSandboxStencilPassMerge` | Name and nearby text say it disables the sandbox stencil-pass merge; exact render-path consequences are unknown. |
| `m.Portal.EnablePortalPrefersPerformance` | Nearby value text: `-1` means do not override (default), `0` force off, `1` force on. The feature being preferred is not identified in the adjacent text. |
| `m.Portal.EnableSkyPassStencil` | Controls whether portals use the sky-pass stencil test. |
| `m.Portal.GlobalDistanceFieldUseLumenParam` | Uses the portal view's Lumen parameter for the Global Distance Field. |
| `m.Portal.Lumen.DiffuseIndirect` | Portal diffuse-indirect mode: `0` keeps Lumen, `1` uses SSGI, `2` disables the contribution. |
| `m.Portal.Lumen.Reflection` | Portal reflection mode: `0` keeps Lumen, `1` uses SSR, `2` disables reflections. |
| `m.Portal.Lumen.RadianceCache.UpdateSlow` | Controls slow radiance-cache updates for portal views; adjacent help only describes it as whether to update radiance slowly. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowDistance` | Distance input for slow portal radiance-cache updates; formula/range unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowDistanceFalloff` | Distance-falloff input for slow portal radiance-cache updates; formula/range unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowEnd` | End parameter for slow portal radiance-cache updates; formula/unit unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowPeriod` | Period parameter for slow portal radiance-cache updates; unit/default unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowPeriodMin` | Minimum period parameter for slow portal radiance-cache updates; unit/default unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowSize` | Size parameter for slow portal radiance-cache updates; unit/default unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowSizeFalloff` | Size-falloff parameter for slow portal radiance-cache updates; formula/default unknown. |
| `m.Portal.Lumen.RadianceCache.UpdateSlowStart` | Start parameter for slow portal radiance-cache updates; formula/unit unknown. |
| `m.Portal.Lumen.ScreenProbeSkip` | Nearby help describes skipping Lumen probe placement on portal-mesh areas. |
| `m.Portal.LumenScene.DetailScale` | Portal-view Lumen scene detail scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.LumenScene.LightingQualityScale` | Portal-view Lumen lighting-quality scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.LumenScene.LightingUpdateSpeedScale` | Portal-view Lumen lighting-update-speed scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.LumenScene.NumberOfMeshCardThresholdScale` | Portal-view Lumen mesh-card threshold scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.LumenScene.NumberOfSkipFramesScale` | Portal-view Lumen skipped-frame scale, automatically clamped to `[1.0, 10.0]`. |
| `m.Portal.LumenScene.SurfaceCacheResolutionScale` | Portal-view Lumen surface-cache resolution scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.LumenScene.ViewDistanceScale` | Portal-view Lumen scene view-distance scale, automatically clamped to `[0.1, 1.0]`. |
| `m.Portal.MaxViewDistanceOverride` | Portal-view maximum distance in centimeters. |
| `m.Portal.ResolutionRatio` | Ratio used to change player resolution when a portal opens; exact formula/default unknown. |
| `m.Portal.SSAO.Combined` | Nearby help says `1` turns combined SSAO on (default); behavior of other values is unstated. |

## Practical limits

All 74 names are present as strings in the Shipping executable; this does not prove that every one is a registered console variable, accepted by override loader, or safe to change in a live match. The help text is recovered from nearby binary strings, not confirmed with Ghidra references. The numeric behavior above is only recorded where nearby text explicitly states values/ranges. For settings affecting translation, aim, projectile filtering, portal visibility, or scene capture, use a controlled private-range comparison and restore the original config after the test.
