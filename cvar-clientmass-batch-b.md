# Client Mass CVar batch B: remaining swarm controls

This guide covers the 38 registered `clientmass.*` CVars not listed in batch A. The supplied community help describes physics write batching, object pools, local and remote spell fields, remote projectile judgments, and spawn budgets. The registry does not give a capture build/method; these entries have no snapshot values or exact Epic UE 5.9 defaults.

Build evidence comes from static address-reference scanning of Marvel Rivals Shipping build `1.1.4042190`. For `var` entries the scan only supplies CVar-object setup/address candidates and there is no `ref_rva` value field. For `ref` entries direct-memory candidates may be reads, comparisons, or writes. No surrounding control flow, runtime path, or accepted `.ini` override was established. No live query or gameplay comparison was performed.

## Physics writes and pooled-unit budgets

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.PhysicsWriteBatch` | int32 (`var`) | `—` | `—` | Hit bodies written per physics scene write lock; other scene readers can take the lock between batches. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PhysicsWriteGapUs` | float (`var`) | `—` | `—` | Pause in microseconds between physics write batches. The scene lock lets a releasing writer take it straight back, so without a pause readers woken by the release (game-thread movement sweeps) stay blocked for the whole write. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PoolGrowthPerFrame` | int32 (`var`) | `—` | `—` | Pooled resources created per frame, 0..16384; 0 forbids growth, so an empty pool backpressures. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PoolIdleSeconds` | float (`var`) | `—` | `—` | A free pooled unit is reclaimed only after being idle this long, 0..3600 s; 0 disables the age rule. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PoolMax` | int32 (`var`) | `—` | `—` | Free pooled units the world keeps at most, 0..16384; the pool never grows past this. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PoolReclaimPerFrame` | int32 (`var`) | `—` | `—` | Idle pooled resources destroyed per frame, 0..16384; 0 disables reclaim. Never touches an active lease. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.PoolWarmup` | int32 (`var`) | `—` | `—` | Pooled units pre-created when a looping run starts, 0..16384; capped by clientmass.PoolMax. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |

## Remote attackers, fields, and projectiles

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.QueryByObject` | int32 (`ref`) | `—` | `—` | Overlap-mode swarm queries use an object-type overlap (swarm proxies ignore all channels). 0 = old channel overlap. | 5 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote` | int32 (`ref`) | `—` | `—` | Remote attackers (simulated pawns) kill client swarm units. 0 = only the local player, as before. | 6 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.BoundsMargin` | float (`var`) | `—` | `—` | Margin (cm) around a route run's bounds: a field outside gets no window for that run (all fields). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.CheckBudget` | int32 (`var`) | `—` | `—` | Unit x remote field checks per frame (separate from clientmass.LocalScopeCheckBudget). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.MaxProjectileFields` | int32 (`var`) | `—` | `—` | Max remote projectiles tracked at once. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.MaxScopeFields` | int32 (`var`) | `—` | `—` | Max remote replicated scope fields alive at once. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.MaxShadowFields` | int32 (`var`) | `—` | `—` | Max frozen remote shadow fields (no-actor scopes the client never spawns) alive at once. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.MaxWindows` | int32 (`var`) | `—` | `—` | Max remote field windows (field x route run) alive at once. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.NpcGate` | int32 (`ref`) | `—` | `—` | 1 = only remote characters whose replicated loose tags hold CustomEffect.HideHpBarAndName (spawner NPCs) damage the swarm. 0 = every remote character, as before. | 5 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.NpcGateRejectTTL` | float (`ref`) | `—` | `—` | Seconds a remote attacker refused by clientmass.Remote.NpcGate stays refused before its tag is read again. <= 0 = read on every attack. | 5 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.Projectile` | int32 (`ref`) | `—` | `—` | Remote replicated projectiles judged along their sampled path. 0 = off. | 4 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.ProjectileDebugActor` | FString (`var`) | `—` | `—` | Log remote projectile lifecycle events for this exact actor name only. Empty = off. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.ProjectileJudgeDelay` | float (`var`) | `—` | `—` | Seconds a remote projectile's path is judged behind its sampled position, so a late server hit still clips it. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.ProjectileMinRadius` | float (`var`) | `—` | `—` | Minimum judge radius (cm) of a remote projectile (its table RoleCollisionRadius otherwise). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.ProjectileServerHit` | int32 (`ref`) | `—` | `—` | Deliver server hits to registered remote flights. 0 = only prediction-paired replicas (old). | 4 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.ProjectileZMargin` | float (`var`) | `—` | `—` | Extra vertical half extent (cm) of remote projectile paths and the explosions they leave. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.Remote.QueryBudget` | int32 (`ref`) | `—` | `—` | Remote client-traced scope attacks physics-queried per frame (local attacks are not limited). | 4 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.Scope` | int32 (`ref`) | `—` | `—` | Remote replicated scope actors (passive fields). 0 = off. | 4 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.Shadow` | int32 (`ref`) | `—` | `—` | Remote no-actor scopes (other players' and NPC melee) captured on simulated proxies for the client swarm. 0 = off. | 5 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.Remote.ZMargin` | float (`var`) | `—` | `—` | Extra vertical half extent (cm) of remote fields: simulated pawns replicate no pitch, directions are horizontal. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |

## Local spell scopes and segmented attacks

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.ScopeCheckPeriod` | float (`var`) | `—` | `—` | Seconds between checks of a local player spell field against the client swarm (min 0.033). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeEnable` | int32 (`ref`) | `—` | `—` | Local player spell fields (client trace off) kill client swarm units. 0 = off (emergency switch). | 4 direct-memory candidate(s), 2 address-taken reference(s); direction, callers, and runtime path were not traced. |
| `clientmass.ScopeIntervals` | int32 (`var`) | `—` | `—` | Static spell field windows use route intervals (1) or the plain shape test (0). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeRectSweep` | int32 (`var`) | `—` | `—` | Moving box fields sweep from the previous check's pose to the current one. 0 = current pose only. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeRefusedRetry` | int32 (`var`) | `—` | `—` | Consume every refused window for bounded one-shot retries. 0 = require skipped/overflow counters (old). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeSegmentCommitOnSuccess` | int32 (`var`) | `—` | `—` | Commit a segment endpoint only after its field is accepted. 0 = commit before building (old). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeSegmentFinalByTime` | int32 (`var`) | `—` | `—` | Hero segment attacks: 1 = judge the explosion list when its scope is due; 0 = when the list first changes (old). | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeSegmentFinalSlack` | float (`var`) | `—` | `—` | Hero segment attacks: seconds after the computed explosion time before its list is judged. < 0 = the source's default. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.ScopeSegments` | int32 (`var`) | `—` | `—` | Hero segment attacks (e.g. Q 106361 ground strip) kill swarm units. 0 = off. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |

## Client swarm spawn budgets

| Exact CVar | Type | Snapshot | Epic 5.9 default | Supplied community help | Build address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `clientmass.SpawnBudget` | int32 (`var`) | `—` | `—` | Maximum client swarm units instantiated per PrePhysics tick. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |
| `clientmass.SpawnBudget.DueOnly` | int32 (`var`) | `—` | `—` | 1: a finite wave asks for spawn budget only for candidates already due and spends it per candidate processed. 0: legacy accounting (asks for every remaining plan, spends per unit created), which lets an earlier wave's future plans starve later waves; kept to reproduce that case. Read once per tick. | CVar-object address/setup candidates only; this `var` has no `ref_rva` value field, so runtime value consumption is unverified. |

## Reading the limits

- The help defines values and behavior for these entries, but it does not establish Marvel Rivals runtime values, accepted ranges beyond those explicitly stated, or how settings combine in the match.
- A `0` value has different meanings across the family: it can disable a path, mean no cap, forbid pool growth, or select an older behavior. Use each row’s help text rather than treating zero as a universal off switch.
- Remote attacker/projectile and spell-scope controls can change which effects interact with the client swarm. They are gameplay/simulation controls, not generic graphics performance settings.
- The `var`/`ref` registry labels and static address candidates do not prove mod-loader editability or a live gameplay effect.

For the first client swarm controls, see [Client Mass batch A](cvar-clientmass-batch-a.md). The [community CVar registry](cvar-community-registry.md) explains the snapshot and exact-name UE-reference limitations; build scan scope is described in [the CVar inventory](EVIDENCE.md#build-specific-static-analysis).
