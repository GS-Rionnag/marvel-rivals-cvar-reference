# Graphics candidates in the console object table and Epic reference

These 14 exact names appear in both the community console-object table and the preserved Epic UE 5.9 comparison. All 14 literal names also appear in the x64 and ARM64EC Shipping 1.1.4042190 executables. Each lacks a `var` or `ref` registry row and a captured value. The evidence supports the described engine purpose and leaves Marvel Rivals runtime availability and configuration acceptance unresolved.

## Visualization and anti-aliasing

| Exact name | Object flags | Epic 5.9 default | Meaning and source differences |
| --- | ---: | --- | --- |
| `r.Lumen.Visualize.ViewMode` | 1 | Empty string | Selects the channel in Lumen Visualization view. Both help texts name `Overview`, `LumenScene`, `GeometryNormals`, `ReflectionView`, and `SurfaceCache`. Epic also lists two channels absent from the object help. |
| `r.Nanite.Visualize` | 1 | Empty string | Selects a channel in Nanite Visualization view. Both sources list channels such as `Triangles`, `Clusters`, `Overdraw`, and `MaterialID`. The object help ends mid-list. |
| `r.Nanite.VisualizeOverview` | 0 | Comma-separated preset | Controls the tiles in Nanite’s visualization overview. Both sources describe empty positions between commas as gaps. Epic’s preset includes `Triangles`, `Clusters`, `Instances`, `Primitives`, `Overdraw`, `MaterialID`, `RasterBins`, and `EvaluateWPO`. |
| `r.Shadow.Virtual.Visualize` | 1 | Empty string | Selects a channel in Virtual Shadow Map Visualization view. Both sources name `mask`, `mip`, `vpage`, `cache`, and `raycount`, among others. Epic also lists `naniteoverdraw`, which the object help omits. |
| `ShowFlag.AntiAliasing` | 1 | `2` | Overrides the anti-aliasing show flag. Both help texts describe `0` as forced off, `1` as forced on, and `2` as leaving the flag under normal control. |

## Graphics task scheduling

Both sources describe a three-character setting. The first character sets thread priority (`h`, `n`, or `b` for high, normal, or background). The second sets task priority (`h` or `n`), and the third sets task priority if execution is forced onto a normal-priority thread (`h` or `n`). The defaults below are Epic reference values.

| Exact name | Object flags | Epic 5.9 default | Work described by both sources |
| --- | ---: | --- | --- |
| `fx.Niagara.TaskPriorities.Background` | 0 | `bnn` | Niagara’s background priority class. |
| `fx.Niagara.TaskPriorities.High` | 0 | `hnn` | Niagara’s high priority class. |
| `fx.Niagara.TaskPriorities.Low` | 0 | `nnn` | Niagara’s low priority class. |
| `fx.Niagara.TaskPriorities.Normal` | 0 | `hnn` | Niagara’s normal priority class. |
| `TaskGraph.TaskPriorities.GatherShadowPrimitives` | 0 | `hnn` | Shadow primitive gathering. |
| `TaskGraph.TaskPriorities.ParallelTranslateCommandList` | 0 | `nnn` | Parallel command-list translation. |
| `TaskGraph.TaskPriorities.ParallelTranslateCommandListPrepass` | 0 | `nnn` | Parallel command-list translation for the render prepass. |
| `TaskGraph.TaskPriorities.RHIThreadOnTaskThreads` | 0 | `nnn` | Render Hardware Interface tasks when scheduled on task threads. |
| `TaskGraph.TaskPriorities.SceneRenderingTask` | 0 | `nnn` | Various scene rendering tasks. |

Object flags are transcribed as source metadata. The available evidence leaves flag interpretation, mutability, and scheduling effects unresolved. See the [community console-object catalog](cvar-community-console-objects.md) and the [preserved Epic comparison and binary evidence](cvar-engine-reference-only.md).
