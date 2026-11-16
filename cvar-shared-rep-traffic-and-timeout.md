# SharedRep traffic control and actor-channel frame timeout

This guide covers three undocumented `Net.SharedRep` variables in local build 1.1.4042190. The community registry has no help for these entries; all meanings below come from static code paths and name-based interpretation. Snapshot values are recorded observations, not defaults.

## `Net.SharedRep.TrafficControl.Enable`

- Registry: bool, `ref_rva=0x10020B58`; snapshot `false`.
- The build has seven direct reads of the reference.
- At `0x14520EBF8` and `0x1452157D9`, the value participates in a branch with an object byte at offset `0x944`. When that object byte is set, a nonzero CVar allows a special virtual-method path at object offset `0x3F8`; zero skips that path in the inspected cases.
- Other reads at `0x145202B54`, `0x145203693`, `0x145210130`, `0x145215E3B`, and `0x145215E5F` gate or propagate related processing. One path also checks a neighboring global byte at `0x150020B59`, whose name and role are not recovered.

This establishes an opt-in branch for some flagged objects inside shared-replication code. The method's source-level name, the object flag's meaning, and which actors or traffic are affected remain unknown. The word “traffic control” is only a name-based hint.

## `Net.SharedRep.TrafficControl.Distance`

- Registry: float, `ref_rva=0xF830728`; snapshot `0.5`.
- One direct read appears at `0x1451FB439` inside vector/range arithmetic.
- The value is compared with another derived float. Depending on that comparison, the code uses either the CVar value directly or multiplies an object float at offset `0x2BC` by the CVar. It then compares the resulting float with a vector-length value and records the result in a local flag.

The observed role is a distance-like threshold or scale used by the traffic-control path. The units, range, and precise interpretation of the object field are unknown; `0.5` is not established as a default or recommended value.

## `Net.SharedRep.ActorChannelFrameTimeout`

- Registry: int32, `ref_rva=0x10020B50`; snapshot `0`.
- Seven direct reads appear at `0x1451F48DD`, `0x14520E9F5`, `0x14520EFBB`, `0x14520FDC9`, `0x1452143A5`, `0x145216463`, and `0x14521C784`.
- The inspected sites use zero/nonzero gates. In several, a nonzero value enables a calculation that combines frame-like counters (`WORD` values at record offset `0x30` or `0x40`), an integer at object offset `0x88`, and another input. The result is clamped so the stored integer at record offset `0x34` is not reduced.
- At `0x1451F48D0`, this calculation occurs before a 32-byte record is written to an array. Similar calculations appear in several replication-related routines.

This supports that a nonzero setting enables extra updates to a frame-like field. Although the name suggests an actor-channel timeout, the field's exact type, units, timeout meaning, and whether positive integer values beyond `1` differ are not recovered. The inspected code treats the CVar as an enable gate rather than using its numeric value as a frame count.

## Override limits

The registry does not provide help or accepted ranges for these three CVars. The static evidence shows behavior branches in one shipping build, not a match-tested result, safe value, or performance benefit. Check the [CVar source notes](EVIDENCE.md#build-specific-static-analysis) for the executable hash and limits of the address scan; recheck the code after game updates.
