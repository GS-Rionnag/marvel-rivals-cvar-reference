# Remaining registry names with limited help

This final group completes exact-name coverage of the preserved community registry. It is intentionally conservative: a registry row shows that a name was present in the dump, not that the game accepts a startup override or that the setting is safe, effective, or available in the current build. Names with missing help are left unresolved. Help-derived descriptions below report only the documented scope and do not imply runtime verification.

| Exact name | Registry type | What the preserved source establishes |
| --- | --- | --- |
| `AbilitySystemOpt.EnableCloseScopeClientTrace_Testing` | `bool` / `ref` | The translated object help associates this testing entry with disabling a client-side spell-field check. Runtime availability and effect are unverified. |
| `Dash.HeightFilter.SkipPawn` | `bool` / `ref` | No descriptive help. The name suggests a pawn-related height-filter condition; the affected logic is unknown. |
| `Dash.Server.CheckClientStartLocLimit` | `float` / `ref` | Help describes a distance comparison between server and client dash start locations. Its units and runtime use are unverified. |
| `Dash.Server.UseClientStartDashZ` | `bool` / `ref` | No descriptive help. The name associates it with the vertical component of a client dash start location; behavior is unverified. |
| `FogVisActor.CheckOcclusionOnlyClient` | `bool` / `ref` | No descriptive help. The name associates it with client-side occlusion checks for a fog-visibility actor. |
| `Hero_1062.Ability_106241.ForceTeleportNoSweep` | `bool` / `ref` | Supplied help describes a character-positioning path for an ability, with a fallback condition. This guide does not infer runtime acceptance or recommend changing it. |
| `M2201.Activity.Cmd` | `FString` / `ref` | Help labels this an activity command used by tooling. The syntax and effects are not reproduced or assessed here. |
| `M2212.Bubble.Force` | `int32` / `var` | Translated help associates this with a mode-specific projectile-to-bubble behavior. The affected mode and runtime behavior are unverified. |
| `TraceMgr.CVar_IgnorePortalLogic` | `bool` / `ref` | See the [focused build-evidence note](cvar-tracemgr-ignore-portal-logic.md); the registry row itself has no descriptive help. |
| `ability.1040.CVarServerCheckClientSelectResult` | `bool` / `ref` | No descriptive help. The name suggests a server-side check concerning a client selection result; the condition and effect are unknown. |
| `ability.104241.GIgnoreCheckInWeb` | `bool` / `ref` | No descriptive help. The name alone is insufficient to establish its behavior. |
| `ability.104241.GNoHideSummoner` | `bool` / `ref` | No descriptive help. The name alone is insufficient to establish its behavior. |
| `d.IgnoreAternatableActorPenetration` | `bool` / `var` | Supplied help describes whether alternate actors are excluded while resolving penetration. The exact scope is unverified. |
| `hero.1054.DisableFlamePursueFrameGuard` | `bool` / `var` | Supplied help associates the flag with a same-frame guard in a named ability function. Its practical effect is unverified. |
| `net.MaxNumberOfAllowedTArrayChangesPerUpdate` | `int32` / `ref` | The registry supplies a numeric snapshot, but no descriptive help. The name indicates an update-related array-change limit; units and runtime scope are not established. See [the focused analysis](cvar-network-array-update-limits.md) for the preserved source discussion. |
| `net.MaxNumberOfAllowedTArrayDeletionsPerUpdate` | `int32` / `ref` | The registry supplies a numeric snapshot, but no descriptive help. The name indicates an update-related array-deletion limit; units and runtime scope are not established. See [the focused analysis](cvar-network-array-update-limits.md) for the preserved source discussion. |

The source dump does not establish current-build registration, editability, or runtime effects for these names. Several entries have only names or short help labels; those are kept explicitly unresolved rather than expanded into behavioral claims.

[Community registry and source notes](cvar-community-registry.md) · [Evidence and scope](EVIDENCE.md#build-specific-static-analysis)
