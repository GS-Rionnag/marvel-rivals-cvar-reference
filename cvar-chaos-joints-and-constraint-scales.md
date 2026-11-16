# Chaos joint and joint-constraint CVars

This guide covers the eight `p.Chaos.Joint.*` and thirteen `p.Chaos.JointConstraint.*` registry variables. It combines the supplied registry with direct reads in Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified defaults or recommendations.

## Joint behavior settings

| CVar | Type | Snapshot | Registry meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Joint.AngularVelocityThresholdToApplyRestitution` | float | `0.01` | In Quasipbd, apply restitution only when initial angular velocity exceeds this threshold. Read from the registered value in several code paths, including `0x1428D50FD`, `0x1428D5311`, `0x1428F1DD6`, and `0x1428F2979`. |
| `p.Chaos.Joint.DegenerateRotationLimit` | float | `-0.998` | Cosine of the swing angle considered degenerate; help gives `cos(176°)` as the default reference. Read at `0x1428E08BA`, `0x1428F1CA6`, `0x1428FA645`, and `0x1428FD3F7`. The snapshot `-0.998` is close to, but not exactly, the stated cosine reference. |
| `p.Chaos.Joint.DisableSoftLimits` | bool | `false` | Debug switch to disable soft limits. The byte is checked in three separate branches at `0x14293B649`, `0x14293B6A9`, and `0x14293B709`; the complete limit-solving effects are not followed here. |
| `p.Chaos.Joint.LinearVelocityThresholdToApplyRestitution` | float | `0.01` | In Quasipbd, apply restitution only when initial linear velocity exceeds this threshold. Read at `0x1428D7733`, `0x1428F2FDE`, `0x1428F30BE`, `0x1428F44A5`, and `0x1428F5120`. |
| `p.Chaos.Joint.MultiDimension` | int32 | `1` | No help text is present in either community table, and the saved scanner output has no direct reference-value read candidate. Meaning and runtime effect remain unknown. |
| `p.Chaos.Joint.NewProjection` | bool | `true` | Selects the new joint projection algorithm, per help. The switch is read at `0x1428D5D66`; the selected branch's implementation is not fully mapped here. |
| `p.Chaos.Joint.Plasticity.ClampToLimits` | bool | `true` | Clamps drive position targets to their defined limits after plasticity computation, per help. The saved scanner has no direct reference-value read candidate, so the local build's use is not independently confirmed. |
| `p.Chaos.Joint.VelProjectionAlpha` | float | `0.1` | Fraction of velocity correction applied during projection; help equates it to `1 - damping` for the projection velocity delta. Read at `0x1428D8148` and `0x1428F93C8`. |

## Joint-constraint conversion settings

The local binary contains small scalar-return routines for the scale entries: each loads the corresponding CVar, converts its float value to double, and returns it. This establishes that the value is exposed to the consuming code as a conversion factor; it does not reveal every downstream multiplication or resulting physical effect.

| CVar | Type | Snapshot | Registry meaning and local accessor |
| --- | --- | ---: | --- |
| `p.Chaos.JointConstraint.AngularBreakScale` | float | `1` | Conversion factor for angular break threshold. Read and returned by the accessor at `0x142B9E2A0`. |
| `p.Chaos.JointConstraint.AngularDriveDampingScale` | float | `1.5` | Conversion factor for angular drive damping. Accessor at `0x142B9E2B0`. |
| `p.Chaos.JointConstraint.AngularDriveStiffnessScale` | float | `1.5` | Conversion factor for angular drive stiffness. Accessor at `0x142B9E2C0`. |
| `p.Chaos.JointConstraint.JointStiffness` | float | `1` | Hard-joint solver stiffness. Accessor at `0x142BA2CF0`. |
| `p.Chaos.JointConstraint.LinaearDriveDampingScale` | float | `1` | Conversion factor for linear drive damping. The misspelling `Linaear` is the exact registered key. Accessor at `0x142BA2D50`. |
| `p.Chaos.JointConstraint.LinearBreakScale` | float | `1` | Conversion factor for linear break threshold. Accessor at `0x142BA2D40`. |
| `p.Chaos.JointConstraint.LinearDriveStiffnessScale` | float | `1` | Conversion factor for linear drive stiffness. Accessor at `0x142BA2D60`. |
| `p.Chaos.JointConstraint.SoftAngularDampingScale` | float | `1000` | Conversion factor for soft-joint angular damping. Accessor at `0x142BA69F0`. |
| `p.Chaos.JointConstraint.SoftAngularForceMode` | int32 | `0` | Soft angular constraint force mode; help lists `0: Acceleration` and `1: Force` but the source help text is truncated after “Force”. Getter at `0x142BA6A00`. |
| `p.Chaos.JointConstraint.SoftAngularStiffnessScale` | float | `100000` | Conversion factor for soft-joint angular stiffness. Accessor at `0x142BA6A10`. |
| `p.Chaos.JointConstraint.SoftLinearDampingScale` | float | `1.2` | Conversion factor for soft-joint linear damping. Accessor at `0x142BA6A20`. |
| `p.Chaos.JointConstraint.SoftLinearForceMode` | int32 | `0` | Soft linear constraint force mode; help lists `0: Acceleration` and `1: Force` but the source help text is truncated after “Force”. Getter at `0x142BA6A30`. |
| `p.Chaos.JointConstraint.SoftLinearStiffnessScale` | float | `1.5` | Conversion factor for soft-joint linear stiffness. Accessor at `0x142BA6A40`. |

## Evidence and limits

- Names, types, help, and reference addresses come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), with alternate object help from [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and captured values from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The source manifest records that the Discord attachments match these preserved files byte for byte.
- Direct read candidates come from [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), with instruction semantics checked in the local executable disassembly. A missing scanner read is not proof the CVar is unused: indirect access and accesses outside the scanned instruction patterns can be missed.
- No controlled in-game CVar changes were tested. Do not interpret snapshot values as defaults or tuning recommendations.

Related guides: [Immediate Physics joint CVars](cvar-chaos-immphys-joints.md), [Chaos solver joint CVars](cvar-chaos-solver-joint.md), [Chaos collision CVars](cvar-chaos-collision-tolerances.md), and [CVar overrides and loader syntax](cvar-overrides.md).
