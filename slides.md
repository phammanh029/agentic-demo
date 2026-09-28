---
theme: default
title: From Prompting to Agentic Engineering
info: A 60-minute Shop 6 engineering workshop
author: Shop 6 engineering
duration: 60min
timer: countdown
presenter: true
colorSchema: dark
fonts:
  sans: Inter
  mono: JetBrains Mono
layout: cover
---

<div class="eyebrow">SHOP 6 ENGINEERING WORKSHOP · 60 MINUTES</div>

# From Prompting to
# Agentic Engineering

<div class="subtitle">A Shop 6 task, two workflows, evidence-based comparison</div>

<div class="cover-rule"></div>
<div class="cover-meta"><span class="pill cyan">Prompt-driven</span><span>→</span><span class="pill violet">Agentic</span><span class="muted">same engineering accountability</span></div>

<!--
Duration: 2 minutes · cumulative target 02:00
Talking points: Welcome the developers, QA, and DevOps engineers. This is a practical comparison, not a product pitch. “Legacy” means prompt-driven AI usage, not development without AI.
Demonstrate / ask: Ask for a show of hands: who has pasted a failing test or log into an AI chat this week? Set the expectation that both workflows use prompts.
Transition: “We will use one bounded storefront task and inspect the evidence produced by each path.”
-->

---
layout: section
---

<div class="section-kicker">00 → 05 · INTRODUCTION AND TASK</div>

# The question is not
# “AI or no AI?”

<div class="section-line"></div>
<p class="section-lede">Who owns context, tool execution, and the feedback loop?</p>

<!--
Duration: 3 minutes · cumulative target 05:00
Talking points: The same model and IDE can support either workflow. The useful distinction is the operating model: who gathers context, runs tools, reacts to failures, and decides when the result is acceptable.
Demonstrate / ask: Read the agenda aloud and name the live-demo boundaries. Ask participants to listen for human checkpoints, not for speed claims.
Transition: “Here is the shared scenario. Treat it as a training bug, not a claim about the real repository.”
-->

---
layout: default
---

<div class="eyebrow">SHARED TRAINING SCENARIO · ILLUSTRATIVE</div>

# Page 5. New category. Empty result.

<div class="scenario-grid">
  <div class="browser-card">
    <div class="browser-bar"><span></span><span></span><span></span><code>/shop?category=boots&amp;page=5&amp;sort=price-asc</code></div>
    <div class="browser-body"><div class="product-ghost"></div><div class="empty-state">No products found</div><div class="page-chip">page 5 / 2</div></div>
  </div>
<div class="acceptance-card">
    <div class="card-label cyan-text">ACCEPTANCE CRITERIA</div>
    <ol>
      <li>Category change → <code>page=1</code>.</li>
      <li>Search + sort stay unchanged.</li>
      <li>Back/forward restores URL state.</li>
      <li>Regression fails before, passes after.</li>
    </ol>
    <div class="illustrative">Illustrative code and outcomes only — verify against the actual checkout.</div>
  </div>
</div>

<!--
Duration: 2 minutes · cumulative target 07:00
Talking points: State the exact proposed training bug. It is deliberately small enough for a bounded delegation and rich enough to exercise URL state, tests, and review.
Demonstrate / ask: Point to the “page 5 / 2” mismatch. Ask: which acceptance criterion is easiest to accidentally break while fixing the first one?
Transition: “Before the demos, make the operating-model difference explicit.”
-->

---

<div class="eyebrow">A WORKING DISTINCTION</div>

# Both start with a prompt.
# The loop is different.

<div class="two-up">
  <div class="workflow-card prompt-card">
    <div class="workflow-name"><span class="dot cyan-dot"></span>Prompt-driven</div>
    <div class="flow-row"><b>Human</b><span>→</span><b>AI</b><span>→</span><b>Human</b></div>
    <p>Human gathers context, chooses each next action, applies changes, and feeds back results.</p>
  </div>
  <div class="workflow-card agent-card">
    <div class="workflow-name"><span class="dot violet-dot"></span>Agentic</div>
    <div class="flow-row"><b>Human</b><span>→</span><b>Agent</b><span>↺</span><b>Human</b></div>
    <p>Human delegates a bounded outcome; the agent gathers, edits, runs checks, and iterates within guardrails.</p>
  </div>
