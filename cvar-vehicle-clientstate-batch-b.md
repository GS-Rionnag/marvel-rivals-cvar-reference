# Vehicle client-state CVar batch B

This page records 25 exact `p.Vehicle.ClientStateDriven.*` entries from the preserved community registry. The attachment does not identify its game build or capture procedure. The help strings below describe the community source's claims; they are not independently validated explanations of the installed Marvel Rivals build.

## Registry help and captured values

All 25 entries are `kind=var`, with `ref_rva=0x0`. The values in the `CVarDump.txt` column are captured snapshot values, not confirmed defaults or recommended settings. Only `SyncMode` help explicitly labels a default.

| Exact name | Type | Captured snapshot | Community help |
| --- | --- | ---: | --- |
| `p.Vehicle.ClientStateDriven.IdleLinearVelocityThreshold` | float | `10` | Maximum chassis speed in cm/s permitted for idle publication cadence. |
| `p.Vehicle.ClientStateDriven.IdlePublicationHz` | float | `15` | Owning Client publication rate after the complete neutral/low-speed/no-collision idle hold. |
| `p.Vehicle.ClientStateDriven.LiveAcceptedDriftWarningDistance` | float | `50` | Live collision-carrier versus Accepted State drift in cm which emits a bounded outward-gather warning. |
| `p.Vehicle.ClientStateDriven.MaximumPacketDeltaTime` | float | `0.1` | Maximum simulated DeltaTime in one Reliable interval; larger accumulated spans are split without dropping time. |
| `p.Vehicle.ClientStateDriven.MeaningfulInputThreshold` | float | `0.02` | Absolute continuous input threshold which immediately selects active publication cadence. |
| `p.Vehicle.ClientStateDriven.MinimumEmergencyUploadInterval` | float | `0.02` | Minimum spacing between significant-collision emergency interval closes. |
| `p.Vehicle.ClientStateDriven.ServerMaxIntervalsPerFrame` | int32 | `4` | Per-vehicle cap for same-server-frame Reliable interval processing; overflow terminates the Epoch and recovers. |
| `p.Vehicle.ClientStateDriven.SignificantCollisionImpulseThreshold` | float | `1000` | Normal impulse magnitude which permits an emergency interval close. |
| `p.Vehicle.ClientStateDriven.Stream.ActiveTimeoutSeconds` | float | `0.5` | No-packet timeout for active Client-State-Driven traffic before mandatory full-simulation recovery. |
| `p.Vehicle.ClientStateDriven.Stream.IdleTimeoutSeconds` | float | `1` | No-packet timeout for genuinely idle Client-State-Driven traffic before mandatory full-simulation recovery. |
| `p.Vehicle.ClientStateDriven.SyncMode` | int32 | `0` | Server-controlled Chaos Vehicle synchronization mode. `0`: Legacy (help says default); `1`: ClientStateDriven. |
| `p.Vehicle.ClientStateDriven.Validation.HardPositionResidual` | float | `100` | Trapezoidal integration physical-rejection residual in cm. |
| `p.Vehicle.ClientStateDriven.Validation.HardRotationResidualDegrees` | float | `25` | Angular integration physical-rejection residual in degrees. |
| `p.Vehicle.ClientStateDriven.Validation.MaxAngularSpeed` | float | `20` | Server-owned chassis angular-speed limit in rad/s. |
| `p.Vehicle.ClientStateDriven.Validation.MaxDiscreteTransitions` | int32 | `1` | Maximum discrete gear transitions in one interval. |
| `p.Vehicle.ClientStateDriven.Validation.MaxInputRate` | float | `40` | Maximum continuous input units per second. |
| `p.Vehicle.ClientStateDriven.Validation.MaxIntervalDuration` | float | `0.1` | Maximum structurally consumable interval duration. |
| `p.Vehicle.ClientStateDriven.Validation.MaxLinearAcceleration` | float | `10000` | Server-owned chassis acceleration limit in cm/s^2. |
| `p.Vehicle.ClientStateDriven.Validation.MaxLinearSpeed` | float | `10000` | Server-owned chassis speed limit in cm/s. |
| `p.Vehicle.ClientStateDriven.Validation.MaxSceneQueriesPerServerFrame` | int32 | `256` | Server-wide cap on authority-validation scene queries per engine frame across all vehicles; exhaustion fails closed to full simulation + Epoch recovery. |
| `p.Vehicle.ClientStateDriven.Validation.MaxSweepAngularStepDegrees` | float | `10` | Maximum Root Chassis rotational query step in degrees. |
| `p.Vehicle.ClientStateDriven.Validation.MaxSweepSegmentLength` | float | `200` | Maximum Root Chassis sweep segment length in cm. |
| `p.Vehicle.ClientStateDriven.Validation.MaxSweepSegments` | int32 | `32` | Hard cap on Root Chassis WorldStatic sweep segments. |
| `p.Vehicle.ClientStateDriven.Validation.SleepAngularVelocityThreshold` | float | `0.5` | Maximum angular speed for client-proposed Sleep. |
| `p.Vehicle.ClientStateDriven.Validation.SleepLinearVelocityThreshold` | float | `5` | Maximum speed for client-proposed Sleep. |

The terms “Epoch,” “Accepted State,” “Root Chassis,” and “outward-gather” are retained from the supplied help. Their exact protocol/data-structure meanings have not been established independently.

## Local build scan

The saved address scan contains four `obj_rva` instruction candidates for each name: one address-taking `lea` and three `mov QWORD PTR [rip+...], register` writes. These are references to the registry's object-address field, not direct reads from a CVar value slot. No entry in this batch has a nonzero `ref_rva` in the community table, and the scan provides no local consumer/value-read evidence for this family. The scan is limited to direct RIP-relative references in the installed x64 Shipping executable; indirect accesses or code in other modules can be missed.

The registry and snapshot attachments do not identify a game build. Consequently, names and detailed help alone do not prove that build `1.1.4042190` registers these settings, accepts them from the loader, or executes the described vehicle behavior. The local evidence here is insufficient to classify any of these 25 as live, user-modifiable game controls.

## Loader syntax versus editability

The supplied override loader template can express a line such as `p.Vehicle.ClientStateDriven.SyncMode=1` under `[Overrides]`. That is syntax-level editability only. This batch has no runtime evidence showing that the game accepts an override, retains it after startup, or changes behavior. The distinctions and the recommended live-dump check are described in [CVar override evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) and [live registry dump feasibility](cvar-overrides.md#can-a-normal-packaged-mod-list-the-live-cvar-registry).

## Sources

- Registry help and reference metadata: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Address candidates and scan limitations: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and [CVar research source notes](EVIDENCE.md#build-specific-static-analysis).
- Related first batch: [Vehicle client-state-driven CVars](cvar-vehicle-clientstate-driven.md).
