# AssetValidation CVar batch A

This focused guide covers the nine currently uncovered exact-case `AssetValidation.*` variable rows. Their supplied help describes an asset-validation feature, including camera validation throttles and mismatch handling. Registry presence does not establish runtime registration or loader editability.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 | Meaning from supplied help and uncertainty | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `AssetValidation.Camera.ClientDrainInterval` | `float` (`var`) | 1 | — | Seconds between client drain reports after an asset-load flush leaves pending entries. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Camera.ClientMaxPendingEntries` | `int32` (`var`) | 64 | — | Maximum camera assets retained in the client pending queue. Each report contains at most 2 entries. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Camera.MaxPendingTasksGlobal` | `int32` (`var`) | 64 | — | Maximum accepted camera validation reports pending in a world. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Camera.MaxPendingTasksPerUID` | `int32` (`var`) | 4 | — | Maximum accepted camera validation reports pending per UID. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Camera.ServerBaselinePropertiesPerFrame` | `int32` (`var`) | 64 | — | Maximum camera properties captured for server baselines per frame. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Camera.ServerMaxEntriesPerFrame` | `int32` (`var`) | 16 | — | Maximum camera property and curve digest comparisons per server frame after baseline completion. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.Enable` | `int32` (`var`) | 1 | — | Enable asset validation. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.ModeList` | `FString` (`var`) | — | — | Comma-separated EGameModeType_Behavior allowlist; empty means all. The snapshot contains no value for this entry. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |
| `AssetValidation.StopAfterFirstMismatch` | `int32` (`var`) | 1 | — | Stop validation for a UID after its first mismatch. | Name appears in both scanned Shipping executable string inventories; `4` `obj_rva` address-reference scan hits (3 direct-memory candidates, 1 address-taken). Static candidates only; no validated reads or writes. |

## Evidence limits

- `console_vars.tsv` reports all nine as `var` rows with help text; this is community-supplied registry evidence, and its capture build is unknown.
- Snapshot values come from `CVarDump.txt`; they are observations, not documented defaults. `AssetValidation.ModeList` is absent from that snapshot.
- No exact-name UE 5.9 reference match was found for these nine names. This does not identify the game’s engine version.
- The build inventory records printable name presence in scanned Shipping binaries. Static address-reference hits target `obj_rva` candidate locations only; they do not verify registration, code use, or runtime effects.
- No controlled test established whether the loader accepts these through `[Overrides]`, whether they are mutable in Shipping, or how they affect Marvel Rivals.

Sources: [community CVar registry](cvar-community-registry.md), [preserved source attachments](EVIDENCE.md#community-sources), [raw registry](EVIDENCE.md#community-sources), [snapshot](EVIDENCE.md#community-sources), [build CVar string inventory](EVIDENCE.md#build-specific-static-analysis), and [static address-reference scan](EVIDENCE.md#build-specific-static-analysis).
