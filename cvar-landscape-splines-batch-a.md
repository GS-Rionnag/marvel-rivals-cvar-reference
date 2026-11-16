# Landscape spline conversion CVar batch A

This note documents the currently uncovered `Landscape.Splines.ApplyToSplineComponentMaxIterations` registry entry. Its supplied help defines a maximum iteration count for converting a landscape spline into a spline component. It does not describe the conversion algorithm, iteration units, behavior when the limit is reached, or whether this editor-oriented operation is used in the live game.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `Landscape.Splines.ApplyToSplineComponentMaxIterations` | `int32` (`ref`) | `200` | — | Maximum possible iterations when converting a landscape spline into a spline component. No zero/negative semantics or clipping behavior are supplied. | Name appears in both scanned Marvel Shipping executable inventories; 1 `ref_rva` hit (address-taken only) and 4 `obj_rva` hits (3 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- The help describes spline conversion but does not establish whether the setting is used at runtime, only in editor tooling, or in a particular conversion workflow.
- The captured `200` is an observed snapshot value, not a verified default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or acceptance of a startup `.ini` override. There is no evidence here for the effect of changing the value.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
