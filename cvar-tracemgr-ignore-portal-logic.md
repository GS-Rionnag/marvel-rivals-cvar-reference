# `TraceMgr.CVar_IgnorePortalLogic`

The community registry identifies this as an undocumented boolean. Its name and namespace suggest portal-related trace handling, but the local code does not expose enough names to verify the exact behavior.

## Registry and build evidence

- Community row: `kind=ref`, `vtype=bool`, blank help, `ref_rva=0x100AA531`, `obj_rva=0x100AA548`.
- Captured snapshot: no matching row in `CVarDump.txt`; no captured value is available.
- The build 1.1.4042190 address scan found seven direct references to the value, at `0x146344722`, `0x1463452A6`, `0x14635A4DD`, `0x14635F4EE`, `0x149467C5D`, `0x1494684F2`, and `0x1494685CC`. The surrounding initialization-like sequence is present at `0x140BE885B` and later stores the returned object pointer at `0x1500AA548`.

## What the inspected branches show

- At `0x146344722`, a nonzero value jumps to `0x1463447C7`. Zero continues into a path that prepares arguments and conditionally calls a virtual method at object offset `0x418`.
- At `0x1463452A6`, nonzero jumps over a block that checks object fields and performs a nested lookup followed by a helper call. The zero path is gated by those additional field and lookup checks.
- At `0x14635A4DD`, nonzero enters a path that reads a stored value and calls helper `0x146D53940`. Zero takes another path through helpers `0x146D544F0` and `0x1438BAA30`.
- At `0x14635F4EE`, the CVar is compared with a local byte. Equality takes a path that can call `0x146D544F0` and `0x1438BAA30`; inequality takes a stored-value path through `0x146D53940`.

These observations establish that the setting changes control flow in several trace-manager-related routines. They do not establish the source-level meaning of the helper calls or show that every alternate path omits portal tests. “Ignore portal logic” is therefore a name-based interpretation, not a verified description of what a player will see.

## Use limits

No snapshot value, exact default, accepted runtime range, performance effect, or match-tested result is available. The static evidence supports only that zero and nonzero can choose different paths in this build. Do not treat `1` as a proven safe or recommended override. Recheck the addresses after game updates; see the [CVar source notes](EVIDENCE.md#build-specific-static-analysis) for the executable identity and scan limits.
