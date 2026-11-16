# Chaos Newton and PBD evolution CVars

This guide covers the twelve `p.Chaos.NewtonEvolution.*` and `p.Chaos.PBDEvolution.*` variables in the supplied community registry. The names are present in the Marvel Rivals Shipping `1.1.4042190` executable and ARM64EC companion, but every row has `ref_rva=0`; the saved scan therefore cannot identify a direct value-read site in the solver. Captured values below are not verified defaults or recommendations.

## NewtonEvolution

| CVar | Type | Snapshot | Help and confidence |
| --- | --- | ---: | --- |
| `p.Chaos.NewtonEvolution.FastPositionBasedFriction` | bool | `true` | No registry help. The name suggests a fast position-based-friction path, but no local value-read site was recovered to confirm its effect. |
| `p.Chaos.NewtonEvolution.MinParallelBatchSize` | int32 | `300` | No registry help. The name suggests a minimum batch threshold for parallel work; the unit and exact branch are unknown. |
| `p.Chaos.NewtonEvolution.ParalleIntegrate` | bool | `false` | Registry help: “Run the integration step in parallel for.” The key is spelled `ParalleIntegrate` in the source. Help does not identify the parallel primitive, eligibility conditions, or performance effect. |
| `p.Chaos.NewtonEvolution.UseNestedParallelFor` | bool | `true` | No registry help. The name suggests nested `parallelFor` scheduling, but this remains unverified. |
| `p.Chaos.NewtonEvolution.UseSmoothTimeStep` | bool | `true` | No registry help. The name suggests a smoothed timestep choice, but its formula and effect remain unknown. |
| `p.Chaos.NewtonEvolution.WriteCCDContacts` | bool | `false` | Registry help says this writes CCD collision contacts and normals for debugging and may cause CCD collision threads to lock. The local value-read path was not recovered, so its availability and lock behavior in this Shipping build are not confirmed. |

## PBDEvolution

| CVar | Type | Snapshot | Help and confidence |
| --- | --- | ---: | --- |
| `p.Chaos.PBDEvolution.FastPositionBasedFriction` | bool | `true` | No registry help. The name suggests a fast position-based-friction path, but no local value-read site was recovered to confirm its effect. |
| `p.Chaos.PBDEvolution.MinParallelBatchSize` | int32 | `300` | No registry help. The name suggests a minimum batch threshold for parallel work; the unit and exact branch are unknown. |
| `p.Chaos.PBDEvolution.ParalleIntegrate` | bool | `false` | Registry help: “Run the integration step in parallel for.” The key is spelled `ParalleIntegrate` in the source. Help does not identify the parallel primitive, eligibility conditions, or performance effect. |
| `p.Chaos.PBDEvolution.UseNestedParallelFor` | bool | `true` | No registry help. The name suggests nested `parallelFor` scheduling, but this remains unverified. |
| `p.Chaos.PBDEvolution.UseSmoothTimeStep` | bool | `true` | No registry help. The name suggests a smoothed timestep choice, but its formula and effect remain unknown. |
| `p.Chaos.PBDEvolution.WriteCCDContacts` | bool | `false` | Registry help says this writes CCD collision contacts and normals for debugging and may cause CCD collision threads to lock. The local value-read path was not recovered, so its availability and lock behavior in this Shipping build are not confirmed. |

## What the local binary establishes

- All twelve names are listed as exact strings in both local executable variants in the [build CVar inventory](EVIDENCE.md#build-specific-static-analysis). This proves string presence, not runtime registration, mutability, or which evolution backend is used.
- The community table gives each entry `ref_rva=0`. The saved reference scan has no matching value-read candidates. Its `obj_rva` address-taking and pointer-store hits occur in constructor/initialization-like code; those are not evidence that a solver reads the configured values during evolution.
- `NewtonEvolution` and `PBDEvolution` have parallel sets of names and captured values. This symmetry suggests paired backend settings, but does not prove that both backends are active or that each setting behaves identically.
- No controlled in-game override was tested. Preserve the original spelling `ParalleIntegrate` when referencing the key; do not infer safe tuning ranges from the snapshot.

Evidence files: [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), [`console_objects.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322), [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452), and [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The source manifest records that the preserved tables and snapshot match the Discord attachments byte for byte.
