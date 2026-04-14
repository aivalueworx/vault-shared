---
layout: aivalueworx-base.njk
title: "Task library framework.<br><strong>For review before full build.</strong>"
eyebrow: "AI Value Worx — Workflow Management System"
meta: "Working Document · Mike & Peter — internal · April 2026"
navTitle: "Task library framework"
navSection: "Reference"
order: 7
permalink: "/docs/wms-task-library-framework.html"
description: "Phase × workstream matrix and sample tasks"
---

<div class="banner banner-amber"><strong>This is a framework document, not a finished library.</strong> It proposes six phases, five workstreams, and ~72 tasks — with full done_when criteria written for one representative task per phase. The purpose is to validate the structure against what AI Value Worx actually delivers before the full 72-task build. Review questions are at the bottom. Every structural correction made here saves significant rework later.</div>

<div class="divider"></div>

<div class="section-label">Proposed library at a glance</div>

<div class="stats-row cols-5">
<div class="stat-cell"><div class="stat-num">6</div><div class="stat-label">Phases from readiness to sustained</div></div>
<div class="stat-cell"><div class="stat-num">5</div><div class="stat-label">Workstreams running across phases</div></div>
<div class="stat-cell"><div class="stat-num">~72</div><div class="stat-label">Total tasks in the full library</div></div>
<div class="stat-cell"><div class="stat-num">3–5</div><div class="stat-label">Verifiable done criteria per task</div></div>
<div class="stat-cell"><div class="stat-num">6</div><div class="stat-label">Sample tasks fully specified below</div></div>
</div>

<div class="divider"></div>

<div class="section-label">Phase × workstream structure — proposed</div>

<p class="section-intro">Each cell shows the 2–3 tasks that live at that intersection. The full library has ~2–4 tasks per populated cell. Empty cells are intentional — not every workstream is active in every phase.</p>

<div class="matrix-wrap">
<table class="matrix">
<thead><tr>
<th class="ws-header">Workstream ↓ / Phase →</th>
<th class="ph ph-1">Phase 1<br>Readiness</th>
<th class="ph ph-2">Phase 2<br>Governance</th>
<th class="ph ph-3">Phase 3<br>Pilot</th>
<th class="ph ph-4">Phase 4<br>Evaluate &amp; Decide</th>
<th class="ph ph-5">Phase 5<br>Scale</th>
<th class="ph ph-6">Phase 6<br>Sustain</th>
</tr></thead>
<tbody>
<tr>
<td>Governance<span class="task-count">16</span></td>
<td><div class="cell-tasks"><div class="cell-task">AI readiness audit</div><div class="cell-task">Data inventory</div><div class="cell-task">Risk register baseline</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">AI policy drafted</div><div class="cell-task">Acceptable use defined</div><div class="cell-task">Approval workflow set</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Data classification</div><div class="cell-task">Pilot governance applied</div><div class="cell-task">Incident log active</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Pilot risk review</div><div class="cell-task">Scale decision recorded</div><div class="cell-task">Governance updated for scale</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Vendor review</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Annual policy review cycle</div><div class="cell-task">Compliance audit</div></div></td>
</tr>
<tr>
<td>Pilot<span class="task-count">18</span></td>
<td><div class="cell-tasks"><div class="cell-task">Use case longlist</div><div class="cell-task">Prioritisation workshop</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Pilot brief written</div><div class="cell-task">Success metrics defined</div><div class="cell-task">Pilot team assembled</div><div class="cell-task">Tool access provisioned</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Week 1–4 running</div><div class="cell-task">Mid-point review</div><div class="cell-task">Pilot close review</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Results vs metrics</div><div class="cell-task">Build vs buy decision</div><div class="cell-task">Next pilot or scale brief</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Rollout plan</div><div class="cell-task">Second workstream pilot</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">—</div></div></td>
</tr>
<tr>
<td>Capability<span class="task-count">14</span></td>
<td><div class="cell-tasks"><div class="cell-task">Skills gap assessment</div><div class="cell-task">Learning path designed</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">AI literacy baseline</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Pilot team trained</div><div class="cell-task">Prompt library started</div><div class="cell-task">Lessons documented</div></div></td>
<td></td>
<td><div class="cell-tasks"><div class="cell-task">Internal champion programme</div><div class="cell-task">Onboarding pack for new users</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Community of practice launched</div><div class="cell-task">Annual skills review</div><div class="cell-task">External training reviewed</div></div></td>
</tr>
<tr>
<td>Technology<span class="task-count">12</span></td>
<td><div class="cell-tasks"><div class="cell-task">Tool landscape mapped</div><div class="cell-task">Integration constraints noted</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Security review of tools</div><div class="cell-task">Data residency confirmed</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Pilot stack deployed</div><div class="cell-task">Access controls in place</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Tech debt from pilot noted</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Production deployment</div><div class="cell-task">Monitoring in place</div><div class="cell-task">Integration to core systems</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Tech stack review</div></div></td>
</tr>
<tr>
<td>Change &amp; Comms<span class="task-count">12</span></td>
<td><div class="cell-tasks"><div class="cell-task">Stakeholder map</div><div class="cell-task">Sponsor confirmed</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Communication plan</div><div class="cell-task">Leadership narrative</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Pilot team comms</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Results communicated</div><div class="cell-task">Broader stakeholder update</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Organisation-wide launch comms</div><div class="cell-task">Resistance mapped and addressed</div></div></td>
<td><div class="cell-tasks"><div class="cell-task">Normalisation — AI as standard practice</div></div></td>
</tr>
</tbody>
</table>
</div>

