# Evidence, sources, and scope

This repository contains Markdown documentation only. It does not distribute game executables, mods, local configuration files, raw binary scans, source-dump files, scripts, or personal computer paths.

## Community sources

- [Community CVar registry message](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) provides the registry attachments discussed in the guides.
- [Community CVar snapshot message](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452) provides the captured value snapshot. Snapshot values are not assumed to be defaults.
- Epic Unreal Engine documentation links are included next to upstream CVar descriptions where relevant.

## Build-specific static analysis

Some guides report analysis of Marvel Rivals Shipping build 1.1.4042190. The raw executable, hashes, file inventories, and disassembly/address-scan exports are intentionally omitted. Those findings are static evidence only: a name string or address reference is not by itself proof of runtime registration, startup-config acceptance, or an in-game effect. Direct value reads are distinguished from object-address setup references where the available evidence permits.

## Method and reproducibility

The guides preserve the source of each claim and distinguish community help, upstream Unreal behavior, snapshots, and build-specific analysis. Raw scan exports and local analysis scripts are not included; readers should treat exact addresses as build-specific and revalidate them against the build they use.

## Coverage counts

The preserved community registry contains 8,973 distinct, case-sensitive names with a variable or reference entry. The focused tables cover 8,916 of these names (99.36%). Three additional names have individual explanations in guide prose, bringing coverage across both formats to 8,919 (99.40%). The remaining 54 names lack a focused explanation.

These counts measure reference coverage. Registration in a particular Shipping build, effective values, and startup override support require separate evidence. Commands and candidates found only in snapshots, console objects, or upstream and binary comparisons fall outside the registry denominator.

The nine focused candidate guides cover 83 distinct names outside the registry. Of these, 55 have snapshot values and 26 have upstream Epic reference entries without snapshot values. Two additional candidates come from a third-party config and Shipping strings. Four visualization names appear in both the graphics candidate and source comparison guides and count once.

The snapshot-only inventory contains 67 exact names, including the 55 with focused candidate notes. The other 12 lack exact matches in the preserved Epic reference and scanned Shipping string inventory. Their captured values remain inventory evidence, with game registration and runtime behavior unresolved. See [the snapshot-only inventory](cvar-snapshot-only.md).
