---
layout: aivalueworx-base.njk
title: "Integration analysis.<br><strong>What changes, on which side, and why.</strong>"
eyebrow: "AIValueWorx — WMS × Template Set"
meta: "Internal working document · All six templates confirmed · April 2026"
navTitle: "WMS × template integration (full)"
navSection: "Templates"
order: 9
permalink: "/docs/wms-template-integration.html"
description: "Per-template analysis — all six templates"
---

<div class="banner banner-blue"><strong>Coverage:</strong> Full file-level analysis for all six templates — <code>template-ai-project</code>, <code>template-stack-recommender</code>, <code>template-gh-automation</code>, <code>template-cf-pages-static</code>, <code>template-cf-workers-fullstack</code>, <code>template-railway-service-core</code> — confirmed from live GitHub repo reads. Earlier inferred analysis has been superseded by confirmed content throughout.</div>

<div class="section-label">The core tension — two overlapping governance layers</div>

`template-ai-project` and the WMS are solving **adjacent problems from different angles**, and they share several file responsibilities. Neither approach is wrong. The template governs **code development sessions** (feature → PR → merge). The WMS governs **project-level state and institutional memory** across the whole engagement.

Concern

template-ai-project approach

WMS approach

AI tool instructions

`CLAUDE.md` → `@AGENTS.md`

`CLAUDE.md` (standing rules)

Coding standards / taste

`CONVENTIONS.md`, `AGENTS.md`

`COMPOUND.md`

Decisions register

`DECISIONS.md` + `docs/adr/`

`COMPOUND.md` decisions section

Cross-session memory

`HANDOFF.md`, `MEMORY.md`

`INDEX.md`, `SKILL_*.md`

Cursor rules

`.cursor/rules/*.mdc` (5 rules)

`.cursor/rules/api_cost_governance.mdc`

Claude Code skills

`.claude/skills/*.md` (invokable scripts)

n/a — SKILL files are design-tool context inputs, not scripts

Task state

`docs/agentic-workflow/TASKS-TEMPLATE.md` (per-feature)

`dashboard.json` (project-wide state machine)

Knowledge accumulation

Feeds back into `CONVENTIONS.md` / `AGENTS.md`

SKILL files

Session audit

`TRANSCRIPT_LOG.md` + Willison toolchain

Briefing archive + `COMPOUND.md`

<div class="banner banner-green">The merge challenge for <code>template-ai-project</code> is specific and bounded. For all other five templates, the WMS drops in cleanly — none of them have AI governance files, so there's no merging complexity at all.</div>

<div class="divider"></div>

<div class="section-label">Per-template analysis — click to expand</div>

1

`template-ai-project`

8-layer compound engineering documentation stack — CLAUDE.md, Cursor rules, Claude Code skills, ADRs, adversarial review

Fully confirmed

▾

Conflicts — require active resolution

`CLAUDE.md` — direct collision

Both systems write a `CLAUDE.md` at the repo root with different content. Template version: entry point delegating to `@AGENTS.md`, project context, model preferences. WMS version: standing governance rules — cost ceilings, model tier assignments, preflight verification requirements.  
  
**What to change:** Merge into a single `CLAUDE.md` with two clearly labelled sections: `## Project Context` (template content) and `## Governance Rules` (WMS content, non-negotiable). Governance section must come second so it overrides conflicting instructions above.

Impact: Medium — without merging, whichever file was written last wins

`.cursor/rules/` — additive collision

Template ships five `.mdc` rules. WMS adds `api_cost_governance.mdc`. Content doesn't conflict — but both the template's `committer.mdc` and the WMS governance rule intercept commits. Verify they don't produce contradictory commit instructions.  
  
**What to change:** Verify both rules. If commit instructions conflict, merge into one file.

Impact: Low if no conflict · Medium if commit rules contradict

`HANDOFF.md` vs `INDEX.md` — functional overlap

Both serve as cross-session AI context files read at session start. `INDEX.md` is more structured (80-line target, fixed sections). `HANDOFF.md` is more freeform.  
  
**Recommended resolution:** Keep both with differentiated scope — `HANDOFF.md` covers code-level task state (active feature, current PR); `INDEX.md` covers project-level state (phase, workstream, governance). The session start ritual must specify which file governs which domain.

Impact: Medium — mixed signals at session start if not clarified

`DECISIONS.md` + `docs/adr/` vs `COMPOUND.md` — overlap

