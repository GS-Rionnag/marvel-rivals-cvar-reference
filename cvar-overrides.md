# Marvel Rivals CVar overrides: research notes

Started 2026-11-15. This guide catalogs all 89 setting lines (85 distinct keys) in the original post in [the Discord thread](https://discord.com/channels/1452445537298022637/1556428197820633269), including its 83 ordinary lines and six `!` reset lines. Four ordinary keys appear to be input config properties rather than CVars. The guide explains what can be established about each one and separates engine facts from unverified claims about Marvel Rivals.

## Evidence and scope

The analyzed game build identifies itself as Marvel Rivals 1.1.4042190 Shipping. Its user settings expose game-specific scalability and frame-generation properties, but do not enumerate the engine CVar registry. Cooked game content does not provide a readable project config-source tree.

The game's `GameUserSettings.ini` was rechecked. Its `[ScalabilityGroups]` section has nine `sg.*` quality-group keys, and all nine have exact `var`/`ref` entries in the community registry. The `[/Script/Marvel.MarvelGameUserSettings]` section stores game settings such as supersampling mode, screen percentage, DLSS preset, CAS sharpness, and latency options as serialized config properties.

A read-only byte-string scan of the x64 Shipping executable found 65 of the thread's 83 ordinary setting keys as exact printable strings. The five distinct keys from the `!` reset block were all present. Fifteen CVar-like thread keys were not found in the main executable, and the full 126-file executable/DLL scan did not recover those same names; the three input-property names were also absent from the main executable. The expanded scan includes likely engine and game-fork namespaces such as `Marvel.*`, `marvel.*`, `ChaosGC.*`, `AbilitySystem.*`, `ABS.*`, `AOI.*`, `m.*`, and `marvelstats.*`; it lists 10,236 string candidates, including 8,816 exact names from the community `var`/`ref` registry, 8,326 names from the value snapshot, and 4,436 exact Epic 5.9 reference matches. The registry-name pass added 1,438 matches that were previously hidden in the unclassified printable-string set, and the snapshot pass surfaced two more names. A companion [nearby-text index](EVIDENCE.md#build-specific-static-analysis) records raw neighboring strings for all 10,236 candidates; 7,149 have some preceding printable text, though this often includes unrelated strings. This binary-layout evidence is not confirmed CVar help. See the [build-specific inventory](EVIDENCE.md#build-specific-static-analysis) and [repeatable scanner](EVIDENCE.md#method-and-reproducibility).

For a wider namespace audit, the scan found 46,547 distinct dotted printable identifiers across 126 executable/DLL files. The separate [unclassified index](EVIDENCE.md#build-specific-static-analysis) lists the 36,311 identifiers not selected by the prefix, Epic-reference, or exact community-registry-name filters.

## Community registry attachments

Two later community attachments provide a much broader static registry than the original override thread. The [registry message](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) supplied `console_vars.tsv` and `console_objects.tsv`; the [earlier dump message](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452) supplied `CVarDump.txt`. That file's header calls it a “community CVar dump” and marks it re-importable. The loader method and version associated with the snapshot are unverified, as are the capture build and whether values are defaults, runtime values, or user-overridden. The original source messages are linked above.

A separate [third-party `engine.ini` cross-check](cvar-third-party-config-crosscheck.md) covers 132 dotted names in a pinned community config from 2025. Ninety-six match the `var`/`ref` table; two more strings occur in the local binary scan; 34 match none of the registry, dump, Epic 5.9 reference, or local dotted-string inventory. Treat the config values as community proposals, not defaults.

The registry contains **8,973 unique names with `var` or `ref` rows**, plus **395 command names**. The separate objects table has **427 additional names**. The generated catalogs include the [CVar registry](cvar-community-registry.md), [snapshot-only candidates](cvar-snapshot-only.md), [Epic-reference-only binary candidates](cvar-engine-reference-only.md), [definition gaps](cvar-unresolved-definitions.md), [commands](cvar-community-commands.md), and [additional objects](cvar-community-console-objects.md). The value snapshot has 8,445 entries matching the `var`/`ref` registry; 528 registry names are absent from that snapshot, and 67 snapshot names have no `var`/`ref` row. Those 67 are documented as [snapshot-only CVar candidates](cvar-snapshot-only.md); 40 also appear in the object table, while 27 do not. The dump header calls it re-importable, so its values are recorded as a snapshot, not as defaults.

The `var`/`ref` table has help text for 7,553 names. Exact matches to the Epic 5.9 reference provide upstream defaults/descriptions for 4,387 of those registry names. A further 49 Epic-reference names appear in local binaries without a `var`/`ref` row; 21 of those also appear in the snapshot-only list, so the two supplemental lists add 95 distinct names beyond the 8,973 `var`/`ref` set (9,068 total candidate names across these sources). The [definition-gap worklist](cvar-unresolved-definitions.md) flags 1,049 registered names with no useful text in either attachment or exact Epic 5.9 match.

The registry attachment does not identify the game build or executable hash. Compared with the local 1.1.4042190 binary string index, 8,816 registered names are present in the selected dotted binary candidates; 157 registry names are outside that selected set (40 are undotted and outside the scanner filter, while 117 dotted names were absent from all scanned binaries). Another 1,420 selected binary candidates have no `var`/`ref` registry row. These are static-source differences, not proof that either side is exhaustive at runtime. An exact-name cross-check against the CVar-like keys in the original post finds 66 of 81 keys in the registry; their types and help are tabulated under [Registry definitions for the posted CVar keys](#registry-definitions-for-the-posted-cvar-keys). The remaining 15 have no exact entry in this attachment. Custom behavior still needs source-code or runtime evidence.

## Epic reference and community benchmark

For standard Unreal variables, this guide uses Epic's public [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference) and [Texture Streaming Configuration](https://dev.epicgames.com/documentation/unreal-engine/texture-streaming-configuration-in-unreal-engine). Marvel Rivals' precise Unreal fork/version can differ. A variable appearing in Epic's reference is evidence of its meaning in that engine version, not proof that Marvel Rivals registers it or honors runtime changes. `Not located` means it was not present in the Epic 5.9 reference during this review; it may still be a Marvel-specific, plugin-specific, older-version, or fork-only variable. Verify registration/effect in the current game before relying on it.

The thread's author says the list was assembled from things other people used and that they had **not individually benchmarked** each entry. Three screenshots attached to the original post show different Practice Range views with FPS counters, but no matched scene/config pair. A later chart in the thread compares “1600x1200 w/ CMDS @ 100% AA” with “1600x1200 Mid No CMDS 100% AA”: it reports 253.3 average / 111.6 1st-percentile / 86.4 0.1-percentile FPS for the first row and 199.6 / 103.7 / 81 for the second. The chart does not identify the exact override set, test hardware, benchmark method, or repetitions; these figures are a community-reported comparison, not causal proof that the posted CVars produced the average-FPS difference.

## How to read these in the example loader

According to the loader instructions supplied for this task:

- Lines beginning with `;` are comments and do nothing. The example block must be copied below the actual `[Overrides]` marker and uncommented before it takes effect.
- An ordinary `name=value` line under `[Overrides]` is a CVar override. The loader says these merge above existing configuration and take precedence, including switches.
- In this loader, `!name=` removes the configured value so the game's own value applies. Keep the `=`. This is the loader's behavior; it is not a general Unreal CVar reset syntax.
- The loader's own instructions say settings that can remove smoke or other effects are ignored. This is a loader policy statement; it does not identify every protected setting or promise that all visual changes are detected the same way.
- The `[Section]` format is for non-CVar config properties. In the thread, `bDisableMouseAcceleration`, `bEnableMouseSmoothing`, `bViewAccelerationEnabled`, and `RawMouseInputEnabled` look like config properties, not console variables. They should only be used in the setting's real config section if the game defines them there; putting them under `[Overrides]` does not make them CVars.
- The thread's `!r.SkeletalMeshLODBias=15` and `=16` are two alternative reset lines, not a way to set a range. Under the supplied loader semantics both remove the configured value; neither requests LOD 15 or 16.

The example loader format has an `[Overrides]` section and per-key add, replace, and reset syntax. Those loader semantics establish how to express a value, not whether the game accepts a particular CVar.

The six reset lines and the status of the variable each names are:

| Exact line | What this loader does / CVar status |
| --- | --- |
| `!r.Streaming.UsePerMeshBias=0` | Removes the configured value for this key; `0` is not applied. Not located in Epic 5.9, and the name must be treated as possibly game/fork-specific or misspelled. |
| `!r.SkeletalMeshLODBias=15` | Removes the configured value. Epic documents the underlying LOD-bias CVar, but this line does not set bias 15. |
| `!r.SkeletalMeshLODBias=16` | Same reset operation for the same key; the `15` and `16` versions are redundant alternatives. |
| `!r.SkeletalMeshLODRadiusScale=0.25` | Removes the configured value. The number does not apply; Epic documents the underlying screen-radius scale separately. |
| `!r.FreeSkeletalMeshBuffers=1` | Removes the configured value; `1` is not applied. Epic documents this CVar as controlling whether skeletal-mesh buffers stay in CPU memory to support skeletal-mesh merging (`0` keeps them, `1` frees them). |
| `!r.Streaming.PoolSizeForMeshes=0` | Removes the configured value; zero is not applied. Epic documents the underlying mesh-pool CVar separately. |

## Does a CVar actually change in Marvel Rivals?

“Editable” has several separate meanings. The supplied loader instructions say that a syntactically valid line below `[Overrides]` is merged over the config and wins over its existing values. That establishes what the loader intends to do with the line; by itself it does **not** establish that the game accepts the setting or that gameplay/rendering changes.

For this research, use these evidence levels and do not collapse them into a single yes/no label:

| Evidence level | What it establishes | What it does not establish |
| --- | --- | --- |
| Loader syntax | The line is uncommented, in the right section, and uses the loader's documented `name=value` form (or its documented `!name=` reset form). | That the key is a CVar, recognized by this build, or read by active code. |
| Name/registration evidence | The name occurs in a community registry attachment, a local binary string, or stronger registration-like binary evidence. | That the current game build exposes it to config loading, permits this source's priority, or applies its value. The registry attachment's exact game build is unknown. |
| Config application evidence | A startup log, in-game query, or comparable runtime check shows the requested value was applied and not rejected/overridden. | That any live feature reads the value or changes because of it. |
| Local code-use evidence | The Shipping build contains a direct value read or a registration/callback path tied to the setting. | That the path executes in a normal match, that the requested config value reaches it, or that the visible effect is beneficial. Address-taking alone is not a value read. |
| Controlled behavior evidence | A repeatable in-game A/B change, with other settings and the scene controlled, demonstrates an observable effect. | Effects in modes, maps, patches, or hardware not covered by the test. |

Unreal's public documentation says CVars may be set from config files and that different sources have priorities; a higher-priority value can prevent a lower-priority source from setting the CVar. It also documents special config sections for some engine CVar namespaces. Those are Unreal-engine rules, not proof that Marvel Rivals uses the same fork behavior, loads the mod loader at the same priority, or accepts a particular custom CVar. See Epic's [configuration-file guidance](https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#SetConsoleVariablesinConfigurationFiles) and [C++ CVar priority guidance](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine#priority).

Some CVar families documented below were analyzed only from registry metadata and static executable references. For those, say “loader-configurable by syntax; game acceptance/effect unverified” unless there is specific runtime evidence. The loader also explicitly says it ignores settings that can remove smoke or other effects; this can veto an otherwise valid line, and the rule should be checked before testing any effect-removal proposal. A variable can therefore be syntactically editable without being accepted, behaviorally active, or allowed by the loader.

## Can a normal packaged mod list the live CVar registry?

The normal asset-mod workflow in this repository replaces cooked Unreal assets and packages them into an IoStore `.pak`/`.ucas`/`.utoc` set. The [evidence and scope notes](EVIDENCE.md#method-and-reproducibility) also cover PAK-based INI/config edits, while the example loader syntax describes startup config merging and per-key overrides. These workflows can carry or set predetermined values; none of the inspected instructions exposes a way for a `.pak`/INI mod to enumerate the engine's live `IConsoleManager` registry or write its current state to a file. That is a limitation of the inspected workflow, not a claim that no other Marvel Rivals mod framework can run code.

Before building a custom code mod, the low-impact route is to check whether the current game exposes Unreal's built-in console commands. Epic documents `DumpCVars [Prefix] [-showhelp] [-csv=[path]]` as listing CVars and values, optionally filtered and saved as CSV, and `DumpConsoleCommands` as listing variables, commands, and discovered execs. These are UE 5.9 engine-reference capabilities, **not verified as available in Marvel Rivals Shipping build 1.1.4042190**. A printable-string search of the installed MarvelGame `.exe` and `.dll` files and the preserved community command attachment did not find these exact command names; availability through another path is still unknown. If the game accepts `DumpCVars`, its output would provide a valuable live name/value/help list, but Epic's command description does not promise to include CVar flags or `LastSetBy`. Even a live current value does not by itself prove that a loader override is accepted or that the changed value affects gameplay. See Epic's [Console Commands Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-commands-reference) and [CVar flag reference](https://dev.epicgames.com/documentation/unreal-engine/API/Runtime/Core/EConsoleVariableFlags).

If the built-in command is unavailable, a true runtime enumerator would need code that runs inside the game and queries the live console manager. That is a native plugin/hook-style task, not the cooked asset replacement workflow used by the existing mods here. The workspace has no documented mod build path for such a runtime component. Do not describe a normal `.pak`/IoStore asset mod as a live registry dumper unless it can demonstrate that code execution and output path. A practical editable-CVar check would record a baseline live dump, apply one loader override, relaunch, then dump again and compare the target value; test a resulting in-game effect separately.

### Loader implementation scope

This guide documents the example override syntax and research evidence. No launcher, loader binary, game executable, local config file, or raw scan artifact is included in this documentation-only project. Loader acceptance and runtime behavior remain unverified unless a guide states otherwise.

## Current Marvel Rivals policy on injected mods and config changes

Marvel Rivals' official [Use of Mods and Violation Management notice (2026-10-15)](https://www.marvelrivals.com/20261015/41525_1316797.html) says that certain mods using memory-injection and modification behaviors trigger anti-cheat detection and that prohibited mods can receive disciplinary action. Its official [Prohibited Software & Hardware List](https://www.marvelrivals.com/guide/20250226/41348_1214569.html) also lists unauthorized client-config changes, graphics-rendering `.ini` modifications, third-party plugins, and unfair mod resources as prohibited while the game runs. These notices do not establish whether the loader's reported startup-time method is the same as the memory-injection methods called out in the newer notice, but they do mean we cannot verify that an injected or config-loading CVar dumper is safe or authorized for online use. This project will use the supplied dumps and static/offline analysis rather than build or run a dumper in the live client.

## Additional lines in the installed override loader loader config

The installed `SigeonLoader.ini` also has active entries beyond the Discord post. Its selected baseline is `low`; the file itself does not list that variant's full CVar defaults. This section records only the relevant setting lines; local loader credentials and unrelated personal data are omitted. The loader's own comment block says `[Overrides]` lines win over merged config values and that `!name=` drops the configured value. Treat `!` rows as resets, not as assignments.

| Exact line | What the line means / evidence |
| --- | --- |
| `!r.VelocityOutputPass=2` | Reset only: the `2` does not apply. The underlying Unreal CVar chooses when to write the velocity buffer: `0` during depth pass, `1` during base pass, `2` after base pass. This setting affects motion vectors used by temporal AA and motion blur; it is not a general performance switch. |
| `r.Streamline.DeepDVC.Intensity=1` | NVIDIA Streamline DeepDVC intensity; NVIDIA documents range 0–1, with 0 preserving the original image and larger values strengthening adaptive vibrance. `1` is the maximum documented intensity. Whether the game's Streamline integration is enabled is a separate question. |
| `r.Streamline.DeepDVC.SaturationBoost=1.00` | NVIDIA documents this as a 0–1 color saturation boost, active when intensity is raised. `1.00` is the maximum documented boost. Exact registration through this Unreal CVar spelling is build-specific. |
| `r.SeparateTranslucency=1` | Enables a separate translucency render target/pass, keeping translucency unaffected by depth of field. Epic's reference says this costs GPU performance and memory; `1` is also the upstream default. Effects and cost in Marvel Rivals still depend on its renderer/content. |
| `!r.debug.ForceDefaultMtl=1` | Reset only: `1` is not applied. The underlying name is embedded in the game executable but is not in Epic's reference; its exact meaning remains unknown. |
| `!r.MipMapLODBias=15` | Reset only: bias `15` is not applied. The underlying Epic CVar adds a global mip bias to 2D textures (documented range −15 to 15); positive bias generally selects blurrier/lower-resolution mips. |

The installed file also has these **commented** motion-blur examples, so none is currently active:

| Commented example | Meaning / status |
| --- | --- |
| `r.DefaultFeature.MotionBlur=1.5` | Epic describes this as the project default for motion blur, with `0` off and `1` on; camera/post-process settings can override it. The example is commented and its `1.5` value is outside the documented 0/1 choices. |
| `r.MotionBlurQuality=5` | Epic's current reference describes values 0–4 (off through very high), with 3 high; the posted `5` is outside that documented range. Commented, so inactive. |
| `r.MotionBlur.Amount=0.5` | Overrides post-process motion-blur amount when set to an override value. Commented, so inactive. |
| `r.MotionBlur.Max=5` | Overrides maximum blur length as a percent of screen width. Commented, so inactive. |
| `r.MotionBlur.Scale=1.5` | Scales motion-blur intensity from the post-process setting. Commented, so inactive. |
| `r.MotionBlur.TargetFPS=162` | Target FPS used to scale motion-blur velocity length; Epic documents −1 for the post-process setting, 0 for a moving-average current frame rate, and 1–120 for an explicit target. The example `162` is outside that documented range. Commented, so inactive. |

The game install contains Streamline's `sl.deepdvc.dll` (file version `2.11.1.0`) and NVIDIA's `nvngx_deepdvc.dll` (file version `310.6.0.0`) under `Engine/Plugins/Marketplace/StreamlineCore/Binaries/ThirdParty/Win64/`. This confirms the plugin components are present in the inspected build, but does not prove DeepDVC is enabled in a running session or that the two CVar lines are honored. NVIDIA's linked programming guide is version 2.14.16, newer than the installed 2.11.1 plugin; use it as an upstream description of the controls, not as exact proof of this build's behavior.

The full executable/DLL scan also found these related strings in both Shipping architectures. They are absent from the installed config and have no public Epic definition:

| Game-build candidate | Current interpretation |
| --- | --- |
| `r.Streamline.DeepDVC.Enable` | Likely enable/disable switch by its name. NVIDIA's API requires the feature mode to be set on before it applies, but the string alone does not prove this CVar maps to that API mode. Default and exact game behavior are unknown. |
| `r.Streamline.Load.DeepDVC` | Likely controls whether the DeepDVC plugin is loaded, but this is name-based inference; startup timing and effect are unverified. |

The local config places the four mouse-input properties listed earlier under `[Overrides]`. They still look like config properties rather than documented Unreal CVars; the loader's sample syntax says non-CVar properties require their owning `[Section]`. Their current effective behavior is not verified.

## NVIDIA plugin candidates in this build

The full install scan found 27 `r.NGX.*` and 35 `r.Streamline.*` strings in the two Shipping game executables. They are listed individually, with file evidence, in the [build inventory](EVIDENCE.md#build-specific-static-analysis). NVIDIA's official DLSS documentation confirms that its Unreal plugin exposes controls under `r.NGX`; official Streamline docs describe DeepDVC and the feature/plugin APIs. Those references explain the feature families, but do not establish the Marvel build's registration, defaults, or behavior for every candidate.

At a name level, `r.NGX.DLSS.*` covers DLSS enablement, exposure, denoising, presets, memory handling, and reflection options; `r.NGX.DLSSRR.Preset` appears to select a Ray Reconstruction preset. `r.NGX.Enable` / `r.NGX.Enable.AllowCommandLine` and `r.NGX.BinarySearchOrder` appear to control NGX startup/library selection; the exact game-specific flags need code evidence. `r.NGX.Automation.*` names suggest image-quality/performance automation and view selection.

`r.Streamline.*` candidates include `DLSSG.*` options (frame generation, generated-frame count, dynamic resolution, status and UI detection), `DeepDVC.*` color controls, `Load.*` module switches, `InitializePlugin`, Reflex plugin registration, motion-vector handling, resource tags, swapchain proxies, and logging. NVIDIA's Streamline guide confirms that DLSS-G uses a proxy swap chain and tagged backbuffer/depth/motion-vector/UI inputs, which gives context to the `Tag*`, `MotionVector*`, and swapchain names. These group descriptions are category-level inference from the names; use the inventory's explicit uncertainty labels and do not treat an embedded string as proof that the setting is safe or accepted.

## Game-specific meanings recovered from nearby binary text

The x64 Shipping executable contains natural-language text close to several first-party CVar-like names. These strings look like their help text, but the pairing comes from data layout rather than confirmed Ghidra cross-references or runtime `DumpConsoleVariables` output. The [nearby-text index](EVIDENCE.md#build-specific-static-analysis) preserves the raw strings and offsets for review.

| Candidate | Embedded description and practical reading |
| --- | --- |
| `Marvel.GameState.EnableDamageEventBudgetThrottle` | A master switch for frame-budget-based `BroadcastDamageEvent` callback throttling; the embedded text says `false` disables it. This is gameplay/event scheduling, not a rendering-quality toggle. |
| `Marvel.GameState.DamageEventBudgetThresholdMs` | Per-frame time budget in milliseconds for `BroadcastDamageEvent` callbacks. When exceeded, the text says `CanBeMerged` targets are auto-throttled. |
| `Marvel.GameState.DamageCallbackForceTriggerSeconds` | Maximum time a `CanBeMerged` target can go without a damage callback before a forced trigger, even while over budget. |
| `Marvel.GameState.DamageEventLODDistance` / `TreatEventLODDistance` | Client-only event culling by distance from the local player, in centimeters. Damage or Treat events are skipped when both source and target are not self and are farther than the set distance; `0` disables the filter. |
| `Marvel.GameState.AttributeEventCullingMinCount` | Enables Damage/Treat LOD culling only when the sorted event count exceeds this threshold; values `<=0` disable the count gate. |
| `Marvel.GameState.CameraInfoFOVFilter` | Enables per-connection camera RPC FOV filtering, catch-up, and spectator updates; `0` restores legacy broadcasts. This changes network update behavior. |
| `Marvel.GameState.CameraInfoQuantizedThreshold` | Minimum encoded Pitch/Yaw change since the last send to a connection; the adjacent help says default `20` matches existing camera setters and spectated targets bypass the threshold. |
| `Marvel.GameState.CameraInfoMindControlFix` | Keeps the original player's AI-controlled character camera rotation synchronized during possession, including skill camera actors. The help says it requires `CameraInfoFOVFilter`; `0` preserves existing filtering logic. |
| `Marvel.GameState.CameraRPCBatchCompressed` | `1` uses UID and 23-bit Pitch/Yaw in the camera batch RPC; `0` uses `SendCameraInfoRpc`. This is a network-format/update path, not image quality. |
| `Marvel.GameState.PhysProfile` | Embedded help says true opens a physics profile; appears to be a profiling/debug switch. |
| `AbilitySystem.GameplayCue.AudioThrottle.Enable` | Enables per-tag audio throttling and a per-frame concurrent limit for GameplayCues. Nearby text says disabling it in an emergency lets all audio play unconditionally. |
| `AbilitySystem.GameplayCue.AsyncHandlingWorkerNum` | Number of worker threads for asynchronous GameplayCue handling. `0` selects the synchronous path; positive counts are clamped to the Task Graph worker count. |
| `AbilitySystem.GameplayCue.DisableDynamicBudgetTimeOffset` | `0` keeps adaptive Cue queue-budget offsets enabled (default); `1` holds `BudgetTimeOffset` steady. The embedded help says to set it before gameplay. |
| `AbilitySystem.GameplayCue.EnablePerfOptimization` | Toggles experimental GameplayCue/CueCombine optimizations; embedded default is `0` (off), `1` enables them. |
| `AbilitySystem.GameplayCue.EnablePlaybackCache` | Toggles `CuePlaybackCache` for cue-index lookup (`0` off, `1` on). |
| `AbilitySystem.GameplayCue.EnableCueEventQueue` | Embedded help says it enables a queue to optimize GameplayCue handling. The exact queue policy and default are not stated. |
| `AbilitySystem.GameplayCue.MergeWhitelistReadLocks` | Merges whitelist reads under one lock; embedded text says `0` keeps legacy separate locks and `1` uses the merged path (default). |
| `AbilitySystem.GameplayCue.EnableAggressiveWhiteListCueOptimization` | Embedded help says cues are optimized except those on the whitelist. This is a behavior/performance switch whose impact on cue delivery should be checked in a match. |
| `AbilitySystem.GameplayCue.EnableAbilityCueTagUpdate` | When enabled, ability cues update the owning actor's tag map. This can change gameplay tag state as well as cue behavior. |
| `AbilitySystem.GameplayCue.EnableIgnoreCueTag` | Enables ignoring cue tags that could not be found; related command-like candidate `ClearIgnoredCueTags` clears the global ignored-tag set. |
| `AbilitySystem.GameplayCue.EnableCueAsyncForWeapon` / `EnableCueAsyncForWeaponAmmo` | The embedded help for both names says it enables async handling for `WeaponAmmoBase` and subclasses. Their separate implementation effects are not established. |
| `AbilitySystem.GameplayCue.CustomMaxCueActorsToPreAllocate` | Maximum number of GameplayCue actors to preallocate. |
| `AbilitySystem.GameplayCue.CustomPreAllocatedCueActorLifeSpan` | Lifetime for preallocated GameplayCue actors; unit is not stated in the adjacent text. |
| `AbilitySystem.GameplayCue.TickPreAllocateCueActorsInterval` | How often the preallocator ticks; unit and default are not stated. |
| `AbilitySystem.GameplayCue.TimeThresholdToRestoreBudgetOffset` | Number of seconds before attempting to restore the cue-queue budget offset; `0` disables restoration timing according to the help text. |
| `AbilitySystem.GameplayCue.EnableClearRedundantEventsForMissingCue` | Controls whether redundant events are cleared while their cue is still missing. |
| `AbilitySystem.GameplayCueFailLoads` | Command-like candidate: while true, it pretends all GameplayCues are unloaded and keeps requesting loads; false allows cues to play. This is unsuitable as a general performance override. |
| `AbilitySystem.GameplayCue.RunOnDedicatedServer` | Controls whether GameplayCue events run on a dedicated server. This can affect server/gameplay behavior. |
| `AbilitySystem.GameplayCue.EnableCueAsyncForCharacter` | Enables asynchronous cue handling for `MarvelBaseCharacter` and subclasses. |
| `AbilitySystem.GameplayCue.EnableCueAsyncForReticle` | Enables asynchronous cue handling for `MarvelAbilityWorldReticle_CueVisualization` and subclasses. |
| `AbilitySystem.GameplayCue.EnableCueAsyncForSummoned` | Enables asynchronous cue handling for `MarvelSummonedComponent` and subclasses. |
| `AbilitySystem.GameplayCue.EnableCueAsyncForTargetBase` | Enables asynchronous cue handling for `MarvelAbilityTargetActor_Base` and subclasses. |
| `AbilitySystem.EnableTaskPool` | `0` disables pooling; values above `0` pool non-simulated tasks; values above `2` use the owning actor as the outer. Simulated tasks are never pooled. |
| `AbilitySystem.GameplayEffects.MaxScopedExecutionNestCount` | Maximum nested Gameplay Effect applications within one scope. The default and response at the limit are not stated. |
| `AbilitySystem.GameplayEffects.MaxVersion` | Overrides the current Gameplay Effect version, disabling upgrade code paths. Treat as a compatibility/debug control. |
| `AbilitySystem.CueUserData.EnableVisibilityOptimization` | Enables visibility optimization while `CueDataProcessor` ticks. |
| `AbilitySystem.DisableGameplayCues` | Disables all GameplayCue events in the world. This removes gameplay effects/feedback and is not a rendering-only optimization. |
| `AbilitySystem.DisplayGameplayCues` | Displays GameplayCue events as text in the world; a debug visualization. |
| `ABS.EnableDamageCallbackCooldown` / `ABS.DamageCallbackCooldown` | Master switch for a damage-callback cooldown on `CanBeMerged` targets; false disables it. The cooldown is in seconds, and `0` disables it. This reduces callback frequency and can affect event timing. |
| `ABS.RemoteAttributeChangedEvent.Coalesce` | Coalesces complete remote simulated-proxy attribute-event dispatch for ASC opt-in actors (`0` off, `1` on). |
| `ABS.RemoteAttributeChangedEvent.IntervalMs` | Interval in milliseconds for coalesced remote attribute dispatch; `0` means next tick. |
| `ABS.SkipMonsterDamageCallbacks` | Bit flags for skipping damage notifications on Ability System Components whose `bTriggerDamageNotify` is false: bit `1` skips `OnApplyDamage`, bit `2` skips `OnTakeDamage`, `0` disables skipping. This changes gameplay callbacks. |
| `GAS.MaxNumActiveGameplayEffects` | Maximum number of active Gameplay Effects; `0` means unlimited. |
| `GAS.GameplayActorOverflowThreshold` | Per-class GameplayActor count threshold for overflow warnings; `0` disables the warning. |
| `GAS.DisableAbilitiesMT` | Embedded text says positive values disable ability multithreaded playback. Exact accepted values and whether this is a command or persistent CVar need confirmation. |
| `GAS.Projectile.EnableMergeOptimize` | Global switch for projectile merge/culling optimizations. This can alter projectile behavior and networked results. |
| `GAS.Projectile.MergeThreshold` | Active-actor count threshold that triggers spawn merging per `(Instigator, ProjId)`. |
| `GAS.Projectile.MergeMaxAngle` | Maximum direction difference in degrees for projectile merging. |
| `GAS.Projectile.MergeSpawnRadius` | Maximum spawn-location distance in centimeters for projectile merging. |
| `GAS.Projectile.MaxClientPerChar` / `MaxServerPerChar` | Projectile-count cap per `(Instigator, ProjId)` on client/server; `0` means unlimited. These can change projectile spawning or replication. |
| `GAS.Merge.ShouldPredict` | When projectile/scope merging is active, `0` disables client prediction (server-only, default), `1` predicts on the client. This is network/gameplay behavior. |
| `m.VisualMeshClone.Enable` | Global switch for a shared visual mesh-clone layer. The embedded help says ability-level opt-ins must use legacy paths when the global switch is disabled. |
| `marvelstats.HitchDetectThresholdInSeconds` | Frame time above this value is considered a hitch. |
| `marvelstats.MaxRingBufferSizeMB` | Maximum expanded ring-buffer size while collecting hitches; embedded help says it cannot exceed 256 MB. |
| `marvelstats.EnableOnlineHitchCounting` | Candidate for enabling online hitch counting by its name; adjacent text does not state its default or effect. |
| `marvelstats.HitchCollectDelayInSeconds` / `HitchCountingThresholdInSeconds` | Names indicate delay/threshold inputs for hitch collection/counting, but adjacent text does not establish their exact meanings or defaults. |
| `pve.ForceExecutionRate` | Forces the round-table execution rate in PvE damage calculation: `-1` uses normal `FMath::FRand()`; a value above `0` is used directly (help gives `0.99` for PlainHit and `0.01` for Dodge). This directly changes combat outcomes. |
| `pve.RedirectSourceToInstigator` | `1` uses a summon's instigator as the PvE damage source for attribute lookup; `0` (default) keeps the owner of the source Ability System Component. |
| `pve.RegenBeforeInitCost` | Reinitializes reduce/regen ability state before initializing gameplay ability cost to avoid attribute drift; default false. |
| `m.M2212.EndMatchOccluderDither.Enable` | Client-only master switch for M2212 end-match occluder dithering (`0` off, `1` on). |
| `m.MIParameterLock.UsePerInstance` | Selects the material-instance parameter lock scheme, effective immediately: `true` (default) uses per-instance `FRWSpinLock` to reduce cross-instance contention; `false` uses a legacy global mutex. The embedded help says to change it only at a safe point. |
| `m.MIParameterLog.Enable` | Enables material-instance parameter information on the console. Appears to be diagnostic output. |
| `m.MaterialTranslucencyPass.EnableOverride` | Enables the material-instance override for the material translucency pass. |
| `m.DisableDepthTest.EnableOverride` | Enables the material-instance override for `DisableDepthTest`. |
| `m.PinOther.Priority.Enable` | Enables priority-based admission for `UMarvelAbilityTask_PinOther`: only strictly higher-priority pins preempt, equal priority is first-come-first-served; `0` restores legacy indiscriminate preemption; default `1`. This affects ability behavior. |
| `m.PinnedMotion.ForceServerSocketUpdate` | Forces `GetSocketLocation` instead of lazy socket-transform lookup; `0` off (default), `1` on. |
| `m.PinnedMotion.PathAware.Enable` | Enables Path-Aware Corner Slide for PinnedMotion; `0` off (default), `1` on. |
| `m.PinnedMotion.PathAware.MaxStepSize` / `MinStepSize` | Maximum/minimum corner-slide step per frame in centimeters; defaults `80` and `8`. The minimum keeps motion when the source is stationary. |
| `m.PinnedTask.OutOfRangeDelay` | Sets the delay before a pinned task is considered out of range; unit and default are not stated in adjacent help. |
| `m.Ability230.KeepItemsOnEnd` | When true, ability `230` does not clear its interactive-item list on end. The embedded help says this addresses nearby portals becoming unusable after teleporting through one. |
| `m.Cue.SpawnByTargetName` | Controls whether to spawn a GameplayCue actor by target-actor name; default/range unknown. |
| `m.ability.<id>.UseVisualMeshCloneLayer` | Several hero/ability-specific switches opt into the shared visual mesh-clone layer. The global switch is `m.VisualMeshClone.Enable`; per-ability defaults and effects require their own code references. |
| `ChaosGC.ChaosCollisionNumThreshold` | Embedded description says this is a threshold for the number of fragment collisions. |
| `ChaosGC.EnableGlobalChaosCombineEffect` | Nearby text calls this a Boolean for enabling the global Chaos combine effect. |
| `ChaosGC.FrameISMCMaxTime` / `FrameISMCMaxNum` | Nearby default strings are `2.0` and `50` respectively. The names indicate time/count limits for frame-based ISMC work, but the time unit and handling are not stated. |
| `ChaosGC.FrameNiagaraMaxTime` | Nearby default string is `1.5`; the name suggests a frame-time budget for Niagara work, but units and behavior are not stated. |
| `ChaosGC.Niagara.MaxChaosEventNum` | Nearby help says this is the maximum number of break events sent to one component per frame; a nearby default string says `40`. |
| `ChaosGC.NiagaraRenderMeshPercent` | Embedded help calls it the rendering percentage of secondary fragments. The valid range and effect on gameplay state are unknown. |
| `ChaosGC.OnLikeMapLoaded_UpdateFrameBudget` | Frame budget, in seconds, for updating Chaos actors and client GC actors in an `OnLikeMapLoaded` callback; embedded text says `0` means no budget limit. |
| `marvel.AOIRelevantCache.Enable` | Enables a per-frame cache for `GetRelevantCharacters`: `0` uses the legacy traversal, `1` uses cached lookup, and `2` is labeled `opt copy`. The exact mode-2 behavior is unknown. |
| `marvel.TeamRelationCache` | Enables a per-frame TeamRelation cache (`1` on, `0` off) to avoid repeated `GetTeamComponent` lookups for actor pairs queried by cues. |
| `marvel.AllowClientSideNavigation` | Allows a client to create NavigationSystem and load Recast NavData (`0` off by default, `1` on). The help explicitly says set it before `LoadMap`; changing it after map load does not affect the current map. This is a memory/navigation behavior setting. |
| `marvel.Bink.AudioMode` | Chooses the Bink audio backend: `0` native Bink output, `1` routes through the Wwise bridge. Embedded help says to restart before first Bink playback after changing it. |
| `marvel.audio.DisableFootstep` | Footstep-audio policy: `0` preserves current behavior; `1` keeps the local player and components tagged `Audio.IgnoreDisableFootstep` while disabling others; `2` disables all footsteps. It changes audio content, not graphics. |
| `Marvel.Oodle.DisableLowCoreThreshold` | Logical-core threshold (including hyperthreads) at or below which Oodle is disabled on the client; read at `BeginPlay`. Related `Marvel.Oodle.bEnableLowCoreDisable` enables/disables this feature. This is a platform/network-compression control. |
| `Marvel.ProjectileRoute.EnableBattleRuleOverride` | Master gate for BattleRule projectile-class replacement. Help says `0` uses authored classes for all routes; `1` uses replacement classes only for selected routes (default enabled with ability `103021` selected). Toggling affects future spawns and preserves individual route states. This is gameplay behavior, not a safe graphics tweak. |
| `Marvel.HeroAssetLoader.ExcludeDomains.Local` / `ExcludeDomains.Remote` | Adds comma-separated asset `LoadDomain` exclusions for local/remote in-match presentation; `None` restores config and an invalid list is ignored. Help says set before a new match/PIE; existing subscriptions are not rebuilt. |
| `Marvel.HeroAssetLoader.KeepResident.Local` / `KeepResident.Remote` | Controls local/remote in-match presentation residency: `-1` follows config, `0` loads then releases, `1` holds resident; other values follow config. It does not change selected domains or grant timing, and must be set before a new match/PIE to affect existing subscriptions. |
| `Marvel.M2212.BoneSegment.EnableServerComponent` | Controls M2212's authoritative fracture component. `1` uses a server Dynamic component plus replicated client Kinematic presentation/hit proxies (default); `0` uses legacy client-only GameplayCue presentation while capsule and hit shapes remain authoritative. This changes replicated gameplay/physics presentation. |
| `Marvel.M2212.BoneSegment.RecoveryFloorClearance` | Extra centimeters above the floor used when the authoritative fracture center relocates a recovering character. |
| `Marvel.M2215.BoneSegment.FullServerSimulation` | Fracture replication policy sampled on authority at activation: `1` simulates/replicates every fragment (default); `0` makes only pelvis midline halves authoritative and other fragments local. The reduced mode requires a skill opt-in and complete pelvis halves or full simulation remains. |
| `Marvel.MonsterAbility408111.ClientComputeGhost` | Selects who computes ghost assignment/offsets for that monster ability: `1` client computes them, `0` server sends them. This changes gameplay/network behavior. |
| `Marvel.Scope.103811.UseRepTarget` | Uses the replicated target for ability 103811 on simulated proxies (default true). The help warns that marked-target drain is supported only when enabled; disabled falls back to primary-target-only rendering. |
| `Marvel.UI.EnableOverrideLoadFixup` | Enables a UI asset-load fix for a silent `OnLoaded` drop (default enabled); help associates it with an invisible battle panel bug. This is a targeted compatibility fix, not a general rendering control. |
| `Marvel.WeaponFireMerge.Enabled` | Merges weapon-fire requests by origin/direction when enabled (`1`, default); `0` fires each direction independently. This can affect weapon behavior. |
| `Marvel.GameState.TreatEventLODDistance` | Client-only: skips Treat events when both source and target are not the local player and are farther than this distance in centimeters. `0` disables the distance filter. |

These are stronger leads than names alone, but still require Ghidra references or runtime query before being treated as confirmed registered variables. The other unresolved entries remain listed in the full inventory without an asserted meaning.

The expanded `m.*` namespace surfaced a full portal-renderer family; the focused [portal CVar guide](cvar-game-build-4042190-portal-family.md) documents every one of its 74 `m.Portal.*` candidates, including value ranges where adjacent binary text provides them.

## Thread entries

“Epic 5.9” means Epic's reference describes the CVar. “Not located” means current status is unconfirmed for Marvel Rivals. Values in the first column are exactly what the author posted; they are not recommended defaults.

For the static scan, an embedded name is only a literal-presence fact. In particular, `r.TextureStreaming.DiscardUnusedMips`, `r.VirtualTextureReducedMemory`, `TaskGraph.MaxWorkerThreads`, `TaskGraph.MaxTaskThreadsPerGroup`, `r.DirectX.UsePerQueueFence`, `r.ParallelInitDynamicRHI`, `r.RHICmdUseThread`, `r.TaskGraph.TasksPerThread`, `a.ParallelSkeletalMeshUpdate`, `au.DisableParallelAudioProcessing`, `gc.AssetClusteringEnabled`, `gc.CreateGarbageCollectorUObjectClusters`, `gc.MinDesiredObjectsPerSubTask`, `p.AsyncSceneEnabled`, and `s.LevelStreamingActorsPerPage` were not found as exact strings in this executable. The three absent input keys are `bDisableMouseAcceleration`, `bViewAccelerationEnabled`, and `RawMouseInputEnabled`.

### Texture and mesh streaming

| Posted override | Meaning / evidence |
| --- | --- |
| `r.Streaming.MipBias=0` | Global streaming mip bias. Zero requests no extra mip reduction; positive values drop detail levels to reduce memory demand. Epic documents this. |
| `r.Streaming.MaxNumTexturesToStreamPerFrame=32` | Limits texture uploads from CPU memory to GPU memory per frame; non-positive means unlimited in Epic's reference. Epic notes it only has an effect with `r.Streaming.AmortizeCPUToGPUCopy` enabled. |
| `r.Streaming.DelayProcessPendingMipCopyRequests=1` | Not located in Epic 5.9. Name suggests scheduling pending mip-copy work, but exact semantics and validity in Marvel Rivals are unknown. |
| `r.Streaming.FramesForFullUpdate=30` | Frames between full texture-streamer updates. Higher values reduce update work but make the streamer react more slowly to viewpoint/visibility changes. |
| `r.TextureStreaming.DiscardUnusedMips=1` | Not located as written. Epic documents `r.TextureStreaming` and the separate `r.Streaming.*` family, but not this exact name. Do not assume it is accepted or that it means “free unused mips.” |
| `r.VirtualTextureReducedMemory=0` | Epic documents this as reducing virtual-texture cost through a more packed layout when enabled. The posted zero leaves that optimization disabled in the documented engine. |
| `r.MeshStreaming=1` | Epic labels mesh streaming experimental and says nonzero enables it. This may depend on game asset support and build-time setup; enabling it does not create missing mesh LOD data. |
| `r.Streaming.PoolSize=12288` | Texture streamer pool target in MB in the Epic reference. The pool can include UI, non-streaming textures, cubemaps, and platform-dependent resources. A larger number reserves/allows more budget; it is not a guarantee that 12 GB is available or safe. |
| `r.Streaming.PoolSizeForMeshes=512` | Epic: negative shares texture/mesh pools; nonnegative sets a dedicated mesh pool size. The thread's 512 is a 512 MB mesh-pool target in the referenced implementation. |
| `r.Streaming.PoolSizeForGCs=256` | Not located in Epic 5.9. Exact owner, units, and whether “GCs” means geometry collections or garbage collection are unconfirmed. Do not infer its behavior from the name. |
| `r.Streaming.LimitPoolSizeToVRAM=1` | Epic: limits texture pool size to available GPU memory when enabled. It is not a VRAM allocator and cannot make an oversized pool safe; combined pool accounting may differ by platform/game fork. |
| `r.Streaming.AmortizeCPUToGPUCopy=1` | Epic: when enabled, `MaxNumTexturesToStreamPerFrame` limits the number of 2D textures copied from CPU to GPU per frame. It spreads streaming work out; the direct benefit is smoother upload workload, not necessarily a higher average frame rate. |
| `r.Streaming.NumStaticComponentsProcessedPerFrame=50` | Epic: number of static components incrementally processed per frame before a level is visible (in the streaming setup described by the reference). It is not a general per-frame texture count. |
| `r.Streaming.MaxEffectiveScreenSize=0` | Zero means use actual vertical screen size in Epic's reference; a positive value clamps the screen-size input used to calculate wanted texture mips. |

### GPU, render thread, and latency

| Posted override | Meaning / evidence |
| --- | --- |
| `r.ParallelInitDynamicRHI=1` | Not located in Epic 5.9. The name implies parallel initialization of the Render Hardware Interface, but whether this CVar exists or has any effect in the Marvel build is unknown. |
| `r.RHICmdUseThread=1` | Not located in Epic 5.9. Likely related to dispatching RHI commands from a dedicated thread based on the name; do not treat that guess as a verified description. |
| `r.DirectX.UsePerQueueFence=1` | Not located in Epic 5.9. Likely a DirectX queue/fence synchronization switch; exact behavior, supported queues, and safety are unverified. |
| `r.D3D12.GPUTimeout=0` | Epic's reference says zero disables GPU timeout and explicitly warns that a GPU stall can freeze the PC. This is a watchdog/debugging behavior change, not a latency optimization. Avoid recommending it as a routine setting. |
| `r.OneFrameThreadLag=1` | Epic CVar reference describes the engine's one-frame render-thread lag behavior. This setting can affect CPU/GPU pipelining and latency; its name alone does not tell whether enabling or disabling is preferable for a given bottleneck. |
| `RHI.MaximumFrameLatency=1` | RHI frame-latency limit. Lower queued frames can reduce input-to-display delay but may reduce throughput or cause uneven frame pacing. Exact behavior depends on the RHI/driver and game integration; verify in-game. |
| `r.GTSyncType=2` | Not located in Epic 5.9 reference. The poster says “try 1 or 2”; exact modes and behavior in this game are unverified. The number cannot be assumed to mean a universal sync policy. |
| `r.MeshCardRepresentation.Async=1` | Epic reference lists the CVar, but its description is just “.”; the adjacent `r.MeshCardRepresentation` family concerns mesh cards (used by rendering features such as Lumen in UE). The exact async operation/effect in Marvel Rivals is not documented by Epic's entry. |
| `r.SkinCache.CompileShaders=1` | Epic: controls whether to compile GPU compute skin-cache shaders. The documented default is 0. Epic notes changing it requires touching a shader source file to cause a recompile, so forcing `1` in a shipping config is not evidence that it compiles anything or switches meshes to compute skinning. |
| `r.TeamOutline.LineWidth=2` | Not located in Epic 5.9. Likely game-specific outline width from the name, but this has not been verified in the Marvel build. Do not assume its units or allowed range. |

### Task graph, animation, physics, and audio

| Posted override | Meaning / evidence |
| --- | --- |
| `TaskGraph.MaxWorkerThreads=8` | Not located in Epic 5.9. Name suggests a cap for Task Graph worker threads; exact semantics and whether the game uses this legacy/custom variable are unknown. |
| `TaskGraph.MaxTaskThreadsPerGroup=8` | Not located in Epic 5.9. Exact scheduling behavior is unknown; do not assume it simply adds eight threads. |
| `r.TaskGraph.TasksPerThread=2` | Not located in Epic 5.9. Could be fork-specific scheduler tuning; runtime registration and interpretation unknown. |
| `r.ForceAllCoresForShaderCompiling=1` | Not located in Epic 5.9. Shader compilation is mostly a startup/build-time concern; a shipping client may not expose this or recompile shaders due to this setting. |
| `a.EnableVisibilityBasedTickOptimization=1` | Not located in Epic 5.9. Name suggests suppressing/tuning actor or animation updates when not visible; precise scope and gameplay consequences unknown. |
| `a.ParallelAnimUpdate=1` | Epic: permits animation blend-tree/native update, asset player, and montage update work on worker threads where possible. |
| `a.ParallelAnimEvaluation=1` | Epic: evaluates animation across the Task Graph instead of purely on the game thread. |
| `a.ParallelAnimInterpolation=1` | Epic: runs animation interpolation across the Task Graph instead of purely on the game thread. |
| `a.ParallelSkeletalMeshUpdate=1` | Not located in Epic 5.9. Likely a Marvel/engine-fork switch for parallel skeletal-mesh component updates; exact implementation and safety are unknown. |
| `spine.MaxSkeletonFrameRate=0` | Not located in Epic 5.9. Likely belongs to a Spine runtime/plugin, but the meaning of zero (unlimited, disabled cap, or default) is unknown. |
| `p.AsyncSceneEnabled=1` | Not located in Epic 5.9. Appears to be a physics async-scene switch from its name; modern Chaos physics configuration may not use it. Exact game behavior is unknown. |
| `tick.AllowAsyncProjectileComponent=1` | Not located in Epic 5.9. Likely game-specific asynchronous projectile component ticking. Potentially gameplay-sensitive; no implementation evidence yet. |
| `tick.AllowAsyncNetTicks=1` | Not located in Epic 5.9. Likely asynchronous network-related ticking; exact scope, compatibility, and effect on authoritative gameplay are unknown. |
| `tick.AllowAsyncSummonedComponent=1` | Not located in Epic 5.9. Likely game-specific ticking for summoned components; exact behavior is unknown. |
| `au.DisableParallelAudioProcessing=0` | Not located in Epic 5.9. Name implies `1` disables parallel audio processing, so the posted `0` would leave it enabled if the CVar exists; exact game implementation is unverified. |

### Chaos geometry collections (physics effects)

These names use `GC` in the Chaos/physics section and should not be conflated with `gc.*` Unreal UObject garbage-collection variables below.

| Posted override | Meaning / evidence |
| --- | --- |
| `p.Chaos.GCRemoveInternalfaceFaceRender=0` | Not located in Epic 5.9. The spelling is exactly as posted. It appears to concern internal-face removal/rendering for Chaos Geometry Collections, but exact semantics are unknown. |
| `p.Chaos.GGCRemoveInternalfaceFaceInShadow=0` | Not located in Epic 5.9. Spelling includes `GGC`; do not silently “correct” it. Likely geometry-collection shadow handling, but unverified. |
| `p.chaos.ChoseGCLOD=1` | Not located in Epic 5.9. Likely a game-specific Geometry Collection LOD selector. The misspelling/casing is preserved from the post; effect and valid values unknown. |
| `p.chaos.ChoseGCSecondaryLOD=1` | Not located in Epic 5.9. Likely a secondary Geometry Collection LOD selector; exact behavior and valid values unknown. |
| `p.Chaos.ClientGCMaxRenderNum=64` | Not located in Epic 5.9. Likely a client-side rendering cap/count for Geometry Collections. Whether `64` counts objects, pieces, or something else is unknown. |
| `p.Chaos.PerformGeometryReduction=1` | Not located in Epic 5.9. Name suggests reducing Geometry Collection geometry, but whether this is runtime, cooking, or game-specific is unknown. |

### UObject garbage collection and loading

| Posted override | Meaning / evidence |
| --- | --- |
| `gc.MultithreadedDestructionEnabled=1` | Epic: frees object memory from a worker thread. It is about UObject destruction, not Chaos Geometry Collections. |
| `gc.CreateGCClusters=1` | Epic: attempts object clusters for more efficient garbage collection. |
| `gc.AllowParallelGC=1` | Epic: controls parallel garbage collection. |
| `gc.MinDesiredObjectsPerSubTask=120` | Not located in Epic 5.9. Likely a game-fork threshold for dividing GC work among subtasks; exact units/meaning unknown. |
| `gc.AssetClusteringEnabled=True` | Not located with this exact spelling. Epic's reference instead lists `gc.AssetClustreringEnabled` (misspelled) for asset-file clusters. Do not assume this thread spelling maps to that CVar. |
| `gc.ActorClusteringEnabled=True` | Epic documents `gc.ActorClusteringEnabled` as controlling actor clusters. Its reference default is `0`; setting it to true enables the feature in builds that support it. |
| `gc.CreateGarbageCollectorUObjectClusters=True` | Not located in Epic 5.9. Likely a game-specific cluster switch; do not confuse it with the documented `gc.CreateGCClusters`. |
| `gc.LowMemory.MemoryThresholdMB=2048` | Epic: threshold in MB for low-memory GC mode. Setting 2048 means the threshold is 2 GiB in the documented version, though the game may define what memory measurement triggers it. |
| `gc.LowMemory.TimeBetweenPurgingPendingKillObjects=10.0` | Epic: seconds between purges of pending-kill objects in low-memory mode. Lower values may reclaim sooner but can increase GC work/hitches. |
| `gc.TimeBetweenPurgingPendingKillObjects=60` | Epic: interval in seconds between purging references to pending-kill objects. This is not a fixed 60-second full-GC cadence. |
| `gc.IncrementalBeginDestroyEnabled=1` | Epic: spreads object destruction over frames using a per-frame time limit. This can trade a long destruction spike for work across multiple frames. |
| `s.IoDispatcherDecompressionWorkerCount=6` | Epic: number of IoDispatcher decompression workers. More workers may increase parallel decompression throughput while also consuming CPU and memory bandwidth. |
| `s.IoDispatcherBufferMemoryMB=1024` | Epic: IoDispatcher buffer memory size in MB. The reference default is 8 MB; a 1024 MB override is a large memory budget change, not automatically faster. |
| `s.IoDispatcherCacheSizeMB=2048` | Epic: IoDispatcher cache memory size in MB. The reference default is 0; a nonzero cache can consume substantial memory. Whether it helps Marvel Rivals' asset access is unbenchmarked. |
| `s.MaxPrecacheRequestsInFlight=32` | Epic: maximum number of in-flight precache requests. Higher concurrency can raise CPU/storage pressure and does not guarantee faster loading. |
| `s.MinBulkDataSizeForAsyncLoading=0` | The Epic 5.9 row's description appears inconsistent with its name (“Minimum time the time limit exceeded warning will be triggered by”). Treat intended threshold/units and the effect of zero as unresolved until checked against Marvel's exact source/build. |
| `s.ProcessPrestreamingRequests=1` | Epic: when nonzero, processes prestreaming requests in cooked builds. This controls request processing, not a general “load everything earlier” toggle. |
| `s.IoDispatcherTocsEnablePerfectHashing=1` | Epic: enables perfect hashmap lookups for IoStore TOCs. This is a lookup implementation detail; runtime/build support is required. |
| `s.AsyncLoadingThreadEnabled=1` | Epic labels this a placeholder CVar that is currently not used at runtime. Do not count on the `1` enabling a loading thread. |
| `s.AsyncLoadingTimeLimit=2.0` | Epic documents milliseconds per frame spent on async loading. The reference's default is 5; the community post's 2.0 is a smaller budget and may defer load work rather than speed it up. |
| `s.ForceGCAfterLevelStreamedOut=0` | Epic: whether to force GC after levels stream out, reclaiming memory at the cost of a hitch. Zero avoids forcing that GC through this mechanism. |
| `s.LevelStreamingActorsPerPage=1000` | Not located in Epic 5.9. Likely a game-specific level-streaming actor batch/page setting; meaning, units, and effect unknown. |
| `s.AdaptiveAddToWorld.Enabled=1` | Epic: enables adaptive AddToWorld time slicing, replacing `s.LevelStreamingActorsUpdateTimeLimit` in the documented version. The default is off. |

### Visual detail and model LODs

| Posted override | Meaning / evidence |
| --- | --- |
| `skelot.ForceLOD=0` | Not located in Epic 5.9. Likely belongs to a project/plugin named Skelot. Zero may mean “do not force” but that is only a naming guess; plugin code/game runtime is needed. |
| `r.SkeletalMeshLODRadiusScale=1.0` | Epic: scales the screen radius used to compute skeletal-mesh discrete LOD; documented range is 0.25–1. A lower value can make LOD selection behave as if the mesh were smaller on screen, leading to earlier lower-detail LODs. |
| `r.SkeletalMeshLODBias=0` | Epic's scalability reference says this globally biases skeletal-mesh LOD selection. Zero adds no global bias; positive/negative direction should be checked against the specific engine version and mesh LOD setup before use. |
| `r.EnableMorphTargets=1` | Epic: enables morph targets. This does not make morph data appear on a mesh that was cooked without the needed morph targets. |
| `r.StaticMeshLODBias=0` | Not located in Epic 5.9 reference. It may be fork-specific; Epic documents `r.StaticMeshLODDistanceScale`, which is a different CVar and must not be substituted by name. |
| `r.ViewDistanceScale=1` | Epic CVar reference describes a global multiplier for view distance. Increasing it can retain/draw more objects farther away, with CPU/GPU cost. |
| `r.StaticMeshLODDistanceScale=1` | Epic: scales distance for static-mesh discrete LOD selection. Higher values make LOD transitions earlier (for example, 2 means twice as quickly/half the distance); 1 is the reference default. |
| `r.DetailMode=2` | Epic: detail mode determines which components are updated/ticked; 0 low, 1 medium, 2 high, 3 epic in the reference. It can suppress detail-tagged content; it is not simply texture quality. |

### Image effects

| Posted override | Meaning / evidence |
| --- | --- |
| `r.PostProcessing.DisableMaterials=1` | Not located in Epic 5.9. Likely disables post-process materials in this game/fork; possible visual/gameplay/UI side effects unknown. The thread's “disable Chronovision” label is an author claim, not verified causation. |
| `r.LightTile.Enable=0` | Not located in Epic 5.9. Name suggests a tiled-lighting feature; exact feature and visual/performance consequences unknown. |
| `r.CustomDepth=0` | Epic: controls custom depth rendering (the reference discusses the CVar family). Disabling it can break outlines, occlusion effects, and other materials that depend on the custom-depth buffer. It may affect character visibility cues, so do not present this as a harmless performance switch. |

### Input settings copied from the post (not established as CVars)

| Posted line | Status |
| --- | --- |
| `bDisableMouseAcceleration=1` | Looks like a boolean config property, not a CVar. Its owning config section and whether Marvel Rivals reads it are not established. |
| `bEnableMouseSmoothing=0` | Looks like a boolean config property, not a CVar. Do not assume Unreal's generic input option uses this exact key. |
| `bViewAccelerationEnabled=0` | Looks like a boolean config property, not a CVar. Game-specific registration/section unknown. |
| `RawMouseInputEnabled=1` | Looks like a boolean config property, not a CVar. Game-specific registration/section unknown. |

## Additional related CVars found in Epic's reference

These are useful research leads beyond the original post, not confirmed Marvel Rivals overrides:

| CVar | Documented role |
| --- | --- |
| `r.Streaming.UsePerTextureBias` | Lets the streamer assign individual mip bias values to fit the texture pool; it changes how global mip bias is applied. |
| `r.Streaming.FullyLoadUsedTextures` | Streams used textures to their highest available resolution and keeps them resident. Epic describes it as an alternative to disabling texture streaming entirely; it can use much more memory. |
| `r.Streaming.UseAllMips` | Removes mip-resolution limits in the documented streamer. Epic recommends it for showcases/promotional rendering, not as a general low-risk optimization. |
| `r.Streaming.UseFixedPoolSize` | Prevents the pool size from changing at runtime when nonzero. |
| `r.Streaming.MaxTempMemoryAllowed` | Caps temporary memory used to update streamed texture mips; too low can limit streaming speed. |
| `r.Streaming.UseMaterialData` | Uses material texture scale/coordinate data when calculating texture streaming requirements. |
| `s.LevelStreamingActorsUpdateTimeLimit` | Per-frame time limit for actor registration during level streaming. `s.AdaptiveAddToWorld.Enabled` replaces this mechanism in the documented configuration. |
| `gc.IncrementalGCTimePerFrame` | Time budget per frame for incremental garbage collection. This is distinct from `gc.IncrementalBeginDestroyEnabled`. |
| `TaskGraph.NumForegroundWorkers` | Number of foreground Task Graph worker threads (Epic 5.9 default: 2). Epic says the scheduler must be restarted for a change to take effect. The name is also embedded in this Marvel build. |
| `TaskGraph.ForkedProcessMaxWorkerThreads` | Worker-thread count for forked child processes that allow Task Graph multithreading (Epic default: 2); it does not mean “set the whole game's worker pool to this many.” Embedded in the Marvel build. |
| `TaskGraph.UseBackgroundThreads` | When positive, allows background tasks to use background-priority threads; zero routes them to normal-priority Task Graph threads (Epic default: 1). Embedded in the Marvel build. |
| `TaskGraph.UseHiPriThreads` | When positive, enables high-priority Task Graph worker threads; zero routes background tasks to normal-priority workers (Epic default: 1). Embedded in the Marvel build. |
| `TaskGraph.UseDynamicPrioritization` | Adjusts thread priority per task so high-priority work on background threads is less likely to be preempted (Epic default: true). Embedded in the Marvel build. |
| `tick.AllowAsyncComponentTicks` | General Unreal control for asynchronous component ticks (Epic default: 1). This is a different, broader variable than Marvel's `tick.AllowAsyncProjectileComponent`, `tick.AllowAsyncNetTicks`, and `tick.AllowAsyncSummonedComponent`, whose individual effects remain undocumented. Embedded in the Marvel build. |

Before adding any of these, confirm the current game's registry and compare behavior with the setting absent. A generic Unreal reference is not a Marvel Rivals compatibility list.

## Registry definitions for the posted CVar keys

The following cross-check uses exact CVar names from the posted override list, including keys that appear only in the reset block. Registry help text is copied from the preserved community attachment; it is a direct static definition when present, but still does not prove runtime behavior in build 1.1.4042190. The source does not include 15 of these names.

| CVar | Registry status | Type(s) | Help text |
|---|---|---|---|
| `a.EnableVisibilityBasedTickOptimization` | Registered in attachment | int32 | When enabled, skeletalmeshcomponent will stop tick when bVisible == false or bHiddenInGame == true |
| `a.ParallelAnimEvaluation` | Registered in attachment | int32 | If 1, animation evaluation will be run across the task graph system. If 0, evaluation will run purely on the game thread |
| `a.ParallelAnimInterpolation` | Registered in attachment | int32 | If 1, animation interpolation will be run across the task graph system. If 0, interpolation will run purely on the game thread |
| `a.ParallelAnimUpdate` | Registered in attachment | int32 | If != 0, then we update animation blend tree, native update, asset players and montages (is possible) on worker threads. |
| `a.ParallelSkeletalMeshUpdate` | No exact registry entry | — | — |
| `au.DisableParallelAudioProcessing` | No exact registry entry | — | — |
| `gc.ActorClusteringEnabled` | Registered in attachment | int32 | Whether to allow levels to create actor clusters for GC. |
| `gc.AllowParallelGC` | Registered in attachment | int32 | Used to control parallel GC. |
| `gc.AssetClusteringEnabled` | No exact registry entry | — | — |
| `gc.CreateGarbageCollectorUObjectClusters` | No exact registry entry | — | — |
| `gc.CreateGCClusters` | Registered in attachment | int32 | If true, the engine will attempt to create clusters of objects for better garbage collection performance. |
| `gc.IncrementalBeginDestroyEnabled` | Registered in attachment | int32 | If true, the engine will destroy objects incrementally using time limit each frame |
| `gc.LowMemory.MemoryThresholdMB` | Registered in attachment | float | Memory threshold for low memory GC mode, in MB |
| `gc.LowMemory.TimeBetweenPurgingPendingKillObjects` | Registered in attachment | float | Time in seconds (game time) we should wait between purging object references to objects that are pending kill when we're low on memory |
| `gc.MinDesiredObjectsPerSubTask` | No exact registry entry | — | — |
| `gc.MultithreadedDestructionEnabled` | Registered in attachment | int32 | If true, the engine will free objects' memory from a worker thread |
| `gc.TimeBetweenPurgingPendingKillObjects` | Registered in attachment | float | Time in seconds (game time) we should wait between purging object references to objects that are pending kill. |
| `p.AsyncSceneEnabled` | No exact registry entry | — | — |
| `p.chaos.ChoseGCLOD` | Registered in attachment | int32 | warning, for low memory machine, we choose the lod level, and discards other lod resources |
| `p.chaos.ChoseGCSecondaryLOD` | Registered in attachment | int32 | warning, for low memory machine, we choose the lod level for secondary fragment, and discards other lod resources |
| `p.Chaos.ClientGCMaxRenderNum` | Registered in attachment | int32 | Define the max number of client gc to render |
| `p.Chaos.GCRemoveInternalfaceFaceRender` | Registered in attachment | int32 | Disable rendering of internal face in geometry collection |
| `p.Chaos.GGCRemoveInternalfaceFaceInShadow` | Registered in attachment | int32 | Disable shadow rendering of internal face in geometry collection |
| `p.Chaos.PerformGeometryReduction` | Registered in attachment | int32 | Perform convex geometry simplification to increase performance in Chaos physics. |
| `r.CustomDepth` | Registered in attachment | int32 | 0: feature is disabled<br>1: feature is enabled, texture is created on demand<br>2: feature is enabled, texture is not released until required (should be the project setting if the feature should not stall)<br>3: feature is enabled, stencil writes are enabled, texture is not released until required (should be the project setting if the feature should not stall) |
| `r.D3D12.GPUTimeout` | Registered in attachment | int32 | 0: Disable GPU Timeout; use with care as it could freeze your PC!<br>1: Enable GPU Timeout; operation taking long on the GPU will fail(default) |
| `r.DetailMode` | Registered in attachment | int32 | Current detail mode; determines whether components of actors should be updated/ ticked.<br> 0: low, show only object with DetailMode low or higher<br> 1: medium, show all object with DetailMode medium or higher<br> 2: high, show all objects (default) |
| `r.DirectX.UsePerQueueFence` | No exact registry entry | — | — |
| `r.EnableMorphTargets` | Registered in attachment | int32 | Enable Morph Targets |
| `r.ForceAllCoresForShaderCompiling` | Registered in attachment | int32 | When set to 1, it will ignore INI settings and launch as many ShaderCompileWorker instances as cores are available.<br>Improves shader throughput but for big projects it can make the machine run OOM |
| `r.FreeSkeletalMeshBuffers` | Registered in attachment | int32 | Controls whether skeletal mesh buffers are kept in CPU memory to support merging of skeletal meshes.<br>0: Keep buffers(default)<br>1: Free buffers |
| `r.GTSyncType` | Registered in attachment | int32 | Determines how the game thread syncs with the render thread, RHI thread and GPU.<br>Syncing to the GPU swap chain flip allows for lower frame latency.<br> 0 - Sync the game thread with the render thread (default).<br> 1 - Sync the game thread with the RHI thread.<br> 2 - Sync the game thread with the GPU swap chain flip (only on supported platforms). |
| `r.LightTile.Enable` | Registered in attachment | int32 | — |
| `r.MeshCardRepresentation.Async` | Registered in attachment | int32 | — |
| `r.MeshStreaming` | Registered in attachment | int32 | Experimental - When non zero, enables mesh stremaing. |
| `r.OneFrameThreadLag` | Registered in attachment | int32 | Whether to allow the rendering thread to lag one frame behind the game thread (0: disabled, otherwise enabled) |
| `r.ParallelInitDynamicRHI` | No exact registry entry | — | — |
| `r.PostProcessing.DisableMaterials` | Registered in attachment | int32 | Allows to disable post process materials. |
| `r.RHICmdUseThread` | No exact registry entry | — | — |
| `r.SkeletalMeshLODBias` | Registered in attachment | int32 | LOD bias for skeletal meshes (does not affect animation editor viewports). |
| `r.SkeletalMeshLODRadiusScale` | Registered in attachment | float | Scale factor for the screen radius used in computing discrete LOD for skeletal meshes. (0.25-1) |
| `r.SkinCache.CompileShaders` | Registered in attachment | int32 | Whether or not to compile the GPU compute skinning cache shaders.<br>This will compile the shaders for skinning on a compute job and not skin on the vertex shader.<br>GPUSkinVertexFactory.usf needs to be touched to cause a recompile if this changes.<br>0 is off(default), 1 is on |
| `r.StaticMeshLODBias` | Registered in attachment | int32 | Static Mesh LOD Bias |
| `r.StaticMeshLODDistanceScale` | Registered in attachment | float | Scale factor for the distance used in computing discrete LOD for static meshes. (defaults to 1)<br>(higher values make LODs transition earlier, e.g., 2 is twice as fast / half the distance) |
| `r.Streaming.AmortizeCPUToGPUCopy` | Registered in attachment | int32 | If set and r.Streaming.MaxNumTexturesToStreamPerFrame > 0, limit the number of 2D textures streamed from CPU memory to GPU memory each frame |
| `r.Streaming.DelayProcessPendingMipCopyRequests` | Registered in attachment | bool | If true, call ProcessPendingMipCopyRequests at the beginning of UpdateResourceStreaming.This means the process is delay until the next frame, but it can optimize the time spent on waiting FUpdateStreamingRenderAssetsTask. |
| `r.Streaming.FramesForFullUpdate` | Registered in attachment | int32 | Texture streaming is time sliced per frame. This values gives the number of frames to visit all textures. |
| `r.Streaming.LimitPoolSizeToVRAM` | Registered in attachment | int32 | If non-zero, texture pool size with be limited to how much GPU mem is available. |
| `r.Streaming.MaxEffectiveScreenSize` | Registered in attachment | float | 0: Use current actual vertical screen size<br>> 0: Clamp wanted mip size calculation to this value for the vertical screen size component. |
| `r.Streaming.MaxNumTexturesToStreamPerFrame` | Registered in attachment | int32 | Maximum number of 2D textures allowed to stream from CPU memory to GPU memory each frame. <= 0 means no limit. This has no effect if r.Streaming.AmortizeCPUToGPUCopy is not set |
| `r.Streaming.MipBias` | Registered in attachment | float | 0..x reduce texture quality for streaming by a floating point number.<br>0: use full resolution (default)<br>1: drop one mip<br>2: drop two mips |
| `r.Streaming.NumStaticComponentsProcessedPerFrame` | Registered in attachment | int32 | If non-zero, the engine will incrementaly inserting levels by processing this amount of components per frame before they become visible |
| `r.Streaming.PoolSize` | Registered in attachment | int32 | -1: Default texture pool size, otherwise the size in MB |
| `r.Streaming.PoolSizeForGCs` | Registered in attachment | int32 | < 0: GeometryCollection and texture share the same pool, otherwise the size of pool dedicated to GeometryCollections. |
| `r.Streaming.PoolSizeForMeshes` | Registered in attachment | int32 | < 0: Mesh and texture share the same pool, otherwise the size of pool dedicated to meshes. |
| `r.Streaming.UsePerMeshBias` | Registered in attachment | int32 | If non-zero, each mesh will be assigned a mip bias between 0 and MipBias as required to fit in budget. |
| `r.TaskGraph.TasksPerThread` | No exact registry entry | — | — |
| `r.TeamOutline.LineWidth` | Registered in attachment | int32 | Team outline line width (only 1 or 2 width avaliable now).Not working for LineMode 0, only LineMode 1 and 2Exterior line mode : skip internal pixels;Internal line mode : True/1 -> 4 samples, False/0 ->8 samples |
| `r.TextureStreaming.DiscardUnusedMips` | No exact registry entry | — | — |
| `r.ViewDistanceScale` | Registered in attachment | float | Controls the view distance scale. A primitive's MaxDrawDistance is scaled by this value.<br>Higher values will increase view distance but at a performance cost.<br>Default = 1. |
| `r.VirtualTextureReducedMemory` | No exact registry entry | — | — |
| `RHI.MaximumFrameLatency` | Registered in attachment | int32 | Number of frames that can be queued for render. |
| `s.AdaptiveAddToWorld.Enabled` | Registered in attachment | int32 | Enables the adaptive AddToWorld timeslice (replaces s.LevelStreamingActorsUpdateTimeLimit) (default: off) |
| `s.AsyncLoadingThreadEnabled` | Registered in attachment | int32 | Placeholder console variable, currently not used in runtime. |
| `s.AsyncLoadingTimeLimit` | Registered in attachment | float | Maximum amount of time to spend doing asynchronous loading (ms per frame). |
| `s.ForceGCAfterLevelStreamedOut` | Registered in attachment | int32 | Whether to force a GC after levels are streamed out to instantly reclaim the memory at the expensive of a hitch. |
| `s.IoDispatcherBufferMemoryMB` | Registered in attachment | int32 | IoDispatcher buffer memory size (in megabytes). |
| `s.IoDispatcherCacheSizeMB` | Registered in attachment | int32 | IoDispatcher cache memory size (in megabytes). |
| `s.IoDispatcherDecompressionWorkerCount` | Registered in attachment | int32 | IoDispatcher decompression worker count. |
| `s.IoDispatcherTocsEnablePerfectHashing` | Registered in attachment | int32 | Enable perfect hashmap lookups for iostore tocs |
| `s.LevelStreamingActorsPerPage` | No exact registry entry | — | — |
| `s.MaxPrecacheRequestsInFlight` | Registered in attachment | int32 | Controls the maximum amount of precache requests to have in flight. |
| `s.MinBulkDataSizeForAsyncLoading` | Registered in attachment | int32 | Minimum time the time limit exceeded warning will be triggered by. |
| `s.ProcessPrestreamingRequests` | Registered in attachment | int32 | If non-zero, then we process prestreaming requests in cooked builds. |
| `skelot.ForceLOD` | Registered in attachment | int32 | similar to r.ForceLOD, -1 to disable |
| `spine.MaxSkeletonFrameRate` | Registered in attachment | int32 | If 0 (default), no limit is enforced. If greater than 0, the maximum frame rate for a skeleton is limited to this value. |
| `TaskGraph.MaxTaskThreadsPerGroup` | No exact registry entry | — | — |
| `TaskGraph.MaxWorkerThreads` | No exact registry entry | — | — |
| `tick.AllowAsyncNetTicks` | Registered in attachment | int32 | Set 0 for disable parallel optimation for net tick. |
| `tick.AllowAsyncProjectileComponent` | Registered in attachment | bool | Set 0 for disable parallel optimation of projectile movement component. |
| `tick.AllowAsyncSummonedComponent` | Registered in attachment | bool | Set 0 for disable parallel optimation for components of Summoners. |

## Important corrections and risks in the community bundle

- The 5060 Ti pool values (`12288`, `512`, `256`) are not automatically valid for a 16 GB card. They are pool budgets, with different resources and drivers potentially counted differently; VRAM also has to cover render targets, buffers, game assets, and the desktop.
- `r.D3D12.GPUTimeout=0` removes the GPU timeout guard in Epic's documented implementation and can freeze the machine if the GPU hangs.
- `s.IoDispatcherBufferMemoryMB=1024` and `s.IoDispatcherCacheSizeMB=2048` reserve large memory budgets. Larger buffers/caches can crowd out other game/system memory and are not proof of higher throughput.
- Some variables are spelling-sensitive. Preserve exact names, including `gc.AssetClusteringEnabled` vs Epic's differently spelled `gc.AssetClustreringEnabled`, and the thread's `GGC`, `Chose`, and `InternalfaceFace` names, until the game's own registration confirms the intended spelling.
- The `!` lines under “Fix Broken Retexture Mods” use this loader's reset-to-game-value behavior. They do not force high LODs. The section also contains duplicate resets of the same `r.SkeletalMeshLODBias` key.
- Turning off custom depth or post-process material paths can remove visual information, not just cosmetic effects.
- Parallel/tick/physics/network variables may affect timing or gameplay correctness. Names imply intent but do not prove thread safety in the game's fork.

## Follow-up research needed

1. Confirm exact CVar registration and startup values from the running Marvel Rivals build (console query, engine log, or sufficiently complete binary/runtime inspection). A config line being accepted by the loader is not proof the engine recognized it.
2. Inspect the thread's four attached screenshots for their actual benchmark setup/results and determine whether there is a usable controlled pair; the post's text alone does not attribute gains to any particular setting.
3. Find the code or reliable build-specific evidence for the names marked “Not located,” especially task graph, `tick.*`, `p.Chaos.*`, `spine.*`, the outline variable, and the alleged input keys.
4. Once registration is confirmed, run controlled one-variable comparisons per engine/build and record frame-time distributions, memory use, visual differences, and crash/stability outcomes. Do not use a single FPS average as the only success measure.
5. Expand this catalog with newly found Marvel-specific CVars and refresh evidence after game patches. Epic's reference will continue to be a useful index of upstream UE variables, but cannot define the entire game fork.

## References

- [Discord original post and discussion](https://discord.com/channels/1452445537298022637/1556428197820633269) (thread ID `1556428197820633269`; read on 2026-11-15).
- [Unreal Engine 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference).
- [Unreal Engine 5.9 Texture Streaming Configuration](https://dev.epicgames.com/documentation/unreal-engine/texture-streaming-configuration-in-unreal-engine).
- [NVIDIA Streamline DeepDVC programming guide](https://github.com/NVIDIA-RTX/Streamline/blob/main/docs/ProgrammingGuideDeepDVC.md), for DeepDVC intensity and saturation boost ranges/roles.
- [NVIDIA Streamline DLSS Frame Generation programming guide](https://github.com/NVIDIA-RTX/Streamline/blob/main/docs/ProgrammingGuideDLSS_G.md), for how frame generation uses generated-frame count, tagged buffers, and a proxy swap chain.
- [NVIDIA DLSS Unreal Engine plugin overview](https://developer.nvidia.com/blog/now-available-nvidia-dlss-3-for-unreal-engine-5/), which confirms the plugin exposes console controls under `r.ngx`.
- [Unreal Engine 5.8 Scalability Reference: Skeletal Mesh LOD Bias](https://dev.epicgames.com/documentation/unreal-engine/scalability-reference-for-unreal-engine).
- Local current game build metadata: `MarvelGame/version.json` (`1.1.4042190`, Shipping), and local user config `Saved/Config/Windows/GameUserSettings.ini`. Personal monitor identifiers and user-specific paths are intentionally not reproduced here.
