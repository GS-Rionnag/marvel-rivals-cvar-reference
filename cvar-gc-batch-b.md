# Garbage collection CVar batch B

This guide documents the final three currently uncovered exact lowercase `gc.*` names. Together with batch A and earlier focused guides, the explanatory guides cover all 37 distinct `gc.*` variable/reference names in the supplied registry. Inventory-only cross-check tables are not counted as explanations.

Community help describes intended diagnostic checks; it does not establish active behavior in Marvel Rivals. Snapshot values are observations, Epic UE 5.9 defaults are upstream references, and static address matches do not prove the runtime path executes or that startup overrides are accepted.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help and separate upstream explanation | Static scan evidence |
| --- | --- | --- | --- | --- | --- |
| `gc.VerifyAssumptionsChance` | float (`ref`) | `0` | `0` | Chance (0-1) to randomly verify GC assumptions on each GC. *(community registry help)* Epic UE 5.9 reference: Chance (0-1) to randomly verify GC assumptions on each GC. | `ref_rva`: 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `gc.VerifyAssumptionsOnFullPurge` | bool (`ref`) | `false` | `false` | Whether to verify GC assumptions (disregard for GC, clustering) on full purge GCs. *(community registry help)* Epic UE 5.9 reference: Whether to verify GC assumptions (disregard for GC, clustering) on full purge GCs. | `ref_rva`: 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `gc.VerifyUObjectsAreNotFGCObjects` | int32 (`ref`) | `0` | `0` | If true, the engine will throw a warning when it detects a UObject-derived class which also derives from FGCObject or any of its members is derived from FGCObject *(community registry help)* Epic UE 5.9 reference: If true, the engine will throw a warning when it detects a UObject-derived class which also derives from FGCObject or any of its members is derived from FGCObject | `ref_rva`: 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- `gc.VerifyAssumptionsChance` documents randomized verification on GC; its exact probability/sampling implementation in this game build has not been inspected.
- The other two descriptions concern verification during full-purge GC and warning on UObject/FGCObject inheritance; supplied text is not proof those checks are enabled in the Shipping path.
- Values in the community snapshot are not defaults or recommendations. Epic 5.9 defaults may differ from the game fork.
- Direct-memory candidates can be reads, writes, comparisons, or initialization; address-taking matches alone do not establish value consumption.

Sources: [community CVar registry](cvar-community-registry.md), [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis), [build-specific CVar inventory](EVIDENCE.md#build-specific-static-analysis).
