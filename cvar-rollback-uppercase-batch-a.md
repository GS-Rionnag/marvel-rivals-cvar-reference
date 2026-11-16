# Uppercase `Rollback.*` CVar batch A

This guide covers the 12 exact-case uppercase `Rollback.*` entries. They are distinct from the lower-case `rollback.*` debug variables documented separately. The supplied descriptions mention a rollback/lazy-evaluation master switch and interpolation settings; most other entries have names but no useful help. The community registry does not identify its capture build.

None of these variables has an exact-name Epic UE 5.9 CVar reference match. Snapshot values are observations, not defaults. Chinese help translations are unreviewed. Build-specific string adjacency and address scans are static leads only; they do not prove registration, reads/writes, execution, startup `.ini` acceptance, or in-game effects.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `Rollback.CalcRollbackOffsetByCreateTime` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Client.CreateSubsystem` | `int32` (`var`) | `0` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Debug.Vlog.DrawShapes` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. The name alone does not establish what geometry is drawn or when. | `ref_rva`: 5 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Enable` | `int32` (`var`) | `1` | — | Supplied help: master switch for the rollback and lazy-evaluation extension. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Hit.IgnoreDeath` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; the exact meaning and scope remain unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.IgnoreMaskAgentPenetrable` | `int32` (`ref`) | `0` | — | No useful supplied help or exact-name Epic description; the name does not establish which mask or agent types are affected. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.InnerEnable` | `int32` (`var`) | — | — | Community help (translated, unreviewed): “Do not set this variable directly; use `CVarRollbackEnableAll`.” This warning should be preserved; the registry does not define the other variable's accepted config path. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Interp` | `int32` (`var`) | `1` | — | Supplied English help: whether to use an interpolation frame in rollback. The accepted values and exact interpolation stage are not described. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `Rollback.InterpDistance` | `int32` (`ref`) | `500` | — | Community help (translated, unreviewed): do not interpolate when displacement over two frames exceeds this value. Units and how displacement is measured are unspecified. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.InterpTime` | `int32` (`ref`) | `5` | — | Community help (translated, unreviewed): interpolation interval in milliseconds. | `ref_rva`: 3 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Rollback.Summoner.Enable` | `int32` (`var`) | `1` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `Rollback.UseRollbackCollisionInfo` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. The name does not establish what collision data is selected or when. | `ref_rva`: 6 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The uppercase `Rollback.*` names are a separate namespace from lower-case `rollback.*`; similar spelling does not imply shared controls.
- The strongest documented actionable note is the community warning not to set `Rollback.InnerEnable` directly. Its suggested `CVarRollbackEnableAll` reference is in source help, but the target's own defaults and configuration semantics are not included here.
- `Rollback.InterpDistance` and `Rollback.InterpTime` describe interpolation thresholds/intervals but do not define a complete algorithm, range, or expected gameplay consequence.
- Nearby strings and address matches in the Shipping build are not control-flow traces. Direct-memory candidates can reflect reads, writes, or comparisons, and address-taking references may be registration-related.
- No controlled runtime or `.ini` override test was performed. Whether these entries are accepted by the loader remains unverified.

Sources: [community registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
