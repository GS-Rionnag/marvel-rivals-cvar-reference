# Python GC quota variables

This guide covers three undocumented `Python.*` references in build 1.1.4042190. Their names and static call paths tie them to a GC-related quota, but the Python calls and lifecycle hooks have not been validated at runtime.

## Variables and captured values

| CVar | Registry type | Snapshot |
|---|---|---:|
| `Python.PythonScopedGCQuota` | int32 | `0` |
| `Python.PythonGCAfterUnrealGC` | bool | `false` |
| `Python.SetPythonGCQuotaAfterWorldCleanup` | bool | `false` |

All three have blank help in the community variable and object tables. Snapshot values are not confirmed defaults.

## Quota reset path

At `0x144C2C47D`, code checks `Python.PythonGCAfterUnrealGC`. If it is false, the code checks `Python.SetPythonGCQuotaAfterWorldCleanup` and a positive integer field at `[rsi+0x10]`. When either condition selects the path, it clears that field and stores decimal `19` in `Python.PythonScopedGCQuota` (`0x144C2C495`–`0x144C2C4A3`).

The code confirms the two booleans can reset that field and set the quota to 19. The nearby cleanup/lifecycle name comes from the CVar names; the containing function's exact event and the meaning of `[rsi+0x10]` are not identified.

## Countdown and helper path

At `0x144D1A660` and `0x144D1A870`, code first calls `0x1496BD6C0`, then checks whether the quota is positive. If a second gate (`0x140EB07B0`) is true, it subtracts one. When that decrement reaches zero, it calls `0x144C27E90`. Similar compare/decrement sequences account for most of the 42 direct-reference scan hits; repeated sites should not be treated as 42 distinct features.

The helper at `0x144C27E90` accesses static data containing the strings `gc` and `disable`, checks Python-runtime/thread-local state, and calls a runtime wrapper. This links quota exhaustion to Python GC-related work, but does not by itself establish whether the exact operation collects, disables, re-enables, or otherwise manages Python GC. No collected object count or time interval is directly supplied by this CVar in the inspected instructions: it is used as a decrementing integer quota.

## Limits

This is static evidence from one Shipping build. Exact caller names, the second decrement gate, the Python wrapper's API contract, thread restrictions, performance impact, and loader acceptance are unknown. `19` is a literal assigned by the inspected reset path, not a recommended CVar value. The [source notes](EVIDENCE.md#build-specific-static-analysis) identify the executable hash and limits of the address scan.
