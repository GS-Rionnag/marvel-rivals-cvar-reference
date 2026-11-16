# Chaos collision margins and triangle-mesh tolerances

This guide adds seven `p.Chaos.Collision.*` settings that control or feed collision margin, culling-distance, and triangle-mesh tolerance paths in the installed Marvel Rivals Shipping build `1.1.4042190`. The binary evidence is static. Values below are from a community snapshot and are not verified defaults or recommended overrides.

## Variables

| CVar | Registry type | Snapshot | Evidence-backed behavior |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.MarginFraction` | float | `-1` | Help says it overrides the collision margin fraction from Physics Settings when the value is `>= 0`. The build checks for a negative value; a nonnegative value is copied into a local fraction used by the setup path. `-1` therefore takes the leave-the-Physics-Settings-value path in this code. |
| `p.Chaos.Collision.MarginMax` | float | `-1` | Help says it overrides the maximum collision margin from Physics Settings when the value is `>= 0`. The build checks for a negative value; nonnegative values are copied to a local maximum-margin slot. `-1` skips that override in this path. |
| `p.Chaos.Collision.ConvexZeroMargin` | float | `0` | The build loads this value in a convex margin setup routine. A zero-valued branch takes a `maxss` path using the configured value and another local; a nonzero path compares local values and reaches min/max operations. This indicates participation in margin calculation, but the locals and resulting geometric meaning are not identified. Despite the name, the trace does not prove that setting it to zero globally removes all convex margins. |
| `p.Chaos.Collision.CullDistanceReferenceSize` | float | `0.01` | Loaded as a scalar in a routine that reads shape/bounds dimensions, finds maximum component differences, scales those dimensions, and combines the results with a max operation. The code shows this value contributes to a size-based cull-distance calculation; the relevant structure fields and final units are not identified. |
| `p.Chaos.Collision.MinCullDistanceScale` | float | `1` | Loaded in the same bounds/cull-distance routine as `CullDistanceReferenceSize`. The trace confirms both values feed the calculation, but does not recover the precise clamp formula or demonstrate which objects use the result. |
| `p.Chaos.Collision.TriangeMeshPhiToleranceScale` | float | `1` | The spelling `TriangeMesh` is present in the registry. In four triangle-mesh collision routines, this value is converted to double precision, multiplied by a shape-related float, and stored in local solver data passed to a helper. This supports a scale on a phi-like tolerance; the meaning of phi and its downstream comparison are unresolved. |
| `p.Chaos.Collision.TriangeMeshDistanceTolerance` | float | `0.1` | In the same four routines, this value is converted to double precision and stored in the local solver data passed to a helper. The name indicates a triangle-mesh distance tolerance, but the exact distance test and units are not recovered. |

## Build evidence

The community registry supplies the names, types, reference RVAs, and the two Physics Settings override descriptions. The snapshot values are included for identification only. Direct reads in the local executable are:

- `MarginFraction` at `0x143FEB4A9`: a negative value skips the assignment; a nonnegative value is copied into the local fraction slot.
- `MarginMax` at `0x143FEB4E8`: a negative value skips the assignment; a nonnegative value is copied into the local maximum-margin slot.
- `ConvexZeroMargin` at `0x142829239`: loaded into the convex-margin setup path, which branches and performs min/max scalar operations. The exact output field is unresolved.
- `CullDistanceReferenceSize` at `0x142828D22` and `MinCullDistanceScale` at `0x142828D2A`: both are loaded as floats and converted to double precision. The surrounding routine calculates maximum differences across three shape/bounds dimensions and multiplies size-derived values before combining them. This supports a size-scaled cull distance, but the full formula and object-level application remain unresolved.
- `TriangeMeshPhiToleranceScale` is read at `0x142751CF2`, `0x1427525BE`, `0x142752DFE`, and `0x14275337C`.
- `TriangeMeshDistanceTolerance` is read at `0x142751DD5`, `0x1427526A1`, `0x142752EF6`, and `0x142753446`.

In the first inspected triangle-mesh route, the phi scale is multiplied by a shape-related float and stored in solver-local data; the distance tolerance is stored in a neighboring local field. A helper later receives that data. The four repeated sites are consistent with multiple or inlined collision paths, but do not prove every triangle-mesh contact uses them.

## Evidence and limits

- Types, help, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Snapshot values are not treated as defaults.
- The address candidates are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). Instruction addresses above were checked against the local `1.1.4042190` Shipping executable.
- `MarginFraction` and `MarginMax` have clear help text and direct negative/nonnegative branches. The remaining interpretations combine variable names with the observed data flow; exact margin, culling, and tolerance mathematics still need deeper tracing.
- No in-game comparison or runtime test of these settings is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md), [Chaos collision feature and pruning CVars](cvar-chaos-shape-pairs-pruning.md), and [CVar overrides and loader syntax](cvar-overrides.md).