<div class="divider"></div>

<div class="section-label">Sample tasks — one per phase, fully specified</div>

<p class="section-intro">These are representative tasks with complete done_when criteria, dependencies, and workstream assignment. <strong>This is the level of specificity the full library needs to maintain.</strong> Vague done criteria — "stakeholders are aligned," "governance is in place" — are unusable. Every criterion must be something a third party could walk in and verify without asking a question.</p>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#6B8AFF;"></div>
<span class="phase-name">Phase 1 — Readiness</span>
<span class="phase-desc">Understanding the starting point before committing to anything</span>
<span class="phase-tag" style="background:rgba(107,138,255,0.12);color:#6B8AFF;">~12 tasks</span>
</div>

<div class="task-card open">
<div class="task-header">
<div class="task-id">P1-GOV-01</div>
<div class="task-title">AI Readiness Audit</div>
<div class="task-ws ws-gov">Governance</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>A written audit document exists covering: current AI tool usage (sanctioned and unsanctioned), data handling practices, existing governance structures, and skills distribution across the organisation</li>
<li>Each of the four audit areas has a RAG status with specific evidence cited — not an opinion</li>
<li>At least three named stakeholders have reviewed and signed off on the document</li>
<li>The audit is registered in REGISTRY.md and its location is recorded</li>
<li>A summary of the top three readiness gaps is recorded in the WMS as a note on this task</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">none — first task</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">2–3 weeks including stakeholder interviews and document review</div>
</div>
</div>
<div class="task-note"><strong>Why this matters:</strong> The audit is the foundation everything else is built on. An organisation that skips it and goes straight to pilot selection will select the wrong pilot — one that looks tractable but runs into a governance or data problem that was visible from day one. The done_when criteria above are designed to prevent the "audit in name only" failure mode where a conversation gets filed as an audit.</div>
</div>
</div>
</div>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#34D399;"></div>
<span class="phase-name">Phase 2 — Governance</span>
<span class="phase-desc">Putting the rules in place before the first use case runs</span>
<span class="phase-tag" style="background:rgba(52,211,153,0.12);color:#34D399;">~10 tasks</span>
</div>

