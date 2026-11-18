# Additional evidence for unresolved rendering CVars

These observations supplement the existing guides for 15 names in the [CVar definition gaps](cvar-unresolved-definitions.md). Names, types, and help text come from the preserved registry attachment; the displayed snapshot values come from the separate community snapshot and are observations, not defaults. The compiled operations come from the build 1.1.4042190 static-reference table summarized in the [build-specific scan documentation](EVIDENCE.md#build-specific-static-analysis). To reproduce them with a copy of the scan table, filter it by exact name, `target_field=ref_rva`, and `access_class=direct-memory-candidate`. Read the mnemonic and operand direction to distinguish a load, comparison, and store. The table covers references to the backing storage. Runtime reachability, config editability, and rendered effects remain unverified.

## Streamline DLSS frame-generation VSync status

`r.Streamline.DLSSGIsVsyncSupportAvailable` is a boolean reference with a snapshot of `false`. The table records a conditional byte store (`sete`, which stores 1 when the selected condition holds and 0 otherwise) and a separate byte load (`movzx`). NVIDIA documents the similarly named `sl::DLSSGState::bIsVsyncSupportAvailable` as reporting whether the current DLSS-G build supports VSync. The matching terminology and compiled write/read pair support interpreting the CVar as a capability status. The predicate input, link to that SDK field, and downstream consumer in Marvel Rivals remain unconfirmed. [Rendering batch BL](cvar-rendering-r-batch-bl.md) · [NVIDIA Streamline DLSS-G programming guide](https://github.com/NVIDIA-RTX/Streamline/blob/main/docs/ProgrammingGuideDLSS_G.md#221-checking-vsync-support)

## ACEScg HDR curve parameters

The six adjacent scalar loads already recorded in [Rendering general batch A](cvar-rendering-general-batch-a.md) have a close parameter-level match to an implementation of Hajime Uchimura’s GT tone-mapping curve. All six snapshot values align with the implementation's example settings. This suggests the mappings below. The Marvel Rivals shader formula, the units of its values, and the role of its separate enable flag remain open. [Polyphony Digital’s GT Tone Mapping presentation, slides 129–135](https://s3.amazonaws.com/gran-turismo.com/pdi_publications/s2025_PBS_Physically_Based_Tone_Mapping_GT7.pdf#page=129) · [Uchimura filmic operator implementation](https://github.com/tizian/tonemapper/blob/master/src/operators/UchimuraFilmicOperator.cpp#L527-L537)

| CVar | Snapshot | Corresponding role in the reference implementation |
| --- | ---: | --- |
| `r.AcescgHdr.MaxBrightness` | 1 | `P`, peak output of the curve |
| `r.AcescgHdr.Contrast` | 1 | `a`, slope of the linear section |
| `r.AcescgHdr.m` | 0.22 | `m`, start of the linear section |
| `r.AcescgHdr.l` | 0.4 | `l`, parameter controlling the length of the linear section |
| `r.AcescgHdr.c` | 1.33 | `c`, exponent shaping the dark end of the curve |
| `r.AcescgHdr.b` | 0 | `b`, additive offset at the dark end of the curve |

## Post-process volume bloom and viewport copy references

- `r.StandardlizePPV.Enable` (snapshot `0`) has a comparison against zero. The same short code region includes scalar loads from `r.StandardlizePPV.Bloom.Intensity` (`0.7`) and `r.StandardlizePPV.Bloom.Threshold` (`0.2`). This places the test and both bloom settings in the same compiled region. The saved reference rows leave control flow, override precedence, and bloom units unresolved. [Rendering batch BI](cvar-rendering-r-batch-bi.md)
- `r.MultiViewport.Broadcast.MaxCopySizeX` and `r.MultiViewport.Broadcast.MaxCopySizeY` (snapshots `2560` and `1440`) have nearby 32-bit loads. Their placement supports investigating them as paired broadcast-copy size inputs. The unit, enforcement, and copy direction remain open. [Rendering batch AH](cvar-rendering-r-batch-ah.md)

## Shader code and distance-field references

- `r.ShaderCode.ShaderZlibBitWindowSize` (snapshot `12`) has two 32-bit backing-value loads. The registry help for neighboring `r.ShaderCode.ShaderCompressWithZlib` distinguishes Oodle and zlib. The zlib API uses `windowBits` as the base-2 logarithm of the compression window in bytes, so `12` would mean 4 KiB if passed directly to that parameter. The saved references leave the exact call sites and argument mapping unverified. [Rendering batch AY](cvar-rendering-r-batch-ay.md) · [zlib manual](https://zlib.net/manual.html)
- `r.ShaderCodeLibrary.MaxProcessShaderEntryDeletionPerFrame` (snapshot `10`) has two 32-bit loads and a comparison of a 32-bit register with its backing value. That comparison supports a limit interpretation. The register’s source, comparison direction, and deletion schedule are unresolved. [Rendering batch AY](cvar-rendering-r-batch-ay.md)
- `r.DistanceFields.GlobalSDFUpdateNum` (snapshot `50`) likewise participates in a comparison against a 32-bit register. This narrows the reference to an integer comparison in the compiled code. What is counted and when the comparison applies remain unknown. [Rendering batch J](cvar-rendering-r-batch-j.md)
