# StaticScopeSuppression CVar batch A

This guide covers all seven currently uncovered exact-case `StaticScopeSuppression.*` registry entries. Supplied help describes count limiting for static scopes globally or individually, four priority-specific count limits, and a cooldown duration. The source does not define what a “static scope” is in game terms, how global and individual limits interact, or whether the limits are per frame, actor, or another lifetime.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `StaticScopeSuppression.CooldownTime` | `float` (`ref`) | `0.1` | Cooldown duration in seconds after a tag scope executes; help says `0` means no cooldown. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 3 address-taking references to `ref_rva`. |
| `StaticScopeSuppression.CountLimit0` | `int32` (`ref`) | `1` | Count limit for priority 0, which the help identifies as the lowest priority. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `StaticScopeSuppression.CountLimit1` | `int32` (`ref`) | `1` | Count limit for priority 1. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `StaticScopeSuppression.CountLimit2` | `int32` (`ref`) | `1` | Count limit for priority 2. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `StaticScopeSuppression.CountLimit3` | `int32` (`ref`) | `2` | Count limit for priority 3. The help does not state how priority 3 ranks relative to priorities 1 and 2. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `StaticScopeSuppression.Global.Enable` | `bool` (`ref`) | `false` | Enables or disables count limiting of static scopes globally. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |
| `StaticScopeSuppression.Individual.Enable` | `bool` (`ref`) | `true` | Enables or disables count limiting of static scopes individually. The meaning of “individually” is not specified. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 2 direct-memory candidates and 1 address-taking reference to `ref_rva`. |

## Interpretation and limits

- The four `CountLimit*` values are per-priority settings according to help. Only priority 0 is explicitly called the lowest; neither the ordering of other priorities nor what is counted is established.
- Global and individual enable flags can both be present, but the registry help does not explain precedence, combination, or whether one mode is a fallback for the other.
- The cooldown description refers to a “tag scope”; the relationship between that phrase, static scopes, and count limiting is not explained in the supplied material.
- Snapshot values are captured observations, not verified defaults or recommendations. Address-reference scan results are static candidates only and do not prove runtime use, registration, effect, or acceptance from a startup `.ini` override.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
