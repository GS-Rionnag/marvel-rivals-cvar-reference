# Chaos Suspension CVars

This guide covers the eight `p.Chaos.Suspension.*` variables in the supplied community registry. It records registry help and captured values, then connects the values to direct instruction reads in Marvel Rivals Shipping build `1.1.4042190`. A binary read proves that the executable contains a consumer path; it does not prove the game's maps or heroes instantiate suspension constraints. Snapshot values are not verified defaults or tuning advice.

| CVar | Type | Snapshot | Registry meaning and local-build evidence |
| --- | --- | ---: | --- |
| `p.Chaos.Suspension.Hardstop.Enabled` | bool | `true` | Enables/disables the hardstop part of the suspension constraint, per help. The byte gates hardstop work at `0x1429C12E9` and `0x1429C22D7`; zero branches around those paths. |
| `p.Chaos.Suspension.MaxPushout` | float | `5` | Registry help calls this the maximum suspension pushout value. At `0x1429C1346`, the value is loaded in the hardstop path; nearby math takes the minimum of it and a second limit derived from `MaxPushoutVelocity` times an input scalar. The exact units and caller-supplied scalar are not identified. |
| `p.Chaos.Suspension.MaxPushoutVelocity` | float | `100` | Registry help calls this the maximum suspension pushout velocity. At `0x1429C133B`, it is loaded and multiplied by an input scalar; the result is capped by `MaxPushout` in the same routine. The scalar's unit and full solver interpretation are unresolved. |
| `p.Chaos.Suspension.SlopeSpeedBlendThreshold` | float | `10` | Help says the anti-slide-on-slope blend begins below this speed. Read at `0x1429C1E53` in a path that computes a vector magnitude and compares it with a threshold derived from this CVar. The exact blend curve is not fully reconstructed. |
| `p.Chaos.Suspension.SlopeSpeedThreshold` | float | `1` | Help says the anti-slide-on-slope mechanism is fully employed below this speed. Read at `0x1429C1DCE`; the value is scaled, squared, and compared with a computed speed-related magnitude in the slope-control path (`0x1429C1DCE`–`0x1429C1E53`). |
| `p.Chaos.Suspension.SlopeThreshold` | float | `0.707` | Help says this cosine threshold determines when slope anti-slide is employed; it gives `cos(angle)` examples. The value is read at `0x1429C1DB9` and participates in a comparison in the same slope-control path. The comparison's vector components and exact boundary convention are not recovered. |
| `p.Chaos.Suspension.Spring.Enabled` | bool | `true` | Enables/disables the spring part of the suspension constraint, per help. At `0x1429C1727`, zero skips a subsequent helper call; this is a separate gate from `Hardstop.Enabled`. |
| `p.Chaos.Suspension.VelocitySolve` | bool | `true` | Enables/disables `VelocitySolve`, per help. The byte is tested at `0x1429C22E4` after the hardstop gate at `0x1429C22D7`; either false value exits before the subsequent constraint loop. |

## Interpretation limits

- Names, types, help, and reference addresses come from [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), corroborated by [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). Snapshot values come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). The source manifest records exact matches between the linked Discord attachments and the preserved files.
- Direct read candidates are in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included); the instruction paths listed above were inspected in the installed executable's `.text` disassembly.
- The traces support local solver gates and scalar data flow, but do not establish that suspension constraints are used in active Marvel Rivals gameplay, nor do they establish safe override ranges. No in-game override was tested.

Related guides: [Chaos joint and joint-constraint CVars](cvar-chaos-joints-and-constraint-scales.md), [Chaos CCD controls](cvar-chaos-ccd-axis-targets.md), [CVar overrides and loader syntax](cvar-overrides.md), and [CVar definition gaps](cvar-unresolved-definitions.md).
