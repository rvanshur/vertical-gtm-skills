---
name: gtm-graph-health
description: "Diagnoses knowledge base structure health by measuring tag sprawl, link density, and item age, not whether items are true, but whether the system is usable"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [graph-health, knowledge-base, structure, taxonomy, orphans, operating-discipline]
requires:
  skills: []
---

# Graph Health

## Overview

Measures whether your knowledge base is well-structured and usable as a system, independent of whether each individual item is true.

A base can be mostly accurate and still be a mess. Tags fragment into one-off variants that nothing will find, items sit isolated with no connections, half-finished items never get promoted or retired. None of that shows in a single item. All of it shows when you measure the structure.

This skill runs three gauges, tag sprawl, link density, and provisional item age, and produces a health score. It is read-only. It flags problems but does not fix them.

**Core Principle:** A system where every item is true but the structure is broken is unusable. Health is a property of the whole, not the parts.

---

## Why This Skill Exists

Documentation systems decay silently. A wrong number looks exactly like a right one. There is no error message. The decay only surfaces when someone tries to find something and cannot.

The skill exists because of a specific pattern. A base was maintained carefully. Entries were added one at a time. Nobody kept count of the tags. One person used `GTM-strategy`, another used `gtm-strategy`, a third used `go-to-market`. The search surface fractured without anyone noticing. A base can be mostly true and completely unusable if its structure has broken.

The thresholds below are the author's working rules, not an industry standard, so tune them in CUSTOMIZE.md. Tag sprawl above 40% means search becomes noise, too many one-off tags that nothing else will find. Orphan items (fewer than three links) need discovery. A note nobody can find except by exact recall stays frozen. Hub items (more than ten links) are a sign that something needs splitting, nothing that large gets updated cleanly. Age of provisional items matters too. Mark something as emergent and it will stay emergent forever unless someone forces a call. Thirty days is when to decide. Sixty is when it becomes critical.

---

## Role

You are a **structural auditor**, not a content reviewer. Your job is not to judge whether items are accurate or complete. It is to measure how well-formed the system is and flag where structure has broken.

---

## Input Contract

**If required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Knowledge base location | Required | Where the items / nodes are stored (directory path) |
| Taxonomy file | Required | The blessed list of tags (if one exists) |
| Item metadata conventions | Required | How items are marked up (status field name, link format, etc.) |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Health score | Yes | 0-100, with explanation |
| Inventory | Yes | Count of items by domain, status, type |
| Tag analysis | Yes | Sprawl %, single-use tags, non-blessed tags |
| Link analysis | Yes | Orphan items, hub items, broken links |
| Lifecycle analysis | Yes | Aging provisional items, decision points |
| Recommendations | Yes | Top 3 actions to improve health |

---

## Context

If `profiles/client-profile.md` has a `## Knowledge Base Structure` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Step 1. Inventory

Walk the knowledge base directory. Count all items:
- By domain (if your system uses domain tags: technical, business, GTM, methodology, etc.)
- By status (emergent, validated, canonical, archived)
- By type (concept, pattern, case-study, framework, reference)

Report totals. This is your baseline.

### Step 2. Tag Health Analysis

Read the taxonomy file (blessed tags). Then scan all item metadata:
- Count unique tags actually in use
- Count tags that appear only once
- Count tags not in the taxonomy (sprawl)

**Sprawl calculation:** (single-use tags / total unique tags) * 100

| Sprawl % | Health |
|---|---|
| <20% | Healthy |
| 20-40% | Warning |
| >40% | Unhealthy |

List the single-use tags and non-blessed tags.

### Step 3. Link Health Analysis

For each item, count its connections (wiki-links, references, or whatever your system uses):

| Link Count | Category | Implication |
|---|---|---|
| <3 | Orphan | Nobody will find this except by exact recall. Needs discovery |
| 3-10 | Connected | Healthy density |
| >10 | Hub | Likely needs splitting. Nothing this large gets maintained |

List orphan items and hub items by name.

### Step 4. Lifecycle Analysis

