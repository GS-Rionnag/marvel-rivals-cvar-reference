# Gameplay and engine CVar addendum

These 12 exact registry names cover event mechanics, collision, and movement or task scheduling. Snapshot values are observations from an unspecified capture build. A dash indicates no value or match in the associated source.

The build string column lists exact names found in build 1.1.4042190. The two hit columns give x64 direct-memory candidates / address-taking instructions. Runtime effects and startup override support remain unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `Hero.1061.Portal.SVONCacheTTL` | `float` / `ref` | `0` | The help describes the portal SVON reachability cache lifetime in seconds. It takes the larger of the configured lifetime and the CVar. At 0 the configured lifetime applies. | — | 3 / 1 | 3 / 1 |
| `M2212.Damage.EnableDistanceDamageSourcePercent` | `bool` / `var` | `false` | Controls whether mode M2212 uses a distance-based source-damage percentage in its damage pipeline. The help gives no formula. | x64, ARM64EC | 3 / 1 | — |
| `ProjectileSuppression.Enable` | `bool` / `ref` | `false` | The help describes limiting the total count of projectiles outside the current view-target source. It gives no cap. | x64, ARM64EC | 3 / 1 | 6 / 1 |
| `SpiderMan.CompatibleWithInhibitedBuff` | `bool` / `ref` | `true` | Toggles compatibility with suppressed buffs. The help maps 0 to disabled and 1 to enabled. The compatibility rules are unspecified. | x64, ARM64EC | 2 / 1 | 4 / 1 |
| `StormGirl.LineTraceFindGround` | `bool` / `ref` | `false` | Toggles line tracing for Storm's ground-finding logic. The help maps 0 to false and 1 to true. | x64, ARM64EC | 2 / 1 | 2 / 1 |
| `Summoned.DestroyedBySummonCollision.Enabled` | `bool` / `ref` | `true` | Supplied help describes a collision rule where a summoned entity breaks a destruction object marked bDestroyedBySummonCollision and takes damage rather than ending. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Summoned.EnableEndAgentByFrameTask` | `bool` / `ref` | `false` | Supplied help identifies an option to execute EndAgentTask through a frame task. Ordering and timing are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `Tether.SelfCollision` | `int32` / `var` | `0` | Name suggests tether self-collision. The registry gives no help on value mapping or scope. | x64, ARM64EC | 3 / 1 | — |
| `TraceFunction.FindGround.MultiTrace` | `bool` / `ref` | `true` | Toggles multi-trace for FindGround. The help maps 0 to false and 1 to true. | x64, ARM64EC | 2 / 1 | 1 / 1 |
| `pm.CVarUsingParallelOptimizationMovement` | `bool` / `ref` | `true` | Name suggests a parallel movement optimization. The registry supplies no help on work split or scheduling. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `pve.RecycleRedirectionInterval` | `float` / `ref` | `0` | Name suggests an interval for recycling PvE redirection state. The registry supplies no help on units or trigger. | x64, ARM64EC | 3 / 1 | 2 / 1 |
| `splines.blockall` | `int32` / `ref` | `0` | Supplied help says the setting selects the BlockAll collision profile for splines in place of each spline's stored collision profile. | x64, ARM64EC | 3 / 1 | 1 / 1 |

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
