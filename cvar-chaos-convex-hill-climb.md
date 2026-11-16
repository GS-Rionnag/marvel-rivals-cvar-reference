# Chaos convex-hull builder and hill-climb CVars

This guide covers the four `p.Chaos.Convex.*` variables in the supplied registry. It combines registry help, captured values, and direct reads in Marvel Rivals Shipping build `1.1.4042190`. Three source descriptions are Chinese; the English translations below are assistant-generated and unreviewed. Snapshot values are not verified defaults or recommendations.

| CVar | Type | Snapshot | Meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Convex.HillClimbMinVertices` | int32 | `32` | Unreviewed translation: build hill-climb data only when the convex hull has at least this many vertices; changes affect newly built or loaded hulls. At `0x142855DDD`, code compares the hull vertex count with the CVar and also rejects counts above `256` from this path (`0x142855DE3`); counts below the setting or above that bound branch to the alternate path. The exact alternate builder behavior is not identified here. |
| `p.Chaos.Convex.MaxHillClimbSteps` | int32 | `64` | Unreviewed translation: maximum iterations for one hill-climb query. At `0x14285C113`, the value is loaded and clamped to at least `1`; it is used as a loop bound in the surrounding query routine. |
| `p.Chaos.Convex.UseHillClimb` | int32 | `1` | Unreviewed translation: enables convex-hull support hill-climbing; `0` means scan all vertices and `1` uses hill-climbing; runtime kill switch. Six solver paths compare the value with zero (`0x142773B7F`, `0x142773F0D`, `0x14277477F`, `0x142774B0D`, `0x142774E23`, `0x14277513F`), confirming a runtime branch at multiple support-query sites. |
| `p.Chaos.Convex.UseTConvexHull3Builder` | bool | `true` | Registry help says to use the newer Geometry Tools path for convex-hull generation when the default build method is selected; help gives `true` as default. The value is read in two hull-generation paths at `0x14274CECF` and `0x14274EA3E`, where it participates in branch selection. The complete selection logic and generated-hull differences are not reconstructed. |

## Evidence and limits

- Names, types, original help, and reference addresses come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); snapshot values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). English renderings for the three Chinese descriptions are in [`cvar-help-translations.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and are explicitly unreviewed.
- Direct-reference candidates come from [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); code behavior above was checked in the local executable disassembly. This is static evidence for code paths, not proof that a given hull/query in a match takes that path.
- No controlled in-game override was tested. Do not treat the snapshot as a default or tuning recommendation.

Related guides: [Chaos collision CVars](cvar-chaos-collision-tolerances.md), [Chaos collision margin CVars](cvar-chaos-collision-margins-tolerances.md), [Chaos CCD settings](cvar-chaos-ccd-axis-targets.md), and [CVar overrides and loader syntax](cvar-overrides.md).
