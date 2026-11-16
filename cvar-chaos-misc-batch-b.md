# Chaos miscellaneous CVars: batch B

This page documents 20 exact lower-case-`chaos` names from the community registry. Exact capitalization matters: these `p.chaos.*` names are separate strings from similarly named `p.Chaos.*` entries.

## Registry and snapshot

| Exact CVar | Type | Registry help | Captured value | Local build reference evidence |
| --- | --- | --- | ---: | --- |
| `p.chaos.clustering.breakonlystrained` | int32 | If enabled, only process strained clusters for breaks; if disabled, traverse and check all clusters. | `1` | Direct compare with `1` at `0x14292F88F`. |
| `p.chaos.CueManagerHandleClientGCSecondaryFragment` | bool | *(blank)* | `true` | Direct byte compare at `0x146C8F729`. |
| `p.chaos.DebugDrawGCRenderBound` | bool | Debug draw GC render bound. | `false` | The saved scan has an address-taking match, but no direct value-read candidate. |
| `p.chaos.DisableGCStreaming` | bool | If true, GC render data loads fully during initialization instead of streaming. | `false` | Direct byte compare at `0x142DD98F8`. |
| `p.chaos.DontUseChaosSceneSimCallBack` | bool | Don't use `FChaosSceneSimCallBack`. | `true` | Four direct byte comparisons at `0x142B840A7`, `0x142B849B6`, `0x142B9A87E`, and `0x142BA6656`. |
| `p.chaos.EnableFragmentVfxCulling` | bool | *(blank)* | `true` | Direct byte compare at `0x146C80E26`. |
| `p.chaos.EnableSyncFragmentVfxCulling` | bool | *(blank)* | `true` | Direct byte compare at `0x146C80E84`. |
| `p.chaos.FragmentVfxCullDistance` | float | *(blank)* | `5000` | Direct float load at `0x146C80E58`. |
| `p.chaos.gpdispatch.collisions.reduce` | int32 | Enable reduced collision-event dispatch (`0` off, `1` on). | `0` | Direct compare with `1` at `0x142D30C20`. |
| `p.chaos.gpdispatch.collisions.reduceamount` | float | Percentage of collisions actually dispatched (`0`–`1`). | `0.1` | Direct float load at `0x142D30C29`. |
| `p.chaos.HitShapeAddToSolver` | bool | HitShape add to solver. | `false` | Direct byte compare at `0x143A009F2`. |
| `p.chaos.HitShapePhysicsParallelUpdate` | bool | HitShape PhysicsParallelUpdate. | `true` | Direct byte compare at `0x1439E2E90`. |
| `p.chaos.ImmediatelyHiddenFractureClientGC` | bool | Immediately hidden fracture ClientGC. | `true` | Direct byte compare at `0x146C948A8`. |
| `p.chaos.MinContactSpeedForStrainEval` | float | Minimum contact speed before accumulating for strain evaluation. | `1` | Direct float load at `0x14292CE6E`. |
| `p.chaos.MinImpulseForStrainEval` | float | Minimum accumulated impulse before accumulating for strain evaluation. | `65.3333` | Direct float load at `0x14292CF1A`. |
| `p.chaos.RefreshISMCWhenInstantReplayStopped` | bool | Refresh ISMC after instant replay stops. | `true` | Direct byte compare at `0x146C9481C`. |
| `p.chaos.StreamingMaxReferenceChecks` | int32 | Number of times the engine waits for references to be released before forcing stream-out (help says default `2`). | `2` | Compared twice with a local integer at `0x142DEDC38` and `0x142DEDC4C`. |
| `p.chaos.SyncFragmentVfxCullDistance` | float | *(blank)* | `5000` | Direct float load at `0x146C80EBD`. |
| `p.chaos.UseClientGCInstanceRender` | int32 | Whether to use an instance-based way to render ClientGC. | `1` | Direct integer comparisons at `0x146C9A010` and `0x146C9A9C8`. |
| `p.chaos.UseContactSpeedForStrainEval` | bool | Whether contact speed discards contacts during cluster-strain updates (`true`: speed, `false`: impulse). | `true` | Direct byte compare at `0x14292CD97`. |

