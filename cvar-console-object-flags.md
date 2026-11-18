# Community console-object flags

The community `console_objects.tsv` attachment provides a decimal integer in its `flags` column. The attachment identifies neither the capture method nor the game or engine revision. The values are consistent with Unreal's `EConsoleVariableFlags` in the examples below. Applying those names assumes the exporter preserved the Unreal flag word without transformation. [Community registry attachments](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) · [Evidence and scope](EVIDENCE.md)

## Low-bit counts

Take the distinct, case-sensitive names from `console_vars.tsv` whose kind is `var` or `ref`. Join them by exact name to `console_objects.tsv`. Each of the 8,973 names has exactly one object row with an integer flag value. Test each mask with `(flags & mask) != 0` so that composite values count too.

| Mask | Matching names | Meaning if the enum mapping holds |
|---|---:|---|
| `0x1` | 264 | `ECVF_Cheat`, which changes how the variable is handled in release builds |
| `0x4` | 510 | `ECVF_ReadOnly`, which restricts edits from the interactive console |

One name has both bits set. In total, 773 names have at least one and 8,200 have neither. These counts describe the captured rows. Whether a Marvel Rivals build accepts a startup config override or allows a particular runtime edit requires independent evidence. [Epic UE 5.5 enum](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/HAL/EConsoleVariableFlags?application_version=5.5)

## Composite values and engine versions

For `r.BloomQuality`, the table reports `16777568` (`0x01000160`). The low 16 bits are `0x0160`, the combination of `0x100`, `0x40`, and `0x20`. Epic's enum labels those bits `ECVF_Preview`, `ECVF_Scalability`, and `ECVF_RenderThreadSafe`. Neither counted bit is set. As a cross-check that the tally includes composite values, `r.AllowStaticLighting` has `50331684` (`0x03000024`), which sets both `0x20` and the `0x4` counted in the second row above. [Epic UE 5.5 enum](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/HAL/EConsoleVariableFlags?application_version=5.5)

Epic documents the high byte as the `SetBy` source or priority field, extracted with `flags & 0xff000000`. UE 5.5 assigns `0x01000000` to `ECVF_SetByScalability` and `0x03000000` to `ECVF_SetByProjectSetting`. The UE 5.8 enum assigns scalability `0x02000000` and uses `0x03000000` for `ECVF_SetByGameSetting`. To identify what set a Marvel Rivals value, the export schema and the capture build's enum would need to be verified. [Epic UE 5.5 enum](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/HAL/EConsoleVariableFlags?application_version=5.5) · [Epic UE 5.8 enum](https://dev.epicgames.com/documentation/unreal-engine/API/Runtime/Core/EConsoleVariableFlags)
