---
name: gtm-second-opinion
description: "Send work to a model from a different vendor for review, trading the builder's blind spots for a different set. Packages the work for the other vendor, then triages what comes back. Catches what the same vendor-family would miss"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
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

That has one practical consequence. **The assistant running this skill is usually the builder's
own vendor**, for example Claude reviewing work Claude helped build. So this skill does not ask
it to be the reviewer. It asks it to do the two jobs around the review: package the work so a
different vendor can review it cold, and triage the findings when they come back.

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

You run the second-opinion loop. You are not the second opinion yourself unless you come from a
different vendor than the one that built the work. If you do, skip to Step 3 and review. If you
do not, or you are not sure, your job is to get the work in front of a different vendor with
everything it needs, and then to judge what it sends back on behalf of the builder.

You are not the authority. You are the orthogonal check, or the person who arranges one.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| The work to review | Required | A code diff, a PR, a design, a prompt, a document |
| What the builder says it does | Required | The one-sentence claim |
| The vendor that built it | Required | Decides whether you can review it yourself |
| Which other vendor the user can reach | Required | A chat app, a CLI, or an API key. See Step 2 |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Review packet | When routing out | The claim, the work, and the reviewer instructions in one block the user can send |
| Findings | Yes | Blocking or advisory, each with your read (do you believe it, and why) |
| Vendor of the reviewer | Yes | So the user knows the pair |
| Cost and time | When asked | Helps the user compare against internal review |

---

## Context

If `profiles/client-profile.md` has a `## Review Process` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Step 1. Pin the builder's claim

Quote it. The work should do exactly this thing and nothing more. Note which vendor built it.

### Step 2. Get it to a different vendor

If you are the same vendor as the builder, do not review. Build the **review packet** below and
route it one of three ways, whichever the user actually has.

1. **Paste into another vendor's chat.** Works for anyone. Open ChatGPT, Gemini or any other
   vendor's assistant and paste the packet. No setup, and it is the right default for copy,
   plans and documents.
2. **A second vendor's CLI.** If the user has another vendor's command-line agent installed
   (for example OpenAI's Codex CLI and its non-interactive mode, `codex exec`; check `--help`
   for your version), send the packet from the same terminal so the reviewer can read the files
   itself. The best fit for code.
3. **An API call.** If the user has another vendor's API key, a short script can send the packet
   and save the reply. Worth it once reviews are routine, because it can run as a gate.

The review packet, which you fill in and hand to the user:

```
You are reviewing work built by a different AI vendor. You have no stake in it.

CLAIM: [the builder's one-sentence claim]
WORK: [the diff, document or design, in full, or the file paths if you can read them]
CONTEXT YOU LACK: [anything about the business or data shape the reviewer needs]

Find where the work does not do what the claim says. For each finding give: what is wrong,
where, how you know, and whether it blocks shipping. Say plainly if you found nothing, and
what you checked to reach that. Do not rewrite the work.
```

For anything expensive to get wrong, send the same packet to two vendors separately, and do not
show either one the other's answer.

### Step 3. Review (only when you are the different vendor)

Read the work completely. Do not skim. Look for the gaps between what it claims and what it
does, then emit findings in the format the packet asks for.

### Step 4. Triage what comes back

Each finding gets a label (blocking or advisory) and your own read: "I think it is real",
"I think it is wrong in context, because...", or "I need you to explain this." The reviewer has
context the builder's vendor lacks, and the builder has context the reviewer lacks. Nothing is
applied automatically. Where two reviewers flag the same thing independently, say so, because
that agreement is the strongest signal this skill produces.

### Step 5. Close with the recommendation

Approve, ask questions, or flag for the builder to address before it ships. Name the reviewer's
vendor and, if the user asked, what the review cost.

---

## Epistemic Rules

- Different vendor, different blind spots. That is the whole value. A review by the builder's
  own vendor, however careful, is not a second opinion, and this skill says so rather than
  quietly running one.
- If the second opinion agrees completely with the first, you have not achieved diversity.
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
- Start with the paste route. It costs nothing to set up, and it tells you within a week
  whether the findings are worth automating.

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

- **1.1.0 (2026-09-29):** The skill now works when the assistant running it is the builder's
  own vendor. New Step 2 (review packet plus three routes: another vendor's chat, a second
  vendor's CLI, an API call), a triage step, the builder's vendor as a required input, and a
  Context section that reads the Review Process profile section.
- **1.0.0 (2026-09-28):** Initial release. Single reviewer and panel modes, vendor diversity,
  cost structure, "disagree with reason" verdict pattern.