Genuinely complementary, not conflicting. ADRs (immutable, CODEOWNERS-protected, architecture-level) belong in `docs/adr/`. `COMPOUND.md` covers engineering taste and session-level decisions. `DECISIONS.md` can be deprecated in favour of `COMPOUND.md` + ADR links, or kept as the ADR index only.  
  
**What to change:** Agree at project start which decisions go where and record that agreement as ADR #0002.

Impact: Low — risk is decisions recorded in two diverging places

`.claude/skills/` vs `SKILL_*.md` — naming confusion

Template has `.claude/skills/` containing invokable Claude Code scripts (`doc-sync`, `adr-stub`, etc.). WMS `SKILL_*.md` files are knowledge documents loaded as context, not scripts. No technical conflict — but new collaborators will confuse them.  
  
**What to change:** Consider renaming WMS SKILL files to `KNOWLEDGE_*.md` or moving to `Claude_Project_Files/Knowledge/`.

Impact: Low technically · Medium for collaborator onboarding

Additive changes — no conflict, just gaps

The following WMS files have no equivalent in the template and need to be added:

WMS file

What to add

`Claude_Project_Files/dashboard.json`

Task state machine — not covered by template

`Claude_Project_Files/INDEX.md`

Project-level session navigation

`Claude_Project_Files/REGISTRY.md`

Asset registry

`tools/validate_dashboard.py`

Governance validator

`Claude_Project_Files/dashboard.html`

Visual dashboard

**Additional additions:** Add `dashboard-validate.yml` to GitHub Actions (extends WMS validator into CI — catches `--no-verify` bypasses before merge). Add WMS ephemeral files to `.gitignore`. Register `docs/agent-governance/` contract templates in `REGISTRY.md`.

Summary table

Change

Side

Effort

Merge `CLAUDE.md` into two-section file

Both

Low

Verify `.cursor/rules/` commit rule compatibility

Both

Low

Decide `HANDOFF.md` vs `INDEX.md` session start role

Both

Medium

Consolidate decision records (DECISIONS.md → COMPOUND.md)

Template

Low

Rename WMS SKILL files to avoid `.claude/skills/` confusion

WMS

Medium

Add `Claude_Project_Files/` structure

WMS

Low

Update `.gitignore` for WMS ephemeral files

Template

Low

Add `dashboard-validate.yml` GitHub Actions workflow

Template

Low

2

`template-stack-recommender`

Meta-template — pre-code project classification, stack selection, plan/ file generation. No application code.

Fully confirmed

▾

Key finding — solves the plan/ mystery

Every implementation template has a `plan/` directory because this meta-template produces one. The `plan/` folder is not boilerplate — it's the output of working through `STACK-RECOMMENDER.md`, then copied into whichever implementation template was chosen.

The highest-value integration in the full set

The recommender already captures everything needed to seed Phase 1 WMS tasks: project classification, constraints, risks, delivery phases, setup checklist. Current flow vs WMS-integrated flow:

**Current:**

1.  Fill in `STACK-RECOMMENDER.md`
2.  Convert output into the other `plan/` files
3.  Choose an implementation template

**WMS-integrated:**

1.  Fill in `STACK-RECOMMENDER.md`
2.  Convert output into `plan/` files **and** a pre-populated `dashboard.json` seed
3.  Choose an implementation template — which already contains the correct `Claude_Project_Files/` structure with Phase 1 tasks loaded

The gap between "project classified" and "WMS running" collapses from a day's setup to minutes. This is the setup trigger the deployment guide identified as missing. **The recommender IS that trigger.**

plan/ overlaps — now confirmed and mappable

plan/ file

WMS equivalent

Resolution

`ARCHITECTURE-DECISION.md`

`COMPOUND.md` + `docs/adr/`

Use ADRs for significant decisions. Deprecate or make ADR #0001 stub.

`DELIVERY-PHASES.md`

WMS task library phases

Keep both — different audiences. Cross-reference explicitly.

`RISKS-AND-CONSTRAINTS.md`

`COMPOUND.md` risk notes

Register in `REGISTRY.md`, link from `COMPOUND.md`. Don't maintain two risk registers.

`REPO-SETUP.md`

WMS Week One Deployment Guide

Differentiate clearly: `REPO-SETUP.md` = template setup; Deployment Guide = governance layer. Add cross-references.

`PROJECT-CLASSIFICATION.md`

No WMS equivalent

Keep as-is. Register in `REGISTRY.md`.

`STACK-RECOMMENDER.md`

No WMS equivalent

Keep as-is. Extend with WMS seed output step.

Impact: Medium — overlaps create confusion about authoritative record, not technical failures

3

`template-gh-automation`

