---
name: openxr
description: Answer questions about OpenXR by referencing local cloned repos. Use this skill whenever the user asks anything about OpenXR, XR/VR/AR runtimes, the OpenXR loader, API layers, sessions, swapchains, action/input systems, spaces and reference frames, view configurations, frame submission, OpenXR extensions, or the OpenXR conformance suite. Always consult the local repos before answering — do not rely solely on training knowledge.
---

# OpenXR Local Reference Skill

When answering any question about OpenXR, always consult the local repos first. They are located inside this skill's `references/` folder:

```
references/OpenXR-SDK/          ← Released headers (openxr.h, reflection) + loader build
references/OpenXR-SDK-Source/   ← Full source: loader, API layers, conformance tests, xr.xml registry
references/OpenXR-Docs/         ← Official OpenXR specification source (AsciiDoc)
references/OpenXR-Guide/        ← Conceptual guides and design philosophy
references/OpenXR-Registry/     ← Published spec snapshots (HTML/PDF), per-version man pages
```

## How to use the repos

### Answering API questions
1. Check `references/OpenXR-SDK/include/openxr/openxr.h` for the actual struct/enum/function signatures
2. Check `references/OpenXR-SDK/include/openxr/openxr_reflection.h` for enum↔string reflection macros
3. Check `references/OpenXR-Docs/specification/sources/chapters/` for spec language and usage rules
4. Cross-reference `references/OpenXR-SDK-Source/specification/registry/xr.xml` for the authoritative registry (extension numbers, struct types, version info)

### Answering loader / API-layer questions
1. Check `references/OpenXR-SDK-Source/src/loader/` for runtime/loader discovery and negotiation
2. Check `references/OpenXR-SDK-Source/src/api_layers/` for API layer implementation patterns
3. Check `references/OpenXR-SDK/include/openxr/openxr_loader_negotiation.h` for the loader↔runtime↔layer ABI

### Answering conceptual questions
- Prefer `OpenXR-Guide/chapters/` for high-level concepts (frame submission, design philosophy, "what is OpenXR")
- Prefer `OpenXR-Docs/specification/sources/chapters/` for precise spec-level answers
- Use `OpenXR-Registry/specs/<version>/man/html/` for quick per-symbol reference pages

### Answering extension questions
1. Look up the extension in `references/OpenXR-SDK-Source/specification/registry/xr.xml`
2. Read its chapter in `references/OpenXR-Docs/specification/sources/chapters/extensions/`
3. Confirm the symbols in `references/OpenXR-SDK/include/openxr/openxr.h`

## Key locations to know

| Repo | Key paths |
|------|-----------|
| OpenXR-SDK | `include/openxr/openxr.h`, `openxr_reflection.h`, `openxr_platform.h`, `openxr_loader_negotiation.h` |
| OpenXR-SDK-Source | `specification/registry/xr.xml`, `src/loader/`, `src/api_layers/`, `src/conformance/`, `src/tests/` |
| OpenXR-Docs | `specification/sources/chapters/` (`fundamentals.adoc`, `session.adoc`, `rendering.adoc`, `input.adoc`, `spaces.adoc`, `semantic_paths.adoc`, `view_configurations.adoc`), `chapters/extensions/`, `specification/sources/openxr.adoc` |
| OpenXR-Guide | `chapters/what_is_openxr.md`, `frame_submission.md`, `goals_design_philosophy.md` |
| OpenXR-Registry | `specs/1.1/html/xrspec.html`, `specs/1.1/man/html/<Symbol>.html` (also `1.0`, `1.0-khr`, `1.1-khr`, `0.90`) |

## Answering strategy

- **Always grep or read local files** before answering — training data may be outdated on extension support, spec revisions, or current OpenXR version
- When a struct or function is asked about, find its definition in `openxr.h` and read the relevant chapter in `OpenXR-Docs`
- For extensions, confirm the version number and dependencies via `xr.xml` rather than relying on memory
- Distinguish core spec behavior (Docs/SDK) from runtime-specific behavior — note when something is left to the runtime
- Cite which repo/file your answer comes from so the user can follow up
