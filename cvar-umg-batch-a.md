# UMG CVar batch A

This guide documents all 10 currently uncovered exact-case `UMG.*` variable/reference rows. Supplied help describes animation evaluation, control flow, profiling, and flush timing. Help, snapshot values, UE 5.9 defaults, and executable scan evidence are kept separate.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help and uncertainty | Build 1.1.4042190 address evidence |
| --- | --- | --- | --- | --- | --- |
| `UMG.AllowMovieSceneAsyncUpdate` | `bool` (`ref`) | false | — | When true, the UMG sequence runner performs a flush on `MovieSceneAsyncCallThread`. | Name appears in the Shipping executable string inventory. `ref_rva`: 5 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.AnimationBudgetMs` | `float` (`ref`) | 1 | 0 | Experimental per-frame budget, in milliseconds, for evaluating all UMG animations. The supplied help gives default 0; the captured snapshot is 1 and the UE 5.9 reference is 0. | Name appears in the Shipping executable string inventory. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.AnimationMarkers` | `bool` (`ref`) | false | false | Whether to emit profiling frame markers at the start and stop of UMG animations. | Name appears in the Shipping executable string inventory. `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.AsyncAnimationControlFlow` | `bool` (`ref`) | true | true | Whether animation control-flow operations such as Play, Pause, and Stop run asynchronously. | Name appears in the Shipping executable string inventory. `ref_rva`: 4 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.DebugAnimation` | `bool` (`ref`) | false | — | Whether to enable UMG animation debugging; help does not specify the emitted diagnostics. | Name appears in the Shipping executable string inventory. `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.DisableTakeWidgetOpt` | `int32` (`ref`) | 0 | — | No supplied help. The name suggests disabling a TakeWidget optimization, but the optimization and effect are not defined by the available sources. | Name appears in the Shipping executable string inventory. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.EnableLegacyTrackEvalIfNoTick` | `bool` (`ref`) | false | — | Whether to evaluate a legacy track template when a widget has no Tick. The supplied help appears to say default true; the snapshot is false. The precise legacy-track path is not explained. | Name appears in the Shipping executable string inventory. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.FlushAnimationsAtEndOfFrame` | `int32` (`ref`) | 0 | 1 | Whether outstanding animations are flushed at frame end or left until the following frame. The UE 5.9 catalog says default 1, while the snapshot is 0; this is not resolved for the game. | Name appears in the Shipping executable string inventory. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.PlayAnimationEvenIfNotVisible` | `bool` (`ref`) | false | — | When true, allow animations to play even while the widget is not visible. | Name appears in the Shipping executable string inventory. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |
| `UMG.RunLatentActionsFlushCallback` | `bool` (`ref`) | false | — | When true, the runner flushes after running latent actions. | Name appears in the Shipping executable string inventory. `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. Unvalidated static candidates. |

## Evidence limits

- Snapshot values are observations from `CVarDump.txt`, not verified game defaults or recommendations.
- Epic values are exact-name UE 5.9 reference matches. They do not establish the game’s engine version.
- Printable names in the Shipping binaries establish string presence only. Address references to registry fields are unvalidated scan candidates, not proof of registration, value access, or execution.
- The supplied help for `UMG.DisableTakeWidgetOpt` is empty; its name alone is not a definition.
- Snapshot/help/Epic mismatches for `AnimationBudgetMs`, `EnableLegacyTrackEvalIfNoTick`, and `FlushAnimationsAtEndOfFrame` are called out rather than reconciled.
- No controlled runtime test established whether these names are accepted through the loader’s `[Overrides]` section or what their effects are in Marvel Rivals.

Sources: [community CVar registry](cvar-community-registry.md), [Epic UE 5.9 comparison and captured values](cvar-community-registry.md), [preserved community attachments](EVIDENCE.md#community-sources), [build CVar string inventory](EVIDENCE.md#build-specific-static-analysis), and [build address-reference scan](EVIDENCE.md#build-specific-static-analysis).
