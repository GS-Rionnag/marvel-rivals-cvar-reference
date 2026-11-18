# ImgMedia, NVENC, and Level Sequence CVars

This guide covers five registry variables in each of three exact-case namespaces. Snapshot values are captured observations, and a dash indicates that the snapshot has no entry. Defaults mentioned in the supplied help or community catalog are recorded separately from observations.

## ImgMedia

| Exact name | Type / kind | Snapshot | Supplied help |
| --- | --- | --- | --- |
| `ImgMedia.FieldOfViewMultiplier` | `float` / `var` | `1` | Multiplier applied to the active camera field of view for ImgMedia tile selection. The help describes widening frusta to mitigate missing-tile artifacts. |
| `ImgMedia.FrameInvalidationMaxCount` | `int32` / `var` | `2` | Maximum number of cached frames that can be invalidated when the newest mips or tiles are missing. |
| `ImgMedia.ICVFX.InnerOnlyTiles` | `bool` / `var` | `false` | Restricts tile calculations to Display Cluster inner viewports. With Media Plate upscaling, other viewports can show lower-resolution mips. Without upscaling, they show only the tiles loaded for the inner viewport. |
| `ImgMedia.MipMapDebug` | `bool` / `var` | `false` | Shows debug information for ImgMedia mipmaps and tiles. The help describes `0` as off and the default, and `1` as on. |
| `ImgMedia.MipMapLevelPadding` | `float` / `var` | `0` | Pads the loader's estimated minimum and maximum mip levels. The help leaves the exact rounding and clamping behavior unspecified. |

## NVENC

| Exact name | Type / kind | Snapshot | Supplied help |
| --- | --- | --- | --- |
| `NVENC.EnableStats` | `bool` / `var` | `false` | Enables NVENC statistics. The stated default is `false`. |
| `NVENC.IntraRefreshCountFrames` | `int32` / `var` | `0` | Number of frames used for intra refresh within each period. The help says smaller counts can speed stream recovery at the cost of bandwidth. The stated default is `0`. |
| `NVENC.IntraRefreshPeriodFrames` | `int32` / `var` | `0` | Number of frames between intra refreshes. Smaller positive values schedule refreshes more frequently. The stated default is `0`, and values at or below zero disable intra refresh. |
| `NVENC.KeyframeInterval` | `int32` / `var` | `300` | Sends an IDR (Instantaneous Decoder Refresh) frame every N frames. The stated default is `300`, and values at or below zero disable periodic IDR frames. |
| `NVENC.KeyframeQPUseLastQP` | `bool` / `var` | `true` | When enabled, keyframe quantization quality is at least as good as the last transmitted frame, potentially at a latency cost. When disabled, worse keyframe quality can accommodate network conditions and reduce latency. The stated default is `true`. |

## Level Sequence

| Exact name | Type / kind | Snapshot | Supplied help |
| --- | --- | --- | --- |
| `LevelSequence.DefaultClockSource` | `int32` / `var` | `0` | Default clock for newly created level sequences. The listed sources are `0` Tick, `1` Platform, `2` Audio, `3` RelativeTimecode, `4` Timecode, and `5` Custom. |
| `LevelSequence.DefaultDisplayRate` | `FString` / `var` | — | Default display frame rate for new sequences. This is also the playback frame rate for frame-locked sequences. The community catalog lists `30fps` as a default. |
| `LevelSequence.DefaultLockEngineToDisplayRate` | `int32` / `var` | `0` | The supplied help maps `0` to playback locked to playback frames and `1` to unlocked playback with subframe interpolation. |
| `LevelSequence.DefaultTickResolution` | `FString` / `var` | — | Default tick resolution for newly created sequences. The community catalog lists `24000fps` as a default. |
| `LevelSequence.InvalidBindingTagWarnings` | `bool` / `ref` | `true` | Controls whether invalid object binding tags used to override bindings emit warnings. |

The registry help for both rate strings gives examples including `30 fps`, `120/1`, `30000/1001`, and `0.01s`. The first two represent 30 and 120 frames per second, the third is approximately 29.97 frames per second, and the fourth is a 10 ms period. [Raw registry](EVIDENCE.md#community-sources)

## Build and source evidence

- All 15 names appear in the x64 and ARM64EC Shipping string inventories for build 1.1.4042190. The local community catalog includes UE 5.9 help matches for `ImgMedia.MipMapDebug` and `LevelSequence.DefaultLockEngineToDisplayRate`, with no upstream default listed for either. [Build string inventory](EVIDENCE.md#build-specific-static-analysis) · [Community registry](EVIDENCE.md#community-sources)
- The x64 address scan has three direct-memory candidates and one address-taking instruction against `obj_rva` for each ImgMedia variable and each Level Sequence `var`. For `LevelSequence.InvalidBindingTagWarnings`, the counts are two direct-memory candidates and one address-taking instruction against `obj_rva`, plus three and one respectively against `ref_rva`. Each NVENC variable has two direct-memory candidates against `obj_rva`. The two NVENC booleans also have two address-taking instructions each, and the three NVENC integers have one each. [Address-reference scan](EVIDENCE.md#build-specific-static-analysis)
- The source attachments have unspecified capture builds. String and address matches leave feature usage, runtime effects, and startup override support unverified in Marvel Rivals. [Raw snapshot](EVIDENCE.md#community-sources) · [Source notes](EVIDENCE.md#community-sources)
