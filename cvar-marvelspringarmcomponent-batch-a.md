# MarvelSpringArmComponent CVar batch A

This guide covers the eight currently uncovered exact-case `MarvelSpringArmComponent.*` `var` entries. Supplied help describes remote camera rotation, water-zone pitch constraints, animation update timing, adaptive interpolation, replay camera return, mesh rotation, and portal traces. The help is terse and occasionally inconsistent with the declared type, so the entries below preserve those uncertainties instead of guessing valid values.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 scan |
| --- | --- | --- | --- | --- |
| `MarvelSpringArmComponent.EnableRemoteDesiredRotationLerpCheck` | `bool` (`var`) | `true` | When enabled, the spring arm may set a remote desired rotation directly to its target without interpolation. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.EnableWaterSurfaceCameraConstraint` | `bool` (`var`) | `false` | Enables water-zone limits on spring-arm pitch before the camera enters the configured water surface. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.ForceUpdateCurveValue` | `bool` (`var`) | `false` | Forces an animation update immediately. The help warns this may stall the game thread while it waits for animation evaluation. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.InterpFixedValue` | `float` (`var`) | `0.05` | The help says this “if enable” uses adaptive interpolation, otherwise a fixed value. That wording sounds like a toggle despite the registry declaring a float; it does not define how the numeric value is used. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.ReplayCameraReturn` | `int32` (`var`) | `1` | During replay, selects a return interpolation/rotation path rather than using mesh rotation. The source phrase “return lerp rotation” is ambiguous, and it does not state accepted integer values. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.UseAdaptiveLerp` | `int32` (`var`) | `0` | Chooses adaptive interpolation when enabled and a fixed value otherwise. Although declared `int32`, help presents it as an enable/disable choice; valid nonzero values are unspecified. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.UseMeshRotationAsRemoteDesiredRotation` | `bool` (`var`) | `false` | Uses mesh rotation as the remote desired rotation when enabled. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |
| `MarvelSpringArmComponent.UsePortalTrace` | `bool` (`var`) | `true` | Enables portal tracing. The help gives no further details about trace behavior or cases where it applies. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`; no validated runtime use. |

## Interpretation and limits

- Snapshots are captured observations, not verified defaults or recommendations. The apparent true/false semantics in some `int32` help do not establish accepted ranges.
- Three address matches per name consist of two direct-memory candidates and one address-taking reference to the `obj_rva`. They are static scan candidates only; they do not prove runtime registration, reads, writes, execution, or visible camera behavior.
- The community registry classifies these as `var` entries, but that does not prove that a `[Overrides]` startup `.ini` line is accepted by Marvel Rivals.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
