---
name: gtm-ingest
description: "Transforms raw content (transcripts, documents, calls, notes) into structured knowledge items with metadata, two-tier truth/timeline structure, and wiki-links for discovery"
version: 1.0.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-28
tags: [ingest, capture, knowledge-base, structure, content-processing, operating-discipline]
requires:
  skills: []
---

# Ingest

## Overview

Turns raw content, transcripts, documents, call notes, meeting records, decisions, into structured knowledge items that are findable, updatable, and connected.

The ingest habit is where the pile of notes becomes a system. Raw transcripts are not searchable. Structured items are. A loose collection of observations cannot tell you what changed. A timeline of dated observations can. The conversion is unglamorous and nobody schedules it, which is why the pile grows and why every new hire rediscovers what the company learned years ago.

**Core Principle:** Capture beats recall. If it is not structured enough to retrieve, it is not captured.

---

## Why This Skill Exists

Organizations lose knowledge constantly. A customer calls with a question, and the answer exists in a transcript from March, but nobody has time to search every transcript since. So the team rebuilds the answer, the customer waits, and the rebuilding becomes the norm.

The skill exists because of a specific pattern. Information arrives, a call transcript, a decision meeting, a research document, notes from a conversation. The person who receives it reads it and absorbs it. But they do not have time to convert it into something others can find. So it sits in their inbox, or gets filed with a vague name, or stays only in their head. When they leave, it evaporates.

The conversion is the skill. What makes the conversion valuable is two mechanisms. First, every item has two permanent zones, compiled truth at the top (the current best understanding, rewritten as understanding changes) and a timeline at the bottom (append-only, dated, every interaction in order, exact quotes never paraphrased). When the team re-reads something six months later and finds they were wrong, the top gets rewritten and a new entry goes in the timeline. The record of how you got there stays intact. The top can be wrong and fixed. The bottom is the audit trail.

Second, when an ingested item is about a person, the skill checks whether one already exists, and if it does, appends a timeline entry instead of starting a duplicate. One person, one record, every interaction in order. It sounds trivial until you picture a team holding four half-notes about the same customer, written by people who did not know the others existed, and a new rep reading one and walking into a call missing the other three.

---

## Role

You are a **knowledge architect**, not a transcriptionist. Your job is to extract meaning, structure it so it can be found, and connect it to what is already known.

---

## Input Contract

**If required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Raw content | Required | Transcript, document, call notes, or pasted text |
| Content type | Required | Is this a call / meeting / document / notes / decision? |
| Item taxonomy | Required | Domain / type / status values for your system |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Items created | Yes | Count and names of new items |
| Items updated | Yes | Any existing items that received new timeline entries |
| Key concepts extracted | Yes | What atomic ideas are present in this content |
| Relationships identified | Yes | How new items connect to existing ones |
| Warnings | Yes | Any metadata not in taxonomy, any person mentioned without a dedicated page |

---

## Core Workflow

### Step 1. Analyze Content Type

Determine what has arrived:
- **Transcript** → Extract decisions, action items, concepts, quotes, objections, commitments
- **Document** → Extract thesis, key points, frameworks, relationships, evidence
- **Notes** → Extract ideas, questions, insights, TODOs, patterns
- **Sales call** → Extract objections, commitments, pain points, coaching moments
- **Meeting** → Extract decisions, action items, behavioral patterns, commitments

### Step 2. Identify Concepts

Ask: what atomic ideas are present in this content?
- What domain? (technical / business / methodology / gtm / other)
- What relationships exist between them?
- Which concepts are new to the system, and which overlap existing items?

Be conservative. One clear concept per item beats ten vague ones.

### Step 3. Check for Existing Items

Before creating a new item:
- Search existing KB for items on this concept
- If one exists with the same subject, append a timeline entry instead of creating a duplicate
- If one exists but in a different context (same topic, different angle), mark as "related concept"

**Special rule for person entities:** Every person gets one record. If the person already has an item, append a timeline entry. One person, one record, every interaction in order.

### Step 4. Create or Update Knowledge Item

For each new concept, generate a knowledge item:

**Template:**

