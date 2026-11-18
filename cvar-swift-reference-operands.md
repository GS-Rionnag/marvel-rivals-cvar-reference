# Swift CVar reference operands in Shipping build 1.1.4042190

This review checks the instruction operands for all 30 exact-case `Swift.*` names in the [unresolved definitions ledger](cvar-unresolved-definitions.md). [Batch A](cvar-swift-batch-a.md) and [batch B](cvar-swift-batch-b.md) retain the registry metadata and snapshot values.

| Reference-target evidence | Count | Exact names |
| --- | ---: | --- |
| Byte comparison and address taking | 2 | `Swift.Bugfix.273182`, `Swift.Collision.BanLongRollbackTime` |
| Address taking only | 8 | `Swift.Verify.RecordRemoveTolerance`, `Swift.Verify.RecordTolerance`, `Swift.Verify.RequestRecordDeltaTime`, `Swift.Verify.RequestRecordIntervalTime`, `Swift.Verify.ServerCheckPosDeltaTime`, `Swift.Verify.UseNewTraceCheckStartPos`, `Swift.Verify.UseTraceCheckExRange`, `Swift.Verify.UseTraceDoubleCheck` |
| No reference-target match in the scan | 20 | `Swift.Cache.Open`, `Swift.Debug`, `Swift.Draw.Position`, `Swift.Hit.VerifyChangeIndex`, `Swift.Open`, `Swift.Refected.Open`, `Swift.SpawnTime`, `Swift.Verify.Debug`, `Swift.Verify.EnableSecure`, `Swift.Verify.FlyTime`, `Swift.Verify.HitAll`, `Swift.Verify.HitDistance`, `Swift.Verify.MaxFPS`, `Swift.Verify.MinFPS`, `Swift.Verify.Reasonable`, `Swift.Verify.Refected.EndHit`, `Swift.Verify.Refected.ProcessHit`, `Swift.Verify.TrustClient`, `Swift.VerifyBox.DiffLength`, `Swift.VerifyBox.UseCapsule` |

Both comparisons use a byte at the registry's reference target and the low byte of a register. They read memory and set condition flags. The scan does not establish the register value, the branch that uses those flags, or the owning function. The eight address-only entries each have one `lea` against their reference target. Their downstream consumers remain unknown.

At the registry object targets, all 87 direct-memory candidates are 64-bit stores from registers. Each of the 30 names also has one object-target address-taking instruction. These object-target matches establish the direction of the recorded instructions. Indirect reads through an object or a pointer remain possible.

The address join uses the community registry and the [Shipping build scan](EVIDENCE.md#build-specific-static-analysis). Name-to-storage registration in the executable, live execution, configuration acceptance, and gameplay effects remain unverified. All 30 definitions remain open.