For items marked as provisional / emergent / incomplete:
- Calculate age (today's date minus creation date or last update)
- Flag items >30 days without a status decision as needing a call
- Flag items >60 days as critical, decide now

### Step 5. Check for Broken Links

Scan all references. For each link:
- Does the target item exist?
- Flag broken links

Count and list them.

### Step 6. Calculate Health Score

Start at 100. Deduct:
- -3 per stale item (>30 days, no decision point, no valid_until)
- -4 per expired item (past expiry, not archived)
- -5 per dead reference
- -4 per broken link
- -2 per single-use tag (max -10)
- -3 per non-blessed tag (max -15)
- -2 if tag sprawl is in warning band (20-40%)
- -5 if tag sprawl is unhealthy (>40%)
- -1 per orphan item (max -10)
- -2 per hub item (max -10)

Floor at 0.

| Score | Health |
|---|---|
| 90-100 | Excellent, system is clean and usable |
| 70-89 | Good, minor structure issues, no urgency |
| 50-69 | Fair, accumulating debt, consolidation recommended |
| <50 | Poor, structure has broken, usability at risk |

### Step 7. Recommendations

Based on the analysis, list top 3 actions:
1. Most impactful (usually: fix tag sprawl, archive aged items, or split hub items)
2. Second
3. Third

Be specific. "Consolidate tags" is not an action. "merge 7 single-use tags into 3 categories" is.

### Step 8. Report

Present findings in this structure:

```
# Knowledge Base Health Report, {date}

## Summary
Overall Health: {score}/100 ({Excellent|Good|Fair|Poor})

## Inventory
Total Items: {N}
By Domain: {breakdown}
By Status: {breakdown}
By Type: {breakdown}

## Tag Health
Tag Sprawl: {X}% ({Healthy|Warning|Unhealthy})
Single-use tags: {count} ({list top 10})
Non-blessed tags: {count} ({list top 10})

## Link Health
Orphan Items (<3 links): {count}
  - Item 1 ({N} links)
  - Item 2 ({N} links)
Hub Items (>10 links): {count}
  - Item 1 ({N} links)
Broken Links: {count}

## Lifecycle Health
Aging Provisional Items (>30 days): {count}
  - Item 1 ({N} days, decision needed)
Critical Age (>60 days): {count}
  - Item 1 ({N} days, DECIDE NOW)

## Top Recommendations
1. [Specific, measurable action]
2. [Specific, measurable action]
3. [Specific, measurable action]
```

---

## Quick Reference

| Metric | Threshold | Implication |
|---|---|---|
| **Tag Sprawl** | >40% | Search becomes noise |
| **Orphan Items** | >20% of base | Discovery problem. Items are unfindable |
| **Hub Items** | Any | Probably needs splitting |
| **Broken Links** | >5 | Referential integrity broken |
| **Aging Provisional Items** | >30 days | Requires a decision call |
| **Critical Age** | >60 days | Resolve immediately |

---

## Epistemic Rules

- **Structure is orthogonal to accuracy.** A base can be mostly true and completely unusable. This skill measures usability, not truth.
- **Tags measure discoverability.** A tag used once is not a bug. It is a sign that search surface has fragmented.
- **Orphans are not wrong.** An item with no links is not bad in itself. It is unfindable except by exact recall, which is a discovery problem.
- **Hubs signal overload.** An item with 15 links is trying to be a table of contents. It needs splitting.
- **Provisional is not a permanent status.** If an item is marked emergent at creation, it should have a decision point, not drift forever.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "KB directory not found" | Path is wrong or KB does not exist | Ask for the correct path. If no KB exists, this skill does not apply |
| "Can't read metadata" | Item format is unknown | Ask what metadata format is in use. Each item should declare its metadata format |
| "High sprawl but most tags are intentional" | Taxonomy is wrong, not tags | Tags may be correctly specialized. This is when CUSTOMIZE.md matters. Adapt the threshold |
| "Lots of orphans but they are intentional" | KB uses a different discovery pattern | Some systems use full-text search instead of links. Adapt the orphan rule in CUSTOMIZE.md |

---

## Best Practices

- Run this after bulk ingestion of new content, and monthly as preventive maintenance.
- Do not run this on a knowledge base that has <10 items. The metrics are meaningless on tiny bases.
- Use the score as a trend. One month's score is a snapshot. Three months is a trajectory.
- Share the report with the team. Structure health is everyone's responsibility.

---

## Integration with Other Skills

- **`O8-dream`** runs deep consolidation. This flags what that skill should focus on.
- **`O6-weekly-review`** uses a lightweight version of this for weekly pulse checks.
- **`O9-ingest`** adds new items. This measures whether the accumulated items form a usable system.
- Together, ingest (add) → graph-health (check structure) → dream (prune) is the cycle.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section added, so the skill reads the profile section its CUSTOMIZE.md writes.
- **1.0.0 (2026-09-28):** Initial release. Structure health measurement across tag sprawl, link density, and provisional item age.
