# Graphics candidates from Epic documentation and Shipping strings

Five exact graphics names appear in the preserved Epic UE 5.9 comparison and as literal strings in both the x64 and ARM64EC Shipping executables for build 1.1.4042190. These names are absent from the community variable registry, object table, and value snapshot. The table describes Epic’s upstream settings. The Shipping evidence leaves their registration, availability, and configuration behavior in Marvel Rivals unknown.

| Exact name | Epic UE 5.9 default | Upstream purpose |
| --- | --- | --- |
| `r.BufferVisualizationOverviewTargets` | Empty string | Selects the post-process materials shown in the Buffer Visualization overview. Epic describes a comma-separated list, with empty entries leaving gaps in the overview. |
| `r.BufferVisualizationTarget` | Empty string | Selects the channel when the viewport is already in Buffer Visualization mode. Epic lists channels such as `BaseColor`, `Roughness`, `WorldNormal`, and `Velocity`. |
| `r.GPUStatsMaxQueriesPerFrame` | `8192` | Caps GPU timing timestamp allocations per frame. Epic describes `-1` as unlimited. |
| `r.ShowMaterialDrawEvents` | `0` | Emits a draw event with asset information around every mesh draw call when enabled. Epic describes substantial CPU and GPU overhead when collecting these events. |
| `r.VelocityTest` | `0` | Runs a velocity-rendering diagnostic. Epic describes `1` as adding random data to the skeletal mesh bone-data buffer for testing the velocity path used by object motion blur and temporal antialiasing. |

The [preserved Epic comparison and module inventory](cvar-engine-reference-only.md) records the exact names, defaults, and binary hits. The [community source inventory](EVIDENCE.md#community-sources) identifies the three inputs checked for exact-name absence.
