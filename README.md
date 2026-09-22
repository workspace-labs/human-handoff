# Human handoff

**An AI agent finishes a job and hands back a long report. You still have to decide: accept it or not? This skill reads the report and answers in a few plain lines — then waits for you.**

Human Handoff is an Agent Skill. It turns a finished agent handoff, a delivery or a review, into a short recommendation: what happened, one of three answers, and why. It works with any model that reads Agent Skills: Claude, Codex, Kimi, Grok or a terminal agent. It was made for everyday agent sessions outside the author's own board, Workspace, which has review gates of its own, so it steps aside there.

The skill is one file — [`skills/human-handoff/SKILL.md`](skills/human-handoff/SKILL.md).

---

## In practice

```
What happened:
Kimi built the password reset form and token storage and says the task is complete.

Recommendation:
DO NOT ACCEPT

Why:
The task's one requirement is that a reset sends exactly one email, and Kimi's own test run shows that test failing.

Your call. If you agree with the rejection, say so and I will write the corrective prompt.
```

*A made-up example: the report said "task complete", and its own test output said otherwise.*

---

## The three answers

- **ACCEPT** — what the handoff shows is enough to accept the work. Then it stops.
- **CLARIFICATION REQUIRED** — the handoff is too unclear, incomplete or contradictory to decide. This is not a rejection: it names what is unclear and gives you one question to send back.
- **DO NOT ACCEPT** — the handoff itself shows a blocking defect or a failed requirement. Then it stops and waits for you.

It recommends. You decide.

---

## When it runs

- **On its own, best effort:** when a finished delivery or a finished review comes back to you, whether it is a report you paste in or the agent's own finished work. Every agent decides for itself when a skill applies, so it can miss one.
- **When you ask:** `/human-handoff` in Claude Code, `$human-handoff` in Codex, or "should I accept this?" in any agent.
- **Not for:** progress updates, plans, quoted or old reports, work still waiting for its review, or its own earlier answers. One answer per delivery, unless something new arrives or you ask again.

---

## What it will and won't do

- **It judges only what it is given.** It doesn't open the repository, run commands or tests, edit files, start agents, or check claims beyond the handoff in front of it. A claim with nothing shown stays a claim.
- **Missing proof is not a defect.** It never invents a failure. When a gap decides the answer, it asks.
- **Nothing corrective before your yes.** After DO NOT ACCEPT it writes no fix prompt until you agree with the rejection. Nothing is sent or run for you.
- **One corrective output, never two.** If the handoff comes from a skill with its own corrective format, such as a reviewer's repair packet, that format wins and it adds nothing of its own. Otherwise it writes one short prompt: fix only this, keep the rest, change nothing else, send back the proof.

---

## Use it

One line, for every project on your machine:

```bash
npx skills add workspace-labs/human-handoff -g
```

Or copy it by hand:

```bash
git clone https://github.com/workspace-labs/human-handoff.git
mkdir -p ~/.claude/skills
cp -R human-handoff/skills/human-handoff ~/.claude/skills/
```

For Codex:

```bash
mkdir -p ~/.codex/skills
cp -R human-handoff/skills/human-handoff ~/.codex/skills/
```

Any other agent that reads Agent Skills takes the same folder in its own skills directory.

---

## What it costs

- **One more short block** at the end of a finished job.
- **It can only be as right as the handoff.** A report that states a false result in convincing detail can still get ACCEPT; it can't see what it isn't shown.
- **Smaller models follow it less reliably.** In testing, a small model sometimes broke its rules where a larger one did not.

**Worth it when:** you read agents' reports and have to decide what to accept.

**Not worth it when:** you check the work yourself anyway.

---

## The shortest version

> Read the handoff. Say accept, ask, or don't accept — and why. Then wait: nothing corrective until the person agrees.

---

<sub>by Workspace Labs</sub>
