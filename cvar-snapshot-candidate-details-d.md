# Low-confidence engine and rendering snapshot candidates

This guide covers six benign-looking engine, rendering, and effects-management names from the remaining snapshot-only set. Each appears in `CVarDump.txt`, but none has a `var`/`ref` row in `console_vars.tsv`, an object-table row in `console_objects.tsv`, an exact Epic UE 5.9 reference entry, or an exact printable-name match in the scanned Shipping binary inventory. Their values and meanings are therefore weakly supported: the value is a community snapshot observation, and the likely role is only a name-based possibility.

| Snapshot name | Captured value (not default) | Conservative name-based possibility | Evidence and confidence |
| --- | --- | --- | --- |
| `a.ForceUseAnimNotifyFilters` | `false` | May control whether animation notify filters are forced on. Exact scope and effect are unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |
| `GameplayCue.DisableBuffCueRecycle` | `false` | May disable recycling of buff gameplay-cue actors or effects. Whether this affects visuals, memory use, or another lifecycle behavior is unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |
| `GameplayCue.DisableTargetActorCueRecycle` | `false` | May disable recycling of target-actor gameplay cues. The affected actor class and behavior are unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |
| `GameplayCue.EnableCueActorCache` | `false` | May enable a cache for cue actors. Cache lifetime, contents, and effect are unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |
| `mass.EnableMassCMCParallelUpdate` | `false` | May control parallel updates for a system referred to as “Mass CMC”; the expansion, affected objects, and runtime behavior are unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |
| `r.BatchedElementUsePoolResource` | `1` | May select pooled resources for batched rendering elements. The type, accepted values, and effect are unknown. | Snapshot only; no help/type metadata or exact Shipping string match. Low confidence. |

## Limits

- These six are documented as candidates because their names suggest engine/rendering resource or presentation behavior; the names do not establish their implementation.
- No type is assigned: the snapshot `name=value` format does not establish whether a value is a bool, integer, enum, or another type.
- No default, recommendation, editability, or live-game effect is inferred from the captured value.
- Other remaining names were not promoted here where their names point toward abilities, teleportation, matchmaking/network identity, feedback diagnostics, or signature checks and the available source evidence was insufficient to classify their behavior as benign.

Source: [community snapshot and related registry attachments](EVIDENCE.md#community-sources); the snapshot-only inventory records the absent object-table, Epic-reference, and build-string evidence for these candidates.
