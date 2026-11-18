# WindowsCursor CVar batch A

This guide documents the currently uncovered `WindowsCursor.UseInvisibleCursorForNoneCursorType` registry entry. Its supplied help describes the native Windows cursor representation used when the engine cursor type is `None`: enabled means assigning a transparent cursor handle instead of a null handle. This describes a platform cursor fallback detail, not a general cursor-visibility control.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `WindowsCursor.UseInvisibleCursorForNoneCursorType` | `bool` (`ref`) | `false` | — | If enabled, sets the platform `HCursor` to a transparent cursor rather than null when the mouse cursor type is `None`. The help does not specify OS-level consequences of a null handle or behavior on non-Windows platforms. | Name appears in both scanned Marvel Shipping executable inventories and CrashReportClient; 2 `ref_rva` hits (1 direct-memory candidate, 1 address-taken) and 3 `obj_rva` hits (2 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- “Transparent cursor” and “null” are the distinction made in supplied help. The source does not establish when the engine chooses `None` or whether this setting changes visible cursor behavior in Marvel Rivals.
- Snapshot `false` is an observation, not a guaranteed default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or startup `.ini` acceptance. No cursor behavior has been tested with this override.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