```yaml
---
name: CONCEPT_NAME_IN_CAPS
description: One sentence description
domain: technical|business|methodology|gtm|other
node_type: concept|pattern|case-study|framework|decision|person
status: emergent|validated|canonical
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags:
  - [domain]
  - [relevant tags from taxonomy]
related_concepts:
  - "[[related-item-1]]"
  - "[[related-item-2]]"
source:
  type: transcript|document|notes|call|meeting
  date: YYYY-MM-DD
  reference: [where this came from, if citable]
---

# Concept Name

## Compiled Truth

[2-3 paragraph explanation of the current best understanding.
Rewrite this section when evidence changes.]

### Key Points
- Point 1
- Point 2
- Point 3

## Timeline

[Append-only, reverse chronological order. Only add, never edit existing entries.]

### YYYY-MM-DD. [Source event]
- What was learned
- Exact quote (if applicable)
- Source attribution
```

**Compiled truth rule:** Facts and synthesis go here. Rewrite this section as understanding evolves.

**Timeline rule:** Dated observations, exact quotes, evidence, timestamps. Append only. Never edit.

### Step 5. Establish Connections

For each new item, identify [[wiki-links]] to existing items:
- Related concepts
- Blocking concepts
- Examples or evidence of the concept

Aim for 2-5 connections per item. An item with zero connections is an orphan.

### Step 6. Check Metadata

Before saving:
- All required frontmatter fields present and correct
- Tags align with system taxonomy (warn if creating new tags)
- Status is appropriate (usually starts as `emergent`)
- Source is attributed

### Step 7. Save and Report

Save the item(s) to the correct location.

Report:
- Number of items created and their names
- Number of existing items updated (timeline entries added)
- New relationships discovered
- Any new tags not in taxonomy

---

## Quick Reference

| Input Type | How to Extract | Key Output |
|---|---|---|
| **Transcript** | Re-read, mark decisions and direct quotes | Decisions made, patterns, commitments |
| **Document** | Identify thesis + supporting points | Frameworks, evidence, core claims |
| **Notes** | Sort by idea, ignore editorial | Observations, questions, hypotheses |
| **Call** | What changed about what we believe? | Buyer behavior, objections, shifts |
| **Meeting** | What was decided? Why? By whom? | Decisions, action ownership, rationale |

---

## Epistemic Rules

- **Capture beats interpretation.** If unsure whether something is important, capture it. Status `emergent` lets it stay until proven.
- **Exact quotes are evidence.** Paraphrase only for synthesis. Preserve originals in timeline.
- **One person, one record.** Every interaction goes to their timeline, never a new half-note.
- **Connected items matter.** An orphan item is unfindable except by accident. Every item should have 2+ connections.
- **Compiled truth is mutable.** Timelines are immutable. Top can be wrong. Bottom is the audit trail.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "This feels like 10 concepts, not 1" | Content is too broad | Split it. One concept per item. |
| "I don't know if this is important yet" | You are overthinking it | Mark as `emergent` and ingest it. Status changes later. |
| "There's already an item about this" | Check if it is the same concept or a different angle | Same? Add timeline entry. Different? Create new item + link them. |
| "I can't extract atomic concepts" | The source content is too scattered | Ask for clarification or wait for a clearer source. Garbage in = garbage out. |

---

## Best Practices

- Ingest while the content is fresh, not weeks later from memory.
- If the source is a person's words (transcript, notes), preserve exact quotes.
- Tag conservatively. Better to under-tag than to fragment the search space.
- Connect to existing items. Isolated items are useless.
- When in doubt about importance, ingest it. You can archive it later.

---

## Integration with Other Skills

- **`O7-graph-health`** measures whether ingested items form a usable system.
- **`O8-dream`** consolidates items ingested over time.
- **`O6-weekly-review`** tracks whether ingestion is keeping up.
- Together, ingest (add) → graph-health (diagnose) → dream (consolidate) is the cycle.

---

## Changelog

- **1.0.0 (2026-09-28):** Initial release. Compiled-truth/timeline structure, person-entity deduplication, metadata validation, and relationship discovery.
