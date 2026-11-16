# Chaos acceleration-structure CVars

This guide covers the eight `p.Chaos.AccelerationStructure*` entries in the preserved community registry. Their names are exact: there is no dot between `AccelerationStructure` and the suffix.

## Registry values and help

| CVar | Type | Community help (plain-language reading) | `CVarDump.txt` snapshot |
|---|---|---|---:|
| `p.Chaos.AccelerationStructureCacheOverlappingLeaves` | int32 | Set to `1` to cache overlapping leaves for faster overlap queries; any other value disables the feature. | `0` |
| `p.Chaos.AccelerationStructureIsolateQueryOnlyObjects` | int32 | Set to `1` so QueryOnly objects are not moved to acceleration structures on the Physics Thread. | `0` |
| `p.Chaos.AccelerationStructureSplitDestruction` | int32 | Set to `1` to move destructions into separate acceleration structures; any other value disables the feature. | `1` |
| `p.Chaos.AccelerationStructureSplitStaticDynamic` | int32 | Set to `1` to sort dynamic and static bodies into separate acceleration structures; any other value disables the feature. | `1` |
| `p.Chaos.AccelerationStructureTimeSlicingMaxBytesCopy` | int32 | Maximum bytes to copy to the external acceleration structure during Copy Time Slicing. | `100000` |
| `p.Chaos.AccelerationStructureTimeSlicingMaxQueueSizeBeforeForce` | int32 | If the update queue reaches this limit, time slicing is disabled and the acceleration structure is built at once. | `1000` |
| `p.Chaos.AccelerationStructureUseDirtyTreeInsteadOfGrid` | int32 | Use a dynamic tree structure for dirty elements instead of a 2D grid. | `1` |
| `p.Chaos.AccelerationStructureUseDynamicTree` | int32 | Use a dynamic BVH tree structure for dynamic objects. | `1` |

The help column is the registry's supplied wording, lightly normalized for spelling and capitalization. `console_objects.tsv` repeats the same descriptions. The dump values are a capture of unknown provenance; they are not verified defaults or recommendations.

## Local static evidence, build 1.1.4042190

The local Shipping executable's `.text` scan found direct-memory instruction candidates for all eight registry `ref_rva` addresses. Counts below are scanner candidates, not necessarily unique logical uses. Candidate instructions are listed in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); registry names and help are in [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). The address scanner warns that matches may be reads, writes, or initialization code, so the examples below are interpreted conservatively.

| CVar | Direct candidates | What the inspected instructions establish |
|---|---:|---|
| `p.Chaos.AccelerationStructureCacheOverlappingLeaves` | 3 | At `0x14298D02F`, the stored integer is compared with zero and the following branch skips a call when zero. This is consistent with the help's enable/disable gate in this path. The exact called operation and what data is cached are not identified. |
| `p.Chaos.AccelerationStructureIsolateQueryOnlyObjects` | 4 | At `0x14298E61E`, the variable is compared with a local state value; the nearby branches select between two calls. At `0x142B9F4A3` and `0x142B9F4FF`, it is compared with `1`. These uses are consistent with conditional handling of QueryOnly objects, but do not independently identify the Physics Thread or prove the full behavior stated in help. |
| `p.Chaos.AccelerationStructureSplitDestruction` | 7 | At `0x14298E689`, the variable is compared with a local state value; equality gates the next path. Several other sites compare it with `1`. This supports a conditional destruction-related path, but the allocation and contents of the purported separate structure were not traced. |
| `p.Chaos.AccelerationStructureSplitStaticDynamic` | 11 | The direct candidates include comparisons with `1` (for example `0x1427550DB`, `0x142999BF2`) and a comparison with a local state value at `0x14298E615`. This is consistent with a switch used in body handling; the sorting/grouping result is not independently established from the excerpts inspected. |
| `p.Chaos.AccelerationStructureTimeSlicingMaxBytesCopy` | 1 | At `0x1429B9F00`, the integer is loaded into a local stack slot near the start of a function. The subsequent copy loop and byte accounting were not followed, so the role is supported by help only. |
| `p.Chaos.AccelerationStructureTimeSlicingMaxQueueSizeBeforeForce` | 1 | At `0x14298D0B3`, the integer is loaded and compared against a field at `[rdi+0x3e0]`; `setg` records whether that field is greater than the CVar. This directly supports a threshold comparison. The exact queue field and the downstream forced-build action are not identified at this site. |
| `p.Chaos.AccelerationStructureUseDirtyTreeInsteadOfGrid` | 1 | At `0x14298E4B7`, the variable is compared with `1` and the equality result is stored as a boolean (`sete`). This proves a binary selection input in the local path, but the tree/grid alternatives are known only from help. |
| `p.Chaos.AccelerationStructureUseDynamicTree` | 12 | Several sites compare the integer with zero, including `0x14298D038` and `0x14298E781`, indicating boolean-style gates. At `0x14298D038`, a zero value skips a following virtual call. This is consistent with an optional dynamic-tree path; the exact data structure effects are not fully traced. |

The disassembly evidence is from the installed `Marvel Rivals Shipping executable`, build 1.1.4042190, SHA-256 `omitted from this documentation-only project`, analyzed with GNU objdump 2.47.20260726 and image base `0x140000000`. Registry `ref_rva` addresses were matched to RIP-relative instruction targets. This supports local static use in the scanned binary, not that every community attachment was captured from this same build.

## Override and interpretation limits

These are registered as `ref` entries with `int32` type in the community table, so the mod loader's `[Overrides]` syntax can express them as `name=value`. This confirms syntax compatibility only. No runtime experiments were performed to verify that each override is accepted, changes the live code path, persists across modes, improves performance, or is safe.

The community descriptions are the strongest plain-language evidence for intended meanings. Static reads support that several settings gate or parameterize code paths, but do not prove the exact internal acceleration-structure design. In particular, the data does not establish that the settings affect rendering, remove effects, or provide a general performance improvement. The game engine revision and the dump capture procedure are also unknown.

For the broader source provenance and scan methodology, see [CVar research attachments](EVIDENCE.md#build-specific-static-analysis), [community registry](cvar-community-registry.md), and [CVar registration evidence in build 4042190](cvar-registration-evidence-4042190.md).
