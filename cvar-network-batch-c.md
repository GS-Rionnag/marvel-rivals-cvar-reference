# Network CVar batch C

This page documents 23 networking entries from the preserved community registry. The attachment does not state its game build or capture method. Captured values below are snapshots, not assumed defaults. The local binary evidence comes from the complete `.text` disassembly reference scan of Marvel Rivals Shipping build `1.1.4042190`; a matched instruction is a candidate read/write, not proof that a setting is applied in a normal match.

## Dormancy controls

| Exact name | Registry type | Snapshot | Meaning and local evidence |
| --- | --- | ---: | --- |
| `net.DormancyEnable` | `ref` / int32 | `1` | Registry help says this enables network dormancy to reduce CPU and bandwidth work for infrequently updated actors (`0` disables it). The exact Epic 5.9 entry has default `1`. Local integer comparisons at `0x143E7E45A` and `0x143E9348A` read the referenced field, consistent with a gate; the scan does not identify the actors or establish the path runs in retail play. |
| `net.DormancyHysteresis` | `ref` / float | `0` | A positive value is the delay, in seconds, before a channel becomes fully dormant; the stated purpose is to reduce churn when dormancy changes frequently. Epic 5.9 also lists `0`. Local float loads at `0x143B2B202` and `0x143B2B239` read the field. The timer's exact branch and units are described by the community help, not independently reconstructed from this instruction-only scan. |
| `net.DormancyValidate` | `ref` / int32 | `0` | Registry help marks this server-only validation: `0` off, `1` validate on wake, `2` validate on each network update. Epic 5.9 default is `0`. Local comparisons at `0x143B191D8`, `0x143E49029`, and `0x143E91B60` read the value, including a comparison with `2`, consistent with multiple modes. No validation failure path was traced here. |

## Duplicate-send policy controls

The registry groups these settings under client/server duplicate-send policy and loss thresholds. The tier labels and override conditions below come from its help text. They describe a retransmission/duplication policy, but the attachment does not define the packet type, threshold units, formulas, or exact conditions for duplicating a send. These entries are `var` rows with no `ref_rva`; their `obj_rva` matches in the static scan are not sufficient to establish runtime value reads.

| Exact name | Registry type | Snapshot | Meaning and limits |
| --- | --- | ---: | --- |
| `net.DuplicateSendClientAggressiveness` | `var` / int32 | `2` | Client-side aggressiveness tier: `0` conservative, `1` balanced, `2` aggressive. The names do not reveal how the tiers change send behavior. |
| `net.DuplicateSendClientCloseLossOverride` | `var` / float | `0` | A value greater than zero overrides the client close-loss threshold selected by its tier. Snapshot `0` means the documented override condition is not met in that snapshot. Threshold units and the close/open transition are not defined. |
| `net.DuplicateSendClientOpenLossOverride` | `var` / float | `0` | A value greater than zero overrides the client open-loss threshold selected by its tier. Snapshot `0` does not activate that documented override condition. Threshold units and the open/close transition are not defined. |
| `net.DuplicateSendMinSamplesForDecision` | `var` / int32 | `100` | Cold-start guard requiring this many notified packets before evaluating loss. The snapshot is `100`; the help does not define packet eligibility, reset behavior, or what action follows a loss decision. |
| `net.DuplicateSendServerAggressiveness` | `var` / int32 | `1` | Server-side aggressiveness tier: `0` conservative, `1` balanced, `2` aggressive. The relationship between a server tier and specific duplicate sends is not documented. |
| `net.DuplicateSendServerAllowClient` | `var` / int32 | `1` | Server master switch: `1` allows client upstream duplicate sending; `0` forbids it. The help does not say whether the switch affects only negotiation/permission or how it interacts with client thresholds. |
| `net.DuplicateSendServerCloseLossOverride` | `var` / float | `0` | A positive value overrides the server close-loss threshold chosen by its tier. Snapshot `0` leaves this override condition inactive per the help; units and threshold transition semantics are unknown. |
| `net.DuplicateSendServerOpenLossOverride` | `var` / float | `0` | A positive value overrides the server open-loss threshold chosen by its tier. Snapshot `0` leaves this override condition inactive per the help; units and threshold transition semantics are unknown. |

## Other networking entries

