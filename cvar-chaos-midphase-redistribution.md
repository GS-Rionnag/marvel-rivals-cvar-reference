# Chaos midphase redistribution CVars

This guide covers the three `p.Chaos.MidPhase.*` variables. The registry and object table provide descriptions, and the installed Marvel Rivals Shipping build `1.1.4042190` has direct reads for all three. The names are absent from the supplied `CVarDump.txt`, so no captured value is available here.

| CVar | Type | Meaning and local-build evidence |
| --- | --- | --- |
| `p.Chaos.MidPhase.Redistribution` | int32 | Help says this selects the legacy `ParallelFor` path that splits midphase assignment/narrow-phase work into balanced worker batches; assignment and narrow phase share one `ParallelFor` unless a midphase modifier is registered. At `0x1429A37A7`, the value is compared with local mode state; a mismatch calls helper `0x142855890` at `0x1429A37BC` before the routine continues. The full helper policy and mode values are not reconstructed. |
| `p.Chaos.MidPhase.RedistributionMinItems` | int32 | Minimum overlap count required for redistribution, per help. In the checked path at `0x1428558E8`–`0x14285590B`, code sets a minimum threshold of at least `1`, raises that threshold to the CVar if larger, and rejects the work item when its computed count is below the threshold. |
| `p.Chaos.MidPhase.RedistributionMaxBatchItems` | int32 | Maximum overlaps or midphases in one work batch, per help. Two local call paths clamp the value to a range with minimum `1` and maximum `4096` before passing the batch limit to helper `0x142855CC0` (`0x142855A27`–`0x142855A4F` and `0x14285DCAB`–`0x14285DCD7`). The helper's scheduling policy is not fully recovered. |

## Evidence and limits

- Names, types, descriptions, and reference addresses come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). The [source manifest](EVIDENCE.md#build-specific-static-analysis) records the preserved attachment provenance. `CVarDump.txt` has no rows for these three names.
- Direct-read locations are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The instruction behavior above was checked against the local executable's `.text` disassembly.
- These static paths establish that the values can reach redistribution logic in the executable, not that a Marvel Rivals map or match activates the legacy path. No in-game override was tested.

Related guides: [Chaos solver island/iteration settings](cvar-chaos-solver-islands-iterations.md), [Chaos solver collision settings](cvar-chaos-solver-collision.md), and [CVar overrides and loader syntax](cvar-overrides.md).
