# Evidence, sources, and scope

This repository contains Markdown documentation only. It does not distribute game executables, mods, local configuration files, raw binary scans, source-dump files, scripts, or personal computer paths.

## Community sources

- [Community CVar registry message](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322) provides the registry attachments discussed in the guides.
- [Community CVar snapshot message](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452) provides the captured value snapshot. Snapshot values are not assumed to be defaults.
- A separately shared [`userengine.ini`](https://github.com/RitzDaCat/MarvelRivalsConfig/blob/26cf358988f2d74004544ca128fd3a3ae1a3aa79/userengine.ini) is tracked only as a source of unverified CVar-shaped names; it is not treated as a tested game config.
- A [public Scalability.ini gist](https://gist.github.com/RoboMWM/ae6fd0689c949322ba973322cada2888), a pinned [FPS Booster template](https://github.com/n0tmar/Marvel-Rivals-FPS-Booster/blob/0eee0d36c0775fca09b8ae7fb30537c2d6e562a3/MarvelRivalsFPSBooster.hta), and two [Pastebin configs](https://pastebin.com/DGiLxGgp) ([second](https://pastebin.com/GpwmPxpc)) linked by [Odyi's guide](https://github.com/Odyi/Config-settings-for-marvel-rivals/blob/main/Instructions.md) are tracked only for unverified CVar-shaped names. They are not treated as evidence of registration or working overrides.
- Epic Unreal Engine documentation links are included next to upstream CVar descriptions where relevant.

## Build-specific static analysis

Some guides report analysis of Marvel Rivals Shipping build 1.1.4042190. The raw executable, hashes, file inventories, and disassembly/address-scan exports are intentionally omitted. Those findings are static evidence only: a name string or address reference is not by itself proof of runtime registration, startup-config acceptance, or an in-game effect. Direct value reads are distinguished from object-address setup references where the available evidence permits.

## Method and reproducibility

The guides preserve the source of each claim and distinguish community help, upstream Unreal behavior, snapshots, and build-specific analysis. Raw scan exports and local analysis scripts are not included; readers should treat exact addresses as build-specific and revalidate them against the build they use.

## Coverage counts

The preserved community registry contains 8,973 distinct, case-sensitive names with a variable or reference entry. The focused guide tables now account for all 8,973 names (100% exact-name coverage). This is an inventory-coverage measure, not a claim that every behavior is understood: where supplied help is absent or ambiguous, the guides say so and leave the meaning unresolved. Three names also have dedicated prose analyses linked from the final registry-remainder guide.

These counts measure exact-name coverage of the preserved registry only. They do not establish registration in a particular Shipping build, effective values, startup override support, or complete behavioral understanding. Commands and candidates found only in snapshots, console objects, or upstream and binary comparisons fall outside the registry denominator.

The eleven focused candidate guides cover 114 distinct names outside the registry. Of these, 55 have snapshot values and 26 have upstream Epic reference entries without snapshot values. Two additional candidates are supported by a third-party config and Shipping strings. Seven CVar-shaped names are found only in a separate public userengine.ini, and 19 additional distinct names appear only across other public community configs/templates; all 26 remain unverified. Five AudioLink and stereo-emulation candidates are supported by embedded Shipping strings. Four visualization names appear in both the graphics candidate and source comparison guides and count once.

The snapshot-only inventory contains 67 exact names, including the 55 with focused candidate notes. The other 12 lack exact matches in the preserved Epic reference and scanned Shipping string inventory. Their captured values remain inventory evidence, with game registration and runtime behavior unresolved. See [the snapshot-only inventory](cvar-snapshot-only.md).

The rendering cache guide records three candidate commands from nearby Shipping text. These fall outside both the registry-variable count and the variable-candidate count.
