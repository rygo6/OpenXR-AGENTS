# OpenXR-AGENTS

An agent skill that answers OpenXR questions by referencing locally cloned official repositories, rather than relying solely on training data. It is agent-agnostic and works with any coding agent that supports skills (Claude Code, Codex, etc.).

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/OpenXR-SDK` | Released headers (`openxr.h`, reflection headers) and loader build |
| `references/OpenXR-SDK-Source` | Loader, API layers, tests, and `xr.xml` registry |
| `references/OpenXR-CTS` | Conformance Test Suite: conformance framework, test cases, and validation layer |
| `references/OpenXR-Docs` | Official OpenXR specification source (AsciiDoc) |
| `references/OpenXR-Guide` | Conceptual guides and design philosophy |
| `references/OpenXR-Registry` | Published spec snapshots (HTML/PDF) and per-version man pages |

## Installation

Install once into the shared agent skills directory, then symlink it into each agent's skills folder.

The reference repositories are Git submodules. Initialize them without nested dependencies for
source lookup:

```bash
git clone git@github.com:rygo6/OpenXR-AGENTS.git ~/.agents/skills/openxr
cd ~/.agents/skills/openxr
git submodule update --init
```

Do not pass `--recursive` or clone with `--recurse-submodules`.

The commands above use the recorded reference revisions. To deliberately refresh existing
references, review local changes first, then run `git submodule update --remote` and inspect the result.

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

Once installed, request the `openxr` skill by name or use your agent’s skill picker or invocation syntax.
