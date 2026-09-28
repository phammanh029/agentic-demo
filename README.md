# From Prompting to Agentic Engineering

A runnable Slidev deck for a 60-minute Shop 6 engineering workshop.

The workshop compares prompt-driven and agentic workflows using one bounded, illustrative Next.js pagination scenario. It intentionally does not claim the scenario exists in the real Shop 6 repository and does not invent repository paths, APIs, test results, or productivity gains.

## Run

Requirements: Node.js `>=22.12.0` and pnpm.

```bash
pnpm install
pnpm dev
```

Open the audience view at `http://localhost:3030/` and the presenter view at `http://localhost:3030/presenter`. Slidev’s documented presenter mode keeps audience navigation synchronized while keeping notes in the presenter view. Use two browser windows; put the presenter window on the laptop/second display while sharing only the audience window.

The deck enables Slidev’s documented 60-minute presenter countdown with `duration: 60min` and `timer: countdown`. The local `global-top.vue` layer adds a presenter-only timer panel with Start, Pause/Resume, Next section, and Reset controls. It uses timestamp-based elapsed calculations, localStorage refresh recovery, explicit reset confirmation for active sessions, visible two-minute/30-second/expiry cues, and no audio or OS notifications.

## Export

```bash
pnpm build
pnpm export
pnpm export:notes
```

`pnpm build` builds the static web app. `pnpm export` creates a PDF using Slidev’s export command. `pnpm export:notes` exports presenter notes. The presenter timer is intentionally presenter-only and is not intended to appear in exported audience slides.

## Contents

- `slides.md` — 16-slide deck with per-slide duration, cumulative target, talking points, demo instructions, prompts, and transitions in presenter notes.
- `components/PresenterTimer.vue` — small local presenter-only timer panel.
- `global-top.vue` — documented Slidev global layer that hides the panel outside presenter context.
- `styles/index.css` — dark navy engineering visual system with cyan prompt-driven and violet agentic accents.
- `docs/demo-prep.md` — preparation checklist, exact agent brief, and static fallback walkthrough.

## Validation status

The source is written against the official Slidev APIs documented for presenter mode, notes, global layers, components, `@slidev/client` context, and the 60-minute countdown. Run `pnpm install`, `pnpm build`, and the visual/timer checks in your environment before presenting. The illustrative scenario and simulated outputs are not repository validation; use a verified checkout if you want a live code demo.
