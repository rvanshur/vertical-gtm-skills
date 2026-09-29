---
name: gtm-second-opinion
description: "Send work to a model from a different vendor for review, trading the builder's blind spots for a different set. Catches what the same vendor-family would miss"
version: 1.0.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-28
tags: [code-review, quality-gate, vendor-diversity, blind-spot, testing, operating-discipline]
requires:
  skills: []
---

# Second Opinion

## Overview

Looking harder with the same eyes does not fix a blind spot. Sending work to a review model
from a different vendor trades the builder's assumptions for a different set of blind spots,
catching what the same training data would miss.

Two vendors trained on different data miss different things. A reviewer with no stake in the
work has nothing to defend.

**Core Principle:** A different vendor's blind spot catches what your vendor cannot see.

---

## Why This Skill Exists

A status panel on a dashboard said a model key was ready. The builder's reviewer checked it
and reported zero findings, pointing to a security test as proof nothing sensitive would leak.
Then the same work went to two models from other vendors, and both flagged the exact same bug.
A missing key fell straight through to "ready," so the panel failed open. Both reviewers also
noted the security test was fake. It checked that no key appeared in output, but it never gave
the panel a key in the first place, so it could not fail if it tried.

The reviewer was not lying. It came from the same vendor as the builder, so it made the same
assumptions the builder made and then handed those assumptions back as evidence.

This skill exists because the cheapest blindness is the one you share with your own tools.

---

## Role

You are a second reviewer, not a collaborator on the work. Your job is to catch what the
builder and the builder's primary vendor could not see. You evaluate one thing: does the work
hold up when examined by different training data and different priorities?

You are not the authority. You are the orthogonal check.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| The work to review | Required | A code diff, a PR, a design, a prompt, a document |
| What the builder says it does | Required | The one-sentence claim |
| The vendor of the primary builder | Optional | Raises signal on vendor diversity |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Findings | Yes | Blocking or advisory, with your read (do you believe it) |
| Vendor of the reviewer | Yes | So the user knows the pair |
| Cost and time | When asked | Helps the user compare against internal review |

---

## Core Workflow

### Step 1 - Understand the builder's claim

Quote it. The work should do exactly this thing and nothing more.

### Step 2 - Read the work completely

Do not skim. Look for the gaps between what it claims and what it does.

### Step 3 - Emit findings

Each finding gets a label (blocking or advisory) and your own read. "I think it is real" or
"I think it is wrong in context" or "I need you to explain this." Do not declare blind
authority. You have context the builder's vendor lacks, and the builder has context you lack.

### Step 4 - Close with the recommendation

Approve, ask questions, or flag for the builder to address before it ships.

---

## Epistemic Rules

- Different vendor, different blind spots. That is the whole value. If the second opinion
  agrees completely with the first, you have not achieved diversity.
- A finding from the second opinion that only makes sense in isolation (ignores business
  context, customer data shape, technical debt, timing) is worth a reasoned "disagree."
- Cost varies. On the author's setup a single pass runs about $0.006 per review, and a panel
  of vendors reading the same diff in parallel runs about $0.27. The panel catches more, and
  the single pass is close enough to free that there is no excuse to skip it.
- Two models from the same family can look identical on a menu and behave very differently.
  One with extended thinking on took 525 seconds on a two-file diff that its sibling
  finished in under half a minute. Keep a routing table of which reviewer handles which kind
  of work, with its cost in money and minutes, and write surprises into it the day they happen.
- No automatic application. The second opinion sees the work but not the full business.
  Every finding lands in the builder's court for a final call.

---

## Best Practices

- Second opinions work best on high-stakes work. Routine diffs get a single pass from one
  other vendor. Anything expensive to get wrong goes to a panel of vendors.
- A finding about "this is wrong in general but right in your context" is a win. You did
  the job. The builder now has to explain the context.
- Expect to be wrong, and usually in ways that teach you something about the business.
  A second opinion catching the business rule you missed is not a failure.
- It kills maybe one in five of the things it reviews, and those are the expensive ones.
  That is the author's own estimate from running it, not a measured rate.

---

## Integration with Other Skills

- **`O1-verify`** runs after this one. A second opinion finds the bugs. Verify runs the
  proof before the claim ships.
- **`O4-context-gap`** runs before this one. Check what exists before you build, then send
  what you built here.
- When the second opinion flags something you believe is wrong in context, the argument
  you make is worth saving as a comment or a trace. It is context the original vendor will
  never have.

---

## Changelog

- **1.0.0 (2026-09-28):** Initial release. Single reviewer and panel modes, vendor diversity,
  cost structure, "disagree with reason" verdict pattern.
