# LiveLink CVar batch A

This guide covers the seven `LiveLink.*` registry entries classified as variables. Their supplied descriptions concern LiveLink frame/static-data ingestion, component evaluation, timed-data buffering, smoothing, and clock-offset updates. The names and help indicate Unreal's LiveLink/timed-data subsystem; they do not establish that Marvel Rivals connects to a LiveLink source or uses these settings in normal gameplay.

Snapshot values are captured observations, not recommended or guaranteed defaults. The supplied registry has no Epic UE 5.9 reference values for these rows. Each name has static address-reference candidates in the scanned Shipping build 1.1.4042190, but the candidates do not prove runtime use or `.ini` acceptance.

| Exact name | Type / kind | Snapshot | Supplied help and practical reading | Build scan evidence |
| --- | --- | --- | --- | --- |
| `LiveLink.Client.MaxNewFrameDataPerUpdate` | `int32` (`var`) | `2048` | Maximum number of new frame-data items that may be added in one Unreal frame. This is a per-frame ingestion cap according to the help; the resulting latency or drop behavior is not specified. | 3 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.Client.MaxNewStaticDataPerUpdate` | `int32` (`var`) | `256` | Maximum number of new static-data items that may be added in one Unreal frame. The help does not describe what happens when the cap is reached. | 3 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.Component.EnableLiveLinkEvaluation` | `bool` (`var`) | `true` | Controls whether LiveLink components evaluate their subject. The description does not specify component classes, evaluation timing, or whether disabling it affects other systems. | 3 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.TimedDataInput.MaxBufferSize` | `int32` (`var`) | `200` | Upper bound on the buffer size that a timed-data input is allowed to set. The help does not define units or how the input chooses a size within the bounds. | 2 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.TimedDataInput.MinBufferSize` | `int32` (`var`) | `5` | Lower bound on the buffer size that a timed-data input is allowed to set. The help does not define units or behavior when configured bounds conflict. | 2 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.TimedDataInput.NumFramesForSmoothOffset` | `float` (`var`) | `1.5` | Fractional number of source frames used as an offset for smooth evaluation time. The description does not specify the interpolation formula or resulting delay. | 2 direct-memory candidates and 1 address-taken reference; static only. |
| `LiveLink.TimedDataInput.UpdateClockOffset` | `bool` (`var`) | `true` | Clock offset is continuously updated for each source by default; disabling this variable pauses updates and fixes the offset at its then-current value, according to supplied help. Re-enabling behavior is not described. | 2 direct-memory candidates and 1 address-taken reference; static only. |

## Interpretation and limits

- The source material describes LiveLink data and timed inputs. It does not show that these controls are exposed to players or affect Marvel Rivals matches.
- Static scanner counts are address-reference candidates in one build, not proof of registration, executed code, runtime reads/writes, or an effect.
- Whether the game's `[Overrides]` `.ini` loader accepts any of these settings remains unverified.
- The registry's spelling `Maximun` in two help strings is retained as source wording in meaning; the table paraphrases it as “maximum.”

## Sources

Names, types, help, and captured values are from the preserved [community source attachment notes](EVIDENCE.md#community-sources). Build inventory and scanner limitations are in the [build-specific CVar analysis](EVIDENCE.md#build-specific-static-analysis).
