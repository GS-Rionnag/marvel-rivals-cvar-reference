# AI CVar batch D: SVON path-cost controls

This final batch documents the last 2 currently uncovered exact-case registered `ai.*` names. Combined with existing AI navigation and game-specific batches plus batch C, it closes the 75-name `ai.*` `var`/`ref` inventory found in the supplied registry.

Community help records the source author’s stated behavior; it does not confirm that Marvel Rivals exercises these paths. Snapshot values come from `CVarDump.txt`; Epic UE 5.9 values are exact-name upstream references. Static address candidates come from Shipping build `1.1.4042190`; direct-memory matches do not distinguish reads, writes, comparisons, or initialization, and address-taking matches alone do not establish value use. No runtime or startup override test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help and separate upstream explanation | Static scan evidence |
| --- | --- | ---: | ---: | --- | --- |
| `ai.svon.bCheckAllMeetNodes` | bool (`ref`) | `true` | `—` | If true, check all meet node cost to choose best path, ONLY work in bidirectional A* *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `ai.svon.bLinkIncludeCheck` | bool (`ref`) | `true` | `—` | If true, check link include when calculate cost *(community registry help)* | `ref_rva`: 0 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- Registry membership and snapshot values do not establish startup `.ini` acceptance, player editability, or live gameplay effect.
- Epic references are upstream exact-name matches; version alignment with the game build is unconfirmed.
- Static address matches are not complete value-use traces.

Sources: [community CVar registry](cvar-community-registry.md), [preserved research attachments](EVIDENCE.md#community-sources), and [build-specific CVar inventory](EVIDENCE.md#build-specific-static-analysis).
