# Ambient-occlusion rendering CVars

This page documents the **13** `r.AmbientOcclusion.*` entries found in the preserved `console_vars.tsv` registry and assigned for review. It combines the community help and snapshot, exact-name Unreal Engine 5.9 reference matches, and the local Marvel Rivals Shipping build scan. The attachment does not identify its game build or capture method, and the local game's exact Unreal revision is unknown. A registry row or printable name does not alone prove that a startup override is accepted or affects a live renderer path.

## Entries

| Exact CVar | Type | Snapshot | What the available help says | Local build evidence |
| --- | --- | ---: | --- | --- |
| `r.AmbientOcclusion.AsyncComputeBudget` | int32 (`var`) | `1` | Chooses an async-compute budget from 0 (least) to 4 (most) for balancing compute work against graphics work. Help says it matters only when the SSAO compute-shader path is active and supported. The community text marks 1 as default but omits labels for 2 and 3. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Compute` | int32 (`var`) | `0` | Selects the SSAO pixel-shader path (`0`) or compute-shader variants (`1`–`3`) when supported. The community help calls the compute modes work-in-progress and describes fallbacks; its PS4-specific note is old upstream context, not a statement about current Marvel Rivals hardware paths. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Compute.Smooth` | int32 (`var`) | `1` | Community help says this smooths SSAO output when TAA is disabled. No additional range or exact filter is documented in the attachment. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.ConsoleAmbientOcclusionTypeOverride` | int32 (`var`) | `-1` | Community object-table help describes `-1` as no override, `0` as off, `1` as legacy SSAO/GTAO, and `2` as Lumen short-range AO. The entry has no useful `console_vars.tsv` help and no exact Epic 5.9 reference match. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser` | int32 (`var`) | `2` | Chooses the denoising algorithm: `0` disables it, `1` forces the renderer default, and `2` selects `GScreenSpaceDenoiser`, which help says a plugin may override. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.HistoryConvolution.KernelSpreadFactor` | float (`var`) | `7` | Multiplies sample offsets for the history convolution kernel; help states default 7. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.HistoryConvolution.SampleCount` | int32 (`var`) | `1` | Sets the number of samples for the history post-filter; community help states default 16. The captured snapshot `1` therefore differs from that stated default. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.KernelSpreadFactor` | float (`var`) | `4` | Sets the spread factor for pre-convolution passes. No supported range or default is stated in community help. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.PreConvolution` | int32 (`var`) | `2` | Sets the number of pre-convolution passes; community help states default 1. The captured snapshot `2` differs from the stated default. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.ReconstructionSamples` | int32 (`var`) | `16` | Maximum sample count for the reconstruction pass; community help states default 16. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Denoiser.TemporalAccumulation` | int32 (`var`) | `1` | Enables accumulating samples over multiple frames according to the help. No history length or other numeric behavior is specified. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.DepthBoundsTest` | int32 (`var`) | `1` | Uses a depth-bounds test to cull distant pixels during the AO pass. Help limits it to the pixel-shader path (`r.AmbientOcclusion.Compute=0`) without upsampling. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |
| `r.AmbientOcclusion.Method` | int32 (`var`) | `0` | Selects SSAO (`0`, help default) or GTAO (`1`). The name also occurs in the Shipping image. | Name occurs in the Shipping image. Address scan hits target `obj_rva` only; no `ref_rva` value read was identified. |

## Interpretation and editability limits

The snapshot values are captured values, not Marvel Rivals defaults or recommendations. In particular, the denoiser history sample count and pre-convolution snapshot differ from the defaults stated by their community help. The community attachment's help itself may be upstream-derived or version-specific; it is not proof that the current game build uses the same implementation.

For every row above, the local address-reference scan matched `obj_rva` entries, with `lea` address-taking and pointer/global-storage candidates. It did **not** identify a direct `ref_rva` value read for these CVars. Therefore the scan establishes local object-address references, not that the renderer reads an override or that the selected code runs in a match. The strings also occur in the selected Shipping image, which is name-presence evidence only.

Per the loader example supplied for this research, these are syntactically representable as `name=value` overrides under `[Overrides]`. Actual registration in the running renderer, loader acceptance/priority, and visual/performance effect remain unverified. Do not infer that choosing a more expensive denoiser sample count improves image quality or performance without a controlled in-game comparison.

## Names not found in the preserved registry

The four additional names included in the initial assignment were checked against `console_vars.tsv`, `console_objects.tsv`, `CVarDump.txt`, and existing CVar guides, but no exact match was found:

- `r.AmbientOcclusion.MipLevelFactor`
- `r.AmbientOcclusion.RadiusInWS`
- `r.AmbientOcclusion.RadiusInWSGlobalDF`
- `r.AmbientOcclusion.UseHistory`

They are omitted from the 13-entry registry coverage above. Their absence from these attachments and guides does not prove that no other Unreal version or game fork defines a similarly named variable.

## Sources

- [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322): community types, help, and reference RVAs.
- [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452): snapshot values; capture game build and collection procedure are unknown.
- [Community registry catalog](cvar-community-registry.md): consolidated snapshot, Epic 5.9 exact-match context, and source help.
- [Build 4042190 string inventory](EVIDENCE.md#build-specific-static-analysis): printable name presence in local executables/DLLs.
- [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included): x64 references matched to the community RVAs; `obj_rva` hits are not equivalent to value reads.
