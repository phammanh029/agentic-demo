---
theme: default
title: From Prompting to Agentic Engineering
colorSchema: light
fonts:
  sans: Nunito Sans
  serif: Rubik
  mono: JetBrains Mono
transition: fade
mdc: true
duration: 60min
layout: cover
---

# From Prompting to Agentic Engineering

How we ship with agents at Shop 6 — and how it can speed up your tasks

<div class="mt-8 flex gap-3 text-lg">
  <span class="rounded-full bg-slate-200 px-5 py-2">Laptop optional</span>
  <span class="rounded-full border border-slate-400 px-5 py-2">Bring a real task</span>
</div>

<div class="mt-7 flex items-center gap-4" aria-label="A playful agent passing work along">
  <div class="agent-mascot animate-agent-bob rounded-2xl bg-[#2F6DB5] px-4 py-3 text-3xl text-white">🤖 <span class="text-sm font-semibold">agent</span></div>
  <div class="agent-task animate-agent-pass rounded-xl border-2 border-[#D9772B] bg-white px-4 py-3 text-sm"><span class="font-semibold text-[#D9772B]">you</span> decide → next task</div>
</div>

<div class="mt-8 text-sm opacity-70">Shop 6 · Tue 29 Sept · CodeLeap office</div>

<style>
@keyframes agent-bob { 0%, 100% { transform: translateY(0) rotate(-2deg); } 50% { transform: translateY(-8px) rotate(2deg); } }
@keyframes agent-pass { 0%, 100% { transform: translateX(0); } 50% { transform: translateX(12px); } }
.animate-agent-bob { animation: agent-bob 2s ease-in-out infinite; }
.animate-agent-pass { animation: agent-pass 2s ease-in-out infinite; }
@media (prefers-reduced-motion: reduce) { .animate-agent-bob, .animate-agent-pass { animation: none; } }
</style>

<!--
How Shop 6 works today, not a vendor demo. 60 minutes, one focused hands-on comparison, laptop optional. Keep a real task in mind for the end.
-->

---
layout: center
---

<div class="text-center text-xl opacity-70">Not 'AI or no AI?'</div>

# Who owns the context — and the feedback loop?

<div class="mx-auto mt-8 grid max-w-5xl grid-cols-2 gap-8">
  <div class="aspect-square max-w-[320px] justify-self-center rounded-full border-2 border-slate-300 bg-slate-100 p-8 text-center flex flex-col items-center justify-center">
    <div class="text-3xl font-bold">Context</div>
    <div class="mt-3 text-lg">ticket, repos, wiki, rules, history</div>
  </div>
  <div class="aspect-square max-w-[320px] justify-self-center rounded-full border-2 border-slate-300 bg-slate-100 p-8 text-center flex flex-col items-center justify-center">
    <div class="text-3xl font-bold">Feedback loop</div>
    <div class="mt-3 text-lg">who checks the result, who decides next</div>
  </div>
</div>

<!--
Everyone already uses AI somewhere. The question is who holds the context and who closes the loop. In prompting you do both; in agentic engineering you hand parts over, on purpose, with boundaries.
-->

---

<div class="absolute inset-0 flex flex-col items-center justify-center bg-slate-50 p-14 text-[#1E2530]">
  <div class="mb-8 inline-flex rounded-full bg-slate-200 px-5 py-2 text-lg font-semibold">QUICK PULSE · 2 MINUTES</div>
  <h1 class="text-center text-5xl font-bold">What do you think AI can handle in our work today?</h1>
  <div class="mt-10 max-w-5xl text-center text-3xl">Which tasks would you trust it with — and where would you still step in?</div>
</div>

<!--
Take a quick show of hands, then invite two short answers: which tasks would people delegate today, and where would they still step in? Keep it open and non-judgmental. Return to the question after the same-task comparison.
-->

---

<div class="mx-auto w-full max-w-full text-center">

# Shop 6 today: an agentic pipeline

<p class="text-2xl">One ticket. Several repos. Agents do the legwork, people decide.</p>

