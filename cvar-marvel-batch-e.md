# Marvel CVar batch E

This guide documents the final two currently uncovered registered `marvel.*` variables. Together with the preceding focused guides, this covers the 32 exact-case names in the supplied community registry. Community help, snapshot values, Epic UE 5.9 references, and Shipping-build address scans remain separate evidence types.

Snapshot values are observations, not defaults. Static reference matches do not prove access direction, execution, or startup override acceptance.

| Exact CVar | Type / kind | Snapshot | Epic 5.9 default | Supplied help and provenance | Build scan evidence and limits |
| --- | --- | --- | --- | --- | --- |
| `marvel.UsingBattlePanelV7` | bool (var: 1) | true | — | Community help: Using battle panel v7 | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime behavior not traced. |
| `marvel.UsingEnhancedActivateInput` | bool (var: 1) | true | — | Community help: 使用EnhancedInput激活技能 Object-table help: EnhancedInput Unreviewed assistant translation: Use Enhanced Input to activate abilities. | `ref_rva`: no recorded matches; `obj_rva`: 3 direct-memory candidate(s), 1 address-taking reference(s); runtime behavior not traced. |

## Interpretation limits

- Exact-name Epic descriptions/defaults do not confirm the game fork’s behavior or active path.
- Address-taking evidence alone does not establish a value read; direct-memory candidates may be reads, writes, comparisons, or initialization.
- The source registry does not identify its capture build or prove `.ini` editability.

Sources: [community CVar registry](cvar-community-registry.md), [build 1.1.4042190 address-reference scan](EVIDENCE.md#build-specific-static-analysis), and [build-specific CVar inventory](EVIDENCE.md#build-specific-static-analysis).
