# Fast Array networking CVars

## Registry entry

The community `console_vars.tsv` attachment classifies `net.ShareFastArrayCompare` as a `ref` of type `bool`, with no help text. The captured `CVarDump.txt` value is `false`; this is a snapshot value, not a documented default. The registry gives `ref_rva=0xFE412C8`. Adding the local image base `0x140000000` yields `0x14FE412C8`, the address referenced in the installed build's `.text` disassembly.

Source rows: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The attachments do not identify the game build or capture method.

## What the installed build shows

Target: Marvel Rivals Shipping build `1.1.4042190`, executable SHA-256 `omitted from this documentation-only project`.

The scanner found 96 direct instruction candidates for this reference. Representative sites:

- At `0x1443D22A8`, the containing function zeroes `edi`; at `0x1443D2448`, the code compares the CVar byte to `dil` (therefore zero). When it is zero, control skips the following comparison between a field at `[object+0x70]` and a value at `[r13+0x54]`. When nonzero, equality can branch to `0x1443D2D5E`, bypassing later comparison/serialization work in this routine.
- At `0x1443D26E1`, zero branches to `0x1443D2B04`, skipping a hash-table lookup. A nonzero value reaches a hash calculation based on `r13`, probes a table, and compares a stored pointer with `r13`.
- At `0x144E92F40`, a second generated path compares the CVar directly with zero. Zero branches to `0x144E93360`; nonzero enters another pointer-derived hash lookup. This corroborates the alternate hash path without relying on an unverified register value.

These repeated gates are direct shipped-code evidence that the reference selects between a conventional comparison path and a shorter path using stored state and a hash lookup. Together with the name, the best current interpretation is that enabling the CVar allows cached/shared Fast Array comparison work. The precise cache ownership, validity rules, and performance impact have not been established from these snippets; treat that interpretation as an inference, not a verified definition.

## Practical reading

- `false` follows the fallback path at the inspected sites and avoids the shown hash lookup.
- `true` enables the alternate path; in the inspected examples it may short-circuit further work when stored state matches.
- The snapshot contains `false`, but it does not prove the game default or recommended value.
- The static trace does not establish whether changing this setting at runtime is safe, whether the CVar is read only during startup, or whether the optimization improves performance in this game.
- Configuring it through the loader proves only that the override is applied to configuration. It does not prove a particular runtime effect.

## Evidence and limitations

The control-flow locations above were read from GNU `objdump` disassembly of the local executable using the exact address mapping in the community registry. The full reference-candidate list is in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), and the ranked unresolved-name list is in [`cvar-unresolved-ref-triage-4042190.md`](EVIDENCE.md#build-specific-static-analysis).

No controlled runtime comparison has been recorded. The snippets do not establish runtime safety, actual performance impact, or server behavior.

## `net.FastArrayIgnoreLocalID`

### Registry entry

The community registry marks this as a `ref` of type `bool`, with no help text. Its captured value is `true`, which is not proof of the default. Its `ref_rva=0xF6AB658` maps to `0x14F6AB658` in the installed build, matching direct references in `.text`. Sources: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).

### What the installed build shows

The address scan found 32 direct memory-instruction candidates plus one address-taking reference. Repeated loops at `0x1443DF613`, `0x144E96678`, and `0x144FB2268` compare the flag to zero. At `0x1443DF613`, the code is iterating entries with a 32-byte stride. For a non-sentinel integer at entry offset `+4`, a nonzero flag enables an additional comparison against the integer at offset `+0`, but only when the auxiliary collection count at `[auxiliary+8]` is nonzero. If those fields differ, execution goes to the per-entry helper. If they match, the code checks an auxiliary pointer and can advance to the next entry without calling that helper when the pointer's first word is zero. With the flag zero, this extra equality check is skipped and the helper path is taken.

This is consistent with the name: the CVar changes whether an item-ID-like value is checked against a second local field, and a matching case can be ignored under an additional condition. The disassembly does not identify the fields' source-level names or fully explain the auxiliary state, so the exact meaning of “local ID” and all cases where work is skipped remain unresolved.

The snapshots show `net.FastArrayIgnoreLocalID=true` and `net.ShareFastArrayCompare=false`; neither value is established as a default or recommendation. No controlled runtime comparison has been recorded for either variable.
