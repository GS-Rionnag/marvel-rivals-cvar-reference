# Chaos collision solver CVars

This guide traces ten `p.Chaos.Collision.*` settings into the installed Marvel Rivals Shipping build `1.1.4042190`. It records static code behavior only; the community snapshot values are captured values, not verified defaults or recommendations.

## Variables

| CVar | Registry type | Snapshot | Evidence-backed behavior |
| --- | --- | ---: | --- |
| `p.Chaos.Collision.UseGJK2` | bool | `false` | A byte comparison directly selects between two distinct collision-computation call paths. With the byte zero, the code calls `0x142703250`; with it nonzero, it calls `0x1426FEE40`. The names of those internal routines and what differs in their results are not recovered. |
| `p.Chaos.Collision.GJKEpsilon` | float | `1e-06` | The routine reads this float, converts it to double precision, and stores it in its local solver data before dispatch. This supports that it supplies a numeric value to the GJK-related computation. The exact convergence test or comparison using it is not established by this trace. |
| `p.Chaos.Collision.EPAEpsilon` | float | `1e-06` | The routine likewise reads and converts this float to double precision and stores it in local solver data before dispatch. Its use as an EPA-related tolerance is consistent with the name, but the exact comparison and effect on the result remain unverified. |
| `p.Chaos.Collision.UseCapsuleTriMesh2` | bool | `true` | In one compiled route, nonzero selects a call to `0x1427E09F0`; zero takes an alternate path beginning with setup at `0x14272CB31`. The call targets are not identified, so this is evidence of a selector between two capsule/triangle-mesh processing paths, not proof of which implementation is newer or better. |
| `p.Chaos.Collision.UseConvexTriMesh2` | bool | `true` | In one compiled route, nonzero calls `0x142803DE0`, while zero calls `0x1426E6950`. This selects between two convex/triangle-mesh processing routines; their algorithmic differences are not recovered. |
| `p.Chaos.Collision.Manifold.PlaneContactNormalEpsilon` | float | `0.001` | The registry describes this as the normal tolerance distinguishing face contacts from edge-edge contacts. In the build, code reads the float, converts it to double precision, and sets a byte when the epsilon is greater than or equal to an absolute-valued scalar. The analyzed slice does not recover the scalar's full derivation or label the downstream branches. |
| `p.Chaos.Collision.EnableManifoldGJKReplace` | bool | `false` | In a contact-processing path, a non-matching flag causes a helper call; if that helper returns true, processing jumps to a later path. A second path checks this setting alongside `EnableManifoldGJKInject`. The setting name suggests a manifold-GJK replacement mode, but exact contact-data changes are not recovered. |
| `p.Chaos.Collision.EnableManifoldGJKInject` | bool | `false` | In an indexed contact loop, when the selected index is the `-1` sentinel and `EnableManifoldGJKReplace` is zero, this setting is checked. If both are zero, control jumps to `0x14283001F`; if either is nonzero, the current loop index is copied into the selected-index register and processing continues. The names suggest manifold contact injection/replacement; the contact structure semantics remain unverified. |
| `p.Chaos.Collision.Manifold.ForceOneShotManifoldEdgeEdgeCaseZeroCullDistance` | bool | `false` | Community help says that for Convex/Convex one-shot manifolds, an edge-edge hit forces cull distance to zero so any separation discards the contact. The build compares the setting with a local byte and, on the differing-value path, performs an additional floating-point comparison that can branch to a later rejection path. This is consistent with the help but does not independently identify the locals or contact classification. |
| `p.Chaos.Collision.OneSidedHeightField` | bool | `true` | A compiled collision path checks this byte. Zero skips a following weighted-sum and scalar comparison; nonzero runs that additional calculation before continuing or exiting. The name suggests one-sided heightfield handling, but the exact scalar's geometric meaning and the selected path's effect are not recovered. |

## Build evidence

