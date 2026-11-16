# Chaos Immediate Physics timing and runtime CVars

This guide covers the 15 `p.Chaos.ImmPhys.*` entries outside the collision, inertia-conditioning, and joint groups. Evidence combines the community registry with direct reference-address reads in Marvel Rivals Shipping build `1.1.4042190`. Snapshot values are captured values, not verified engine defaults or recommended overrides.

## Time-step selection and iteration overrides

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.ImmPhys.DeltaTimeCount` | int32 | `100` | Number of ticks used for the moving-average time calculation, per registry help. Initialization copies the value into the timing state at `0x143FDE23D`–`0x143FDE249`; the state also tracks the initial seed step. |
| `p.Chaos.ImmPhys.InitialStepTime` | float | `0.033` | Initial step time before calculation from the rolling average, per help. The value is converted to double and stored as the current step-time seed at `0x143FDE220`–`0x143FDE23C`; the sample counter is initialized to one. |
| `p.Chaos.ImmPhys.FixedStepTime` | float | `-1` | Help defines positive as fixed-step mode, zero as variable-step mode, and negative as PhysicsAsset-defined mode. Read at `0x143FFE34D` in the step setup. The downstream dispatch uses the value alongside computed step state; the complete mode path is not reconstructed here. |
| `p.Chaos.ImmPhys.StepTime` | float | `0` | Override step time when nonzero, per help. The local path at `0x143FFE833` only replaces the working step when the value is positive. |
| `p.Chaos.ImmPhys.MinStepTime` | float | `0.01` | When nonzero, if the calculated step is lower than this value, switch to fixed-step mode using this timestep, per help. Read at `0x143FFE861`; the path compares it with the candidate step and raises a smaller candidate to the threshold. |
| `p.Chaos.ImmPhys.FixedStepTolerance` | float | `0.05` | Fraction of fixed-step time required for a remainder to count as another step, per help. Read at `0x143FFE89B`; code multiplies it by the working step duration and compares that threshold with the remaining time. |
| `p.Chaos.ImmPhys.NumSteps` | int32 | `0` | Override number of simulation steps when nonzero, per help. The local path at `0x143FFE844` replaces the calculated count only for a positive value. |
| `p.Chaos.ImmPhys.PositionIterations` | int32 | `-1` | Override the position-loop count when nonnegative, per help. Read at `0x143FFE374`; negative values take the no-override branch. The application path caps the selected value at `127` before passing the iteration setting onward. |
| `p.Chaos.ImmPhys.VelocityIterations` | int32 | `-1` | Override the velocity-loop count when nonnegative, per help. Read at `0x143FFE36D`; negative values take the no-override branch. The applied value is capped at `127` before being stored in an 8-bit field at `0x143FFE44E`–`0x143FFE49F`. |
| `p.Chaos.ImmPhys.ProjectionIterations` | int32 | `-1` | Override the projection-loop count when nonnegative, per help. Read at `0x143FFE35D`; negative values take the no-override branch. The applied value is capped at `127` before being stored in an 8-bit field at `0x143FFE4A2`–`0x143FFE4E3`. |

### How the step controls interact

The local code indicates a layered choice: initialize from `InitialStepTime`, maintain rolling-average state using `DeltaTimeCount`, optionally use `StepTime`, and then select or constrain the step according to fixed-step settings and `MinStepTime`. `NumSteps` can override the resulting count. The `FixedStepTolerance` read scales the remainder threshold relative to the working step duration. This describes the observed local data flow, not a recommendation; interactions with asset-defined modes and all boundary cases remain partly unresolved.

## Other runtime settings

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.ImmPhys.DisableInactiveByIndex` | int32 | `1` | Help says to disable bodies that are no longer active by index rather than by count. The value is tested at `0x143FFD962` and `0x143FFD9F5`; this proves the switch gates two relevant paths, but the complete body-state update is not traced. |
| `p.Chaos.ImmPhys.NumCollisionsPerBlock` | int32 | `50` | Collision-pool block size. Registry help says a larger block improves cache efficiency but can waste memory when the pool does not need that many. Read at `0x143FDE064` and passed as an argument to helper `0x142913B80` at `0x143FDE08E`; the allocator's exact block policy is not recovered. |
| `p.Chaos.ImmPhys.SimSpaceCentrifugalAlpha` | float | `1` | Registry help groups this with settings for the simulation-space system for rigid-body nodes. Read at `0x143FFDCB4` and copied into a settings field at offset `0xBF8`. The exact coefficient/application formula is unresolved. |
| `p.Chaos.ImmPhys.SimSpaceCoriolisAlpha` | float | `0.5` | Same registry help group. Read at `0x143FFDCC7` and copied into a settings field at offset `0xBF0`; exact formula is unresolved. |
| `p.Chaos.ImmPhys.SimSpaceEulerAlpha` | float | `1` | Same registry help group. Read at `0x143FFDCDA` and copied into a settings field at offset `0xC00`; exact formula is unresolved. |

## Evidence and limits

- Names, types, help, and `ref_rva` values come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); captured values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The source manifest records that the Discord attachments match these preserved inputs byte for byte.
- The code locations correspond to direct reads identified in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and checked in the local executable's `.text` disassembly. These reads establish data flow and branch gates, but several helper implementations and final physics outcomes remain untraced.
- No controlled in-game changes were tested. Do not interpret snapshot values as defaults or suggested tuning values.

Related guides: [Immediate Physics collision and inertia CVars](cvar-chaos-immphys-collision-inertia.md), [Immediate Physics joint CVars](cvar-chaos-immphys-joints.md), [Chaos solver CVars](cvar-chaos-solver-joint.md), and [CVar overrides and loader syntax](cvar-overrides.md).
