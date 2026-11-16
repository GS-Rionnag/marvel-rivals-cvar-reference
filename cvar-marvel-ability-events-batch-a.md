# Marvel ability, attribute, and replication CVars batch A

This guide documents 23 currently uncovered registered `Marvel.*` CVars across ability initialization, component caching, attribute-event RPCs, and GameState replication. Community help and captured values come from an unversioned community registry; exact-name Epic UE 5.9 references are shown separately where available. Neither source establishes the live build or current runtime value.

Build evidence is from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. A direct-memory candidate may be a read, comparison, or write; a `var` object reference may be registration/setup. These matches do not establish a runtime path, branch direction, or accepted startup override. No controlled config or in-game test was performed.

## Ability and component-cache controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Marvel.Ability.10274101.EnableUpdateTeamVisualEffects` | int32 (`var`) | `0` | `—` | Enable ACue_Ability_Loop_10274101::UpdateTeamVisualEffects refresh logic. 0=Disabled, 1=Enabled *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.Ability.10340101.AeroCollectTickInterval` | int32 (`var`) | `—` | `—` | Original: ACue_Ability_Loop_10340101 Tick 中贴地悬浮判定的采集间隔 Tick 数。1=每 Tick 检测的原始逻辑 English rendering: Number of Ticks between grounded-hover checks in ACue_Ability_Loop_10340101 Tick. 1 = the original logic checks every Tick. (assistant translation, not independently reviewed). *(source: community help; translation unreviewed)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.Ability.10340101.EnableUpdateTeamVisualEffects` | int32 (`var`) | `0` | `—` | Enable ACue_Ability_Loop_10340101::UpdateTeamVisualEffects refresh logic. 0=Disabled, 1=Enabled *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.Ability.DelayInitializeProxyAbilities` | bool (`ref`) | `true` | `—` | If true, delay the initialize of Proxy Abilities until manually triggered. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.Ability.FixDynamicTypeTagDoubleRemove` | bool (`ref`) | `true` | `—` | When true, force-enable the dynamic-type-change LooseTag leak fix for all abilities; when false, only abilities whose bFixDynamicTypeTagDoubleRemove is true are fixed. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.Ability.WaitingRemoveAbilityCheckInterval` | float (`ref`) | `1` | `—` | Check interval in seconds for waiting remove ability timeout. Default: 1.0 *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.Ability.WaitingRemoveAbilityTimeout` | float (`ref`) | `10` | `—` | Timeout in seconds for waiting remove ability groups. Default: 20.0 *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.AgentComponentCache.LRU.Enable` | int32 (`var`) | `0` | `—` | Enable LRU eviction for AgentComponentCache (0=off, 1=on) *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.AgentComponentCache.LRU.MaxSize` | int32 (`var`) | `2000` | `—` | Max number of cached agent components when LRU is enabled *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.AgentComponentCache.SkipEmptyReadableName` | int32 (`ref`) | `0` | `—` | When enabled (1), allow cache reuse for components with no CustomReadableName (0=off, 1=on) *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |

## Attribute event RPC controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Marvel.AttributeEvent.BatchDictionary` | int32 (`var`) | `—` | `—` | 1: try the separate shared-table Batch RPC; 0: use the unchanged legacy RPC. *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `Marvel.AttributeEvent.MaxTargetsPerGroup` | int32 (`ref`) | `64` | `—` | Max targets per optimized RPC batch (default: 128) *(source: community help)* | 6 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.AttributeEvent.PVE` | int32 (`ref`) | `0` | `—` | Enable optimized attribute event RPC with lossy compression 0 = Disabled (use original MulticastAttributeEvent_NewMerge) 1 = Enabled (use optimized FMulticastAttributeEventOptimized) *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.AttributeEvent.Verification` | int32 (`ref`) | `0` | `—` | Enable verification mode: send both old and new RPCs for data comparison 0 = Disabled 1 = Enabled (send both RPCs, log serialization size and data comparison) *(source: community help)* | 5 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |

## GameState and camera RPC controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Marvel.GameState.BigBoundsThreshold` | int32 (`ref`) | `20000` | `—` | Marvel.GameState.BigBoundsThreshold *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.CameraRPCCompressed` | int32 (`ref`) | `1` | `—` | Original: 1=CameraInfo 直发走 23bit 压缩 RPC，0=走原版 English rendering: 1 = send CameraInfo directly using a 23-bit compressed RPC; 0 = use the original path. (assistant translation, not independently reviewed). *(source: community help; translation unreviewed)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.CameraRPCUseChar` | int32 (`ref`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in the available references. *(source: not described)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.CheckPhysicsInterval` | float (`ref`) | `5` | `—` | Marvel.GameState.CheckPhysicsInterval *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.EnableKillBroadcastRegisterPrefilter` | bool (`ref`) | `true` | `—` | Original: 击杀广播预过滤开关：1=对 bNeedGameStateRegister=false 的角色跳过 OnPlayerKill_NextFrame_Dispatcher 广播，0=回退全广播 English rendering: Kill-broadcast prefilter: 1 skips the OnPlayerKill_NextFrame_Dispatcher broadcast for characters with bNeedGameStateRegister=false; 0 restores broadcasts for all. (assistant translation, not independently reviewed). *(source: community help; translation unreviewed)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.GUseRPCBatchOpt` | bool (`ref`) | `false` | `—` | GUseRPCBatchOpt *(source: community help)* | 10 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.MoreShpaesThreshold` | int32 (`ref`) | `500` | `—` | Marvel.GameState.MoreShpaesThreshold *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.MovingParticleThreshold` | int32 (`ref`) | `100` | `—` | Marvel.GameState.MovingParticleThreshold *(source: community help)* | 3 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |
| `Marvel.GameState.RpcRatio` | float (`ref`) | `0.2` | `—` | RPCBatchNumRatio *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); reads/writes and runtime callers were not distinguished. |

## Interpretation limits

- These settings can alter abilities, tag handling, attribute replication, camera RPC encoding, or GameState event filtering. The descriptions do not establish what the game enables, whether a setting is safe in a match, or whether a config layer accepts it.
- Help translated from Chinese is labeled as an unreviewed English rendering; the original text is retained alongside it.
- Snapshot values are observations from an unversioned capture, not recommendations or confirmed defaults. Epic 5.9 values are upstream references only.
- Direct address candidates and object setup references are static evidence, not observed runtime reads.

For related findings, see the [game-specific embedded-text guide](cvar-game-specific-embedded-help.md), [community CVar registry](cvar-community-registry.md), and [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis).
