# OpenGL CVar batch A

This guide documents all 12 currently uncovered exact-case `OpenGL.*` variable/reference rows. The supplied community registry contains 12 such names. These descriptions identify the documented OpenGL backend paths; no supplied evidence establishes that this Windows game build selects OpenGL at runtime.

| Exact CVar | Type / kind | Snapshot | Epic UE 5.9 default | Meaning from supplied help | Build 1.1.4042190 address-scan candidates |
| --- | --- | --- | --- | --- | --- |
| `OpenGL.BindlessTexture` | `int32` (`ref`) | 0 | — | When enabled, use `GL_ARB_bindless_texture` rather than traditional `glBindTexture` / `glBindSampler` calls. | `ref_rva`: 6 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.MaxSubDataSize` | `int32` (`ref`) | 262144 | — | Maximum data size sent to `glBufferSubData` in one call. | `ref_rva`: 3 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.RebindTextureBuffers` | `int32` (`ref`) | 0 | — | When enabled, rebind `GL_TEXTURE_BUFFER` objects to their GL texture name whenever the underlying buffer changes. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.SkipCompute` | `int32` (`ref`) | 0 | — | When enabled, do not issue compute-dispatch work. | `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UBODirectWrite` | `int32` (`ref`) | 1 | — | Enables direct writes to uniform buffer objects through buffer storage. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 2 address-taking. These are unvalidated static candidates. |
| `OpenGL.UBOPoolSize` | `int32` (`ref`) | 16777216 | — | Size of the uniform-buffer-object pool; zero disables the pool. | `ref_rva`: 0 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UseBufferDiscard` | `int32` (`ref`) | 1 | — | When enabled, use the dynamic-buffer orphaning hint. | `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UseEmulatedUBs` | `int32` (`var`) | 1 | 1 | When enabled, use emulated uniform buffers in OpenGL Mobile mode; use in the game’s selected backend is unconfirmed. | `ref_rva`: 0 direct-memory / 0 address-taking; `obj_rva`: 2 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UseGlClipControlIfAvailable` | `int32` (`ref`) | 1 | — | When enabled, attempt to use `glClipControl` if the graphics driver supports it. | `ref_rva`: 1 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UseMapBuffer` | `int32` (`ref`) | 0 | — | When enabled, use `glMapBuffer`; otherwise use `glBufferSubData`. | `ref_rva`: 4 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UsePersistentMappingStagingBuffer` | `int32` (`ref`) | 1 | — | When enabled, use persistent mapping for the staging buffer. | `ref_rva`: 4 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |
| `OpenGL.UseStagingBuffer` | `int32` (`ref`) | 1 | — | Enables mapping dynamic vertex buffers through a staging buffer. | `ref_rva`: 2 direct-memory / 1 address-taking; `obj_rva`: 3 direct-memory / 1 address-taking. These are unvalidated static candidates. |

## Evidence limits

- Snapshot values are observations from `CVarDump.txt`, not verified game defaults or recommendations.
- `Epic UE 5.9 default` reports an exact-name comparison only. A dash means no matching default was recorded; this does not prove that the game uses UE 5.9.
- The community registry’s `var`/`ref` labels do not establish game-build registration or config writeability.
- Address-scan classes are candidate instructions referring to registry `ref_rva`/`obj_rva` locations. They were not control-flow-validated and do not prove runtime reads, writes, selected backend, or visible effect.
- No controlled runtime test established whether these values are accepted through the loader’s `[Overrides]` section.

Sources: [community CVar registry](cvar-community-registry.md), [Epic UE 5.9 comparison and captured values](cvar-community-registry.md), [preserved community attachments](EVIDENCE.md#community-sources), and [build-specific address-reference scan](EVIDENCE.md#build-specific-static-analysis).
