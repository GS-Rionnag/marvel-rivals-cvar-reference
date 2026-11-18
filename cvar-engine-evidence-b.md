# Additional gameplay and engine CVar evidence

These exact registry names concern web target tracing, view-target notifications, portal transform calculation, and wall building. Snapshot values are observations from an unspecified capture build.

The build string column lists exact names found in build 1.1.4042190. Address counts give x64 direct-memory candidates / address-taking instructions. A dash indicates no value or match in the associated source. Runtime effects and startup override support remain unverified.

| Exact name | Type / kind | Snapshot | Meaning and evidence limits | Build strings | Object hits | Ref hits |
| --- | --- | --- | --- | --- | --- | --- |
| `SpiderManager.GSimpleTraceTargetInWeb` | `bool` / `ref` | — | No supplied help. The name suggests a simplified target trace in the web subsystem. The trace method, scope, and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | 4 / 1 |
| `Team.GlobalCanIgnoreViewTargetChange` | `bool` / `ref` | `false` | No supplied help. The name suggests a team-system setting for responding to view-target changes. The affected event, conditions, and value mapping are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `pp.UsePortalEndTransformV2` | `bool` / `ref` | `true` | The help describes using a virtual second resolve when calculating the end-portal transform for ability 101861. The second resolve and output differences are unspecified. | x64, ARM64EC | 3 / 1 | 1 / 1 |
| `wb.Feature.AllowWallBuildOnAlly` | `bool` / `ref` | `false` | No supplied help. The name suggests a wall-building rule involving allies. The conditions and value mapping are unspecified. | x64 | 3 / 1 | 2 / 1 |

## SpiderManager web-trace flag: branch detail

Disassembly of the matching build 1.1.4042190 executable shows that the four references at RVAs `0x70249CC`, `0x7024A60`, `0x7024E61`, and `0x7025550` compare the flag byte with a register initialized to zero earlier in the same routine. The branches use both polarities: at the first two sites, zero skips a pointer-list scan or count-checked helper block; at the latter two, nonzero skips an indexed lookup/resolver block and another object-processing block. This confirms that the flag gates concrete data-processing paths, but the helper and accessed structures have no recovered names here. The instructions do not establish that those paths are web-target tracing or show the flag's visible effect, so “simplified target trace” remains a name-based interpretation.

## Sources

[Raw registry](EVIDENCE.md#community-sources) | [Snapshot](EVIDENCE.md#community-sources) | [Build string inventory](EVIDENCE.md#build-specific-static-analysis) | [Address scan](EVIDENCE.md#build-specific-static-analysis)
