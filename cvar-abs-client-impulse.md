# ABS client-impulse CVars

The community registry contains three undocumented `ABS` booleans associated by name with client impulse and impulse-field processing. The installed build reads all three directly, but the source dump has no help text and the call targets are not symbolized. This guide records the branch behavior we can verify without claiming a fully recovered gameplay meaning.

## Variables

| CVar | Type | Snapshot value | Evidence and current interpretation |
|---|---|---:|---|
| `ABS.EnableClientImpulseAndFieldSys` | bool | — | No snapshot entry or help text. It is tested at `0x146403434`; false branches past the following block. It is also tested near the start of several functions, including `0x14657D697`, `0x14657ED99`, and `0x14657F1EC`, where false skips most of the function body. The name suggests a master gate for the client impulse/field system, but the covered operations are not fully mapped. |
| `ABS.EnableClientImpulse` | bool | `true` | No help text. In one path, the flag is read at `0x146606FA5`; false skips a block that calculates and packages vector data, while true enters it. Reads at `0x1466072A1` and `0x146607443` add branches in the same broader routine. This supports a client-impulse calculation gate, but does not identify the exact impulse type or game-visible effect. |
| `ABS.EnableClientImpulseField` | bool | `true` | No help text. At `0x14657D707`, it changes a conditional path in an impulse-related routine; direct reads also occur at `0x14657EDFA` and `0x14657F2E5`. These checks confirm it is active in the build; the exact meaning of “field” and the effects of each value remain unresolved. |

## What the code establishes

All three names are `ref bool` entries in the community registry. For this build, the reference-address scan found 23 direct memory candidates for `EnableClientImpulseAndFieldSys`, 9 for `EnableClientImpulse`, and 15 for `EnableClientImpulseField`. These counts include repeated instruction sites, not unique functions or proof of runtime frequency.

At `0x149467C0F`–`0x149467C29`, code copies three adjacent globals into fields at offsets `0xB0`–`0xB2` of a state object. The globals are `EnableClientImpulseAndFieldSys`, `EnableClientImpulse`, and `EnableClientImpulseField`, respectively. Another path at `0x1494684A4`–`0x1494684BE` copies the same three globals to another object. This supports that the flags are grouped together in state, but the object type and later consumer are unidentified.

The snapshot records `true` for `EnableClientImpulse` and `EnableClientImpulseField`, and has no value for `EnableClientImpulseAndFieldSys`. These are captured values only; the attachment does not say they are defaults or identify its game build. No in-game test was performed.

## Limits

- The `ABS` prefix and “client impulse” labels are not defined in the attachment.
- The sampled control flow proves conditional reads and skipped/executed blocks, but helper calls have no usable symbols here. It does not establish whether an override changes movement, knockback, animation, prediction, or networking in a particular match.
- The three switches may interact. Do not assume that each can be tuned independently or that disabling them is a safe performance optimization.
- All 3 names remain in the [definition-gap worklist](cvar-unresolved-definitions.md) until their source behavior or controlled runtime effects are established.
