# D3D12 CVar batch B

This guide covers 5 currently undocumented registered `d3d12.*` variables after the preceding batches. Community help records intended behavior; snapshots and exact-name Epic UE 5.9 references are separate evidence.

Static candidates come from Marvel Rivals Shipping build `1.1.4042190`. Direct-memory candidate and address-taking counts do not prove a completed value trace or executed path. No controlled config override or live behavior test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help / translation | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `d3d12.UploadHeap.SmallBlock.PoolSize` | int32 (`ref`) | `4194304` | `4194304` | Pool size for the upload memory small block allocator *(community registry help)* | `ref_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); execution path not traced. |
| `d3d12.VRAMBufferPoolDefrag` | int32 (`ref`) | `1` | `1` | Defrag the VRAM buffer pool *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); execution path not traced. |
| `d3d12.VRAMBufferPoolDefrag.MaxCopySizePerFrame` | int32 (`ref`) | `33554432` | `33554432` | Max amount of data to copy during defragmentation in a single frame (default 32MB) *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); execution path not traced. |
| `d3d12.VRAMTexturePoolDefrag` | int32 (`ref`) | `1` | `1` | Defrag the VRAM Texture pool (enabled by default) *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); execution path not traced. |
| `d3d12.VRAMTexturePoolDefrag.MaxCopySizePerFrame` | int32 (`ref`) | `33554432` | `33554432` | Max amount of data to copy during defragmentation in a single frame (default 32MB) *(community registry help)* | `ref_rva`: 1 direct-memory candidate(s), 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); execution path not traced. |

## Interpretation limits

- Empty help and upstream matches remain unknown; snapshots are not defaults.
- Registry membership and address references do not establish player editability or `.ini` acceptance.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), and [build-specific CVar inventory](EVIDENCE.md#build-specific-static-analysis).