JavaScript starter for repo-triggered automation — CI/CD, scheduled reports, prompt evals, artifact generation. 100% JavaScript.

Fully confirmed

▾

Conflicts (confirmed)

`scripts/` vs `tools/` — naming collision

Template uses `scripts/` for automation. WMS uses `tools/` for the validator. The template's quick start says "Replace the placeholder scripts in `/scripts`" — someone following this could delete the WMS validator assuming it's a placeholder.  
  
**What to change:** Keep both. Document in `CLAUDE.md`: `scripts/` = project automation; `tools/` = WMS governance. Never merge them.

Impact: Low if documented · Medium if not

Python (WMS) in a JavaScript project

The WMS validator is Python. This template is 100% JavaScript. `requirements.txt` will sit alongside `package.json` with no other Python in sight.  
  
**What to change:** Add a comment to `requirements.txt`: `# WMS governance scripts only — not application dependencies`. Document in one-time setup guide.

Impact: Low — annotation prevents pip-in-wrong-environment errors

Additive opportunities

Three new workflows to add to `.github/workflows/`:

-   **`validate-dashboard.yml`** — runs `python3 tools/validate_dashboard.py` on any PR touching `Claude_Project_Files/`. Extends WMS governance from local pre-commit into CI. Catches `--no-verify` bypasses before merge.
-   **`skill-freshness.yml`** — weekly cron that flags SKILL files older than 90 days without a review date update. Template already ships a scheduled workflow pattern to follow.
-   **`prompt-eval-tracker.yml`** — "prompt evals" is an explicit best-fit use case. WMS task tracking for eval runs: each run becomes a task, results go into a SKILL file, dashboard tracks status. The most distinctive integration opportunity in this template.

Impact: Medium-positive — prompt eval integration is genuinely new capability

4

`template-cf-pages-static`

TypeScript/JS starter for static or mostly-static public sites — marketing, landing pages, docs, forms. Cloudflare Pages + Functions.

Fully confirmed

▾

Deployment exposure — revised from earlier inference

Earlier analysis flagged this as a definite High risk. The confirmed file structure changes the picture: the template has a `public/` directory, which is the standard CF Pages pattern for serving from a subdirectory only. **If `wrangler.jsonc` correctly sets `pages_build_output_dir = "public"`**, then `Claude_Project_Files/` is already excluded automatically.

```
// Safe — only public/ is deployed
{ "pages\_build\_output\_dir": "public" }

// Unsafe — Claude\_Project\_Files/ goes public
{ "pages\_build\_output\_dir": "." }
```

**What to check:** Verify `wrangler.jsonc` setting before first deploy. Add an explicit comment noting that `Claude_Project_Files/`, `tools/`, and `docs/` are intentionally not deployed.

Impact: High if misconfigured — dashboard.json exposes task state publicly

Additional confirmed findings

`.dev.vars` vs `.env`

Cloudflare uses `.dev.vars` instead of `.env`. WMS Python scripts use standard environment variables, not `.dev.vars`. No conflict — but document in `CLAUDE.md` so AI tools don't mistakenly suggest loading `.dev.vars` for Python scripts.

Impact: Low — documentation fix

TypeScript compiler exclusions

Add to `tsconfig.json`:

```
{ "exclude": \["Claude\_Project\_Files", "tools", "node\_modules"\] }
```

Impact: Low — one exclude entry

Edge Function production AI cost

If any `functions/` edge function calls the Anthropic API in production, that is a separate production cost surface not governed by the WMS `api_cost_governance.mdc` rule. See cross-cutting section.

Impact: Medium — needs separate production cost governance

5

`template-cf-workers-fullstack`

Pure TypeScript edge-first stack — Workers, Durable Objects, queues, LLM routing. Explicit best-fit: lightweight LLM routing.

Fully confirmed

▾

Deployment risk — lower than cf-pages-static

Workers bundle from `src/` — only the bundle deploys to the edge. `Claude_Project_Files/` at the repo root **cannot be accidentally served publicly** via a standard Workers deployment. The one exception: if `wrangler.jsonc` includes an `assets` binding pointing at the repo root, which standard Workers fullstack setup doesn't do. Verify in `wrangler.jsonc`.

Add `Claude_Project_Files` and `tools` to `tsconfig.json` exclude (same as cf-pages-static).

LLM routing — the most significant governance gap

"Lightweight LLM routing" is an explicit best-fit use case. This is the only template besides Railway that can make Anthropic API calls in production. The critical distinction:

What

Governed by

Scope

Claude Code API calls during development

WMS `api_cost_governance.mdc`

Dev-time, per-session