<div class="task-card">
<div class="task-header">
<div class="task-id">P2-GOV-02</div>
<div class="task-title">AI Acceptable Use Policy — drafted, reviewed, and ratified</div>
<div class="task-ws ws-gov">Governance</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>A policy document exists that specifies: permitted use cases, prohibited use cases, data handling requirements when using AI tools, employee responsibilities, and consequences of breach</li>
<li>The policy has been reviewed by legal or compliance — not just noted but formally cleared with a named reviewer and date recorded</li>
<li>The policy has been ratified by a named senior sponsor with authority to enforce it</li>
<li>All employees who will use AI tools in Phase 3 have confirmed receipt and understanding — confirmation method and date recorded</li>
<li>A review date is set (no more than 12 months from ratification) and owned by a named individual</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">P1-GOV-01</span> <span class="dep-tag">P2-GOV-01</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">3–4 weeks including legal review cycle</div>
</div>
</div>
<div class="task-note"><strong>Common failure mode:</strong> Policy drafted but never formally ratified — sits in a SharePoint folder, nobody is sure if it's in force. The done criteria above force ratification and distribution to be explicit, dated, and named. "In progress" cannot be the status on this task until all five criteria are met.</div>
</div>
</div>
</div>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#22C55E;"></div>
<span class="phase-name">Phase 3 — Pilot</span>
<span class="phase-desc">Running a bounded, governed, measurable first use case</span>
<span class="phase-tag" style="background:rgba(34,197,94,0.12);color:#22C55E;">~20 tasks</span>
</div>

<div class="task-card">
<div class="task-header">
<div class="task-id">P3-PIL-03</div>
<div class="task-title">Pilot success metrics defined and baselined</div>
<div class="task-ws ws-pilot">Pilot</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>A metrics document exists with at least two quantitative measures and one qualitative measure for the pilot — each with a current baseline value and a target value</li>
<li>Each metric has a named owner responsible for measuring it and a defined measurement method that does not rely on self-reporting alone</li>
<li>Baseline values are recorded with source and date — not estimates</li>
<li>The pilot team and sponsor have reviewed and agreed the metrics in a recorded session (date, attendees, decision noted)</li>
<li>Metrics are loaded into the WMS as task completion criteria for P3-PIL-05 (Pilot Close Review)</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">P2-PIL-01</span> <span class="dep-tag">P2-PIL-02</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">1 week with the pilot team</div>
</div>
</div>
<div class="task-note"><strong>Why baselines must be real:</strong> The most common pilot failure is metrics defined after the pilot starts, when the outcome is already visible. The requirement for pre-existing baseline values with source and date makes retroactive metric setting impossible to hide. If the baseline can't be measured before the pilot starts, the metric is probably the wrong one.</div>
</div>
</div>
</div>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#FBBF24;"></div>
<span class="phase-name">Phase 4 — Evaluate &amp; Decide</span>
<span class="phase-desc">Turning pilot results into a defensible next decision</span>
<span class="phase-tag" style="background:rgba(251,191,36,0.12);color:#FBBF24;">~8 tasks</span>
</div>

<div class="task-card">
<div class="task-header">
<div class="task-id">P4-PIL-01</div>
<div class="task-title">Scale vs stop decision — made and recorded</div>
<div class="task-ws ws-pilot">Pilot</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>A decision document exists that states: the decision (scale / iterate / stop), the three primary reasons supporting it, and the data from the pilot that drove each reason</li>
<li>The document explicitly addresses counter-arguments — why the decision was not the alternative</li>
<li>The decision has been made by a named individual with authority to commit budget for Phase 5 — not a committee recommendation</li>
<li>If scale: a Phase 5 brief exists as a draft and is registered in REGISTRY.md</li>
<li>If stop: a lessons document exists and is added to the SKILL library</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">P3-PIL-05</span> <span class="dep-tag">P4-GOV-01</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">1–2 weeks from pilot close</div>
</div>
</div>
<div class="task-note"><strong>The "stop" path is a first-class outcome.</strong> A pilot that results in a well-documented stop decision — with reasons and lessons captured in the SKILL library — is more valuable than a scale decision made without rigour. The done_when criteria treat both paths equally; neither is allowed to be undocumented.</div>
</div>
</div>
</div>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#A78BFA;"></div>
<span class="phase-name">Phase 5 — Scale</span>
<span class="phase-desc">Extending proven use cases across the organisation</span>
<span class="phase-tag" style="background:rgba(167,139,250,0.12);color:#A78BFA;">~14 tasks</span>
</div>

