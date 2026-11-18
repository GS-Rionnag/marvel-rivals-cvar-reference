# Remaining exact N–Z variable registry entries

This inventory records 15 names from the preserved community variable registry after comparing exact names with the focused guides. Types come from the registry. Descriptions identify the subsystem or purpose where source help supports it. For entries with blank or punctuation-only help, behavior remains unresolved. [Community registry and source notes](cvar-community-registry.md)

| Exact CVar | Registry type | Source-supported scope |
| --- | --- | --- |
| `Physics.SkipOverlap` | `int32` | Physics overlap control. The affected overlap paths are unspecified. |
| `ReplicateSubobjects_Attributes.Ignore` | `int32` | Replication policy for Zombie Mass attributes. |
| `Summoned.DefaultRepPredictionKeyMap` | `bool` | Unknown. The available object help contains only punctuation. |
| `Swinging.DisableMeshPenetrationTrace` | `bool` | Swinging mesh-trace setting. Runtime scope remains unverified. |
| `TraceFunction.FindGround.CVarFindGroundValidTargetPortalSegmentCheck_S3_1` | `bool` | Unknown. The registry gives no descriptive help. |
| `TraceMgr.CVar_EnableHeadHitIgnoreBlockRange` | `bool` | Occlusion policy for an additional head-hit check. |
| `TraceMgr.CVar_SwiftProjectileFilterPenetrateReceiver` | `bool` | Swift projectile trace filtering. Runtime scope remains unverified. |
| `VirtualProjectile.ServerCheckPosDeltaTime` | `float` | Unknown. The registry gives no descriptive help or units. |
| `VirtualProjectile.ServerPosCheckHitRange` | `float` | Unknown. The registry gives no descriptive help or units. |
| `Weapon.Ammo.EnableSplitSceneKeepPenetrable` | `bool` | Weapon ammunition scene handling. Runtime scope remains unverified. |
| `n.VerifyPeer` | `int32` | Certificate verification for the HTTPS peer in libcurl. |
| `oss.PlatformOverride` | `FString` | Client platform selection for debugging. |
| `pp.CheckInvalidPlaceArea` | `bool` | Invalid-placement check. The help leaves the area and validation rules unspecified. |
| `pve.SkipServerEffectLedgerApply` | `bool` | Server-side handling of the replicated PvE effect ledger. |
| `scope.AllowAttachTypeTrustClient` | `bool` | Client-position handling for attach-type gameplay fields. |

The separate `r.LockView` candidate appears as a literal in both Shipping executables and is named in the help for the community command `r.CopyLockedViews`, which describes copying locked views for later reload. The literal could come from that same help text. The exact `r.LockView` name has no community registry row, and its registration and argument format remain unverified. [Community command catalog](cvar-community-commands.md) · [Build-specific static-analysis scope](EVIDENCE.md#build-specific-static-analysis)
