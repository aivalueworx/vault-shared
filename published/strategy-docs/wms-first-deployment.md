---
layout: aivalueworx-base.njk
title: "From zero to first session.<br><strong>Your week one deployment guide.</strong>"
eyebrow: "AIValueWorx — Workflow Management System"
meta: "Technical Guide · For your implementation lead · April 2026"
navTitle: "First deployment — week one"
navSection: "Guides"
order: 3
permalink: "/docs/wms-first-deployment.html"
description: "Technical guide for implementation lead"
---

<p class="section-intro">This guide takes you from a blank machine to a running WMS session in one week. Day 1 is the only day with significant time investment — everything after that is verification, first use, and calibration. Steps are marked with who does them: a human decision, an AI-assisted action, or a verification checkpoint.</p>

<div class="section-label">The week at a glance</div>

<div class="stats-row cols-5">
  <div class="stat-cell">
    <div class="stat-num">Day 1</div>
    <div class="stat-label">~4 hours<br>Build the infrastructure</div>
  </div>
  <div class="stat-cell">
    <div class="stat-num">Day 2</div>
    <div class="stat-label">~1 hour<br>Load the methodology</div>
  </div>
  <div class="stat-cell">
    <div class="stat-num">Day 3</div>
    <div class="stat-label">~2 hours<br>First real session</div>
  </div>
  <div class="stat-cell">
    <div class="stat-num">Day 4</div>
    <div class="stat-label">~30 min<br>Review and calibrate</div>
  </div>
  <div class="stat-cell">
    <div class="stat-num">Day 5</div>
    <div class="stat-label">~30 min<br>Handover check</div>
  </div>
</div>

<div class="divider"></div>

<!-- DAY 1 MORNING -->
<div class="phase-block">
  <div class="phase-title-row">
    <div class="phase-pip" style="background:var(--blue);"></div>
    <div class="phase-name">Day 1 — Morning</div>
    <div class="phase-desc">Prerequisites — confirm before building anything</div>
    <div class="phase-tag" style="background:rgba(107,138,255,0.12);color:var(--blue);">~45 min</div>
  </div>

  <div class="task-card open">
    <div class="task-header">
      <div class="task-id">1.1</div>
      <div class="task-title">Confirm your tool mapping</div>
      <div class="task-ws ws-gov">Decision</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Before installing anything, confirm which of your tools fills each of the three WMS roles. Use the Tool Mapping Guide if you haven't already. Write it down: <strong>Design tool = ___. Code execution tool = ___. Governed file execution tool = ___.</strong> Everything else in this guide assumes you have an answer for all three.</p>
        <p>If you're unsure: default to <strong>Claude Desktop + Claude Code + Cursor</strong>. All three are free to trial, all three are validated, and you can migrate roles to your preferred tools later once you understand the system from the inside.</p>
        <p>Throughout this guide, steps are written against the Claude Desktop + Cursor + Claude Code reference implementation. If you mapped different tools in the step above, substitute your tool names wherever these appear. The process is identical — only the tool names change.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">1.2</div>
      <div class="task-title">Install and verify Python 3</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Run <code>python3 --version</code> in a terminal. You need 3.8 or later. If not installed, use your OS package manager or python.org. The validator script and local dashboard server both require Python 3 — nothing else will work without it.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">1.3</div>
      <div class="task-title">Initialise a Git repository</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Create your project folder and run <code>git init</code> inside it. If a repository already exists for this project, use that. The validator script requires Git to register its pre-commit hook — the hook is what enforces the audit chain on every commit.</p>
        <p>Folder name recommendation: use something short and path-safe. No spaces. e.g. <code>ai-implementation</code></p>
        <p>Make an initial commit now — even an empty one — so the hook has a baseline to work from: <code>git commit --allow-empty -m "init"</code></p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">1.4</div>
      <div class="task-title">Configure your design tool's file access</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Point your design tool at your repository root. For Claude Desktop, this means configuring the filesystem MCP server in <code>claude_desktop_config.json</code> to include your repo path. For other tools, configure project-level file access according to their documentation. The design tool must be able to read files from your repo at session start.</p>
        <p><strong>Critical:</strong> Verify the design tool can actually read a file from the repo before moving on. Open a test session, ask it to read <code>README.md</code>, and confirm the content is returned. If this doesn't work, nothing downstream will work as intended.</p>
      </div>
    </div>
  </div>
