# Uppercase `Trace.*` CVar batch A

This guide documents the 11 currently uncovered exact-case `Trace.*` entries. They are distinct from other case-sensitive trace namespaces such as `trace.*` and `TraceMgr.*`. The supplied help identifies a FindWall debug-draw policy, a scope-trace merge switch, a scope-difference debug filter, and a shape-orientation compatibility switch. The other names lack useful descriptions. None has an exact-name Epic UE 5.9 CVar reference match.

The snapshot is an observation, not a default. Local build scans match registry address fields to instructions; they do not prove value reads/writes, runtime execution, or config acceptance. Build-context text windows show adjacent names and strings, which are not proof of a functional relationship. No `.ini` or in-game test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `Trace.AllowToLimitMaxTraceNum` | `bool` (`ref`) | `false` | — | No useful supplied help or exact-name Epic description. The name and neighboring `Trace.TickTraceMaxCount` string are not enough to confirm a runtime limit gate. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.DebugDrawClimbWall` | `int32` (`ref`) | `0` | — | Supplied help: `-1` shows no FindWall traces; `0` shows them only when `EnableDebugDraw` is true; `1` shows all FindWall traces. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.DefaultRollback` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.EffectCompWaitTraceEnd` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.EnableCustomPreFilter` | `int32` (`var`) | `1` | — | No useful supplied help; the object-table fragment is only `.`. Exact filter behavior and accepted values are unresolved. | `ref_rva`: no recorded matches; `obj_rva`: 2 direct-memory candidates and 1 address-taking reference. |
| `Trace.EnableScopeTraceMerge` | `bool` (`ref`) | `false` | — | Supplied help: global switch for scope-tick trace-merge optimization. The merge conditions and functional impact are not described. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.GDebugScopeDiffHit` | `int32` (`ref`) | `-1` | — | Supplied help: `-1` disables it, `0` applies to all scopes, and a scope ID selects one scope. The exact difference being debugged is not described. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.ScopeTracePolicy` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description; behavior remains unresolved. | `ref_rva`: 6 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.SupplementShapeOrientationFix` | `bool` (`ref`) | `true` | — | Supplied help: `1` uses the regular `CheckDir` direction for `bTraceSupplement` shape orientation; `0` restores the older movement-vector behavior. | `ref_rva`: 3 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.TickTraceMaxCount` | `int32` (`ref`) | `999` | — | No useful supplied help or exact-name Epic description. Its relationship to `AllowToLimitMaxTraceNum` is not established. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `Trace.UseHittedProjectileRollback` | `bool` (`ref`) | `true` | — | No useful supplied help or exact-name Epic description. The registry spelling `Hitted` is retained; exact rollback behavior remains unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- `DebugDrawClimbWall` describes a FindWall trace visibility policy. It does not say that trace execution is enabled or changed by the debug-draw setting.
- `EnableScopeTraceMerge` describes an optimization switch but does not specify what queries can merge, their ordering, or effects on gameplay.
- `SupplementShapeOrientationFix` gives two source-described direction choices; no test establishes the behavior in the installed game.
- Nearby `Trace.*` entries in the build-context inventory are string/address neighbors. They do not establish data flow or that one CVar controls another.
- Static address counts are not function-level evidence. Whether any of these names is registered as an editable CVar or honored by startup `.ini` overrides is unverified.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
