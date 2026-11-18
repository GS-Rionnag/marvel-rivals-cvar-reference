# Combat mechanics CVar metadata

These registry entries concern projectile targeting, projectile task setup, ammunition penetration, and a flame-stack pursuit trigger. The descriptions come from supplied help where available. Registry metadata leaves Shipping behavior unverified.

| Exact name | Type / kind | Supplied meaning or evidence limit |
| --- | --- | --- |
| `Projectile_10302101.ForceHomingHitPawn` | `bool` / `ref` | Selects the Pawn as the homing collision target in place of its HitShape. The help leaves the collision outcome and affected targets unspecified. |
| `Projectile_10302101.ServerEventRunItself` | `bool` / `ref` | Supplied help associates this variable with initializing the same-named event flag before `BeginAgentTask`. It leaves event scheduling and dispatch semantics unspecified. |
| `Weapon.Ammo.PenetrateCount` | `int32` / `ref` | No supplied help. The name suggests a penetration count. The registry leaves what is counted and how the value is used unspecified. |
| `Weapon.InstantAmmo.EnableNearRangePenetratePolyline` | `bool` / `ref` | No supplied help. The name suggests a near-range penetration polyline option for instant ammunition. Scope and behavior remain unknown. |
| `hero.1054.DisableFlameExplodePursue` | `bool` / `var` | Supplied help associates the variable with whether reaching the flame-stack threshold triggers `TryPursue`. Other triggers and resulting behavior remain unspecified. |

[Community registry](EVIDENCE.md#community-sources) · [Raw registry](EVIDENCE.md#community-sources)
