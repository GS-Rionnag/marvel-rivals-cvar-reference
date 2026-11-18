# Additional snapshot-only candidates with object-table evidence

This guide adds 15 benign graphics, UI, audio/input, and rendering-support candidates from the existing 67-name snapshot-only set. Every entry has a community snapshot value and a separate `console_objects.tsv` row with help text. Six also have an exact Epic UE 5.9 reference entry. Fourteen have exact printable-name matches in both the x64 and ARM64EC Shipping executable inventories; `ShowFlag.SmartObjects` does not. All 15 lack a `var` or `ref` row in `console_vars.tsv`.

These intersections improve confidence that the source community treated the names as settings and help explain their intended role. They still do not confirm Marvel Rivals runtime registration, accepted config overrides, or in-match effects. Snapshot values are observations, not defaults.

| Exact name | Community snapshot / object flags | Supplied object-table help | Exact Epic UE 5.9 entry | Shipping binary string |
| --- | --- | --- | --- | --- |
| `au.ThreadedSwapDebugExtraTime` | `0` / `0` | Simulates a slow device swap by adding extra time to the swap task. Source spelling is “addional.” | Default `0`; matching description. | x64 + ARM64EC |
| `r.Composure.CompositingElements.Editor.WarnWhenSceneCaptureIsMissingCamera` | `true` / `0` | By default, scene-capture compositing elements rely on a camera. The editor shows a warning image if none is set; disabling the setting allows capture from the element’s own position and orientation. | — | x64 + ARM64EC |
| `r.DumpingMovie` | `0` / `1` | Dumps each rendered frame to disk (slow frame rate). Help says `<=0` is off, `<0` remains on, and `>0` remains on for that many frames; the overlapping negative-value statements are internally inconsistent. | Default `0`; similar description and the same overlapping negative-value wording. | x64 + ARM64EC |
| `r.EnableStereoEmulation` | `0` / `4` | Emulates stereo rendering. | Default `0`; matching description. | x64 + ARM64EC |
| `r.SkeletalMesh.MinLodQualityLevel` | `-1` / `320` | Quality level for the minimum stripping LOD. Help does not define available levels or the meaning of `-1`. | Default `-1`; matching description. | x64 + ARM64EC |
| `r.StaticMesh.MinLodQualityLevel` | `-1` / `320` | Quality level for the minimum stripping LOD. Help does not define available levels or the meaning of `-1`. | Default `-1`; matching description. | x64 + ARM64EC |
| `r.StaticMesh.SimplifyWithTargetPlatform` | `-1` / `0` | `1` simplifies static meshes using target-platform LOD settings; `0` disables the option. | — | x64 + ARM64EC |
| `r.StaticMesh.SimplifyWithWorldSetting` | `-1` / `0` | `1` simplifies static meshes using world settings; `0` disables the option. | — | x64 + ARM64EC |
| `r.Streaming.NoRefLODBiasQualityLevel` | `-1` / `320` | Quality level for the no-reference mesh-streaming LOD bias. The help does not define available levels or the meaning of `-1`. | Default `-1`; matching description. | x64 + ARM64EC |
| `r.Streamline.Load.DeepDVC` | `true` / `36` | Controls whether the DeepDVC feature is loaded; help says this can resolve conflicts when multiple Streamline features are incompatible. | — | x64 + ARM64EC |
| `r.Streamline.Load.DLSSG` | `true` / `36` | Controls whether the DLSS Frame Generation feature is loaded; help says this can resolve conflicts when multiple Streamline features are incompatible. | — | x64 + ARM64EC |
| `r.Streamline.Load.Reflex` | `true` / `36` | Controls whether Reflex is loaded; help says this can resolve conflicts when multiple Streamline features are incompatible. | — | x64 + ARM64EC |
| `sony.NumMissedMotionUpdatesToCombine` | `0` / `0` | Number of missed motion updates to combine into the latest when sending motion events from a PlayStation controller. Help says at most 64 missed updates are stored. | — | x64 + ARM64EC |
| `sony.UnifyMotionSpace` | `0` / `0` | Nonzero values unify acceleration and rotation-rate coordinate space. `0` keeps legacy behavior; `1` uses Unreal’s left-handed, Z-up space; `2` swaps X/Y for right-handed space. Nonzero also changes rotation-rate units to radians/second and acceleration units to g. | — | x64 + ARM64EC |
| `ShowFlag.SmartObjects` | `2` / `0` | General show-flag help: `0` forces the flag off, `1` forces it on, and `2` means do not override (stated default). Help says show-flag overrides work in editor and game; `show` is game-only and UI is editor-only. This row has no exact printable-name match in the scanned Shipping executable set. | — | No exact string match |

## Interpretation and limits

- The community object flags are raw table values, not known mutability or priority markers. Values such as `36`, `320`, and `4` are not interpreted as safety, type, or editability.
- Asset simplification and minimum-LOD settings may apply to cook/build workflows; their presence in Shipping binaries does not prove that those paths run in a match.
- Streamline names identify feature-loading controls in the supplied help, but do not prove that the relevant NVIDIA feature is available, enabled by the driver, or used by the game build.
- `ShowFlag.SmartObjects` has snapshot and object-help evidence but lacks a matching printable string in the scanned binaries, making its relationship to this build weaker than the other entries.
- Exact Epic UE 5.9 matches for six names are upstream comparisons only. They do not establish the game’s exact Unreal version or registration behavior.
- None of these names is listed as `var`/`ref`. Even the strongest cross-source overlap does not establish that a startup `.ini` override is read or changes the running game.

Sources: [community snapshot and object-table attachments](EVIDENCE.md#community-sources), [snapshot-only candidate inventory](cvar-snapshot-only.md), [Epic reference matches](cvar-engine-reference-only.md), and [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis).
