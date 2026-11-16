# Chaos AABB debug logging controls

This guide covers two `p.debug.*` entries associated with AABB logging in the community object table. The local binary confirms their code paths are used as branches/counters, but it does not reveal the final debug output or a tested runtime effect.

## `p.debug.AABBLog`

- Registry: `ref bool`; companion object help says “Ignore AABB log.”
- Snapshot: `false`; this is not a confirmed default.
- The address scan finds 78 direct-memory instruction candidates against its reference. At representative sites such as `0x14297009F` and `0x142970177`, code compares the CVar byte with a local byte. Equal values branch around the following call/update block; unequal values enter it.

The object help and name associate this switch with AABB logging. The local byte's meaning and the contents/effect of the skipped block are not identified, so the branch alone does not establish the exact polarity or output behavior.

## `p.debug.AABBLogCount`

- Registry: `ref int32`; companion object help repeats the name “AABBLogCount.”
- Snapshot: `100000`; this is not a confirmed default or recommendation.
- At `0x142923E5F`, code reads the current integer count from object offset `0xD8`, increments that field, and compares the old count with this CVar. While the old count is less than the CVar, it returns through the short path at `0x14292473B`; at or above the threshold, it continues through a larger processing path.

This is direct evidence for a counter threshold. The field's owner, reset schedule, threshold direction relative to any emitted log, and what the larger path does remain unresolved. “Number of AABB logs” is suggested by the variable and object names, not confirmed by the inspected consumer.

## Limits

Both observations are static traces from build 1.1.4042190. The reference scan reports many repeated AABBLog reads but only one direct AABBLogCount read; counts of address matches do not imply separate features. No in-game test or safe override range is established. See the [source notes](EVIDENCE.md#build-specific-static-analysis) for the executable hash and address-scan limits.
