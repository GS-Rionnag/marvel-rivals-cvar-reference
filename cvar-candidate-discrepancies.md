# Source discrepancies for graphics candidates outside the variable registry

These exact names appear in the community console-object table, the preserved Epic UE 5.9 comparison, and both Shipping executables for build 1.1.4042190. They have no exact `var` or `ref` registry row or captured snapshot value. The source differences leave game behavior and override acceptance unresolved.

| Exact name | Epic UE 5.9 | Community object evidence | What remains unknown |
| --- | --- | --- | --- |
| `r.ForceLOD` | Describes a forced level of detail, with `-1` disabling the override. | Flags `16777240`. The complete help text is `IAmNoRealVariable`. | The sources give different signals about the exact name. The object help could be a placeholder. Its text and the literal binary match leave registration, mutability, and the effect of `-1` unverified in Marvel Rivals. |
| `r.Lumen.Visualize.ViewMode` | Includes `PerformanceOverview` and `DedicatedReflectionRays` in the mode list. | Flags `1`. Lists five shared modes and omits those two modes. | Whether the game supports either additional mode. |
| `r.Nanite.Visualize` | Supplies a longer visualization channel list, including `Patches` and `PixelProgrammable`. | Flags `1`. Omits those two names from the visible list and ends mid-word at `MaterialZDe`. | Which channels the game implements and how much of the object help was cut off. |
| `r.Nanite.VisualizeOverview` | Supplies a longer list of overview modes, including `Patches` and `PixelProgrammable`. | Flags `0`. Omits those two names from the visible list and ends mid-word at `Hi`. | Which modes the game accepts and whether the visible differences reflect the object help or engine behavior. |
| `r.Shadow.Virtual.Visualize` | Includes `naniteoverdraw` as a Virtual Shadow Map visualization channel. | Flags `1`. Lists the other channels from the preserved Epic comparison and omits `naniteoverdraw`. | Whether that channel is available in the game build. |

The similar `skelot.ForceLOD` has its own registry row whose help mentions `r.ForceLOD`. That cross-reference identifies the comparison the help makes and leaves the exact `r.ForceLOD` name unresolved. Object flags are recorded as raw metadata.

Sources are the [community object catalog](cvar-community-console-objects.md), the [preserved Epic comparison and executable inventory](cvar-engine-reference-only.md), and the [registry attachments](EVIDENCE.md#community-sources).
