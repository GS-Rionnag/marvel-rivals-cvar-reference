# Pak cache CVar batch A

This guide documents all 10 currently uncovered exact-case lower-case `pakcache.*` variable/reference rows. The supplied descriptions cover cache organization, precaching budgets, filesystem I/O request limits, and trimming of unused blocks.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 address evidence |
| --- | --- | --- | --- | --- | --- |
| `pakcache.CachePerPakFile` | `int32` (`ref`) | 0 | — | When greater than zero, use a separate cache for each pak file. | Name appears in both Shipping executable string inventories. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.Enable` | `int32` (`ref`) | 1 | — | When greater than zero, enable the pak cache. | Name appears in both Shipping executable string inventories. `ref_rva`: 4 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.EnableIOPoolCPUWork` | `int32` (`ref`) | 0 | — | When greater than zero, run I/O CPU work in the I/O thread pool. | Name appears in both Shipping executable string inventories. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.EnableNoCaching` | `int32` (`ref`) | 0 | — | When greater than zero, allow a read request’s pak-cache memory to be discarded early; this does not describe disabling the whole pak cache. | Name appears in both Shipping executable string inventories. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.MaxBlockMemory` | `int32` (`ref`) | 128 | — | Soft memory budget in MB for precaching; the system attempts to stay within it. | Name appears in both Shipping executable string inventories. `ref_rva`: 1 direct-memory / 2 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.MaxRequestSizeToLowerLevellKB` | `int32` (`ref`) | 1024 | — | Maximum size in KB of individual I/O requests submitted to the operating-system filesystem. Exact spelling is preserved from the registry. | Name appears in both Shipping executable string inventories. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.MaxRequestsToLowerLevel` | `int32` (`ref`) | 2 | — | Maximum number of simultaneous I/O requests submitted to the operating-system filesystem, additionally limited by `PAK_CACHE_MAX_REQUESTS`. | Name appears in both Shipping executable string inventories. `ref_rva`: 5 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.NumUnreferencedBlocksToCache` | `int32` (`ref`) | 10 | — | Maximum number of unreferenced blocks to retain. Supplied help estimates maximum wasted memory as `MaxRequestSizeToLowerLevellKB × NumUnreferencedBlocksToCache`. | Name appears in both Shipping executable string inventories. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.TimeToTrim` | `float` (`ref`) | 0 | — | How long a cached, unreferenced block is kept before trimming; the unit is not stated in the supplied help. | Name appears in both Shipping executable string inventories. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `pakcache.UseNewTrim` | `int32` (`ref`) | 0 | — | When greater than zero, use a round-robin trim strategy per pak file. | Name appears in both Shipping executable string inventories. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |

## Evidence limits

- Snapshot values are observations from `CVarDump.txt`, not verified defaults or recommendations.
- No exact Epic UE 5.9 default was recorded for these pak-cache names. This comparison does not establish the game’s engine version.
- The Shipping string inventory confirms only printable-name presence. Address-scan counts are candidate references to registry fields, not proof of runtime registration, reads, writes, or execution.
- `var`/`ref` labels in the community registry do not establish that the loader accepts a startup override. No controlled runtime change was performed.
- Some unit and policy details are absent from the supplied help and are called out rather than inferred.

Sources: [community CVar registry](cvar-community-registry.md), [Epic UE 5.9 comparison and captured values](cvar-community-registry.md), [preserved community attachments](EVIDENCE.md#community-sources), [build CVar string inventory](EVIDENCE.md#build-specific-static-analysis), and [build address-reference scan](EVIDENCE.md#build-specific-static-analysis).
