# OSSNull CVar batch A

This guide covers all eight currently uncovered exact-case `OSSNull.*` registry rows. Their supplied help describes the Unreal “Null” online subsystem’s login, identity, offline, and external-UI options. The shared references are useful for understanding the names, but do not prove that Marvel Rivals uses these settings in a live account flow or accepts them from the mod loader.

| Exact name | Type / kind | Snapshot | Epic UE 5.9 | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- | --- |
| `OSSNull.AddUserNumToNullId` | `bool` (`ref`) | false | false | True if login name should include the local user number, which allows different stable Ids per user num | Name appears in both scanned Shipping executable string inventories; `3` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.AutoLoginAtStartup` | `bool` (`ref`) | true | true | True if it should login the first user at startup like single-user platforms, false to only login when requested | Name appears in both scanned Shipping executable string inventories; `3` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.ForceOfflineMode` | `bool` (`ref`) | false | false | True if it should fail faked network queries and act like an offline system | Name appears in both scanned Shipping executable string inventories; `4` `ref_rva` and `3` `obj_rva` scan hits (4 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.ForceShowLoginUIUserChange` | `bool` (`ref`) | false | false | True if the user index should change during login UI to emulate a platform user change | Name appears in both scanned Shipping executable string inventories; `3` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.ForceStableNullId` | `bool` (`ref`) | false | false | True if it should use a system-stable null Id for login, same as -StableNullID on command line | Name appears in both scanned Shipping executable string inventories; `4` `ref_rva` and `3` `obj_rva` scan hits (4 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.RequireLoginCredentials` | `bool` (`ref`) | false | false | True if login should require a user/pass to act like an external service, false to match most platforms and use the default | Name appears in both scanned Shipping executable string inventories; `4` `ref_rva` and `3` `obj_rva` scan hits (4 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.RequireShowLoginUI` | `bool` (`ref`) | false | false | True if login requires calling ShowLoginUI on the externalUI, depends on SupportExternalUI | Name appears in both scanned Shipping executable string inventories; `3` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 3 address-taken), unvalidated. |
| `OSSNull.SupportExternalUI` | `bool` (`ref`) | false | false | True if it should support an external UI interface | Name appears in both scanned Shipping executable string inventories; `3` `ref_rva` and `3` `obj_rva` scan hits (3 direct-memory candidates, 3 address-taken), unvalidated. |

## Evidence limits

- The community registry marks all eight entries as `ref`, not `var`; registration, mutability, and `[Overrides]` acceptance are unverified.
- The Epic UE 5.9 descriptions/defaults are exact-name reference matches. They explain the underlying Null subsystem options, but do not establish that the game uses this implementation or that the UE 5.9 default is the game default.
- `CVarDump.txt` values are captured snapshot values, not recommendations. The snapshot and Epic reference agree for these entries; that agreement is not runtime verification.
- Printable strings and address-reference scan hits do not prove that the variables are registered, read, written, or used in live Marvel Rivals flows.
- Avoid treating `ForceOfflineMode` or the login/UI flags as safe gameplay tweaks: available evidence documents their intended offline/login semantics but does not establish live-game consequences.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [community source notes](EVIDENCE.md#community-sources), [community source notes](EVIDENCE.md#community-sources), [community source notes](EVIDENCE.md#community-sources), [build-specific static-analysis notes](EVIDENCE.md#build-specific-static-analysis), and [static address-reference scan](EVIDENCE.md#build-specific-static-analysis).
