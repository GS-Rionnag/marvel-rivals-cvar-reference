# Dash registry entries with unresolved meanings

The registry and console-object tables supply no help for these five previously uncovered names. Their settings, meanings, and supported contexts remain unresolved. Snapshot values record observations from the preserved dump.

| Exact CVar | Kind / type | Snapshot | Direct memory (ref / obj) | Address taken (ref / obj) |
| --- | --- | ---: | ---: | ---: |
| `Dash.AngleFilter.SkipPawn` | `ref` / `bool` | `true` | 1 / 3 | 1 / 1 |
| `Dash.Server.CheckServerStartDashMultiTime` | `ref` / `int32` | `1` | 1 / 3 | 1 / 1 |
| `Dash.UseForceStopDash` | `ref` / `bool` | `true` | 2 / 3 | 1 / 1 |
| `dash.BindOnActorHit.ThreadSafe` | `ref` / `bool` | `false` | 3 / 3 | 1 / 1 |
| `dash.debug.msg` | `ref` / `int32` | `0` | 0 / 3 | 1 / 1 |

The four exact lowercase `charmove.*` entries already have help and focused coverage. The three movement update entries appear in [A–H batch C](cvar-residual-ah-c.md), and the remaining entry appears in the [motion CVar guide](cvar-motion-residual.md).

Static candidates for Shipping build 1.1.4042190 may include initialization, reads, writes, and address passing. They leave runtime behavior and override acceptance unverified. See the [preserved registry and snapshot](EVIDENCE.md#community-sources) and [address-match TSV](EVIDENCE.md#build-specific-static-analysis).
