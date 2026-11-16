# D3D12 CVar batch B: uppercase namespace

This guide documents the final three uncovered registered names whose exact first component is uppercase `D3D12`. Together with batch A, this completes all currently registered names in the case-sensitive `D3D12.*` family. They are separate from lower-case `d3d12.*` entries.

Static scan counts are instruction-reference candidates; they do not establish access direction, execution, startup override acceptance, or runtime effect.

| Exact CVar | Type(s) | Snapshot | Epic 5.9 default | Supplied help and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `D3D12.UpdateMemoryStatsForShipping` | int32 | 1 | — | Community help: Enable update d3d12 memory stats for shipping games. | `ref_rva`: 1 address-taking reference(s); `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access and effect not established. |
| `D3D12.UseUpdateTexture3DComputeShader` | int32 | 0 | `0` | Community help: If enabled, use a compute shader for UpdateTexture3D. Avoids alignment restrictions 0: off (default)<br> 1: on Object-table help: If enabled, use a compute shader for UpdateTexture3D. Avoids alignment restrictions 0: off (default)  1: on Epic 5.9 description: If enabled, use a compute shader for UpdateTexture3D. Avoids alignment restrictions 0: off (default)   1: on | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime access and effect not established. |
| `D3D12.ZeroBufferSizeInMB` | int32 | 4 | `4` | Community help: The D3D12 RHI needs a static allocation of zeroes to use when streaming textures asynchronously. It should be large enough to support the largest mipmap you need to stream. The default is 4MB. Epic 5.9 description: The D3D12 RHI needs a static allocation of zeroes to use when streaming textures asynchronously. It should be large enough to support the largest mipmap you need to stream. The default is 4MB. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidate(s), 1 address-taking reference(s); runtime access and effect not established. |

## Interpretation limits

- Snapshot values are observations, not defaults. Epic UE 5.9 entries are upstream matches and do not prove this game uses the same engine code path.
- Community registration intent and binary-string presence do not prove these names are writable from startup `.ini` files.
- Static instruction references are leads; read/write behavior and runtime execution remain unverified.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis), and [build-specific candidate inventory](EVIDENCE.md#build-specific-static-analysis).
