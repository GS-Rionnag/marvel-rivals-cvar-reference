# Slate CVar batch D: tooltips, transforms, and world widgets

This final batch records all 9 currently uncovered registered `Slate.*` entries after checking the latest public guides and source drafts. It closes the remaining tooltip, fullscreen mouse-transform, font-cache, widget timing, and world-widget ordering entries in the 84-name registry family.

Snapshot values come directly from the supplied CVar dump. Exact-name Epic UE 5.9 defaults are upstream references, not verified Marvel Rivals defaults. Community `ref` registration and static scan evidence do not prove the game accepts a startup override or applies it in a live match.

Static address-reference evidence is from Marvel Rivals Shipping build `1.1.4042190`. The scan’s `direct-memory-candidate` hits are distinguished from `address-taken` references. Candidate hits are not directionally traced, and the build was not tested at runtime.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied meaning and source | Build scan evidence and limits |
| --- | --- | ---: | ---: | --- | --- |
| `Slate.TooltipIntroDuration` | float (`ref`) | `0.1` | `0.1` | How long it takes for a tooltip to animate into view, in seconds. *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.TooltipSummonDelay` | float (`ref`) | `0.15` | `0.15` | Delay in seconds before a tooltip is displayed near the mouse cursor when hovering over widgets that supply tooltip data. *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.Transform.FullscreenMouseInput` | bool (`ref`) | `true` | `true` | Set true to transform mouse input to account for viewport stretching at fullscreen resolutions not natively supported by the monitor. *(community CVar help)* | `ref_rva`: 6 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.Transform.FullscreenMouseInputMultiScreenCorrection` | bool (`ref`) | `true` | `—` | Set true to correct TransformFullscreenMouseInput with multi-screen. *(community CVar help)* | `ref_rva`: 5 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.UnloadFreeTypeDataOnFlush` | int32 (`ref`) | `1` | `1` | Releases the free type data when the font cache is flushed *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.UseFixedDeltaTime` | bool (`ref`) | `false` | `false` | True means we use a constant delta time on every widget tick. *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 3 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.UsingFontMaterialUnityUV` | bool (`ref`) | `true` | `—` | Using unity uv for font material *(community CVar help)* | `ref_rva`: 2 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 2 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.WorldWidgetIgnoreNotVisibleWidgets` | bool (`ref`) | `false` | `false` | Whether to not update the position of world widgets if they are not visible - to prevent invalidating the whole layer unnecessarily *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 3 `direct-memory-candidate`, 1 `address-taken`. |
| `Slate.WorldWidgetZOrder` | int32 (`ref`) | `1` | `1` | Whether to re-order world widgets projected to screen by their view point distance 0: Disable re-ordering 1: Re-order by distance (default, less batching, less artifacts when widgets overlap) *(community CVar help)* | `ref_rva`: 1 `direct-memory-candidate`, 1 `address-taken`; direction and execution were not established. `obj_rva`: 3 `direct-memory-candidate`, 1 `address-taken`. |

## Scope and evidence limits

- The tooltip settings are described in seconds; no Marvel Rivals-specific animation timing was measured.
- The fullscreen transform controls describe mouse-coordinate correction for stretched resolutions and multi-screen layouts. The source help does not establish the supported display modes in this build.
- `Slate.UsingFontMaterialUnityUV` is only accompanied by a short community label; the precise material-coordinate behavior is not described in the available evidence.
- World-widget help describes skipping updates for invisible widgets and optionally ordering projected widgets by view distance. The scan does not prove which policy the game uses.
- This batch completes the 84 registered `Slate.*` names in the current catalog coverage review; the separate `UI.*` family is not included.

Sources: [community CVar registry](cvar-community-registry.md), [preserved registry and snapshot attachments](EVIDENCE.md#community-sources), and [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis).
