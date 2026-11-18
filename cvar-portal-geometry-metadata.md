# Portal geometry CVar metadata

These two ability-system entries concern portal overlap and source-plane geometry. The registry identifies both as boolean references and supplies no help. The interpretations below follow the names and remain unverified.

| Exact name | Type / kind | Name-based interpretation |
| --- | --- | --- |
| `AbilitySystemLibrary.CVarGetOverlappingPortalBeforeGetSourcePlanePoint` | `bool` / `ref` | Suggests an ordering choice involving the overlapping-portal lookup and source-plane point computation. Candidate selection and fallback behavior are unknown. |
| `AbilitySystemLibrary.CVarGetSourcePlaneClampInPortal` | `bool` / `ref` | Suggests a clamp applied during source-plane geometry computation for a portal. The clamped quantity and bounds are unknown. |

Both names appear in the preserved build string inventory for 1.1.4042190. These observations leave call order and runtime effects unverified.

[Community registry](EVIDENCE.md#community-sources) · [Build string inventory](EVIDENCE.md#build-specific-static-analysis)
