---
name: gtm-dream
description: "Consolidates and prunes knowledge base by finding stale, contradicted, or duplicated items, with a hard rule that strips dead links but never deletes the words that surround them"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [consolidation, pruning, maintenance, memory, contradiction-detection, operating-discipline]
requires:
  skills: []
---

# Dream

## Overview

Runs a consolidation pass on your knowledge base to identify stale, contradicted, or duplicated items. It fixes what it can safely fix without human judgment. For everything else, it flags the item and asks before touching it.

The metaphor is REM sleep: prune what is no longer true, consolidate what is, identify what needs a decision.

**Core Principle:** Stale intelligence is worse than none. People trust it, and then they act on it. The most important fixes are the ones that remove wrong information.

---

## Why This Skill Exists

A knowledge base decays silently. Items are added. Time passes. The world changes. Nobody updates the old items. A year in, nobody knows which items are still true. A person reads an old item with confidence, acts on it, and learns too late that it was wrong.

The skill exists because of a specific pattern. Early consolidation runs worked like a text editor. If something was wrong, delete it. That sounded right until one run encountered an index entry that ran 2,371 characters, linked ten related items, one of which had a dead reference. The naive rule would have deleted all nine live references and a paragraph of project history to fix one broken pointer.

The rule that came out of it is procedural, not motivational. Every fix that runs without human approval has to be additive or markup-only. If a fix removes words someone wrote, it belongs under "ask first," no exceptions. The fix became a four-word rule, "de-link, never de-line." Strip the markup around the dead reference and keep every word. Applied correctly, the cost was exactly 252 characters of markup, and zero words lost.

The pass also teaches what not to automate. A rule to auto-correct vague dates looked useful until measurement: 107 raw matches, about 5 real ones. Most were quoted speech or state descriptors ("currently missing"), which were correct as written. Run automatically, the rule would have silently falsified the record it was meant to clean.

---

## Role

You are a **curator and contradiction hunter**, not a janitor. Your job is to identify what is stale, contradicted, or duplicated, and to prune with surgical precision. Every word a human wrote is presumed valuable until proven otherwise.

---

## Input Contract

**If required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Knowledge base location | Required | Path to all items to be consolidated |
| Age thresholds (stale) | Required | How old does an item have to be to be flagged? (usually >30 days) |
| Expiry dates | Required | Any items marked with an expiry date? |
| Metadata format | Required | How items mark their status, age, relationships |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Health score | Yes | Before and after, with explanation |
| Stale items found | Yes | Items past age threshold, candidates for review |
| Contradictions found | Yes | Multiple items claiming different things about the same topic |
| Duplicates found | Yes | Near-duplicate content, candidates for merge |
| Dead references found | Yes | Broken links, items that reference non-existent others |
| Changes made | When asked | Additive or markup-only fixes applied |
| Approval needed | Yes | List of items requiring human judgment before deletion |

---

## Context

If `profiles/client-profile.md` has a `## Knowledge Base Consolidation` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Phase 1. Scan

Discover all items in the knowledge base.

1. Glob all `.md` files in the KB directory
2. Read each item's metadata (status, created date, updated date, any expiry date)
3. Count totals and report them

### Phase 2. Analyze

For each item, check for issues:

**Staleness:**
- Read the created/updated dates
- If an expiry date is set and today's date is past it → flag as expired
- If no expiry date and age >30 days with no evidence of review → flag as stale
- If an item is marked "provisional" / "emergent" and age >30 days → flag as aging (needs a decision)

**Dead references:**
- Scan all links / references in the item
- Check if the target item exists
- Flag broken links

**Contradictions (within clusters):**
- Group items by subject (common keywords in filename or tags)
- Within each group, look for items claiming different facts about the same thing
- Example: two items about the same topic with conflicting numbers, dates, or claims
- Flag pairs for review

**Duplicates:**
- Look for items that are substantially the same content
- Look for items with high keyword overlap but different names
- Flag for merge review

