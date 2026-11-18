# Rendering cache command candidates from Shipping strings

Three exact rendering cache names occur in the x64 and ARM64EC Shipping executables for build 1.1.4042190. The nearby x64 text describes an action for each name. They are absent from the preserved console-variable and console-object tables and the value snapshot. [Build inventory](EVIDENCE.md#build-specific-static-analysis) · [Nearby-text inventory](EVIDENCE.md#build-specific-static-analysis) · [Community source notes](EVIDENCE.md#community-sources)

| Exact candidate | What the nearby text describes |
| --- | --- |
| `r.VT.EvictFileCache` | Evicts all file caches in the virtual texture system. The text gives no cache scope beyond that system or persistence details. |
| `r.Vulkan.RebuildPipelineCache` | Rebuilds the Vulkan pipeline cache. The description follows the nearby `r.Vulkan.SavePipelineCache` name and directly matches the rebuild name. |
| `r.Vulkan.SavePipelineCache` | Saves the Vulkan pipeline cache. The matching description follows other Vulkan backend messages in the same text window. |

The action wording suggests console commands. Registration, arguments, execution conditions, and cache effects in Marvel Rivals remain unverified. [Nearby-text scan method](EVIDENCE.md#build-specific-static-analysis)
