# `p.Chaos.DisallowSetKinematicTargetOnDynamics`

## Registry entry

The community registry marks this as a `ref` of type `bool`, with no help text. Its captured value is `true`, not a verified game default. The registry's `ref_rva=0xF6C3EED` maps to `0x14F6C3EED` with the local executable's image base; the same address is directly referenced in the installed build's `.text` section.

Sources: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Neither attachment gives a build identity or capture procedure.

## Build-specific code evidence

Target: Marvel Rivals Shipping build `1.1.4042190`, executable SHA-256 `omitted from this documentation-only project`.

At `0x1429B99AA`, the code compares the CVar byte with zero. A nonzero value branches to `0x1429B99EA`, bypassing five 16-byte stores that otherwise write an 80-byte block into an array-backed structure at `[rcx + rdx*8 + 0x330]`. That path is reached only after another element-tag check; an element with tag value `2` skips the write regardless of this CVar. A related path at `0x142776261` also reads the same CVar before a block of writes, and the full address scan found nine direct memory-instruction candidates for its reference.

## Interpretation and limits

Observed: when the flag is nonzero, the inspected branch skips the 80-byte state write under the described condition; when it is zero, that write proceeds. This supports the literal “disallow setting ... on dynamics” reading, but the disassembly snippets do not recover the source-level identity of the structure, its fields, or the exact class/type condition. The description of the 80-byte block as a kinematic target is therefore a name-based inference, not a proven field mapping. Do not assume this suppresses every kinematic-target update or changes server-side physics.

No controlled runtime comparison has been recorded. The snapshot value `true` is not a recommendation or proof of the CVar's default.

## Evidence files

The direct-reference rows are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The CVar remains on the [unresolved definition worklist](cvar-unresolved-definitions.md) because its exact field semantics and game effect are not fully recovered.
