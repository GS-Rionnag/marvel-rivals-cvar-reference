# WidgetComponent CVar batch A

This guide covers all 10 currently uncovered exact-case `WidgetComponent.*` entries. Their supplied descriptions include render-target dimension caps, an occlusion-bounds adjustment, modulo-based refresh selection, and a default tick-mode switch. Several names have no useful help. The registry and snapshot do not establish that the installed game's widget components use the same code paths or defaults.

Only three entries have exact-name Epic UE 5.9 matches. Static scan counts below match registry address fields against the local Shipping binary; direct-memory candidates do not prove access direction or execution. Nearby strings in the build-context inventory are not proof of code relationships. No loader override or runtime test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `WidgetComponent.DumpStats` | `bool` (`var`) | `false` | — | No useful supplied help or exact-name Epic description; the name alone does not specify what statistics are dumped or when. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.EnableParallelTick` | `int32` (`ref`) | `1` | — | No useful supplied help or exact-name Epic description; accepted values and which work is parallelized are unknown. | `ref_rva`: 3 direct-memory candidates and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.ForceRunOnAnyThread` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; which callback/task is affected and its thread-safety requirements are unknown. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.MaximumRenderTargetHeight` | `int32` (`ref`) | `2160` | `2160` | Community and Epic help: maximum height for a Widget Component's render target. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.MaximumRenderTargetWidth` | `int32` (`ref`) | `3840` | `3840` | Community and Epic help: maximum width for a Widget Component's render target. | `ref_rva`: no direct-memory candidate; 2 address-taking references. `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.OcclusionScaleExtention` | `float` (`ref`) | `5` | — | Supplied help: enlarge the UI widget's bounding box to address incorrect occlusion tests with materials using `WorldPositionOffset`. The exact scale calculation is unspecified; registry spelling `Extention` is preserved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.PrintTick` | `bool` (`var`) | `false` | — | No useful supplied help; exact logging content and scope are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.ReMountWidgetOnHUDReady` | `bool` (`var`) | `true` | — | No useful supplied help or exact-name Epic description; the name does not define which widget is remounted or which HUD-ready event applies. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.RefreshModulo` | `int32` (`ref`) | `0` | — | Supplied help: refresh a widget component when `(FrameNumber % Modulo) == (ComponentId % Modulo)`. Handling of `Modulo=0`, accepted range, and refresh timing are unspecified. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `WidgetComponent.UseAutomaticTickModeByDefault` | `bool` (`ref`) | `false` | `false` | Community/Epic help: `true` disables ticking by default for Widget Components; `false` enables ticking by default. The default is applied “by default” and does not describe per-widget overrides. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The target dimension help says maximum dimensions, not that all widget render targets will be resized to those values.
- The occlusion help describes a bounding-box adjustment for a stated false-occlusion case; its multiplier/geometry and possible cost are not specified.
- `RefreshModulo` has an observed snapshot of `0`, while the help uses modulo arithmetic without documenting zero handling. Do not infer the snapshot is safe or a default.
- The build-context table includes nearby widget/tick strings, but proximity does not prove the relevant event, callback, or code path.
- Registry presence and snapshot values do not establish that these entries are accepted by the mod loader's startup `.ini` override mechanism.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
