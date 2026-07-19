---
name: openxr
description: Answer questions about OpenXR and WebXR by referencing local cloned repos. Use this skill whenever the user asks anything about OpenXR, XR/VR/AR runtimes, the OpenXR loader, API layers, sessions, swapchains, action/input systems, spaces and reference frames, view configurations, frame submission, OpenXR extensions, the OpenXR conformance suite, or the WebXR Device API (the browser-facing XR spec). Always consult the local repos before answering — do not rely solely on training knowledge.
---

# OpenXR Local Reference Skill

When answering any question about OpenXR, always consult the local repos first. They are located inside this skill's `references/` folder:

```
references/OpenXR-SDK/          ← Released headers (openxr.h, reflection) + loader build
references/OpenXR-SDK-Source/   ← Full source: loader, API layers, conformance tests, xr.xml registry
references/OpenXR-CTS/          ← Conformance Test Suite: conformance framework, test cases, runtime validation
references/OpenXR-Docs/         ← Official OpenXR specification source (AsciiDoc)
references/OpenXR-Guide/        ← Conceptual guides and design philosophy
references/OpenXR-Registry/     ← Published spec snapshots (HTML/PDF), per-version man pages
references/WebXR/               ← WebXR Device API spec source (Bikeshed) + explainers
```

> OpenXR is the native runtime API; WebXR is the browser-facing API. They are distinct specs from different bodies (Khronos vs. W3C Immersive Web WG). Consult `references/WebXR/` only for WebXR questions, `references/OpenXR-*` for native OpenXR questions.

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

### Answering conformance / testing questions
1. Prefer `references/OpenXR-CTS/` — the dedicated Conformance Test Suite repo
2. Check `references/OpenXR-CTS/src/conformance/framework/` for the test harness and helpers
3. Check `references/OpenXR-CTS/src/conformance/conformance_test/` for the actual test cases per feature/extension
4. Check `references/OpenXR-CTS/src/conformance/conformance_layer/` for the validation API layer used during testing
5. See `references/OpenXR-CTS/src/conformance/README.md` and `BUILDING.md` for how the suite is run and structured

### Answering WebXR (browser API) questions
1. The normative spec lives entirely in `references/WebXR/index.bs` (Bikeshed source) — grep it for interfaces (`XRSession`, `XRFrame`, `XRReferenceSpace`, `XRWebGLLayer`, etc.), IDL, and algorithm steps
2. For conceptual / non-normative context, read the explainers at the repo root:
   - `explainer.md` — overall WebXR Device API overview
   - `input-explainer.md` — input sources, select events, targeting
   - `spatial-tracking-explainer.md` — reference spaces, viewer/local/bounded/unbounded tracking
   - `privacy-security-explainer.md` — permissions, user consent, data exposure
   - `accessibility-considerations-explainer.md` — accessibility guidance
   - `webvr-migration.md` — migrating from the legacy WebVR API
3. The core Device API is only one module — AR, layers, hand input, depth sensing, anchors, etc. live in separate `immersive-web` repos not vendored here; note that when a feature isn't in `index.bs`

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
| OpenXR-CTS | `src/conformance/framework/`, `src/conformance/conformance_test/`, `src/conformance/conformance_layer/`, `src/conformance/conformance_cli/`, `src/conformance/README.md`, `BUILDING.md` |
| OpenXR-Docs | `specification/sources/chapters/` (`fundamentals.adoc`, `session.adoc`, `rendering.adoc`, `input.adoc`, `spaces.adoc`, `semantic_paths.adoc`, `view_configurations.adoc`), `chapters/extensions/`, `specification/sources/openxr.adoc` |
| OpenXR-Guide | `chapters/what_is_openxr.md`, `frame_submission.md`, `goals_design_philosophy.md` |
| OpenXR-Registry | `specs/1.1/html/xrspec.html`, `specs/1.1/man/html/<Symbol>.html` (also `1.0`, `1.0-khr`, `1.1-khr`, `0.90`) |
| WebXR | `index.bs` (full spec source), `explainer.md`, `input-explainer.md`, `spatial-tracking-explainer.md`, `privacy-security-explainer.md`, `accessibility-considerations-explainer.md`, `webvr-migration.md` |

## Answering strategy

- **Always grep or read local files** before answering — training data may be outdated on extension support, spec revisions, or current OpenXR version
- When a struct or function is asked about, find its definition in `openxr.h` and read the relevant chapter in `OpenXR-Docs`
- For extensions, confirm the version number and dependencies via `xr.xml` rather than relying on memory
- Distinguish core spec behavior (Docs/SDK) from runtime-specific behavior — note when something is left to the runtime
- Cite which repo/file your answer comes from so the user can follow up
