---
layout: aivalueworx-base.njk
title: "System at a glance.<br><strong>Four views, four minutes.</strong>"
eyebrow: "AI Value Worx — Workflow Management System"
meta: "Orientation · Read before the specs · April 2026"
navTitle: "System diagrams"
navSection: "Reference"
order: 4
permalink: "/docs/wms-system-diagrams.html"
description: "Four ASCII views and quick reference"
---

<p class="section-intro">Four views. Read in order. Each takes under a minute. Start here before Spec A, Spec B, or the Quick Start Guide.</p>

<div class="section-head">
  <span class="section-badge badge-blue">View 1 of 4</span>
  <span class="section-count">The System — What is this thing and how do the pieces connect?</span>
</div>

```
╔══════════════════════════════════════════════════════════════════╗
║  WORKFLOW MANAGEMENT SYSTEM — THE FULL PICTURE                  ║
╚══════════════════════════════════════════════════════════════════╝

  ┌──────────────────────────────────────────────────────────────┐
  │  YOU                                                         │
  │  goals · decisions · approvals · "do the cleanup"           │
  └─────────────────────────────┬────────────────────────────────┘
                                │  intent
                                ▼
  ┌──────────────────────────────────────────────────────────────┐
  │  CLAUDE DESKTOP                          [ DESIGN TOOL ]     │
  │                                                              │
  │  At session start, reads live:                               │
  │    dashboard.json  ←  what needs doing                       │
  │    INDEX.md        ←  where things are                       │
  │    SKILL_*.md      ←  what we've learned                     │
  │                                                              │
  │  Produces:  briefings only                                   │
  │  NEVER:     writes to governed files directly                │
  └─────────────────────────────┬────────────────────────────────┘
                    writes       │                reads (live MCP)
                    briefings    │           ┌────────────────────
                                 ▼           │
  ┌──────────────────────────────────────────────────────────────┐
  │  REPOSITORY (git + GitHub)              [ SOURCE OF TRUTH ]  │
  │                                                              │
  │  ┌── WMS LAYER ──────────────────────────────────────────┐  │
  │  │  dashboard.json   task state machine                  │  │
  │  │  INDEX.md         session navigation (80-line target) │  │
  │  │  REGISTRY.md      every significant file, registered  │  │
  │  │  SKILL_*.md       institutional memory (grows daily)  │  │
  │  │  COMPOUND.md      engineering taste + decisions log   │  │
  │  │  briefings/       handoffs between tools              │  │
  │  └───────────────────────────────────────────────────────┘  │
  │                                                              │
  │  ┌── APPLICATION LAYER ──────────────────────────────────┐  │
  │  │  src/  functions/  scripts/  plan/                    │  │
  │  │  wrangler.jsonc  railway.json  .github/workflows/     │  │
  │  └───────────────────────────────────────────────────────┘  │
  └──────────────┬────────────────────────────────┬─────────────┘
                 │  governed writes + commit       │  build + deploy
                 ▼                                 ▼
  ┌─────────────────────────────┐   ┌─────────────────────────────┐
  │  CURSOR                     │   │  Cloudflare Pages           │
  │  [ GOVERNED FILE EXECUTION ]│   │  Cloudflare Workers         │
  │  applies briefings          │   │  Railway                    │
  │  verifies pre-flight stamp  │   │  GitHub Actions             │
  │  runs validator             │   └─────────────────────────────┘
  │  commits                    │
  ├─────────────────────────────┤
  │  CLAUDE CODE                │
  │  [ CODE EXECUTION ]         │
  │  runs scripts + pipelines   │
  │  builds tools               │
  │  serves dashboard locally   │
  └─────────────────────────────┘
```

<div class="banner banner-blue">
  <strong>Key rule:</strong> Claude Desktop reasons and plans. It never writes governed files. That separation is the audit chain.
</div>

<div class="banner banner-amber">
  <strong>Tool note:</strong> Claude Desktop, Cursor, and Claude Code are the reference implementation. The WMS is tool-agnostic — any tool that fills the design, code execution, and governed file execution roles will work. See the <strong>Tool Mapping Guide</strong> for Microsoft, Google, GitHub-centric, and internal LLM configurations. You do not need to adopt new tools to run this system.
