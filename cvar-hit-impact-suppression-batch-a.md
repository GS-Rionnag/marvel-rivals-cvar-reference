# HitImpactSuppression CVar batch A

This guide covers all 11 currently uncovered exact-case `HitImpactSuppression.*` variable/reference rows. Supplied help describes a per-frame hit-impact count limit with priorities and an early-out path; it does not fully specify all branches or how ViewTarget cues interact with the limits.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Supplied meaning and uncertainty | Build 1.1.4042190 address-scan candidates |
| --- | --- | --- | --- | --- | --- |
| `HitImpactSuppression.ApplyOnViewTarget` | `bool` (`ref`) | true | — | Controls whether a hit impact caused by the view target can be suppressed; the conditions and priority behavior are not further described. | `ref_rva`: 3 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CloseRangeDistance` | `float` (`ref`) | 500 | — | Distance in centimeters within which a target is treated as close range. | `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CountLimit0` | `int32` (`ref`) | 1 | — | Hit-impact count limit for priority 0; supplied help says priority 0 is the lowest priority. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CountLimit1` | `int32` (`ref`) | 1 | — | Hit-impact count limit for priority 1; priority scale details beyond priority 0 being lowest are not supplied. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CountLimit2` | `int32` (`ref`) | 1 | — | Hit-impact count limit for priority 2; priority scale details beyond priority 0 being lowest are not supplied. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CountLimit3` | `int32` (`ref`) | 3 | — | Hit-impact count limit for priority 3; priority scale details beyond priority 0 being lowest are not supplied. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.CountLimitMultiplier` | `float` (`ref`) | 1 | — | A larger multiplier increases the count limit; the exact calculation is not given. | `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.Enable` | `bool` (`ref`) | false | — | Controls whether the system limits hit impacts counted in a frame. | `ref_rva`: 6 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.SkipAllHitImpactCues` | `bool` (`ref`) | false | — | When budgets are exhausted and a cue is not from the ViewTarget, an early-out can skip the full HitResult loop. Supplied help says 1 enables it and calls that the default, while the captured snapshot is false; this conflict is unresolved. | `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.SupresssHitResultsApplyOnViewTarget` | `bool` (`ref`) | false | — | No supplied help. The exact spelling is preserved; the name suggests a control over suppressing HitResults on the ViewTarget, but the behavior is unverified. | `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `HitImpactSuppression.SupresssHitResultsNum` | `int32` (`ref`) | 0 | — | No supplied help. The exact spelling is preserved; the name suggests a count related to suppressed HitResults, but its unit and role are unverified. | `ref_rva`: 3 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |

## Evidence limits

- Snapshot values are observations from `CVarDump.txt`, not verified defaults or recommendations.
- No exact Epic UE 5.9 default was recorded for these game-specific names. The UE 5.9 comparison does not establish the game’s engine version.
- Build scan counts are instructions that reference the registry `ref_rva` and `obj_rva` fields. They are candidate classes, not control-flow-validated value reads or proof of execution.
- Two names use the supplied misspelling `Supresss`; it is preserved verbatim. They have no help text, so their meanings remain name-based guesses.
- The `SkipAllHitImpactCues` help’s stated default and the captured value differ. Neither value should be treated as the game’s verified default.
- No controlled runtime test established whether any entry is accepted through the loader’s `[Overrides]` section or what effect changing it has.

Sources: [community CVar registry](cvar-community-registry.md), [captured values and preserved community attachments](EVIDENCE.md#community-sources), and [build-specific address-reference scan](EVIDENCE.md#build-specific-static-analysis).
