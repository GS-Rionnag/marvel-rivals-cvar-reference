# `Performance.DestroyActorFrame.Enable`

This guide records the local build's code paths for one undocumented CVar. The name suggests a per-frame actor-destruction optimization, but the recovered instructions do not establish that interpretation or its runtime effect.

## Registry evidence

- The community table classifies it as `ref bool`; both help columns are blank.
- `CVarDump.txt` records `false`. This is a captured value, not a confirmed default.
- Its community `ref_rva` is `0x100E2E40`. The address scan found nine direct memory comparisons against that reference in game code, plus three direct-memory writes to the companion `obj_rva=0x100E2E90`. It also found one address-taking instruction for the reference and one for the object address; neither is a value read. Confirm the scan and executable details in the [source notes](EVIDENCE.md#build-specific-static-analysis).

## Observed code path

At `0x146A6CE70`, a shared helper first rejects null or flagged inputs, resolves another object, and rejects that object if its flags match mask `0x60000000`. It then checks this CVar. When enabled, it continues through object/state checks and appends a pointer to a dynamically managed array; the visible append updates the array count and writes an eight-byte item. When disabled, this helper returns without taking that path.

Several callers branch on the same reference before invoking the helper. For example:

- At `0x146466136`, a nonzero value enters object/container checks and can call `0x146A6CE70`; the zero path calls `0x1436C4940` with a mode argument of `1` instead.
- At `0x146A84ABB`, a nonzero value attempts actor/object resolution and calls the shared helper when the required objects are available; the alternate branch calls `0x1436C4940`.
- At `0x146B583BA`, zero jumps to the fallback path and nonzero continues through object checks toward the shared helper.
- At `0x146B49926`, the CVar is compared with a local byte; equality takes the fallback path, while inequality enters the object-check/helper path. This site therefore combines the CVar with per-item state rather than acting as a plain unconditional toggle.

Together these sites show a real branch between a common object-processing path and a helper path that can append eligible objects to a list. The CVar name is consistent with actor destruction being involved, but the inspected instructions do not identify the list's consumer, its timing, or whether list insertion itself destroys an actor.

## Limits

This is static evidence from build 1.1.4042190, not a controlled in-game comparison. Exact source types, caller names, list purpose, frame scheduling, performance impact, safe values, and whether the user's loader accepts this setting remain unknown. The CVar remains in the unresolved-definition catalog until those semantics are recovered.