</div>

<div class="divider"></div>

<div class="section-head">
  <span class="section-badge badge-teal">View 2 of 4</span>
  <span class="section-count">The Session — What actually happens in one working day?</span>
</div>

```
╔══════════════════════════════════════════════════════════════════╗
║  ONE SESSION — START TO CLOSE                                   ║
╚══════════════════════════════════════════════════════════════════╝

  ┌────────────────────────────────────────────────────────────┐
  │  OPEN                                              ~5 min  │
  │                                                            │
  │  git pull                                                  │
  │    └─► Claude Desktop reads dashboard.json + INDEX.md      │
  │              └─► "current state is X, next task is Y"      │
  │                        └─► you confirm or redirect         │
  └────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
  ┌────────────────────────────────────────────────────────────┐
  │  WORK                                          repeating   │
  │                                                            │
  │  Claude Desktop writes a briefing                          │
  │    ├── pre-flight: files to verify before touching         │
  │    ├── steps: numbered, one governed change each           │
  │    └── done when: observable completion criteria           │
  │                         │                                  │
  │                         ▼                                  │
  │  You review the briefing ──► approve or revise             │
  │                         │                                  │
  │                         ▼                                  │
  │  Cursor executes the briefing                              │
  │    ├── check pre-flight stamp on each file                 │
  │    ├── apply steps in sequence                             │
  │    ├── run validate_dashboard.py                           │
  │    └── commit  (blocked if validator fails)                │
  │                                                            │
  │  ▲ repeat for each task                                    │
  └────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
  ┌────────────────────────────────────────────────────────────┐
  │  CLOSE  (the Compound Step)                        ~10 min │
  │                                                            │
  │  Claude Desktop reviews the session                        │
  │    └─► "what did we learn that isn't in the SKILL library?"│
  │              └─► write SKILL_*.md for new patterns         │
  │                        └─► update INDEX.md                 │
  │                                  └─► //clean-up//          │
  │                                            └─► final commit│
  │                                                    │       │
  │                                                git push    │
  └────────────────────────────────────────────────────────────┘
```

<div class="banner banner-green">
  <strong>The rule that matters most:</strong> If the session closes without the Compound Step, the knowledge it contained is lost. The SKILL library only grows if someone writes to it.
</div>

<div class="divider"></div>

<div class="section-head">
  <span class="section-badge badge-green">View 3 of 4</span>
  <span class="section-count">The Knowledge Loop — Why the system gets more valuable the longer you use it</span>
</div>

```
╔══════════════════════════════════════════════════════════════════╗
║  THE KNOWLEDGE LOOP — HOW SKILL FILES COMPOUND                  ║
╚══════════════════════════════════════════════════════════════════╝

                      WEEK 1
   ┌─────────────────────────────────────────────────────────┐
   │  Something goes wrong or a new pattern is discovered    │
   │                         │                               │
   │                         ▼                               │
   │             SKILL file written                          │
   │             (10 minutes, at session close)              │
   │                         │                               │
   │                         ▼                               │
   │        Stored in Claude_Project_Files/Skills/           │
   └─────────────────────────────────────────────────────────┘
                             │
                             │  loaded at next session start
                             ▼
                      WEEK 2
   ┌─────────────────────────────────────────────────────────┐
   │  Claude Desktop reads the SKILL file as context         │
   │  before producing any briefing                          │
   │                         │                               │
   │                         ▼                               │
   │  The same failure mode doesn't recur.                   │
   │  The pattern is applied correctly first time.           │
   └─────────────────────────────────────────────────────────┘
                             │
                             │  more sessions, more SKILL files
                             ▼
                      MONTH 3
   ┌─────────────────────────────────────────────────────────┐
   │  SKILL library: 30–50 files covering                    │
   │    · failure modes encountered and diagnosed            │
   │    · validated patterns for this codebase               │
   │    · architectural decisions and their reasoning        │
   │    · briefing quality standards                         │
   │    · deployment gotchas for this stack                  │
   │                         │                               │
   │  Every new session starts with this knowledge loaded.   │
   │  Every new collaborator inherits it from day one.       │
   └─────────────────────────────────────────────────────────┘

  WHAT THIS MEANS IN PRACTICE:

  Month 1  ┤░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
  Month 2  ┤░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
  Month 3  ┤░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
           └──────────────────────────────────────────────────────►
                                AI tool quality per session

  Competing teams working without a SKILL library start every
  session from scratch. The WMS makes institutional memory a
  system output, not a heroic effort.
```

