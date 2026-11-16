# Vulkan rendering CVar batch A

This page covers 25 exact `r.Vulkan.*` entries from the preserved community registry. All are typed `int32`; six are `var` rows and nineteen are `ref` rows. The supplied attachments do not state their game build or capture method. Captured values are snapshots, not defaults unless the community help itself labels a default.

## Registry help, snapshot, and local evidence

| Exact name | Kind | Snapshot | Community help, summarized | Local build evidence |
| --- | --- | ---: | --- | --- |
| `r.Vulkan.Allow16bitOps` | var | `0` | 16-bit operations intended to speed up TSR; help says `0` disables (default), `1` enables. | Name occurs in the Shipping image; only `obj_rva` setup/address references were found, with no direct `ref_rva` value read. |
| `r.Vulkan.Allow64bitShaderAtomics` | var | `1` | Enables 64-bit buffer/image atomics; help says Nanite requires them and marks `1` default. | Name occurs in the Shipping image; only `obj_rva` setup/address references, no direct `ref_rva` value read. |
| `r.Vulkan.AllowAsyncCompute` | var | `0` | Allows use of an async-compute queue when available; `0` disables. | Name occurs in the Shipping image; only `obj_rva` setup/address references, no direct `ref_rva` value read. |
| `r.Vulkan.AllowHostQueryReset` | var | `1` | Enables Vulkan Host Query Reset support; help marks `1` default. | Name occurs in the Shipping image; only `obj_rva` setup/address references, no direct `ref_rva` value read. |
| `r.Vulkan.AllowPresentOnComputeQueue` | var | `0` | Selects graphics-queue presentation (`0`) or allows presenting on the compute queue when available (`1`). | Name occurs in the Shipping image; only `obj_rva` setup/address references, no direct `ref_rva` value read. |
| `r.Vulkan.AllowSynchronization2` | var | `1` | Enables synchronization2/separate-depth-stencil-layout barrier support; help says it is needed for parallel command-buffer generation and marks `1` default. | Name occurs in the Shipping image; only `obj_rva` setup/address references, no direct `ref_rva` value read. |
| `r.Vulkan.AllowUniformUpload` | ref | `1` | Controls uniform-buffer uploads outside render passes: `0` reallocates buffers, `1` permits outside-pass uploads. | Direct comparison at VA `0x142528BCB`; this is a code-use candidate, not proof that the Vulkan path runs in a match. |
| `r.Vulkan.AllowVariableRateShading` | ref | `1` | Allows variable-rate shading when available; help marks `1` default. | Direct comparison at `0x1424F5FE8`. |
| `r.Vulkan.AutoCorrectExpectedLayouts` | ref | `0` | Uses layout tracking to correct mismatched expected layouts; help warns this is unsafe with multithreaded command-buffer generation and marks `1` default. | Direct comparison at `0x1424BB5FE`. |
| `r.Vulkan.AutoCorrectUnknownLayouts` | ref | `0` | Uses layout tracking to correct unknown layouts; same multithreaded-generation warning and help default `1`. | Direct comparisons at `0x1424B0A1E` and `0x1424B31FF`. |
| `r.Vulkan.Bindless.BufferOffsetUpdates` | ref | `0` | `0` sets all offsets for every draw/dispatch; `1` sets resource-descriptor offsets once and updates uniform-buffer offsets per draw/dispatch. | Direct comparisons at `0x1424B3A01` and `0x1424BA867`. |
| `r.Vulkan.Bindless.Enabled` | ref | `0` | Enables bindless use only when all support conditions are met. | Direct comparison at `0x1424B06AA`. |
| `r.Vulkan.Bindless.MaxResourceAccelerationStructureCount` | ref | `65536` | Maximum bindless acceleration-structure descriptor count. | Direct 32-bit load at `0x1424B5F7D`. |
| `r.Vulkan.Bindless.MaxResourceSampledImageCount` | ref | `262144` | Maximum bindless sampled-image descriptor count. | Direct 32-bit load at `0x1424B5EB1`. |
| `r.Vulkan.Bindless.MaxResourceStorageBufferCount` | ref | `65536` | Maximum bindless storage-buffer descriptor count. | Direct 32-bit loads at `0x1424B5F5B` and `0x1424B5F6C`. |
| `r.Vulkan.Bindless.MaxResourceStorageImageCount` | ref | `65536` | Maximum bindless storage-image descriptor count. | Direct 32-bit load at `0x1424B5EC5`. |
| `r.Vulkan.Bindless.MaxResourceStorageTexelBufferCount` | ref | `65536` | Maximum bindless storage-texel-buffer descriptor count. | Direct 32-bit loads at `0x1424B5F09` and `0x1424B5F1D`. |
| `r.Vulkan.Bindless.MaxResourceUniformBufferCount` | ref | `786432` | Maximum bindless uniform-buffer descriptor count. | Direct 32-bit loads at `0x1424B5F35` and `0x1424B5F46`. |
| `r.Vulkan.Bindless.MaxResourceUniformTexelBufferCount` | ref | `65536` | Maximum bindless uniform-texel-buffer descriptor count. | Direct 32-bit loads at `0x1424B5EDD` and `0x1424B5EF1`. |
| `r.Vulkan.Bindless.MaxSamplerDescriptorCount` | ref | `2048` | Maximum bindless sampler descriptor count. | Direct 32-bit load at `0x1424B5E9D`. |
| `r.Vulkan.Bindless.RebindBuffers` | ref | `1` | Rebinds buffers for every draw/dispatch; community help calls this useful for debugging but poor for performance. | Direct comparison at `0x1424BA831`. |
| `r.Vulkan.BudgetScale` | ref | `100` | Scales Vulkan memory budget from 0–100 percent, only when `VK_EXT_memory_budget` is available. | Sixteen direct sign-extending 32-bit loads from `ref_rva` in one code region, `0x1424EAE76` through `0x1424EB0CB`. |
| `r.Vulkan.CompressSPIRV` | ref | `0` | `0` keeps SPIR-V source uncompressed; `1` compresses on load to save RAM, with possible shader-creation hitching during decompression. Help marks `0` default. | Direct comparison at `0x1424FD2F8`. |
| `r.Vulkan.CPURenderthreadFramePacer` | ref | `1` | Controls the simple Vulkan render-thread CPU frame pacer. | Direct comparison at `0x142512E6A`. |
| `r.Vulkan.CPURHIThreadFramePacer` | ref | `1` | Controls the simple Vulkan RHI-thread CPU frame pacer. | Direct comparison at `0x14250AAB6`. |

