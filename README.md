# OpenXR-AGENTS

An agent skill that answers OpenXR questions by referencing locally cloned official repositories, rather than relying solely on training data. It is agent-agnostic and works with any coding agent that supports skills (Claude Code, Codex, etc.).

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/OpenXR-SDK` | Released headers (`openxr.h`, reflection headers) and loader build |
| `references/OpenXR-SDK-Source` | Full source: loader, API layers, conformance tests, `xr.xml` registry |
| `references/OpenXR-Docs` | Official OpenXR specification source (AsciiDoc) |
| `references/OpenXR-Guide` | Conceptual guides and design philosophy |
| `references/OpenXR-Registry` | Published spec snapshots (HTML/PDF) and per-version man pages |

## Installation

Install once into the shared agent skills directory, then symlink it into each agent's skills folder.

Clone with `--recurse-submodules` — the reference repos are git submodules:

```bash
git clone --recurse-submodules git@github.com:rygo6/OpenXR-AGENTS.git ~/.agents/skills/openxr
cd ~/.agents/skills/openxr
git submodule update --remote
```

Then link it into the agents you use:

```bash
mkdir -p ~/.claude/skills ~/.codex/skills
ln -s ~/.agents/skills/openxr ~/.claude/skills/openxr
ln -s ~/.agents/skills/openxr ~/.codex/skills/openxr
```

## Usage

Once installed, invoke `/openxr` from any agent that supports skills.
