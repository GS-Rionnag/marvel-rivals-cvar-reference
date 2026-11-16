# SkinWeightProfileManager CVar batch A

This guide documents the currently uncovered `SkinWeightProfileManager.AllowCPU` registry entry. Supplied help describes whether CPU buffer generation is allowed. The help does not identify which buffers or skin-weight operations use this path, whether enabling it also enables another path, or any performance tradeoff.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `SkinWeightProfileManager.AllowCPU` | `int32` (`ref`) | `1` | — | Whether or not to allow CPU buffer generation. The source does not specify accepted values beyond the apparent boolean form, nor what happens when disabled. | The name is absent from the scanned Marvel Shipping executable string inventories. The supplied address-reference export associates it with 2 `ref_rva` hits (1 direct-memory candidate, 1 address-taken) and 4 `obj_rva` hits (3 direct-memory candidates, 1 address-taken); those matches are unvalidated and do not independently prove the name is registered in the binary. |

## Interpretation and limits

- The snapshot value `1` is an observation, not a guaranteed default or recommendation.
- `AllowCPU` suggests a CPU-versus-other buffer-generation choice, but the registry help alone does not establish a GPU alternative, which operations are affected, or a measurable cost.
- Address matches without a corresponding string-inventory entry are limited static evidence. They do not prove runtime reads, writes, execution, registration, or startup `.ini` acceptance.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
