# D3D12 view-address and graphics-workaround CVars

This guide covers two `r.D3D12.*` integer references that have no help text in either community registry. The installed build contains direct checks for both. One gates a D3D12 descriptor-address diagnostic; the other gates an adapter compatibility path that explicitly tests NVIDIA's PCI vendor ID and logs when the device is eligible for workarounds.

## Variables

| CVar | Type | Snapshot | Observed build behavior | Limits |
|---|---|---:|---|---|
| `r.D3D12.AllowViewAddressCheck` | int32 | `0` | At `0x1424891AE` and `0x14248E00E`, the code compares the CVar value to a runtime integer and skips the following check when the CVar is less than or equal to that integer. The guarded path checks a descriptor-related value against a global bound; on the invalid branch, the binary's diagnostic text is `Bingo!!Invalid descriptor address[%d]`. | The compared register and descriptor index are not identified by this disassembly excerpt, so the exact threshold/count semantics remain unknown. The name is consistent with the observed address-validation path, but setting values were not tested. |
| `r.D3D12.EnableWorkaroundForGraphicsCapabilities` | int32 | `1` | The reference is compared against zero at `0x14249619D`. When positive, the adapter path checks for vendor ID `0x10DE` (NVIDIA), calls an eligibility helper at `0x1424A1160`, and, if that helper succeeds, writes `1` to a shared global flag (`0x14FF17B94`). A nearby diagnostic string says `Current device is eligible for workarounds.` | The helper's full eligibility rules and the consumers/effect of the shared flag are not established here. This is a compatibility/workaround control, not a documented image-quality setting. No runtime A/B test was performed. |

## Evidence

- The community rows identify both entries as `ref int32`, with blank help in `console_vars.tsv` and blank object help in `console_objects.tsv`.
- `CVarDump.txt` captures `r.D3D12.AllowViewAddressCheck = 0` and `r.D3D12.EnableWorkaroundForGraphicsCapabilities = 1`. These are captured values, not confirmed defaults or recommendations.
- Direct `ref_rva` reads are at `0x1424891AE` and `0x14248E00E` for the view-address setting, and `0x142495CBB` and `0x14249619D` for the graphics-workaround setting. The additional adapter, eligibility, flag-write, and log sequence is at `0x1424961A6`–`0x1424961E4`.
- The embedded diagnostic data includes the source path `D3D12RHI/Private/D3D12View.cpp`; this identifies a compiled source-path string, not the exact engine revision or accessible source code.
- Build: Marvel Rivals `1.1.4042190` Shipping, SHA-256 `omitted from this documentation-only project`. Raw direct-reference hits are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included).

Both settings remain in the [definition-gap worklist](cvar-unresolved-definitions.md) because the exact operational semantics and runtime consequences are incomplete. Do not infer that changing either value improves performance or image quality.
