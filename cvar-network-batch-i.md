# Network CVar batch I

This guide records 25 registered `Net.*` entries that did not have focused guide coverage in the docs audit. Names and types below come from the preserved community `var`/`ref` registry, which is separate from a live enumeration of the game. Help text is community-supplied metadata; where it was Chinese, the English rendering is an unreviewed translation. The snapshot column is copied from the attached `CVarDump.txt` when an entry was present. A snapshot is one captured value, not a verified default or proof that a startup override is accepted.

## Character movement synchronization

The supplied descriptions present this family as a character-movement replication experiment: a legacy ActorChannel path, a shadow comparison mode, and an active aggregate FastArray path. The settings describe the intended design, but the local build scan is static and does not prove that the mode is enabled in normal matches, which machine or process consumes each setting, or whether startup INI changes take effect.

| Exact CVar | Type | Snapshot | Supplied meaning |
| --- | --- | ---: | --- |
| `Net.CharMove.DisableForceNetUpdate` | bool (`ref`) | — | Completely disables character `ForceNetUpdate`; described as an extreme setting for comparison experiments. Help says the default is false. |
| `Net.CharMove.ForceNetUpdateInterval` | float (`ref`) | — | No direct help was supplied. Nearby captured text associates positive values and `Enable=2` with a `ForceNetUpdate` timer and shows `<=0` as a branch, but this text is only adjacent binary context; exact interval units and behavior are not established. |
| `Net.CharMove.Sync.AllowStaticBase` | bool (`ref`) | — | Whether a character whose movement base is Static and whose velocity is near zero may still use the aggregation path. Help says true by default; false restores the older rule that excludes any character with a base. |
| `Net.CharMove.Sync.Enable` | int32 (`ref`) | — | Master mode: `0` = legacy path (help says default); `1` = shadow mode, writing both paths and comparing fields without sending the aggregate; `2` = active mode, using a global FastArray for movement and disabling the character ActorChannel movement property. |
| `Net.CharMove.Sync.ExcludeHeroIDs` | FString (`ref`) | — | Comma-separated hero IDs excluded from movement aggregation (examples: `1011,1041`). Matching heroes use the legacy ActorChannel movement path; empty means no exclusions. |
| `Net.CharMove.Sync.FlushDeferredOnExclude` | bool (`ref`) | — | When a character leaves MoveSync with a deferred `ForceNetUpdate`, true (help default `1`) clears the timer and immediately performs one bounded `AActor::ForceNetUpdate`; false leaves the original timer to fire at its scheduled time for A/B comparison. |
| `Net.CharMove.Sync.LogUnresolvedRate` | int32 (`ref`) | — | Client-side log sampling for FastArray entries that cannot be resolved to a character: once per N entries; `0` disables. |
| `Net.CharMove.Sync.ModePollInterval` | float (`ref`) | — | No direct help supplied. Nearby binary text contains `Actor`, `Off`, and `On`, but does not establish the exact polling condition, units, or effect. |
| `Net.CharMove.Sync.PerActorLogInterval` | int32 (`ref`) | — | Emit a per-character `[SyncActor]` line every N frames with legacy/new/coexisting path frame counts and their Hz. `0` disables; help says default `300`. Requires `ShadowLogInterval > 0` and shares the `[Sync]`/`[SyncClient]` debug switch. |
| `Net.CharMove.Sync.ShadowLogInterval` | int32 (`ref`) | — | In shadow mode, emit an aggregate-payload versus ActorChannel `ReplicatedMovement` comparison summary every N frames. `0` disables. |
| `Net.CharMove.Sync.ShadowMismatchLogRate` | int32 (`ref`) | — | In shadow mode, sample per-field mismatch details once per N mismatches to identify fields with remaining mismatches. `0` disables. |
| `Net.CharMove.Sync.StaticBaseVelTolerance` | float (`ref`) | — | Velocity threshold in cm/s for treating a movement base as effectively stationary; help says default `1`. Characters above it are excluded. |

## Client-frame settings

These eight names form a `Net.ClientFrame` cluster. Their help fields are empty. Names and snapshot values alone are not enough to identify what frame is uploaded, what “upload” means, or what bounds and test timing control. Do not treat the following descriptions as established semantics; only the names, types, and captured values are known.

