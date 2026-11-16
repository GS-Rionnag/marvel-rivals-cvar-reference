# `AbilitySystem.ServerAttributeMergeSameAny.Enable`

This guide records the verified local-build behavior for one undocumented ability-system CVar. The captured snapshot value is `0`; that is an observed value, not a default or recommendation.

## Evidence

- The community registry row classifies the name as `kind=ref`, `vtype=int32`, with blank help and `ref_rva=0x100C22B0`.
- The local 1.1.4042190 x64 Shipping executable has fourteen direct-reference candidates for that ref address in [`build-4042190-cvar-address-hits.tsv`](EVIDENCE.md#evidence-artifacts-not-included). The registration-like pattern is also summarized in [the registration evidence guide](cvar-registration-evidence-4042190.md).
- The snapshot entry is in [`CVarDump.txt`](https://discord.com/channels/1512820805615091712/1512825591529869383/1562934699502866452). Its capture method and build are not recorded.

## What the code shows

The CVar is not used as a simple boolean at every inspected site:

- At `0x14660A747`, zero selects helper `0x146629C70`, while any nonzero value selects `0x146629DB0`.
- At `0x146629DB0`, the helper first checks bytes at offsets `0x10` and `0x12` in each of its two input records. If all four bytes are zero, values below `2` return success at that point. Values `>= 2` additionally compare data rooted at offset `0x6B0` in both records through helper `0x1432B5570`; a failed comparison returns false.
- At `0x14662CE04`, zero and nonzero values again select different helpers (`0x14662C7A0` and `0x14662CE70`) in a collection-processing path. Other direct reads occur while preparing or updating ability-attribute state.

Together, these instructions show at least three effective code regions: `0`, `1`, and `2 or higher`. This is a conclusion about the observed branches, not proof that all integer values are accepted or intended. The name associates the setting with server-side “merge same any” attribute processing, but the input structures, compared field at `+0x6B0`, equality rules in the alternate helper, and networking consequences have not been recovered.

## Practical limits

The binary evidence establishes that changing the value can select different comparison paths. It does not establish which mode the server uses in a live match, whether clients can influence authoritative state, what a safe value is, or whether any value improves performance. Keep the captured `0` separate from defaults and recommendations. Do not describe this as a networking or gameplay fix without controlled runtime evidence.

This guide is for build 1.1.4042190, whose executable SHA-256 is recorded in the [CVar source notes](EVIDENCE.md#build-specific-static-analysis). Address-based findings can change between builds.
