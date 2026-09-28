# Shop 6 issue-to-delivery demo preparation

The workshop compares prompt-driven and agentic handling of the same Shop 6 workflow:

1. Gather evidence from multiple projects.
2. Draft a self-contained implementation issue.
3. Publish the approved draft to GitHub and assign it to Copilot.
4. Review the resulting code and verification evidence.
5. Update the affected documentation.
6. Move to the next issue only after the completion gates pass.

## Verified workflow boundary

The `create-implementation-issue` skill at `.agents/skills/create-implementation-issue/SKILL.md` is a local issue-drafting workflow. It gathers repository evidence, writes an issue under `.tmp/github-issues/`, and then stops. It explicitly does not publish a GitHub issue, implement the change, or mutate a remote system. GitHub publication and Copilot assignment are later workflow steps and must be demonstrated separately.

The skill requires documentation to be treated as an implementation deliverable when affected. It also requires fresh verification and an appropriate independent implementation review before the issue can be reported complete. Keep those checks visible in both demos.

## Before the workshop

- Select one small, approved Shop 6 issue that has relevant context in more than one project.
- Verify the branch, commit, and worktree state for each project used as evidence. Use read-only sibling project access.
- Prepare a disposable or explicitly approved GitHub issue target if demonstrating publication and Copilot assignment live. Otherwise use the static fallback and label it simulated.
- Do not publish against a production backlog, assign a real agent, or expose credentials/customer data without the workshop owner's explicit approval.
- Prepare the current implementation review skill/process and identify which specs, tests, docs, examples, or operational guidance are in scope for this sample issue.
- Run the Slidev audience view. The per-slide and 60-minute timers start automatically when the deck opens; revisit a slide to confirm its countdown resumes rather than resetting.

## Live demo 1 · Create and hand off the task · 7 minutes

Presenter: Shop 6 team member 1. Show the creation and handoff portion of the Shop 6 agentic pipeline.

1. Refine the task against wiki, docs, and sibling-repository evidence; pause for team review.
2. Run `create-implementation-issue`; review the evidence-backed local issue draft.
3. Publish the approved issue to GitHub and assign it to Copilot. After handoff, start the next issue while Copilot works.

The skill ends at a local draft. The person publishes the GitHub issue and assigns Copilot.

## Live demo 2 · Implement end to end · 8 minutes

Presenter: Shop 6 team member 2. Pick up an assigned task and show the implementation return and completion gates.

1. Show the task implemented using Shop 6's Spec Kit workflow.
2. Run `/review`; inspect the verdict, severity-ranked findings, and suggestions.
3. Read the evidence and merge as a person; the verdict never auto-merges.
4. Show post-merge docs sync opening a docs PR, review it, then hand off to the next issue.

Use an approved live task/PR or clearly label the prepared fallback. Do not fabricate test output or a review verdict.

## Hands-on comparison · 14 minutes

Use the same small task and repository for both runs: six minutes for a prompt-only manual context and drafting loop, six minutes for `create-implementation-issue`, and two minutes to compare elapsed time, evidence, and rework. Do not use Superpowers as the prompt-only control; it is itself an agentic skills workflow. This exercise ends at a local issue draft, while the two live demos show the full flow including Spec Kit implementation.

Prompts to use one at a time:

```text
Inspect the relevant Shop 6 project and sibling project context for this request.
Draft one evidence-backed implementation issue locally. Cite repository paths,
branches/commits, relevant decisions, validation commands, and unresolved questions.
Keep scope bounded and make affected documentation explicit. Do not invent evidence,
publish the issue, assign an agent, or implement the change.
```

```text
Review this implementation against every issue acceptance criterion. Inspect the
final diff and fresh verification evidence. Identify any required documentation,
specification, example, or operational guidance that is missing or stale. Report
unverified criteria and findings; do not claim completion without the required
independent review verdict.
```

```text
Work on one bounded Shop 6 issue using the create-implementation-issue workflow.
First inspect the repository instructions and relevant owning and sibling projects.
Produce a self-contained, evidence-backed local issue draft with exact paths,
repository snapshots, acceptance criteria, validation, and affected documentation.
Save and report the local issue draft, then stop this skill. After human approval,
use the separate approved GitHub publication and Copilot-assignment workflow. When
implementation is returned, inspect the diff and
fresh verification, obtain the required independent code review, ensure affected
documentation is current, and report residual gaps. Start the next issue only after
the current issue meets its completion gates. Never invent paths, results, or
review verdicts; do not merge or deploy.
```

Show these checkpoints in the live demos:

- **Issue approval:** cross-project evidence supports the scope and acceptance criteria.
- **Remote handoff:** a human approves GitHub publication and Copilot assignment.
- **Implementation review:** final diff and fresh verification satisfy all criteria; required independent review passes.
- **Documentation:** in-scope docs and artifacts reflect delivered behavior.
- **Next issue:** carry forward only verified context and explicit follow-ups.

## Static fallback

Use a prepared issue with sections for objective, evidence from each project, confirmed decisions, scope, acceptance criteria, required tests, required documentation, review gate, and incomplete follow-ups. Walk the issue through the handoffs with a clearly marked simulated GitHub issue and Copilot assignment. For the implementation return, show a sample review checklist and the documentation paths identified for the selected issue; do not fabricate test output or an approval verdict.

## Comparison scorecard

Record results live; leave unavailable values blank rather than estimating.

| Measure | Prompt-driven | Agentic |
|---|---|---|
| Time to approved issue |  |  |
| Context coverage across projects |  |  |
| Manual handoffs / interventions |  |  |
| Review findings and rework |  |  |
| Documentation completeness |  |  |
| Time to start next issue |  |  |

One workshop run is illustrative, not a productivity benchmark. Compare total delivery effort, review quality, evidence coverage, and handoffs.
