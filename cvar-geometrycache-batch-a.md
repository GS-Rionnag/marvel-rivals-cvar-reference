# GeometryCache CVar batch A

This guide covers all six exact-case `GeometryCache.*` entries classified as variables. Supplied help describes codec logging, frame interpolation, animation-data residency around playback, and offloading updates from the render thread. The descriptions do not establish that Marvel Rivals loads Geometry Cache assets in normal matches or quantify performance impact.

Captured values are observations, not recommendations or verified defaults. No Epic UE 5.9 reference values were recorded for these entries. Static address-reference candidates from Shipping build 1.1.4042190 are not proof of runtime execution, visible effects, or startup `.ini` acceptance.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `GeometryCache.Codec.Debug` | `int32` (`var`) | `0` | Enables debug logging for the codec. The log destination and detail level are unspecified. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `GeometryCache.InterpolateFrames` | `int32` (`var`) | `1` | Interpolates between Geometry Cache frames when topology permits it. The help does not define fallback behavior when topology prevents interpolation. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `GeometryCache.LookaheadSeconds` | `float` (`var`) | `5` | Amount of animation data, in seconds, to try to keep resident ahead of playback; the help says this applies regardless of playback direction. It is a residency target, not a guarantee that data is available. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `GeometryCache.OffloadUpdate` | `int32` (`var`) | `0` | Help says some updates are offloaded from the render thread to worker and RHI threads. The supplied word “Offloat” appears to be a typo for “Offload”; scheduling details and performance effect are not specified. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `GeometryCache.PrefetchSeconds` | `float` (`var`) | `0.5` | Amount of animation data, in seconds, to preload. The help says this data is loaded blocking when the component spawns. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `GeometryCache.TrailingSeconds` | `float` (`var`) | `2.5` | Amount of animation data, in seconds, to try to keep resident behind the playback direction. | 3 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |

## Interpretation and limits

- These settings describe the Geometry Cache subsystem. The presence of their names in the build does not show that relevant assets or code paths are used during a match.
- Snapshot values are not verified defaults or recommendations for the installed version.
- Static address matches can reflect initialization, writes, or address passing; they do not prove executed behavior or visible changes.
- Registry classification as `var` does not prove that the game's loader accepts an override.

## Sources

Names, types, help, and snapshot observations are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner limitations are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
