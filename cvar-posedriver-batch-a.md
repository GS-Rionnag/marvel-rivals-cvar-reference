# PoseDriver CVar batch A

This note documents the currently uncovered `PoseDriver.EnableSetMorphTarget` registry entry. The registry classifies it as a `bool` variable, but supplies no help text. Its name suggests a switch related to setting morph targets from a pose driver; that reading is only a name-based inference, and the controlled component, call sites, and visual effects are not established by the available evidence.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Supplied meaning | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `PoseDriver.EnableSetMorphTarget` | `bool` (`var`) | `true` | — | No help supplied. The name suggests enabling a pose-driver morph-target operation, but does not define what is enabled or under what conditions. | Name appears in both scanned Marvel Shipping executable inventories; 0 `ref_rva` and 3 `obj_rva` matches (2 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- `PoseDriver` and `SetMorphTarget` provide a plausible feature hint, not verified semantics. Do not infer that this changes a particular hero, animation, or character mesh.
- The captured value `true` is an observed snapshot, not a guaranteed default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or acceptance of a startup `.ini` override. No controlled in-game comparison has been made.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
