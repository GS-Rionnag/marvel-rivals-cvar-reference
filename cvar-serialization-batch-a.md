# Serialization CVar batch A

This guide covers all five currently uncovered exact-case `Serialization.*` `var` entries. Their supplied help refers to Unreal bulk-data sidecars, package trailers, offset repair, source-control syncing, and virtualized payloads. These descriptions concern asset/package serialization paths; the registry and static scan do not establish whether the settings are used during ordinary Marvel Rivals gameplay or only in tooling/content workflows.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `Serialization.AllowSidecarSyncing` | `bool` (`var`) | `false` | When true, `FEditorBulkData` may sync its `.upayload` sidecar through source control if the first load attempt from it fails. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `Serialization.ApplyBulkDataOffsetFix` | `bool` (`var`) | `true` | When true, attempts to repair potentially invalid bulk-data offsets. The help does not state which formats are supported or how repair is selected. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `Serialization.LoadFromSidecar` | `bool` (`var`) | `false` | When true, `FEditorBulkData` loads from its sidecar file. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `Serialization.LoadFromTrailer` | `bool` (`var`) | `false` | When true, loads payloads through the package trailer rather than the package itself. The help does not describe fallback behavior or precedence with sidecar loading. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `Serialization.RehydrateOnSave` | `bool` (`var`) | `false` | When true, virtualized `FVirtualizedUntypedBulkData` payloads are hydrated and stored locally when a package is saved. The help does not identify the package-writing workflows that use this. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |

## Interpretation and limits

- `FEditorBulkData` and `FVirtualizedUntypedBulkData` point to editor/package asset handling in the supplied help. Do not assume these settings alter graphics, gameplay, or runtime asset loading during a match.
- The snapshot values are captured observations, not verified defaults or recommendations. `ApplyBulkDataOffsetFix=true` does not establish that any fix is applied in the shipped game.
- Static scan hits are direct-memory/address-taking candidates only. They do not prove runtime execution, the affected serialization path, or acceptance from a startup `.ini` override.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
