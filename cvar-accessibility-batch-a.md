# Accessibility CVar batch A

This guide records the currently uncovered `Accessibility.Enable` registry entry. Its supplied help describes Unreal's accessible-API query path: when false, queries from accessible APIs are ignored. The text does not identify which accessibility APIs or features Marvel Rivals uses, so this cannot be read as a general accessibility on/off switch.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `Accessibility.Enable` | `bool` (`ref`) | `false` | — | If false, queries from accessible APIs are ignored. Supplied help notes that some platforms require an application restart for the change to take effect. The API set and affected game features are unspecified. | Name appears in Marvel Shipping, Marvel Shipping ARM64EC, and CrashReportClient string inventories; 3 `ref_rva` hits (2 direct-memory candidates, 1 address-taken) and 1 `obj_rva` direct-memory candidate, unvalidated. |

## Interpretation and limits

- This wording concerns queries from accessible APIs. It does not establish that setting false disables all accessibility features, menus, input support, or assistive technology in Marvel Rivals.
- The captured `false` value is a snapshot observation, not a guaranteed default or recommendation.
- Static address matches do not prove runtime use, registration in the running build, or acceptance of a startup `.ini` override. The restart note is supplied help, not a tested result for this game.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