```mermaid
flowchart LR
  A[Refinement skill<br/>wiki · docs · repo evidence] --> R{{team reviews}}
  R --> B[create-implementation-issue<br/>context · approach · local draft]
  B --> S{{you publish + assign}}
  S --> C[Cloud agent<br/>Spec Kit · implements → PR]
  C --> D[/review workflow<br/>verdict + findings/]
  D --> M{{you merge}}
  M --> E[Docs-sync workflow<br/>out-of-sync docs → PR]
  classDef person fill:#D9772B,stroke:#D9772B,color:#ffffff
  classDef work fill:#2F6DB5,stroke:#2F6DB5,color:#ffffff
  class A,B,C,D,E work
  class R,S,M person
```

<!--
A skill refines the ticket using cross-repo knowledge (wiki, docs); the team reviews it. create-implementation-issue gathers context, finds the approach and saves a local issue draft. A person publishes the GitHub issue and assigns it to the cloud agent. On the PR, /review gives a verdict — approve or reject, with findings by severity and suggestions. A person merges. After merge, a workflow finds out-of-sync docs and opens a PR. Agents run most steps; people own the gates.
-->

</div>

---

# Both start with a prompt. The loop is different.

<div class="mt-7 grid grid-cols-1 gap-5">
  <div class="rounded-2xl border border-slate-300 p-5">
    <div class="mb-3 text-xl font-bold">Prompt-driven</div>
    <div class="flex items-center justify-between gap-2 whitespace-nowrap text-base">
      <span class="rounded-lg bg-[#D9772B] px-3 py-2 text-white">You</span><span>→</span><span>Prompt</span><span>→</span><span>Answer</span><span>→</span><span class="rounded-lg bg-[#D9772B] px-3 py-2 text-white">You</span><span>→</span><span>Prompt → Answer →</span><span class="rounded-lg bg-[#D9772B] px-3 py-2 text-white">You …</span>
    </div>
  </div>
  <div class="rounded-2xl border border-slate-300 p-5">
    <div class="mb-3 text-xl font-bold">Agentic</div>
    <div class="flex items-center justify-between gap-2 whitespace-nowrap text-base">
      <span class="rounded-lg bg-[#D9772B] px-3 py-2 text-white">You</span><span>→</span><span>Brief + boundaries</span><span>→</span><span class="rounded-xl bg-[#2F6DB5] px-4 py-3 text-center text-white">Agent: gather · draft · check</span><span>→</span><span>Evidence</span><span>→</span><span class="rounded-lg bg-[#D9772B] px-3 py-2 text-white">You decide</span>
    </div>
  </div>
</div>

<!--
Prompt-driven, you're the glue between every step. Agentic, you set the workflow and boundaries once; the agent loops and returns evidence. You move from doing steps to deciding at gates.
-->

---

# The agentic approach

<p class="text-xl text-slate-600">Six questions before you delegate</p>

<div class="mt-6 grid grid-cols-3 gap-4">
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">Who are we?</div>
    <div class="mt-1 text-sm text-slate-600">Project, conventions, rules</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> AGENTS.md, wiki, docs</div>
  </div>
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">What do we want?</div>
    <div class="mt-1 text-sm text-slate-600">The outcome, and what “done” means</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> refined ticket, acceptance criteria</div>
  </div>
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">How do I verify it?</div>
    <div class="mt-1 text-sm text-slate-600">Tests, evidence, who checks</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> tests, /review verdict, docs-sync</div>
  </div>
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">What must it not touch?</div>
    <div class="mt-1 text-sm text-slate-600">Scope and boundaries</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> sibling repos read-only, issue scope</div>
  </div>
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">When should it stop and ask?</div>
    <div class="mt-1 text-sm text-slate-600">Uncertainty, risky areas, repeated failures</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> team review, assign gate, three-failed-fixes rule</div>
  </div>
  <div class="rounded-2xl border border-slate-300 bg-white p-5">
    <div class="text-xl font-bold">What happens if it’s wrong?</div>
    <div class="mt-1 text-sm text-slate-600">The blast radius</div>
    <div class="mt-3 border-t pt-3 text-base"><b>Shop 6:</b> decides in-loop, cloud agent, or a workflow on its own</div>
  </div>
</div>

<!--
Before delegating, answer these six questions for the agent: who the project is, what outcome is wanted, how the result will be verified, what is out of scope, when to stop and ask, and what happens if the result is wrong. Shop 6 answers them through repository guidance, refined tickets and acceptance criteria, tests and review, read-only sibling repos, human review and assignment gates, and different execution modes for different blast radii.
-->

