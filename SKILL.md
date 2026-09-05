---
name: openxr
description: Use local Khronos specifications, SDK headers, loader source, and conformance tests to answer questions and develop or debug OpenXR code. Use for OpenXR sessions, swapchains, input, spaces, frame submission, extensions, loaders, and API layers. Use webxr for the browser API.
---

# OpenXR Local Reference Skill

Search the relevant local sources before answering technical questions. Paths below are relative to this skill directory; read only the sources needed for the request.

```text
references/OpenXR-SDK/              ← Released headers (openxr.h, reflection) + loader build
references/OpenXR-SDK-Source/       ← Loader, API layers, tests, and xr.xml registry
references/OpenXR-CTS/              ← Conformance Test Suite: conformance framework, test cases, runtime validation
references/OpenXR-Docs/             ← Official OpenXR specification source (AsciiDoc)
references/OpenXR-Guide/            ← Conceptual guides and design philosophy
references/OpenXR-Registry/         ← Published spec snapshots (HTML/PDF), per-version man pages
```

Use `webxr` for browser XR API questions. For OpenXR, identify the target API version, enabled extensions, graphics binding, and runtime where these affect the answer.

## How to use the repos

### Answering API questions

1. Check `references/OpenXR-SDK/include/openxr/openxr.h` for the actual struct/enum/function signatures.
2. Check `openxr_platform.h` for platform and graphics-binding declarations, and `openxr_reflection.h` when enum reflection is relevant. Both are under `references/OpenXR-SDK/include/openxr/`.
3. Check `references/OpenXR-Docs/specification/sources/chapters/` for spec language and usage rules.
4. Cross-reference `references/OpenXR-SDK-Source/specification/registry/xr.xml` for the authoritative registry (extension numbers, struct types, version info).

### Answering loader / API-layer questions

1. Check `references/OpenXR-SDK-Source/src/loader/` for runtime/loader discovery and negotiation.
2. Check `references/OpenXR-SDK-Source/src/api_layers/` for API layer implementation patterns.
3. Check `references/OpenXR-SDK/include/openxr/openxr_loader_negotiation.h` for the loader↔runtime↔layer ABI.

### Answering conformance / testing questions

1. Prefer `references/OpenXR-CTS/` — the dedicated Conformance Test Suite repo.
2. Check `references/OpenXR-CTS/src/conformance/framework/` for the test harness and helpers.
3. Check `references/OpenXR-CTS/src/conformance/conformance_test/` for the actual test cases per feature/extension.
4. Check `references/OpenXR-CTS/src/conformance/conformance_layer/` for the validation API layer used during testing.
5. See `references/OpenXR-CTS/src/conformance/README.md` and `BUILDING.md` for how the suite is run and structured.

### Answering conceptual questions

- Prefer `OpenXR-Guide/chapters/` for high-level concepts (frame submission, design philosophy, "what is OpenXR").
- Prefer `OpenXR-Docs/specification/sources/chapters/` for precise spec-level answers.
- Use `OpenXR-Registry/specs/<version>/man/html/` for quick per-symbol reference pages.

### Answering extension questions

1. Look up the extension in `references/OpenXR-SDK-Source/specification/registry/xr.xml`.
2. Read its chapter in `references/OpenXR-Docs/specification/sources/chapters/extensions/`.
3. Confirm the symbols in `references/OpenXR-SDK/include/openxr/openxr.h`.

## Key locations to know

| Repo | Key paths |
|------|-----------|
| OpenXR-SDK | `include/openxr/openxr.h`, `openxr_reflection.h`, `openxr_platform.h`, `openxr_loader_negotiation.h` |
| OpenXR-SDK-Source | `specification/registry/xr.xml`, `src/loader/`, `src/api_layers/`, `src/tests/` |
| OpenXR-CTS | `src/conformance/framework/`, `src/conformance/conformance_test/`, `src/conformance/conformance_layer/`, `src/conformance/conformance_cli/`, `src/conformance/README.md`, `BUILDING.md` |
| OpenXR-Docs | `specification/sources/chapters/` (`fundamentals.adoc`, `session.adoc`, `rendering.adoc`, `input.adoc`, `spaces.adoc`, `semantic_paths.adoc`, `view_configurations.adoc`), `chapters/extensions/`, `specification/sources/openxr.adoc` |
| OpenXR-Guide | `chapters/what_is_openxr.md`, `frame_submission.md`, `goals_design_philosophy.md` |
| OpenXR-Registry | `specs/1.1/html/xrspec.html`, `specs/1.1/man/html/<Symbol>.html` (also `1.0`, `1.0-khr`, `1.1-khr`, `0.90`) |

## Answering strategy

- When a struct or function is asked about, find its definition in `openxr.h` and read the relevant chapter in `OpenXR-Docs`.
- For extensions, confirm the version number and dependencies via `xr.xml` rather than relying on memory.
- Distinguish core spec behavior (Docs/SDK) from runtime-specific behavior — note when something is left to the runtime.
- Cite the source files and relevant sections used. Make local file links resolvable from the user's workspace.

## Reference availability and versions

- Local checkouts are snapshots. Match the sources to the user's target version; verify current claims against official upstream sources when freshness matters. Do not silently update existing checkouts.
- If a needed submodule is missing, initialize only that reference with `git submodule update --init -- references/<repo>` from this skill directory. Omit `--recursive`; nested build dependencies are unnecessary for source lookup.
- If a source remains unavailable, state the limitation and use an official upstream source when accessible. Do not present an unverified recollection as a source-backed conclusion.
