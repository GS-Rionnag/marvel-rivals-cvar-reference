# `geometry.*` CVar batch A

The lowercase `geometry.*` registry family contains six variables and one Editor command. The supplied help covers Dynamic Mesh duplication, pooling, and debugging, plus grid limits in Geometry Script and threading in Mesh Scene Adapter. [Geometry Cache animation settings](cvar-geometrycache-batch-a.md) have their own namespace.

| Exact name | Registry type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 string inventory |
| --- | --- | --- | --- | --- |
| `geometry.DynamicMesh.DupeStashTimeout` | `int32` / `var` | `300` | Timeout in seconds for references held by the internal `UDynamicMesh` duplication helper, identified as `FDynamicMeshCopyHelper`. | x64 and ARM64EC |
| `geometry.DynamicMesh.EnableDebugMeshes` | `bool` / `var` | `false` | Toggles global debug mesh support for `FDynamicMesh3`. The help describes the support as Editor-only. | x64 and ARM64EC |
| `geometry.DynamicMesh.MaxPoolSize` | `int32` / `var` | `1000` | Maximum number of meshes a `UDynamicMeshPool` allows before running garbage collection. The help describes the pool’s threshold. | x64 and ARM64EC |
| `geometry.DynamicMesh.TextBasedDupeTriThreshold` | `int32` / `var` | `1000` | Triangle-count threshold for Base64 text duplication of `UDynamicMesh`. The help warns that large values are slow and leaves the exact boundary behavior unspecified. | ARM64EC |
| `geometry.GeometryScript.AllowUnclampedGridDimensions` | `bool` / `var` | `false` | Allows Geometry Script grid-based operations to bypass grid-dimension clamping. The help leaves clamp limits and affected operations unspecified. | x64 and ARM64EC |
| `geometry.MeshSceneAdapter.SingleThreaded` | `int32` / `var` | `0` | Controls multithreading in Mesh Scene Adapter. The name suggests a single-threaded override, but the help gives no value mapping. | x64 and ARM64EC |
| `geometry.DynamicMesh.ClearDebugMeshes` | `cmd` | — | Discards meshes in the global `FDynamicMesh3` debug mesh set. The help says the command works only in the Editor. | x64 and ARM64EC |

## Evidence limits

- The snapshot records six captured values. The capture build and the relationship of these values to defaults or overrides are unknown. The local Epic UE 5.9 cross-check has no exact-name match for the six variables. [Community registry](EVIDENCE.md#community-sources) · [Raw snapshot](EVIDENCE.md#community-sources) · [Registry source notes](EVIDENCE.md#community-sources)
- Each of the seven names has three direct-memory candidates and one address-taking instruction targeting `obj_rva` in the x64 executable scan. There are no `ref_rva` hits. For `TextBasedDupeTriThreshold`, the x64 scan matched the address supplied by the registry, while the string inventory lists the name only in ARM64EC. An address match alone leaves the link between that name and the x64 code unverified. [Address-reference data](EVIDENCE.md#build-specific-static-analysis) · [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Command string inventory](EVIDENCE.md#build-specific-static-analysis)
- Runtime registration, execution in Marvel Rivals, and startup override support remain unverified. For the debug mesh variable and command, the supplied help explicitly limits functionality to the Editor. [Raw registry](EVIDENCE.md#community-sources)