</div>
<div class="callout">Same tool can do either. Permission scope and review discipline matter more than the label.</div>

<!--
Duration: 3 minutes · cumulative target 10:00
Talking points: Avoid rigid product categories. A chat window can be agentic if it has tool access and an iteration loop; an agent can be used prompt-by-prompt. The difference is context and execution ownership.
Demonstrate / ask: Have the audience classify a quick example: “Paste one stack trace, ask for three hypotheses, then stop.” Prompt-driven. “Inspect repo, run the focused test, edit, rerun, report.” Agentic.
Transition: “Now we will run the first path with deliberate human orchestration.”
-->

---
layout: section
---

<div class="section-kicker cyan-text">05 → 20 · LIVE DEMO A</div>

# Prompt-driven workflow

<div class="demo-banner cyan-bg"><span class="live-dot"></span> LIVE DEMO · switch between this deck, IDE, browser, terminal</div>
<div class="demo-steps"><span>context</span><i>→</i><span>diagnose</span><i>→</i><span>apply</span><i>→</i><span>test</span><i>→</i><span>review</span></div>

<!--
Duration: 3 minutes · cumulative target 13:00
Preparation: Open the illustrative task in the IDE, a terminal, the browser, and the AI chat. If the tools or network are unavailable, use the static fallback in docs/demo-prep.md.
Talking points: The developer remains the conductor. This is a valid workflow: deliberate, inspectable, and useful for learning an unfamiliar code path.
Demonstrate: Switch to the IDE on a second display or side-by-side window; keep this presenter window visible on the laptop display. Do not imply that a hidden browser tab guarantees reminders.
Transition: “The first cost is context transfer.”
-->

---

<div class="eyebrow cyan-text">DEMO A · 1 / 3 · FIND + DIAGNOSE</div>

# Give the model a useful slice.

<div class="prompt-box"><div class="prompt-label">ONE STEP AT A TIME</div><pre>Find the state owner for category, page, search, and sort.
Explain the likely cause and smallest fix. Do not edit files.
Do not invent repository facts.</pre></div>
<div class="flow-strip"><span>locate</span><i>→</i><span>select context</span><i>→</i><span>diagnose</span><i>→</i><span>challenge</span></div>
<div class="side-note">The human decides what context moves forward.</div>

<!--
Duration: 5 minutes · cumulative target 18:00
Preparation: Use an illustrative snippet or the real checkout only if the presenter has verified it. Label any simulated output.
Exact prompts: Copy the two prompts shown on the slide. Add the selected component and URL-state hook as context; never paste secrets.
Expected observations: The response should identify state ownership and name risks to URL/back-forward behavior. A confident answer is still a hypothesis.
Demonstrate: In the IDE, show the file selection; in chat, ask for diagnosis only; switch to terminal briefly to show baseline test intent.
Fallback: Read the prompt and show the prepared “likely cause” card in docs/demo-prep.md; say “simulated output.”
Transition: “The human reviews the suggestion before applying anything.”
-->

---

<div class="eyebrow cyan-text">DEMO A · 2 / 3 · APPLY + FEEDBACK</div>

# Keep the loop deliberate.

<div class="timeline">
  <div><b>03</b><span>Review</span><small>Does it preserve search and sort?</small></div>
  <div><b>04</b><span>Apply</span><small>Human accepts the smallest change.</small></div>
  <div><b>05</b><span>Test</span><small>Capture exact failure output.</small></div>
  <div><b>06</b><span>Feed back</span><small>Ask for a correction, not a guess.</small></div>
