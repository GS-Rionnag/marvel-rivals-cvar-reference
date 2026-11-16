# Ability resource loading and table-lookup CVars

These five settings form a focused AbilityRes/table-loading group in the community registry and installed build. Two `AbilityRes.*` variables have explanatory help text. Three `AbilitySystem.CVarUseNewGet*` references select code paths for general data tables, ability-resource tables, and UI-asset tables; their exact old/new behavioral differences remain unknown.

## Variables

| CVar | Type | Snapshot | What the evidence supports | Limits |
|---|---|---:|---|---|
| `AbilityRes.LoadAssetsOnDemand` | int32 | `0` | Community help says values above `0` make locally controlled player characters eagerly load AbilityRes, while simulated proxies load replicated montage presentation assets on demand before playback. The help lists startup arguments `-AbilityResLoadAssetsOnDemand`, `-AbilityResLoadAssetsOnDemand=0/1`, and `-NoAbilityResLoadAssetsOnDemand`. The local binary includes messages that a CVar flip is rejected while a combat world is alive and reverted; a flip outside combat resets the AbilityRes pipeline. | The text does not establish precise values above `1`, memory or network costs, or whether every montage path follows this rule. Treat it as a lifecycle-sensitive loading mode, not a universal load-time reduction. |
| `AbilityRes.Cache.MaxCount` | int32 | `16` | Help says this is the maximum number of resident AbilityRes cache entries. `0` disables and clears the resident cache. | Eviction order, memory size per entry, and the effect of low positive limits are unspecified. This controls cache retention, not the on-demand policy itself. |
| `AbilitySystem.CVarUseNewGetTable` | bool | `true` | Direct reads gate a table-access path. At `0x146EA01D8`, false branches to `0x146EA0340`; true continues through code that passes the literal table key `EquipmentTable` to helper `0x146EB8720` and processes returned entries. Other direct reads occur at nine additional sites. Nearby binary table-name strings also include `BondEffectTable` and `FlyConfigTable`. | The complete set of tables controlled by this switch, the old path, and functional differences are not recovered. |
| `AbilitySystem.CVarUseNewGetAbilityResTable` | bool | `true` | Three direct reads occur in ability-resource lookup code. At `0x146EC8A09`, the CVar is compared with a local path flag; the unequal branch proceeds into helper `0x146E98EE0`. This is consistent with selecting between old and new ability-resource-table lookup paths. | The exact table contents, fallback behavior, and old/new result equivalence are unknown. |
| `AbilitySystem.CVarUseNewGetUIAssetTable` | bool | `true` | Eight direct reads occur in UI asset lookup code. At `0x146EE247F`, a false value branches to `0x146EE27B4`, while true continues into the alternate path. Nearby binary strings name `UIAssets`, `UMarvelGameData::GetAbilityUIAsset.*`, and UI-asset override functions. | The complete call graph and old/new differences are not recovered; no UI comparison was run. |

## Evidence and limits

- The first two entries are `var int32` rows with the help shown in the registry; the three `CVarUseNewGet*` entries are `ref bool` rows with blank variable help and placeholder object help (`.`).
- The captured values above come from `CVarDump.txt`; they are not established defaults or recommendations.
- The build's embedded text contains `AbilityRes.LoadAssetsOnDemand`, startup-argument examples, the combat-world rejection message, and the pipeline-reset message. These are compiled strings; the static evidence does not show that any particular message occurred at runtime.
- The reference scan found 10 direct `ref_rva` memory candidates for `CVarUseNewGetTable`, 3 for `CVarUseNewGetAbilityResTable`, and 8 for `CVarUseNewGetUIAssetTable`. Addresses and build identity are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); the build is Marvel Rivals `1.1.4042190` Shipping, SHA-256 `omitted from this documentation-only project`.
- No controlled comparison was performed. Do not infer that disabling an alternate table path improves performance or preserves identical asset results.

The three table-switch references remain in the [definition-gap worklist](cvar-unresolved-definitions.md) because the exact lookup differences and consequences are still open.
