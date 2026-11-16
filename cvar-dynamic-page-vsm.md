# Dynamic Page VSM CVars

The community registry has four undocumented `r.Shadow.DynamicPageVSM.*` references. In build 1.1.4042190, code reads all four in a shared initialization path; the `Enable` value also gates additional update work. The code supports describing how these settings feed the custom dynamic-page resource setup, but not their full visual effect or safe tuning range.

## Variables

| CVar | Type | Snapshot value | What the available evidence supports |
|---|---|---:|---|
| `r.Shadow.DynamicPageVSM.Enable` | int32 | `0` | In the examined update path, zero skips a follow-up call; a nonzero value can enter it when a local state value equals 1 (`0x141B3D242`–`0x141B3D258`). In another path, a change from a local value triggers the page-resource setup helper at `0x14232FE60` (`0x141B39308`–`0x141B3933A`). This supports an enable/state gate for dynamic-page VSM work, but does not prove that nonzero fully enables all VSM rendering. |
| `r.Shadow.DynamicPageVSM.PoolSize` | int32 | `4096` | Loaded at `0x14232FEBC` during setup of the dynamic-page resource object. The helper derives a power-of-two scale from the value and incorporates it into later dimension/capacity calculations. The accepted range, unit, and precise relationship to physical-page count are not recovered. |
| `r.Shadow.DynamicPageVSM.MinPageSize` | int32 | `128` | Loaded at `0x14232FF00`. In the same setup helper, a negative input is clamped to zero and the value can raise the computed size when it is larger than that size. The source does not identify the unit or whether this is a pixel dimension. |
| `r.Shadow.DynamicPageVSM.MaxPageSize` | int32 | `2048` | Loaded at `0x14232FF23` and combined with values returned by platform/helper calls before further sizing calculations. This supports an upper page-size bound in resource setup, but exact clamp order and limits are not fully reconstructed. |

## Build evidence

- Source metadata: the four names are `ref int32` rows in [`console_vars.tsv`](https://discord.com/channels/1512820805615091712/1512825591529869383/1570970983353950322). Their help fields are empty. The values above come from [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452); they are captured settings, not defaults or recommendations.
- Installed executable: `Marvel Rivals Shipping executable`, build 1.1.4042190, SHA-256 `omitted from this documentation-only project`.
- Direct-use candidates from [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included): 25 for `Enable`, and one each for `PoolSize`, `MinPageSize`, and `MaxPageSize`. The page-size and pool variables converge in setup code around `0x14232FEBC`–`0x14232FF63`; the `Enable` reads are in several separate functions.
- The registry also contains `r.AllowDebugDynamicPageVSM` with help text “Allow Debug Dynamic Page VSM.” This corroborates the feature label in the same configuration set, but does not define the four settings above.
- Epic's general Unreal Engine documentation explains that Virtual Shadow Maps use virtual pages and a physical page pool. That is upstream context only: it does not document Marvel Rivals' `DynamicPageVSM` variables or prove that the custom sizes map directly to Epic's standard 128×128 virtual tiles. See [Virtual Shadow Maps in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine).

## Practical limits

Treat this as a custom rendering-resource configuration group. The snapshot values do not reveal the shipped defaults, and no controlled render comparison was performed. Changing the pool or page-size values may alter resource allocation or shadow quality, but the executable evidence does not establish a performance direction, image-quality result, memory cost, or reliable override range. The four names remain in the [definition-gap worklist](cvar-unresolved-definitions.md) until those effects or the exact source-level fields are recovered.
