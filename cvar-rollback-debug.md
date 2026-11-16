# Rollback debug CVars

This guide covers the twelve currently uncovered, exact-case `rollback.*` variable/reference entries in the community registry. Their supplied help describes debugging and visualization for rollback trace results and hero or summon positions. These names and descriptions do not establish that a startup `.ini` override is accepted or that a setting affects a live match.

All twelve entries are `ref` rows in the supplied registry. Snapshot values below are from the attached `CVarDump.txt`; a dash means the name had no value in that snapshot. None has an exact-name entry in the Epic UE 5.9 CVar reference catalog, so no upstream default or description is claimed.

| Exact CVar | Type | Snapshot | Supplied meaning | `ref_rva` scan | `obj_rva` scan |
| --- | --- | --- | --- | --- | --- |
| `rollback.debug` | `int32` | `0` | Trace recording mode: `0` off, `1` record hits only, `2` always record. | 0 direct-memory candidates; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.fakemiss` | `float` | `0` | Debug-test rate from 0.0 to 1.0 that converts recorded hits to misses; supplied help gives 0.3 as 30%. | 2 direct-memory candidates; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos` | `int32` | — | Position debug-draw bitmask: `0` off, bit 0 (`1`) body capsules including child actors, bit 1 (`2`) hit shapes, `3` both. | 3 direct-memory candidates; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos.duration` | `float` | — | DrawDebug lifetime in seconds; help says default 0.1 and suggests 0.05–0.2 to trade flicker for stale overlapping draws. | 0 direct-memory candidates; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos.heroes` | `FString` | — | Compatibility alias for `.ids`; supplied help says summons use their own derived object IDs, not their source HeroID. | 1 direct-memory candidate; 4 address-taking references. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos.ids` | `FString` | — | Comma-separated object ID filter: HeroID for characters and each summon’s own derived object ID; `0` means all. | 1 direct-memory candidate; 4 address-taking references. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos.interval` | `int32` | — | Draw every N frames; help says `1` means every frame. | 1 direct-memory candidate; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.pos.side` | `int32` | — | Draw-side bitmask: `1` client/local (blue), `2` server/RPC to clients (red), `3` both. | 2 direct-memory candidates; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.result` | `int32` | `0` | Server-side trace result filter: `0` all, `1` hits only, `2` misses only. | 1 direct-memory candidate; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.source` | `int32` | `255` | Server-side source-type bitmask: bit 0 unknown, 1 unified sweep, 2 enemy sweep, 3 ally sweep, 4 scene sweep, 5 collision component, 6 hit verify, 7 scope trace; `0xFF` all. Help also gives common combinations such as `64` hit verify and `192` hit verify plus scope. | 1 direct-memory candidate; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.stackinfo` | `int32` | `0` | Stack capture depth for each trace record; `0` off. Supplied help warns of performance impact when enabled. | 1 direct-memory candidate; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |
| `rollback.debug.target` | `int32` | `2` | Server-side target-type bitmask for hit records; misses bypass this filter. Bit 1 character, bit 2 summoned, bit 3 other (scene/shields); help calls `0xE` all in Editor and gives `2` character only and `6` character plus summoned. | 1 direct-memory candidate; 1 address-taking reference. | 3 direct-memory candidates; 1 address-taking reference. |

## Reading the evidence

The supplied registry help labels these as debug, filtering, and drawing controls. The paired `result`, `source`, and `target` descriptions explicitly identify server-side recording filters; `.side` describes whether client, server, or both sides draw position diagnostics. `fakemiss` is described as a debug display/test aid, not as a change to actual hit detection. The available material does not show whether these controls are exposed in a retail UI or honored by a startup config.

The build 1.1.4042190 address scan reports candidate references to both registry address fields. An address-taking (`lea`) match only obtains an address; a direct-memory instruction can be a read, write, or initialization. These counts do not identify the exact runtime branch or prove the claimed behavior. In particular, most entries have only one `ref_rva` direct-memory candidate in the scan, and the common `obj_rva` matches do not independently establish per-variable use.

Sources: [community CVar registry](cvar-community-registry.md), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), and [build-specific registration/static-analysis notes](cvar-registration-evidence-4042190.md).
