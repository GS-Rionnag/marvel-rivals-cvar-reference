# Character CVar batch A

This guide documents seven exact-case `Character.*` variables and references. The supplied registry help is blank for six entries. Their names suggest character hit/replication, shape, and rollback topics, but do not define implementation, units, scope, or visible effects. One entry includes a short URO update-rate description, summarized without expanding the acronym.

Captured values are observations, not recommended or verified defaults. No Epic UE 5.9 reference values were supplied. Static address-reference candidates from Shipping build 1.1.4042190 do not establish runtime behavior or startup `.ini` acceptance.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `Character.CVarSetOverlappingPortal_S4_1` | `bool` (`ref`) | `true` | No help supplied. The name suggests a setting associated with overlapping portals; the `S4_1` suffix and exact behavior are unexplained. | 1 `ref_rva` and 2 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `Character.HitPosition` | `bool` (`ref`) | `false` | No help supplied. The name suggests a hit-position-related switch, but does not say whether it controls recording, replication, tracing, or something else. | 1 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `Character.RepCheckTime` | `float` (`var`) | `0.03` | No help supplied. The name suggests a replication-check interval or time value, but units and use are unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `Character.Shape.FPS` | `int32` (`var`) | `30` | No help supplied. The name suggests an FPS-related shape setting; what is measured or controlled is unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `Character.Shape.Log` | `int32` (`var`) | `0` | No help supplied. The name suggests logging related to character shape, but the logged information and value semantics are unknown. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `Character.Shape.Rollback.SkipOuterBound` | `int32` (`var`) | `0` | No help supplied. The name suggests skipping an outer-bound check in a shape rollback path; the operation and consequences are unverified. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |
| `Character.UROUpdateRate` | `int32` (`var`) | `4` | Supplied help says this value is the URO update per `CVarUROUpdateRate` frame. The source does not define URO, the counting rule, or how this CVar relates to `CVarUROUpdateRate`. | 2 `obj_rva` direct-memory candidates and 1 address-taken candidate; no `ref_rva` hit. |

## Interpretation and limits

- Name-based readings are not definitions. In particular, do not infer that these controls alter hit detection, replication, or rollback in a live match.
- Snapshot values are not verified defaults or recommendations for the installed build.
- Static candidates may reflect initialization, writes, or address passing. They do not prove that code executes or that an override is accepted.
- `var` and `ref` are source classifications, not evidence of `.ini` editability.

## Sources

Names, types, help, and snapshot observations are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner limitations are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
