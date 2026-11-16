# Virtual Texturing CVar batch C

This guide covers the 13 remaining currently undocumented registered `r.VT.*` variables after the preceding batches. Community help describes intended controls, snapshots are captured values, and exact-name Epic UE 5.9 defaults are upstream references. These sources do not prove that the corresponding path is active in Marvel Rivals.

Build evidence is from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. Direct-memory candidates may be reads, writes, comparisons, or initialization; address-taking matches do not demonstrate runtime value use. No controlled startup override or in-game comparison was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `r.VT.Residency.LockedUpperBound` | float (`var`) | `0.65` | `0.65` | Virtual Texture pool locked page residency above which we kill any mip bias. That's because locked pages are never affected by the mip bias setting. So it is unlikely that we can get the pool within budget. Default 0.65 *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Residency.LowerBound` | float (`var`) | `0.95` | `0.95` | Virtual Texture pool residency below which we decrease mip bias. Default 0.95 *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Residency.MaxMipMapBias` | float (`var`) | `4` | `4` | Maximum mip bias to apply to prevent Virtual Texture pool residency over-subscription. Default 4 *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Residency.Notify` | int32 (`var`) | `0` | `0` | Show on screen notifications for virtual texture physical pool residency *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Residency.Show` | int32 (`var`) | `0` | `0` | Show on screen HUD for virtual texture physical pool residency *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Residency.UpperBound` | float (`var`) | `0.95` | `0.95` | Virtual Texture pool residency above which we increase mip bias. Default 0.95 *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.SplitPhysicalPoolSize` | int32 (`var`) | `0` | `0` | Create multiple physical pools per format to keep pools at this maximum size in tiles.A value of 64 tiles will force 16bit page tables. This can be a page table memory optimization for large physical pools.Defaults to 0 (off). *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.SyncProduceLockedTiles` | int32 (`var`) | `1` | `1` | Should we sync loading when producing locked tiles *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.TileBorderSize` | int32 (`var`) | `4` | `4` | Size in pixels to use for virtual texture tiles borders (rounded to next power-of-2) *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.TileSize` | int32 (`var`) | `128` | `128` | Size in pixels to use for virtual texture tiles (rounded to next power-of-2) *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.TranscodeRetireAge` | int32 (`ref`) | `60` | `60` | If a VT transcode request is not picked up after this number of frames, drop it and put request in cache as free. default 60 *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.UploadMemoryPageSize` | int32 (`var`) | `4` | `4` | Size in MB for a single page of virtual texture upload memory. *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |
| `r.VT.Verbose` | int32 (`var`) | `0` | `0` | Be pedantic about certain things that shouln't occur unless something is wrong. This may cause a lot of logspam 100's of lines per frame. *(community registry help)* | `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); direction/execution not traced. |

## Interpretation limits

- Empty help and missing UE matches remain unknown; names are not used as substitutes for definitions.
- Snapshot/default differences are provenance observations, not proof of an intentional change.
- Registry entries and static references do not establish player editability, startup `.ini` acceptance, or in-game effects.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
