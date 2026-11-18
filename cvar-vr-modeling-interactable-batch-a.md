# VR, Modeling, and InteractableActor CVar batch A

This guide covers the 15 currently uncovered exact-case entries under `vr.*`, `modeling.*`, and `InteractableActor.*` (five from each namespace). Their supplied help describes engine VR rendering/input options, Unreal Modeling Tools settings, and simulated interactable-actor behavior. Registry membership, snapshots, and static scan candidates do not establish that these options are exposed or useful to Marvel Rivals players.

## `vr.*`

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `vr.AllowMotionBlurInVR` | `int32` (`var`) | `0` | For projects with motion blur enabled, allows motion blur to remain enabled while in VR. The help does not define nonzero values beyond that intent. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `vr.EnableMotionControllerLateUpdate` | `int32` (`var`) | `1` | Enables (`1`) or disables (`0`) applying motion-controller late update. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `vr.InstancedStereo` | `int32` (`var`) | `0` | `0` disables and `1` enables instanced stereo, according to supplied help. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `vr.MobileMultiView` | `int32` (`var`) | `0` | `0` disables and `1` enables mobile multi-view, according to supplied help. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `vr.RoundRobinOcclusion` | `int32` (`var`) | `0` | `0` disables and `1` enables round-robin occlusion queries for stereo rendering, according to supplied help. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |

These entries describe VR/stereo rendering or controller paths. Their presence in the scanned binaries does not prove that Marvel Rivals supports a VR play mode or that toggling them affects normal desktop rendering.

## `modeling.*`

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `modeling.CreateMesh.IgnoreProjectSettings` | `bool` (`var`) | `false` | When enabled, new mesh objects do not use the preferences in Modeling Tools’ Project Settings. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `modeling.EnableVolumeSnapping` | `bool` (`var`) | `false` | Enables snapping to volumes. The help gives no details about supported volume types or snapping behavior. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `modeling.PolyEdit.EdgeLimit` | `int32` (`var`) | `60000` | Maximum number of edges supported by PolyEd and TriEd. Meshes exceeding the limit disable the tools to avoid editor hangs. | 2 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `modeling.Selection.FullHoverHighlights` | `int32` (`var`) | `0` | Selects full hover highlights instead of simplified highlights. The help does not define integer values. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `modeling.WorldRenderCapture.VTWarmupFrames` | `int32` (`var`) | `5` | Number of frames to render before each capture to warm up the virtual texture (VT). | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |

The supplied descriptions name Modeling Tools, PolyEd/TriEd, and project settings, indicating tool/editor-oriented functionality. This does not prove those tools are present in the retail game or that the settings affect rendered gameplay.

## `InteractableActor.*`

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help or name | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `InteractableActor.EnableDebug` | `bool` (`ref`) | `false` | No help supplied. The name suggests a debug toggle; what is logged or visualized is unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `InteractableActor.EnableDelayDeactivate` | `bool` (`var`) | `true` | Enables delayed deactivation of an interactable actor. Delay duration and triggering conditions are unspecified. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InteractableActor.EnableInteractorPhysicsOptimize` | `bool` (`var`) | `true` | Enables the feature named `InteractorPhysicsOptimize`; the supplied help does not explain its mechanism or tradeoffs. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `InteractableActor.MaxSimulatingNum` | `int32` (`ref`) | `50` | Maximum number of simulating interactable actors. The help does not describe how additional actors are selected or handled. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `InteractableActor.ResetFrameLimitTime` | `float` (`ref`) | `0.002` | Frame-limit time when resetting interactable actors. The help does not specify the unit or exact reset operation. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- All 15 entries appear in the captured `CVarDump.txt`; values above are observations, not verified defaults or recommendations.
- Supplied help is transcribed in meaning, but does not demonstrate actual runtime behavior, accepted value ranges beyond explicitly stated choices, or applicability to player-controlled matches.
- Binary address-reference counts are static candidates, not proof of executed reads/writes, runtime registration, config loading, or a visible effect.
- `var`/`ref` classification is not proof that a startup `.ini` override will be honored by Marvel Rivals.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
