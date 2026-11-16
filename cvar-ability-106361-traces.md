# Ability 106361 trace and explosion CVars

This guide covers the 18 `Ability.106361.*` variable entries in the community registry. They configure a named ability's cue simulation, trace sampling, sample filtering, and explosion handling. The descriptions below come from the registry's own help text, checked against direct variable reads in the installed build where available.

## Evidence and scope

- Community descriptions, types, and captured values: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452), preserved from the [Discord registry post](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) and [snapshot post](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Snapshot values are observations, not defaults or recommendations.
- Local binary: `Marvel Rivals Shipping executable`, build 1.1.4042190, SHA-256 `omitted from this documentation-only project`.
- Static instruction matches were cross-checked in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). They show reads and branches on some variables, but do not establish the exact user-visible outcome or which hero uses ability 106361.
- No in-game override experiment was run. The ability ID and cue ID are preserved as named in the source; their character mapping is unknown.

## Variables

| CVar | Type | Snapshot | Meaning and evidence |
|---|---|---:|---|
| `Ability.106361.ExplodeIgnoreStartPenetrating` | bool | `true` | Community help: the 10636103 explosion ignores a trace that starts already penetrating. The CVar has a direct boolean comparison at `0x149320D5A`. |
| `Ability.106361.ExplodeSkipDestruction` | bool | `true` | Community help: do not generate the explosion spell on destruction actors. Direct boolean comparison at `0x14931E1E9`. |
| `Ability.106361.FilterDelaySeconds` | float | `0.02` | Delay in seconds after each `RawTracePoint` before step filtering; the help says this lets 102 dispersion damage finish before filtering. A float load appears at `0x1493234FA`. |
| `Ability.106361.FilterDistanceThreshold` | float | `300` | If the distance between current and previous locations is below this threshold, skip the intermediate step and connect directly. Compared as a float at `0x14931E53D`. |
| `Ability.106361.FilterProbeLength` | float | `300` | Vertical probe-trace length, in centimeters, at each step point. Float load at `0x14931E156`. |
| `Ability.106361.FilterStepDistance` | float | `300` | Distance in centimeters between adjacent step probes. Float load at `0x14931E625`. |
| `Ability.106361.OnlyBoxTraceOnDS` | bool | `true` | Community help says the 10636102/10636103 box trace runs only on the dedicated server, skipping the client to reduce trace cost. Direct boolean checks include `0x149320819`, `0x149320911`, and `0x149320BC6`. |
| `Ability.106361.OnlyStepOnDS` | bool | `true` | No help text. A direct comparison occurs at `0x1493206EF` in code that then checks a network-role-like byte before setting a state byte. The name and branch support a server-only stepping interpretation, but the exact role mapping and effect remain inferred. |
| `Ability.106361.SampleSamePlane` | bool | `true` | Enable a same-plane test when comparing two hit samples. Direct boolean check at `0x149322223`. The source description accidentally repeats the angle field where it refers to the height threshold; see the two threshold rows below. |
| `Ability.106361.SampleSamePlaneAngle` | float | `30` | Angle threshold for treating two hit normals as the same plane. Direct loads at `0x149321070` and `0x1493225F1`. |
| `Ability.106361.SampleSamePlaneHeight` | float | `200` | Height-difference threshold for treating two hit samples as the same plane. This interpretation follows its separate source field name and the companion help's explicit `SampleSamePlaneHeight` placeholder; direct loads include `0x149320F3E`, `0x14932227B`, and `0x1493223C0`. |
| `Ability.106361.SimulationSkipCueInterp` | bool | `false` | If enabled, do not interpolate cue `10636101` in simulation. Direct boolean checks include `0x14931D555` and `0x149325F1C`. |
| `Ability.106361.StepByBinary` | bool | `false` | No help text and no direct `ref_rva` read candidate in the local scan. The name alone is not enough to define its algorithm; meaning is unknown. |
| `Ability.106361.StepBySameDistance` | bool | `true` | Step by equal distances between traces when enabled; the source says zero switches to stepping by equal angles. Direct boolean check at `0x14931EF3F`. |
| `Ability.106361.StepCountByDistance` | bool | `true` | The source says the number of steps increases from one to `StepTraceCount` across `StepMinDistance` to `StepMaxDistance`. A boolean check appears at `0x149321251`. The help's placeholder text is imperfect, so treat the stated relationship as source wording rather than a complete formula. |
| `Ability.106361.StepMaxDistance` | float | `3000` | Upper distance bound for the distance-based step-count behavior, in game distance units (the source does not state the unit). Float load at `0x1493212D0`. |
| `Ability.106361.StepMinDistance` | float | `500` | Lower distance bound for the distance-based step-count behavior, in game distance units (the source does not state the unit). Float load at `0x1493212E5`. |
| `Ability.106361.StepTraceCount` | int32 | `10` | No standalone help. The `StepCountByDistance` description identifies this as the upper step-count value; code near `0x149321251` reads it with the min/max distance values. The precise interpolation and clamping behavior need more analysis. |

## Practical reading

These are ability-specific implementation controls rather than general graphics or network tuning. The trace-related entries appear to trade sampling detail against work: equal-distance or equal-angle stepping, a distance-based step count, vertical probe length, and a filter that can skip nearby points. `OnlyBoxTraceOnDS` explicitly moves the named box trace off clients when enabled. Those statements describe the source comments; they do not prove a performance gain or a particular in-match result on a live server.

The captured values are a useful baseline for the source dump, but the attachment does not identify its game build or capture procedure. Several values may be changed or ignored by a different build. Avoid treating the snapshot as a safe override preset.

## Remaining questions

- Which hero or gameplay feature maps to ability 106361?
- Does `OnlyStepOnDS` gate all step traces, a particular step phase, or a replication path?
- What algorithm does `StepByBinary` select, and is it read indirectly or only during initialization?
- What are the units, bounds, and exact interpolation formula for `StepMinDistance`, `StepMaxDistance`, and `StepTraceCount`?
- Do any of these CVar values affect remote clients, server authority, or both in a live match?
