# Live video, portal rendering, and presentation CVars

These six registry names cover live video, portal rendering, and entries with sparse help. Snapshot values are observations. A dash indicates an absent snapshot value.

| Exact CVar | Kind / type | Snapshot | Registry help and unresolved details | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `M2201.LiveStreamingUrl` | `ref` / `FString` | — | Help identifies this as the Times Square livestream URL. The endpoint, supported formats, and playback conditions are unknown. | 1 / 3 | 2 / 1 |
| `Summoned.NetSmoothing.CubicSplineEnabled` | `ref` / `bool` | `false` | The supplied help is blank. The name suggests cubic-spline smoothing for a summoned entity. Its scope and implementation remain unknown. | 1 / 3 | 1 / 1 |
| `m.Portal.LumenScene.NumberOfMeshCardThresholdScale` | `ref` / `float` | `0.25` | Scales the Lumen mesh-card count threshold in portal views. Help gives a clamp range of `0.1` to `1.0`. | 1 / 3 | 1 / 1 |
| `m.Portal.RenderWithPostProcess` | `ref` / `bool` and `ref` / `int32` | `false` | The `bool` row gives `0` for scene-capture parameter control and `1` for disabled. The `int32` row gives `0` disabled, `1` on demand, and `2` always enabled. The captured value uses Boolean spelling, and the active registration remains unverified. | 3 / 6 | 2 / 2 |
| `pp.debug.msg` | `ref` / `bool` | `false` | The supplied help is blank. The messages, trigger, and output destination remain unknown. | 0 / 3 | 1 / 1 |
| `pv.debug.portalclip` | `var` / `int32` | `0` | The supplied help is blank. The clipping diagnostics and mode values remain unknown. | 0 / 3 | 0 / 1 |

The static scan counts address matches in Shipping build 1.1.4042190. Counts for the duplicate `m.Portal.RenderWithPostProcess` name combine the two registry rows. Direct-memory candidates can include initialization, reads, and writes. Runtime effects and override acceptance remain unverified.

See the [preserved registry and snapshot](EVIDENCE.md#community-sources) and [static address scan](EVIDENCE.md#build-specific-static-analysis).
