# MediaIO CVar batch A

This guide covers the seven exact-case `MediaIO.*` entries classified as variables. Supplied help describes render-fence polling priority, threaded frame scheduling and readback, GPU-direct video copies, a field-flipping fix, JIT media-rendering insights, and timed-data channel buffer limits. These descriptions do not show that the game uses these media-input paths during ordinary play.

Captured values are snapshot observations, not recommendations or verified defaults. No Epic UE 5.9 reference values were recorded for these entries. The scanned Shipping build 1.1.4042190 contains static address-reference candidates, but those do not prove runtime execution, config acceptance, or an in-game effect.

| Exact name | Type / kind | Snapshot | Supplied help and practical meaning | Build scan evidence |
| --- | --- | --- | --- | --- |
| `MediaIO.Capture.PollTaskPriority` | `int32` (`var`) | `0` | Priority of the task that polls the render fence. The help does not specify the priority scale or scheduling policy. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.EnableExperimentalScheduling` | `int32` (`var`) | `1` | Whether to send out a frame on a separate thread (experimental). | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.EnableGPUDirectInput` | `int32` (`var`) | `0` | Whether to enable GPU-direct input for faster video-frame copies (experimental). The help does not describe hardware/API requirements. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.JITR.Insights` | `bool` (`var`) | `false` | Generates detailed Just-in-Time Media Rendering insights. The exact output destination and performance cost are unspecified. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.PreventFieldFlipping` | `int32` (`var`) | `1` | Enables an interlaced-field-flipping fix (experimental). The help does not define the affected devices or meaning of other values. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.ScheduleOnAnyThread` | `int32` (`var`) | `1` | Whether to wait for resource readback in a separate thread (experimental). | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `MediaIO.TimedDataChannel.MaxBufferSize` | `int32` (`var`) | `32` | Maximum buffer size a MediaIO channel is allowed to set. Units and behavior at the limit are not specified. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |

## Interpretation and limits

- `MediaIO` names point to media capture/input infrastructure; they do not establish use in normal Marvel Rivals gameplay.
- The numeric values are captured observations, not verified defaults for the currently installed game build.
- Static scanner matches can represent initialization, writes, or address passing. They do not prove that code executed or that a startup `[Overrides]` line is accepted.

## Sources

Exact names, types, help, and captured values are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner methodology are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
