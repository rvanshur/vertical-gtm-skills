---
name: gtm-debug
description: "Enforce evidence-based debugging with a circuit breaker. No fix without a hypothesis first. After three failed hypotheses the session stops, writes a handoff, and re-plans"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [debugging, root-cause-analysis, circuit-breaker, hypothesis-testing, evidence, operating-discipline]
requires:
  skills: []
---

# Debug

## Overview

The most expensive habit in technical work is trying the same approach a fourth time with
slightly different inputs. It feels like persistence, but it is almost always a sign the
diagnosis is wrong and not the execution.

This skill enforces two rules: no fix without a written hypothesis stating what is wrong and
what evidence would prove it, and a circuit breaker. After three failed hypotheses the
session stops, writes a handoff, and re-plans.

**Core Principle:** Three attempts is data. A fourth attempt is just thrashing.

---

## Why This Skill Exists

A bug lives in a method. The right answer is to read the method top to bottom. Instead, the
first instinct is to try something, see if it works, and if not try something slightly
different. Four full build-restart-rerun cycles later, about ten minutes each, nothing has
changed and nobody has written down what each attempt proved. The fifth attempt is not
another guess. It is sitting down and reading the whole method from start to finish, which
could have happened forty minutes earlier.

This skill exists because the loop is invisible from the inside. Each attempt feels like
progress. Only the written record makes the pattern visible.

The discipline is not about being smarter. It is about being honest about what you know and
what you do not know. A stated hypothesis is a bet that you have enough evidence to make a
prediction. Three failed bets means the evidence you had was wrong, and the next move is not
another bet. It is to stop and gather better evidence.

---

## Role

You are a circuit breaker, not a debugger. Your job is to stop the thrashing and force the
handoff when the approach is not working.

You are not the one fixing the bug. You are the one making sure the fix attempt is built on
evidence, not hope.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| The symptom | Required | What is wrong, what did you expect, what happened instead |
| The environment | Required | Where it breaks (local, CI, production, intermittent) |
| Recent changes | Optional | What changed right before it broke |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Hypothesis | Yes | Statement of what is wrong and why, before evidence gathering |
| Evidence gathered | Yes | Source trace, reproduction recipe, logs, test results |
| Verdict | Yes | Hypothesis confirmed, disproved, or unfinished |
| Action | Yes | The fix, or the handoff to re-plan |

---

## Context

If `profiles/client-profile.md` has a `## Debugging` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Step 1 - State the hypothesis (BEFORE evidence)

Write one sentence: "I believe the root cause is X because Y."

X must name the specific file, function, line, or condition. Not "state management issue"
(rejected). "The component calls setLoading before the request completes, so the loading
state never clears" (accepted).

Y must reference evidence already in hand. If you cannot write Y, you do not have enough
evidence yet. Go gather it.

List all observable symptoms. The hypothesis must explain every one. A partial explanation
means you are at the symptom level, not the root cause.

### Step 2 - Gather evidence (in order)

1. **Source trace** - exact file, line, condition that triggers the symptom
2. **Deterministic reproduction** - smallest command or click path that reproduces
3. **Runtime inspection** - logs, state, cache, database rows
4. **Test verification** - does the test suite agree the symptom exists
5. **Real runtime check** - for UI bugs, screenshot or artifact

Compare working vs. broken code completely. No skimming. List every difference.

### Step 3 - Hypothesis confirmation gate

Progress to fix ONLY if one of these is true:

- A log line or instrumentation confirms the hypothesis
- You can predict the next error before running it
- You understand the full propagation path from root cause to symptom
- You can write a test that fails on unfixed code

If the hypothesis fails at any gate, discard it entirely. Do not patch it. Do not "just add
one more thing." Discard and re-orient.

### Step 4 - Implement the fix

One change at a time. Never stack multiple fixes. Write evidence in the same message as the
fix claim: the test that now passes, the output that changed, the line that proves it.

---

## The Circuit Breaker

After three failed hypotheses, the session stops.

**Emit a handoff:**

```
Stopping after 3 failed hypotheses. Re-planning needed.

Hypotheses tried (with disproving evidence):
1. [Hypothesis]. Disproved by: [evidence]
2. [Hypothesis]. Disproved by: [evidence]
3. [Hypothesis]. Disproved by: [evidence]

Evidence collected:
- [Source trace findings]
- [Reproduction recipe]
- [Runtime inspection results]

Remaining unknowns:
- [Specific questions evidence has not answered]

Suggested next moves:
- [Concrete next step requiring user input or different approach]
```

Do not attempt a fourth hypothesis. Do not guess. Hand off clean and re-plan.

---

## Epistemic Rules

- "I'll just try this" without a stated hypothesis is rejected. Write the hypothesis first.
- One untracked change becomes ten. Write the hypothesis before touching any code.
- Confidence without proof is hope. Do not confuse the two.
- "Probably the same issue as before" is bias. Re-read the code from scratch.
- A patch applied to a symptom creates a new bug somewhere else. Fix the root cause.
- Stacking a second fix on the first obscures what is actually working. Rebuild from evidence.

---

## Best Practices

- Hypothesis first, evidence after. Write it down before anything changes. The writing breaks
  the loop because you cannot list three attempts without noticing they all share an
  assumption.
- The handoff is a file, not a conversation. It has a shape (problem in one line, every
  hypothesis with what disproved it, what we now believe is happening, a concrete next
  action). A next action is "add logging at line 47," not "keep investigating."
- Three attempts teaches what two would not. The pattern only shows up when you see it
  written down.
- For regressions (used to work), add what commit broke it, why it recurred, and why the fix
  prevents recurrence.

---

## Integration with Other Skills

- **`O1-verify`** confirms the fix actually works. This skill stops the guessing, and that one
  stops a guess from shipping.
- **`O4-context-gap`** runs before this. You should not be debugging something you should
  not be building.
- Stop after three. Hand off. Let somebody else look. A fresh pair of eyes sees what
  thrashing has obscured.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section added, so the skill reads the profile section its CUSTOMIZE.md writes.
- **1.0.0 (2026-09-28):** Initial release. Hypothesis-first discipline, three-attempt circuit
  breaker, handoff format, evidence-gathering order.
