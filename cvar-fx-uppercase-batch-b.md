# FX CVar batch B: uppercase namespace

This guide records the final two currently uncovered registered names with exact case-sensitive component `FX`. Together with batch A, this completes all 27 registered `FX.*` names. These are distinct from lowercase `fx.*` controls.

Snapshots are captured values, not defaults. Static reference classes do not prove access direction, execution, or `.ini` acceptance.

| Exact CVar | Type(s) | Snapshot | Epic 5.9 default | Supplied help and provenance | Build scan evidence and limits |
|---|---|---|---|---|---|
| `FX.Trail.MaxTangentTessellation` | int32 | 65535 | `65535` | Community help: Maximum tessellation steps allowed for tangent based tessellation. Epic 5.9 description: Maximum tessellation steps allowed for tangent based tessellation. | `ref_rva`: 2 direct-memory candidates, 1 address-taking references; `obj_rva`: 2 direct-memory candidates, 1 address-taking references; runtime effect unverified. |
| `FX.VisualizeGPUSimulation` | int32 | 0 | `0` | Community help: Visualize the current state of GPU simulation.<br>0 = off<br>1 = visualize particle state<br>2 = visualize curve texture Object-table help: Visualize the current state of GPU simulation. 0 = off 1 = visualize particle state 2 = visualize curve texture Epic 5.9 description: Visualize the current state of GPU simulation.  0 = off  1 = visualize particle state  2 = visualize curve texture | `ref_rva`: 2 direct-memory candidates, 1 address-taking references; `obj_rva`: 2 direct-memory candidates, 1 address-taking references; runtime effect unverified. |

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build address-reference scan](EVIDENCE.md#build-specific-static-analysis), and [build-specific candidate inventory](EVIDENCE.md#build-specific-static-analysis).
