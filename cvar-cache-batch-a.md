# Cache CVar batch A

This guide documents all currently uncovered registered names with the exact case-sensitive first dotted component `Cache` (17 entries). Help text, snapshot values, Epic UE 5.9 matches, and build-address scan counts are kept separate. The supplied registry does not confirm game-build alignment or startup `.ini` acceptance.

The static scanner’s `direct-memory-candidate` and `address-taken` classes are leads only. They do not establish read/write direction, execution, or gameplay effect. Translations are unreviewed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `Cache.ChannelClose` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Client.Debug` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Delete` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Draw.Position` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Log.Use` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.MetricLog` | int32 (`var: 1`) | — | — | Community help: Emit structured cache lifecycle metrics: Create, Reuse, Recycle. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Net.Remove` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Net.Rep` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Open` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.OpenForReplay` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.PoolHanle.DebugClass` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Prediction.Open` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Relevant.Avatar` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Reset.Delegate` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Reset.Property` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.Summoned.Open` | int32 (`var: 1`) | 1 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |
| `Cache.VisualLog` | int32 (`var: 1`) | 0 | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access/effect unverified. |

## Interpretation limits

- Snapshot values are captured observations, not defaults or recommendations.
- Epic UE 5.9 matches are upstream context and do not establish the game’s engine version or runtime path.
- Registry entries and static reference candidates do not prove startup-config acceptance or in-game effect.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis), and [build-specific candidate inventory](EVIDENCE.md#build-specific-static-analysis).