| Exact CVar | Type | Snapshot | What can be stated |
| --- | --- | ---: | --- |
| `Net.ClientFrame.AsyncUpload` | int32 (`var`) | `1` | Registered integer; help absent. The name suggests an asynchronous-upload switch, but its effect is unverified. |
| `Net.ClientFrame.Enable` | int32 (`var`) | `1` | Registered integer; help absent. What feature it enables is unknown. |
| `Net.ClientFrame.MaxFrame` | int32 (`var`) | `2000` | Registered integer; help absent. Its unit and relationship to the other ClientFrame settings are unknown. |
| `Net.ClientFrame.MinFrameTime` | float (`var`) | `5` | Registered float; help absent. Its unit and use are unknown. |
| `Net.ClientFrame.TestCount` | int32 (`var`) | `0` | Registered integer; help absent. Whether this is a test count or an unrelated parameter is unverified. |
| `Net.ClientFrame.TestRandMaxTime` | float (`var`) | `0.01` | Registered float; help absent. The name suggests a random-time bound, but units and behavior are unknown. |
| `Net.ClientFrame.TestRandMinTime` | float (`var`) | `0.001` | Registered float; help absent. The name suggests a random-time bound, but units and behavior are unknown. |
| `Net.ClientFrame.UploadInterval` | float (`var`) | `1` | Registered float; help absent. The unit and upload behavior are unknown. |

## Other networking controls

| Exact CVar | Type | Snapshot | Supplied meaning and limits |
| --- | --- | ---: | --- |
| `Net.BunchPool.HardCap` | int32 (`var`) | `2000` | Community help identifies this as the `FOutBunchPool` hard cap, with client default `2000` and server default `100000`. The local client binary context contains the `FOutBunchPool HardCap` label. The server number is help text, not a server build observation. |
| `Net.DeferAbilityActorInitialRep` | int32 (`var`) | — | Help says `1` defers ability-actor initial replication to a multithreaded batch path (`BuildGlobalSharedConsiderList`); `0` globally falls back to immediate `ManualReplicateSingleActorToClients`. No default is specified. |
| `Net.FastArrayDirty` | int32 (`ref`) | `0` | Help: “enable fastarray push mode.” This is a short description, not a contract for which FastArrays are affected or the exact dirty-marking behavior. |
| `Net.ForceNetUpdateFor.PriorityFirst` | int32 (`var`) | — | Help says `ForceNetUpdateFor` calls `ForceNetPriorityUpdate` before `ForceNetUpdate` when enabled (default `1`); disabling restores the previous order. |
| `Net.IsPushModelEnabled` | bool (`ref`) | `true` | Push Model lets game code notify networking when state changes rather than having networking scrape for changes. This general description does not identify every affected replicated property or prove the mode is active in a particular session. |

## What the local build scan establishes

The saved address-reference scan is for build 4042190. It reports instruction candidates that target a CVar's `ref_rva` separately from matches to the CVar object's `obj_rva`. An address-taking instruction (`lea`) is not a value read. An object-RVA setup/write is evidence that the object address is referenced, not evidence that the CVar's current value is consumed. Even a direct memory instruction candidate needs its surrounding function and control flow checked before it can be called a runtime read.

For this batch, the 12 `Net.CharMove.*` entries, `Net.FastArrayDirty`, and `Net.IsPushModelEnabled` have `ref_rva` instruction candidates in the saved scan. These sets mix address-taking and memory instructions; examples include compares or scalar loads, but this guide does not claim each candidate has been traced to an active runtime decision. The other 11 entries have no `ref_rva` candidate in this scan and only object-RVA matches: `Net.BunchPool.HardCap`, all eight `Net.ClientFrame.*` entries, `Net.DeferAbilityActorInitialRep`, and `Net.ForceNetUpdateFor.PriorityFirst`.

This evidence says nothing conclusive about client/server authority, config precedence, whether a CVar is writable by the supplied loader, or live gameplay effects. In particular, metadata registration as `var` or `ref` is not a controlled test of the `[Overrides]` mechanism. No runtime override or multiplayer test was performed.

## Sources

- Exact names, types, supplied help, and reference RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); build and capture method are unknown.
- English renderings for CJK help: [Chinese help translations](cvar-chinese-help-translations.md); translations are marked unreviewed.
- Build-specific strings: [build 4042190 context index](EVIDENCE.md#build-specific-static-analysis); adjacency does not prove a string's exact relationship to a setting.
- Static address candidates: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included) and [scanner limitations](EVIDENCE.md#build-specific-static-analysis).
- Exact Epic 5.9 reference matches and registry metadata are indexed in the [community registry](cvar-community-registry.md); engine-version alignment with the game build is unconfirmed.
