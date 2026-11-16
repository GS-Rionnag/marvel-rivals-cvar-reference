# Vehicle debug and visualization CVar batch D

This page covers 23 exact `p.Vehicle.*` names from the preserved community registry. The attachment does not identify the game build or capture method. Help text is reproduced as the source's stated purpose; `CVarDump.txt` values are captured values, not confirmed defaults.

## Debug visualization toggles

The following fifteen entries are `ref` booleans. The help describes vehicle debug visualizations. Their snapshot values are all `false`.

| Exact name | Community help | Local build evidence |
| --- | --- | --- |
| `p.Vehicle.ShowAerofoilForces` | Enable/Disable Aerofoil Force Visualisation. | One `ref_rva` address-taking candidate; no direct value-read candidate in the saved scan. |
| `p.Vehicle.ShowAerofoilSurface` | Enable/Disable a very approximate visualisation of where the Aerofoil surface is located and its orientation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowAllForces` | Enable/Disable Force Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowBatchQueryExtents` | Enable/Disable Suspension Forces Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowCOM` | Enable/Disable Center Of Mass Debug Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowModelOrigin` | Enable/Disable Model Origin Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowRaycastComponent` | Enable/Disable Raycast Component Hit Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowRaycastMaterial` | Enable/Disable Raycast Material Hit Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowStepAssist` | Enable/Disable Step Assist Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowStepClimb` | Enable/Disable StepClimb visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowSuspensionForces` | Enable/Disable Suspension Forces Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowSuspensionLimits` | Enable/Disable Suspension Limits Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowSuspensionRaycasts` | Enable/Disable Suspension Raycast Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowWheelCollisionNormal` | Enable/Disable Wheel Collision Normal Visualisation. | One address-taking candidate; no direct value-read candidate. |
| `p.Vehicle.ShowWheelForces` | Enable/Disable Wheel Forces Visualisation. | One address-taking candidate; no direct value-read candidate. |

The saved scanner found only `lea` address-taking instructions for these fifteen `ref_rva` targets in the installed Shipping executable. Taking a variable's address is not a value read. This negative result is scoped to direct RIP-relative references in the scanned `.text`; indirect accesses, other modules, and paths outside the scan can be missed. The scan does not prove these toggles are unused, nor does it establish that debug rendering is active or visible in normal matches.

## Vehicle behavior settings with direct value-reference candidates

| Exact name | Type | Captured snapshot | Community help | Local build evidence |
| --- | --- | ---: | --- | --- |
| `p.Vehicle.SleepCounterThreshold` | float | `15` | Set The Sleep Counter Iteration Threshold. | At `0x1456865A0`, `comiss` compares an `xmm0` value against the CVar storage. This confirms a floating-point comparison, but the compared quantity and resulting sleep behavior are not recovered here. |
| `p.Vehicle.SteeringOverride` | float | `0` | Hard code steering input on. | A float load occurs at `0x1456A35CD` in a vehicle-related path. The help suggests an input override, but the surrounding conditions, valid range, and exact effect were not followed. |
| `p.Vehicle.ThrottleOverride` | float | `0` | Hard code throttle input on. | Float loads occur at `0x14568F31D` and `0x14568F33A`. The help suggests an input override; the exact branch conditions, units/range, and resulting vehicle behavior remain unresolved. |
| `p.Vehicle.TraceTypeOverride` | int32 | `0` | Override ray trace type, 1=Simple, 2=Complex. | Integer loads occur at `0x1456A0F00` and `0x1456A1913`. These show two local reads, but do not establish when either trace path runs or which values besides `1` and `2` are accepted. |

## Vehicle visual-logger settings

These four entries are `kind=var`. Their `ref_rva` is zero, so the saved direct-value scanner has no variable-storage target to follow. The local `obj_rva` matches are address-taking and QWORD writes, consistent with object/registration setup; they are not evidence that runtime code reads the value.

| Exact name | Type | Captured snapshot | Community help | Local evidence and limit |
| --- | --- | ---: | --- | --- |
| `p.Vehicle.VLog` | int32 | `0` | Vehicle Visual Logger category bitmask: `1` lifecycle, `2` raw input, `4` game-thread input, `8` async, `16` physics, `32` wheel, `64` network, `128` camera. | Bit meanings come from community help. No local value consumer was established. |
| `p.Vehicle.VLog.ErrorDistCm` | float | `30` | Vehicle VLOG correction distance in centimeters that upgrades network correction entries to warnings. | Help describes a warning threshold; no local value consumer was established. |
| `p.Vehicle.VLog.OwnerFilter` | FString | *(empty)* | Only emit vehicle VLOG for actors whose name or path contains this text. | Help describes a string filter; no local value consumer was established. |
| `p.Vehicle.VLogIncludeRemote` | int32 | `0` | Include simulated proxies and other remote client vehicles in `p.Vehicle.VLog` output. | Help describes which vehicles to include; no local value consumer was established. |

## Loader expression versus game editability

The supplied override loader `[Overrides]` syntax can express lines such as `p.Vehicle.ShowCOM=true` or `p.Vehicle.ThrottleOverride=0.5`. That only establishes that the loader format can express an assignment. There is no controlled runtime test showing that this build accepts the assignment, keeps the value after startup, or produces the described effect. The fifteen visualization toggles are especially uncertain because the local scan found no direct value reads. See [the editability evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) and [live-dump feasibility](cvar-overrides.md#can-a-normal-packaged-mod-list-the-live-cvar-registry).

## Sources

- Exact names, types, help, and reference RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); values are not treated as defaults.
- Instruction candidates and scan limitations: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and [local scan notes](EVIDENCE.md#build-specific-static-analysis).
- Related pages: [vehicle client-state batch A](cvar-vehicle-clientstate-driven.md), [batch B](cvar-vehicle-clientstate-batch-b.md), and [batch C](cvar-vehicle-batch-c.md).
