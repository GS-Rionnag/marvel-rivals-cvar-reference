# AbilitySystem CVar batch D

This guide covers the three registered `AbilitySystem.*` CVars not already listed in the explanatory AbilitySystem guides at the time of this audit. The community registry supplies their types, help, and snapshot values; the capture build and method are unknown. No exact Epic UE 5.9 default was found for these names.

The build evidence comes from static address scanning of Marvel Rivals Shipping build `1.1.4042190`. Direct references identify candidate reads or writes but do not establish the surrounding branch, caller, runtime path, or effect in a match. No live CVar query or controlled `.ini` override was performed.

| Exact CVar | Type | Snapshot | What supplied help says | Build evidence and limits |
| --- | --- | ---: | --- | --- |
| `AbilitySystem.GameplayCue.EnableCueAsyncForWeapon` | bool (`ref`) | `true` | Enables asynchronous handling of cues for `ShootingWeapon` and its subclasses. The help does not describe scheduling details, fallback behavior, or a performance/gameplay tradeoff. | One direct comparison candidate (`cmp` against the reference value) and one address-taken reference. The other scan hits point at the CVar object and can be registration/setup. The compared branch and cue execution path were not traced. |
| `AbilitySystem.PeriodicDamageManager` | int32 (`ref`) | `1` | When enabled, intercepts periodic DamageEffects and drives them internally as instant effects through the merge pipeline. The help does not state accepted integer values beyond the enabled wording or describe timing/stacking semantics. | Two direct comparison candidates and one direct store candidate target the reference value, plus address/setup hits. The branch and write context were not traced, so the snapshot is not confirmed as the live default. |
| `AbilitySystem.UseTableNameIndex` | bool (`ref`) | `—` | Uses a table-asset name index for exact `GetTable` lookup when `1`; `0` falls back to a full AssetRegistry scan. This describes the lookup strategy but gives no measured cost or cache invalidation behavior. | Two direct comparison candidates target the reference value, plus object/setup references. The lookup callers and runtime effect were not traced. |

## Interpretation limits

- The three descriptions are registry help, not confirmation that Marvel Rivals registers or honors the settings in a match.
- Snapshot `true`/`1` values are observations from an unversioned community capture, not recommendations or verified defaults. A missing snapshot is shown as `—`.
- Static comparison candidates show that code may inspect the reference value; they do not prove which branch corresponds to enabled/disabled or when it runs.
- These settings can affect gameplay-cue handling, periodic damage processing, or asset-table lookup. They are not general graphics-performance switches.
