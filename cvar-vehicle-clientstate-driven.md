# Vehicle client-state-driven CVars

This page covers 25 exact `p.Vehicle.*` names from the preserved community `console_vars.tsv` and snapshot. The registry attachment does not identify its game build or collection method. Captured values are snapshots, not proven defaults or recommendations.

## Registry descriptions and captured values

| Exact name | Registry kind/type | Snapshot | Registry help / supported reading |
| --- | --- | ---: | --- |
| `p.Vehicle.BatchQueries` | `ref` / bool | `false` | Enables or disables batching of suspension raycasts. |
| `p.Vehicle.CacheSuspensionOffset` | `ref` / bool | `true` | Caches a trace for animation optimization. The help does not define the cache lifetime or trace inputs. |
| `p.Vehicle.CacheTraceOverlap` | `ref` / bool | `false` | Enables caching of the suspension trace overlap test; the help says it is valid only when `BatchQueries` is enabled. |
| `p.Vehicle.ClientStateDriven.ActiveHoldSeconds` | `var` / float | `0.2` | Minimum time to keep active-cadence publication after input, wake, collision, depenetration, correction, or velocity activity. |
| `p.Vehicle.ClientStateDriven.ActivePublicationHz` | `var` / float | `30` | Owning-client publication rate while moving or inside the active hold window. |
| `p.Vehicle.ClientStateDriven.Correction.DynamicImpulseRecoveryThreshold` | `var` / float | `5000` | Claimed WorldDynamic normal impulse threshold above which missing trusted history terminates the Epoch. |
| `p.Vehicle.ClientStateDriven.Correction.MaximumDriveAcceleration` | `var` / float | `3000` | Server cap, in cm/s², for tuning-derived longitudinal acceleration in an approximate transaction. |
| `p.Vehicle.ClientStateDriven.Correction.MaximumYawAcceleration` | `var` / float | `8` | Server cap, in rad/s², for inertia-based steering integration in one approximate transaction. |
| `p.Vehicle.ClientStateDriven.Correction.OwnerHardPositionCentimeters` | `var` / float | `300` | Position-error threshold at or above which the owning client performs a physical hard set. |
| `p.Vehicle.ClientStateDriven.Correction.OwnerHardRotationDegrees` | `var` / float | `45` | Rotation-error threshold at or above which the owning client performs a physical hard set. |
| `p.Vehicle.ClientStateDriven.Correction.OwnerHardVelocityCentimetersPerSecond` | `var` / float | `2000` | Linear-velocity-error threshold at or above which the owning client performs a physical hard set. |
| `p.Vehicle.ClientStateDriven.Correction.OwnerHistorySeconds` | `var` / float | `2` | Owning-client history window keyed by AuthorityEpoch and InputSequence. |
| `p.Vehicle.ClientStateDriven.Correction.OwnerSmoothSeconds` | `var` / float | `0.15` | Physical transform and velocity reconciliation duration for an ordinary correction. |
| `p.Vehicle.ClientStateDriven.Correction.PresentationSmoothSeconds` | `var` / float | `0.12` | Mesh/camera relative-transform decay used to hide a required physical hard set. |
| `p.Vehicle.ClientStateDriven.Correction.ResponseRateHz` | `var` / float | `10` | Maximum reliable rate for ordinary correction responses; suppressed responses are replaced by the newest result. |
| `p.Vehicle.ClientStateDriven.Diagnostics` | `var` / int32 | `0` | Help defines `0` as off, `1` as bounded summaries/warnings, and `2` as verbose cadence and traffic decisions. |
| `p.Vehicle.ClientStateDriven.EpochMaxSends` | `var` / int32 | `5` | Maximum sends for one Epoch handshake. On exhaustion, the help says the server keeps full simulation without disconnecting the owner. |
| `p.Vehicle.ClientStateDriven.EpochRetrySeconds` | `var` / float | `0.5` | Delay between reliable Epoch baseline retries; retries reuse the same authority Epoch and BaselineToken. |
| `p.Vehicle.ClientStateDriven.Fallback.InputDecaySeconds` | `var` / float | `0.35` | Time after the grace interval over which continuous controls decay to neutral and safe braking is raised. |
| `p.Vehicle.ClientStateDriven.Fallback.InputGraceSeconds` | `var` / float | `0.15` | Time full-simulation fallback may retain the last legal continuous input; the help says gear events are never retained. |
| `p.Vehicle.ClientStateDriven.Fallback.SafeBrakeInput` | `var` / float | `0.75` | Server-owned braking target after a stream fallback. |
| `p.Vehicle.ClientStateDriven.Fallback.ViolationHoldEnabled` | `var` / int32 | `0` | Optional prolonged server-full-simulation response after a protocol/physical violation; help says disabled by default. |
| `p.Vehicle.ClientStateDriven.Fallback.ViolationHoldSeconds` | `var` / float | `2` | Duration of an optional violation-triggered server-full-simulation hold; the help says timeout/disconnect fallback remains enabled regardless. |
| `p.Vehicle.ClientStateDriven.IdleAngularVelocityThreshold` | `var` / float | `1` | Maximum chassis angular speed allowed for idle publication cadence. |
| `p.Vehicle.ClientStateDriven.IdleHoldSeconds` | `var` / float | `0.5` | Continuous quiet time required before client-state-driven publication enters idle cadence. |