---
layout: section
---

<div class="absolute inset-0 grid place-content-center bg-[#1E2530] px-20 text-center text-white">
  <h1 class="text-6xl font-bold">Before · Prompt-driven</h1>
  <p class="mt-6 text-3xl">Where most of us started. You drive every step.</p>
</div>

<!--
Not Shop 6 today — the baseline we compare against.
-->

---

# Assemble the evidence by hand.

<div class="mt-8 grid grid-cols-[1.2fr_auto_1fr_auto_1fr] items-center gap-4">
  <div class="space-y-3">
    <div class="rounded-xl border border-slate-300 p-4 text-center">Jira ticket</div>
    <div class="rounded-xl border border-slate-300 p-4 text-center">repo A</div>
    <div class="rounded-xl border border-slate-300 p-4 text-center">repo B</div>
    <div class="rounded-xl border border-slate-300 p-4 text-center">wiki/docs</div>
    <div class="rounded-xl border border-slate-300 p-4 text-center">Slack thread</div>
  </div>
  <div class="space-y-5 text-3xl text-slate-500"><div>→</div><div>→</div><div>→</div><div>→</div><div>→</div></div>
  <div class="grid h-44 w-44 place-content-center rounded-full bg-[#D9772B] text-center text-4xl font-bold text-white">You</div>
  <div class="text-4xl text-slate-500">→</div>
  <div class="rounded-xl border-2 border-[#D9772B] p-5 text-center text-2xl"><div class="mb-2 text-base text-[#D9772B]">you</div>Draft issue</div>
</div>

<!--
Tabs, copy, paste. You're the integration layer; the AI helps at each step but you carry everything between steps.
-->

---

# You own every handoff — one issue at a time.

<div class="mt-7 grid grid-cols-[repeat(5,minmax(0,1fr))_1.1fr] items-center gap-3 text-center">
  <div class="rounded-xl border border-slate-300 p-3"><span class="rounded-full bg-[#D9772B] px-3 py-1 text-sm text-white">you</span><div class="mt-3">Read draft</div></div>
  <div class="rounded-xl border border-slate-300 p-3"><span class="rounded-full bg-[#D9772B] px-3 py-1 text-sm text-white">you</span><div class="mt-3">Publish issue</div></div>
  <div class="rounded-xl border border-slate-300 p-3"><span class="rounded-full bg-[#D9772B] px-3 py-1 text-sm text-white">you</span><div class="mt-3">Implement</div></div>
  <div class="rounded-xl border border-slate-300 p-3"><span class="rounded-full bg-[#D9772B] px-3 py-1 text-sm text-white">you</span><div class="mt-3">Review</div></div>
  <div class="rounded-xl border border-slate-300 p-3"><span class="rounded-full bg-[#D9772B] px-3 py-1 text-sm text-white">you</span><div class="mt-3">Update docs</div></div>
  <div class="space-y-2 text-left text-sm text-slate-400"><div class="rounded-lg bg-slate-100 p-2">Issue · waiting</div><div class="rounded-lg bg-slate-100 p-2">Issue · waiting</div><div class="rounded-lg bg-slate-100 p-2">Issue · waiting</div></div>
</div>

<!--
It works, it's serial, your attention is the queue. Docs are the step that gets skipped when you're tired.
-->

---
layout: section
---

<div class="absolute inset-0 grid place-content-center bg-[#1E2530] px-20 text-center text-white">
  <h1 class="text-6xl font-bold">Now · Shop 6 agentic pipeline</h1>
  <p class="mt-5 text-2xl">Two live demos · two Shop 6 team members</p>
  <p class="mt-3 text-xl">1 · Create and hand off the task &nbsp; → &nbsp; 2 · Implement end to end</p>
</div>

<!--
Session 1: team member 1 refines the request, gathers context, drafts the issue, publishes it, and assigns Copilot. Session 2: team member 2 walks an assigned task through Spec Kit implementation, /review, human merge, docs sync, docs PR review, and the next-issue handoff. Use an approved live task/PR or clearly label any prepared fallback.
-->

---

<div class="mb-3 text-sm font-semibold text-[#2F6DB5]">LIVE DEMO 1 · TEAM MEMBER 1 · CREATE THE TASK</div>

