---
theme: default
title: Shop 6 Agentic
colorSchema: light
fonts:
  sans: Nunito Sans
  serif: Rubik
  mono: JetBrains Mono
transition: fade
mdc: true
layout: cover
---

# Shop 6 Agentic

Our daily workflow with agents

<div class="mt-7 flex items-center gap-4" aria-label="A playful agent passing work along">
  <div class="agent-mascot animate-agent-bob rounded-2xl bg-[#2F6DB5] px-4 py-3 text-3xl text-white">🤖 <span class="text-sm font-semibold">agent</span></div>
  <div class="agent-task animate-agent-pass rounded-xl border-2 border-[#D9772B] bg-white px-4 py-3 text-sm"><span class="font-semibold text-[#D9772B]">you</span> decide → next task</div>
</div>

<div class="mt-8 text-sm opacity-70">Shop 6 · Engineering sharing</div>

<style>
@keyframes agent-bob { 0%, 100% { transform: translateY(0) rotate(-2deg); } 50% { transform: translateY(-8px) rotate(2deg); } }
@keyframes agent-pass { 0%, 100% { transform: translateX(0); } 50% { transform: translateX(12px); } }
.animate-agent-bob { animation: agent-bob 2s ease-in-out infinite; }
.animate-agent-pass { animation: agent-pass 2s ease-in-out infinite; }
@media (prefers-reduced-motion: reduce) { .animate-agent-bob, .animate-agent-pass { animation: none; } }
</style>

<!--
Share how Shop 6 uses agents in daily delivery, what we have learned, and how our engineering role changes as agents handle implementation. Keep current practice distinct from proposed improvements.
-->


---

<div class="mx-auto w-full max-w-full text-center">

# Our workflow

<p class="text-xl">From ticket to implementation, review, and docs.</p>

```mermaid
flowchart LR
  subgraph Prepare
    direction TB
    A[Ticket refinement] --> B[Issue]
    B --> C[Triage]
    C --> D[Ready for implementation]
  end
  subgraph Deliver
    direction TB
    D --> E[Implement]
    E --> F[Review]
    F -->|Comments| G[Remediate comments]
    G --> F
    F -->|Ready to approve| H[Approve]
    H --> I[Merge]
    I --> J[Sync docs]
  end
  classDef work fill:#2F6DB5,stroke:#2F6DB5,color:#ffffff
  classDef gate fill:#D9772B,stroke:#D9772B,color:#ffffff
  class A,B,E,G,J work
  class C,D,F,H,I gate
```

<!--
This is the current Shop 6 sequence supplied by the team: ticket refinement → issue → triage → ready for implementation → implement → review → remediate comments → review → approve → merge → sync docs. Review and remediation repeat until the changes are ready for approval. Approval is separate from merge. Colors distinguish execution steps from decision/checkpoint stages; they do not assign an unconfirmed human or agent owner to triage or readiness.
-->

</div>

---

# Agentic workflows

<p class="text-xl text-slate-600">At Shop 6, we use GitHub Agentic Workflows to automate daily tasks.</p>

<div class="mt-6 grid grid-cols-3 gap-4">
  <div class="rounded-2xl border border-slate-300 p-5">
    <div class="text-xl font-bold">Implementation planning</div>
    <p class="mt-3 text-base">Read the issue and repository context. Prepare the approach, task breakdown, and verification plan.</p>
    <div class="mt-4 border-t pt-3 text-sm font-semibold text-[#2F6DB5]">Output: a reviewable implementation plan</div>
  </div>
  <div class="rounded-2xl border border-slate-300 p-5">
    <div class="text-xl font-bold">Task implementation</div>
    <p class="mt-3 text-base">Work from a ready issue and spec. Implement the scoped change, run checks, and return evidence.</p>
    <div class="mt-4 border-t pt-3 text-sm font-semibold text-[#2F6DB5]">Output: changes ready for review</div>
  </div>
  <div class="rounded-2xl border border-slate-300 p-5">
    <div class="text-xl font-bold">Documentation updates</div>
    <p class="mt-3 text-base">Find docs affected by merged changes. Update them to match the implementation and prepare a docs PR.</p>
    <div class="mt-4 border-t pt-3 text-sm font-semibold text-[#2F6DB5]">Output: documentation changes to review</div>
  </div>
</div>
<div class="mt-5 rounded-xl bg-[#2F6DB5] p-4 text-center text-base text-white">Configured trigger → focused agent task → reviewable output + evidence</div>
<div class="mt-3 text-xs opacity-70"><a href="https://github.github.com/gh-aw/about/" class="underline">GitHub Agentic Workflows</a> · Agent tasks run through GitHub Actions.</div>

<!--
The team identifies three uses of GitHub Agentic Workflows: implementation planning, task implementation, and documentation updates. Explain their inputs and reviewable outputs, then show the actual configured triggers and artifacts in the demo; do not invent label names, commands, or automatic stage transitions. GitHub Agentic Workflows defines agent tasks using Markdown instructions and configuration and runs them through GitHub Actions. Official reference: https://github.github.com/gh-aw/about/. In Shop 6, these tasks fit inside the current delivery flow; triage, readiness, the review/remediation loop, approval, and merge remain explicit stages.
-->

---

# What agents do, what we do

