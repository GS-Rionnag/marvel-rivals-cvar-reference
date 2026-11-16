# Replay recording and checkpoint CVars, batch B

This batch covers 21 uncovered `demo.DeathReplay.*`, `demo.Record.*`, and `demo.Checkpoint.*` variables, plus four related replay lifecycle/recording controls. Community help, exact-name Epic UE 5.9 descriptions/defaults, and the untagged community snapshot are kept separate. Namespace and name patterns are not treated as proof of detailed behavior.

Build evidence comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. Direct-memory candidates can be reads, comparisons, or writes. For registry `var` entries, object-address references may only show setup. No call-path trace, live CVar query, controlled config override, or gameplay replay test was performed.

## Death replay controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `demo.DeathReplay.BufferHintSeconds` | float (`var`) | `25` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.ClientDataVersion` | int32 (`var`) | `2` | `—` | 0: Default, 1: ChunkSplit, 2: NetPacketReplay *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.ClientEnableNetPacketReplay` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.NetPacketChunkTime` | float (`var`) | `0.5` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.RecordPerFrame` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.ServerDataVersion` | int32 (`var`) | `2` | `—` | 0: Default, 1: ChunkSplit, 2: NetPacketReplay *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.DeathReplay.ServerEnableNetPacketReplay` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |

## Recording and checkpoint controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `demo.Checkpoint.DelayRepTime` | int32 (`var`) | `0` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Checkpoint.Opt` | int32 (`var`) | `4` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Checkpoint.RestorePrevAckOverride` | int32 (`ref`) | `1` | `—` | When enabled (default), ProcessCheckpointActors restores the OverridePackageMapExportAckStatus pointer active at entry instead of unconditionally resetting to the main ack state; closes the main-state window for checkpoint states chained in the same TickCheckpoint call. Set 0 for legacy reset-to-main behavior. *(source: community help)* | 4 direct-memory candidate(s), 2 address-taken reference(s); access direction and call path were not traced. |
| `demo.Record.BattleType` | int32 (`var`) | `0` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.CheckpointLevelOpt` | int32 (`var`) | `0` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.CloseAddCustomData` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.Continue` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.FakeVersion` | int32 (`var`) | `0` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.LevelOpt` | int32 (`var`) | `4` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.MapOpt` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.MinCheckpointUploadDelay` | float (`var`) | `3` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.Open` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.ReplayNetVersion` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.Record.ServerTime` | int32 (`var`) | `1` | `—` | No explanatory help was supplied; exact behavior remains unresolved in available references. *(source: not described)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |

## Replay lifecycle and recording controls

| Exact CVar | Type | Snapshot | Epic 5.9 default | Description and provenance | Build reference evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `demo.AsyncLoadWorld` | int32 (`var`) | `0` | `0` | If 1, we will use seamless server travel to load the replay world asynchronously *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.CheckpointSaveMaxMSPerFrameOverride` | float (`var`) | `6` | `-1` | If >= 0, this value will override the CheckpointSaveMaxMSPerFrame member variable, which is the maximum time allowed each frame to spend on saving a checkpoint. If 0, it will save the checkpoint in a single frame, regardless of how long it takes. *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.ClientRecordAsyncEndOfFrame` | int32 (`var`) | `0` | `0` | If true, TickFlush will be called on a thread in parallel with Slate. *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |
| `demo.CullDistanceOverride` | float (`var`) | `0` | `0` | If > 0, will represent distance from any viewer where actors will stop being recorded. *(source: community help)* | CVar-object setup/address references only; this `var` has no `ref_rva`, so runtime value consumption was not established. |

## Scope

- The help text includes replay format modes (`Default`, `ChunkSplit`, `NetPacketReplay`), recording controls, checkpoint upload/save behavior, asynchronous world loading, end-of-frame recording, and actor recording distance. Entries with no help remain unresolved.
- Captured snapshot values are not recommendations or verified defaults. An Epic 5.9 match is upstream context and does not prove Marvel Rivals uses that engine version.
- A registered name and static address candidate do not establish that the CVar is runtime-editable or accepted by a startup override.

For related coverage, see [Replay memory and playback CVars](cvar-demo-replay-memory-playback-batch-a.md) and [the community CVar registry](cvar-community-registry.md).
