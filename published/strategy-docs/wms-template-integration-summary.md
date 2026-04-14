---
layout: aivalueworx-base.njk
title: "What to change, on which side,<br><strong>and in what order.</strong>"
eyebrow: "AI Value Worx — WMS × Template Set Integration"
meta: "Internal Summary · All six templates confirmed · April 2026"
navTitle: "Template integration — summary"
navSection: "Templates"
order: 10
permalink: "/docs/wms-template-integration-summary.html"
description: "Short internal summary"
---

<div class="section-label">How the template set fits together — and where the WMS sits</div>

Step 0 — Classify

stack-recommender

Classify the project, select the right template, produce plan/ files

↳ WMS seed opportunity

Layer 1 — AI Governance

template-ai-project

CLAUDE.md, Cursor rules, SKILL scripts, ADRs, memory files

↳ Merge required

Layer 2 — CI/CD

template-gh-automation

Workflows, prompt evals, scheduled jobs, release packaging

↳ Add validator workflow

Impl — Static

cf-pages-static

TypeScript/JS static or mostly-static sites on Cloudflare Pages

↳ Verify wrangler.jsonc

Impl — Edge API

cf-workers-fullstack

TypeScript edge APIs, LLM routing, Durable Objects, queues

↳ Production AI cost gap

Impl — Backend

railway-service-core

JS/Python monorepo, persistent services, MCP servers

↳ MCP evolution path

<div class="divider"></div>

<div class="section-label">What to do and when — full priority order</div>

Pri

Action

Applies to

Why

Side

🔴

**Merge CLAUDE.md into two-section file** — Project Context + Governance Rules sections, governance second

ai-project

Whichever file was written last wins. The other system's rules silently disappear.

Both

🔴

**Narrow MCP filesystem scope** to Claude\_Project\_Files/ and docs/ only — not repo root

All templates

In monorepos and deploy-config repos, unrestricted MCP scope covers wrangler.jsonc, railway.json, .env files.

WMS config

🔴

**Verify wrangler.jsonc pages\_build\_output\_dir = "public"** not "."

cf-pages-static

If set to root, dashboard.json deploys publicly — task state and decision register exposed.

Template

🔴

**Add production AI cost governance** for deployed Workers and Railway services — Cloudflare spend alerts, app-level rate limits

cf-workers-fullstack railway-service-core

WMS api\_cost\_governance.mdc governs dev-time only. A live LLM router has no spend ceiling without this.

Both

🟡

**Add WMS .gitignore entries** — briefing files, \_\_pycache\_\_, \*.pyc

All templates

Without this, untracked briefing files appear in every git status.

Template

🟡

**Annotate requirements.txt** — "WMS governance scripts only — not application dependencies"

gh-automation cf-pages-static cf-workers-fullstack

Three JS/TS templates will have requirements.txt with no other Python. Needs to be explicit.

WMS

🟡

**Decide HANDOFF.md vs INDEX.md** session start role — code-level vs project-level

ai-project

Both serve as cross-session AI context files. Mixed signals at session start.

Both

🟡

**Register template files in REGISTRY.md** — AGENTS.md, wrangler.jsonc, plan/ contents, workflow files

All templates

WMS validator blocks commits that reference unregistered assets. Register at project start.

WMS

🟡

**Add WMS seed output step to stack-recommender flow** — plan/ output → dashboard.json Phase 1 seed

stack-recommender

Recommender already captures everything needed for Phase 1 WMS tasks. Closing this gap collapses setup from a day to minutes.

Both

🟡

**Verify .cursor/rules/ commit rules don't conflict** between template committer.mdc and api\_cost\_governance.mdc

ai-project

Two rules intercepting commits will produce unpredictable Cursor commit behaviour.

Both

🟡

**Add tsconfig.json exclude entries** for Claude\_Project\_Files/, tools/

cf-pages-static cf-workers-fullstack

TypeScript compiler processes repo root by default. Spurious errors without this.

Template

🟢

**Add dashboard-validate.yml GitHub Actions workflow**

gh-automation

Extends WMS validator from local pre-commit into CI. Catches --no-verify bypasses before merge.

Template

🟢

**Add skill-freshness.yml weekly cron workflow** — flags SKILL files older than 90 days

gh-automation

Automates the stale SKILL file risk. One scheduled workflow, no ongoing maintenance.

Template

🟢

**Add .dockerignore WMS exclusions** — Claude\_Project\_Files/, tools/, docs/, plan/

railway-service-core

Keeps WMS files out of Docker build image. Low risk but clean hygiene.

Template

🟢

**Consolidate plan/ overlaps** — ARCHITECTURE-DECISION.md → ADRs, RISKS → COMPOUND.md, DELIVERY-PHASES → cross-reference only

stack-recommender

Prevents decisions and risks being maintained in two diverging places.

Both

🟢

**Rename WMS SKILL files** to KNOWLEDGE\_\*.md or move to Knowledge/ subfolder

ai-project

Avoids confusion with .claude/skills/ executable scripts. Important for new collaborators.

WMS

🟢

**Add WMS MCP server path to COMPOUND.md** as future architecture decision

railway-service-core

Railway + MCP server = the right substrate for a network-accessible WMS state layer. Capture the path now before it needs retrofitting.

WMS

<div class="divider"></div>

<div class="section-label">Four findings that change the picture from the inferred analysis</div>

Finding 1 — stack-recommender

The recommender is the missing WMS setup trigger

It's not an AI tool — it's a structured planning document set that already captures everything needed to seed Phase 1 WMS tasks. **Making recommender output feed directly into dashboard.json collapses setup from a day to minutes.** This is the highest-value integration in the set.

Finding 2 — template-ai-project only

CLAUDE.md merge complexity is isolated to one template

Only template-ai-project has AI governance files. The other four implementation templates have none — **the WMS drops in cleanly with no merging required.** The merge problem is real but limited in scope.

Finding 3 — cf-workers + railway

Production AI cost is ungoverned by the WMS

Two templates support runtime AI API calls (LLM routing, MCP servers). The WMS cost ceiling covers dev-time only. **A deployed service can exceed the dev cost ceiling in a single day with no WMS alert.** Needs explicit production-side governance.

Finding 4 — railway-service-core

Railway + MCP = the natural WMS evolution path

The template explicitly lists MCP servers as a best-fit. **A Railway-hosted WMS MCP server would replace the local filesystem MCP** — shared live state across team members, no git pull/push coordination, programmatic rule enforcement. The right substrate is already in the set.

<div class="divider"></div>

<div class="section-label">SKILL files to create at project start — one per integration pattern</div>

SKILL\_TEMPLATE\_SET\_  
PLAN\_DIRECTORY.md

plan/ is infrastructure planning; Claude\_Project\_Files/ is project governance. Different horizons, different audiences. Do not merge.

SKILL\_CF\_PAGES\_  
WMS.md

wrangler.jsonc output dir verification, .dev.vars vs env vars, tsconfig exclusions, edge Function cost boundary.

SKILL\_LLM\_ROUTING\_  
GOVERNANCE.md

Dev vs production cost boundary, Cloudflare spend alert setup, rate limiting patterns for LLM endpoints.

SKILL\_WMS\_MCP\_  
SERVER\_PATTERN.md

Architecture outline for Railway-hosted WMS MCP server — shared state, programmatic rule enforcement, team coordination.