The preserved community registry classifies the first three variables as `ref` entries with no help; `PlaneContactNormalEpsilon` has the help noted above. Their reference RVAs map, for the local PE image base `0x140000000`, to `0x14FF331E7`, `0x14F6C1E98`, `0x14F6C1E9C`, and `0x14F6C1E80`, respectively. The additional boolean reference locations are `EnableManifoldGJKReplace` at `0x14FF331E5`, `EnableManifoldGJKInject` at `0x14FF331E6`, `ForceOneShotManifoldEdgeEdgeCaseZeroCullDistance` at `0x14FF331E4`, `OneSidedHeightField` at `0x14F6C1EA9`, `UseCapsuleTriMesh2` at `0x14F6C1EB4`, and `UseConvexTriMesh2` at `0x14F6C1EB5`. Direct code reads occur at:

- `UseGJK2`: `0x1426CE6A0` compares the referenced byte with zero. The flags survive the intervening arithmetic/setup instructions to `0x1426CE822`, where `je` selects the zero-valued path. The nonzero path calls `0x1426FEE40`; zero calls `0x142703250`.
- `EPAEpsilon`: `0x1426CE780` loads the float and `0x1426CE793` converts it from single to double precision.
- `GJKEpsilon`: `0x1426CE7CB` loads the float and `0x1426CE7D3` converts it from single to double precision.
- `UseCapsuleTriMesh2`: `0x14272CB15` compares the byte with zero; nonzero calls `0x1427E09F0`, while zero proceeds to the alternate setup path.
- `UseConvexTriMesh2`: `0x1427409AB` compares the byte with zero; zero calls `0x1426E6950`, while nonzero calls `0x142803DE0`.
- `PlaneContactNormalEpsilon`: `0x1426CEAB6` loads the float and `0x1426CEABE` converts it; `0x1426CEADD` compares it with a computed scalar, and `0x1426CEAE8` stores the comparison condition in a byte register for later logic.
- `EnableManifoldGJKReplace`: at `0x1426D29DF`, the byte is compared with a local state byte; when they differ, helper `0x14282DEC0` runs, and a true return jumps to `0x1426D39C8`. In the indexed contact loop at `0x14282FF40`, the replace and inject bytes are checked together when the chosen index is `-1`; either nonzero setting takes the common continuation, while both zero take `0x14283001F`.
- `ForceOneShotManifoldEdgeEdgeCaseZeroCullDistance`: read at `0x1426D2DFE`; the non-equal path performs a double-precision comparison at `0x1426D2E0E` and can jump to `0x1426D398C`.
- `OneSidedHeightField`: at `0x142888C67`, zero skips to `0x142888C9A`; nonzero runs the additional calculation and comparison beginning at `0x142888C75`.

Similar reads of the first four settings appear in three compiled routines at `0x1426CE...`, `0x1426CF...`, and `0x1426D0...`, consistent with repeated or inlined solver logic. This pattern does not identify the exact call-site inputs or prove that every gameplay collision uses these paths.

## Evidence and limits

- Types, help text, and reference RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- The direct-reference candidates are preserved in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The instruction addresses above were checked against the local build's disassembly; build identity and hash are documented in the [source notes](EVIDENCE.md#build-specific-static-analysis).
- `UseGJK2` is documented as a branch selector because that is directly observable. The “GJK,” “EPA,” and plane-normal-tolerance interpretations are grounded in variable names and, for the last one, community help; the exact solver math and resulting collision behavior are not recovered.
- Snapshot values do not establish defaults or safe overrides. No in-game test of these settings is recorded.

Related guides: [Chaos collision manifold and contact CVars](cvar-chaos-collision-manifold-contacts.md), [Chaos collision margins and triangle-mesh tolerances](cvar-chaos-collision-margins-tolerances.md), [Chaos scene-query CVars](cvar-chaos-scene-queries.md), [Chaos kinematic-target CVar](cvar-chaos-kinematic-target.md), and [CVar overrides and loader syntax](cvar-overrides.md).