</div>

<div class="banner banner-blue">
  <strong>🔵 Gate 1 — Before building the WMS files</strong><br><br>
  All of the following must be true before proceeding:
  <ul style="padding-left:16px;margin-top:8px;">
    <li>Three tool roles are confirmed and written down</li>
    <li>Python 3 installed and verified</li>
    <li>Git repo initialised with at least one commit</li>
    <li>Design tool can read a file from the repo</li>
  </ul>
</div>

<div class="divider"></div>

<!-- DAY 1 LATE MORNING -->
<div class="phase-block">
  <div class="phase-title-row">
    <div class="phase-pip" style="background:var(--teal);"></div>
    <div class="phase-name">Day 1 — Late morning</div>
    <div class="phase-desc">Build the WMS infrastructure</div>
    <div class="phase-tag" style="background:rgba(52,211,153,0.12);color:var(--teal);">~2 hours</div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">2.1</div>
      <div class="task-title">Read Spec A in full before writing a single file</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Spec A establishes the process discipline the entire system depends on. The files you're about to build are only useful in the context of the session ritual, the briefing format, and the SKILL file conventions Spec A defines. Do not skip this. A WMS built without reading Spec A is infrastructure without a methodology — it will appear to work and produce no value.</p>
        <p><strong>Estimated read time: 40 minutes.</strong> Take notes as you read. Write down anything that prompts a question — those questions become your first interaction with AIValueWorx after the build session, and each one is a gap in the specification that will be addressed.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">2.2</div>
      <div class="task-title">Use your code execution tool to build the Spec B file structure</div>
      <div class="task-ws ws-pilot">AI-assisted</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Open your code execution tool (e.g. Claude Code) in your repo directory. Provide it with Spec B and the following instruction: <strong>"Working from the build sequence in Appendix D of this specification, create the complete WMS file structure in this repository. Do not deviate from the schema or file naming. Flag any step you are uncertain about rather than interpreting it."</strong></p>
        <p>Files it will create: <code>Claude_Project_Files/dashboard.json</code>, <code>Claude_Project_Files/INDEX.md</code>, <code>Claude_Project_Files/REGISTRY.md</code>, <code>tools/validate_dashboard.py</code>, <code>Claude_Project_Files/dashboard.html</code></p>
        <p>Standing governance files: <code>CLAUDE.md</code>, <code>.cursor/rules/api_cost_governance.mdc</code></p>
        <p>This step uses AI to build infrastructure from a specification — which is the system working as designed. Watch how it interprets the spec; any deviation is information about where the spec needs clarification.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">2.3</div>
      <div class="task-title">Adapt the three dashboard constants for your context</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Open <code>Claude_Project_Files/dashboard.html</code> and update the three configuration constants at the top of the file: <strong>TOOLS</strong> (your three mapped tools), <strong>TOOL_ORDER</strong> (the display sequence), and <strong>PROJECTS</strong> (your workstream names). Everything else in the dashboard is driven by <code>dashboard.json</code> and should not be edited directly.</p>
        <p>TOOLS example: <code>{ "design": "Claude Desktop", "code": "Claude Code", "execute": "Cursor" }</code></p>
        <p>PROJECTS should match the workstream names you'll use in dashboard.json task entries. If you're starting with the pre-populated task library, these names will be provided — do not invent your own yet.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">2.4</div>
      <div class="task-title">Install the pre-commit hook and run the validator</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>The validator script registers itself as a Git pre-commit hook. Run it once manually first to confirm it works: <code>python3 tools/validate_dashboard.py</code>. A clean run produces no output. Any error output tells you exactly what is inconsistent in the current state — fix those before committing.</p>
        <p>To install as a pre-commit hook: <code>cp tools/validate_dashboard.py .git/hooks/pre-commit &amp;&amp; chmod +x .git/hooks/pre-commit</code></p>
        <p>From this point forward, any commit that fails validation is blocked. This is the governance-as-code principle in operation. Do not disable the hook — if a commit is being blocked, fix the inconsistency rather than bypassing it.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">2.5</div>
      <div class="task-title">Serve the dashboard locally and confirm it renders</div>
      <div class="task-ws ws-tech">Verify</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Run <code>python3 -m http.server 8000 --directory Claude_Project_Files</code> and open <code>http://localhost:8000/dashboard.html</code> in a browser. You should see the tool band with your configured tool names and an empty task area. If the dashboard is blank or shows errors, check that <code>dashboard.json</code> is valid JSON and that the PROJECTS constants match what's in the JSON.</p>
      </div>
    </div>
  </div>
