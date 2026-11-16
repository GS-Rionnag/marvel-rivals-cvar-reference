# ProfileLibrary CVar batch A

This guide covers the 10 currently uncovered `ProfileLibrary.*` registry entries. Supplied descriptions point to cue/effect visibility filtering using camera-frustum and distance information, plus an effect-suppression setting for dueling. Several threshold names have no help, so their exact role remains unresolved. None has an exact-name Epic UE 5.9 CVar reference match.

Snapshot values are observations, not defaults. The static scan matches registry address fields against Shipping build 1.1.4042190; counts are candidates, not proof of reads, writes, execution, or config acceptance. No loader override or runtime test was performed.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `ProfileLibrary.CVarProfile_Distance_Frustum_Filter` | `bool` (`ref`) | `true` | — | No useful supplied help. The name suggests a distance/frustum filter switch, but its behavior and interaction with other profile settings are unverified. | `ref_rva`: 5 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Distance_Multiplier` | `float` (`ref`) | `1` | — | Supplied help: multiply all distance thresholds by this value; larger values mean more view distance and greater quality. The exact threshold set and response curve are unspecified. | `ref_rva`: 5 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Distance_Segment_Filter` | `bool` (`ref`) | `false` | — | Supplied help: whether to enable distance filtering by segment type, with `InstantAmmo` as an example. | `ref_rva`: 4 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Frustum_Distance` | `int32` (`ref`) | `4000` | — | No useful supplied help or exact-name Epic description; distance units, subject, and filter behavior remain unresolved. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Frustum_Distance_Segment` | `int32` (`ref`) | `4000` | — | No useful supplied help or exact-name Epic description; its relation to segment filtering is not defined. | `ref_rva`: 3 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Ignore_Minimum_Distance` | `bool` (`ref`) | `true` | — | Supplied help: whether to ignore the minimum distance. The help does not define how that setting interacts with `CVarProfile_Minimum_Distance`. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Maximum_CueRadius` | `int32` (`ref`) | `800` | — | Supplied help: if a cue's radius exceeds this value, it cannot be excluded. Units and the exact meaning of “excluded” are unspecified. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CVarProfile_Minimum_Distance` | `int32` (`ref`) | `500` | — | Supplied help: a point within this range cannot be excluded. Units and which point/cue-distance calculation are not specified. | `ref_rva`: no direct-memory candidate; 1 address-taking reference. `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.CameraFrustumFrameCache` | `bool` (`ref`) | `true` | — | Supplied help: cache the camera frustum once per frame for high-frequency cue-visibility filtering. | `ref_rva`: 2 direct-memory candidates and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |
| `ProfileLibrary.EnableEffectSuppressionForDueling` | `bool` (`ref`) | `false` | — | Supplied help: when true, suppress most types of cues and effects if the view target is dueling. Which effects, modes, or view targets qualify are not described. | `ref_rva`: 1 direct-memory candidate and 1 address-taking reference; `obj_rva`: 3 direct-memory candidates and 1 address-taking reference. |

## Interpretation limits

- The supplied descriptions identify visibility/cue filters and camera-frustum caching, but do not specify which cues are considered, whether filters run client-side, or how results affect network traffic and rendering.
- The names `Frustum_Distance` and `Frustum_Distance_Segment` lack unit/behavior help. Snapshot values `4000` do not define a safe or effective distance.
- The “cannot be excluded” descriptions for maximum cue radius and minimum distance imply filter exceptions, but do not define all filtering predicates or precedence.
- Nearby `ProfileLibrary.*` strings in the build-context inventory do not establish a call-flow relationship among these entries.
- The registry, static scan, and snapshots do not verify `.ini` acceptance or behavior in the installed game.

Sources: [community registry](cvar-community-registry.md), [build-specific name inventory](EVIDENCE.md#build-specific-static-analysis), [build-specific text context](EVIDENCE.md#build-specific-static-analysis), and [snapshot/address-reference scan provenance](EVIDENCE.md#community-sources).
