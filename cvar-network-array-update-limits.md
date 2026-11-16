# Network replicated-array update limits

This guide covers two `net.*` integer variables whose community help is blank. Epic's UE 5.9 reference lists `2048` for both but supplies no description. Their names and local code paths point to limits on array change/deletion counts carried through an update. The source-level serializer and full runtime policy are not recovered.

## `net.MaxNumberOfAllowedTArrayChangesPerUpdate`

- Registry: `ref int32`, blank community help, `ref_rva=0xF6AB65C`.
- Epic UE 5.9 reference value: `2048`, with no description. The community snapshot also records `2048`; neither value alone proves the Marvel build's default.
- At `0x1443ED22F`, code loads the CVar and compares it with a sign-extended 16-bit count previously read into a local field. A count at or below the limit continues; a count above it takes the error path.

## `net.MaxNumberOfAllowedTArrayDeletionsPerUpdate`

- Registry: `ref int32`, blank community help, `ref_rva=0xF6AB660`.
- Epic UE 5.9 reference value: `2048`, with no description. The community snapshot also records `2048`; neither value alone proves the Marvel build's default.
- At `0x1443ED159`, code loads this CVar and compares it with a 32-bit count held at `[rsp+0x78]`. A count at or below the limit continues; a count above it takes the error path.

## Shared behavior in the inspected path

Both comparisons occur while a routine reads array-related values from a property stream. If either count exceeds its configured limit, control reaches the common path at `0x1443ED25A`, which calls `0x140FE2FA0` and returns `false`. This is evidence that the limits can reject an over-limit update in this path. A related routine at `0x1443F1C54`/`0x1443F1C5B` loads both settings for threshold checks and diagnostics.

The addresses above are representative sites, not a count of independent serializers. The `.text` scan reports 64 direct references per CVar; repeated compiled property layouts account for many hits, and those copies do not establish 64 distinct behaviors.

## Limits

The variable names are consistent with caps on array changes and deletions per update, and the inspected stream/count comparisons support that reading. The precise update type, whether these values are applied on client, server, or both, the logging/error policy outside the traced path, and safe override ranges remain unknown. These are not documented as performance-tuning recommendations. The [Community CVar registry](cvar-community-registry.md) preserves the registry and snapshot rows; Epic's [UE 5.9 Console Variables Reference](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-console-variables-reference) is the upstream comparison, but supplies no description for these two entries. The [source notes](EVIDENCE.md#build-specific-static-analysis) identify the binary and static-scan limits.