</div>

<div class="banner banner-green">
  <strong>🟢 Gate 2 — End of Day 1</strong><br><br>
  The infrastructure is ready when all of these are true:
  <ul style="padding-left:16px;margin-top:8px;">
    <li>All Spec B files exist in the correct locations</li>
    <li>Dashboard constants updated for your tools and projects</li>
    <li>Validator runs clean with no errors</li>
    <li>Pre-commit hook installed and active</li>
    <li>Dashboard renders correctly at localhost:8000</li>
    <li>CLAUDE.md and governance .mdc file in place</li>
  </ul>
</div>

<div class="divider"></div>

<!-- DAY 2 -->
<div class="phase-block">
  <div class="phase-title-row">
    <div class="phase-pip" style="background:var(--green);"></div>
    <div class="phase-name">Day 2</div>
    <div class="phase-desc">Load the methodology — task library and SKILL seed</div>
    <div class="phase-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">~1 hour</div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">3.1</div>
      <div class="task-title">Load the pre-populated task library into dashboard.json</div>
      <div class="task-ws ws-pilot">AI-assisted</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>The pre-populated task library is provided as a JSON fragment by AIValueWorx. Use your governed file execution tool (e.g. Cursor) to merge it into <code>dashboard.json</code> following the briefing you'll receive alongside the library. Do not edit <code>dashboard.json</code> directly in a text editor without a briefing — this is the first governed write operation and it establishes the pattern for everything that follows.</p>
        <p><strong>Why this matters:</strong> The first time you make a change via a briefing rather than a direct edit, the audit chain starts. Every subsequent change will be traceable. Starting this way from day one costs nothing and builds the habit that makes the whole system reliable.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">3.2</div>
      <div class="task-title">Copy the SKILL library seed into Claude_Project_Files/Skills/</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>The SKILL seed files are provided as a folder by AIValueWorx. Copy the entire folder to <code>Claude_Project_Files/Skills/</code>. Each file follows the SKILL format defined in Spec A — read two or three of them to understand the structure before your first session. These files will be referenced in your INDEX.md Skills Inventory table.</p>
        <p>After copying, update the Skills Inventory table in INDEX.md to list each SKILL file with its domain tag. Your code execution tool can do this from the file listing — ask it to "read the YAML front matter from each file in Claude_Project_Files/Skills/ and generate the Skills Inventory table for INDEX.md."</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">3.3</div>
      <div class="task-title">Run the validator and commit</div>
      <div class="task-ws ws-tech">Verify</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Run <code>python3 tools/validate_dashboard.py</code>. Every task loaded from the library should have a corresponding entry in <code>REGISTRY.md</code> — the library import briefing will have added these. If the validator flags missing registry entries, add them before committing. This is the first real test of the governance chain end-to-end.</p>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- DAY 3 -->
