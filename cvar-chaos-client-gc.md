# Chaos client-side GC CVars

This guide covers the 12 exact `var`/`ref` registry names beginning with `p.Chaos.ClientGC` or the lowercase-`chaos` variants `p.chaos.ClientGC`. “Client GC” here is the naming used by the game's community registry; the sources do not establish a broader expansion of “GC.” This guide excludes the separate `p.Chaos.GC.*` family.

## Evidence and limits

The community `console_vars.tsv`, `console_objects.tsv`, and `CVarDump.txt` were preserved from Discord; their build and capture procedure are unknown. Snapshot values below are captured values, not defaults, recommendations, or proof of what the current game applies. The registry's `help` text is reproduced as supplied, with spelling preserved where useful.

The installed Shipping executable is Marvel Rivals build `1.1.4042190` (image base `0x140000000`, SHA-256 `omitted from this documentation-only project`). The `ref_rva` values below matched RIP-relative data references in its `.text` section. Disassembly confirms local instructions read some matching addresses, but the Discord registry's relationship to this binary is not proven. An instruction read establishes access, not the full gameplay meaning or whether the branch is reached in normal play. Four entries had no direct value-read candidate in the scan; that does not prove they are unused.

The observed reads use the image address `0x140000000 + ref_rva`. Addresses are listed as virtual addresses (VA) in the disassembly. The parent catalog [explains the scan method and limitations](EVIDENCE.md#build-specific-static-analysis).

## Registry entries with local direct-read evidence

| Exact name | Type | Registry help | Captured value | Local build evidence |
| --- | --- | --- | ---: | --- |
| `p.Chaos.ClientGC.DisableBreakAudioWhenCollapse` | bool | *(blank)* | `true` | Byte read at VA `0x146C7C623`; see below. |
| `p.Chaos.ClientGC.EnableDelayRepData` | bool | Whether to delay sending clientGC rep data. | `true` | Byte reads at `0x146C7F861`, `0x146C81A75`, `0x146C81F3E`, `0x146C82662`, and `0x146C82787`. |
| `p.Chaos.ClientGC.EnableQueuedRepInfo` | bool | *(blank)* | `true` | Byte reads at `0x146C7F86D` and `0x146C82324`. |
| `p.Chaos.ClientGC.ShouldAggregateRepHitData` | bool | Whether to aggregate clientGC hit rep data (hit indicator only show once). | `true` | Byte reads at `0x146C81E43` and `0x146C9B841`. |
| `p.Chaos.ClientGCCollapseNum` | int32 | Define the number of client gc to determine whether it is in collapse state | `25` | Integer compared at `0x146CA44E8`; the same block also compares a count with a second threshold. |
| `p.Chaos.ClientGCMaxRenderNum` | int32 | Define the max number of client gc to render | `25` | Integer read at `0x146C9C491`, tested for a negative sentinel, then compared with a running index. |
| `p.chaos.ClientGCDetailCullMode` | int32 | Client GC cull mode(based on detail mode)0 - Disable, 1 - SimulateButNoCollision, 2 - NoSimulation | `0` | Integer loaded at `0x146CA2DED` into a local field passed onward. |
| `p.chaos.ClientGCUseSecondaryFragment` | bool | ClientGC use secondary fragment effect intead of physics particle. | `true` | Byte reads at `0x146C8F69A` and `0x146CA3A96`; each conditions a branch in code handling a component/fragment-like object. |

### What the local instructions show

- **`DisableBreakAudioWhenCollapse`:** At `0x146C7C623`, a byte comparison gates a nearby helper call: when the CVar is set, a preceding local boolean is tested and can skip the call. This is consistent with a disable/conditional gate, but the surrounding code does not identify the helper as an audio routine. The name's exact “break audio” interpretation therefore remains registry-only.
- **`EnableDelayRepData`:** At `0x146C7F861`, the byte is loaded into `edx`; if a local status equals `3`, `EnableQueuedRepInfo` is loaded instead at `0x146C7F86D`, and the selected value is passed to an indirect call. In a separate block, the flag gates a comparison of a float at object offset `+0x774` against a value at another object offset before execution continues. These show configuration-dependent decisions, but do not reveal the complete replication scheduling behavior.
- **`EnableQueuedRepInfo`:** At `0x146C82324`, false branches around a block that copies entries from a local array into newly allocated records. This establishes a queue-related conditional path in the local code; the name and blank help alone do not identify the record format or when this path runs.
- **`ShouldAggregateRepHitData`:** At `0x146C81E43` and the start of a routine at `0x146C9B841`, false branches skip substantial processing. The supplied help calls this aggregation of hit-rep data and says the hit indicator should show once; the static branches are compatible with that help, but do not independently prove the UI effect or the exact aggregation algorithm.
- **`ClientGCCollapseNum`:** At `0x146CA44E8`, a loaded count is compared with this threshold (`setge` records the result). Nearby code compares that count with another threshold and passes values to another routine. Registry help identifies the count as a collapse-state threshold; local code confirms the comparison, not the full state transition.
- **`ClientGCMaxRenderNum`:** The code at `0x146C9C491` reads the value. Negative values bypass the following check; otherwise a current index is compared against the CVar and the result is stored as a local flag. This supports a count limit/gate, while the registry help supplies the “render” label. Do not assume a particular render path or frame policy from this fragment alone.
- **`ClientGCDetailCullMode`:** At `0x146CA2DED`, the integer is copied into a stack record which is then passed to a helper. The supplied help lists `0` Disable, `1` SimulateButNoCollision, and `2` NoSimulation, but this code fragment does not expose which branches implement those modes.
- **`ClientGCUseSecondaryFragment`:** At `0x146C8F69A`, false jumps past checks before a helper call; at `0x146CA3A96`, false jumps to a false return while true allows more object checks. This is a direct gate in component/fragment handling. The supplied help says it selects a secondary fragment effect instead of a physics particle; the binary fragments do not identify those object types by name, so treat that specific replacement behavior as community-help meaning.

## Registry entries without direct value-read candidates

These four entries are registered in the community variable table and have captured values and help, but the local address scanner found no direct `ref_rva` memory-read candidate in build `1.1.4042190`. Their detailed behavior remains unknown from this research.

| Exact name | Type | Registry help | Captured value | What can be said |
| --- | --- | --- | ---: | --- |
| `p.Chaos.ClientGCCollapseTimeRange` | float | Define the time range of client gc | `5` | The help associates it with a client-GC time range; units, windowing, and the effect of changing it are not established. |
| `p.Chaos.ClientGCEnableTimeFilter` | int32 | Enable time filter for client gc | `1` | The help says it enables a time filter; accepted values and the filter's role are unknown. |
| `p.Chaos.ClientGCLinkMethod` | int32 | ClientGC link method. 0 - Scaled ActorBoundingBox, 1 - Level 1 Particle BoundingBox | `0` | Help describes two linking methods; the local binary scan did not identify their implementation or whether other values are accepted. |
| `p.Chaos.ClientGCMaxRenderNumInMultiFrame` | int32 | Define the max number of client gc to render | `10` | Help repeats the render-count description, but does not clarify how this relates to `ClientGCMaxRenderNum`; the local scan found no direct value read. |

## Practical use in the loader

The repository's override loader loader places CVar lines under `[Overrides]`; a line there overrides the game's config. To try one, use the exact spelling and casing shown in the registry, for example:

```ini
[Overrides]
p.Chaos.ClientGC.EnableDelayRepData=true
```

The data here does not establish that any particular override improves performance, visual quality, or stability. Capture the original config before changing it and compare one change at a time in a controlled session. The modding-specific loading and rollback procedure is in [CVar overrides](cvar-overrides.md).

## Sources

- Preserved registry and snapshot: [CVar research source notes](EVIDENCE.md#build-specific-static-analysis), `console_vars.tsv`, `console_objects.tsv`, and `CVarDump.txt`.
- Local direct-reference output: [address hits TSV](EVIDENCE.md#evidence-artifacts-not-included); entries were cross-checked against the Shipping executable listed above.
- Local disassembly ranges inspected: `0x146C7C623`, `0x146C7F861` / `0x146C7F86D`, `0x146C81E43`, `0x146C82324`, `0x146C9B841`, `0x146C9C491`, `0x146CA2DED`, `0x146CA3A96`, and `0x146CA44E8`.
