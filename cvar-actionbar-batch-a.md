# ActionBar CVar batch A

This guide documents the currently uncovered `ActionBar.IgnoreOptOut` registry entry. Its supplied help says that enabling it makes the Bound Action Bar display bindings even when those bindings are not configured with `bDisplayInReflector`. The help does not explain the Bound Action Bar's intended audience or whether this is a developer-facing or player-facing UI.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `ActionBar.IgnoreOptOut` | `bool` (`ref`) | `false` | — | When true, the Bound Action Bar displays bindings even when they are not configured for display in the reflector. The description implies an opt-out/display-filter bypass for this UI, but does not define other binding views or UI contexts. | Name appears in both scanned Marvel Shipping executable inventories; 2 `ref_rva` hits (1 direct-memory candidate, 1 address-taken) and 2 `obj_rva` hits (1 direct-memory candidate, 1 address-taken), unvalidated. |

## Interpretation and limits

- `bDisplayInReflector` is preserved from the supplied help. The registry does not specify how the game maps the Bound Action Bar to the reflector terminology.
- The captured `false` value is an observation, not a guaranteed default or recommendation.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or startup `.ini` acceptance. The exact visual or input effect has not been tested in game.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
