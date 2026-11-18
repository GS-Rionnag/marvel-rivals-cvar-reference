# Replay and spectate CVars

This guide covers six `Replay.*` and six `Spectate.*` variables. Snapshot values are captured observations from an unspecified build. A dash indicates no recorded value or matching evidence in the relevant source.

The build string column lists exact names found in build 1.1.4042190. The two address columns report x64 scan counts as direct-memory candidates / address-taking instructions. These static observations leave runtime effects and startup override support unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `Replay.Debug.Pause` | `int32` / `var` | `0` | No supplied help. The name suggests replay pause diagnostics. The trigger and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | — |
| `Replay.Debug.Start` | `int32` / `ref` | `0` | No supplied help. The name suggests replay-start diagnostics. The trigger and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `Replay.NetworkTool.OnlyReplay` | `int32` / `var` | `1` | No supplied help. The name suggests a replay-only mode in a network diagnostic tool. Its scope is unspecified. | x64, ARM64EC | 3 / 1 | — |
| `Replay.ReverseTickList` | `bool` / `ref` | `true` | No supplied help. The name suggests reversing a replay tick list. Ordering and call-site behavior are unverified. | x64, ARM64EC | 3 / 1 | 0 / 1 |
| `Replay.SuppressTimeJump` | `int32` / `var` | `0` | At 1, suppresses calls to SetCurrentReplayTimeToSeconds. The help describes preventing timeline resets by the replay panel while TakeRecorder ManagerSource controls it. | x64, ARM64EC | 3 / 1 | — |
| `Replay.UseReplayConnection` | `bool` / `var` | `false` | No supplied help. The name suggests selecting the replay connection. The fallback and affected callers are unspecified. | x64, ARM64EC | 2 / 1 | — |
| `Spectate.EnableSpectate` | `int32` / `var` | `1` | The help says OpenSpectate. The name suggests an enable switch, with no supplied value mapping. | x64, ARM64EC | 2 / 1 | — |
| `Spectate.EnableSwitchBlend` | `int32` / `var` | `1` | Blends camera transitions when switching spectator view targets in a replay. The help says 0 selects a hard cut. | x64, ARM64EC | 2 / 1 | — |
| `Spectate.Fix494485` | `int32` / `var` | `1` | Addresses loss of spectator lock when a hero switch temporarily clears the view target. The help maps 0 to the old behavior and 1 to ignoring the null target. | x64, ARM64EC | 2 / 1 | — |
| `Spectate.FixTopDownRotation` | `int32` / `var` | `1` | Normalizes the top-down camera heading with zero roll. The help says 0 selects legacy rotation. | x64, ARM64EC | 2 / 1 | — |
| `Spectate.StateSelfManaged` | `int32` / `var` | `1` | Translated help describes managing spectator state locally on each side to avoid a race from client state updates. | x64, ARM64EC | 3 / 1 | — |
| `Spectate.UseCharacterRegistry` | `bool` / `ref` | — | At 1, the stated default, camera selection and spectate respawn-follow use the game state's character registry. The help says 0 uses legacy pawn iteration. | x64, ARM64EC | 3 / 1 | 2 / 1 |

The [Q–Z CVar guide](cvar-residual-qz-b.md) covers the four `ReplayDataExport.*` variables.

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Help translations](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
