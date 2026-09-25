---
name: human-handoff
description: "Turns a finished agent handoff into a short recommendation for the human: What happened, then ACCEPT, CLARIFICATION REQUIRED or DO NOT ACCEPT, then Why, judged only from the supplied text. Use when a completed delivery or completed review, your own or another agent's (Claude, Codex, Kimi, Grok, a terminal agent), is handed back to the human for a decision; when the human pastes an agent's final report and wants to know whether to accept it; or when the human asks for human-handoff by name. On DO NOT ACCEPT it also writes, at once, one corrective prompt the human can paste to the agent that built the work. Never opens files or runs commands, and never replaces the builder's or reviewer's own report. Not for progress updates, plans, subtasks inside ongoing work, quoted or old reports, talk about this skill, corrective prompts, earlier Human Handoff summaries, work still headed to an independent reviewer, or Workspace or Backloop board activity."
---

# Human Handoff

Turns a finished agent handoff, however long, into a few plain lines the human can act on. Any agent can use it: Claude, Codex, Kimi, Grok, a terminal agent. It is not part of Workspace.

**READ HANDOFF → UNDERSTAND → RECOMMEND → HUMAN GATE.** Nothing more.

## When it runs

Automatically only when the context clearly is a finished delivery or a completed review coming back to the human, whether it is a handoff someone brings you or your own finished work as you hand it back: the task or review has reached its stopping point, the result has been presented, the agent has stopped working, and the next move is the human's. For your own work, the summary ends your final message, and its Why says you did the work yourself, so it is not an independent check. Also whenever the human asks for it.

Not automatically for:

- progress updates, or a finished subtask while the main task goes on;
- plans;
- quoted examples, and historical or old reports;
- ordinary discussion, including discussion of this skill;
- corrective prompts;
- earlier Human Handoff summaries, your own included;
- Workspace or Backloop board activity, which has its own gates;
- a delivery still waiting for its independent review (a finished review is not one).

Words such as done, complete, review, handoff or passed are never a trigger by themselves. When unsure, do not run; the human can still ask for it.

## Beside other handoff skills

Skills such as engineering-builder-handoff (the builder's report) and independent-review-handoff (the reviewer's report) write a handoff; this skill never writes or replaces one. When one of them writes your final report, that report comes first and stays whole: never trim it or merge into it, and add the summary after it only when the next move is the human's.

## Evidence boundary

Judge only what the conversation or the pasted handoff supplies. Do not open files, inspect the repository, run commands or tests, use tools to check a claim, edit anything, start agents or hand over to another skill. Do not review the code yourself or widen the scope.

- **Supported** — the handoff shows how it is known: command output, exact counts or results, named checks with their outcomes, a reviewer's verdict.
- **Claimed** — the agent's word alone: "done", "fixed", "works", "tests pass" with nothing shown.

Missing evidence is not a defect. Never invent a failure. When a gap decides the outcome, ask about it; do not reject for it.

## Recommend

Exactly one of three. It is always about the delivered work; for a review, the work that was reviewed, never the review itself.

- **ACCEPT** — the supplied evidence is enough to accept the requested work. Then stop: no new task and no prompt unless the human asks.
- **CLARIFICATION REQUIRED** — the context is too unclear, incomplete or contradictory to decide: it is unclear whether a required test ran, two statements conflict, it is unclear whether the whole scope was done, or an important point is not explained. This is not a rejection. Ask one focused question about the point that decides it — no corrective prompt, no open-ended request for reassurance. When the answer comes back, decide on it; do not ask again about a point it settled. If the open point is really the human's own product or scope choice, say so in Why instead of adding a state.
- **DO NOT ACCEPT** — only when the supplied evidence itself establishes a blocking defect, a failed requirement or an unmet acceptance condition. The corrective prompt follows in the same reply; then stop.

## Output

Plain words for someone who does not read code:

```
What happened:
<one or two sentences>

Recommendation:
<ACCEPT | CLARIFICATION REQUIRED | DO NOT ACCEPT>

Why:
<one to three short sentences>
```

CLARIFICATION REQUIRED adds:

```
What is unclear:
<one short line>

Question to send:
<one focused question, ready to paste to the agent>
```

DO NOT ACCEPT adds:

```
Corrective prompt:
<the one corrective output described under Corrective prompt below>
```

and then ends with exactly this line: `Your call. The prompt above is ready to paste to the agent that built the work if you agree with the rejection.`

## Corrective prompt

With every DO NOT ACCEPT, exactly one corrective output follows in the same reply, addressed to the agent that built the work. If the handoff comes from a skill with its own corrective format, such as independent-review-handoff's CLAUDE CORRECTIVE HANDOFF, use that format and write no prompt of your own: reply with the handoff's own version unchanged if it has one, write it by that skill's rules with every detail they require if that skill is available here, or else tell the human to ask the agent that wrote the handoff for it. Otherwise, write one concise corrective prompt they can copy, in this shape:

```
Fix only: <each blocking issue, with the evidence that showed it>
Keep unchanged: <what already works, and anything already accepted>
Do not: <add features, clean up, or change anything else>
Send back: <the exact check to run, and its result>
```

Only what the handoff established goes into it: no issue the evidence did not show, and no new task. Do not send it, run it or act on it. Write it once; write another version only when the human asks. ACCEPT and CLARIFICATION REQUIRED get no corrective prompt.

## Human gate

The human decides. Never present a recommendation as the human's decision, and never write it as "accepted" or "rejected". The corrective prompt is an offer, not an action: the human chooses whether to send it, and if the human decides otherwise, that decision stands.

## One summary per delivery

At most one Human Handoff summary per task and delivery revision. Give a new one only when materially new evidence arrives, the delivery materially changes, or the human asks for another assessment. If the same delivery comes back unchanged, say in one line that the earlier recommendation stands. Never treat a Human Handoff summary, yours or a pasted one, as a new handoff to assess.

Provenance: before this skill was built, the open skills ecosystem was searched on 2026-09-22 for human handoff, handoff summary, handoff recommendation, accept or reject recommendation, review verdict summary and agent report summary. The nearest results were session-continuity handoffs, a fixed-format build-handoff record, a review-verdict schema and a pull-request summary that runs shell commands; none turned a finished agent handoff into a gated recommendation for the human.
