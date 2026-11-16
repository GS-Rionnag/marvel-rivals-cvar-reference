# Ragdoll CVars

The community registry contains seventeen `a.ragdoll.*` `var`/`ref` entries: fourteen `ref` entries and three `var` entries. The table records each entry's registry kind, type, description, and separate `CVarDump.txt` snapshot. Snapshot values are not assumed to be defaults. The capture build and method are not identified.

| CVar | Kind | Type | Community help | Snapshot |
|---|---|---|---|---:|
| `a.ragdoll.DeactivateRagdollSpeedThreshold` | ref | float | Speed threshold to deactivate ragdoll when `DeactivateRagdollWhenSpeedLowerThanThreshold` is true; help states default `50`. | `50` |
| `a.ragdoll.DeactivateRagdollWhenSpeedLowerThanThreshold` | ref | bool | Whether to deactivate ragdoll when speed is lower than the threshold; help states default `true`. | `true` |
| `a.ragdoll.DeathAnimationComponentAsyncUpdate` | ref | bool | Whether to update `DeathAnimationComponent` asynchronously (`0` disable, `1` enable). | `false` |
| `a.ragdoll.DebugDeathAnimationComponent` | ref | bool | Whether to debug `DeathAnimationComponent` (`0` disable, `1` enable). | `false` |
| `a.ragdoll.DebugEnable` | ref | bool | Whether to debug ragdoll. | `false` |
| `a.ragdoll.ForceSetRagdollParams.Enable` | var | int32 | `0` uses physics-asset parameters (help marks this as default); `1` forces angular damping to `20.0` and gravity scale to `1.0`. | `0` |
| `a.ragdoll.GOffsetThresholdCanAvoidRagdollPassWalls` | ref | float | Offset threshold that can avoid ragdoll passing through walls; help states default `100`. | `100` |
| `a.ragdoll.ImpulseApplyRagdollByAbility` | ref | bool | Whether abilities may apply impulse to ragdolls; help states default `false`. | `false` |
| `a.ragdoll.ImpulseApplyRagdollByMove` | ref | bool | Whether character movement may apply impulse to ragdolls; help states default `false`. | `false` |
| `a.ragdoll.KineActorAddToSpatialAcceleration` | ref | bool | `0` keeps the death-animation joint anchor (`KineActor`) out of spatial acceleration and without collision (default); `1` restores its pre-exclusion behavior for A/B comparison. | No snapshot entry |
| `a.ragdoll.LODDistance` | ref | float | Empty. | `50000` |
| `a.ragdoll.MaxTargetOffsetOfPhysAnimationInDeath` | ref | float | Maximum target offset of physical animation during death; help states default `300`. | `300` |
| `a.ragdoll.PauseAnimInDeath` | ref | bool | Whether to pause animation during death. | `true` |
| `a.ragdoll.RagdollDelayHidden.Enable` | var | bool | `0` do not hide ragdoll; `1` hide ragdoll after a delay. | `false` |
| `a.ragdoll.RagdollDelayHiddenTime` | var | float | Delay before hiding ragdoll; help states default `3.0s`. | `3` |
| `a.ragdoll.SkipUpdateGameAC` | ref | bool | Whether to skip updating game spatial acceleration; help states default `true`. | `true` |
| `a.ragdoll.TraceGroundIntervalAfterStopRagdoll` | ref | float | Ground-trace interval after ragdoll stops. | `0.1` |

The community help defines the intended controls but is not a versioned game manual. Ten entries have help that states a default; nine corresponding snapshot values match, while `KineActorAddToSpatialAcceleration` has no snapshot entry. This agreement does not identify the capture build or establish runtime defaults in the installed game. The LOD distance has a snapshot value but no help text.

The full `.text` direct-reference scan produced at least one instruction candidate matching each of the fourteen community `ref_rva` values in the local build. This is a useful lead that the addresses are used, not a full registration or semantics proof for every row. The three `var` entries have `ref_rva=0`, so that scan cannot check them using this method. Address hits can reflect reads, writes, or initialization, and the community address convention is undocumented.

All seventeen entries are listed as `var` or `ref` console-variable rows, so the supplied loader format for a CVar override is `[Overrides]` followed by `name=value`. This establishes the config syntax only; the snapshots and help do not prove that every setting can be changed successfully or safely in the installed game.

## `a.ragdoll.LODDistance`

| Field | Evidence |
|---|---|
| Registry kind / type | `ref` / `float` |
| Community help | Empty |
| Community snapshot value | `50000` |
| Local build | Marvel Rivals Shipping `1.1.4042190` |

The snapshot value is a captured value, not a verified default or recommendation. The community registry does not identify its capture build or explain the setting.

## Static runtime use

The installed executable reads the variable's `ref_rva` storage (`0x14F9F3134`) in two code paths:

- At VA `0x146DC5793`, the code loads the float, multiplies it by itself, computes the squared distance between two 3D vectors, and compares the results. If the squared distance is greater than the squared setting, it enters an additional path; if the distance is less than or equal to the threshold, it skips that path.
- At VA `0x146DD6BFE`, a second path repeats the same pattern: square the CVar, calculate a squared 3D distance, and enter an update path only when the distance exceeds the squared threshold. That path sets a byte flag and calls a helper.

This supports describing the variable as a distance cutoff for ragdoll-related logic. The CVar name supplies the ragdoll association; the disassembly establishes the threshold comparison and branch, but does not identify the compared objects' source types or fully establish what the extra/update paths do. The code squares the setting before comparison, so this check does not use the sign of an ordinary finite value to distinguish positive from negative thresholds. No clamp or range validation was established from these use sites.

## Practical interpretation and limits

- Increasing the magnitude of the threshold makes the `distance > threshold` condition harder to satisfy in these paths; decreasing it makes that condition easier to satisfy. This is a direct consequence of the observed comparison, not an in-game performance measurement.
- The snapshot value `50000` is unusually large relative to typical scene distances, but the attachment gives no units or capture context. Do not infer that this is the game default or that changing it will improve performance.
- No controlled gameplay comparison has established visible LOD changes, ragdoll fidelity, CPU/GPU impact, affected modes, or a useful override value.
- The CVar has a registry row and direct use-site evidence in the local executable; this is stronger than string presence alone. The community registry's `ref_rva` address association is used as a lead and was corroborated against the local disassembly, but no live runtime override was performed.

See the [unresolved CVar worklist](cvar-unresolved-definitions.md) for other animation and ragdoll controls still lacking usable definitions, and the [registration evidence guide](cvar-registration-evidence-4042190.md) for the surrounding static-analysis provenance.
