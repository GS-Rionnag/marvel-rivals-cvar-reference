# Chaos Geometry Collection CVars

This guide covers the twelve `p.Chaos.GC.*` variables in the supplied community registry. It records the source descriptions and captured values, then adds direct-read evidence from Marvel Rivals Shipping build `1.1.4042190` where the address scan found it. Snapshot values are not verified defaults or recommendations.

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.GC.CacheComponentSpaceBounds` | bool | `true` | Help says to cache component-space bounds for performance. The build checks the value at `0x142D78650`; zero skips the cache-related path beginning at `0x142D78666`. The exact cached structure and performance effect are not measured. |
| `p.Chaos.GC.ChaosDelay2DormantFrameCnt` | int32 | `1000` | Help says this delays `DormantAll` by a number of frames. No direct reference-value read candidate was found in the saved scan, so this build's use is not independently confirmed here. |
| `p.Chaos.GC.EmitRootBreakingEvent` | bool | `false` | Help says true sends a breaking event when the root breaks. The value gates a path at `0x142D9EFC7`; the following code also checks a positive component field before calling event-related helpers. This supports a gated root-break event path, but not the exact event payload. |
| `p.Chaos.GC.EnableCollisionParticles` | bool | `true` | Help says this enables collision particles for collision and gives a help default of true. A local accessor at `0x142A84340` loads the byte and returns it as a boolean-like value. The consuming collision behavior is not traced from this accessor. |
| `p.Chaos.GC.ISMPoolDebugDraw` | int32 | `0` | Help says this controls debug drawing for ISM pools. The registry row has no usable reference RVA, and no direct value read was found; only registry help and snapshot evidence are available. |
| `p.Chaos.GC.ISMPoolDebugStats` | int32 | `0` | Help says this controls display of ISM-pool statistics. The registry row has no usable reference RVA, and no direct value read was found; only registry help and snapshot evidence are available. |
| `p.Chaos.GC.InitConstantDataParallelForBatchSize` | int32 | `5000` | When `InitConstantData` uses `parallelFor`, this sets the minimum vertices per batch, per help. No direct reference-value read candidate was found in the saved scan. |
| `p.Chaos.GC.InitConstantDataUseParallelFor` | bool | `true` | Help says enabling this uses `parallelFor` to copy some constant data. No direct reference-value read candidate was found in the saved scan; scheduling behavior and whether this is exercised in the retail build remain unknown. |
| `p.Chaos.GC.MaxGeometryCollectionAsyncPhysicsTickIdleTimeMs` | int32 | `30` | Maximum idle time in milliseconds before the asynchronous tick turns off when otherwise idle, per help. No direct reference-value read candidate was found in the saved scan. |
| `p.Chaos.GC.RecordLongMoveGCThreshold` | int32 | `3000` | The registry help repeats the CVar name without defining its threshold or unit. No direct reference-value read candidate was found; the `3000` snapshot value does not establish whether it is milliseconds, distance, frames, or another quantity. |
| `p.Chaos.GC.RemovalTimerMultiplier` | float | `1` | Help describes a multiplier for removal-time evaluation but is malformed: it says `> 1` means faster removal and then repeats `> 1` for slower removal. The value is loaded at `0x142DB3948`, clamped upward against a constant, and multiplied by a computed time value at `0x142DB3950`–`0x142DB395C`; the constant and final removal-time semantics are not identified. |
| `p.Chaos.GC.UseCustomRenderer` | bool | `true` | Help says to use a custom renderer when one is specified. The value is checked at `0x142D7E37D` and `0x142DA497B`; zero branches around renderer-selection work in these paths. The renderer implementation and visual impact are not tested. |

## Evidence and limits

- Names, types, help, and reference addresses come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); snapshot values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Alternate help is in [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); the source manifest records exact matches between the Discord attachments and preserved files.
- Direct reference candidates and scanner limitations are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The described instruction paths were inspected in the installed executable's `.text` disassembly. No direct read is not proof of no use: indirection and non-RIP-relative accesses may be missed.
- No in-game overrides were tested. Do not treat the snapshot as a default or as performance advice.

Related guides: [Chaos CCD settings](cvar-chaos-ccd-axis-targets.md), [Chaos solver settings](cvar-chaos-solver-runtime-controls.md), [CVar overrides and loader syntax](cvar-overrides.md), and [CVar definition gaps](cvar-unresolved-definitions.md).