The `ClientStateDriven` wording and the detailed networking/physics descriptions above are transcribed from community help. They describe intended roles, not a validated explanation of the full vehicle protocol. The snapshot values must not be treated as recommended tuning values.

## Local build evidence

The local build inventory lists all 25 names as printable strings in both `Marvel Rivals Shipping executable` and a second platform-specific Shipping executable. String presence proves only that the names are in those binaries.

For the three `ref` entries, the saved x64 address scan found direct reads of the reference addresses in the local Shipping executable:

- `p.Vehicle.BatchQueries`: byte comparison at VA `0x1456A09DC`.
- `p.Vehicle.CacheTraceOverlap`: byte comparison at VA `0x1456A09FB`.
- `p.Vehicle.CacheSuspensionOffset`: byte comparison at VA `0x14569D270`.

These are direct value reads, consistent with the described boolean gates. The scan does not by itself prove those paths execute during a normal match or that the mod loader's requested value reaches them.

The remaining 22 `ClientStateDriven` rows are `kind=var` and have `ref_rva=0x0`. In the saved address-hit TSV, their matches target `obj_rva` and are address-taking or QWORD writes; no direct CVar-value reads were located for these entries by that scan. The presence of the names, detailed community help, and snapshot values does not resolve whether the current build registers them for config application or whether their consumers are active. Do not interpret the object-address writes as proof of runtime use.

## Loader editability and limits

The supplied loader template can express these as `name=value` lines below `[Overrides]`. That is syntax-level editability only. For example:

```ini
[Overrides]
p.Vehicle.ClientStateDriven.Diagnostics=1
```

No controlled runtime override test was performed for this family. In particular, loader acceptance, game CVar-manager acceptance, persistence against later settings, execution of the relevant code path, and an observable in-game behavior change remain separate unverified questions. The loader's stated policy also ignores settings that can remove smoke or other effects. See [CVar override evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) before treating any setting as usable.

## Sources

- Registry, snapshot, build identity, and scan limitations: [CVar research source notes](EVIDENCE.md#build-specific-static-analysis), `console_vars.tsv`, `CVarDump.txt`, and `build-4042190-cvar-address-hits.tsv`.
- Local printable-name matches: [CVar strings in build 4042190](EVIDENCE.md#build-specific-static-analysis).
- Loader syntax and the distinction between config syntax and proven game behavior: [CVar overrides](cvar-overrides.md).
