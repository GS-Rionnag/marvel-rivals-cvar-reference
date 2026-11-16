# Joystick CVar batch B

This guide closes the three `Joystick.*` names not covered in the first joystick guide. Community help text, the captured snapshot, and the build-specific address scan are separate evidence. The source registry does not establish build alignment or `.ini` acceptance.

Translations are assistant renderings and have not been independently reviewed. Direct-memory candidates are scanner classifications only; they do not establish read/write direction or runtime execution.

| Exact CVar | Type / kind | Snapshot | Supplied help and translation | Build scan evidence and limits |
| --- | --- | --- | --- | --- |
| `Joystick.StickSensitivityUpperLimit` | float (`var`) | 0.5 | Community help: 右摇杆水平/垂直灵敏度上限. (Default: 0.5) Object-table help: /       . (Default: 0.5) Unreviewed assistant translation: Upper limit for right-stick horizontal/vertical sensitivity. (Default: 0.5) | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime effect and override acceptance unverified. |
| `Joystick.VerticalAngularSpeedAcceleration` | float (`var`) | 100 | Community help: 垂直角速度加速度. (Default: 100.0) Object-table help: . (Default: 100.0) Unreviewed assistant translation: Vertical angular-speed acceleration. (Default: 100.0) | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime effect and override acceptance unverified. |
| `Joystick.VerticalRotationAngularSpeed` | float (`var`) | -4 | Community help: 视角垂直转动标准角速度. (Default: -4.0) Object-table help: . (Default: -4.0) Unreviewed assistant translation: Standard vertical angular speed for camera rotation. (Default: -4.0) | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime effect and override acceptance unverified. |

## Interpretation limits

- Captured values are observations, not defaults or recommendations. The help text’s stated defaults remain part of that source text.
- Address-reference matches do not establish variable read/write behavior, execution, or gameplay impact.

Sources: [community CVar registry](cvar-community-registry.md), [Chinese help translations](cvar-chinese-help-translations.md), [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis), and [build-specific candidate inventory](EVIDENCE.md#build-specific-static-analysis).
