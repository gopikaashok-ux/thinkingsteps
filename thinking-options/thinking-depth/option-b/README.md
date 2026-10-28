# Option B: thinking steps at three depths, built for smoothness

Same query, agent and seven-step order as Option A (`../README.md`). Option B changes the interaction, guided by four smoothness rules:

1. **No layout jumps.** Live progress stays a fixed height, and a ghost outline holds the answer's space before it streams.
2. **One thing open at a time.** Finished steps fold away on their own; the user never has to collapse anything.
3. **Detail sits next to what it explains.** Reasoning is attached to the claim it supports, and trace data to the figure it produced, instead of a separate place to go and read.
4. **Change depth without re-asking.** The built dashboards put a **Simple · In-depth · Extensive** switch in the chat header (the Case 1 and 3 mockups show an earlier per-answer version; Case 2 has none).

| | Case 1 · Simple | Case 2 · In-depth reasoning | Case 3 · Show everything |
|---|---|---|---|
| **Option A** | Stacked inline blocks | Inline blocks + modal | Side panel |
| **Option B** | **One live line → stamp + popover** | **Reasoning rail → "why" popover on each claim** | **Bottom dock (devtools style)** |
| While running | One 40px line updates in place: plan → action → teaser; dots show step x of 3 | Vertical rail, only the current step open; finished steps fold to one line | One summary row in chat; everything else in the dock's timeline |
| Engaging the user | The line speaks to the user ("74/100, one gap…") | Checkpoint is the active rail node: countdown, recommended ✦, keys 1/2/3 | Checkpoint row stays in chat ("change"); shows as the "You" lane |
| When done | Line shrinks into a `✓ 3 steps · 4s` stamp on the answer | Rail folds into a one-line strip; the user's choice stays highlighted | Answer figures are underlined and linked to the call that produced them |
| Opening detail | Stamp → popover (doesn't push the answer down) | Claim marker → popover with because → so, sources, "Try vendor's 18%" | Hover a figure → tooltip; click → dock selects the call and highlights the field |
| Phone | Same line; popover → small sheet | Same rail; popover → half sheet | Dock → full-screen sheet, timeline as a vertical list |

## When to pick B over A

- **B** suits frequent users and long runs: less scrolling, nothing to collapse by hand, and depth can change after the fact.
- **A** is easier to build and more explicit: every step is always visible as its own block, which helps first-time users and reviewers.

## Images

| File | Shows |
|---|---|
| `b1-simple.png` | Live line at 3 moments, the stamp on the answer, the stamp popover |
| `b2-in-depth.png` | Rail while running (paused on the checkpoint) and the done state with a claim's "why" popover |
| `b3-full-trace.png` | Chat above, bottom dock with per-agent timeline, call table and response viewer |

HTML sources are in `src/` (they import `../../src/base.css`).

## Built: Case 1 in the Majlis dashboard

`/Option B - Simple.html` (repo root) is the Majlis Agents Evaluation · Orchestration dashboard with Case 1 working for real. Pick the **Evaluation** agent, attach a proposal (or use a Try chip) and send:

- The thinking block and the auto-opening orchestration modal are replaced by **one live line**: plan → current action → teaser ("70/100, proceed with conditions…"), with phase dots, a progress ring and a ghost of the answer underneath.
- When the answer lands, the line **shrinks into a `✓ 3 steps · 11s` stamp**; tapping it opens a popover with the three phases.
- The chat header has **Thinking: Simple · In-depth · Extensive** tabs, with Simple selected; the other two say which Option B case they belong to.
- Built only from the file's own tokens (`--accent`, `--c4`, `--tile`, `--pop`…) and motion (`swap`, `shimmer`, `chipIn`, `barRun`); light, dark, RTL-safe and phone layouts. Other agents are unchanged.

Screenshots: `majlis-simple/`.

## Built: Case 2 in the Majlis dashboard

`/Option B-In depth.html` (repo root) is the same dashboard with Case 2 working. Pick the **Evaluation** agent, attach a proposal (or use a Try chip) and send:

- **Reasoning rail** in place of the thinking block and the auto-opening modal: one node per reasoning step (Planned, Read, Scored, Need your call, Weighed, Wrote). Only started steps appear; the current one is open with its sub-steps arriving live, finished ones fold to one line, and past 3 finished steps the earlier ones fold into an "N earlier steps" row.
- **Need your call**: the run really pauses. One proposal asks which volume growth to use (plan 7% / proposal 12% / both); two proposals ask whether to add the missing migration cost. Recommended option first, keys 1–3, a 15s countdown picks the recommendation if you don't. The choice changes the steps that follow and the "why" text.
- **Done**: the rail folds into a one-line strip. Past 5 steps it keeps the first, your choice and the last, and folds the rest into "+N steps"; any chip or "Show steps" opens the full rail.
- **"Why" markers** (1–4) on the executive takeaway's claims open an anchored popover with the because → so chain, sources, confidence and the choice it depends on. Esc or an outside click closes it.
- Header tabs **Simple · In-depth · Extensive**, with In-depth selected. Same tokens and motion as Case 1; light, dark and phone layouts. Other agents are unchanged.

Screenshots: `majlis-indepth/`.
