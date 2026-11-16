# Crosshair CVar: `Crosshair.MakeRandomStream`

This focused note records the single uncovered `Crosshair.*` registry entry. The preserved community registry classifies it as a `ref int32`, but supplies no help text. Its name suggests a random-stream setting associated with crosshair behavior; that interpretation is only a naming inference, and its exact purpose, accepted values, and effect are unknown.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Supplied meaning | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- | --- |
| `Crosshair.MakeRandomStream` | `int32` (`ref`) | — | — | No help supplied. The name alone does not establish what is randomized or how a stream is selected. | Present in both scanned Shipping executable string inventories. The address scan reports one `ref_rva` direct-memory candidate, one `obj_rva` direct-memory candidate, and no address-taking candidates. Static hits do not prove CVar registration, runtime execution, loader acceptance, or visible effect. |

## Evidence limits

- No captured snapshot value or UE 5.9 reference default was recorded for this entry.
- The single direct-memory candidate per address family is consistent with data access but does not identify the consuming function or prove this setting controls crosshair visuals.
- Whether a `[Overrides]` `.ini` line changes it in Marvel Rivals remains unverified.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [captured values](EVIDENCE.md#community-sources), [build 1.1.4042190 static scan inventory](EVIDENCE.md#build-specific-static-analysis), and [research source notes](EVIDENCE.md#community-sources).
