# Additional A–M registry metadata

These entries concern portal geometry, input processing, collision handling, and game-mode behavior. Descriptions based on names are marked explicitly. The preserved registry metadata leaves Shipping behavior unverified.

| Exact name | Type / kind | Description and evidence limit |
| --- | --- | --- |
| `AbilitySystemLibrary.CVarAutoBarrierOcclusionUseRollback` | `bool` / `ref` | No supplied help. The name links rollback to automatic barrier occlusion. The affected stage is unknown. |
| `AbilitySystemLibrary.CVarOcclusionUseRollback` | `bool` / `ref` | No supplied help. The name links rollback to an occlusion path. Its relationship to the barrier-specific setting is unknown. |
| `AbilitySystemLibrary.CVarOcclusionUseRollbackSystem` | `bool` / `ref` | No supplied help. The name links the occlusion path to a rollback subsystem. The subsystem and affected callers are unknown. |
| `AbilitySystemLibrary.FixInsideCapsulePortalStart` | `bool` / `ref` | Help describes correcting the portal firing origin when the origin is inside a capsule. |
| `AimAssist.DeadZoneHorizontalDeceleration` | `float` / `var` | Translated help associates this setting with horizontal aim-assist behavior at the dead zone. Runtime units and the response curve are unverified. |
| `AimAssist.DeadZoneVerticalDeceleration` | `float` / `var` | Translated help associates this setting with vertical aim-assist behavior at the dead zone. Runtime units and the response curve are unverified. |
| `AimAssist.EnablePunisherYawScale` | `bool` / `var` | Translated help describes a yaw sensitivity scale for the Punisher's turret. |
| `AimAssist.HorizontalDeadZoneAccelerationMaxTime` | `float` / `var` | No supplied help. The name suggests a maximum duration for horizontal dead-zone acceleration. Time units and start conditions are unknown. |
| `AimAssist.HorizontalDeadZoneAccelerationTime` | `int32` / `var` | No supplied help. The name suggests a timing setting for horizontal dead-zone acceleration. Its relationship to the maximum-time setting is unknown. |
| `AimAssist.UseOldVersionAimAssist` | `bool` / `ref` | Translated help identifies a legacy aim-assist implementation. The differences between implementations are unspecified. |
| `Hero.1061.Portal.EnableSVONReachableCheck` | `bool` / `ref` | Supplied help describes an SVON reachability check during portal point selection. |
| `JoyStick.HookRightAnalogValueX` | `float` / `var` | Translated help associates the entry with an override of the right-stick X input. |
| `JoyStick.HookRightAnalogValueY` | `float` / `var` | Translated help associates the entry with an override of the right-stick Y input. |
| `MarvelRepGraph.EnableSummonedDuelVisibility` | `bool` / `ref` | Help identifies a visibility check for summoned actors in Times Square duels when viewed from outside the duel. |
| `angela.ServerUseAuthoritativePositionWhenGliding` | `bool` / `ref` | Help associates the entry with authoritative position handling during Angela's glide. Replication and correction behavior are unspecified. |
| `ddos.GOpenDDoSFlag` | `int32` / `ref` | Help identifies DDoS detection as the associated feature. The detection method and runtime enforcement are unspecified. |

This batch records the names and supplied registry help only. Where a name implies a behavior that the available evidence does not establish, the uncertainty is stated explicitly.

[Community registry](cvar-community-registry.md) · [Registry help translations](cvar-chinese-help-translations.md)
