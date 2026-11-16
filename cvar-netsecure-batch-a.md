# NetSecure CVar batch A

This guide covers all seven exact-case `NetSecure.*` entries classified as `ref` variables. The community registry supplies no help text for any of them. Names reference muzzle rollback and projectile-trajectory checks, but their actual algorithms, units, accepted ranges, and gameplay/security roles are unknown. Treat those name-based descriptions as clues only.

Snapshot values are captured observations, not defaults, recommendations, or safe settings. Epic UE 5.9 reference values were not recorded. Each name has static object-address candidates in the scanned Shipping build 1.1.4042190; those scans do not establish runtime behavior or `.ini` acceptance.

| Exact name | Type / kind | Snapshot | What can be said from available evidence | Build scan evidence |
| --- | --- | --- | --- | --- |
| `NetSecure.MuzzleRollbackPostSearchTime` | `float` (`ref`) | `0.5` | No help supplied. The name suggests a time parameter associated with a post-search step in muzzle rollback, but units and meaning are unverified. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.MuzzleRollbackPreSearchTime` | `float` (`ref`) | `0.2` | No help supplied. The name suggests a time parameter associated with a pre-search step in muzzle rollback; units and meaning are unverified. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.ProjectileTrajectory2CheckDir` | `float` (`ref`) | `5` | No help supplied. The name suggests a direction-related parameter for a second projectile-trajectory check; representation and units are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.ProjectileTrajectoryCheckDir` | `float` (`ref`) | `3` | No help supplied. The name suggests a direction-related projectile-trajectory check parameter; representation and units are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.ProjectileTrajectoryCheckDist` | `float` (`ref`) | `300` | No help supplied. The name suggests a distance parameter for a projectile-trajectory check; units and threshold semantics are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.ProjectileTrajectoryCheckTime` | `float` (`ref`) | `0.2` | No help supplied. The name suggests a time parameter for a projectile-trajectory check; units and timing semantics are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |
| `NetSecure.ProjectileTrajectoryReject` | `bool` (`ref`) | `false` | No help supplied. The name suggests a reject-related toggle for projectile trajectory validation, but what it rejects and its effect are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hits. |

## Interpretation and limits

- Every behavior description above is explicitly a naming inference because no community help was supplied.
- Captured values are not validated defaults or recommendations. Do not infer safe or intended changes from the snapshot.
- A `ref` registry row and static address candidates do not prove registration in a current build, runtime reads/writes, or startup override acceptance.
- Static address matches may represent initialization or address passing; they are not function-level evidence of how the settings work.

## Sources

Names, types, and snapshot observations are preserved in the [community CVar source notes](EVIDENCE.md#community-sources). Scanner methodology and build limits are in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
