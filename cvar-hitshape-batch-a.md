# HitShape CVar batch A

This guide documents the 12 currently uncovered exact-case `HitShape.*` `var`/`ref` entries. Supplied object-table descriptions point to controls for remote-teammate updates, update suppression, ally-state caching, and collision while updates are disabled. Five entries have no useful supplied help. Captured values are observations; the attachment does not identify its game build.

None of these names has an exact-name Epic UE 5.9 reference match. Build-specific scans and strings are leads only: direct-memory candidates do not prove that an instruction reads the CVar's value, and adjacent strings do not prove behavior, runtime execution, or startup `.ini` acceptance.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `HitShape.AllowToSkipUpdate` | `bool` (`ref`) | `true` | — | No useful help in either supplied registry table; meaning unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `HitShape.DebugRename` | `bool` (`ref`) | `false` | — | No useful help in either supplied registry table; meaning unresolved. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `HitShape.EnableInGameMode` | `bool` (`ref`) | `true` | — | No useful help in either supplied registry table; meaning unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.EnableLazyUpdate` | `bool` (`ref`) | `true` | — | No useful help in either supplied registry table; meaning unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.ForceCloseRemoteTeammateUpdate` | `bool` (`ref`) | `false` | — | Supplied help: whether to force-close Hit Shape updates for remote teammates. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.ForceDisableAllUpdate` | `bool` (`ref`) | — | — | Object-table help: force-disable HitShape updates for all characters, except characters with `bKeepHitShapeUpdateWhenForceDisable=true`. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.ForceDisableAllUpdate.DisableCollision` | `bool` (`ref`) | — | — | Object-table help: while updates are force-disabled, disable ordinary HitShape collision. `0` restores collision without enabling updates. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.ForceDisableAllUpdate.KeepUpdateByTags` | `bool` (`ref`) | — | — | Object-table help: while `ForceDisableAllUpdate` is enabled, preserve updates for characters matching `KeepHitShapeUpdateWhenForceDisableTags`. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.RemoteTeammateAllyCache` | `bool` (`ref`) | — | — | Object-table help: cache `ClientIsAllyToViewerSide` for remote-teammate HitShape skipping. `1` caches the callback result; `0` uses the legacy per-frame query. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.RemoteTeammateAllyCacheRevalidateInterval` | `float` (`ref`) | — | — | Object-table help: low-frequency ally-cache revalidation interval in seconds; values at or below `0` disable revalidation. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.RemoteTeammateUpdateInterval` | `float` (`ref`) | `-1` | — | Supplied help: Hit Shape update interval for remote teammates. Units, valid range, and the meaning of `-1` are not described. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `HitShape.Show.Time` | `float` (`var`) | `1` | — | No useful help in either supplied registry table; meaning unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The descriptions identify intended control points in the supplied object table, not verified runtime effects in the installed build.
- In particular, `ForceDisableAllUpdate` and its child settings describe a policy with exceptions and a collision toggle. The help does not establish how any character, tag, game mode, or collision path is selected.
- `RemoteTeammateAllyCache` and its revalidation interval describe caching behavior, but cache lifetime and correctness were not verified. `RemoteTeammateUpdateInterval=-1` remains unexplained by the supplied help.
- The local build-context inventory records nearby strings for several names. String proximity is not proof of a CVar read, write, registration, or execution path.
- No entry was tested through the mod loader. Whether the `.ini` override mechanism can modify these variables remains unverified.

Sources: [community CVar registry](cvar-community-registry.md), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
