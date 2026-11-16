# Chaos aggregate and array-collection CVars

This guide covers the five exact `p.Chaos.Aggregate.*` and `p.Chaos.ArrayCollection.*` names present in the preserved community registry. The two namespaces control different areas: aggregate broadphase behavior and particle-array slack handling. Static evidence comes from the supplied registry/snapshot and the local Marvel Rivals Shipping executable, build `1.1.4042190` (changelist `4042190`). It does not establish that a particular override improves performance or is safe in every game situation.

## Evidence and limits

- Registry help and types are taken from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); alternate raw object help is kept separate from it in [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values are from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). They are observations from that dump, not verified defaults or recommendations. See [source notes](EVIDENCE.md#build-specific-static-analysis) for attachment provenance and address-column limitations.
- The local-code observations below use direct memory-reference candidates in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), interpreted against the build's x64 Shipping disassembly. Direct-reference hits establish reads/accesses, but the instruction alone does not establish a full feature's gameplay meaning.
- No in-game A/B test was performed for this guide. Community registry build alignment is unconfirmed.

## `p.Chaos.Aggregate.*`: CPU Chaos aggregate broadphase

These names are grouped in the registry under the CPU Chaos aggregate/broadphase feature. Only `Pruning` has clear explanatory help text. The raw object help for `Enabled` combines several fragments, and the `Validation` object help is abbreviated, so those fragments should not be treated as full definitions.

| CVar | Type | Registry help | Snapshot | Local Shipping evidence |
| --- | --- | --- | --- | --- |
| `p.Chaos.Aggregate.Enabled` | bool | No help text. Raw object help: `CPU Chaos aggregate broadphase p.ChaosAccelerationComputeUseNewMethod=0 IsEnabled() false` (fragments, not a clean definition). | No row | A helper at VA `0x1429CB5A0` returns false if this byte is zero; if nonzero, it also checks `p.ChaosAccelerationComputeUseNewMethod` and returns true only when that second setting is nonzero. This verifies a two-condition enable gate in this helper. It does not explain all aggregate behavior or prove the helper is used in every relevant path. |
| `p.Chaos.Aggregate.Pruning` | int32 | “Enable sorted-array bidirectional box pruning for CPU Chaos aggregate refinement. 0=legacy double loop.” | No row | Eight direct memory reads are recorded at `0x14296983B`, `0x142969DBB`, `0x14296A330`, `0x14296A852`, `0x14296AD86`, `0x14296B2E6`, `0x14296B83B`, and `0x14296BD2D`. At the first site, zero is converted into a true flag and passed to a helper, consistent with the help text's zero/legacy selection. The full pruning algorithm and meanings of nonzero integer values are not established here. |
| `p.Chaos.Aggregate.Validation` | bool | Chinese: `校验 CPU Chaos aggregate broadphase 的成员关系与插入结果。` Unreviewed translation: “Validate CPU Chaos aggregate broadphase membership and insertion results.” | No row | One direct read candidate at `0x1429CB7C0` is an accessor that zero-extends the byte and returns it. This proves the value is exposed by that helper; the validation work it may gate was not traced. The object table only has the shorter fragment `CPU Chaos aggregate broadphase`. |

The word “enabled” must be interpreted narrowly from the code observation: the inspected helper requires both its own CVar and `p.ChaosAccelerationComputeUseNewMethod` to be nonzero. The community object's `false` fragment may describe a displayed result or another field; it is not sufficient to infer a default.

## `p.Chaos.ArrayCollection.*`: particle-array slack sizing

The registry help describes capacity/slack management for particle arrays. In the local binary, both values are loaded together in a routine and passed to a shared helper for multiple array fields. The code supports that these values participate in repeated array-compaction calls, but the helper's exact allocation policy and comparison formula were not fully recovered.

| CVar | Type | Registry help | Snapshot | Local Shipping evidence |
| --- | --- | --- | --- | --- |
| `p.Chaos.ArrayCollection.MaxSlackFraction` | float | “Shrink particle arrays if the number of slack elements exceeds the number of elements by this fraction” | `0.5` | Read at `0x142ADE46B` and passed as a float argument to helper `0x142AEDF60` along with `MinSlack`, across several array fields. The source help suggests a relative-slack threshold; exact denominator, comparison, and resulting capacity are unverified. |
| `p.Chaos.ArrayCollection.MinSlack` | int32 | “Do not reduce the size of particle arrays if it would leave less slack than this” | `100` | Read at `0x142ADE47A` and passed as an integer argument to the same helper. The helper contains a check against this supplied value before iterating the array entries. This is consistent with a minimum-slack constraint, but exact resize rules remain unknown. |

The call sequence starts around VA `0x142ADE468`; it loads the fraction and minimum slack, then repeats calls to `0x142AEDF60` for several collection members. The helper's machine code loops over entries and forwards these arguments to a per-array virtual method. This supports a shared array-maintenance path, not a claim about how much memory a given override saves or whether any particular values are optimal.

## Safe interpretation for overrides

Treat registry help as the best available description for `Pruning` and the two `ArrayCollection` settings, while keeping the local code claims above limited to the inspected paths. For `Enabled` and `Validation`, use only the narrower helper/accessor findings. The two values in the snapshot (`0.5` and `100`) are captured values, not proven defaults. No tuning recommendation is supported by the available static evidence.

Related references: [CVar registration evidence in build 4042190](cvar-registration-evidence-4042190.md), [community CVar registry](cvar-community-registry.md), and [preserved CVar research attachments](EVIDENCE.md#build-specific-static-analysis).