| Exact name | Registry type | Snapshot | Meaning and local evidence |
| --- | --- | ---: | --- |
| `net.EditOnlyClientUseNetEmulation` | `ref` / bool | `true` | The registry's only help is the variable name itself. Its `ref_rva` was only address-taken in the saved scan, with no direct value-read candidate. Do not infer editor-only or client net-emulation behavior from the name alone. |
| `net.EnableCongestionControl` | `var` / int32 | `0` | The help says it enables the congestion-control module. The exact Epic 5.9 reference also gives default `0` and the same short description. The local registry row is `var` with no `ref_rva`, so this scan does not show whether the module is compiled in or reads the setting in this build. |
| `net.EnableDetailedScopeCounters` | `ref` / bool | `true` | Enables detailed networking scope cycle counters. Help warns that there are often many counters and they can negatively affect performance. The exact Epic 5.9 entry has default `true`; the saved scan found only address-taking at `ref_rva`, not a direct read. This is diagnostic instrumentation, not a demonstrated performance optimization. |
| `net.EnableExportGUIDCleanup` | `var` / int32 | `0` | Registry help says `1` runs ExportGUID cleanup logic in Tick and `0` disables it. The local row has no `ref_rva`; the object-address matches cannot establish the cleanup path or its impact. |
| `net.EnableNetInitialSubObjects` | `ref` / bool | `true` | Enables new subobjects to set `bNetInitial`, so all replicated properties are sent. Epic 5.9 has the same default and description. A local byte comparison at `0x143B40644` reads the referenced value, consistent with a gate; replication behavior was not followed beyond this point. |
| `net.EnableUserIdOptimization` | `ref` / bool | `false` | Registry help only says it enables “userid optimization.” Three local byte comparisons (`0x143EC5DE7`, `0x143EC6030`, `0x143EC6470`) read the referenced value, but do not identify the optimized representation or any compatibility/privacy implications. |
| `net.ExportGUIDMaxCount` | `var` / int32 | `10000` | Maximum `AlreadyExportGUIDs` count before force-clearing in `CleanupAckedExportGUIDs`; help labels `10000` as the default. It is related by name/help to export-GUID cleanup, but the local scan has no `ref_rva` value-read evidence for this `var`. The snapshot also happens to be `10000`, which does not independently verify a default. |
| `net.FastDirty` | `ref` / bool | `true` | Help says this enables the Fast Array fast-dirty check. Local byte comparisons at `0x143B33AD6` and `0x143B34B61` read the referenced field, consistent with branching on the option. The scanner does not show what fields are checked or whether enabling it changes network traffic. |
| `net.FilterGuidRemapping` | `ref` / int32 | `1` | Help says it removes destroyed and parent GUIDs from the unmapped list. Local reads/comparisons at `0x143B1BEEE`, `0x143B2B6C1`, `0x143E96F22`, `0x143EC45F8`, `0x143EC4748`, and `0x143EC4779` show the value is consulted in several GUID/remapping-related locations. The exact list mutations and edge cases were not traced. |
| `net.FixedArtificialDelayFlag` | `ref` / int32 | `1` | The registry help is only “fixed artificial delay flag.” Seven local comparisons at `0x143E3BDB0`, `0x143E3C429`, `0x143E4A510`, `0x143E5B198`, `0x143E5B417`, `0x143E5B62B`, and `0x143E6A979` read the field. This proves repeated code use of the referenced value, but without surrounding control flow it does not establish the delay source, units, or whether the flag enables/disables it. |
| `net.FramUpload.Close` | `var` / int32 | `0` | No help or Epic 5.9 match was recorded. Preserve the exact registry spelling `FramUpload`; whether it is a typo, a frame-upload close switch, or something else is unresolved. The local `obj_rva` matches are not proof of a value read. |
| `net.GDuplicateParam1` | `var` / int32 | `50` | No help or Epic 5.9 match was recorded. The `GDuplicate` name alone does not prove a relation to the `net.DuplicateSend*` group; meaning, units, valid range, and runtime consumer remain unknown. |

## What can be concluded about editability

All 23 names have `var` or `ref` rows in the community registry, but that attachment has no confirmed build identity. The `ref`-address scan provides read candidates for eight entries: the three dormancy controls, `net.EnableNetInitialSubObjects`, `net.EnableUserIdOptimization`, `net.FastDirty`, `net.FilterGuidRemapping`, and `net.FixedArtificialDelayFlag`. Other `ref` entries have no value-read candidate in this saved scan. The eight duplicate-send entries, congestion control, export-GUID cleanup/max count, frame-upload name, and `net.GDuplicateParam1` are `var` rows; their object-address hits alone are not a traced CVar value use.

The captured snapshot values are not recommendations. Local loader syntax can express `name=value`, but there is no runtime test here showing that Marvel Rivals accepts these overrides, preserves them after startup, or changes network behavior. For the evidence scale and loader restrictions, see [CVar override evidence levels](cvar-overrides.md#does-a-cvar-actually-change-in-marvel-rivals).

## Sources and scope

- Names, types, help, and RVA fields: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322); normalized help and captured values: [community registry catalog](cvar-community-registry.md).
- Local address matches: [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included), built from the `Marvel Rivals Shipping executable` `.text` disassembly with image base `0x140000000`. Addresses are virtual addresses. The [scan notes](EVIDENCE.md#build-specific-static-analysis) explain why a non-`lea` match is still only a read/write candidate until control flow is inspected.
- UE 5.9 defaults/descriptions are shown only where the generated catalog has an exact-name match. They are upstream context, not proof of the Marvel Rivals fork version or current build behavior.
- No game execution, config modification, or runtime override test was performed for this guide.
