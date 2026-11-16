# Bone reduction CVars

This guide records the client bone-reduction controls described in the preserved community registry, plus nearby toggles whose names suggest related behavior but whose effects are not documented by the available evidence.

## Described controls

| CVar | Type | Community help | `CVarDump.txt` snapshot |
|---|---|---|---:|
| `a.ClientReduceBoneLevel` | int32 | `0` disables client bone reduction. Positive values enable it when `ViewDistanceQuality <= Level`. The help text states a default of `2`. | `0` |
| `a.ClientReduceBone.Strength` | int32 | `0` = Default, `1` = Strong, `2` = Extreme. | `0` |
| `a.ClientReduceBoneLOD` | int32 | `-1` closes the feature; `0` enables reduction at all LODs; the help text for `1` literally ends `1 to skip LOD 0...`, so it does not spell out the full range. | `0` |

The descriptions and captured values come from the [preserved community attachments](EVIDENCE.md#build-specific-static-analysis), not a versioned game manual. The `Level` help explicitly describes its own default as `2`, while the snapshot records `0`; those are different kinds of evidence. The snapshot is not a record of defaults or a recommendation to use its values.

Taken literally, the captured `Level=0` means the documented client reduction gate is disabled, even though `LOD=0` means all LODs are eligible according to that setting's help. This is a configuration-level interpretation of the two descriptions, not a verified runtime interaction. The source set does not explain precedence between them, which `ViewDistanceQuality` values map to each level, or what the `Strong` and `Extreme` modes change in the skeleton.

## Static use in build 1.1.4042190

The local executable provides direct reads that make the three help entries more credible for this build. These are disassembly observations, not a live visual or performance test:

- `a.ClientReduceBoneLOD` is read at `0x143A79BF6` inside a path gated by bit `0x8` of the byte at object offset `0xF80`. The code skips its special branch for a negative value, then compares the setting with the integer argument copied from `r9d` into `r13d`. It enters the helper path only when the setting is less than or equal to that argument. This matches a minimum-LOD threshold: `0` can include every nonnegative LOD, and `1` excludes LOD 0. The argument's source-level identity is not recovered here.
- `a.ClientReduceBone.Strength` is read at `0x146844315`. The helper starts with `2`, replaces that value when the CVar is lower, then floors negative results to `0`; its returned result is therefore clamped to `0..2`. This confirms the numeric range used by the community help, but not what quality differences the modes produce.
- `a.ClientReduceBoneLevel` is read at `0x146DCEB1F`. A value `<= 0` prevents a condition flag from being set. For positive values, code compares an adjacent integer global with the CVar and sets the flag when that global is less than or equal to it, subject to two other boolean checks. This fits the help's quality-level threshold description; this note does not independently identify the global or recover the surrounding setting's source-level name.

The three CVars also have registration-like sequences documented in the [build registration table](cvar-registration-evidence-4042190.md). Their direct runtime reads are separate evidence from those registration sequences.

## Related entries with no usable description

| CVar | Type | Captured value | What is established |
|---|---|---:|---|
| `a.EnableAlwaysReduceBone` | bool | `false` | No useful help text. Direct runtime reads are present in build 1.1.4042190 (details below), but their full source-level effect is not recovered. |
| `a.EnableAutoReduceBoneOnServer` | bool | `false` | The name and type are present in the registry; there is no useful help text in either community table. |

`a.EnableAlwaysReduceBone` has two direct runtime reads in the installed build:

- At `0x143A99428`, a nonzero value (inside a path gated by bit `0x8` at object offset `0xF81`) allows a call through virtual slot `[rax+0x688]` on the current object.
- At `0x144212266`, a nonzero value clears bit `0x1` at object offset `0xF8B`.

Those observations establish that the variable participates in runtime decisions, but the object's source type, the virtual method's purpose, and the semantic meaning of the flag are not recovered. The name still does not establish what “always” means or how this toggle relates to the three client controls above.

`a.EnableAutoReduceBoneOnServer` has no direct memory-instruction candidate matching its community `ref_rva` in the complete `.text` scan. That absence is not proof of no use: indirect access, other sections, or a mismatch in the community address convention can evade this scan. Its name alone does not establish whether it controls server-side skeletal work or replicated outcomes. Both entries remain in the [definition-gap worklist](cvar-unresolved-definitions.md); their registry addresses and registration-like sequences are only leads. See the [registration evidence notes](cvar-registration-evidence-4042190.md) and the [scan limitations](EVIDENCE.md#build-specific-static-analysis).

## Practical use and limits

- These are console-variable entries (`ref` in the community table), so they fit the loader's `[Overrides]` syntax. For example, `a.ClientReduceBoneLevel=0` is syntactically a CVar override; it reproduces the snapshot value and should not be read as a recommendation.
- The source files do not identify their capture build, capture method, or whether the dump records values changed by a particular mod. Do not use its values as proof that an override works in the installed build.
- No controlled in-game comparison has established visual changes, CPU/GPU impact, network effects, or tested override values for these controls.

## Evidence sources

- `console_vars.tsv`: type, community help, and address fields.
- `console_objects.tsv`: duplicate help entries; it adds no missing explanation for the two related toggles.
- `CVarDump.txt`: captured values only.
- Local executable: build 1.1.4042190. Disassembly gives direct control-flow evidence for `a.EnableAlwaysReduceBone`, but not a complete semantic definition. The server toggle remains unresolved. The descriptions for the other three controls remain attributed to community help and are cross-checked against their local code paths.

