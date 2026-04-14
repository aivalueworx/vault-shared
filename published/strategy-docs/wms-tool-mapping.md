---
layout: aivalueworx-base.njk
title: "Mapping your tools<br><strong>to the three WMS roles.</strong>"
eyebrow: "AIValueWorx — Workflow Management System"
meta: "Technical Guide · For your implementation lead · April 2026"
navTitle: "Tool mapping guide"
navSection: "Guides"
order: 6
permalink: "/docs/wms-tool-mapping.html"
description: "Three WMS roles across stacks"
---

<p class="section-intro">The WMS doesn't require a specific tool stack. It requires <strong>three roles</strong> to be filled — design, code execution, and governed file execution. Your organisation almost certainly has tools that can play each role already. This guide helps you identify which tools map where, understand what each role actually does, and know what to do if you have a gap.</p>

<div class="section-label">The three roles — what each one does and doesn't do</div>

<div class="card-grid cols-3">
  <div class="card">
    <div class="card-num c-blue">ROLE 1</div>
    <div class="card-title">The Design Tool</div>
    <div class="card-body">
      <p><em>Reference implementation: Claude Desktop</em></p>
      <p><strong>Responsible for</strong></p>
      <ul style="padding-left:16px;">
        <li>Reading project state at session start</li>
        <li>Reasoning about what to do next</li>
        <li>Producing briefing documents for other tools</li>
        <li>Answering "what should we build and why"</li>
        <li>Capturing knowledge into SKILL files</li>
      </ul>
      <p style="margin-top:12px;"><strong>Never does</strong></p>
      <p>Write directly to governed files (dashboard.json, INDEX.md, SKILL files). If a design tool writes directly to governed files, the audit chain is broken and cannot be recovered.</p>
    </div>
  </div>
  <div class="card">
    <div class="card-num c-teal">ROLE 2</div>
    <div class="card-title">The Code Execution Tool</div>
    <div class="card-body">
      <p><em>Reference implementation: Claude Code</em></p>
      <p><strong>Responsible for</strong></p>
      <ul style="padding-left:16px;">
        <li>Running scripts and pipelines</li>
        <li>Building tools and infrastructure</li>
        <li>Executing long-running or API-driven work</li>
        <li>Running the validator script</li>
        <li>Serving the local dashboard</li>
      </ul>
      <p style="margin-top:12px;"><strong>Never does</strong></p>
      <p>Make architectural decisions or produce briefings. It implements; it does not design. A code execution tool that also designs introduces untracked decisions.</p>
    </div>
  </div>
  <div class="card">
    <div class="card-num c-green">ROLE 3</div>
    <div class="card-title">The Governed File Execution Tool</div>
    <div class="card-body">
      <p><em>Reference implementation: Cursor</em></p>
      <p><strong>Responsible for</strong></p>
      <ul style="padding-left:16px;">
        <li>Applying changes to governed files</li>
        <li>Verifying pre-flight stamps before writing</li>
        <li>Executing cleanup briefings step-by-step</li>
        <li>Committing changes to version control</li>
        <li>Archiving completed tasks</li>
      </ul>
      <p style="margin-top:12px;"><strong>Never does</strong></p>
      <p>Interpret or redesign a briefing it receives. If a step is ambiguous, it stops and flags — it does not fill in the gap. An execution tool that interprets produces untracked decisions.</p>
    </div>
  </div>
</div>

<div class="divider"></div>

<div class="section-label">How to identify which of your tools plays each role</div>

### Design Tool questions

1. Can it hold a long project context in one session — reading multiple files, maintaining state across a conversation?
2. Does it produce written analysis and structured documents, not just code?
3. Can you upload background files (specs, registries, SKILL files) for it to read at session start?
4. Is it conversational — can you iterate on a briefing with it through dialogue?
5. Is it _not_ primarily running code or modifying files directly?

### Code Execution Tool questions

1. Can it run terminal commands and Python scripts in your environment?
2. Does it have access to your file system — can it create, read, and modify files?
3. Can it handle multi-step agentic tasks without a human approving each step?
4. Is it fast and cheap enough to run frequently — validator checks, dashboard refreshes?
5. Can it install Python packages and run a local web server?

### Governed File Execution Tool questions

1. Is it tightly integrated with your IDE or code editor — can it open and edit specific files?
2. Can it follow a numbered sequence of precise instructions reliably, without skipping steps?
3. Does it have native git integration — can it commit and push without switching tools?
4. Will it stop and flag rather than interpret an ambiguous instruction?
5. Can it read a briefing file and execute it as a task, not a conversation?

<div class="divider"></div>

<div class="section-label">Common enterprise tool stacks and how they map</div>

<p class="section-intro">Most enterprise AI deployments will recognise one of these configurations. Find the closest match — then read the notes column for what to watch for.</p>

