# Miscellaneous engine/runtime CVar batch A

This batch documents eight currently uncovered exact-case `var`/`ref` names from low-frequency namespaces. Their names and supplied help point to ability-system logging, allocator telemetry, media encoding, memory tracing, mesh visibility state, mobile UI scaling, and mapped I/O. Build scan hits are address-reference candidates only; they do not prove runtime use or startup `.ini` acceptance.

| Exact name | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 scan evidence |
| --- | --- | --- | --- | --- |
| `Abilities.LogMacros` | `FString` (`ref`) |  | Set Abilities System's Verbosity to Warning | 6 address-reference candidate(s); not a verified runtime read/write or effect. |
| `MallocBinned2.FlushThreadCacheMaxWaitTime` | `float` (`ref`) | 0.02 | The threshold of time before warning about FlushCurrentThreadCache taking too long (seconds). | 7 address-reference candidate(s); not a verified runtime read/write or effect. |
| `MallocBinned3.FlushThreadCacheMaxWaitTime` | `float` (`ref`) | 0.02 | The threshold of time before warning about FlushCurrentThreadCache taking too long (seconds). | 5 address-reference candidate(s); not a verified runtime read/write or effect. |
| `MediaEncoderX.BindBackBufferOnRenderThread` | `int32` (`var`) |  | Bind and unbind the back buffer callback on the render thread. 0: Use the legacy game-thread path (may race with rendering). 1: Use the render-thread path (default). Takes effect on the next encoder start. | 4 address-reference candidate(s); not a verified runtime read/write or effect. |
| `MemoryTrace.Delay` | `bool` (`ref`) | false | Memory trace delay | 5 address-reference candidate(s); not a verified runtime read/write or effect. |
| `MeshHidden.CheckOtherHiddenSourcesOnRemove` | `bool` (`var`) | true | When removing conditional hidden, check if other hidden sources exist before showing. true: Skip showing if Tag hidden or other conditional hidden is still active (default) false: Always execute showing (original behavior) | 4 address-reference candidate(s); not a verified runtime read/write or effect. |
| `Mobile.EnableUITextScaling` | `int32` (`var`) | 0 | Enables Mobile UI Text Scaling | 4 address-reference candidate(s); not a verified runtime read/write or effect. |
| `mmio.enable` | `int32` (`ref`) | 1 | If > 0, then enable memory mapped IO on platforms that support it. | 6 address-reference candidate(s); not a verified runtime read/write or effect. |

## Interpretation limits

- Snapshot values are captured observations, not guaranteed defaults or recommendations. Blank snapshot cells mean no captured value was present in the supplied snapshot.
- `var` and `ref` are registry classifications; neither alone proves the game accepts a startup override through the mod loader.
- Static scan matches are build-specific address-reference candidates. They do not establish registration, runtime execution, or user-visible behavior.
- The help text is reproduced as supplied; interpretation beyond it is not independently verified.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources); [build 1.1.4042190 static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