### Phase 3. Report and Ask Approval

For each class of issue, present findings and ask:
- **Stale items:** Archive or extend? (If extended, update the date)
- **Expired items:** Archive?
- **Dead references:** Fix with de-link (strip markup, keep words)? Delete the entire item?
- **Contradictions:** Which version is correct? Merge or delete one?
- **Duplicates:** Merge into one, or keep separate? (If separate, clarify why)

For dead references inside larger items, always offer de-link as the default.

### Phase 4. Consolidate

Apply approved changes:
- Delete items user approved for deletion
- Merge duplicates into one canonical item
- Strip dead link markup (de-link, keep words)
- Rewrite compiled-truth sections where evidence changed
- Archive old items

**Never edit a stale item's body without asking.** Stale items are candidates for archive or extension, not rewrites.

### Phase 5. Rebuild Index

After all changes, rebuild the knowledge base index (if one exists). Ensure all remaining items are discoverable.

### Phase 6. Report Health Score

Calculate health score before and after (see `O7-graph-health` for scoring rules).

Report the before/after delta.

---

## Quick Reference

| Issue Type | Auto-fix | Ask Approval |
|---|---|---|
| **Dead link inside a live item** | De-link (strip markup, keep words) | Only if the entire item looks orphaned |
| **Stale item** | None | Archive or extend? |
| **Expired item** | None | Archive? |
| **Duplicate items** | None | Merge or keep separate? |
| **Contradiction** | None | Which is true? Delete wrong one? |
| **Orphaned item** | None | Archive or reconnect? |

---

## Epistemic Rules

- **Markup-only is safe to automate.** Stripping a broken link's brackets is safe. Deleting the sentence is not.
- **Words are not garbage.** If a human wrote it, assume it is valuable until proven otherwise.
- **Stale is not false.** An old decision was correct when made. Archiving it means "this is history now," not "this was wrong."
- **Contradictions are data.** Two items claiming different things means either one is wrong, or they describe different contexts. Merge them only if they truly overlap.
- **Measure false positives.** A rule that auto-fixes 107 matches with 102 false positives is broken. Test rules on samples before running them wide.

---

## Hard Rules

- **Never delete words without asking.** This is non-negotiable.
- **De-link, never de-line.** When a link is broken, strip the markup. Keep the words.
- **Don't auto-correct vague dates.** "Currently missing" is correct as written. Don't change it.
- **Don't auto-merge duplicates.** Duplicates might represent different contexts or stages.
- **Preserve the timeline.** If an item has dated evidence entries, keep them. Never edit the timeline.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "Too many stale items to review" | KB has accumulated significant age | Widen the age threshold or run in batches by subject |
| "Nothing is old enough to flag" | Age thresholds are too conservative | Adjust thresholds or check metadata is being read correctly |
| "Can't tell if items contradict" | Items describe different contexts | Ask: do these items conflict or complement? |
| "Deleting this feels like losing work" | You are deleting the wrong thing | Probably: archive instead, or ask the item owner before deleting |

---

## Best Practices

- Run this monthly, or when the health score (from `O7-graph-health`) drops below 70.
- Before running in "make changes" mode, run in report-only mode first.
- When you find a contradiction, look at dates. The newer item might be a correction.
- Share the report with the team if it is a shared KB. Structure is everyone's responsibility.
- If consolidation stalls, that is data. Stopping early is better than making bad calls under time pressure.

---

## Integration with Other Skills

- **`O7-graph-health`** flags what is broken. This fixes it.
- **`O9-ingest`** adds new items. This consolidates the accumulated items.
- **`O6-weekly-review`** uses a lightweight version of stale detection.
- Together, ingest (add) → graph-health (diagnose) → dream (consolidate) is the cycle.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section added, so the skill reads the profile section its CUSTOMIZE.md writes.
- **1.0.0 (2026-09-28):** Initial release. Consolidation pass with de-link-never-de-line rule, stale/expired/contradiction/duplicate detection, and approval-required workflow.
