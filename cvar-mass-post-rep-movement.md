# Mass post-rep movement CVars

The registry lists two undocumented booleans whose names associate them with parallel post-rep movement: one general Mass switch and one Zombie-specific switch. In the installed build, each is checked before a guarded loop over an object list. A false value skips that loop; a true value permits it after object and state checks. The helper called for each list entry is not symbolized, so the exact movement operation and parallel scheduling behavior remain unknown.

## Variables

| CVar | Type | Snapshot | Verified behavior and limits |
|---|---|---:|---|
| `mass.EnableMassPostRepMovementParallel` | bool | `true` | Direct check at `0x14781F12A`; false jumps to `0x14781F189`, past a list-processing block. When true, the code checks a returned object, a type-like result, and another predicate; it then iterates a pointer array and calls `0x1436BF4A0` for non-null entries (`0x14781F154`–`0x14781F189`). More reads occur at `0x14781F203`, `0x147823455`, `0x147823C9B`, and other sites. The name suggests parallel post-rep movement, but this local loop does not itself show task creation or thread selection. |
| `mass.EnableMassZombiePostRepMovementParallel` | bool | `true` | Direct check at `0x1494B401A`; false jumps to `0x1494B4079`, past a structurally similar guarded list loop. When true, code checks the returned object, a type-like result, another predicate, and the list count before calling the same helper `0x1436BF4A0` for non-null entries (`0x1494B4026`–`0x1494B4079`). More reads occur at `0x1494BB305`, `0x1494BC16B`, `0x1494BD6A3`, and other sites. Its Zombie-specific scope comes from the CVar name; affected entity types are not identified by this trace. |

## Evidence and limits

- Both are `ref bool` entries with blank help in `console_vars.tsv` and no non-placeholder description in `console_objects.tsv`.
- The captured `true` values come from `CVarDump.txt`. They are not confirmed defaults or recommendations; the source attachment does not identify a game build or capture method.
- The full build scan found 10 direct `ref_rva` memory candidates for the general switch and 11 for the Zombie switch. These are static instruction sites, not runtime execution counts.
- Installed binary: build 1.1.4042190, SHA-256 `omitted from this documentation-only project`; raw hits are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included).
- No controlled run compared the two settings. This evidence does not establish performance impact, whether the helper executes on worker threads, which actors qualify, or whether one switch depends on the other. Both remain in the [definition-gap worklist](cvar-unresolved-definitions.md) pending fuller source or runtime evidence.
