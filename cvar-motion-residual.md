# Animation, mesh effects, and movement CVars

The supplied registry help describes four previously uncovered settings for animation playback, skeletal mesh effects, and character movement. Snapshot values are observations. A dash means the snapshot omits the entry.

| Exact CVar | Kind / type | Snapshot | Meaning from supplied help | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | --- | ---: | ---: |
| `TeamVisualEffect.UseCueTeamVisualForOwnerMesh` | `ref` / `bool` | `true` | Resolves the team visual for skeletal mesh effects from the cue. `0` restores owner-based resolution. The help says changes apply to later queries. | 1 / 3 | 1 / 1 |
| `Weapon.Animation.SingleNodeUseFastPath` | `ref` / `bool` | — | The `SingleNode` branch of `WeaponAnimation_Play` uses the lightweight FastCache/Deferred path at `1` to avoid waiting for parallel animation tasks. `0` uses the original synchronous path. Translated help gives `1` as the default. | 9 / 2 | 1 / 1 |
| `charmove.SkipRMSClear` | `ref` / `bool` | `false` | Enables skipping an operation called “RMS Clear.” Help leaves the acronym and the affected conditions unspecified. | 1 / 3 | 1 / 1 |
| `skin.LoadExtraMontageFromDefaultSkin` | `ref` / `bool` | `false` | Toggles loading an extra animation montage from the default skin. `0` disables loading and `1` enables it. | 2 / 3 | 1 / 1 |

The static scan counts instructions referencing the registry’s `ref_rva` and `obj_rva` in Shipping build 1.1.4042190. Direct-memory matches may include reads, writes, or initialization. Availability, runtime effects, and startup override acceptance remain unverified.

See the [preserved registry, snapshot, and translated help](EVIDENCE.md#community-sources) and the [static address scan](EVIDENCE.md#build-specific-static-analysis).