<div class="task-card">
<div class="task-header">
<div class="task-id">P5-CAP-02</div>
<div class="task-title">Internal AI champion programme — active</div>
<div class="task-ws ws-cap">Capability</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>At least three named individuals from different business units have been identified, agreed to the champion role, and have a written description of what that role entails</li>
<li>Each champion has completed the internal AI literacy programme (or equivalent) and has a record of completion</li>
<li>A regular champion meeting cadence exists (minimum monthly) with at least two meetings completed and notes recorded</li>
<li>At least one champion has independently run a team-level session without AI Value Worx involvement — session notes exist</li>
<li>Champion programme has a named owner inside the organisation who is responsible for it continuing after the engagement ends</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">P4-PIL-01</span> <span class="dep-tag">P5-CAP-01</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">6–8 weeks to establish</div>
</div>
</div>
<div class="task-note"><strong>The independence criterion is the critical one.</strong> A champion programme that requires AI Value Worx to run every session hasn't transferred capability — it's created dependency. The done criteria above require demonstrated independence before this task can close. "In progress" is the correct status until criterion 4 is met.</div>
</div>
</div>
</div>

<div class="phase-block">
<div class="phase-title-row">
<div class="phase-pip" style="background:#EF4444;"></div>
<span class="phase-name">Phase 6 — Sustain</span>
<span class="phase-desc">Making AI a normal part of how the organisation works</span>
<span class="phase-tag" style="background:rgba(239,68,68,0.12);color:#EF4444;">~8 tasks</span>
</div>

<div class="task-card">
<div class="task-header">
<div class="task-id">P6-GOV-01</div>
<div class="task-title">Annual AI governance review cycle — established</div>
<div class="task-ws ws-gov">Governance</div>
<div class="task-expand">▾</div>
</div>
<div class="task-body">
<div>
<div class="task-section-label">Done when</div>
<ul class="done-when">
<li>A calendar event exists for the first annual review, owned by a named individual, with the review scope defined in a linked brief</li>
<li>The review brief specifies what will be assessed: policy currency, tool landscape changes, incident log review, metrics performance, and skills state</li>
<li>At least one person inside the organisation could run the review without external support — their name is recorded against this task</li>
<li>The output of the review has a defined format (a structured update document) and the template for that document is registered in REGISTRY.md</li>
</ul>
</div>
<div>
<div class="task-section-label">Depends on</div>
<div class="deps-list"><span class="dep-tag">P5-GOV-01</span> <span class="dep-tag">P5-GOV-02</span></div>
<div style="margin-top:16px;">
<div class="task-section-label">Typical duration</div>
<div style="font-size:12.5px;font-weight:300;color:rgba(255,255,255,0.7);">Set up in final engagement session</div>
</div>
</div>
<div class="task-note"><strong>Phase 6 tasks are about handover, not delivery.</strong> Every task in this phase should have a named internal owner as a done criterion. If AI Value Worx is still required to run any Phase 6 process, the engagement has not transferred what it was supposed to. These tasks are the proof of capability transfer.</div>
</div>
</div>
</div>

<div class="divider"></div>

<div class="review-qs">
<div class="rq-title">Questions for Mike and Peter — before the full build</div>
<div class="rq-grid">
<div class="rq">Do these six phases match the actual AI Value Worx engagement journey, or are there phases missing, combined, or named differently in practice?</div>
<div class="rq">Are the five workstreams the right ones? Is there a workstream that's prominent in your engagements that isn't represented here — e.g. a Data workstream separate from Technology?</div>
<div class="rq">The done_when criteria are written to be verifiable by a third party. Are any of them unrealistic for the organisations you work with — things that sound right but would never actually happen?</div>
<div class="rq">Phase 3 has ~20 tasks — the largest phase. Does that reflect the actual weight of pilot work in an engagement, or is it inflated?</div>
<div class="rq">Are there task types that appear in real engagements that aren't represented in the matrix above — e.g. procurement tasks, integration tasks, board-level reporting tasks?</div>
<div class="rq">Should the library have a "pre-engagement" phase (tasks for the client to complete before AI Value Worx engages) or does Phase 1 Readiness cover that?</div>
<div class="rq">The "stop" path in Phase 4 is treated as a first-class outcome. Is that consistent with how AI Value Worx frames it to clients, or would clients find that framing uncomfortable?</div>
<div class="rq">For the enterprise extensions (multi-tab dashboard, deadlines, targets) — do those map to phases or to workstreams? i.e. is a deadline a phase-level milestone or a task-level attribute?</div>
</div>
</div>
