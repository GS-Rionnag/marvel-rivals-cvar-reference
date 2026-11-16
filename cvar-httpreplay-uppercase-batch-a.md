# Uppercase-R `httpReplay.*` CVar batch A

This guide covers the 11 exact-case `httpReplay.*` registry entries. They are distinct from the lower-case `httpreplay.*` names documented in the HTTP replay batches. The uppercase-R entries have no useful supplied help or exact-name Epic UE 5.9 reference match; snapshots are observations, not defaults.

The local build-context inventory places these names among HTTP replay/cache-related strings, but adjacent strings do not prove functional relationships. The address scan below matched only `obj_rva` fields: three direct-memory candidates and one address-taking reference for each entry. That pattern does not establish reads/writes, runtime effects, accepted values, or startup `.ini` acceptance. No behavior or loader test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `httpReplay.CacheUseGlobal` | `int32` (`var`) | `1` | — | No useful supplied help. The name suggests a global-cache switch, but accepted values and what “global” refers to are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.ChunkUploadDelayInSeconds` | `float` (`var`) | `40` | — | No useful supplied help. The name suggests a chunk-upload delay in seconds, but timing points and effect are not defined. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.CustomData.MaxSize` | `int32` (`var`) | `1048576` | — | No useful supplied help. The name suggests a custom-data size limit; units, encoding, and scope are unspecified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.CustomData.MaxTime` | `float` (`var`) | `30` | — | No useful supplied help. The name suggests a custom-data time limit, but the time unit and collection interval are unspecified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.EditorChunkUploadDelay` | `float` (`var`) | `5` | — | No useful supplied help. The name suggests an editor-specific chunk-upload delay, but the unit and when the setting applies are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.LowDelay.ChunkUploadDelayInSeconds` | `float` (`var`) | `2` | — | No useful supplied help. The name suggests a chunk-upload delay in a low-delay mode; the mode, timing rules, and effect are unverified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.MaxCacheSize` | `int32` (`var`) | `10485760` | — | No useful supplied help. The name suggests a cache-size limit; units and which cache it governs are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.MaxPCCacheSize` | `int32` (`var`) | `314572800` | — | No useful supplied help. The name suggests a PC cache-size limit, but “PC,” units, and its relationship to `MaxCacheSize` are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.MetaFilterOverride` | `FString` (`var`) | — | — | No useful supplied help. The name suggests a metadata-filter override; expected syntax and matching behavior are unknown. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.StopClearCache` | `int32` (`var`) | `1` | — | No useful supplied help. The name suggests a cache-clear policy on stop, but which stop event/cache and accepted values are unspecified. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `httpReplay.StreamCacheEachCount` | `int32` (`var`) | `5` | — | No useful supplied help. The name suggests a count associated with stream caching; its unit and behavior remain unknown. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- Names and numeric snapshots do not provide documented defaults or units. The size-like values `1048576`, `10485760`, and `314572800` should not be treated as byte limits without implementation evidence.
- Similar names such as `MaxCacheSize` and `MaxPCCacheSize` may be related, but the registry does not document precedence or whether one is a subset of the other.
- The separate lower-case `httpreplay.*` namespace has its own entries and help text. Those descriptions cannot be transferred to these uppercase-R variables based only on nearby strings.
- Static string presence and address candidates are not a function trace. Whether the game registers or honors these variables through the loader's `.ini` override mechanism remains unverified.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
