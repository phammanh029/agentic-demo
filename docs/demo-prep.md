# Demo preparation and fallback walkthrough

This workshop uses a proposed training bug only. It does not claim the bug exists in the real Shop 6 repository. Any code, terminal output, file path, or agent transcript shown without a verified checkout must be labelled **illustrative** or **simulated**.

## Before the workshop

- Confirm Node.js `>=22.12.0` and run `pnpm install`.
- Run `pnpm dev`, open the audience window at `/`, and open the presenter window at `/presenter`.
- Put the presenter window on the laptop/second display and the audience window on the shared display. Keep the presenter window visible on a second display while spending time in the IDE; a hidden browser tab is not a guaranteed reminder.
- Prepare an approved, disposable checkout or use the static fallback. Do not paste credentials, customer data, or private API keys into the demo.
- Keep a terminal ready for the focused regression command and a browser ready for URL back/forward.
- Start the presenter-only timer on slide 1. Use Pause/Resume around tool/network interruptions. Use Next section manually; expiry never advances slides.

## Prompt-driven fallback

1. Show the scenario and the four acceptance criteria.
2. Read Prompt 01 and Prompt 02 from slide 6.
3. Show a simulated diagnosis: category change updates category but retains page; reset must preserve `q` and `sort`.
4. Show the simulated baseline failure: `expected page=1, received page=5`.
5. Read the correction prompt from slide 7.
6. Show a simulated focused test that fails before the fix and passes after it.
7. Use the review trap on slide 13 to prove that “page reset” is not enough.

## Agentic fallback

Use this complete prompt in the approved agent session:

```text
You are working on a bounded, illustrative Shop 6 training task. First inspect repository instructions and the relevant code. Explain the likely cause and propose a short plan before editing. Wait for human approval of the plan. After approval, implement the smallest change that resets pagination to page 1 when category changes while preserving search text, sorting, and URL-driven back/forward state. Add meaningful regression tests. Demonstrate failure against the original implementation and success afterward. Inspect the final diff and report exact commands, outputs, uncertainty, and any acceptance criterion not proven. Do not refactor unrelated code, add dependencies, merge, or deploy. Do not invent repository paths or results.
```

Fallback transcript: “The agent inspected the relevant state owner, proposed a two-step plan, paused. After approval it added one focused regression test and the smallest state transition. It ran the baseline test against the original behavior, then reran after the change. The presenter now checks the exact output and final diff; written claims alone are not evidence.” Label this transcript simulated.

## Review prompts

- Does category change set page to `1`?
- Does search text remain unchanged?
- Does sorting remain unchanged?
- Does back/forward restore the URL-driven state?
- Does the regression fail against the original implementation and pass afterward?
- Are commands and outputs visible, reproducible, and tied to the final diff?
