# Audio CVar batch B

This guide documents the final five registered names whose exact, case-sensitive first dotted component is `Audio`. Together with batch A, this closes the supplied `Audio.*` family at 30 of 30 unique registered `var`/`ref` names. The lowercase `au.*` namespace is distinct and is not included in this count.

“Snapshot” is the value captured in the supplied registry catalog, not a recommendation or assumed default. The Epic UE 5.9 column records exact-name upstream reference defaults; `—` means no match was recorded. English text derived from Chinese help is marked as an unreviewed assistant translation.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Meaning from supplied help (provenance) | Build 1.1.4042190 address evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Audio.MaxWeaponShootingFps` | int32 (`ref`) | `25` | — | Community help: “max weapon shooting fps.” It does not specify which weapon shots are limited or how the value is applied. | `ref_rva`: 2 direct-memory candidates, 1 address-taking hit; `obj_rva`: 3 direct-memory candidates, 1 address-taking hit. Direction and execution were not traced. |
| `Audio.OnlyLoadAbilityVoice` | bool (`ref`) | `false` | — | Community help: “only load ability voice or load all.” It states the alternatives but does not explicitly map each alternative to a bool value. | `ref_rva`: 1 direct-memory candidate, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. Direction and execution were not traced. |
| `Audio.ThreatValue.DisabledModeOverride` | int32 (`ref`) | — | — | Community help says this overrides the `DisabledModes` check for threat value: `0` follows the `DisabledModes` config; `1` forces disable. | `ref_rva`: 1 direct-memory candidate, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. Direction and execution were not traced. |
| `Audio.ThreatValue.TickInterval` | float (`ref`) | `0` | — | Community help says to set the threat-value tick interval. It does not specify units, clamps, or the meaning of snapshot `0`. | `ref_rva`: 1 direct-memory candidate, 1 address-taking hit; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. Direction and execution were not traced. |
| `Audio.VoiceRuntimeLanguageMode` | bool (`var`) | `true` | — | Original help is Chinese. The unreviewed assistant translation says when off any voice line may trigger; when on, Japanese voice settings require a line available in Chinese/Japanese/English, while Chinese settings require Chinese and English versions. Other language cases and the translation’s accuracy are not independently verified. | No `ref_rva` match; `obj_rva`: 2 direct-memory candidates, 1 address-taking hit. Runtime value consumption was not established. |

## Evidence limits and coverage audit

- The five entries each have one consistent registry row: four are `ref` (int32, bool, int32, float) and one is bool `var`. Four have captured snapshot values; `Audio.ThreatValue.DisabledModeOverride` has no captured value. No exact-name Epic UE 5.9 default is recorded for these five.
- Static scan totals are 16 `direct-memory-candidate` hits and 9 `address-taken` hits. A candidate may represent a read, write, comparison, or initialization; address-taking is not evidence of a value access. These matches do not prove execution, override acceptance, `.ini` editability, or live audio behavior.
- These five names do not overlap batch A or earlier local/public explanatory tables. Batches A and B cover all 30 exact-case `Audio.*` names, leaving zero uncovered. Lowercase `au.*` remains a separate namespace.

Sources: [community CVar registry](cvar-community-registry.md), [preserved registry and snapshot attachments](EVIDENCE.md#community-sources), and [build address-reference scan](EVIDENCE.md#build-specific-static-analysis).
