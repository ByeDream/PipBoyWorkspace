# pip-boy-workspace

A multi-project workspace for [Pip-Boy](https://github.com/ByeDream/Pip-Boy),
a personal assistant agent built on top of Claude Code.

This repository is **the habitat**, not the source code. It pins a Pip-Boy
version, ships a workspace-level operating manual (`CLAUDE.md`) that the
agent loads on every turn, and reserves a `workspace/` directory for
independent projects the agent works on.

## Layout

```
.
├── CLAUDE.md            # Pip-Boy's standing order for this workspace
├── README.md            # this file
├── requirements.txt     # pins pip-boy
├── .gitignore           # ignores .venv, .pip, .env*, workspace/*
└── workspace/           # gitignored; each subdir is an independent project
    └── .gitkeep
```

When you first run Pip-Boy, it scaffolds its own runtime state under
`.pip/` (memory, cron, addressbook, themes, …). That directory is
gitignored — it is per-machine state, not source.

## Bootstrap

```powershell
# 1. Clone the workspace repo
git clone <this-repo-url> PipBoyWorkspace
cd PipBoyWorkspace

# 2. Create the venv
python -m venv .venv

# 3. Activate it
#    Windows PowerShell:
.\.venv\Scripts\Activate.ps1
#    macOS / Linux:
# source .venv/bin/activate

# 4. Install Pip-Boy
pip install -r requirements.txt

# 5. First run
pip-boy doctor                 # read-only env + capability self-check
pip-boy                        # start the host (TUI by default; line mode as fallback).
                               # On first run this scaffolds .pip/ and writes .env at the workspace root.

# 6. Edit .env at the workspace root and fill in ANTHROPIC_API_KEY
#    (and ANTHROPIC_BASE_URL if you go through a proxy gateway), then
#    re-run pip-boy.
```

## Adding a project

Projects live under `workspace/`. The directory is gitignored, so each
project keeps its own git history independently.

```powershell
# Either clone an existing repo:
git clone <project-url> workspace/<project-name>

# Or scaffold a new one:
mkdir workspace/<project-name>
```

Then ask Pip-Boy to update its project registry — it will edit the
**Projects** table in `CLAUDE.md` to reflect the new entry. See
`CLAUDE.md` §5 for the full add / remove / rename contract the agent
follows.

## Updating Pip-Boy

```powershell
.\.venv\Scripts\Activate.ps1
pip install --upgrade pip-boy
```

To pin a specific version, edit `requirements.txt` and re-run
`pip install -r requirements.txt`.

## Why a separate workspace repo?

- **Reproducible bootstrap** — clone the workspace, create a venv, install,
  done. The agent's habitat travels with you.
- **Stable cross-project memory** — Pip-Boy's persistent memory lives in
  `.pip/`, anchored to this directory. Pointing the agent at random cwd's
  fragments its memory across many `.pip/` instances.
- **Clear separation of concerns** — workspace governs *how the agent
  operates*; each project governs *what the agent works on*. The two
  evolve independently.

## License

MIT.
