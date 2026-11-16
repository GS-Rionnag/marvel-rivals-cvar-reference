# Chaos collision UnionBVH CVars

This guide covers the four `p.Chaos.Collision.UnionBVH.*` variables in the community registry and their references in the local Marvel Rivals Shipping build `1.1.4042190`. The registry snapshot values are captures, not verified defaults or recommendations.

| CVar | Type | Snapshot | Registry help | Local-build observation |
| --- | --- | ---: | --- | --- |
| `p.Chaos.Collision.UnionBVH.Enabled` | bool | `true` | Setting false disables BVH use during collision detection without affecting creation or serialization. | A collision path checks the referenced byte at `0x1428BF830`; zero branches around the later parameter loads/helper call, while nonzero continues into them. Other direct checks exist elsewhere in the build. |
| `p.Chaos.Collision.UnionBVH.MaxDepth` | int32 | `8` | Allowed BVH depth when wrapping a shape hierarchy. | The value is loaded into `r12d` at `0x1428BF845` immediately before a helper call at `0x1428BF879`. The trace does not establish the helper's exact interpretation of zero, negative, or unusually large values. |
| `p.Chaos.Collision.UnionBVH.NumShapes` | int32 | `7` | No registry help. | The value is loaded into `r15d` at `0x1428BF864` before the same helper call. Its exact role, limits, and interaction with `MaxDepth` are not recovered. |
| `p.Chaos.Collision.UnionBVH.SplitBias` | float | `0.1` | No registry help. | A later hierarchy-related routine loads it at `0x1428C5AA8`. After accumulating and normalizing three coordinate components, the routine adds this value to each component and stores the results for later use. The exact coordinate frame, units, and resulting split policy are unknown. |

## Evidence and limits

- Names, types, help, and RVAs come from the preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); the values above come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- The local PE image base is `0x140000000`. The referenced value RVAs are `0xF6C24E4` (`Enabled`), `0xF6C24EC` (`MaxDepth`), `0xF6C24E8` (`NumShapes`), and `0xF6C24E0` (`SplitBias`). Exact local build identity and hash are in the [source notes](EVIDENCE.md#build-specific-static-analysis); direct reference candidates are in the [address-hit table](EVIDENCE.md#evidence-artifacts-not-included).
- The branch and loads establish that these values affect local collision-related code. They do not prove that every map or collision shape uses the path, nor reveal safe override values. No in-game test is recorded.

Related guides: [Chaos collision solver CVars](cvar-chaos-collision-tolerances.md) and [CVar overrides and loader syntax](cvar-overrides.md).