<table>
  <thead>
    <tr>
      <th>Stack profile</th>
      <th>Role 1 — Design</th>
      <th>Role 2 — Code execution</th>
      <th>Role 3 — Governed file exec</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Microsoft-first</strong></td>
      <td><span class="cat-tag">OK</span> Copilot Chat (M365) or Azure OpenAI in a chat UI</td>
      <td><span class="cat-tag">OK</span> GitHub Copilot Agent or Azure OpenAI with function calling</td>
      <td><span class="cat-tag">OK</span> GitHub Copilot in VS Code with Edits mode</td>
      <td>Copilot Chat context windows are shorter — keep session start files lean. Test briefing execution reliability in VS Code before committing to this path.</td>
    </tr>
    <tr>
      <td><strong>Claude-native</strong></td>
      <td><span class="cat-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">Strong</span> Claude Desktop with project files</td>
      <td><span class="cat-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">Strong</span> Claude Code</td>
      <td><span class="cat-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">Strong</span> Cursor</td>
      <td>The reference implementation. All three tools are designed to work together and have been validated on this exact workflow. Recommended starting point even if you migrate later.</td>
    </tr>
    <tr>
      <td><strong>GitHub-centric</strong></td>
      <td><span class="cat-tag">OK</span> ChatGPT Enterprise or Claude (API)</td>
      <td><span class="cat-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">Strong</span> GitHub Copilot Agent / Actions</td>
      <td><span class="cat-tag" style="background:rgba(34,197,94,0.12);color:var(--green);">Strong</span> GitHub Copilot in VS Code</td>
      <td>Strong on execution side. The design role needs a tool with long context and file upload — confirm your ChatGPT/Claude deployment supports project-level file persistence.</td>
    </tr>
    <tr>
      <td><strong>Internal LLM deployment</strong></td>
      <td><span class="cat-tag" style="background:rgba(251,191,36,0.12);color:var(--amber);">Verify</span> Internal chat UI on hosted model</td>
      <td><span class="cat-tag" style="background:rgba(251,191,36,0.12);color:var(--amber);">Verify</span> Scripted API calls to internal endpoint</td>
      <td><span class="cat-tag">OK</span> VS Code + any AI edit assistant</td>
      <td>Feasible if the internal model has sufficient reasoning capability and context length. Test the design role specifically — weak reasoning on the design tool degrades briefing quality across all downstream work.</td>
    </tr>
    <tr>
      <td><strong>Google Workspace</strong></td>
      <td><span class="cat-tag">OK</span> Gemini Advanced or Vertex AI chat</td>
      <td><span class="cat-tag">OK</span> Gemini Code Assist or Cloud Shell with AI</td>
      <td><span class="cat-tag">OK</span> Gemini Code Assist in VS Code / IntelliJ</td>
      <td>Reasonable fit. Gemini's long context is an advantage for the design role. Governed file execution is the least-tested Gemini use case — validate briefing adherence before relying on it for governed writes.</td>
    </tr>
    <tr>
      <td><strong>Mixed / no standard</strong></td>
      <td><span class="cat-tag" style="background:rgba(107,138,255,0.12);color:var(--blue);">Choose</span> Any conversational AI with long context</td>
      <td><span class="cat-tag" style="background:rgba(107,138,255,0.12);color:var(--blue);">Choose</span> Any terminal-capable AI agent</td>
      <td><span class="cat-tag" style="background:rgba(107,138,255,0.12);color:var(--blue);">Choose</span> Any IDE-integrated AI with edit + git</td>
      <td>Use the questions above to map your tools to roles. The architecture is tool-agnostic. What matters is that the roles are filled and separated — not which specific product fills each one.</td>
    </tr>
  </tbody>
</table>

<div class="divider"></div>

<div class="section-label">If you have a gap — common situations and how to handle them</div>

<div class="banner banner-amber">
  <strong>No tool clearly fills the governed file execution role</strong><br><br>
  This is the most common gap. The simplest resolution: use your existing code editor (VS Code, IntelliJ) with any AI edit assistant, and rely on explicit human review of each briefing step before committing. The pre-flight stamp mechanism still works — the human reviewer becomes the verification step. Slower, but architecturally sound. As a second option, <strong>Cursor is free to trial</strong> and is the path of least resistance.
</div>

<div class="banner banner-amber">
  <strong>The available design tool has a short context window</strong><br><br>
  Keep the session start files small. The INDEX.md 80-line target exists precisely for this reason. Prioritise loading SKILL files relevant to the current task rather than the full library. If context limits are severe, consider the design tool for conversational reasoning only and have a human read and relay the key file contents — inelegant but functional.
</div>

<div class="banner banner-amber">
  <strong>One tool is being asked to fill two roles</strong><br><br>
  This is acceptable for the <strong>design + governed file execution</strong> combination in low-risk situations — one tool reads, reasons, and writes, with the human enforcing the pre-flight stamp check manually. It is <strong>not acceptable</strong> for the design + code execution combination, because the reasoning and execution traces become entangled and cannot be audited separately. Keep those two roles separated even if the same underlying model powers both tools.
</div>

<div class="banner banner-blue">
  <strong>The organisation requires all AI tools to route through a proxy or gateway</strong><br><br>
  The WMS architecture is unaffected by this — it communicates with AI tools through their normal interfaces (chat UI, IDE integration, CLI), not directly via API. If your proxy adds latency or rate limits, the main practical impact is on the code execution role for long-running tasks. The design and governed file execution roles are conversational and less sensitive to latency.
</div>

<div class="divider"></div>

<div class="section-label">The minimum viable starting configuration</div>

<div class="banner banner-blue">
  <strong>If you're unsure, start here.</strong> Use the reference implementation for the first four weeks regardless of your long-term tool strategy. <strong>Claude Desktop + Claude Code + Cursor</strong> can be running in a day. Once you understand the WMS from the inside, migrating individual roles to your preferred tools is straightforward — the roles are clean and the interfaces between them are just files.
</div>

### What "Spec A only" looks like

If procurement or IT approval blocks tool deployment, you can run **Spec A without Spec B** using nothing more than a text editor, a folder structure, and one AI chat tool. No dashboard, no validator, no JSON schema. The process discipline — sessions, briefings, SKILL files, the Compound Step — delivers value immediately and doesn't require any tooling approval.

### The one thing that must be right from day one

Whatever tools you use, **keep the design role separated from the write-to-governed-files role** from the first session. Everything else can be adjusted, migrated, or simplified. This separation is the audit chain. Once broken, it cannot be reconstructed retrospectively — you'd have to treat everything written before the break as untracked.
