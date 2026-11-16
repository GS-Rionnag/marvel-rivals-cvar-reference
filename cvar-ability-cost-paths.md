# Ability cost and regeneration CVars

This guide covers three undocumented `Ability.*` switches used in cost/regen paths and the two `AbilitySystem.IgnoreCosts*` variables whose registry help explicitly describes bypassing ability costs. The switches appear behavior-sensitive: they change cost-data selection, cache use, or whether gameplay-ability costs are ignored. Captured values are recorded as observations, not recommendations.

## Variables

| CVar | Type | Snapshot | What the evidence supports | Limits |
|---|---|---:|---|---|
| `Ability.UseNewCostConfig` | bool | `true` | The switch is read 27 times in the build. At `0x14652BF45` and `0x14652BF5D`, its value selects between two branches while code examines a cost-data record; the branches read different fields and the true path copies several fields into an ability-related object. Embedded names nearby include `CanUseAbilityCostConfig`, `MarvelAbilityCostData`, `AbilityCostConfigInfo`, and `InitGameplayAbilityCost`. This supports that it selects a newer ability-cost configuration path. | The field meanings, migration/fallback rules, and exact gameplay differences are unknown. The build comparison is static, not an A/B test. |
| `Ability.UseCacheCostRegen` | bool | `true` | At `0x1466908D4`, false jumps to `0x146690946`; true enters additional checks and a calculation path that reads ability/runtime fields before calling helper `0x14668A000`. This is consistent with enabling a cached ability cost-regeneration path. | The caller's full state and what is cached are not recovered. Do not infer that enabling it improves performance or preserves identical regeneration timing. |
| `Ability.UseSharedCostTypeCacheData` | bool | `true` | At `0x146C05272`, zero skips to `0x146C0561A`; nonzero calls helper `0x146BF6400`, then walks a bucket/chain structure and compares keys. This supports use of a shared cost-type lookup cache when enabled. | Cache key identity, lifetime, invalidation, and fallback behavior are unknown. |
| `AbilitySystem.IgnoreCosts` | bool | `false` | The community help says `Ignore costs for all Gameplay Abilities.` A true value is therefore intended to bypass ability costs. | This is a gameplay-changing control, not a performance setting. Exact cost types and server/client enforcement are not described in the registry help. |
| `AbilitySystem.IgnoreCostsMode` | int32 | `0` | The community help calls this the ignore-costs mode for all Gameplay Abilities. The build reads it and copies it through at least two code sites. | The mode values and what each one ignores are not documented by the help or established by the inspected references. `0` is only the captured value, not a confirmed default or meaning. |

## Evidence and limits

- The three `Ability.*` entries are `ref bool` rows with blank help. `AbilitySystem.IgnoreCosts` is a `ref bool` and `AbilitySystem.IgnoreCostsMode` is a `ref int32`; their help is preserved in `console_vars.tsv`.
- `CVarDump.txt` captures `Ability.UseNewCostConfig=true`, `Ability.UseCacheCostRegen=true`, `Ability.UseSharedCostTypeCacheData=true`, `AbilitySystem.IgnoreCosts=false`, and `AbilitySystem.IgnoreCostsMode=0`. None is claimed to be a default.
- The address-reference scan records 27 direct reads of `Ability.UseNewCostConfig`, one of `Ability.UseCacheCostRegen`, one of `Ability.UseSharedCostTypeCacheData`, two of `AbilitySystem.IgnoreCosts`, and two of `AbilitySystem.IgnoreCostsMode`. Raw hits are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included).
- Build: Marvel Rivals `1.1.4042190` Shipping, SHA-256 `omitted from this documentation-only project`.
- No controlled override comparison was performed. A changed value can alter ability activation costs or energy regeneration; the evidence does not establish a performance benefit.

The three undocumented `Ability.*` settings remain in the [definition-gap worklist](cvar-unresolved-definitions.md); the partial traces above do not establish exact data semantics.
