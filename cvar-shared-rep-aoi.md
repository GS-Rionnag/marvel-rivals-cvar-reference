# `Net.SharedRep.AOI.*` variables

This guide covers the nine entries under `Net.SharedRep.AOI.*` in the community registry. The community source describes several settings, while the local build supplies direct-use evidence for six reference variables. Source descriptions and static code reads do not by themselves prove the feature works in a particular match.

## Registry entries and snapshots

| Name | Kind / type | Captured value | Community help or current evidence |
|---|---|---:|---|
| `Net.SharedRep.AOI.DefaultRep` | ref / bool | false | No help text. One direct read at `0x1451FB9C0`; it gates a branch that checks a returned object pointer. Exact meaning is unresolved. |
| `Net.SharedRep.AOI.DisconnectOnly` | ref / bool | — | No help text. At `0x14521913E`, a nonzero value preserves a secondary flag, but only after an earlier AOI-derived condition is true. |
| `Net.SharedRep.AOI.DisconnectOnlyDisguiseExtraCount` | var / int32 | — | “Extra visible actors before static AOI trimming”; source says it is used only when `DisconnectOnlyDisguiseFix` is effective. |
| `Net.SharedRep.AOI.DisconnectOnlyDisguiseFix` | var / int32 | — | Source help: `1` allows “Highest” channels with bounded static AOI overflow; `0` uses legacy static AOI. |
| `Net.SharedRep.AOI.Enable` | ref / bool | false | No help text. Five direct reads gate or alter code paths in the local build; details below. |
| `Net.SharedRep.AOI.FrameInterval` | ref / int32 | 20 | No help text. Used in two paths that compute an integer next-frame value. |
| `Net.SharedRep.AOI.NextNewVisableFrame` | ref / int32 | 10 | No help text. Added to a frame value and stored as a next-frame field. The source spelling `Visable` is preserved. |
| `Net.SharedRep.AOI.PendingVisableActors` | var / int32 | — | Source help: `1` lets selected actors create channels (marked default by source); `0` restores a legacy count-only channel gate. |
| `Net.SharedRep.AOI.VisableInterval` | ref / float | 3 | No help text. Added to a stored time value in a visibility-update path. The source spelling `Visable` is preserved. |

“Captured value” comes from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452), not a default. Help text comes from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). The `var`/`ref` classifications and address fields are community evidence; the attachments do not identify their capture build.

## Local build behavior

Target: Marvel Rivals Shipping build `1.1.4042190`, executable SHA-256 `omitted from this documentation-only project`.

- `Net.SharedRep.AOI.Enable` has five direct memory-instruction candidates, plus one address-taking reference. At `0x145203680`, zero selects the fallback condition; when `AOI.Enable` is nonzero, execution proceeds into bit-mask handling. If it is zero, the code proceeds only when `AOI.DisconnectOnly` is nonzero. At `0x145219108`, a nonzero `AOI.Enable` enters a branch that checks bits in `[r12+0x684]` and writes a derived flag to `[temporary+0x528]`. At `0x14521913E`, `AOI.DisconnectOnly` gates a second flag after that derived flag is set. These observations support treating `AOI.Enable` as an AOI-path switch and `DisconnectOnly` as an additional gate in some paths; they do not recover the meaning of every bit or flag.
- `Net.SharedRep.AOI.FrameInterval` is loaded at `0x1452031AA` and `0x14520321F`. In both snippets, the value is incremented and added to another computed integer before the result is stored at an object field offset `+0x6C0`.
- `Net.SharedRep.AOI.NextNewVisableFrame` is added to `[r13+0x940]` at `0x145202D6F`; the sum is stored at `[rsi+0x48]`.
- `Net.SharedRep.AOI.VisableInterval` is loaded as a float at `0x145212E24`, converted to double, and added to the existing time at `[rdi+0x598]`; the result is stored at `[rbx+0x40]`.
- `Net.SharedRep.AOI.DefaultRep` is read at `0x1451FB9C0`. In that path, the CVar comparison occurs when a byte field is zero; when the CVar is also zero, code invokes a virtual method and compares its returned pointer with another object pointer. This does not identify the operation's source-level “default replication” meaning.

The community help for the related `Net.CharMove.Sync.AllowAOIWithUIDKey` says it has no effect when `Net.SharedRep.AOI.Enable=0`, and says it does not prevent sending coordinates outside view or location leakage. That help is in Chinese; its paired English rendering is unreviewed. It is useful context, not runtime validation of these AOI controls.

## Evidence limits

The full reference scan has direct rows in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The source-level meaning of “AOI,” the exact frame scheduling model, the effect of each `var` setting, and client/server behavior have not been verified in a controlled runtime comparison. See the [community registry](cvar-community-registry.md) for original help text and snapshots, and the [definition-gap worklist](cvar-unresolved-definitions.md) for unresolved entries.