</div>
<div class="terminal-card"><span class="terminal-prompt">$</span> pnpm test --filter pagination-regression<br><span class="simulated">SIMULATED OUTPUT: expected page=1, received page=5</span></div>

<!--
Duration: 5 minutes · cumulative target 23:00
Preparation: Have a prepared failing test command or a transcript. This slide intentionally shows a simulated output; do not claim it came from Shop 6.
Exact prompt after failure: “The focused test reports expected page=1, received page=5. Re-check the state transition and propose the smallest correction. Preserve query and sort params. Do not edit yet.”
Expected observations: The loop is interrupted by the human at every meaningful step. That is the point, not a defect.
Fallback: Use the terminal card and walk the timeline without running a live app.
Transition: “The final step is still a human-owned review and PR handoff.”
-->

---

<div class="eyebrow cyan-text">DEMO A · 3 / 3 · TEST + REVIEW</div>

# A reviewed patch is the outcome.

<div class="checklist-grid">
  <div class="checklist"><span>07</span><p>Ask for a regression test</p><small>“Write a focused test that fails on the original behavior and proves all four criteria.”</small></div>
  <div class="checklist"><span>08</span><p>Review the final diff</p><small>Check URL preservation, test intent, unrelated changes, and uncertainty.</small></div>
  <div class="checklist"><span>09</span><p>Prepare the PR</p><small>Summarize evidence, known limits, and what remains for CI.</small></div>
</div>
<div class="bottom-line">Benefits: low setup overhead · deliberate control · learning · exploratory discussion</div>
<div class="warning-line">Costs: repeated context transfer · manual coordination · interruptions · suggestions can remain unverified</div>

<!--
Duration: 7 minutes · cumulative target 30:00
Exact prompts: “Write the regression test first. Show the test and explain why it would fail before the fix.” Then: “Review this final diff against each acceptance criterion. Call out anything unverified.”
Expected observations: A good prompt-driven session can be careful and successful. The coordination cost is visible in the number of handoffs.
Demonstrate: Switch IDE → terminal → browser → this slide. Pause to ask QA what evidence they would require before approving.
Fallback: Use the static diff-review checklist in docs/demo-prep.md.
Transition: “Now keep the same task, but delegate the bounded loop.”
-->

---
layout: section
---

<div class="section-kicker violet-text">20 → 35 · LIVE DEMO B</div>

# Agentic workflow

<div class="demo-banner violet-bg"><span class="live-dot"></span> LIVE DEMO · delegate the loop, retain the checkpoints</div>
<div class="agent-brief-strip">bounded outcome <span>·</span> repository-aware <span>·</span> test-backed <span>·</span> no merge / no deploy</div>

<!--
Duration: 3 minutes · cumulative target 33:00
Preparation: Open the same illustrative task, the repository instructions, and a clean working state. Ensure the agent has only the permissions needed for the demo. No merging, deployment, or secrets.
Talking points: Delegation changes who manages context and iteration; it does not transfer accountability.
Demonstrate: Keep the presenter window on the laptop/second display, and use the presenter-only timer. The audience sees only the slide window.
Fallback: Use the static walkthrough in docs/demo-prep.md.
Transition: “The brief must be complete enough to constrain the work.”
-->

---

<div class="eyebrow violet-text">DEMO B · THE TASK BRIEF</div>

# Delegate an outcome, not a vibe.

<div class="brief-card">
  <div class="brief-title">SHOP 6 TRAINING BUG · bounded task</div>
  <p>Fix the illustrative pagination bug without losing URL state.</p>
  <div class="brief-columns"><div><b>Prove</b><ul><li>page resets</li><li>query + sort survive</li><li>history works</li><li>test fails then passes</li></ul></div><div><b>Protect</b><ul><li>bounded scope</li><li>existing dependencies</li><li>no merge / deploy</li><li>honest uncertainty</li></ul></div></div>
</div>
<div class="checkpoint-row"><span>1 · approve plan</span><span>2 · inspect diff</span><span>3 · verify evidence</span><span>4 · accept or rework</span></div>

