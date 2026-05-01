# CLAUDE.md — Pip-Boy Workspace Operating Manual

This file is your top-level standing order for how to work here. It is
loaded automatically by the Claude Agent SDK on every turn.

---

## 1. What this workspace is

This directory is a **multi-project workspace**. It is **not** a single
codebase — it is a habitat from which you operate across many independent
projects.

```
<workspace-root>/                    ← you are here
├── .pip/                            ← your runtime state (memory, cron, addressbook, …)
│   └── log/pip-boy.log              ←   rotating host log — first place to look when something looks off
├── .venv/                           ← Python venv that has pip-boy installed
├── CLAUDE.md                        ← this file — workspace-level standing order
├── README.md                        ← human-facing bootstrap guide
├── requirements.txt                 ← pins pip-boy
└── workspace/                       ← all managed projects live here
    ├── .gitkeep                     ← placeholder; the rest is gitignored
    ├── <ProjectA>/                  ← each project is self-contained
    ├── <ProjectB>/
    └── …
```

Key facts:

- **The workspace root is tracked** by git (this repo: `pip-boy-workspace`),
  but everything under `workspace/` is **gitignored** except the placeholder.
  Each project under `workspace/` manages its own version control
  (git, p4, hg, svn, or none at all), dependencies, and conventions.
- You are a **cross-project agent**. You may be asked in a single session
  to add a project, fix a bug in another, then archive a third. Treat each
  project as an independent island.

---

## 2. Projects currently in this workspace

> Single source of truth for what lives under `workspace/`. Keep it in
> sync with reality.

| Project | Path | Origin | Description |
|---|---|---|---|
| _(none yet)_ | — | — | The workspace is empty. |

---

## 3. Work Rules

- When a request targets a project, anchor on `workspace/<project>/` and read its `AGENTS.md` / `CLAUDE.md` before doing anything else.
- Project-level rules override anything in this file.
- §2 must match what is on disk; update it whenever projects are added, removed, or renamed.
- If the target project is missing from §2 or ambiguous, ask the user — don't guess.
- Projects live under `workspace/<name>/` and stay out of this workspace repo's commits.
- This workspace repo is just an init template; root edits (e.g. §2) stay local — no commits needed.
- `.venv/` is the only place to `pip install`; `.pip/` is your runtime state — don't hand-edit it.
- For host-side trouble, read `.pip/log/pip-boy.log` first.