The captured values are from `CVarDump.txt`; they are not verified defaults or recommendations. The help text is the community attachment's text. Empty help cells mean that attachment supplied no description for the entry.

## What the local code supports

The address-hit scan for the installed Shipping executable found direct value references for 19 of these 20 names. `p.chaos.DebugDrawGCRenderBound` had an address-taking match only. A direct read or comparison shows that code accesses the referenced value; a single instruction does not by itself establish its exact branch outcome, when the routine executes, or a visible in-game result.

- **Cluster strain and collision dispatch:** the local code compares `breakonlystrained` with `1`; reads both strain thresholds as floats; and checks `UseContactSpeedForStrainEval`. This supports their use as inputs to a cluster/strain path, consistent with the registry help, but the full accumulation and break algorithm was not traced. The collision-dispatch enable is checked against `1`, and its companion amount is loaded as a float. This is compatible with the help's enable/percentage descriptions; sampling policy and actual external event consumers are not identified here.
- **Fragment VFX culling:** the two enable values are compared with zero, and both distance values are loaded in the same nearby code region. That supports a culling-related code path using switches and distances. The help is blank for these four names, so distance units, which effects are culled, and the distinction between “sync” and ordinary culling are unresolved.
- **Client Geometry Collection paths:** `CueManagerHandleClientGCSecondaryFragment`, `ImmediatelyHiddenFractureClientGC`, and `RefreshISMCWhenInstantReplayStopped` each have a direct byte comparison; `UseClientGCInstanceRender` is compared at two sites. These are direct value-use evidence, but the exact rendering/replication behavior comes only from the names and, for `UseClientGCInstanceRender`, its registry help.
- **Other settings:** `DisableGCStreaming`, `DontUseChaosSceneSimCallBack`, the two HitShape flags, and `StreamingMaxReferenceChecks` are directly accessed. Their help gives a likely purpose, but the inspected references alone do not establish which modes reach the branches or all side effects. The multiple callback comparisons show repeated checks, not that the callback is globally disabled in every path.
- **Debug drawing:** no direct `ref_rva` value read for `DebugDrawGCRenderBound` appears in the saved scan. This does not prove the variable is unused: indirect access or code outside the scan can be missed. The help indicates intended debug visualization, not that it is visible in normal Shipping gameplay.

## Can the loader edit these?

The supplied override loader instructions say an uncommented `name=value` line under `[Overrides]` is merged above config and wins over existing config. Thus the loader syntax can express an override for these exact names, for example:

```ini
[Overrides]
p.chaos.gpdispatch.collisions.reduce=1
p.chaos.gpdispatch.collisions.reduceamount=0.1
```

That is **syntax compatibility only**. The registry and static binary reads do not prove this build accepts the requested value from the loader, retains it after later startup settings, or produces an observable effect. No controlled runtime change was tested for this batch. Also follow the loader's stated rule that settings capable of removing smoke or other effects are ignored; no such effect-removal behavior was established for these 20 entries.

## Sources and scope

- Names, types, help, and `ref_rva` values: preserved [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322).
- Captured values: [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452).
- Direct/address-taking instruction candidates: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); scanner scope and caveats are documented in the [source README](EVIDENCE.md#build-specific-static-analysis).
- Local target: installed `Marvel Rivals Shipping executable`, build `1.1.4042190`, image base `0x140000000`. The community registry's build alignment is unknown.
- Loader behavior and the distinction between syntax, acceptance, code use, and a demonstrated effect: [CVar overrides](cvar-overrides.md).

No controlled runtime experiment was performed. Treat the registry explanations as source help, the snapshot as a captured state, and the disassembly notes as static local-build evidence.