# Refine the ticket with what the whole fleet knows.

<div class="mt-12 flex items-center justify-between gap-3 text-center">
  <div class="space-y-3"><div class="rounded-lg border p-3">Jira ticket</div><div class="rounded-lg border p-3">Wiki</div><div class="rounded-lg border p-3">Docs</div><div class="rounded-lg border p-3">Repo evidence</div></div>
  <div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-7 text-xl text-white"><div class="mb-2 text-sm">agent</div>Refinement skill</div>
  <div class="text-3xl">→</div>
  <div class="rounded-xl border-2 border-slate-300 p-5">Refined ticket</div>
  <div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#D9772B] p-7 text-xl text-white"><div class="mb-2 text-sm">you</div>Team review</div>
</div>

<!--
Team member 1 checks the ticket against wiki, docs and repo evidence, then asks the smallest set of questions. This is a proposal; the team reviews it before anything is written back.
-->

---

<div class="mb-3 text-sm font-semibold text-[#2F6DB5]">LIVE DEMO 1 · TEAM MEMBER 1 · CREATE THE TASK</div>

# Gather the context. Find the approach. Hand it over.

<div class="mt-16 flex items-center justify-between gap-3 text-center">
  <div class="rounded-xl border p-4">Refined ticket</div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">agent</div><div class="font-bold">create-implementation-issue</div><div class="mt-2 text-sm">context · approach · local draft</div></div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#D9772B] p-5 text-white"><div class="mb-2 text-sm">you</div>Publish issue<br/>+ assign</div><div class="text-3xl">→</div>
<div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">agent</div>Cloud agent · Spec Kit</div><div class="text-3xl">→</div><div class="rounded-xl border p-5">PR</div>
</div>

<!--
Team member 1 runs `create-implementation-issue`, reviews the evidence-backed local draft, publishes it as a GitHub issue, and assigns Copilot. After handoff, they move to the next issue while Copilot works. Shop 6 uses Spec Kit for the implementation that follows.
-->

---

<div class="mb-3 text-sm font-semibold text-[#2F6DB5]">LIVE DEMO 2 · TEAM MEMBER 2 · IMPLEMENT END TO END</div>

# /review — a verdict, not a vibe.

<div class="mt-16 flex items-center justify-between gap-5 text-center">
  <div class="rounded-xl border p-6">PR</div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-7 text-xl text-white"><div class="mb-2 text-sm">agent</div>/review</div><div class="text-3xl">→</div>
  <div class="rounded-2xl border-2 border-[#2F6DB5] p-6"><div class="mb-2 text-sm text-[#2F6DB5]">agent</div><div class="text-xl font-bold">Approve / Reject</div><div class="mt-2">Findings by severity · Suggestions</div></div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#D9772B] p-7 text-xl text-white"><div class="mb-2 text-sm">you</div>You merge</div>
</div>

<!--
Team member 2 picks up an assigned Shop 6 task and shows the Spec Kit implementation, then runs `/review`. The verdict includes findings ranked by severity and concrete suggestions. Approve means ready for a human, never auto-merge. A person reads the evidence and merges.
-->

---

<div class="mb-3 text-sm font-semibold text-[#2F6DB5]">LIVE DEMO 2 · TEAM MEMBER 2 · IMPLEMENT END TO END</div>

# After merge, the docs catch up.

<div class="mt-16 flex items-center justify-between gap-3 text-center">
  <div class="rounded-xl border p-5">Merged PR</div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">workflow</div>Docs-sync workflow<br/><span class="text-sm">runs on its own</span></div><div class="text-3xl">→</div>
  <div class="rounded-xl border p-4">Out-of-sync docs found</div><div class="text-3xl">→</div><div class="rounded-xl border p-5">Docs PR</div><div class="text-3xl">→</div>
  <div class="rounded-2xl bg-[#D9772B] p-5 text-white"><div class="mb-2 text-sm">you</div>You review</div>
</div>

<!--
After the human merge, nobody starts docs sync manually. It checks for docs that no longer match the code and opens a PR; team member 2 reviews that PR, then moves to the next issue.
-->

---

# Better context, fewer tokens.

