# Trace manager overlap and blind-logic CVars

This note covers two undocumented booleans from the `TraceMgr` namespace in build 1.1.4042190. The names suggest intent, while the instructions below describe only the observed code paths.

## Registry evidence

| CVar | Type | `ref_rva` | Community help | Snapshot |
|---|---|---:|---|---|
| `TraceMgr.CVar_IgnoreTestOverlapHit` | bool | `0x100AA530` | blank | no row |
| `TraceMgr.CVar_IgnoreBlindlLogic` | bool | `0x100AA532` | blank | no row |

The registry's spelling is `BlindlLogic` (with an `l` before `Logic`). Do not silently normalize it when overriding the key. The repository's [address-hit TSV](EVIDENCE.md#evidence-artifacts-not-included) contains seven direct reads of `CVar_IgnoreTestOverlapHit` and four direct references of `CVar_IgnoreBlindlLogic` (one is in a setup routine).

## `TraceMgr.CVar_IgnoreTestOverlapHit`

At `0x146368E06`, the code checks a per-record count and then compares this CVar with zero. A nonzero value skips the following loop, which performs vector math over records with a `0x210`-byte stride. In two other loops:

- At `0x14636B2A0`, nonzero exits the current iteration before a virtual call at offset `0x3B0`, reading a byte at record offset `0x26D4`, and subsequent item processing.
- At `0x14636D637`, nonzero branches past another virtual call at offset `0x3B0` and the associated `0x26D4` byte read.
- At `0x14636D9A2`, nonzero jumps past a block of vector arithmetic and per-record geometry work.

This supports a limited reading that setting the CVar true skips some test/overlap-record handling. The code does not identify which overlap categories those records represent, and the same namespace flag participates in more than one routine. It is not evidence that all overlap hits, collision, or damage are disabled.

## `TraceMgr.CVar_IgnoreBlindlLogic`

At `0x146359079`, the CVar is compared with zero. Nonzero branches to `0x14635941C`, skipping a large block that otherwise begins with checks of fields at offsets `0x9E9` and `0x1018`, followed by additional work. The binary gives no source-level name for that block, so “blind logic” remains a name-based interpretation.

A setup routine reads the three adjacent `TraceMgr.CVar_Ignore*` bytes into fields at offsets `0xB5` through `0xB7` of a record (`0x1494684E5`–`0x1494684FF`). Later in the same routine, nonzero object flags at offsets `0x360`, `0x530`, or `0x531` set the corresponding `IgnoreTestOverlapHit`, `IgnorePortalLogic`, or `IgnoreBlindlLogic` global byte to `1` (`0x1494685B6`–`0x1494685E2`). This is observed value flow; the owning record and the scope or timing of this setup are not fully recovered.

## Limits for overrides

Neither CVar has a captured snapshot value or community help. The static branches show that nonzero values skip particular code blocks, but they do not establish safe values, match behavior, or performance effects. Do not infer that these switches are harmless just because their names say “Ignore.” See the separate [`TraceMgr.CVar_IgnorePortalLogic` trace](cvar-tracemgr-ignore-portal-logic.md) for its other direct-read paths.
