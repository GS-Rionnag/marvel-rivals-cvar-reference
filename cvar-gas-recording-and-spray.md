# GAS trajectory recording and spray paint in build 1.1.4042190

The Windows Shipping executable contains initialization calls that pass each exact name below and its backing storage to the console manager. Separate instruction sequences read those same locations. The comparison and call behavior below comes from those sequences. Whether initialization runs in a particular session, whether a startup loader accepts an override, and what changes in a running game remain unverified.

| Variable | Static behavior | Remaining uncertainty |
| --- | --- | --- |
| `GAS.Projectile.TrajectoryRecordEnabled` | Gates both creation of a repeating timer and the timer's callback. The setup path also calls that callback once before creating the timer, after other checks pass. | The conditions under which a projectile reaches the setup path and where the recorded data is exposed. |
| `GAS.Projectile.TrajectoryRecordInterval` | Supplies the repeating timer's rate. The setup path skips the immediate call and timer creation when the rate is at or below approximately `1e-8`. The callback is also reached by other code paths. | Whether changing the setting after setup reschedules an existing timer and how often samples are produced in a live session. |
| `GAS.Optimize.SprayPaintQuantityLimit` | When positive, the value can lower the existing count limit before a collection-removal loop. Zero and negative values leave that existing limit in place. | Which collection owns the limit and whether it applies per player, per scene, or at another scope. |
| `GAS.Optimize.SprayPaintLifeSpan` | A value greater than approximately `1e-8` is passed as a float to a virtual method on the affected object. At or below that threshold the call is skipped. | The method's identity, the unit accepted by the method, and the resulting lifetime in a running game. |

## Remaining unresolved names

The preserved registry and console-object tables provide no explanatory help for the 42 unresolved `GAS.*` names. Reading the operands of the existing build scan found 61 direct reads or comparisons across 35 names and two writes, both against the community reference field for `GAS.TreatUseGERepMode`. These counts use address matches from the community table. The exact name-to-storage pairing and follow-on control flow were checked for the four variables above.

Seven names only matched console-object addresses in that scan. They were `GAS.DisableSpawnLoopProjectile`, `GAS.DisableSpawnProjectile`, `GAS.DisableSpawnScope`, `GAS.DisableSpawnSummoned`, `GAS.Projectile.BounceWaitReentryGuard`, `GAS.Projectile.CreateFakeAdvancedKey`, and `GAS.Projectile.ServerWaitClientBounce`. The scan can miss indirect reads through a console object. `GAS.Projectile.CreateFakeAdvancedKey` was also absent from the exact-name string inventory for the main Shipping executable. Its many community object rows do not settle whether the game recognizes that name in this build.

See the [GAS family guide](cvar-gas-batch-a.md), the [second GAS family guide](cvar-gas-batch-b.md), the [first projectile guide](cvar-gas-projectile-batch-a.md), the [second projectile guide](cvar-gas-projectile-batch-b.md), and the [evidence notes](EVIDENCE.md) for source context.
