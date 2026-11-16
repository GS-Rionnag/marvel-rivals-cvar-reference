# Rendering CVar batch C: bloom, base pass, and defaults

This batch covers twelve registered rendering variables that sit outside the larger Vulkan, shadow, ray-tracing, and Lumen guides. The registry help and `CVarDump.txt` values come from the preserved community attachment; its game build and capture method are unknown. Do not treat the captured values as defaults. The installed build is Marvel Rivals 1.1.4042190 Shipping.

## Evidence limits

The community `var`/`ref` registry reports a `var` row for all twelve entries and object RVAs for them. The local address scan finds the CVar object addresses and some registration/setup-like accesses, but for eleven entries the registry has `ref_rva=0`; those object-address hits are not evidence that active rendering code reads the CVar's value. `r.AnisotropicMaterials` has a nonzero `ref_rva` and direct comparison candidates in the binary, so it has stronger local read evidence. The instructions associated with object RVAs often write the object pointer during setup and must not be mistaken for feature reads. No runtime override test was performed. Under the user's loader syntax, these names can be placed in `[Overrides]`; acceptance and visible effect remain unverified.

## Entries

| Exact name | What the available evidence supports | Captured value | Local evidence / caveat |
| --- | --- | --- | --- |
| `r.AnisotropicMaterials` | Registry help says whether anisotropic BRDF is used for anisotropic materials. This concerns the material BRDF model, not the texture anisotropic-filtering setting. | `1` | Nonzero `ref_rva`; the scan found direct integer comparisons at several call sites. This supports value reads, but the exact shader/material branches and visual effect in a match were not traced. |
| `r.AntiAliasingMethod` | Selects the project default AA method in the registry help: 0 off, 1 FXAA, 2 TAA, 3 SMAA, 4 MSAA, 5 TSR. Post-process volumes, cameras, or game settings may override it. | `5` | Local registry entry exists, but its `ref_rva` is zero. Do not assume setting this alone overrides Marvel Rivals' own supersampling/DLSS configuration. |
| `r.BasePassOutputsAdditionalBloom` | Registry help says 0 draws additional bloom in a separate pass and 1 draws it in existing opaque base and translucent passes. This describes pass placement, not turning bloom on or off. | `0` | `ref_rva` is zero; no feature-value read established by this scan. |
| `r.BasePassOutputsMeshSection` | Type is `int32`; the preserved help field is blank. The name alone suggests a base-pass output switch, but does not establish which mesh-section data it emits or what values mean. | `0` | `ref_rva` is zero. Meaning remains unresolved. |
| `r.BasePassOutputsVelocity` | Registry marks it deprecated and points to `r.VelocityOutputPass`. | `-1` | `ref_rva` is zero. Prefer investigating the named replacement; the snapshot value does not prove this deprecated control remains effective. |
| `r.BasePassWriteDepthEvenWithFullPrepass` | Registry help says 0 allows a read-only base pass (avoiding an MSAA depth resolve and allowing EarlyZ for masked materials); 1 forces depth writes in the base pass, useful for diagnosing prepass/base-pass mismatches. | `0` | `ref_rva` is zero. The help describes a debugging/renderer-path control; performance or image effects are untested. |
| `r.Bloom.ApplyLocalExposure` | Registry help says whether local exposure is applied when calculating bloom; its help default is true. | `true` | `ref_rva` is zero. Whether local exposure is active in the game's chosen bloom pipeline is unverified. |
| `r.Bloom.AsyncCompute` | Registry help says whether FFT bloom runs on asynchronous compute. | `1` | `ref_rva` is zero. Hardware scheduling, overlap, and performance impact are not established by the value. |
| `r.Bloom.CacheKernel` | Registry help says whether the FFT bloom kernel is cached in the spectral domain. | `1` | `ref_rva` is zero. Cache lifetime and memory/performance effects are not established. |
| `r.Bloom.ScreenPercentage` | Registry help calls this the axis resolution percentage for FFT bloom convolution. Its captured value is 25, while the registry's Epic 5.9 comparison says 50; neither should be treated as the game's verified default. | `25` | `ref_rva` is zero. Resolution scaling may trade quality and cost, but the exact rounding, minimum, and current game's FFT path are unverified. |
| `r.Bloom.WarnKernelResolution` | Registry help describes 0 as disabled, 1 as warning on consoles, and 2 as warning on all platforms when kernel resolution is unnecessarily high. | `1` | `ref_rva` is zero. This is diagnostic; it does not itself change bloom quality. |
| `r.DepthOfField.NearBlurSizeThreshold` | Registry help says the minimum near-blur size before the effect is forcibly disabled, currently affecting Gaussian DOF; help default is 0.01. | `0.01` | `ref_rva` is zero. This does not establish that Gaussian DOF is used in the relevant game view. |

## Sources and reproducibility

- Exact names, types, help, and snapshot values: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Epic-reference comparisons: [`cvar-community-registry.md`](cvar-community-registry.md). These explain upstream Unreal behavior, not Marvel Rivals' fork-specific runtime.
- Local address hits: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), generated by the documented [CVar address-reference scanner](EVIDENCE.md#method-and-reproducibility). Interpret object-RVA setup hits separately from ref-RVA value reads.
- Loader syntax and its limits: [CVar override research](cvar-overrides.md#how-to-read-these-in-the-users-loader).
