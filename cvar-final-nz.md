# Component, trace, and record CVars with unresolved meanings

Three additional exact registry names have snapshot or static scan evidence. Their help fields are empty or contain only punctuation. The name and metadata leave their behavior, valid values, and runtime availability unknown.

| Exact CVar | Kind / type | Snapshot | Unresolved detail | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `Summoned.EnableEarlyRegisterComponent` | `ref` / `bool` | — | Which component is involved and when registration occurs. | 2 / 3 | 1 / 1 |
| `TraceMgr.CVar_UseDeepCopyCustomPreFilter` | `ref` / `bool` | `true` | The copied data and which filters are affected. | 2 / 3 | 1 / 1 |
| `VirtualProjectile.RequestRecordIntervalTime` | `ref` / `float` | `0.1` | The time unit, measured interval, and affected records. | 3 / 3 | 1 / 1 |

A dash marks an entry absent from the preserved snapshot. Counts are candidates from the Shipping 1.1.4042190 scan and can include initialization, reads, writes, and address passing. See the [preserved registry and snapshot](EVIDENCE.md#community-sources) and the [static address scan](EVIDENCE.md#build-specific-static-analysis).