<div class="mt-6 grid grid-cols-2 gap-5">
  <div class="rounded-2xl border-2 border-[#2F6DB5] p-5">
    <div class="text-2xl font-bold text-[#2F6DB5]">Agents</div>
    <ul class="mt-4 space-y-3 text-lg">
      <li>Gather context and draft plans</li>
      <li>Implement tasks and run checks</li>
      <li>Review changes and remediate comments</li>
      <li>Update documentation</li>
    </ul>
  </div>
  <div class="rounded-2xl border-2 border-[#D9772B] p-5">
    <div class="text-2xl font-bold text-[#D9772B]">We</div>
    <ul class="mt-4 space-y-3 text-lg">
      <li>Understand the business and choose priorities</li>
      <li>Design solutions and define success</li>
      <li>Set boundaries and verify evidence</li>
      <li>Own approval, merge, and outcomes</li>
    </ul>
  </div>
</div>

<!--
Agents carry more execution across the Shop 6 workflow: context gathering, planning, implementation, checks, review assistance, comment remediation, and documentation updates. Engineers remain responsible for business priorities, design decisions, clear acceptance criteria, boundaries, and acceptance of the result. Agent review supports the decision; engineers own approval and merge. Keep triage and readiness as explicit workflow stages without inventing their automation or ownership.
-->

---

# What the engineering team needs to do

<div class="mt-5 grid grid-cols-3 gap-4">
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Use agents daily</div>
    <p class="mt-2 text-base">Delegate focused tasks across planning, coding, review, and docs.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Write clear specs</div>
    <p class="mt-2 text-base">Define business value, design, scope, and acceptance criteria.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Set boundaries</div>
    <p class="mt-2 text-base">State what to do, what to avoid, and when to stop or ask.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Choose the right model</div>
    <p class="mt-2 text-base">Match task complexity, quality needs, speed, and cost.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Control quality and spend</div>
    <p class="mt-2 text-base">Require evidence. Set cost, time, and retry limits.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Improve the workflow</div>
    <p class="mt-2 text-base">Turn lessons into better specs, rules, skills, and checks.</p>
  </div>
</div>

<!--
These are the team's ongoing responsibilities and recommended improvements, not a claim that every control is already automated. Keep AGENTS.md, wiki, and repository context useful. Give each task a focused spec with do/don't instructions, acceptance evidence, and clear stop conditions: done, blocked, budget exhausted, or repeated failures. Choose the model based on observed task quality, cost, and speed. Enforce spending and runtime caps in the runner or provider where supported; a prompt alone is not a reliable hard cap. Verify diffs, tests, and spec coverage before acceptance. Save lessons in shared instructions, skills, templates, and checks so future tasks improve.
-->

---

# What we learn

<p class="text-xl text-slate-600">A daily loop: business goal → spec → bounded execution → evidence → learn.</p>

<div class="mt-5 grid grid-cols-2 gap-4">
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Before: make the work clear</div>
    <p class="mt-2 text-base">Define value, design, acceptance criteria, scope, model, and budget. Decide what needs a human.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">During: give autonomy within limits</div>
    <p class="mt-2 text-base">Use focused tasks and checkpoints. Stop when done, blocked, or at the cost / time / retry cap.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">After: accept with evidence</div>
    <p class="mt-2 text-base">Review the diff, tests, and spec coverage. Compare delivery time, defects, rework, and spend.</p>
  </div>
  <div class="rounded-2xl border border-slate-300 p-4">
    <div class="text-lg font-bold">Learn: change the workflow</div>
    <p class="mt-2 text-base">Too expensive? Add enforced budget caps. Repeated mistakes? Update specs, rules, tests, or skills.</p>
  </div>
</div>
<div class="mt-4 text-center text-base font-semibold">Keep the useful lesson. Check that the next run actually improves.</div>

<!--
This is a proposed daily habit, not a claim that all these controls are already automated at Shop 6. Add agents to more steps: context gathering, ticket refinement, design alternatives, implementation, testing, review, and docs. Separate independent tasks only when the extra coordination and model spend are justified. Example lesson: an expensive run should lead to an enforced runner/provider spending limit where available, a timebox, limited retries, and a clear stop report. Budget exhaustion means report partial progress and ask for a decision; it does not mean silently starting a new run. For ambiguous work, improve the spec and escalation rule. For recurring defects, add a regression check. Save useful lessons in AGENTS.md, skills, templates, or the workflow and verify the effect on later tasks. Measure accepted delivery and business outcomes, not just lines of code or agent activity.
-->

---

# Demo

<p class="text-xl text-slate-600">One task through the Shop 6 workflow.</p>

<div class="mt-6 grid grid-cols-3 gap-4">
  <div class="rounded-2xl border border-slate-300 p-5"><div class="text-xl font-bold">1 · Plan</div><p class="mt-3 text-base">Refined ticket → issue → triage → ready. Show the implementation plan and boundaries.</p></div>
  <div class="rounded-2xl border border-slate-300 p-5"><div class="text-xl font-bold">2 · Implement &amp; review</div><p class="mt-3 text-base">Show the changes and checks. Review → remediate comments → review → approve → merge.</p></div>
  <div class="rounded-2xl border border-slate-300 p-5"><div class="text-xl font-bold">3 · Sync docs</div><p class="mt-3 text-base">Show the documentation workflow and the resulting docs PR.</p></div>
</div>
<div class="mt-7 rounded-xl bg-[#D9772B] p-4 text-center text-lg text-white">Watch for: what the agent does, where we decide, and what proves the task is done.</div>

<!--
Use a real Shop 6 issue and its configured GitHub Agentic Workflow runs. Show the actual trigger, input instructions, implementation plan, code diff, check results, review comments, remediation, approval, merge, and documentation output. Use completed runs where a live run would take too long; say when an artifact is from a previous run. Focus on the daily workflow rather than setup instructions. End by connecting one observed lesson to a concrete spec, boundary, budget, or workflow improvement. This slide is a demo guide, not an instruction to publish issues, dispatch workflows, approve, or merge through this presentation repository.
-->
