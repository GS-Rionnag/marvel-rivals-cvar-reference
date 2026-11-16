# Animation-node CVar batch A

This page covers 18 `a.AnimNode.*` entries in the preserved community registry. The registry supplies descriptions and a `CVarDump.txt` snapshot for all 18. Those values are observations from an attachment with unknown game build and collection method; they are not verified defaults or recommendations.

## Animation and pose nodes

| Exact CVar | Type | Snapshot | What the registry says | Evidence and limits |
| --- | --- | ---: | --- | --- |
| `a.AnimNode.AOWithIK.Enable` | int32 (`var`) | `1` | Enables or disables `AOWithIK`. The help does not expand the acronym or describe its animation inputs and output. | The build string index contains this name. The saved address scan records its object address during setup, not a verified runtime read of its value. |
| `a.AnimNode.AOWithIK.Print` | int32 (`var`) | `0` | Enables or disables `AOWithIK` debug information. The help does not identify the output destination or detail what gets printed. | Same string-index and object-address evidence as the enable entry; actual logging behavior was not traced. |
| `a.AnimNode.AimOffsetLookAt.Debug` | int32 (`var`) | `0` | Toggles LookAt AimOffset debugging. The debug visualization or output is unspecified. | The binary contains the name; scanner hits are associated with the CVar object's address and are not proof of the debug path's value check. |
| `a.AnimNode.AimOffsetLookAt.Enable` | int32 (`var`) | `1` | Enables or disables the LookAt AimOffset node. The registry does not describe how its look target is selected or how disabling it changes the pose. | Name and object-address setup are present in the local build scan; the animation graph and value consumer were not recovered. |
| `a.AnimNode.Inertialization.Enable` | int32 (`var`) | `1` | Enables or disables inertialization. The registry does not describe transition eligibility, duration, or fallback behavior when disabled. | Name and object-address setup are present in the local build scan; runtime branch behavior was not traced. |
| `a.AnimNode.Inertialization.IgnoreDeficit` | int32 (`var`) | `0` | Ignores inertialization time deficit caused by interruptions. The help does not define how the deficit is measured or which interruptions cause it. | The name and help also occur in the local binary string index. Nearby text is descriptive evidence, not a recovered consumer path. |
| `a.AnimNode.Inertialization.IgnoreVelocity` | int32 (`var`) | `0` | Ignores velocity information during inertialization, which the registry describes as effectively reverting to a quintic-difference blend. The exact curve and transition setup are not specified. | The name and help occur in the local binary string index. The scan does not establish the node's full blend calculation. |
| `a.AnimNode.KawaiiPhysics.Debug` | bool (`var`) | `false` | Enables visualization debugging for KawaiiPhysics. The registry does not list the drawn primitives, filtering, or display conditions. | The name is present in the registry and snapshot. A draw or runtime toggle path was not traced in this research. |
| `a.AnimNode.KawaiiPhysics.Debug.LengthRate` | bool (`var`) | `false` | Enables visualization debugging for the KawaiiPhysics bone `LengthRate`. The help does not define the metric or its units. | The name is present in the registry and snapshot. Metric calculation and visualization were not inspected. |
| `a.AnimNode.KawaiiPhysics.Enable` | bool (`var`) | `true` | Enables or disables KawaiiPhysics. The registry does not detail which nodes or actors use it, nor the disabled behavior. | The name is present in the registry and snapshot. No consumer path or in-game effect was verified. |
| `a.AnimNode.SlopeWarping.Enable` | int32 (`var`) | `1` | Toggles slope warping. The help does not explain terrain sampling, foot placement, or fallback behavior. | The registry help is only the short toggle description; no value-consumer path was identified in this batch. |
| `a.AnimNode.StateMachine.EnableRelevancyReset` | int32 (`var`) | `1` | Resets a state machine when it becomes relevant. The help does not specify what “relevant” means in the game's animation update policy or which state is restored. | The registry help is the only direct semantic evidence here; the state-machine transition behavior was not traced. |

## Leg IK controls

| Exact CVar | Type | Snapshot | What the registry says | Evidence and limits |
| --- | --- | ---: | --- | --- |
| `a.AnimNode.LegIK.AveragePull` | int32 (`var`) | `1` | `Leg IK AveragePull`; the help gives no range, units, or true/false interpretation despite the integer type. | The local scan includes address setup for the CVar object, but does not establish a value read or what this setting changes. |
| `a.AnimNode.LegIK.Enable` | int32 (`var`) | `1` | Toggles the Leg IK node. The registry does not define what happens to the leg pose when disabled. | The local scan includes address setup for the CVar object; it does not establish the animation-node branch behavior. |
| `a.AnimNode.LegIK.EnableTwoBone` | int32 (`var`) | `1` | Enables the two-bone code path. The help does not state which solver is used otherwise or the supported skeleton assumptions. | Object-address setup appears in the scan, but the alternative solver path was not recovered. |
| `a.AnimNode.LegIK.MaxIterations` | int32 (`var`) | `0` | Overrides the Leg IK iteration limit when greater than zero; `0` selects the node default. The help does not define the default count or handling of negative values. | This is the clearest mode rule in the registry help. The node's default and iteration loop were not verified in the binary. |
| `a.AnimNode.LegIK.PullDistribution` | float (`var`) | `0.5` | Distributes pull from foot (`0`) through balanced (`0.5`) to hip (`1`). The help does not specify interpolation or behavior outside that range. | Values and range landmarks are from registry help; no formula or clamping behavior was reconstructed. |
| `a.AnimNode.LegIK.TargetReachStepPercent` | float (`var`) | `0.7` | Sets `TargetReachStepPercent`; no further description is supplied. The name alone does not establish its unit, accepted range, or exact role in the solve. | The registry supplies a snapshot value only. No solver read or calculation was recovered. |

## What this establishes about overrides

All entries are registered as `var` in the community attachment, and the local build's string index contains them. This is evidence that they are CVar candidates associated with animation systems; it does not prove that the current client accepts a startup INI override or that a changed value reaches a live animation node. The saved address scan's `obj_rva` matches are registration/object-address evidence, not direct reads of the CVar's current value. No controlled in-game comparison was run for this batch.

The snapshot values must not be treated as canonical defaults. For an override experiment, change one entry at a time, keep a restorable copy of the config, and compare the same character and animation in the same scene. Keep debug switches separate from behavior changes so an observed visualization is not mistaken for a gameplay or performance effect.

## Sources and related notes

- Registry descriptions and captured values come from the community attachments listed in [Evidence, sources, and scope](EVIDENCE.md).
- Local build string inventory: [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
- Nearby printable strings (context only, not verified code references): [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
- Address-scan interpretation and limitations: [the static-analysis method notes](EVIDENCE.md#method-and-reproducibility).
