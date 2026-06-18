# Claude OpenXR Skill

A Claude Code skill that answers OpenXR questions by referencing locally cloned official repositories, rather than relying solely on training data.

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/OpenXR-SDK` | Released headers (`openxr.h`, reflection headers) and loader build |
| `references/OpenXR-SDK-Source` | Full source: loader, API layers, conformance tests, `xr.xml` registry |
| `references/OpenXR-Docs` | Official OpenXR specification source (AsciiDoc) |
| `references/OpenXR-Guide` | Conceptual guides and design philosophy |
| `references/OpenXR-Registry` | Published spec snapshots (HTML/PDF) and per-version man pages |

## Installation

Clone with `--recurse-submodules` — the reference repos are git submodules:

```bash
git clone --recurse-submodules https://github.com/rygo6/OpenXR-AGENTS.git ~/.claude/skills/openxr
cd ~/.claude/skills/openxr
git submodule update --remote
```

## Usage

Once installed open Claude Code and run `/openxr`.
