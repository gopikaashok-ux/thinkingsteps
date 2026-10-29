# Thinking steps at three depths: Evaluation agent (Option A)

Query in all three cases: *"Evaluate this vendor proposal. Should we approve it?"* with `Vendor proposal.pdf` attached and the **Evaluation agent** picked.

All three keep the same order from the lo-fi: **prompt → thinking → message → action + sources → (checkpoint) → message → thinking → summary → final answer**. What changes is how much each step shows, and where the extra detail opens.

| | Case 1 · Simple | Case 2 · In-depth reasoning | Case 3 · Show everything |
|---|---|---|---|
| Who it's for | Exec who wants the verdict | Decision-maker who needs to trust the *why* | Analyst / admin auditing or debugging |
| What the thinking is | A status trail | Part of the answer | Evidence and telemetry |
| Where detail opens | **Inline only** | **Inline accordion + focus modal** | **Side panel (trace)** |
| Thinking default | Collapsed, 1 line | Open while running, collapses at the end | Collapsed step rows, each with a Trace button |
| Step content | Past-tense verb + source chips | Goal / Plan / Watch for; score + reason + page; because → so chains | Tool name, target, latency, tokens, retries |
| User checkpoint | None | Yes, inline, only when one assumption flips the verdict | Yes, inline (shows as wait time in the trace) |
| Final answer | Verdict + 3 bullets + confidence line | + named gaps + "View full reasoning" | + "9/9 figures traced" + "Open full trace" |
| Code / raw data | Never | Never (human words only) | SQL, logs, JSON, export |

## Why each container

- **Inline (case 1).** The steps are reassurance, not reading material. Anything that leaves the chat costs more attention than the content is worth. Expanding pushes content down, one level deep, 3–5 rows max.
- **Inline + modal (case 2).** The reasoning is read *in the flow*, so short reasoning stays inline. The full scoring matrix (6 criteria × 5 columns, plus Assumptions / Counter-arguments / Gaps tabs) is too wide for the chat column and is a **read once, decide, close** job, so it goes in a modal. Not a side panel: nothing needs to stay open next to the answer. On phone the modal becomes a full-height bottom sheet.
- **Side panel (case 3).** The user goes back and forth between the answer and many steps. A side panel stays open, syncs to the selected step, and keeps the answer visible. A modal would hide the answer and close on every step change. ⤢ Expand goes full screen for long logs.

## Rules shared by all three

1. Messages to the user are one sentence, written to the user (not the model talking to itself).
2. The checkpoint is never a modal. It always has a recommended option and a timeout default, so the run never stalls.
3. Confidence always comes with its reason: "High · 1 gap" or a list of named gaps, never a bare label.
4. A source chip opens the source at the cited page or the tool response, nothing else.

## Images

| File | Shows |
|---|---|
| `case-1-simple.png` | Full flow, collapsed, plus the expanded thinking step |
| `case-2-in-depth.png` | Full flow with inline reasoning and the checkpoint |
| `case-2-modal-open.png` | "View full reasoning" modal |
| `case-3-full-trace.png` | Split view: compact chat + trace side panel |

HTML sources are in `src/`. To re-render, screenshot the `.page` element of each file at 2× with Playwright.

## Option B

A second take on the same three cases, built around a smooth experience: one live line instead of stacked blocks, a reasoning rail with "why" popovers on each claim instead of a modal, and a bottom dock instead of a side panel. See [`option-b/README.md`](option-b/README.md).

## Built: Option A · Case 2 in the Majlis dashboard (Peer Benchmarking)

`/Option A - In-depth.html` (repo root) is the Majlis dashboard with Option A's in-depth format working for the **Peer Benchmarking** agent. Pick Peer Benchmarking, ask one of its questions (or use a Try chip) and send. Blocks appear in the thread as the work happens, in the lo-fi order:

1. **Thinking**, open while running: Goal, Plan, Watch for.
2. **Message**: what I'll do next.
3. **Action card**: each indicator lands with Barakah's value, a bar against the peer median, its rank, why, and the sources.
4. **Need your call**, inline: the run pauses on the one assumption that changes the result (e.g. count Unit 4's first fuel cycle: forced loss 1.9% vs 2.3%). Recommended first, keys 1–3, 20s countdown.
5. **Message**: what I found, reflecting your choice.
6. **Thinking again**: the trade-offs as because → so lines.
7. **Quick summary**, collapsed (expands to the table), then the **answer**, with a note when your choice differs from its figures, and **Confidence and gaps** with **View full reasoning**: a focus modal with Evidence / Assumptions / Counter-arguments / Gaps tabs.

When the answer lands the thinking blocks and the action card fold to one line. Content covers all four Peer Benchmarking questions (fleet comparison, forced loss by unit, refuelling outages, value of closing the gap). Header tabs **Simple · In-depth · Extensive** with In-depth selected. Light, dark and phone layouts; other agents unchanged.

Screenshots: `majlis-option-a-indepth/`.
