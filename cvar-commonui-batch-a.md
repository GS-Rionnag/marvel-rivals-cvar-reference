# CommonUI CVar batch A

This guide covers the eight exact-case `CommonUI.*` registry entries in this slice. Seven have supplied help describing cursor visibility, menu input cleanup, viewport validation, input-configuration tracing, or widget focus warnings. The remaining cursor variable has no gathered description. These are primarily UI/input diagnostics and behavior controls; no Epic UE 5.9 CVar reference default was recorded for any of the eight.

Snapshot values are captured observations, not guaranteed defaults. Static scan evidence comes from Shipping build 1.1.4042190 and indicates references/candidate data in the binary, not runtime effects or `.ini` acceptance.

| Exact CVar | Type / kind | Snapshot | Supplied help and practical meaning | Static scan evidence |
| --- | --- | --- | --- | --- |
| `CommonUI.AlwaysShowCursor` | `bool` (`ref`) | `false` | No description was found. The name suggests cursor display behavior, but does not define when or where the cursor appears. | Static reference and object-address candidates |
| `CommonUI.AutoFlushPressedKeys` | `bool` (`ref`) | `true` | Flushes pressed keys when the input mode switches to Menu. This is input-state cleanup at a mode transition. | Static reference and object-address candidates |
| `CommonUI.Debug.CheckGameViewportClientValid` | `bool` (`ref`) | `true` | Logs an error if CommonUI is used without the current game viewport deriving from `CommonGameViewportClient`. | Static reference and object-address candidates |
| `CommonUI.Debug.TraceConfigChanges` | `bool` (`ref`) | `false` | Traces input-configuration transitions; help labels it non-shipping and suggests `Slate.Debug.TraceNavigationConfig` as a companion trace. | Static reference and object-address candidates |
| `CommonUI.Debug.TraceConfigOnScreen` | `bool` (`ref`) | `false` | Displays traces for input configurations on screen; requires `CommonUI.Debug.TraceConfigChanges`. | Static reference and object-address candidates |
| `CommonUI.Debug.TraceInputConfigNum` | `int32` (`ref`) | `5` | Sets the number of input configurations kept in trace history. Help does not specify bounds or memory cost. | Static reference and object-address candidates |
| `CommonUI.Debug.WarnAllWidgetsDeactivated` | `bool` (`ref`) | `false` | Warns when all widgets are deactivated. Help calls this a valid event that may leave input configurations behind; it does not say the warning itself repairs state. | Static reference and object-address candidates |
| `CommonUI.Debug.WarnDesiredFocusNotImplemented` | `bool` (`ref`) | `false` | Warns when a widget is activated without `GetDesiredFocus` implemented. This is a focus-navigation diagnostic. | Static reference and object-address candidates |

## Caveats

- The debug trace help explicitly says `TraceConfigChanges` is non-shipping. The registry and binary presence alone do not establish that this trace is active or useful in a retail Shipping session.
- Snapshot values should not be treated as canonical defaults. Help text/defaults from an upstream engine reference were not available in the gathered Epic 5.9 cross-reference for this family.
- `ref` is the registry classification, not proof of runtime mutability. No `.ini` loading or live override experiment was performed, so editability and in-game behavior remain unverified.
- Static name/reference hits do not prove reachability, frequency, or a user-visible outcome.

## Sources

Exact names, types, and snapshots are in the [community CVar registry](EVIDENCE.md#community-sources) and [community source notes](EVIDENCE.md#community-sources); captured values also appear in [community source notes](EVIDENCE.md#community-sources). Supplied text context is in [build 1.1.4042190 findings](EVIDENCE.md#build-specific-static-analysis); static scan caveats and provenance are in the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis) and [community source notes](EVIDENCE.md#community-sources).