Anthropic API calls from deployed Worker

Application rate limits + CF spend alerts

Runtime, production

**What to change — WMS side:** Add a scope statement to `api_cost_governance.mdc`: "This rule governs Claude Code API usage during development sessions only. It does not govern API calls made by deployed applications." Create `SKILL_LLM_ROUTING_GOVERNANCE.md` covering: dev vs production cost boundary, CF spend alert setup, rate limiting patterns for LLM endpoints.

Impact: High if missed — a deployed LLM router can exceed the dev cost ceiling in a day with no WMS alert

Durable Objects + WMS — future integration path

Durable Objects provide strongly-consistent stateful primitives at the edge. A future integration: a Durable Object that exposes a read-only API view of WMS task state — shared state layer for the whole team, accessible without file system access. Not needed for initial deployment, but this template is the right substrate for it.

**What to capture now:** Add to `COMPOUND.md` as a future architecture decision. Create `SKILL_WMS_MCP_SERVER_PATTERN.md` outlining the approach for when the time comes.

6

`template-railway-service-core`

JavaScript monorepo — persistent backend services, background workers, ingestion pipelines, Python or Node backends. Explicit best-fit: MCP or tool servers.

Fully confirmed

▾

The MCP server finding — the most architecturally significant finding in the set

"MCP or tool servers" as an explicit best-fit is not incidental. A Railway-hosted WMS MCP server would replace the local filesystem MCP — shared live state across team members, no git pull/push coordination, programmatic rule enforcement, fits the enterprise "no file system access on managed machines" constraint.

**This is an architectural evolution path, not a current requirement.** Capture it in `COMPOUND.md` and create `SKILL_WMS_MCP_SERVER_PATTERN.md` so the design isn't lost. The right substrate is in the template set already.

Monorepo structure — MCP scope matters more here

The monorepo has `apps/`, `packages/shared`, and `scripts/` alongside the WMS's `Claude_Project_Files/` and `tools/`. Claude Desktop's MCP pointed at the repo root has read/write access to all application source code — a wider surface than any other template.  
  
Narrow MCP scope to `Claude_Project_Files/` and `docs/` only. More important here because of the monorepo depth.

**`scripts/` vs `tools/`:** Same as gh-automation. Document the distinction in `CLAUDE.md`: `scripts/` = build and CI tooling; `tools/` = WMS governance.

**Docker / deployment:** Railway deploys from subdirectory configs per service — `Claude_Project_Files/` is not a target. If Docker is used, add `.dockerignore` entries:

```
Claude\_Project\_Files/
tools/
docs/
plan/
```

Impact: Low for deployment · Medium for MCP scope (more important in a monorepo)

<div class="divider"></div>

<div class="section-label">Cross-cutting changes — apply to all templates</div>

1\. Unified .gitignore additions

Add to every template's `.gitignore`:

```
\# WMS ephemeral session files
Claude\_Project\_Files/CURSOR\_BRIEFING\_\*.md
Claude\_Project\_Files/CLAUDE\_CODE\_BRIEFING\_\*.md
Claude\_Project\_Files/CLEANUP\_BRIEFING\_\*.md
\# WMS build artefacts
tools/\_\_pycache\_\_/
tools/\*.pyc
```

`Claude_Project_Files/` itself must **not** be gitignored — it contains permanent WMS state that must be version-controlled. Only briefing files are ephemeral.

2\. Narrow MCP filesystem scope

Point Claude Desktop's MCP at specific directories, not the repo root:

```
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": \["-y",
        "@modelcontextprotocol/server-filesystem",
        "/path/to/repo/Claude\_Project\_Files",
        "/path/to/repo/docs"
      \]
    }
  }
}
```

High — unrestricted MCP in a deploy-config repo is a security concern

3\. Register template files in REGISTRY.md

When the WMS is added to a template repo, register all significant template files:

-   `AGENTS.md` / `CONVENTIONS.md` / `DECISIONS.md` (template-ai-project)
-   `docs/adr/` directory
-   `wrangler.jsonc` / deployment configs
-   `.github/workflows/` files

**Why it matters:** The WMS validator checks that tasks reference registered assets. Tasks referencing unregistered template files will block commits.

4\. Create deployment-domain SKILL files

Seed SKILL files at project start — one per template used:

-   `SKILL_TEMPLATE_SET_PLAN_DIRECTORY.md` — `plan/` vs `Claude_Project_Files/` distinction
-   `SKILL_CF_PAGES_WMS.md` — wrangler.jsonc verification, .dev.vars, tsconfig exclusions
-   `SKILL_LLM_ROUTING_GOVERNANCE.md` — dev vs production cost boundary
-   `SKILL_WMS_MCP_SERVER_PATTERN.md` — Railway-hosted WMS evolution path
-   `SKILL_GH_AUTOMATION_WMS.md` — scripts vs tools, prompt eval tracking

<div class="divider"></div>

<div class="section-label">Full template-set observations — visible only with all six</div>

Finding 1

The template set has a complete project lifecycle shape

```ascii
stack-recommender  ← classify and plan
       ↓ plan/ output
template-ai-project  ← governance layer
       +
template-gh-automation  ← CI/CD layer
       +
[choose one implementation]
  cf-pages-static
  cf-workers-fullstack
  railway-service-core
```
The WMS sits across this entire shape. What's missing: an integration point at the start (recommender → WMS seed) and at the end (deployment verification → WMS task close).

Finding 2

CLAUDE.md merge complexity is isolated to one template

Only `template-ai-project` has AI governance files (`CLAUDE.md`, `.cursor/rules/`, `AGENTS.md`, `MEMORY.md`, `HANDOFF.md`). **For all other five templates, the WMS drops in cleanly with no merging required.** The merge problem is real but narrow in scope.

Finding 3

plan/ is the seam between the recommender and implementation

The recommender produces `plan/`. Every implementation template has `plan/` waiting for it. The WMS needs to acknowledge this seam: `plan/DELIVERY-PHASES.md` is the narrative version of what the WMS task library operationalises. Different audiences, different formats — never merge, always cross-reference.

Finding 4

Production AI governance gap appears in two templates

Both `cf-workers-fullstack` (LLM routing) and `railway-service-core` (MCP servers, Python AI backends) can run Anthropic API calls in production. The WMS `api_cost_governance.mdc` rule governs development only. **This is the single most operationally important finding across the full template set.**

Template

Language

Python needed for WMS?

`template-ai-project`

Python + Shell

Natural fit

`template-stack-recommender`

None

Not applicable

`template-gh-automation`

JavaScript

Add "WMS governance only" annotation

`template-cf-pages-static`

HTML/CSS/TS/JS

Add "WMS governance only" annotation

`template-cf-workers-fullstack`

TypeScript

Add "WMS governance only" annotation

`template-railway-service-core`

JavaScript

Natural fit (Python supported)

<div class="divider"></div>

<div class="section-label">Priority order for integration work</div>

Pri

Change

Reason

🔴

**Narrow MCP filesystem scope**

Security — prevents accidental writes to deployment configs, secrets, and production service files

🔴

**Verify `wrangler.jsonc pages_build_output_dir`** (cf-pages-static)

Data exposure — WMS state goes public if set to `"."`

🔴

**Merge `CLAUDE.md` files** (template-ai-project only)

Governance — one system's rules silently disappear without this

🔴

**Add production AI cost governance** (cf-workers-fullstack, railway)

A deployed LLM router can exceed the dev cost ceiling in a day with no WMS alert

🟡

**Add `.gitignore` WMS ephemeral entries**

Hygiene — untracked briefing files in every `git status` otherwise

🟡

**Decide `HANDOFF.md` vs `INDEX.md` role** (template-ai-project)

Mixed signals at session start otherwise

🟡

**Register template files in `REGISTRY.md`**

Validator blocks commits referencing unregistered assets

🟡

**Verify `.cursor/rules/` commit rules don't conflict** (template-ai-project)

Cursor commit behaviour unpredictable if they do

🟡

**Add WMS seed output step to stack-recommender flow**

Closes the gap between "project classified" and "WMS running" — the highest-value integration

🟡

**Add TypeScript compiler exclusions** (cf-pages-static, cf-workers-fullstack)

Spurious compiler errors without this

🟢

**Add `dashboard-validate.yml` GitHub Actions workflow** (gh-automation)

Extends WMS validator into CI — catches `--no-verify` bypasses

🟢

**Add `.dockerignore` WMS exclusions** (railway)

Keeps WMS files out of Docker build image

🟢

**Create deployment-domain SKILL files**

First sessions produce learnings worth capturing — seed before session one

🟢

**Rename WMS SKILL files** to avoid `.claude/skills/` confusion (template-ai-project)

Collaborator onboarding clarity

🟢

**Consolidate `DECISIONS.md` → `COMPOUND.md`** (template-ai-project)

Single decisions register, no divergence

<div class="footer-note">Analysis based on confirmed file-tree reads for all six templates from GitHub. Earlier inferred analysis has been superseded throughout.</div>
