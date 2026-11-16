# Remaining Marvel CVar batch C

This guide covers the 10 remaining registered `Marvel.*` names not found in the existing explanatory tables at the time of this audit. Community help, unreviewed Chinese-to-English renderings, captured snapshot values, and build-specific address candidates are kept distinct. No exact Epic UE 5.9 reference entry was found for these names.

Build evidence is from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. Direct-memory candidates may be reads, comparisons, or writes; `var` object hits may be registration/setup. No control-flow trace, live CVar query, controlled `.ini` override, or gameplay test was performed.

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied help and translation status | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Marvel.RepGraph.EnableSummonedConnectionFilter` | bool (`ref`) | `false` | `—` | Chinese help: 开启针对特定召唤物(104251101, 10427102)的网络连接过滤逻辑。 true: 开启过滤 (默认) false: 关闭过滤。 *Unreviewed English rendering: Enable a network-connection filter for specific summoned actors (104251101, 10427102). true = enable filtering (default); false = disable filtering.* | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime use were not traced. |
| `Marvel.SkipFindMHideMaterial` | bool (`var`) | `false` | `—` | Community help: Skip find m hide material. 0: Don't, 1: Skip | CVar-object setup/address references only; this `var` has no `ref_rva`, so value consumption was not established. |
| `Marvel.SkipJeffSkinCustomization.101582` | bool (`var`) | `false` | `—` | Community help: Skip Jeff skin customization. 0: Don't, 1: Skip | CVar-object setup/address references only; this `var` has no `ref_rva`, so value consumption was not established. |
| `Marvel.SkipJeffSkinCustomization.101871` | bool (`var`) | `false` | `—` | Community help: Skip Jeff skin customization. 0: Don't, 1: Skip | CVar-object setup/address references only; this `var` has no `ref_rva`, so value consumption was not established. |
| `Marvel.SkipMHideMaterialCheck.101871` | bool (`var`) | `false` | `—` | Chinese help: 101871 是否跳过 M_Hide 材质检测逻辑。 *Unreviewed English rendering: Whether 101871 skips the M_Hide material check.* | CVar-object setup/address references only; this `var` has no `ref_rva`, so value consumption was not established. |
| `Marvel.TestGEScript` | int32 (`ref`) | `—` | `—` | No explanatory help was supplied; exact behavior is unresolved. | 3 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime use were not traced. |
| `Marvel.TraceComponent.LockGeometryCollectionDuringPhysics` | bool (`ref`) | `true` | `—` | No explanatory help was supplied. The name suggests a physics-time Geometry Collection lock, but this is name-derived and unverified. | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime use were not traced. |
| `Marvel.TriggerAnimCurveMode` | int32 (`ref`) | `1` | `—` | Chinese help: 更改动画曲线模式，0只生效Index，非0只生效Tag曲线。 *Unreviewed English rendering: Change the animation-curve mode: 0 uses Index curves only; nonzero uses Tag curves only.* | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime use were not traced. |
| `Marvel.UI.EnableAbilityProxyStateFix` | int32 (`var`) | `—` | `—` | Chinese help: 技能图标换绑状态修复：0=关闭，非零=开启；切换从下一次绑定生效。 *Unreviewed English rendering: Fix ability-icon remapping state: 0 = off; nonzero = on. A change takes effect on the next binding.* | CVar-object setup/address references only; this `var` has no `ref_rva`, so value consumption was not established. |
| `Marvel.UseCharActorCommand` | bool (`ref`) | `true` | `—` | No explanatory help was supplied; exact behavior is unresolved. | 6 direct-memory candidate(s), 2 address-taken reference(s); access direction and runtime use were not traced. |

## Limits

- `Marvel.RepGraph.EnableSummonedConnectionFilter` has community help that calls true the default while the unversioned snapshot records false. This may reflect a user override or build/capture difference; the effective default is unknown.
- Four Chinese descriptions use English renderings already labeled unreviewed in the translation catalog. Treat those readings as provisional.
- Several rows have no useful help. Their exact effect is intentionally left unresolved rather than inferred from a name.
- These settings may alter gameplay, network filtering, animation, or material work. Registry presence does not establish runtime editability or a safe value to change.

For registry and build evidence context, see the [community CVar registry](cvar-community-registry.md) and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
