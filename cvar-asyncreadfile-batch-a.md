# AsyncReadFile CVar batch A

This note documents the currently uncovered `AsyncReadFile.CacheHandleForPakFilesOnly` registry entry. Its supplied help controls which files' underlying platform handles are cached by the async read handle: `0` caches handles for all files; `1` caches handles for `.pak` files only, which the help calls the default. This describes file I/O resource handling; the registry does not quantify effects on memory, performance, or loading.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 static evidence |
| --- | --- | --- | --- | --- | --- |
| `AsyncReadFile.CacheHandleForPakFilesOnly` | `int32` (`ref`) | `1` | — | `0`: cache the underlying platform handles for all files. `1`: cache them only for `.pak` files (described as the default in supplied help). Other values are not explained. | Name appears in both scanned Marvel Shipping executable inventories and CrashReportClient; 2 `ref_rva` hits (1 direct-memory candidate, 1 address-taken) and 3 `obj_rva` hits (2 direct-memory candidates, 1 address-taken), unvalidated. |

## Interpretation and limits

- “Default” here is wording in the supplied help. The captured `1` is a snapshot observation, not independent proof of the live game's default.
- The source does not define how the setting interacts with asynchronous request lifetime, non-pak containers, or handle eviction.
- Static address matches do not prove runtime reads, writes, execution, registration in the running build, or acceptance of a startup `.ini` override. No load-time or performance comparison has been performed.

Sources: [community CVar registry](EVIDENCE.md#community-sources), [build 1.1.4042190 inventory](EVIDENCE.md#build-specific-static-analysis), and [static-analysis source notes](EVIDENCE.md#build-specific-static-analysis).