<div class="mt-10 grid grid-cols-3 gap-6">
  <div class="rounded-2xl border border-slate-300 p-6"><div class="text-2xl font-bold">CodeGraph</div><p class="mt-4">Callers · callees · impact radius</p></div>
  <div class="rounded-2xl border border-slate-300 p-6"><div class="text-2xl font-bold">rtk</div><p class="mt-4">Less command noise · fewer tokens</p></div>
  <div class="rounded-2xl border border-slate-300 p-6"><div class="text-2xl font-bold">Wiki &amp; docs</div><p class="mt-4">Cross-repo facts for refinement</p></div>
</div>
<div class="mt-7 text-center text-sm">Also: [other tools we use]</div>
<div class="mt-2 text-center text-xs">Sample: CodeGraph 181–205 ms (3 warm runs) · RTK <code>git log --stat -n 10</code>: 616 tokens saved (50.2% estimate)</div>
<div class="mt-2 text-center text-sm"><a class="text-slate-800 underline" href="/downloads/resources.zip" download>Download skills + tool references</a></div>

<!--
Agents fail on bad context more than bad reasoning; these tools feed them the right context. CodeGraph answers "what calls this, what breaks if I change it" without reading half the repo. Three warm CodeGraph service runs of `JtlSearchAdapter searchProducts callers` took 181–205 ms. The local Shop 6 checkout has no CodeGraph index; the measured query used the existing shared graph. RTK reported 616 estimated tokens saved (50.2%) for `rtk git log --stat -n 10`; that is one command's estimate, not a general saving rate. rtk keeps command output short, so attention goes where it matters and it costs fewer tokens. [our measured saving, if any]
-->

---

<div class="mb-5 inline-flex rounded-full bg-slate-200 px-4 py-2 text-sm font-semibold tracking-wide">FUTURE PLAN · GITHUB AGENTIC WORKFLOWS</div>

# Start the workflow from the ticket.

<div class="mt-8 grid grid-cols-[1.2fr_auto_1fr_auto_1fr_auto_1fr_auto_1fr_auto_1fr] items-center gap-2 text-center">
  <div class="space-y-3">
    <div class="rounded-xl border-2 border-slate-300 p-4">Jira assigned to agent</div>
    <div class="text-xs font-semibold tracking-widest text-slate-500">OR</div>
    <div class="rounded-xl border-2 border-slate-300 p-4">GitHub issue created</div>
  </div>
  <div class="text-3xl text-slate-500">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">workflow</div>Refine ticket</div>
  <div class="text-3xl text-slate-500">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">agent</div>Spec Kit</div>
  <div class="text-3xl text-slate-500">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">agent</div>Implement</div>
  <div class="text-3xl text-slate-500">→</div>
  <div class="rounded-2xl bg-[#2F6DB5] p-5 text-white"><div class="mb-2 text-sm">workflow</div>Code review</div>
  <div class="text-3xl text-slate-500">→</div>
  <div class="rounded-2xl bg-[#D9772B] p-5 text-white"><div class="mb-2 text-sm">you</div>Merge</div>
</div>
<div class="mt-5 grid grid-cols-2 gap-4 text-center text-sm">
  <div class="rounded-xl border border-slate-300 p-3"><b>Spec-driven is our next step:</b> a better harness helps the agent deliver better results.</div>
  <div class="rounded-xl border border-slate-300 p-3"><b>Silly hypothetical:</b> “Make checkout faster.” <b>Agent:</b> removes checkout. Fastest checkout. 😅</div>
</div>
<div class="mt-3 text-center text-sm"><b>Hypothesis to test:</b> a full agentic workflow can outperform a standalone Superpowers skill as tasks grow more complex.</div>

<!--
Future plan: apply GitHub Agentic Workflows so a Jira ticket assigned to an agent or a newly created GitHub issue can trigger refinement, then Spec Kit-guided implementation and code review. A person still owns the merge. We believe spec-driven work is the next step: the better the harness, the better the results. Our hypothesis is that a full end-to-end workflow can outperform a standalone Superpowers skill as tasks grow more complex; measure this in the pilot. Clear instructions help even a capable agent; ambiguity can confuse a smart one too. The checkout line is an intentionally silly hypothetical, not a Shop 6 incident.
-->

---

# Same task. Different control surface.

