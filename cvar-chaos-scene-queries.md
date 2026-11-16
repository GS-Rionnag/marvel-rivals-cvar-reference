# Chaos scene-query BVH CVars

## Variables

| CVar | Type | Community help | `CVarDump.txt` snapshot |
|---|---|---|---|
| `p.Chaos.SQ.UseBVH` | bool | Empty. | `true` |
| `p.Chaos.SQ.BVHTraversalMode` | int32 | Original: `FImplicitBVH 子树遍历模式。0=AABB overlap(旧行为), 1=precise(ray slab + OBB SAT, 默认)。用于性能对比。` Assistant translation: “FImplicitBVH subtree traversal mode. 0 = AABB overlap (old behavior); 1 = precise (ray slab + OBB SAT, default). Intended for performance comparison.” The translation is not independently reviewed. | `1` |
| `p.Chaos.SQ.SweepSingleSortInitialOverlaps` | bool | “SweepSingle sort initial overlaps.” | `true` |

The capture build and method for `CVarDump.txt` are unknown, so `true` and `1` are snapshot values, not verified defaults or recommendations. The `BVHTraversalMode` translation is also preserved in the [translation source table](EVIDENCE.md#evidence-artifacts-not-included).

As upstream terminology only, Epic's UE 5.8 API describes [`FImplicitBVH`](https://dev.epicgames.com/documentation/unreal-engine/API/Runtime/Chaos/FImplicitBVH) as a bounding-volume hierarchy of implicit objects, and its [Chaos Visual Debugger guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/data-visualization-flags-in-chaos-visual-debugger) describes the scene-query acceleration structure as an AABB tree. These references help decode the terms but do not prove that Marvel Rivals uses the same engine revision or implementation.

## Static use in build 1.1.4042190

The local Shipping executable's community `ref_rva` addresses map to `0x14F6C46F0` for `UseBVH`, `0x14F6C46F4` for `BVHTraversalMode`, and `0x14F6C46EF` for `SweepSingleSortInitialOverlaps`. All three have registration-like sequences in the executable. The complete `.text` scan found 144 direct-instruction candidates apiece for the first two and 20 for the third. These hits repeat among generated query-code copies; they should not be read as the same number of independently understood call sites.

One representative path at `0x142B4C920` first zeros `edi`. At `0x142B4C9A8`, it compares `UseBVH` with zero and exits this path when the variable is false. When nonzero, it checks query/object conditions and reaches the `BVHTraversalMode` read at `0x142B4C9C8`. There, zero follows the branch beginning at `0x142B4CAA8`; a nonzero mode branches to `0x142B4CD6D`. In this representative code path, the binary distinguishes zero from nonzero but does not validate specific positive mode values.

This directly supports that `UseBVH` gates a scene-query path and that `BVHTraversalMode` selects between two implementations/branches within the enabled path. The translated help supplies the AABB-overlap versus ray-slab/OBB-SAT labels, but those exact algorithm labels are not independently identified from the local code in this note. No controlled performance comparison was performed, despite the help's stated comparison purpose.

`SweepSingleSortInitialOverlaps` is read at 20 direct-instruction candidates. One representative compare is at `0x142B85E6C`, where its stored byte is compared with `r14b`. This establishes use as a boolean in a query path, but the source of `r14b` and the later sort effect were not followed. The short community help supports the plain-language interpretation that it controls sorting initial overlaps for `SweepSingle`; the exact condition and ordering are not established here.

## Practical use and limits

- These are `ref` console-variable entries, so the supplied loader can express overrides as `name=value` under `[Overrides]`. Syntax does not prove that an override improves performance or is safe for every game mode.
- `UseBVH=true` and `BVHTraversalMode=1` reproduce the community snapshot, not a verified game default.
- The local binary verifies all three registration-like sequences and representative query branches for `UseBVH` and `BVHTraversalMode`. It does not establish every use site's semantics, the full range accepted by the integer setting, runtime mutability, or a performance effect.
- The community registry does not identify the game's exact Chaos/Unreal source revision. Do not use an engine-level interpretation as proof of behavior outside the inspected build.

See the [registration evidence guide](cvar-registration-evidence-4042190.md) for call-site evidence and the [unresolved definition worklist](cvar-unresolved-definitions.md) for other game-specific CVars that still need reverse engineering.
