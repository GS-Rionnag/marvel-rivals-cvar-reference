# Signed-distance-field device and update-pool CVars

The community dump has no help text for these two references. The installed build shows a direct device-eligibility gate for `r.SDF.EnableForIntegratedDevice` and two branches using `r.DistanceFields.GlobalSDFUpdatePoolEnable`. The latter's name identifies its subsystem, but the surrounding data structures are not recovered well enough to describe the pool's exact behavior.

## Variables

| CVar | Type | Snapshot | Observed build behavior | Limits |
|---|---|---:|---|---|
| `r.SDF.EnableForIntegratedDevice` | bool | `true` | At `0x141B726BF` and `0x141B81554`, zero immediately skips the remaining path (one caller clears a result flag; one helper returns false). A true value only allows later device and support checks to run; it does not by itself make the path eligible. | The complete caller context and the exact SDF capability checks are unresolved. The integrated-device scope is stated by the CVar name; no controlled hardware comparison was performed. |
| `r.DistanceFields.GlobalSDFUpdatePoolEnable` | int32 | `1` | At `0x141B83A63`, the code compares this setting with a current integer and skips a block when they are equal. At `0x141B83F23`, zero takes a shorter branch; a nonzero value reaches another integer comparison and additional update logic. This is consistent with a switch participating in global distance-field update-pool handling. | The compared fields, pool operations, and effect on rendered distance fields are not identified. The name-based interpretation is a lead; no runtime A/B test was performed. |

## Evidence

- Both community entries are `ref` rows with blank help in `console_vars.tsv` and blank help in `console_objects.tsv`.
- `CVarDump.txt` captures `r.SDF.EnableForIntegratedDevice = true` and `r.DistanceFields.GlobalSDFUpdatePoolEnable = 1`; these are not confirmed defaults.
- The full scanner records 2 direct `ref_rva` reads for `r.SDF.EnableForIntegratedDevice` and 2 for `r.DistanceFields.GlobalSDFUpdatePoolEnable`; the addresses are listed in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included).
- Build: Marvel Rivals `1.1.4042190` Shipping, SHA-256 `omitted from this documentation-only project`.

Both names remain in the [definition-gap worklist](cvar-unresolved-definitions.md). This note records what the current static trace supports, not a complete definition or tuning recommendation.
