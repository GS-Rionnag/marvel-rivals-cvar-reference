# `scene.*` CVar batch A

This guide documents all seven exact-case `scene.*` references. Supplied help describes component-transform updates, navigation-data update delay, debug logging, and teleportation. The names do not establish which game situations invoke the settings or what players would observe if values changed.

Captured values are observations, not recommendations or verified defaults. No Epic UE 5.9 reference values were supplied. Static address-reference candidates from Shipping build 1.1.4042190 are not proof of runtime behavior or acceptance by the startup `.ini` loader.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `scene.DebugRemoteMeshTeleportationInDeath` | `bool` (`ref`) | `false` | Help says this enables debug output for remote-mesh teleportation in death. It does not specify the output channel or triggering conditions. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hit. |
| `scene.DebugRemoteTeleportation` | `bool` (`ref`) | `false` | Help says this enables remote-teleportation debugging. The exact telemetry and conditions are unspecified. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hit. |
| `scene.EnableUpdateComponentOptimization` | `bool` (`ref`) | `true` | When enabled, `UpdateComponentToWorld` may be skipped when it is not necessary. The help does not define how necessity is determined or all affected component types. | 1 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `scene.PrintUpdateComponentUpdate` | `bool` (`ref`) | `false` | Whether to print `UpdateComponentToWorld` activity. The destination and verbosity are not specified. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hit. |
| `scene.TeleportationDistance` | `float` (`ref`) | `1000` | Help only labels this “Teleportation Distance.” Units, threshold meaning, and the actors or operation it affects are unknown. | 3 `obj_rva` direct-memory candidates and 2 address-taken candidates; no `ref_rva` hit. |
| `scene.UseNewShouldUpdateComponentOpt` | `bool` (`ref`) | `true` | No help supplied. The name suggests an alternate `ShouldUpdateComponent` optimization, but the criteria and behavior are unknown. | 4 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |
| `scene.nav.EnableNavDataUpdateDelay` | `bool` (`ref`) | `true` | When enabled, `UpdateNavData` will be delayed. The help does not specify the delay duration, trigger, or affected navigation data. | 1 `ref_rva` and 3 `obj_rva` direct-memory candidates; 2 address-taken candidates. |

## Interpretation and limits

- Help summaries describe only the supplied text; they do not identify the exact live-game paths or user-visible outcome.
- Snapshot values are not confirmed defaults or recommendations for the installed build.
- Static hits may reflect initialization, writes, or address passing. They do not prove runtime execution or visible effects.
- Registry classification as `ref` does not prove that `[Overrides]` can change a value in Marvel Rivals.

## Sources

Names, types, help, and snapshot observations are in the [community CVar source notes](EVIDENCE.md#community-sources). Build and scanner limitations are described in [build-specific analysis notes](EVIDENCE.md#build-specific-static-analysis).