<!--
Duration: 7 minutes · cumulative target 40:00
Preparation: The complete copyable prompt is in presenter notes below and in docs/demo-prep.md. Paste it only into the approved agent session.
Copyable prompt:
“You are working on a bounded, illustrative Shop 6 training task. First inspect repository instructions and the relevant code. Explain the likely cause and propose a short plan before editing. Wait for human approval of the plan. After approval, implement the smallest change that resets pagination to page 1 when category changes while preserving search text, sorting, and URL-driven back/forward state. Add meaningful regression tests. Demonstrate failure against the original implementation and success afterward. Inspect the final diff and report exact commands, outputs, uncertainty, and any acceptance criterion not proven. Do not refactor unrelated code, add dependencies, merge, or deploy. Do not invent repository paths or results.”
Expected observations: The agent gathers context, pauses for approval, edits, runs checks, iterates, and reports evidence. Written claims are not executed evidence.
Fallback: Read the brief and use the prepared transcript; mark it simulated.
Transition: “Let’s make the human checkpoints visible.”
-->

---

<div class="eyebrow violet-text">DEMO B · HUMAN CHECKPOINTS</div>

# The agent owns the loop.
# The human owns the boundary.

<div class="checkpoint-list">
  <div><span>01</span><b>Approve</b><p>Small, testable, repository-consistent?</p></div>
  <div><span>02</span><b>Challenge</b><p>Which assumptions were actually inspected?</p></div>
  <div><span>03</span><b>Review</b><p>Does the test cover the acceptance criteria?</p></div>
  <div><span>04</span><b>Decide</b><p>Separate evidence from written claims.</p></div>
</div>
<div class="evidence-band"><b>Evidence ladder</b><span>agent says</span><i>→</i><span>command shown</span><i>→</i><span>output observed</span><i>→</i><span>reviewer accepts</span></div>

<!--
Duration: 5 minutes · cumulative target 45:00
Talking points: An agent can reduce coordination, but the review responsibility remains. The strongest signal is reproducible output tied to exact commands and a final diff.
Demonstrate / ask: Ask QA: what would you reject even if the agent says “all tests pass”? Ask DevOps: what permission boundary would you set?
Fallback: Use the evidence ladder as the static walkthrough.
Transition: “Now compare the two workflows against the same dimensions.”
-->

---

<div class="eyebrow">35 → 50 · COMPARE RESULTS AND TRADE-OFFS</div>

# Same task. Different control surface.

<table class="compare-table"><thead><tr><th></th><th class="cyan-text">Prompt-driven</th><th class="violet-text">Agentic</th></tr></thead><tbody>
<tr><td>Workflow ownership</td><td>Human orchestrates each step</td><td>Agent manages bounded loop</td></tr>
<tr><td>Context gathering</td><td>Manually selected and transferred</td><td>Agent inspects within scope</td></tr>
<tr><td>Interventions</td><td>Frequent, explicit handoffs</td><td>Fewer, deliberate checkpoints</td></tr>
<tr><td>Feedback loop</td><td>Human runs tools and feeds results</td><td>Agent runs checks and iterates</td></tr>
<tr><td>Review effort</td><td>Distributed across steps</td><td>Concentrated at plan + diff + evidence</td></tr>
<tr><td>Blast radius</td><td>Usually narrower by default</td><td>Depends on granted permissions</td></tr>
</tbody></table>
<div class="footnote">Neither workflow guarantees correctness. Correctness comes from scope, evidence, and review.</div>

<!--
Duration: 5 minutes · cumulative target 50:00
Talking points: Walk row by row. Cost includes elapsed time, usage cost, and human attention; do not assume fewer prompts means lower total delivery effort.
Demonstrate / ask: Ask the room which row changes most for their team. Capture one answer verbally, not as an invented benchmark.
Transition: “A small review trap shows why acceptance criteria must remain visible.”
-->

---

