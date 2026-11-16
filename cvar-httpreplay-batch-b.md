# HTTP replay CVar batch B

This guide covers 25 currently undocumented registered `httpreplay.*` variables. Community help is source-provided intent; snapshot values and Epic UE 5.9 defaults are separate evidence. They do not establish the game build’s active path.

Static address references are from Marvel Rivals Shipping build `1.1.4042190`; direct-memory candidates are not full read/write or execution traces. No controlled startup config or live gameplay test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `httpreplay.ObDelayTime` | int32 (`var`) | `40` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.ObDownloadAllData` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.Pause.AlwaysRefresh` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.Pause.Enable` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.Pause.RefreshInterval` | float (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.PendingTimeout` | float (`var`) | `6` | `—` | http request max pending time *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.QuickDownloadChunkTime` | float (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.RefreshStateInterval` | float (`var`) | `5` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.RoomObUseFixedDelay` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.ServerMaxRetries` | int32 (`var`) | `3` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.ServerRetryDelay` | float (`var`) | `0.5` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.Storage.Debug` | int32 (`var`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.Storage.Opt` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.TimeoutTime` | float (`var`) | `5` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.URLEmptyCount` | int32 (`ref`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `ref_rva`: 0 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.UpdateTotalTimeInterval` | int32 (`var`) | `15000` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.UseCache` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.AsyncSave` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.AutoClearData` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.EditorSave` | int32 (`var`) | `0` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.Enable` | int32 (`var`) | `1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.FailedCount` | int32 (`ref`) | `0` | `—` | Fake Save failed. *(community registry help)* | `ref_rva`: 0 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.LocationCode` | int32 (`var`) | `410` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.MaxRetryCount` | int32 (`var`) | `15` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |
| `httpreplay.V3.TickAsyncRetryTime` | float (`var`) | `0.1` | `—` | No explanatory help supplied; behavior unresolved. | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime path not traced. |

## Interpretation limits

- Untranslated or empty registry help remains unresolved rather than guessed from the name.
- Exact-name upstream defaults are references, not verified game defaults.
- Registry entries and scan matches do not prove `.ini` acceptance, player editability, or an in-game effect.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
