# Replay CVar batch C: final registered entry

This short final batch documents the sole `replay.*` `var`/`ref` name left after batches A and B: `replay.http.ServerRegion`. The source registry contains 51 distinct names in this prefix. Batches A and B cover 50; with this entry, the current registry has no uncovered `replay.*` variables or references.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help | Build address evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `replay.http.ServerRegion` | `FString` (`var`) | Not captured | Not available in the supplied exact-name reference | None supplied; the accepted values and meaning remain unknown. | No `ref_rva` value-reference is present. The scan has three `obj_rva` direct-memory candidates and one address-taking reference; the direct candidates target the CVar object address and do not establish a read of the `FString` value. |

The registry’s `var` kind, `FString` type, and object-address candidates do not prove the setting is accepted from `.ini`, is exposed to players, or affects a replay session. The snapshot attachment has no assignment for this name, and the catalog supplies no usable snapshot or Epic 5.9 description/default. No runtime replay or override test was performed.

Sources: [community CVar registry](cvar-community-registry.md), [community source notes](EVIDENCE.md#community-sources), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
