# Control Rig CVar batch A

The five exact-case `ControlRig.*` variables cover curve debugging, rig execution in animation nodes and components, debug drawing during play, and a Marvel-specific initialization option.

| Exact name | Registry type / kind | Snapshot | Meaning from supplied help |
| --- | --- | --- | --- |
| `ControlRig.CreateFloatControlsForCurves` | `int32` / `var` | `0` | A nonzero value creates a float control for each curve in the curve container for low-level debugging. |
| `ControlRig.DisableExecutionInAnimNode` | `int32` / `var` | `0` | A nonzero value disables Control Rig execution inside an animation node. |
| `ControlRig.DisableExecutionInComponent` | `int32` / `var` | `0` | A nonzero value disables Control Rig execution inside a `ControlRigComponent`. |
| `ControlRig.EnableDrawInterfaceInGame` | `float` / `var` | `0` | A nonzero value enables debug drawing during play. The help leaves the drawing content and display conditions unspecified. |
| `ControlRig.EnableMarvelOptimizeSkipInitial` | `bool` / `ref` | `true` | Enables skipping Control Rig initialization. The help leaves the eligibility rules and the initialization work affected unspecified. |

## Build and snapshot evidence

- All five names appear in the x64 and ARM64EC Shipping string inventories for build 1.1.4042190. The x64 address scan records three direct-memory candidates and one address-taking instruction targeting `obj_rva` for each name. `ControlRig.EnableMarvelOptimizeSkipInitial` also has two direct-memory candidates and one address-taking instruction targeting `ref_rva`. These matches leave the runtime paths and initialization behavior unverified. [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Address-reference data](EVIDENCE.md#build-specific-static-analysis)
- The source registry and snapshot have unspecified capture builds. The captured values have no established relationship to game defaults or overrides. The local Epic UE 5.9 reference cross-check has no exact-name match for these five entries. Shipping runtime effects and startup override support remain unverified. [Community registry](EVIDENCE.md#community-sources) · [Raw registry](EVIDENCE.md#community-sources) · [Raw snapshot](EVIDENCE.md#community-sources) · [Source notes](EVIDENCE.md#community-sources)
