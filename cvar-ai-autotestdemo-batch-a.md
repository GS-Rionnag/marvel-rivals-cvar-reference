# AIAutoTestDemo CVar batch A

This guide covers all six currently uncovered exact-case `AIAutoTestDemo.*` `var` entries. The namespace suggests an AI automated-test demo or harness, but no supplied evidence explains the broader subsystem or whether these settings are reachable in ordinary matches. Only `CompressJson` has supplied help; the rest are described as name-based hypotheses.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help or name | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `AIAutoTestDemo.AlwaysExportInputData` | `int32` (`var`) | `0` | No help supplied. The name suggests controlling whether input data is always exported; accepted values and export format are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `AIAutoTestDemo.CompressJson` | `bool` (`var`) | `false` | Whether to gzip-compress the output JSON file. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `AIAutoTestDemo.NextSessionTime` | `float` (`var`) | `1` | No help supplied. The name suggests a time value associated with a next session; unit and exact behavior are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `AIAutoTestDemo.PlayTimeRate` | `float` (`var`) | `1` | No help supplied. The name suggests a playback-time rate or multiplier, but the subject, scale, and accepted range are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `AIAutoTestDemo.RawData` | `int32` (`var`) | `0` | No help supplied. The name suggests selecting raw-data output or handling; format and value semantics are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `AIAutoTestDemo.ShutDownTime` | `float` (`var`) | `3` | No help supplied. The name suggests a shutdown timing value; unit and triggering event are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |

## Interpretation and limits

- The automated-test/demo association comes from the namespace name, not confirmed runtime context. The registry does not say whether the code is active in the shipped build or exposed during normal gameplay.
- Snapshot values are captured observations, not verified defaults or recommendations. Values such as `1` and `3` do not establish units or multiplier semantics.
- Static scan hits are direct-memory/address-taking candidates only. They do not prove runtime use, execution, registration, or visible effects.
- A `var` classification does not establish that Marvel Rivals accepts startup `.ini` overrides for these names.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
