# ClientMassSwarm CVar batch A

This guide covers all seven currently uncovered exact-case `ClientMassSwarm.*` entries. The supplied help describes reticle feedback when local attacks kill client-side swarm units, knockback behavior and budgets for NPC deaths, and a route-end death-animation option. Names and help point to swarm/NPC presentation and simulation behavior; they do not establish server authority, competitive-match relevance, or whether these settings are accepted from startup config.

| Exact CVar | Type / kind | Snapshot | Meaning from supplied help | Build 1.1.4042190 static scan |
| --- | --- | --- | --- | --- |
| `ClientMassSwarm.HitFeedback` | `int32` (`ref`) | — | Reticle hit feedback when a local attack kills client-swarm units, at most once per frame. `0` turns it off. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 direct-memory candidate and 1 address-taking reference to `ref_rva`. |
| `ClientMassSwarm.HitFeedback.Audio` | `int32` (`ref`) | — | Controls whether `UIEventBodyHit` audio plays with swarm reticle hit feedback. `0` means animation only. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `ClientMassSwarm.HitFeedback.Scale` | `float` (`ref`) | — | Scales the regular reticle X length for swarm hits. Values `<= 0` use the widget’s `MinRegularHookLengthScale`. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`; 1 address-taking reference to `ref_rva`. |
| `ClientMassSwarm.Knockback.Enable` | `int32` (`var`) | — | `0`: each NPC-scope death retires in place, preserving the prior no-knockback behavior. `1`: units whose rules enable knockback fly off. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ClientMassSwarm.Knockback.MaxConcurrent` | `int32` (`var`) | — | World-wide limit for units launching or flying concurrently; help gives range `0..16384`. Further knockback deaths retire in place as a fallback. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ClientMassSwarm.Knockback.MaxFlightSeconds` | `float` (`var`) | — | Maximum flight duration, `0.1..30` seconds. A unit still airborne at the limit lands at its current height. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |
| `ClientMassSwarm.RouteEndDeath` | `int32` (`var`) | — | Honors the route configuration’s `bRouteEndDeath`, allowing route-end units to play a death animation. `0` always retires silently, preserving prior behavior. | 3 direct-memory candidates and 1 address-taking reference to `obj_rva`. |

## Interpretation and limits

- All seven names are absent from the captured `CVarDump.txt` snapshot. Absence is not a default value and the supplied evidence does not reveal their live settings.
- The three hit-feedback entries are classified as `ref`; the four knockback/route entries are `var`. These registry classifications do not establish that Marvel Rivals accepts startup `.ini` overrides.
- Static address-reference hits are candidates only. They do not prove runtime reads/writes, execution, server/client authority, or visible behavior.
- Supplied ranges and zero-value behavior describe source help; they have not been independently validated in a live match.

Sources: [community registry and snapshot](EVIDENCE.md#community-sources), and [build 1.1.4042190 scan notes](EVIDENCE.md#build-specific-static-analysis).
