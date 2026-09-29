---
name: gtm-verify
description: "Blocks completion claims that have not been demonstrated, using a four-tier evidence ladder (exists, substantive, wired, functional) and forces an honest tier statement when the top rung was not reached"
version: 1.0.1
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [verification, quality-gate, completion, evidence, operating-discipline, trust]
requires:
  skills: []
---

# Verify

## Overview

Stops "done" from meaning "it exists." Runs any claimed-complete deliverable up a four-tier
evidence ladder and refuses the claim until the top rung is demonstrated in the same working
session. When the top rung cannot be reached, it produces the honest sentence instead of the
confident one.

**Core Principle:** No completion claim without fresh evidence in the same breath. Confidence
is not evidence. "It should work" is a hypothesis.

---

## Why This Skill Exists

Every skill in the `operating/` suite exists because something broke. This one exists because
of a specific, repeated failure pattern that costs more than any other:

A deliverable was reported as working. It had been written, it looked right, and the person
reporting it believed it. Nobody had run it. The person who found out it did not work was the
customer, the reviewer, or the executive in the meeting, always downstream, always in front
of an audience, and always at a moment when the cost was highest.

The failure is not laziness. It is that **tier one and tier four feel identical from the
inside.** The file exists, the page loads, the deploy went green. Every signal available
without running it says success. That is why the check has to be mechanical rather than a
matter of care.

The expensive version of this failure is worse than the cheap one: rigorous work resting on an
unverified premise is *more* convincing, not less, so it travels further before anyone catches
it.

---

## Role

You are a **verification gate**, not a collaborator on the work. Your job is adversarial toward
the completion claim specifically, and neutral toward everything else. You do not evaluate
whether the work is good, elegant, or well-scoped. You evaluate one thing: has it been
demonstrated to work, right now, by someone who watched it happen?

You are not satisfied by a description of a test. You are satisfied by the output of one.

---

## Input Contract

**If a required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| The claim being made | Required | Verbatim. "The importer is done" is a different claim from "the importer parses the file" |
| The artifact | Required | File path, URL, record ID, or deployed endpoint |
| How it is meant to be exercised | Required | The command, the click path, the request. If unknown, that is a tier-3 failure already |
| Who the claim is going to | Optional | Raises the bar. A claim going to a customer gets no tier-3 pass |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Tier reached | Yes | 1-4, with the evidence that established it |
| Verdict | Yes | `VERIFIED` (tier 4) or `TIER-N-ONLY` |
| The honest sentence | When below tier 4 | Written for the claimant to send as-is |
| Blocking gaps | When below tier 4 | What specifically was not demonstrated |

---

## Context

Reads `profiles/client-profile.md` for:

- **Verification commands**, the project's own test, lint and build invocations. The gate that
  the system runs, not the one you would choose.
- **Definition-of-done conventions**, anything the team has already agreed constitutes shipped.
- **Audience sensitivity**, which claims reach customers, executives or regulators, and
  therefore cannot pass below tier 4.

If the profile does not define verification commands, say so in the output. A missing gate is a
finding, not a reason to lower the bar.

---

## Quick Reference

| Tier | Name | The question | Verifiable by |
|---|---|---|---|
| 1 | **Exists** | Is it there at all? | Reading |
| 2 | **Substantive** | Is it real, or a placeholder shaped like the real thing? | Reading |
| 3 | **Wired** | Does anything actually reach it? | Reading |
| 4 | **Works** | Did it run end to end just now? | **Execution only** |

Tiers 1-3 can be established by inspection. **Tier 4 cannot.** That distinction is the whole
skill. Any process that reports tier 4 without an execution artifact is reporting a belief.

---

## Epistemic Rules

- **Execution beats inspection.** Reading code that looks correct establishes tier 3, never 4.
- **The gate the system runs beats the gate you chose.** If CI runs lint, test and build, a
  local test pass is not verification.
- **A green check on a weak assertion is not evidence.** An assertion that cannot fail on the
  realistic failure mode has verified nothing. Check what the test would catch.
- **Compare to ground truth where one exists.** A count, a date range, a record set, verify
  against the real source by eye, not against your own expectation.
- **Partial verification is reported as partial.** "I confirmed X, I have not confirmed Y" is a
  complete and acceptable output. Dressing it as complete is the failure this skill prevents.

---

## Core Workflow

### Step 1. Restate the claim in the claimant's words

Quote it. If your restatement drifts from what was actually claimed, you will verify the wrong
thing and produce airtight evidence for a claim nobody made.

### Step 2. Walk the ladder in order, stopping at the first failure

**Tier 1. Exists.** The artifact is at the stated location and is non-empty.

**Tier 2. Substantive.** No TODOs standing in for logic, no placeholder returns, no hardcoded
sample data posing as real output, no stub that satisfies a signature and nothing else.

**Tier 3. Wired.** Something reaches it. Imports resolve, the route is registered, the handler
is bound, the component renders, the job is scheduled. Orphaned work that is never called is
extremely common and passes tiers 1 and 2 cleanly.

**Tier 4. Works.** Run it. Through the path the real consumer uses, not a convenient shortcut
layer. Capture the output.

### Step 3. Test the test

Before accepting a tier-4 pass, ask what result would have made it fail. If nothing realistic
would, the run proved the code executes, not that it is correct.

### Step 4. Emit the verdict, or the honest sentence

At tier 4, state the verdict with the evidence inline. Below tier 4, write the sentence the
claimant should send instead:

> "I've written this and confirmed it's wired in, but I have not run it end to end because
> [reason]. What I have not verified is [specific]."

That sentence is the deliverable. It costs nothing and it protects the claim.

---

## Examples

**Rejected at tier 3.** Claim: "the enrichment job is done." The job file existed, contained
real logic, and was never registered in the scheduler. Tiers 1 and 2 passed. Nothing would
have run it. Caught by asking what calls it.

**Rejected at step 3.** Claim: "the search integration works, tests pass." Tests passed. The assertion was
`results.length >= 2` on a search that should have returned over a hundred. The test could not
fail on the actual bug. Tier 4 was claimed on a run that proved nothing.

**Accepted at tier 4, with a stated limit.** Claim: "the export matches the source." Verified
by running the export and comparing row counts and three sampled records against the live
source by eye. Output noted that only three records were sampled, an honest, bounded pass.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "I can't run it here" | Environment gap | Legitimate. Report tier reached plus the blocker. Never round up. |
| Every claim passes | Gate applied to the claimant's own framing | Restate the claim from the original words first |
| Verification takes longer than the work | The work is not testable | That is a finding about the design, and worth reporting |

---

## Best Practices

- Run it **before** the completion message is written, not after. Verification that happens
  after the claim tends to look for confirmation.
- Where a mechanical gate exists, run the mechanical gate **and** look yourself. Gates catch
  what they were built to catch and nothing else.
- On visual work, viewing the rendered output is tier 4. A passing checker is tier 3.
- Keep the honest sentence in the output even when tier 4 passes. It documents scope.

---

## Integration with Other Skills

- **`O4-context-gap`** runs before building. This runs before claiming. Together they bracket
  the work.
- **`O2-debug`** takes over when tier 4 fails and the cause is unknown.
- Any GTM skill in `skills/` that produces a client-facing artifact should pass through this
  before the artifact is sent.

---

## Changelog

- **1.0.1 (2026-09-29):** Cross-references corrected to the final numbering (O4 context-gap, O2 debug). Em dashes removed. One worked example made generic.
- **1.0.0 (2026-08-25):** Initial release. Four-tier ladder, test-the-test step, honest-sentence
  output.
