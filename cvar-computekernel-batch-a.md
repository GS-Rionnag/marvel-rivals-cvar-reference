# ComputeKernel CVar batch A

This guide records the currently uncovered `ComputeKernel.ShowShaderCompilerWarnings` registry entry. Its supplied help says that setting it to `1` displays all warnings from ComputeKernel shader compilations. It does not state what other values do, where warnings are displayed, or whether this path is used by the game at runtime.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `ComputeKernel.ShowShaderCompilerWarnings` | `int32` (`ref`) | `0` | — | When set to `1`, displays all warnings from ComputeKernel shader compiles. Other values and the warning destination are not specified. | Name appears in both scanned Marvel Shipping executable inventories; 1 `ref_rva` hit (address-taken only) and 4 `obj_rva` hits (3 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- The supplied help describes compiler warnings; it does not say the setting changes shader compilation results or visual quality.
- The captured `0` is an observed snapshot value, not a guaranteed default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or acceptance of a startup `.ini` override. No in-game change has been verified.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
