# Halloween CVar batch A

This guide covers all seven currently uncovered exact-case `Halloween.*` registry entries. Every row is classified as a `ref` and has blank supplied help. The wording in the interpretation column is therefore only a name-based hypothesis; the available evidence does not establish which subsystem these controls belong to, whether they are event-specific, or what changing them does.

| Exact CVar | Type / kind | Snapshot | Name-based hypothesis only | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `Halloween.CVarAsHardMode` | `bool` (`ref`) | `false` | May let some mode or behavior be selected as “hard mode”; the controlled feature is unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `Halloween.IgnoreClientImpulseField` | `bool` (`ref`) | `true` | May bypass or ignore a client impulse field; the object, field, and consequences are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `Halloween.IgnoreOcclusion` | `bool` (`ref`) | `false` | May bypass an occlusion check; which objects or query are affected is unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `Halloween.IgnoreProjectileOcclusion` | `bool` (`ref`) | `true` | May bypass projectile occlusion checks; the trace/query and resulting behavior are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `Halloween.IgnoreRepBounce` | `bool` (`ref`) | `true` | May bypass a replication-related “bounce” condition; the term and behavior are undefined in the supplied evidence. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `Halloween.IgnoreRepPenetrate` | `bool` (`ref`) | `true` | May bypass a replication-related “penetrate” condition; the term and behavior are undefined in the supplied evidence. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `Halloween.OpenOcclusionOpt` | `bool` (`ref`) | `false` | May enable an occlusion optimization or feature; the name does not reveal whether “open” enables an optimization or opens a different code path. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- No supplied help was available for any of the seven entries. Even plausible expansions of the names are not confirmed behavior descriptions.
- Snapshot values are captured observations, not verified defaults or recommendations. The values do not reveal polarity or effect.
- Static address-reference hits are candidates only. They do not prove runtime registration, reads/writes, execution, or visible effect.
- The registry’s `ref` classification does not establish that Marvel Rivals accepts these names as startup `.ini` overrides.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
