# Graphics config keys with build-string evidence

Two keys from the preserved January 2025 third-party config also appear as exact strings in both Shipping executables for build 1.1.4042190. Their registry and snapshot evidence leaves CVar registration and config behavior unverified.

| Exact config key | Third-party assignments | Independent evidence | Interpretation limits |
| --- | --- | --- | --- |
| `r.DefaultFeature.AntiAliasing` | `0` in `[/script/engine.renderersettings]`, line 165 | Exact x64 and ARM64EC strings. The community console-object record contains the placeholder help `IAmNoRealVariable`. | The object record gives no usable behavior description. `r.AntiAliasingMethod` has its own registered entry and help. The preserved sources do not establish an alias or shared value mapping. |
| `r.Strata` | `0` in `[SystemSettings]`, line 46, and `[ConsoleVariables]`, line 162 | Exact x64 and ARM64EC strings. The console-object attachment has no exact entry. | The build strings provide no verified mapping to a setting, renderer path, or supported value. |

Neither exact name has a `var` or `ref` row or a captured snapshot value. The third-party assignments show what the config author chose. The match does not establish whether Marvel Rivals reads these keys from the listed sections.

## Sources

[Third-party config cross-check](cvar-third-party-config-crosscheck.md) · [Preserved assignments](cvar-third-party-config-crosscheck.md) · [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Community console objects](cvar-community-console-objects.md) · [Registered anti-aliasing setting](cvar-rendering-batch-c.md)
