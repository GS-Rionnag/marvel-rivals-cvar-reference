# Level CVar batch A

This guide covers all eight currently uncovered exact-case `Level.*` refs. Supplied material includes temporary timestamp strings and a client timed-GC switch. Three other entries have blank help; their likely scope comes only from their names and must not be treated as confirmed behavior. The English rendering of Chinese help is an assistant translation and has not been independently reviewed.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help or name | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `Level.IgnoreAbilitiesRuleOpt` | `bool` (`ref`) | `false` | No help supplied. The name suggests ignoring an abilities-rule optimization, but does not specify the rule, reason, or effect. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 8 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `Level.Optimize.DisableHitImpulseForMaps` | `FString` (`ref`) | — | No help supplied. The name suggests a map selection/list for disabling hit impulses. The expected string format and whether it applies to all impulses or a particular system are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 4 address-taking references to `ref_rva`. |
| `Level.Optimize.DisableRemoteDecalForMaps` | `FString` (`ref`) | — | No help supplied. The name suggests a map selection/list for disabling remote decals. The expected string format and meaning of “remote decal” are unknown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 4 address-taking references to `ref_rva`. |
| `Level.TempTime0` | `FString` (`ref`) | — | Supplied help labels this temporary level time 0 and gives the format `yyyy-mm-dd_HH:mm:ss`. Its purpose is not further described. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 2 address-taking references to `ref_rva`. |
| `Level.TempTime1` | `FString` (`ref`) | — | Supplied help labels this temporary level time 1 and gives the format `yyyy-mm-dd_HH:mm:ss`. Its purpose is not further described. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 2 address-taking references to `ref_rva`. |
| `Level.TempTime2` | `FString` (`ref`) | — | Supplied help labels this temporary level time 2 and gives the format `yyyy-mm-dd_HH:mm:ss`. Its purpose is not further described. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 2 address-taking references to `ref_rva`. |
| `Level.TempTime3` | `FString` (`ref`) | — | Supplied help labels this temporary level time 3 and gives the format `yyyy-mm-dd_HH:mm:ss`. Its purpose is not further described. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 2 address-taking references to `ref_rva`. |
| `Level.TimedGC.Enable` | `bool` (`ref`) | — | Supplied help says this enables timed garbage collection on the client when set to true. Timing interval and triggers are not supplied. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- Only `Level.IgnoreAbilitiesRuleOpt` appears in the captured value snapshot (`false`). The missing values for the other seven entries do not establish defaults.
- `Disable*ForMaps` are string references, but the registry does not provide accepted map names, separators, wildcard rules, or whether entries are loaded from a config list.
- The temporary timestamp format is stated in help; no meaning for the four slots is established.
- Static address-reference hits are candidate evidence only. They do not prove runtime use, registration, a visible effect, or acceptance of startup `.ini` overrides.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), [Chinese help and translations](cvar-chinese-help-translations.md), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
