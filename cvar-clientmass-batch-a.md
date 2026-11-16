# Client Mass CVar batch A: swarm, hit, and death budgets

This guide covers the first 25 currently uncovered registered `clientmass.*` CVars in registry order. The supplied help describes client swarm capture, world-wide death-resource budgets, hit-body update tiers, local field scopes, and looping-run capacity. The `console_vars.tsv` registry does not identify a capture build or method, and alignment with Marvel Rivals Shipping build `1.1.4042190` is unconfirmed.

All 25 rows are community-registry `var` entries. The community snapshot and exact-name Epic UE 5.9 reference contain no values/defaults for these names, so those columns are shown as `—`. Help text is the source for each meaning below; it describes intended limits and behavior but is not live-game verification.

The build address scan has object-address candidates for these `var` entries, but no separate `ref_rva` value field. Those matches do not establish that code reads the configured value, that the path runs in a match, or that an `.ini` override is accepted. No runtime query or controlled gameplay comparison was performed.

## Swarm bridge and death budgets

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.Bridge` | int32 (`var`) | `—` | `—` | Enable new client swarm attack capture/registration. Existing flights still deliver hit/end. Managed by the mode's CmdOpt. | 4 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.DeathAnimationBudget` | int32 (`var`) | `—` | `—` | World-wide death animation starts per frame, 1..16384. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.DeathMaterialBudget` | int32 (`var`) | `—` | `—` | World-wide per-instance dissolve commits per frame, 1..16384. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.DeathProjectionBudget` | int32 (`var`) | `—` | `—` | World-wide one-shot death ground queries per frame, 0..16384; waiting has a cooked timeout. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.DeathRetireBudget` | int32 (`var`) | `—` | `—` | World-wide completed corpse resource retirements per frame, 1..16384. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.DeathWithdrawBudget` | int32 (`var`) | `—` | `—` | World-wide dead query-body withdrawals per frame, 1..16384; logical hit identity closes immediately. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |

## Hit update and LOD controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.HitBudget` | int32 (`var`) | `—` | `—` | World-wide existing hit-body pose writes per frame, 0..MaxUnits. Independent of PhysicsWriteBatch. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitDemotionSeconds` | float (`var`) | `—` | `—` | Stable lower tier delay in seconds. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitDiagnosticsFrames` | int32 (`var`) | `—` | `—` | On a value change log up to 600 completed frames, with world/frame, counts and refresh intervals; 0 resets. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitHighHz` | float (`var`) | `—` | `—` | High tier target Hz. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitHighScreen` | float (`var`) | `—` | `—` | High projected size threshold. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitLegacyFrames` | int32 (`var`) | `—` | `—` | QA A/B: full-update mode for at most 3600 ticks per world on a value change; 0 resets. Metrics still run. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitLowHz` | float (`var`) | `—` | `—` | Low tier target Hz. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitMediumHz` | float (`var`) | `—` | `—` | Medium tier target Hz. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitMidCm` | float (`var`) | `—` | `—` | Medium tier distance in cm. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitMidScreen` | float (`var`) | `—` | `—` | Medium projected size threshold. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitMinScreen` | float (`var`) | `—` | `—` | Minimum projected diameter / viewport dimension. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitMinimumHz` | float (`var`) | `—` | `—` | Hidden/offscreen/tiny tier target Hz. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.HitNearCm` | float (`var`) | `—` | `—` | High tier distance in cm. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |

## Local scopes and looping runs

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.LocalScopeCheckBudget` | int32 (`var`) | `—` | `—` | Unit x local field checks per frame (separate from the NPC scope budget). | 2 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.LocalScopeIgnoreIds` | FString (`var`) | `—` | `—` | Comma separated scope ids never registered as local scopes (custom hero geometry). Empty = none. | 2 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.LocalScopeMaxWindows` | int32 (`var`) | `—` | `—` | Max local spell field windows (field x route run) alive at once. | 2 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.LoopMaxAlive` | int32 (`var`) | `—` | `—` | Simultaneously Alive units of one looping run, 0..16384; 0 means no per-run limit. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.LoopMaxResident` | int32 (`var`) | `—` | `—` | Resident units of one looping run (Alive+Dying+Dissolving+Retiring), 0..16384; 0 means no per-run limit. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |
| `clientmass.LoopWorldCapacity` | int32 (`var`) | `—` | `—` | Resident units of the whole world, 1..16384. Clamped to the hard limit, which is never raised. | 3 direct-memory object-address candidate(s), 1 address-taken reference(s); no value-level access or control flow was established. |

## Limits and interpretation

- The help text names thresholds, budgets, refresh rates, and caps. It does not provide validated quality/performance tradeoffs, the affected entity set, or fallback behavior for invalid values beyond cases stated directly in the help.
- `0` is not universally an off switch in this family: for example, some help entries define zero as “no per-run limit,” “disable age rule,” or “reset diagnostics.” Read each row’s own description before interpreting a value.
- None of these entries has a snapshot value or exact Epic 5.9 default in the registry, and none has a verified live value here. They are documented as candidates, not recommendations.
- Several rows refer to separate settings such as `clientmass.PhysicsWriteBatch`. Their interaction is not inferred beyond what the supplied help says.

For the complete candidate list and source caveats, see the [community CVar registry](cvar-community-registry.md). The static scan scope is described in the [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
