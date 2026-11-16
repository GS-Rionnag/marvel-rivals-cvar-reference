# Chaos Immediate Physics joint CVars

This guide covers all 25 `p.Chaos.ImmPhys.Joint.*` registry entries in the supplied community table. It separates the registry's descriptions and captured values from what the installed Marvel Rivals Shipping build `1.1.4042190` does with the values. Captured values are not engine defaults or recommended settings.

## What the local binary shows

The local executable reads all 25 reference addresses in one joint-settings assembly path at `0x143FFE54C`–`0x143FFE70A`. Integer switches are converted from zero/nonzero to booleans, while float settings are copied into a temporary settings bundle. The routine passes that bundle and the shock-propagation iteration count to helper `0x142943DD0` at `0x143FFE70F`. This confirms the values feed a joint-settings path in this build; the helper's full implementation and the resulting physics response have not been reconstructed here.

`UseLinearSolver` is read earlier at `0x143FFE3A9` in the surrounding setup. Its registry help says `-1` delegates to the PhysicsAsset setting. The exact mode-selection logic is not fully resolved in this guide.

## Registry entries

| CVar | Type | Snapshot | Registry help and interpretation |
| --- | --- | ---: | --- |
| `p.Chaos.ImmPhys.Joint.AngleTolerance` | float | `0.001` | `AngleTolerance.` Names an angular tolerance; units and threshold use are not specified by this help. Read at `0x143FFE5C1`. |
| `p.Chaos.ImmPhys.Joint.AngularDriveDamping` | float | `-1` | Override 6DoF joint drive damping only when greater than zero. Read at `0x143FFE6EA`. |
| `p.Chaos.ImmPhys.Joint.AngularDriveStiffness` | float | `-1` | Override 6DoF joint drive stiffness only when greater than zero. Read at `0x143FFE6F7`. |
| `p.Chaos.ImmPhys.Joint.AngularProjection` | float | `-1` | Override the 6DoF joint projection amount when the value is nonnegative. Read at `0x143FFE622`. |
| `p.Chaos.ImmPhys.Joint.EnableDrives` | int32 | `1` | Enables/disables drives; zero/nonzero is converted to a boolean at `0x143FFE5F9`. |
| `p.Chaos.ImmPhys.Joint.EnableSwingLimits` | int32 | `1` | Enables/disables swing limits; zero/nonzero is converted to a boolean at `0x143FFE5DF`. |
| `p.Chaos.ImmPhys.Joint.EnableTwistLimits` | int32 | `1` | Enables/disables twist limits; zero/nonzero is converted to a boolean at `0x143FFE5BA`. |
| `p.Chaos.ImmPhys.Joint.LinearDriveDamping` | float | `-1` | Override 6DoF joint drive damping only when greater than zero. Read at `0x143FFE6D7`. |
| `p.Chaos.ImmPhys.Joint.LinearDriveStiffness` | float | `-1` | Override 6DoF joint drive stiffness only when greater than zero. Read at `0x143FFE6CA`. |
| `p.Chaos.ImmPhys.Joint.LinearProjection` | float | `-1` | Override the 6DoF joint projection amount when the value is nonnegative. Read at `0x143FFE639`. |
| `p.Chaos.ImmPhys.Joint.MaxInertiaRatio` | float | `5` | 6DoF joint maximum inertia ratio override when greater than zero. Read at `0x143FFE5EC`. The ratio's calculation is not documented by the registry help. |
| `p.Chaos.ImmPhys.Joint.MinParentMassRatio` | float | `0.2` | 6DoF joint minimum parent-mass ratio override when greater than zero. Read at `0x143FFE5D7`. |
| `p.Chaos.ImmPhys.Joint.NumShockPropagationIterations` | int32 | `-1` | Number of shock-propagation iterations. Read at `0x143FFE6AC`; the registry help does not define special sentinel values. |
| `p.Chaos.ImmPhys.Joint.PositionTolerance` | float | `0.025` | `PositionTolerance.` Names a positional tolerance; units and threshold use are not specified by this help. Read at `0x143FFE57E`. |
| `p.Chaos.ImmPhys.Joint.ShockPropagation` | float | `-1` | 6DoF joint shock-propagation override when the value is nonnegative. Read at `0x143FFE64C`. |
| `p.Chaos.ImmPhys.Joint.SoftLinearStiffness` | float | `-1` | Override 6DoF joint soft linear stiffness only when greater than zero. Read at `0x143FFE65C`. |
| `p.Chaos.ImmPhys.Joint.SoftSwingDamping` | float | `-1` | Override 6DoF joint soft-swing damping only when greater than zero. Read at `0x143FFE69C`. |
| `p.Chaos.ImmPhys.Joint.SoftSwingStiffness` | float | `-1` | Override 6DoF joint soft-swing stiffness only when greater than zero. Read at `0x143FFE689`. |
| `p.Chaos.ImmPhys.Joint.SoftTwistDamping` | float | `-1` | Override 6DoF joint soft-twist damping only when greater than zero. Read at `0x143FFE67C`. |
| `p.Chaos.ImmPhys.Joint.SoftTwistStiffness` | float | `-1` | Override 6DoF joint soft-twist stiffness only when greater than zero. Read at `0x143FFE669`. |
| `p.Chaos.ImmPhys.Joint.SolvePositionLast` | int32 | `1` | Chooses position-then-rotation (`0`) or rotation-then-position (`1`, registry default). The zero/nonzero setting is converted to a boolean at `0x143FFE54C`. |
| `p.Chaos.ImmPhys.Joint.Stiffness` | float | `-1` | Override 6DoF joint stiffness when greater than zero. Read at `0x143FFE611`. |
| `p.Chaos.ImmPhys.Joint.SwingTwistAngleTolerance` | float | `1e-06` | `SwingTwistAngleTolerance.` Names a swing/twist angular tolerance; the unit and use are not specified by the short help. Read at `0x143FFE591`. |
| `p.Chaos.ImmPhys.Joint.UseLinearSolver` | int32 | `-1` | Force linear or nonlinear joint solver; `-1` uses the PhysicsAsset setting. Read at `0x143FFE3A9`. |
| `p.Chaos.ImmPhys.Joint.UsePBDDrives` | int32 | `1` | Chooses whether drives are solved in the position or velocity phase; help says the default is true. Zero/nonzero is converted to a boolean at `0x143FFE5A2`. |

## Evidence and limits

- Names, types, help, and `ref_rva` values come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); snapshot values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The Discord source attachments are byte-identical to the preserved files as recorded in the [source manifest](EVIDENCE.md#build-specific-static-analysis).
- Direct-reference candidates come from [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The instruction addresses above are from the executable's `.text` disassembly. They show values loaded or tested and routed into joint setup, not exact effects on an in-game joint.
- No in-game experiment is recorded. Do not treat the snapshot column as defaults or suggested overrides.

Related guides: [Immediate Physics collision and inertia CVars](cvar-chaos-immphys-collision-inertia.md), [Chaos solver joint CVars](cvar-chaos-solver-joint.md), [CVar overrides and loader syntax](cvar-overrides.md).