The community registry contains an explicit help default for `Allow16bitOps`, `Allow64bitShaderAtomics`, `AllowHostQueryReset`, `AllowSynchronization2`, `AllowVariableRateShading`, `AutoCorrectExpectedLayouts`, `AutoCorrectUnknownLayouts`, and `CompressSPIRV`. Where the listed snapshot happens to match such help, that still does not establish the value applied by the current game. The other snapshot values have no default claim in this source.

None of these 25 names has an exact-name match in the generated Epic Unreal Engine 5.9 CVar-reference column. The descriptions above therefore come from the community attachment, not an Epic-reference match. Names and help in that attachment do not establish Marvel Rivals' Vulkan backend availability, the engine fork version, or runtime behavior.

## What the installed build scan establishes

The installed `Marvel Rivals Shipping executable` is build `1.1.4042190`. All 25 name strings are present in the installed executable inventory. The saved RIP-relative scan found `obj_rva` address/setup references for all 25. For the six `var` rows, the reference table has `ref_rva=0`, and the saved scan has no direct CVar-value reference; its object-address matches are registration/setup evidence only. For the nineteen `ref` rows, the scan found direct-memory candidates at the addresses listed above. The listed `cmp`, `mov`, and `movsxd` instructions read the corresponding CVar address in this binary. They support local code use, but not that a Vulkan renderer is selected, that a relevant initialization path executes, or that a mod-loader value reaches the read.

This scan is static and limited to direct RIP-relative references in the analyzed executable. The community attachment's build alignment is unknown; the names' appearance in both sources does not prove the attachment addresses map to the same live registration in the installed build. There was no controlled runtime override test.

## Editability and use limits

The user's `[Overrides]` syntax can express `r.Vulkan.Name=value` lines, but that is only loader-level syntax. No evidence here establishes that Marvel Rivals accepts a given value from that loader, that later initialization does not replace it, or that the platform/backend uses the setting. These are Vulkan-backend controls; if the running game uses a different RHI, their code paths may be inactive. Even a direct read in the Shipping image is not proof of an observable in-match change.

Before treating any as adjustable in practice, compare the game's live value with and without one loader override and confirm the active RHI. If the game cannot expose a runtime CVar dump, treat the override as unverified; the distinction and dump-command feasibility are in [CVar override evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals) and [live registry dump feasibility](cvar-overrides.md#can-a-normal-packaged-mod-list-the-live-cvar-registry).

## Evidence files

- Registry names, kinds, types, help, and RVAs: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Generated cross-source rows and exact Epic 5.9 match status: [community registry](cvar-community-registry.md).
- Local binary candidate names: [build 4042190 inventory](EVIDENCE.md#build-specific-static-analysis).
- Direct instruction matches: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); scanner limits and binary identity are in [CVar source notes](EVIDENCE.md#build-specific-static-analysis).
