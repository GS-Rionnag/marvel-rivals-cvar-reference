# GAS projectile CVar batch B

This guide covers the seven remaining registered `GAS.Projectile*` entries after batch A. Repeated rows in the supplied registry are treated as repeated registrations of one exact CVar name, not separate variables. Community snapshot values, Epic UE 5.9 matches, community help, and build scan results are separate evidence types.

Address candidates come from static scanning of Marvel Rivals Shipping build `1.1.4042190`. They are not a trace of full functions or proof of executed gameplay branches. No controlled startup override or in-match comparison was done.

| Exact CVar | Kind / type | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `GAS.Projectile.TrajectoryRecordEnabled` | `ref` / bool | `false` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 5 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.Projectile.TrajectoryRecordInterval` | `ref` / float | `0.1` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.Projectile.VirtualProjectileTickExpansionCount` | `ref` / int32 | `0` | `—` | 虚拟投射物tick列表扩容值 *(assistant translation, unreviewed: Expansion amount for the virtual-projectile Tick list.)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.Projectile.VirtualProjectileTickMaxUpdateCount` | `ref` / int32 | `20` | `—` | 虚拟投射物tick最大遍历列表次数 *(assistant translation, unreviewed: Maximum number of entries traversed in the virtual-projectile Tick list.)* | `ref_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.Projectile.VirtualProjectileUseMathVerification` | `ref` / bool | `false` | `—` | 虚拟投射物使用数学模拟 *(assistant translation, unreviewed: Use mathematical simulation/verification for virtual projectiles.)* | `ref_rva`: 20 direct-memory candidate(s), 11 address-taking reference(s); `obj_rva`: 33 direct-memory candidate(s), 11 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.ProjectileForceHomingToRoot` | `ref` / bool | `false` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |
| `GAS.ProjectileMayRepAOITarget` | `ref` / bool | `false` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s). Direction and execution path were not traced. |

## Interpretation limits

- The virtual-projectile help is translated but not independently reviewed; the other four entries have no explanatory help in the attachment.
- A missing Epic match means no exact-name UE 5.9 entry was found in the compared catalog, not that the game has no default.
- A registered `ref` row or static address candidate does not prove that a startup `.ini` override is accepted or that the value changes a match.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
