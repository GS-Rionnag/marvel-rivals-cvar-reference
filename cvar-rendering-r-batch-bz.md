# Vulkan rendering CVars (batch BZ)

These are the next 25 uncovered exact `r.*` variable names in community registry order after [batch BY](cvar-rendering-r-batch-by.md), following the entries already covered by [Vulkan batch A](cvar-rendering-vulkan-batch-a.md). They cover Vulkan diagnostics, memory allocation, pipeline caches, ray tracing, and command submission. All are `int32` except `r.Vulkan.RayTracing.TLASPreferFastTraceTLAS`, which is `bool`.

The snapshot column records captured values. Defaults mentioned in the descriptions come from community help. The local Epic UE 5.9 comparison has no exact-name entries for this batch.

| Exact CVar | Kind | Snapshot | Meaning from supplied help | `ref_rva` memory candidates | `obj_rva` memory candidates |
| --- | --- | --- | --- | ---: | ---: |
| `r.Vulkan.IgnoreCPUReads` | `ref` | `0` | GPU-to-CPU readback diagnostic. `0` reads from the GPU and is the help-stated default. `1` substitutes zeros. | 5 | 3 |
| `r.Vulkan.InputAttachmentShaderRead` | `ref` | `0` | Input attachment access-mask workaround. `0` uses `VK_ACCESS_INPUT_ATTACHMENT_READ_BIT` and is the help-stated default. `1` adds `VK_ACCESS_SHADER_READ_BIT`. | 2 | 3 |
| `r.Vulkan.KeepSwapChain` | `ref` | `1` | Whether to pass the old swap chain when creating the next one. | 1 | 3 |
| `r.Vulkan.LogEvictStatus` | `ref` | `0` | Logs eviction status every frame. | 1 | 3 |
| `r.Vulkan.MemoryBacktrace` | `ref` | `10` | `0` records the source file and line. A nonzero value enables a backtrace with that many steps. | 0 | 3 |
| `r.Vulkan.MemoryFallbackToHost` | `ref` | `1` | `0` retains the legacy crash behavior when render-target allocation runs out of memory. `1` falls back to host memory. | 3 | 3 |
| `r.Vulkan.PSOLRUEvictAfterUnusedFrames` | `ref` | `0` | A positive value sets how many frames an unused pipeline state object (PSO) can stay in the least-recently-used (LRU) cache before destruction. The help names `0` as the default and says it disables age-based eviction. Eviction can save memory and increase hitching. | 2 | 3 |
| `r.Vulkan.PipelineCacheCompression` | `ref` | `1` | Controls compression of the Vulkan pipeline cache file on disk. | 0 | 3 |
| `r.Vulkan.PipelineCacheFromShaderPipelineCache` | `var` | `0` | `0` looks for the Vulkan pipeline cache under its usual paths and names. `1` ties it to the shader pipeline cache and includes the PSO file cache GUID in its filename. | 0 | 3 |
| `r.Vulkan.PipelineCacheLoad` | `var` | `1` | `0` disables loading the pipeline cache. `1` enables using it. | 0 | 3 |
| `r.Vulkan.PipelineDebugForceEvictImmediately` | `var` | `0` | Debug setting. `1` immediately evicts every newly created PSO. | 0 | 2 |
| `r.Vulkan.PipelineLRUCacheEvictBinary` | `var` | `0` | `0` creates pipelines from the binary PSO and shader caches and evicts them as the cache fills. `1` immediately evicts the entries and skips pipeline creation. | 0 | 2 |
| `r.Vulkan.PipelineLRUCacheEvictBinaryPreloadScreen` | `var` | `0` | `1` shows a preload screen while loading PSOs subject to immediate eviction through `r.Vulkan.PipelineLRUCacheEvictBinary`. | 0 | 2 |
| `r.Vulkan.PipelineLRUCapactiy` | `var` | `8192` | Maximum PSO count in the LRU cache. `Capactiy` is the registry spelling. | 0 | 2 |
| `r.Vulkan.PipelineLRUSize` | `var` | `536870912` | Maximum shader memory size. The help leaves the unit unspecified. | 0 | 2 |
| `r.Vulkan.ProfileCmdBuffers` | `ref` | `0` | Inserts GPU timing queries in every command buffer. | 3 | 3 |
| `r.Vulkan.RHIThread` | `var` | `2` | `0` uses only the render thread. `1` uses one Render Hardware Interface (RHI) thread. `2` uses multiple RHI threads. | 0 | 2 |
| `r.Vulkan.RayTracing` | `var` | `1` | `0` disables Vulkan ray tracing extensions. `1` enables experimental ray tracing support and is the help-stated default. | 0 | 2 |
| `r.Vulkan.RayTracing.AllowCompaction` | `ref` | `1` | Controls automatic compaction of static acceleration structures to save GPU memory. The help names `1` as the default. | 3 | 3 |
| `r.Vulkan.RayTracing.MaxBatchedCompaction` | `ref` | `64` | Per-frame maximum for compaction requests and rebuilds. The help names `64` as the default. | 2 | 3 |
| `r.Vulkan.RayTracing.TLASPreferFastTraceTLAS` | `ref` | `true` | Prefers fast tracing when building the top-level acceleration structure (TLAS). The help names `true` as the default. | 2 | 3 |
| `r.Vulkan.ReleaseShaderModuleWhenEvictingPSO` | `ref` | `0` | `0` retains shader modules after PSO eviction and is the help-stated default. `1` destroys them during eviction. The help describes a tradeoff between saving memory and increasing CPU cost or hitching. | 1 | 3 |
| `r.Vulkan.RobustBufferAccess` | `var` | `1` | `0` disables robust buffer access. `1` enables it and is the help-stated default. | 0 | 2 |
| `r.Vulkan.SingleAllocationPerResource` | `ref` | `0` | Uses a single allocation per resource when enabled. | 2 | 3 |
| `r.Vulkan.SubmitAfterEveryEndRenderPass` | `ref` | `0` | `1` forces a submit after every render pass ends. `0` disables this behavior and is the help-stated default. | 2 | 3 |

The memory columns count direct-memory candidates in the Shipping 1.1.4042190 static scan. The scan also found one address-taking instruction for each listed `obj_rva` and one for each `ref` entry's `ref_rva`. Memory matches can include initialization and writes. A zero count leaves indirect and other unscanned uses unresolved. The registry, snapshot, and scan leave Vulkan backend activation, `.ini` acceptance, and runtime effects unverified.

Registry help and captured values are preserved in the [community CVar sources](EVIDENCE.md#community-sources). The [address-match TSV](EVIDENCE.md#build-specific-static-analysis) and [build analysis](EVIDENCE.md#build-specific-static-analysis) provide the static scan details.
