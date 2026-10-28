# Option B: thinking steps at three depths, built for smoothness

Same query, agent and seven-step order as Option A (`../README.md`). Option B changes the interaction, guided by four smoothness rules:

1. **No layout jumps.** Live progress stays a fixed height, and a ghost outline holds the answer's space before it streams.
2. **One thing open at a time.** Finished steps fold away on their own; the user never has to collapse anything.
3. **Detail sits next to what it explains.** Reasoning is attached to the claim it supports, and trace data to the figure it produced, instead of a separate place to go and read.
4. **Change depth without re-asking.** Every answer has a **Brief · Reasoning · Trace** switch over the same run.

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
