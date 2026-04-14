---
layout: aivalueworx-base.njk
title: "Quick Start Guide.<br><strong>Use this on every working day.</strong>"
eyebrow: "AI Value Worx — Workflow Management System"
meta: "Operating guide · Post-build reference · April 2026"
navTitle: "Quick start (post-build)"
navSection: "Guides"
order: 2
permalink: "/docs/quick-start-guide.html"
description: "Day-to-day operating reference for the WMS. Start here after the build session."
---

This guide assumes the WMS has already been built from Spec A and Spec B. If you haven't built it yet, start with the [Week One Deployment Guide](/docs/wms-first-deployment.html). If you are mapping your own tools rather than using Claude Desktop, Cursor, and Claude Code, read the [Tool Mapping Guide](/docs/wms-tool-mapping.html) first.

Full detail lives in `WORKFLOW_MANAGEMENT_SYSTEM_SPEC_A.md` and `WORKFLOW_MANAGEMENT_SYSTEM_SPEC_B.md`.


<div class="divider"></div>


## How tools and files fit together

You bring **intent** (what to build, constraints, approvals). The WMS brings **structure** (where state lives, what gets written, and which tool may write it).

```
YOU (human)                         REPOSITORY (files + git)
-----------                         ------------------------
Goals, questions, decisions         dashboard.json ......... task state machine
"Do the cleanup" / open Cursor      INDEX.md ............... session navigation
Uploads config in Claude Desktop    REGISTRY.md ............ numbered asset list
Approve scope / cost / model use    COMPOUND.md ............ engineering taste
Run terminal commands when asked    SKILL_*.md ............. institutional memory
                                    *.md briefings ......... handoffs between tools
                                    CLAUDE.md / .mdc ....... standing rules
```

### One cycle in plain language

1. **You** tell **Claude Desktop** what you want; it reads live `dashboard.json` and `INDEX.md` via the filesystem MCP.
2. **Claude Desktop** writes a **briefing** only — never directly to governed files. If it writes to a governed file directly, that change has no briefing and cannot be traced to a decision. Treat any direct write as an error to be reverted.
3. **Cursor** (or **Claude Code**) executes the briefing: Cursor updates governed files and commits; Code runs builds and scripts.
4. `validate_dashboard.py` keeps `dashboard.json` and `INDEX.md` consistent.
5. `//clean-up//` produces a cleanup briefing; **Cursor** applies it so session log, registry, compound doc, and dashboard state match what actually happened.

{% callout "blue" %}
**Reference implementation note:** Claude Desktop, Cursor, and Claude Code are the tools this guide is written against. They are not the only options. If your organisation uses a different AI stack, the **[Tool Mapping Guide](/docs/wms-tool-mapping.html)** shows how your existing tools map to the three WMS roles. You can build this system without adopting any new tools.
{% endcallout %}


<div class="divider"></div>


## One-time setup — about 15 minutes on a personal machine

### Step 1 — Tools

- **Cursor** — applies briefings and commits governed files
- **Claude Desktop** — design sessions, reads live state, writes briefings
- **Claude Code** — runs scripts and pipelines from briefings
- **Python 3** — validator and dashboard server
- **Git** — this repo already has a pre-commit hook installed

### Step 2 — Python dependencies

```bash
pip install -r requirements.txt
```

Optional — for automatic notifications when briefing files appear:

```bash
pip install watchdog plyer
```

### Step 3 — Claude Desktop

Point the **filesystem MCP** at this repository root. Full configuration at [docs.anthropic.com](https://docs.anthropic.com).

In **project uploads**, add stable files: SKILL files, `COMPOUND.md`, and specs under `docs/`. Do **not** put `dashboard.json` or `INDEX.md` in uploads — those must be read live via MCP at session start.

In **project instructions**, include at minimum:

1. **Start ritual:** Before anything else, read `Claude_Project_Files/dashboard.json` and `INDEX.md` together.
2. **Governed files:** Never write directly to `dashboard.json`, `INDEX.md`, `REGISTRY.md`, `COMPOUND.md`, `dashboard.html`, or `CLAUDE.md` — produce a Cursor briefing instead.
3. **Cleanup trigger:** Define `//clean-up//` to write `CLEANUP_BRIEFING_YYYY-MM-DD_HHmm.md`.

### Step 4 — Replace placeholder model strings

Edit **`CLAUDE.md`** and **`.cursor/rules/api_cost_governance.mdc`** and replace placeholders with exact model identifiers (e.g. `claude-sonnet-4-6`). Find the current list at [docs.anthropic.com](https://docs.anthropic.com).

{% callout "amber" %}
**Enterprise note:** On a personal machine this setup takes ~15 minutes. On a managed enterprise machine with IT security scanning and corporate proxy configurations, allow one to two days.
{% endcallout %}


<div class="divider"></div>


## GitHub and collaboration

The WMS uses Git for local commit history and the pre-commit validation hook. For team use, the repository should live on GitHub.

**Remote setup.** Push once setup is complete: `git remote add origin <your-repo-url> && git push -u origin main`. Tool configuration (Claude Desktop MCP, Cursor rules) is per-person, not stored in the repo.

**Session coordination.** Two people should not run sessions that modify `dashboard.json` simultaneously. Pull at session start, push at session close. Agree verbally on session windows for same-day work.


<div class="divider"></div>


## Every session — 5 minutes before you start work

| Step | Action |
|------|--------|
| 1 | `git pull origin main` |
| 2 | Claude Desktop: load live `dashboard.json` + `INDEX.md` |
| 3 | Note Current Focus, Open Items, and which tool owns the next step |
| 4 | Cursor: open repo — standing rules load automatically |


<div class="divider"></div>


## See the HTML dashboard

```bash
python3 -m http.server 8080 --directory Claude_Project_Files
```

Open: **http://localhost:8080/dashboard.html**


<div class="divider"></div>


## Cheat sheet

| Goal | Command or action |
|------|-------------------|
| Pull latest state | `git pull origin main` |
| Validate | `python3 tools/validate_dashboard.py --report` |
| Dashboard | `python3 -m http.server 8080 --directory Claude_Project_Files` |
| Cleanup trigger | Type `//clean-up//` in Claude Desktop |
| Push session close | `git push origin main` |


<div class="divider"></div>


## Where to read next

| Document | Use |
|----------|-----|
| [Tool Mapping Guide](/docs/wms-tool-mapping.html) | Map your existing tools to the three WMS roles |
| [Week One Deployment Guide](/docs/wms-first-deployment.html) | Build the WMS from scratch |
| Spec A | Rituals, SKILL files, Compound Step, briefings |
| Spec B | Schemas, validator rules, cleanup steps, dashboard layout |
