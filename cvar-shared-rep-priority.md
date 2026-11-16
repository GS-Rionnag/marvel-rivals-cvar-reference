# `Net.SharedRep.PriorityDelta`

## Registry entry

The community registry classifies this as a `ref` of type `float`; its help field is empty. The captured value is `0.2`, not a verified game default or recommendation. Its `ref_rva=0xF83071C` maps to `0x14F83071C` in the installed executable, matching the direct code references below.

Sources: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The attachments do not identify the captured game build or procedure.

## Build-specific code evidence

Target: Marvel Rivals Shipping build `1.1.4042190`, executable SHA-256 `omitted from this documentation-only project`.

The scanner found nine direct memory-instruction candidates for `ref_rva=0xF83071C`, all in floating-point code. At `0x1451F9B11`, the value is loaded as a scalar float and participates in a per-entry calculation; the CVar name suggests the stored value is priority-related, but the field's source-level identity is unknown:

- A matching 32-bit field causes one `PriorityDelta` subtraction.
- A nonzero byte field contributes another subtraction scaled by `PriorityDelta`.
- Under a separate nonpositive-field branch, a computed ratio adjustment is multiplied by `PriorityDelta` and added.
- The resulting scalar is stored into the current entry at `[rcx]`.

Other sites update a score-like float in `[rdi]`. For example, `0x1451FB1B6` multiplies the CVar by a constant weight and subtracts it; `0x1451FB395` multiplies a normalized term by the CVar and adds it; `0x1451FB4D1` subtracts the CVar directly. Further multiply/subtract uses appear at `0x1451FB1FB`, `0x1451FB288`, `0x1451FB3BA`, `0x1451FB4AD`, and `0x14521B0C4`.

## Interpretation and limits

Observed: the CVar scales or directly supplies several floating-point adjustments in code associated by its name with `Net.SharedRep`. For positive values, increasing it scales up the magnitude of the affected terms; zero removes the CVar-dependent part of those expressions. Some uses subtract a term and another adds one, so the net effect on any actor's priority depends on surrounding conditions and signs. The snippets do not establish whether negative values are accepted or clamped.

This supports describing the variable as a multiplier/step size for several shared-replication priority adjustments. The code snippets do not reveal the exact meaning of every source field, the full scoring model, or whether changing the value improves network performance or gameplay. The snapshot value `0.2` is not a recommended setting.

No controlled runtime comparison has been recorded. The guide remains linked from the [definition-gap worklist](cvar-unresolved-definitions.md) because the precise scoring semantics and observed game effect are still incomplete.

## Evidence files

The complete row-level address matches are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); the triage count is in [`cvar-unresolved-ref-triage-4042190.md`](EVIDENCE.md#build-specific-static-analysis).
