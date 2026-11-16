# Vehicle CVars: validation and force controls

This page covers 25 exact `p.Vehicle.*` entries in the preserved community registry. The attachment does not identify the source game build or collection procedure. The help text is retained as the source's intended meaning; captured `CVarDump.txt` values are snapshots, not confirmed defaults or recommendations.

## Registry help and captured values

| Exact name | Type | Captured snapshot | Community help / supported reading |
| --- | --- | ---: | --- |
| `p.Vehicle.ClientStateDriven.Validation.SoftPositionResidual` | float | `25` | Trapezoidal-integration soft residual in centimeters. The help does not define the comparison formula or disposition. |
| `p.Vehicle.ClientStateDriven.Validation.SoftRotationResidualDegrees` | float | `5` | Angular-integration soft residual in degrees. The exact error calculation is not supplied. |
| `p.Vehicle.ClientStateDriven.Validation.SuspicionDecayPerSecond` | float | `0.25` | Server monotonic-time suspicion decay rate. The score scale and update cadence are unspecified. |
| `p.Vehicle.ClientStateDriven.Validation.SuspicionPerSoftAnomaly` | float | `1` | Suspicion increment per soft anomaly. The anomaly categories are not listed in this row. |
| `p.Vehicle.ClientStateDriven.Validation.SuspicionThreshold` | float | `5` | Suspicion score at which a soft disagreement becomes a physical rejection. The exact rejection response is not described. |
| `p.Vehicle.ClientStateDriven.Validation.TimeBudgetSlack` | float | `0.05` | Server-time budget slack, in seconds. The associated time-budget calculation is unspecified. |
| `p.Vehicle.ClientStateDriven.Validation.TimeRateAllowance` | float | `1.1` | Maximum cumulative client-time rate relative to authorized server time dilation. The exact accounting window is unspecified. |
| `p.Vehicle.ControlInputWakeTolerance` | float | `0.02` | Control-input wake tolerance. The help does not define whether this is an absolute or normalized threshold. |
| `p.Vehicle.DisableAerodynamics` | bool | `false` | Help says this disables/enables aerodynamic drag and downforce forces. |
| `p.Vehicle.DisableAerofoils` | bool | `false` | Help says this disables/enables aerofoil forces. |
| `p.Vehicle.DisableConstraintSuspension` | bool | `false` | Help says this switches from constraint-based suspension to basic force-based suspension without hardstops. |
| `p.Vehicle.DisableFrictionForces` | bool | `false` | Help says this disables/enables wheel-friction forces. |
| `p.Vehicle.DisableRollbarForces` | bool | `false` | Help says this disables/enables rollbar forces. |
| `p.Vehicle.DisableStabilizeControl` | bool | `false` | Help says this disables/enables position-stabilization control. |
| `p.Vehicle.DisableSuspensionForces` | bool | `false` | Help says this disables/enables suspension forces. |
| `p.Vehicle.DisableThrusters` | bool | `false` | Help says this disables/enables thruster forces. |
| `p.Vehicle.DisableTorqueControl` | bool | `false` | Help says this disables/enables direct torque control. |
| `p.Vehicle.DisableVehicleSleep` | bool | `false` | Help says this disables aggressive vehicle sleeping. The sleep policy is not defined further. |
| `p.Vehicle.EnableMultithreading` | bool | `true` | Help says this enables multithreading of vehicle updates. |
| `p.Vehicle.LogStepClimb` | bool | `false` | Help says this enables detailed step-climb logs. |
| `p.Vehicle.OverlapTestExpansionXY` | float | `100` | Expands the raycast overlap-test bounding box in the X/Y axes. Units and whether the value is a total or per-side expansion are not stated. |
| `p.Vehicle.OverlapTestExpansionZ` | float | `50` | Expands the raycast overlap-test bounding box on the Z axis. Units and whether the value is a total or per-side expansion are not stated. |
| `p.Vehicle.ResetMeasurements` | bool | `false` | Help says this resets vehicle performance measurements. Trigger timing and what counters are cleared are unspecified. |
| `p.Vehicle.SetForceDebugScaling` | float | `0.0006` | Help says this sets force-visualization scaling. It does not describe the drawn vectors or scale conversion. |
| `p.Vehicle.SetMaxMPH` | float | `0` | Help says this sets a top speed in MPH affecting all vehicles. The zero-value behavior and conversion path are not explained. |

The names and detailed vehicle/network descriptions above come from community help, not an independently checked game source. In particular, the `ClientStateDriven.Validation.*` entries read like server-side validation/tuning fields, but that reading is still based on the help wording.

## Local build evidence

The installed Shipping binary inventory lists these names as strings. In the saved x64 address scan for build `1.1.4042190`, 16 entries have at least one direct-memory candidate at their `ref_rva`:

- `ControlInputWakeTolerance` and `SetMaxMPH` have direct floating-point loads.
- The `Disable*` controls, `EnableMultithreading`, and `LogStepClimb` have direct byte comparisons in local code.
- `OverlapTestExpansionXY` and `OverlapTestExpansionZ` are both loaded as floats in the same nearby overlap-test path.

These instruction matches establish local code reads/tests at the matched addresses, not that the path runs in a normal match, that override loader applies an override to the live CVar, or that any visible result occurs. The saved scan does not provide sufficient surrounding control-flow evidence to map every comparison to its exact helper/effect.

The two `ref` entries `p.Vehicle.ResetMeasurements` and `p.Vehicle.SetForceDebugScaling` had only address-taking matches in this scan, not direct CVar-value reads. The seven `ClientStateDriven.Validation.*` entries in this page are `kind=var` with `ref_rva=0`; their matching scanner rows address `obj_rva` and do not establish reads of their values. These are open cases, not proof that the settings are unused. The scan can miss indirect/non-RIP-relative access or code in other modules.

No exact Epic UE 5.9 reference match supplies an upstream definition for these names. Their community help remains the only source for the plain-language meanings in this page.

## Loader syntax versus runtime editability

The supplied override loader template can express an assignment such as `p.Vehicle.DisableAerodynamics=true` below `[Overrides]`. That shows only that the loader format can express a key/value line. It does not confirm that Marvel Rivals registers the key in the installed build, accepts the loader's config source/priority, preserves the changed value through startup, executes the relevant code path, or produces an in-game effect. No runtime override test was performed for these entries. See [CVar override evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) and [live registry dump feasibility](cvar-overrides.md#can-a-normal-packaged-mod-list-the-live-cvar-registry).

## Sources

- Names, kinds, types, help, and reference addresses: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); they are not asserted as defaults.
- Static address hits and scan limitations: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and [source notes](EVIDENCE.md#build-specific-static-analysis).
- Related vehicle batches: [vehicle client-state controls, batch A](cvar-vehicle-clientstate-driven.md) and [batch B](cvar-vehicle-clientstate-batch-b.md).
