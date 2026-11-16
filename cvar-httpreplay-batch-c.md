# HTTP replay CVar batch C

This guide covers 2 currently uncovered registered `httpreplay.*` variables. Community help describes intent; snapshots and Epic UE 5.9 exact-name defaults are separate references. Static address candidates are from Marvel Rivals Shipping build `1.1.4042190`, and do not establish runtime reads or startup override acceptance.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `httpreplay.V3.TickAsyncSave` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); not a runtime trace. |
| `httpreplay.WaitimeForNextChunk` | float (`var`) | `5` | `—` | http download next chunk min wait time *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); not a runtime trace. |

## Limits

- Empty help and missing upstream matches remain unresolved.
- Registration and static references do not prove player-facing editability, config acceptance, or a live effect.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