<div class="eyebrow">REVIEW TRAP · ACCEPTANCE CRITERIA IN ACTION</div>

# “It resets pagination.”
# …and silently drops sorting.

<div class="trap-grid"><div class="diff-card bad"><div class="diff-title">PATCH CLAIM</div><pre><span class="minus">- setState({ category, page: 5, sort })</span>
<span class="plus">+ setState({ category, page: 1 })</span></pre><div class="trap-label">page reset: ✓ · sort preserved: ✕</div></div><div class="review-card"><div class="diff-title">REVIEW QUESTION</div><p>Does the URL after category change still contain:</p><div class="url-check"><code>q=boots</code><code>sort=price-asc</code><code>page=1</code></div><p class="muted">Run the same checklist in both workflows. A plausible patch is not acceptance evidence.</p></div></div>
<div class="cue">Pause. Ask: which test would catch this?</div>

<!--
Duration: 5 minutes · cumulative target 55:00
Talking points: This is a realistic failure mode: the primary bug is fixed while another acceptance criterion is regressed. Agents and humans can both miss it.
Demonstrate / ask: Have participants name a test assertion for `sort` and one for back/forward. Then ask whether the final diff or the test output proves each.
Fallback: Use the code card as a static review exercise.
Transition: “We need a scorecard before we claim an advantage.”
-->

---

<div class="eyebrow">SCORECARD · MEASURE LIVE</div>

# Do not invent the benchmark.

<div class="scorecard"><div class="score-row head"><span>Measure</span><span>Prompt-driven</span><span>Agentic</span></div><div class="score-row"><span>Time to a reviewed patch</span><b>To measure live</b><b>To measure live</b></div><div class="score-row"><span>Manual interventions</span><b>To measure live</b><b>To measure live</b></div><div class="score-row"><span>Test results</span><b>To measure live</b><b>To measure live</b></div><div class="score-row"><span>Missed acceptance criteria</span><b>To measure live</b><b>To measure live</b></div><div class="score-row"><span>Review + rework time</span><b>To measure live</b><b>To measure live</b></div><div class="score-row"><span>Usage cost, if available</span><b>To measure live</b><b>To measure live</b></div></div>
<p class="center-note">One workshop demo is illustrative, not a benchmark. Evaluate quality and total delivery effort.</p>

<!--
Duration: 3 minutes · cumulative target 58:00
Talking points: Keep the scorecard blank. We are designing a measurement habit, not announcing productivity gains. If cost data is unavailable, record that explicitly.
Demonstrate / ask: Ask participants to choose one measure they can reliably capture in a two-week pilot.
Transition: “Close with a small, reversible pilot.”
-->

---

<div class="eyebrow">50 → 60 · DISCUSSION AND NEXT STEPS</div>

# Two weeks. One small issue each.

<div class="pilot-grid"><div class="pilot-step"><span>01</span><b>Choose</b><p>Take one small Shop 6 issue with clear acceptance criteria.</p></div><div class="pilot-step"><span>02</span><b>Run</b><p>Use one workflow; record checkpoints, tests, rework, and elapsed time.</p></div><div class="pilot-step"><span>03</span><b>Share</b><p>Bring one outcome and one lesson to the team.</p></div></div>
<div class="responsibility"><b>Engineer</b> frames scope · <b>QA</b> challenges evidence · <b>DevOps</b> constrains blast radius · <b>Everyone</b> owns the decision</div>
<div class="close-line">Optimize for trustworthy delivery — not generated lines of code.</div>

<!--
Duration: 2 minutes · cumulative target 60:00
Talking points: Restate the actionable pilot. Ask each participant to name the issue class they might choose and one measure they will record. Emphasize that agents do not remove engineering accountability.
Demonstrate / ask: Show the timer’s “wrap up” cue at two minutes and stronger cue at 30 seconds if running live. At expiry, the timer shows overtime and does not auto-advance.
Transition: Thank the group and leave the deck in presenter mode for questions.
-->