<div class="divider"></div>

<div class="section-head">
  <span class="section-badge badge-amber">View 4 of 4</span>
  <span class="section-count">The Template Set — Where the six project templates fit into the WMS picture</span>
</div>

```
╔══════════════════════════════════════════════════════════════════╗
║  TEMPLATE SET + WMS — PROJECT LIFECYCLE                         ║
╚══════════════════════════════════════════════════════════════════╝

  BEFORE CODE                          GOVERNANCE LAYER
  ─────────────────────────────────    ─────────────────────────────
  template-stack-recommender           template-ai-project
                                       + WMS (Spec A + Spec B)
  Fill in STACK-RECOMMENDER.md    ──►
  → choose implementation stack        CLAUDE.md  (merged)
  → produce plan/ files                .cursor/rules/
  → seed dashboard.json Phase 1 ◄──    SKILL_*.md
    tasks automatically                COMPOUND.md
                │                      dashboard.json
                │                      briefings/
                ▼
  CHOOSE ONE IMPLEMENTATION            CI / CD LAYER
  ─────────────────────────────────    ─────────────────────────────
                                       template-gh-automation
  ┌─── static / edge ───────────┐
  │ template-cf-pages-static    │      validate_dashboard.yml
  │ HTML / TS / CF Pages        │      skill-freshness.yml
  └─────────────────────────────┘      prompt-eval-tracker.yml
                                                   │
  ┌─── edge API / AI ───────────┐                  │ CI runs validator
  │ template-cf-workers-        │                  │ on every PR
  │ fullstack                   │◄─────────────────┘
  │ TS / CF Workers / Durable   │
  │ Objects / LLM routing       │      ⚠  production AI cost
  └─────────────────────────────┘         ungoverned by WMS
                                          needs CF spend alerts
  ┌─── persistent backend ──────┐
  │ template-railway-service-   │
  │ core                        │      ◈  future: Railway-hosted
  │ JS or Python / monorepo /   │         WMS MCP server
  │ MCP servers                 │         shared state layer
  └─────────────────────────────┘         for whole team

  THE SEAM THAT MATTERS:

  stack-recommender produces plan/ files
           │
           ▼
  plan/ files live in every implementation template
           │
           ▼
  plan/DELIVERY-PHASES.md  =  narrative version of
  dashboard.json task library  =  operational version

  They serve different audiences.
  Never merge them. Always cross-reference them.
```

<div class="divider"></div>

<div class="section-head">
  <span class="section-badge badge-purple">Quick reference</span>
  <span class="section-count">What each tool may and may not do</span>
</div>

```
  ┌────────────────────┬───────────────────┬───────────────────┐
  │  CLAUDE DESKTOP    │  CURSOR           │  CLAUDE CODE      │
  │  (design)          │  (governed exec)  │  (code exec)      │
  ├────────────────────┼───────────────────┼───────────────────┤
  │  ✓ Read any file   │  ✓ Apply briefing │  ✓ Run scripts    │
  │  ✓ Write briefings │  ✓ Edit governed  │  ✓ Build tools    │
  │  ✓ Reason + plan   │    files          │  ✓ Serve dashboard│
  │  ✓ Write SKILLs    │  ✓ Run validator  │  ✓ Run pipelines  │
  │                    │  ✓ Commit + push  │                   │
  ├────────────────────┼───────────────────┼───────────────────┤
  │  ✗ Write governed  │  ✗ Interpret an   │  ✗ Make arch      │
  │    files directly  │    ambiguous step │    decisions      │
  │  ✗ Commit changes  │  ✗ Skip steps     │  ✗ Write briefings│
  └────────────────────┴───────────────────┴───────────────────┘

  governed files = dashboard.json · INDEX.md · REGISTRY.md
                   COMPOUND.md · CLAUDE.md · SKILL_*.md
```

Read next: **Quick Start Guide** → **Tool Mapping Guide** → **Spec A** → **Spec B**
