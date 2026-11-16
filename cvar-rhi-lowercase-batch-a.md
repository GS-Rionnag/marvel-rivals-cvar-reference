# Lower-case `rhi.*` CVar batch A

This guide documents all 11 currently uncovered lower-case `rhi.*` names. They are distinct from uppercase `RHI.*` settings, which have a separate guide. These entries concern bindless shader resources/samplers, present synchronization, frame submission, resource-table caching, and a console-specific FPS option.

All rows have exact-name Epic UE 5.9 reference entries, but those defaults/descriptions do not prove the installed game's engine version, platform support, or behavior. Snapshot values are observations, not recommendations. Static scan candidates do not establish reads/writes, execution, or startup `.ini` acceptance; no runtime override test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `rhi.Bindless.Resources` | `FString` (`ref`) | — | `Disabled` | Community/Epic help: set to `Enabled` for all shader types or `RayTracingOnly` to restrict bindless resources to ray-tracing shaders. | `ref_rva`: 1 direct-memory candidate and 3 address-taking references; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `rhi.Bindless.Samplers` | `FString` (`ref`) | — | `Disabled` | Community/Epic help: set to `Enabled` for all shader types or `RayTracingOnly` to restrict bindless samplers to ray-tracing shaders. | `ref_rva`: 1 direct-memory candidate and 3 address-taking references; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `rhi.EnableConsole120Fps` | `int32` (`ref`) | `0` | `0` | Community/Epic help: enable console 120 FPS when the monitor supports it and the console is configured appropriately. This does not establish PC support. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `rhi.PresentThreshold.Bottom` | `float` (`var`) | `0` | `0` | Community/Epic help: bottom-screen percentage from which tearing is allowed; effective only on supported platforms. Range `0.0`–`1.0`. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `rhi.PresentThreshold.Top` | `float` (`var`) | `0` | `0` | Community/Epic help: top-screen percentage up to which tearing is allowed; effective only on supported platforms. Range `0.0`–`1.0`. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `rhi.ResourceTableCaching` | `int32` (`var`) | `1` | `1` | Community/Epic help: `1` caches resource-table contents within a frame; otherwise the tables are rebuilt for each draw call. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `rhi.SyncAllowEarlyKick` | `int32` (`var`) | `1` | `1` | Community/Epic help: `1` allows the RHI VSync thread to start the next frame early after missing a VSync. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `rhi.SyncAllowVariable` | `int32` (`var`) | `1` | `1` | Community/Epic help: `1` allows variable refresh rate when supported by the output hardware. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `rhi.SyncInterval` | `int32` (`var`) | `1` | `1` | Community/Epic help: VSync interval in supported RHIs. `0` presents immediately; `1` presents every VBlank; `2` every second VBlank; larger values continue the pattern. Supported refresh rates/platforms may differ. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 2 address-taking references. |
| `rhi.SyncSlackMS` | `float` (`var`) | `10` | `10` | Community/Epic help: delays Game Thread kickoff by this many milliseconds before VSync, described as increasing input latency to help performance. This is a source-described tradeoff, not a recommendation. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `rhi.UseSubmissionThread` | `int32` (`var`) | `2` | `2` | Community/Epic help: RHI submission-thread modes: `0` off, `1` on except with multi-GPU, `2` on always. The game's platform and multi-GPU path are not established here. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- Tearing thresholds, variable refresh rate, VSync, and the console 120-FPS option are platform/output dependent. Their presence in the registry does not show those paths are supported in the installed PC build.
- `SyncSlackMS` help describes a latency/performance tradeoff. The wording does not establish the present-day behavior or that raising it improves performance for this game.
- Bindless setting strings are not documented here as safe values for Marvel Rivals; Epic UE 5.9 context alone cannot verify shader compatibility.
- Address-match counts are static candidates, not complete function traces or proof of runtime reads/writes. Whether the loader accepts any of these names in startup `.ini` overrides remains unverified.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
