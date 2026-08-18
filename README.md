# OpenXR-AGENTS

An agent skill that answers OpenXR questions by referencing locally cloned official repositories, rather than relying solely on training data. It is agent-agnostic and works with any coding agent that supports skills (Claude Code, Codex, etc.).

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/OpenXR-SDK` | Released headers (`openxr.h`, reflection headers) and loader build |
| `references/OpenXR-SDK-Source` | Full source: loader, API layers, conformance tests, `xr.xml` registry |
| `references/OpenXR-CTS` | Conformance Test Suite: conformance framework, test cases, and validation layer |
| `references/OpenXR-Docs` | Official OpenXR specification source (AsciiDoc) |
| `references/OpenXR-Guide` | Conceptual guides and design philosophy |
| `references/OpenXR-Registry` | Published spec snapshots (HTML/PDF) and per-version man pages |

## Installation

Install once into the shared agent skills directory, then symlink it into each agent's skills folder.

The reference repos are git submodules. Initialize them one level deep only — they are read-only
references that are never built, so nested build dependencies are pure overhead:

```bash
git clone git@github.com:rygo6/OpenXR-AGENTS.git ~/.agents/skills/openxr
cd ~/.agents/skills/openxr
git submodule update --init
git submodule update --remote
```

Do not pass `--recursive` or clone with `--recurse-submodules`.

Then link it into the agents you use:

```bash
mkdir -p ~/.claude/skills ~/.codex/skills
ln -s ~/.agents/skills/openxr ~/.claude/skills/openxr
ln -s ~/.agents/skills/openxr ~/.codex/skills/openxr
```

On Windows, use `mklink /J` to create a junction instead (run in `cmd`, no admin rights needed):

```bat
mklink /J "%USERPROFILE%\.claude\skills\openxr" "%USERPROFILE%\.agents\skills\openxr"
mklink /J "%USERPROFILE%\.codex\skills\openxr"  "%USERPROFILE%\.agents\skills\openxr"
```

## Usage

Once installed, invoke `/openxr` from any agent that supports skills.
