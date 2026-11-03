# Shop 6 Agentic

A Slidev sharing deck about how Shop 6 uses agents for daily engineering tasks and how engineers focus on business outcomes, design, boundaries, and quality when agents handle implementation.

The current Shop 6 workflow is ticket refinement → issue → triage → ready for implementation → implement → review ↔ remediate comments → approve → merge → sync docs. The deck explains how agents support that flow. It highlights GitHub Agentic Workflows for implementation planning, task implementation, and documentation updates, then covers engineering responsibilities, boundaries, and learning before the demo.

## Run

Requirements: Node.js `>=22.12.0` and pnpm.

```bash
pnpm install
pnpm dev
```

Open the audience view at `http://localhost:3030/` and the presenter view at `http://localhost:3030/presenter`. Slidev’s documented presenter mode keeps audience navigation synchronized while keeping notes in the presenter view. Use two browser windows; put the presenter window on the laptop/second display while sharing only the audience window.

To share the deck over the office network, run:

```bash
pnpm dev --remote
```

Open the **Network** URL printed by Slidev. Share the audience URL, not `/presenter`. Add a password to the `--remote` option if presenter mode should be restricted.

## Export

```bash
pnpm build
pnpm export
pnpm export:notes
```

`pnpm build` builds the static web app. `pnpm export` creates a PDF. `pnpm export:notes` exports presenter notes.

## Contents

- `slides.md` — 7-slide sharing deck with speaker notes: current workflow, GitHub Agentic Workflows, agent and engineer responsibilities, engineering team actions, lessons, and a demo guide.
- `global-top.vue` — empty global layer; the sharing deck has no workshop countdown or activity timeline.
- `docs/demo-prep.md` — retained reference for the original demonstration setup.
- `public/downloads/` — retained reference archives; the presentation no longer links to downloads.

## Validation

Run `pnpm build` to validate the static deck. Preview the slides before presenting to check layout. Keep proposed workflow improvements distinct from current practice and use verified evidence for any delivery claims.