<div class="phase-block">
  <div class="phase-title-row">
    <div class="phase-pip" style="background:var(--amber);"></div>
    <div class="phase-name">Day 3</div>
    <div class="phase-desc">Your first real working session</div>
    <div class="phase-tag" style="background:rgba(251,191,36,0.12);color:var(--amber);">~2 hours</div>
  </div>

  <p>The first session has a specific job: validate that the system works as designed, not just that it was built correctly. You're looking for the session ritual to feel coherent and for the design tool to produce a useful briefing. You are not trying to complete a task — you are testing the machinery.</p>

  <div class="banner banner-blue">
    <strong>Standard Session Ritual — every session follows this structure</strong><br>
    <em>Established in Spec A · Do not skip steps in the first four sessions</em><br><br>
    <strong>Open</strong> — Design tool reads context<br>
    Load <code>INDEX.md</code> (session navigation), <code>dashboard.json</code> (current task state), and relevant SKILL files. Design tool confirms: "Here is what I see as the current state, and here is what I recommend working on today."<br><br>
    <strong>Work</strong> — Briefing + execution cycle<br>
    Design tool produces a briefing → you review and approve → governed file execution tool applies it step by step → validator runs clean → commit.<br><br>
    <strong>Close</strong> — The Compound Step<br>
    Review what was learned or decided. Write at least one SKILL file if a new pattern was encountered. Update <code>INDEX.md</code>. Commit the session close state.
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">4.1</div>
      <div class="task-title">Open the session — load context into your design tool</div>
      <div class="task-ws ws-tech">Verify</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Start a new session in your design tool. Provide <code>INDEX.md</code>, <code>dashboard.json</code>, and the SKILL files marked as relevant to today's work in the INDEX.md Skills Inventory. Then ask: <strong>"Please read these files and give me the current state of the implementation, identify the highest-priority next task, and explain why."</strong></p>
        <p><strong>What good looks like:</strong> The design tool accurately summarises the task state, identifies a specific task from the library as the next priority based on its dependencies and status, and gives a clear rationale. If it produces a vague or generic response, check that the files were actually loaded — ask it to quote a specific line from INDEX.md to confirm.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">4.2</div>
      <div class="task-title">Request a briefing for the first task</div>
      <div class="task-ws ws-pilot">AI-assisted</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Ask the design tool to produce a briefing for the task it identified. The briefing format is defined in Spec A — it should include a pre-flight file list with expected states, numbered steps each governing a single governed-file change, and explicit done criteria. Review it carefully. If any step is ambiguous enough that you'd have to interpret it to execute it, send it back for revision before proceeding.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">4.3</div>
      <div class="task-title">Execute the briefing using your governed file execution tool</div>
      <div class="task-ws ws-pilot">AI-assisted</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Hand the briefing to your governed file execution tool (e.g. Cursor). Ask it to execute the briefing step by step, confirming the pre-flight stamp for each file before modifying it. After execution, run the validator, and commit if clean. The commit message should reference the briefing by name.</p>
        <p><strong>If the validator blocks the commit:</strong> Read the error output precisely — it tells you exactly which rule is violated. Fix that specific thing and retry. Do not remove the hook or force-push. The validator blocking a commit is the system working correctly.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">4.4</div>
      <div class="task-title">Close the session — the Compound Step</div>
      <div class="task-ws ws-pilot">AI-assisted</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>Before closing the design tool session, ask it: <strong>"What did we learn or decide in this session that isn't already captured in the SKILL library? Produce a SKILL file draft for the most significant new pattern."</strong> Review the draft, refine it if needed, and save it to <code>Claude_Project_Files/Skills/</code>. Update the INDEX.md Skills Inventory. This is the most important habit in the entire system — the session close is where institutional memory is created.</p>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- DAYS 4-5 -->
<div class="phase-block">
  <div class="phase-title-row">
    <div class="phase-pip" style="background:var(--purple);"></div>
    <div class="phase-name">Days 4–5</div>
    <div class="phase-desc">Calibrate and handover check</div>
    <div class="phase-tag" style="background:rgba(167,139,250,0.12);color:var(--purple);">~1 hour total</div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">5.1</div>
      <div class="task-title">Day 4: Note what felt wrong and send it to AIValueWorx</div>
      <div class="task-ws ws-cap">Human</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>After the first real session, write down everything that felt awkward, unclear, or didn't work as the spec suggested it should. These are not implementation errors — they are specification gaps or tool-mapping decisions that need adjustment. Send this list before your second session. Each item either produces a revised spec note or a new SKILL file.</p>
      </div>
    </div>
  </div>

  <div class="task-card">
    <div class="task-header">
      <div class="task-id">5.2</div>
      <div class="task-title">Day 5: A second person runs a session cold</div>
      <div class="task-ws ws-tech">Verify</div>
      <div class="task-expand">▾</div>
    </div>
    <div class="task-body">
      <div style="grid-column:1/3;">
        <p>The ultimate test of the system: a colleague who was not involved in the build opens a session using only the files in the repository and the session ritual from Spec A. If they can identify the current state, understand the next priority, and produce a valid briefing without asking you a question, the system is working. If they can't, what they had to ask you is what's missing from INDEX.md or the SKILL library.</p>
        <p><strong>What you're testing:</strong> Is the knowledge layer rich enough to be self-explanatory to a new participant? Every question the second person has to ask identifies a gap. That gap is either a new SKILL file or a revision to INDEX.md — never an oral explanation that doesn't get written down.</p>
      </div>
    </div>
  </div>
</div>
