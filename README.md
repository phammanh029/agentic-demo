# From Prompting to Agentic Engineering

A runnable Slidev deck for a 60-minute Shop 6 engineering workshop.

The workshop compares prompt-driven and agentic workflows using Shop 6's issue-to-delivery cycle: gather context across projects, draft and publish a GitHub issue, assign Copilot, review implementation evidence, keep documentation current, and continue to the next issue. Any step not demonstrated against an approved live checkout is labelled simulated; the deck does not invent repository paths, APIs, test results, or productivity gains.

## Run

Requirements: Node.js `>=22.12.0` and pnpm.

```bash
pnpm install
pnpm dev
```

Open the audience view at `http://localhost:3030/` and the presenter view at `http://localhost:3030/presenter`. Slidev’s documented presenter mode keeps audience navigation synchronized while keeping notes in the presenter view. Use two browser windows; put the presenter window on the laptop/second display while sharing only the audience window.

The `global-top.vue` layer shows an automatic per-slide countdown, a 60-minute total countdown, and a bottom section timeline. A slide timer starts on first open, resumes its accumulated time when revisited, and warns at 70%, 85%, and 100% of its budget. Timer state persists in localStorage; Reset asks for confirmation once timing has started.

## Export

```bash
pnpm build
pnpm export
pnpm export:notes
```

`pnpm build` builds the static web app. `pnpm export` creates a PDF using Slidev’s export command. `pnpm export:notes` exports presenter notes. The presenter timer is intentionally presenter-only and is not intended to appear in exported audience slides.

## Contents

- `slides.md` — 22-slide workshop deck with speaker notes, Shop 6 pipeline, comparison activity, and repository metrics.
- `global-top.vue` — per-slide timer, total timer, and section timeline.
- `public/downloads/shop6-agentic-skills.zip` — downloadable Shop 6 skills for the hands-on comparison.
- `docs/demo-prep.md` — preparation checklist, bounded agent brief, and static fallback walkthrough for issue creation, Copilot handoff, code review, documentation, and issue sequencing.

## Validation status

The source is written against the official Slidev APIs documented for presenter mode, notes, global layers, components, `@slidev/client` context, and the 60-minute countdown. Run `pnpm build` and the visual/timer checks in your environment before presenting. Use an approved Shop 6 issue and verified project snapshots for live workflow steps; label any simulated issue, output, or handoff clearly.