<table class="mt-5 w-full border-collapse text-center text-xs">
  <thead><tr><th></th><th>Refine</th><th>Issue + context</th><th>Publish + assign</th><th>Implement</th><th>Review</th><th>Docs</th></tr></thead>
  <tbody>
    <tr><th>Before</th><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span></td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span></td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span></td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span> / AI chat</td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span></td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span> (if time)</td></tr>
    <tr><th>Shop 6 now</th><td><span class="rounded bg-[#2F6DB5] px-1 text-white">agent</span> → <span class="rounded bg-[#D9772B] px-1 text-white">team reviews</span></td><td><span class="rounded bg-[#2F6DB5] px-1 text-white">agent</span></td><td><span class="rounded bg-[#D9772B] px-1 text-white">you</span></td><td><span class="rounded bg-[#2F6DB5] px-1 text-white">cloud agent</span></td><td>/review → <span class="rounded bg-[#D9772B] px-1 text-white">you</span> merge</td><td><span class="rounded bg-[#2F6DB5] px-1 text-white">workflow</span> → <span class="rounded bg-[#D9772B] px-1 text-white">you</span> review PR</td></tr>
  </tbody>
</table>

<!--
Same steps. Before, you did almost all of them. Now agents do the legwork and people sit at the gates. Accountability didn't move — your name is still on the merge.
-->

---

<div class="mx-auto max-w-6xl">

# Shop 6 agent activity by repository

<table class="mt-5 w-full border-collapse text-center text-sm">
  <thead><tr><th class="p-2 text-left">Repository</th><th>Tasks</th><th>PR-linked</th><th>Sessions</th><th>Completed</th><th>Failed</th><th>Cancelled</th></tr></thead>
  <tbody>
    <tr><th class="p-2 text-left">Shop standards</th><td>21</td><td>21</td><td>47</td><td>20</td><td>0</td><td>1</td></tr>
    <tr><th class="p-2 text-left">Contracts</th><td>121</td><td>121</td><td>171</td><td>114</td><td>4</td><td>3</td></tr>
    <tr><th class="p-2 text-left">Admin</th><td>141</td><td>141</td><td>235</td><td>131</td><td>4</td><td>6</td></tr>
    <tr><th class="p-2 text-left">Storefront</th><td>156</td><td>156</td><td>251</td><td>144</td><td>2</td><td>10</td></tr>
    <tr><th class="p-2 text-left">ERP connector</th><td>157</td><td>151</td><td>181</td><td>152</td><td>0</td><td>5</td></tr>
    <tr><th class="p-2 text-left">Components</th><td>92</td><td>92</td><td>111</td><td>86</td><td>1</td><td>5</td></tr>
    <tr><th class="p-2 text-left">Search</th><td>108</td><td>108</td><td>161</td><td>101</td><td>5</td><td>2</td></tr>
    <tr><th class="p-2 text-left">Infrastructure</th><td>97</td><td>96</td><td>206</td><td>93</td><td>2</td><td>2</td></tr>
    <tr><th class="p-2 text-left">Local</th><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><th class="p-2 text-left">Frontend proxy</th><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr class="border-t-2 font-bold"><th class="p-2 text-left">Total</th><td>893</td><td>886</td><td>1,363</td><td>841</td><td>18</td><td>34</td></tr>
  </tbody>
</table>

<!--
These are the supplied Shop 6 repository totals: tasks, tasks linked to PRs, agent sessions, and task outcomes. Keep the table factual; it describes activity and outcomes, not a controlled comparison with the prompt-driven run.
-->

</div>

---

<div class="mx-auto max-w-5xl">

# Agent session elapsed time

<p class="mt-2 text-center text-sm">76 sessions with recorded start and end times</p>

<table class="mt-7 w-full border-collapse text-center text-lg">
  <thead><tr><th class="p-3 text-left">Repository</th><th>Sessions</th><th>Mean</th><th>Median</th><th>90th percentile</th></tr></thead>
  <tbody>
    <tr><th class="p-3 text-left">Shop standards</th><td>29</td><td>6.5 min</td><td>4.9 min</td><td>12.0 min</td></tr>
    <tr><th class="p-3 text-left">Contracts</th><td>13</td><td>7.6 min</td><td>8.3 min</td><td>10.9 min</td></tr>
    <tr><th class="p-3 text-left">Admin</th><td>20</td><td>25.8 min</td><td>20.0 min</td><td>56.7 min</td></tr>
    <tr><th class="p-3 text-left">Storefront</th><td>14</td><td>8.5 min</td><td>8.4 min</td><td>12.5 min</td></tr>
    <tr class="border-t-2 font-bold"><th class="p-3 text-left">Sample total</th><td>76</td><td>12.1 min</td><td>8.3 min</td><td>20.5 min</td></tr>
  </tbody>
