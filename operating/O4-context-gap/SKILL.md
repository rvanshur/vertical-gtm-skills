---
name: gtm-context-gap
description: "Before any build, search for what already exists. The gap classifier sorts findings into six buckets, and about 40% land at the left end (already done)"
version: 1.0.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-28
tags: [search, discovery, waste-prevention, existing-work, pattern-recognition, operating-discipline]
requires:
  skills: []
---

# Context Gap

## Overview

The first move on any request is not to build. It is to go look. This skill makes that
mechanical, because "look around first" is advice everybody agrees with and nobody follows.

Before any implementation, enumerate what you need, search for what exists, and sort the
findings into one of six buckets. About 40% land at the left end, which is the one nobody
expects to find.

**Core Principle:** What if it is already done? Check before you build.

---

## Why This Skill Exists

A request comes in for an alert when an account goes quiet for three weeks. It feels like a
new build, and the afternoon is open. Five minutes of looking turns up a nightly job that
already scores every account on how recently anything happened and writes that score to a
field nobody reads. The work shrinks from a new system to a threshold and a notification on
a job that runs already.

That example is made up, but the shape happens every week.

This skill exists because the gap you do not find is the work you build twice. The failure
this skill prevents is invisible, which is why it needs a forced discipline. Knowing what
exists tells us whether to build, but the search has to produce a written result. Not "I
looked," but which bucket, the evidence for it, and what the next step is given that bucket.
"You already have this, it is called X" is the most valuable output this habit produces, and
it never feels like a win in the moment, because it feels like five minutes spent not
building. Add it up across a year of requests, though, and it is the biggest single saving
in the operating kit.

---

## Role

You are a discovery gate, not a builder. Your job is to answer one question before any
implementation starts: what exists already, and what would it take to use it instead of
building new?

You are skeptical of assumptions. Anybody can say "this is new," and most do. Your job is
to prove it, or find what they missed.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| What is being requested | Required | The problem statement, or the solution sketch, or both |
| What done would look like | Required | The success condition or the acceptance criteria |
| What you can search | Required | Codebase, knowledge base, prior projects, templates, tools |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| What was searched | Yes | Locations, search terms, scope |
| What was found | Yes | File paths or references to existing work |
| Gap classification | Yes | One of the six buckets |
| Recommended next step | Yes | Specific to the bucket |

---

## The Gap Classifier

Check in order. Most tasks do not need new work.

| Bucket | Definition | Evidence | Next step |
|---|---|---|---|
| **No gap** | Exists and works | Feature is running and already does what was asked | Use it, nothing to build |
| **Config gap** | Exists, needs tuning | System runs, a flag or threshold or rule needs change | Set the value |
| **Completion gap** | Scaffolding exists | Structure is there, < 50 lines to finish | Complete it |
| **Extension gap** | Similar exists | Related feature can be grown to cover this | Extend existing |
| **Pattern gap** | Pattern is shown | Codebase has worked examples to follow | Follow the pattern |
| **True gap** | Nothing exists | No prior art, no related feature, no pattern to follow | Plan new build |

**Rule of thumb:** About 40% of tasks turn out to be already done somewhere. That is the
author's working estimate, not a measured rate, and the split across the other five buckets
has not been measured. A true gap is the rare case people assume is the normal one.

---

## Core Workflow

### Step 1 - Enumerate what you need (30 seconds)

List every piece of context required to complete the task. Problem? Shape of solution?
Success condition? Constraints?

### Step 2 - Search where things live (2-5 minutes)

Search in this order:

1. Existing knowledge or synthesis docs (did anyone already answer this question)
2. Codebase for similar patterns or existing features
3. Tools or libraries you already pay for
4. Documentation or references about how things get built here

Use specific search terms. "Alert" is too broad. "Alert when field is stale for 21 days"
is searchable.

### Step 3 - Classify the gap

Work through the six buckets in order. The first bucket your evidence fits is the answer.

### Step 4 - Report findings

State what was searched, what was found (with file paths or references), which bucket it
landed in, and what the next step is given that bucket.

Never report "I looked and found nothing" without listing exactly where you looked. The
places you searched are part of the evidence. If you did not search, say so.

---

## Epistemic Rules

- Different searches find different gaps. Code patterns live in one place, knowledge lives
  in another. A thorough search hits multiple locations.
- "Not found" means you have evidence of absence. "Did not look there" means you have no
  evidence. The two are not the same.
- Completion gap means under 50 lines of real work, not under 50 lines of typing. Typing
  is cheap. Thinking is what takes time.
- Extension gap means the existing thing was not designed for this, but could be grown to
  cover it without breaking what it does today. If extending it requires a rewrite, it is
  not an extension. It is a new build.
- Configuration gap means the feature is running and just needs a number or a rule changed.
  If deployment or setup is needed, it is a completion gap, not a config gap.

---

## Best Practices

- The search has value even when nothing is found. "We looked here, here, and here, and
  nothing is built yet" is a complete output. You are not hiding a gap. You are proving
  it is real.
- Configuration gaps turn into deployment wins. "We built this two years ago but forgot
  to turn it on" is not a failure of the search. It is a win. You saved a month of work.
- Pattern gaps mean reading code. "Our pattern is X" takes longer than "that is similar."
  Spend the time. It saves the team from building three variations of the same thing.
- Completion gaps are about to become implementation. "The scaffolding is here, go finish
  it" is a concrete handoff. Do not round it up to "just build it from scratch" because
  the scaffolding looks incomplete.

---

## Integration with Other Skills

- **`O3-debate`** comes after this one. You found what exists, now debate whether the plan
  to use it or extend it is any good.
- **`O5-second-opinion`** reviews the decision. Is the gap bucket right?
- Run this first, every time. It is the gate that decides whether to build at all.

---

## Changelog

- **1.0.0 (2026-09-28):** Initial release. Six-bucket classifier, search discipline, written
  output requirement, 40% already-done rule of thumb.
