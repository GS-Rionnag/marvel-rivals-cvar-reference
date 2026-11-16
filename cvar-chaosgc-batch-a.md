# ChaosGC CVar batch A: ISMC and Niagara controls

This guide covers 15 currently uncovered exact-case `ChaosGC.*` `var`/`ref` entries. The supplied descriptions cover per-frame loading limits, Niagara event limits, and several ISMC/mesh toggles. Some entries have only terse identifier-like help, so their precise effect remains unresolved. The community registry and snapshot do not identify their capture build.

None has an exact-name Epic UE 5.9 reference match. Snapshot values are observations, not defaults. Translation entries are unreviewed. Static address matches are instruction candidates and do not prove a CVar value read, write, runtime path, startup `.ini` acceptance, or visible effect.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `ChaosGC.FrameISMCMaxNum` | `int32` (`var`) | `50` | — | Community help (translated, unreviewed): per-frame limit for asynchronously loaded ISMCs; help lists default `50`. Object-table help is fragmentary: `ISMC ... (Default: 50)`. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.FrameISMCMaxTime` | `float` (`var`) | `2` | — | Community help (translated, unreviewed): per-frame ISMC loading time limit; help lists default `2.0`. Units and timing boundary are not specified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.Niagara.MaxPerFrameBreakEventNum` | `int32` (`ref`) | `150` | — | Community help: maximum break events sent to one component per frame. It states default `40` and about `1,600+` particles. The captured snapshot is `150`, so do not treat that observation as the documented default. | `ref_rva`: 3 direct-memory candidates and 2 address-taking references; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.NiagaraMeshPercent` | `int32` (`var`) | `100` | — | Supplied help is the identifier-like text `ChaosNiagaraMeshPercentLoadNum`; the exact percentage semantics and range are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableAsyncISMC` | `bool` (`var`) | `true` | — | Supplied help is `ChaosGCAsyncISMC`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableFrameISMC` | `bool` (`var`) | `true` | — | Supplied help is `ChaosGCISMC`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableFxMeshAsync` | `bool` (`var`) | `true` | — | Supplied help is `ChaosFxMeshAsync`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableFxMeshFraming` | `bool` (`var`) | `true` | — | Supplied help is `ChaosFxMeshFraming`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableISMCCache` | `bool` (`ref`) | `true` | — | Community help (translated, unreviewed): enable the ISMC caching mechanism. | `ref_rva`: 5 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableRenderSS` | `bool` (`var`) | `false` | — | Supplied help is `ChaosGCIRenderSS`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bEnableReplayGCFrame` | `bool` (`var`) | `true` | — | Supplied help is `EnableReplayGCFrame`; exact behavior is unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bMuteRenderSS` | `bool` (`var`) | `true` | — | Supplied help repeats the name (`bMuteRenderSS`) and does not explain what `RenderSS` means or what is muted. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bUseISMCCache` | `bool` (`var`) | `true` | — | Community help (translated, unreviewed): ISMC cache optimization switch. The registry does not establish whether it is separate from `bEnableISMCCache`. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bUseISMCRefresh` | `bool` (`var`) | `true` | — | Community help (translated, unreviewed): ISMC refresh optimization switch. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ChaosGC.bUseNewFrameISMC` | `bool` (`var`) | `false` | — | Community help (translated, unreviewed): use the newer per-frame ISMC loading method. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The two frame limits have help-described default values, but those strings do not prove the current Shipping build uses the same defaults. The `MaxPerFrameBreakEventNum` row specifically has a help/default and snapshot mismatch.
- `bEnableISMCCache` and `bUseISMCCache` are distinct registry names with different kinds and terse descriptions. Similar naming is not proof that one aliases the other.
- The names of the remaining boolean controls are useful search leads, not a reliable specification. Their exact values, interactions, and effect on gameplay or rendering are unverified.
- `obj_rva`/`ref_rva` scan counts are not proof of reads or writes. No controlled test changed these variables through the loader.
- Whether any of these entries can be changed through the loader's `.ini` override mechanism remains unverified.

Sources: [community registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [snapshot and build scan provenance](EVIDENCE.md#community-sources), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), and [build-specific text context](EVIDENCE.md#build-specific-static-analysis).