</table>

<!--
These elapsed-time figures cover only sessions with both a start and end time in the supplied sample. They are session elapsed times, not hands-on time or a matched before/after task benchmark.
-->

</div>

---

# Pros & trade-offs: discuss what matters in your repo.

<div class="mt-6 grid grid-cols-2 gap-8">
  <div class="rounded-2xl border-2 border-slate-300 p-6">
    <div class="mb-4 text-2xl font-bold">Pros</div>
    <ul class="space-y-4 text-lg">
      <li>Shared context across repos goes into the issue draft.</li>
      <li>After handoff, you can start the next ticket.</li>
    </ul>
  </div>
  <div class="rounded-2xl border-2 border-slate-300 p-6">
    <div class="mb-4 text-2xl font-bold">Trade-offs</div>
    <ul class="space-y-3 text-lg">
      <li>Refinement and issue drafting still start by hand.</li>
      <li>Docs catch up after merge; main is briefly stale.</li>
      <li>Activity metrics are not a matched before/after speed benchmark.</li>
    </ul>
  </div>
</div>

<!--
Discuss: which benefit would matter most in your repo, and which trade-off would you address first? Activity and elapsed-session metrics are available; a matched before/after task benchmark is a separate measurement.
-->

---

<div class="absolute inset-0 flex flex-col bg-[#FBE7D6] p-12 text-[#1E2530]">
  <div class="mb-7 inline-flex w-fit rounded-full bg-slate-800 px-5 py-2 text-lg font-semibold text-white">TRY · 14 minutes · laptop optional</div>
  <h1 class="text-4xl font-bold">Run the same task two ways.</h1>
  <div class="mt-6 grid grid-cols-2 gap-6">
    <div class="rounded-2xl border-2 border-slate-400 bg-white p-6">
      <div class="text-xl font-bold">Prompt-only · manual loop</div>
      <div class="mt-3 text-lg">Gather the same cross-repo context yourself. Prompt the model step by step to build the issue draft.</div>
    </div>
    <div class="rounded-2xl border-2 border-slate-400 bg-white p-6">
      <div class="text-xl font-bold">Agentic · Shop 6 skill</div>
      <div class="mt-3 text-lg">Run <code>create-implementation-issue</code>; it gathers evidence and saves a local issue draft. Follow the full pipeline in the two live demos.</div>
    </div>
  </div>
  <div class="mt-5 flex items-center justify-between gap-4 text-base">
    <span>6 minutes each · 2 minutes to compare time, evidence, and rework</span>
    <a class="rounded-full bg-slate-200 px-4 py-2 font-semibold text-slate-900" href="/downloads/resources.zip" download>Download resources · extract at repo root</a>
  </div>
  <div class="mt-3 text-xs">Local draft; a person publishes the GitHub issue. Spec Kit is required for substantial work; cloud-bootstrap can create missing artifacts.</div>
  <div class="mt-2 text-xs">No laptop? Follow the demo.</div>
</div>

<!--
No pair work. Use the same small task and repo for both runs. Spend six minutes manually gathering context and prompting the model to build the issue draft, then six minutes using `create-implementation-issue`; use the last two minutes to compare elapsed time, evidence captured, and rework. This ends at a local issue draft: the skill does not publish the GitHub issue. Do not use Superpowers as the prompt-only control; it is itself an agentic skill. The two live demos show the full Shop 6 flow, including Spec Kit implementation. Our hypothesis is that the full workflow brings more value as task complexity grows; this short comparison does not prove it.
-->

---
layout: center
---

# Thank you

## What would you hand over first?

<div class="mt-10 text-lg">Start here: AGENTS.md in any shop repo · Shop 6 onboarding page</div>

<!--
Take questions. If quiet, ask the closing question.
-->
