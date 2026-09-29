---
name: context-os-setup
description: "Build a structured knowledge base for GTM intelligence. Two-layer architecture (atomic concepts + strategic documents) using semantic linking so facts are defined once and referenced everywhere. Turn scattered notes into compounding knowledge."
version: 1.0.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-28
tags: [knowledge-base, context-OS, GTM-intelligence, semantic-linking, documentation, operating-discipline, memory]
requires:
  skills: []
---

# Context OS Setup

## Overview

Builds a structured knowledge system where go-to-market intelligence is defined once and referenced everywhere. Two-layer architecture separates atomic concepts (customer archetypes, competitors, proof points) from strategic documents (positioning, launch plan, narratives) that compose them.

Every fact stored is a fact not re-derived. Every reference to that fact stays synchronized when the fact changes.

**Core Principle:** Define once, reference everywhere. Facts start to drift the moment two documents each hold their own copy.

---

## Why This Skill Exists

A founder runs discovery. They learn the customer profile. They write it in Notion. Launch planning reads the same notes and rewrites it in a different document. Growth analysis re-extracts the same customer archetype into a spreadsheet. Six months later, three versions of the customer exist. They do not agree. Which one is true?

Or discovery finds that "Competitor A charges $X per month." Positioning document cites it. Pricing model uses it. Competitive battlecard quotes it. Then Competitor A changes their pricing. Now updating it requires finding it in three places and hoping you did not miss one.

This skill prevents that drift by building a knowledge base where facts are stored atomically. The customer archetype exists once. Every piece of work that needs it links to that node, not a copy. When the archetype gets updated from new customer feedback, every document that references it reflects the update automatically.

Why this skill ranks above the four operating disciplines: They all read from and write to this foundation. Discovery without a foundation is research that evaporates. Positioning without one is a statement that drifts. Launch without one quotes numbers that were true in March. Engine without one re-derives the market every quarter.

---

## Role

You are a **knowledge architect**, not an archivist. Your job is to help the user build a structure where knowledge compounds, not accumulates. You design the layers and the connections, not catalog everything.

You are not satisfied by a "knowledge base" that is just a folder of files. You are satisfied by a system where facts are connected, definitions stay in sync, and the person working in month six knows exactly what was learned in month one.

---

## Input Contract

| Input | Required | Notes |
|-------|----------|-------|
| Purpose of the knowledge base (GTM, product, research, consulting) | Required | This determines the layer structure |
| Seed content (positioning docs, customer notes, competitor research, transcripts) | Required | A knowledge base built on zero content is a museum of empty rooms |
| Who uses this knowledge | Required | Are you the only user, or a team? Does this feed other systems? |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Directory structure (Layer 1 and Layer 2) | Yes | Where things live |
| Taxonomy of blessed tags | Yes | How to categorize knowledge |
| Ontology of relationships | Yes | How concepts connect |
| Documentation guide | Yes | How to add knowledge without breaking the system |
| First ingest completed | Yes | Proof the system works |

---

## Context

You read the folder structure. You assess existing scattered knowledge. You understand the team's workflow. You do not assume knowledge architecture is already in place.

---

## Quick Reference

| Element | Purpose | Example |
|---------|---------|---------|
| **Layer 1: Atomic Knowledge** | Individual concepts, reusable, with metadata | Customer profile, competitor deep-dive, value metric option, regulatory trigger |
| **Layer 2: Strategic Documents** | Documents that compose Layer 1 by reference, not by restating | Positioning statement, launch plan, narrative, competitive battlecard |
| **Taxonomy** | Blessed tags for categorization | segment-profile, competitor, value-driver, regulatory, proof-point |
| **Ontology** | Rules for how concepts relate | "CompetitorA competesFor SegmentB" or "RegulatoryChange affectsSegment X" |
| **Synthesis Nodes** | The 5% that answers 95% of questions | Quarterly growth plan, ICP summary, top 5 competitors |

---

## Epistemic Rules

- **One source of truth.** If a fact exists in two places and they conflict, trust is broken. Facts live once, are referenced everywhere.
- **Metadata matters.** A fact without a date, source, or confidence level is gossip. Every node needs: what, when, why, who learned it, confidence grade.
- **Synthesis docs are decision-makers.** Layer 1 is atomic. Layer 2 is actionable. A positioning statement should be two pages max. If it is 20, the reader will ignore it.
- **Tags are grown, not designed.** Start with 5-7 tags. Add tags as they become necessary. Do not pre-design a 50-tag taxonomy. It will not fit.
- **Breaking changes are announced.** If discovery learns something that changes the customer profile fundamentally, that change gets flagged. Not everyone gets surprised. The system broadcasts the update.

---

## Core Workflow

### Step 1. Assess the Current State

Does a knowledge base already exist? Is it connected or scattered?

Ask:
- What GTM documents do you have right now?
- Where are they (Notion, Google Drive, documents, scattered)?
- What is working and what is not?

If a knowledge base exists, offer to run a health check instead. If content exists, go to Step 1B. If starting from scratch, go to Step 1A.

### Step 2A. Blank Slate Setup

For a new knowledge base, ask:
- What is this base for? (GTM, product, research, consulting)
- What content do you have to seed it? (Even one positioning doc is enough)

Do not build on zero content. Seed with something real.

### Step 2B. Existing Content Setup

Map what exists. Ask which is the source of truth and which is derivative. Keep the source. Archive derivatives.

### Step 3. Create Directory Structure

Build two layers:

**Layer 1: Atomic Knowledge** (knowledge_base/)
- Each concept has one home
- Metadata on every node: date created, last updated, confidence, source
- Wiki-links to other nodes
- No duplication

**Layer 2: Strategic Documents** (00_foundation/)
- Positioning, messaging, launch plan, narratives
- These COMPOSE Layer 1 by reference, not by redefining
- When a Layer 1 fact changes, Layer 2 automatically reflects it

Example structure:

```
[project]/
├── knowledge_base/
│   ├── gtm/
│   │   ├── customer-archetype.md
│   │   ├── competitor-landscape.md
│   │   ├── value-drivers.md
│   │   └── regulatory-triggers.md
│   ├── competitors/
│   │   ├── competitor-a-profile.md
│   │   ├── competitor-b-profile.md
│   │   └── ...
│   └── methodology/
│       └── [your frameworks]
├── 00_foundation/
│   ├── positioning-statement.md
│   ├── launch-plan.md
│   ├── strategic-narrative.md
│   └── _synthesis/
│       └── [the 5% that answers 95%]
└── _system/
    └── knowledge_graph/
        ├── taxonomy.yaml
        └── ontology.yaml
```

### Step 4. Create Taxonomy

Start small. Five to seven tags. Examples:
- discovery (from research, not yet validated)
- validated (confirmed by customers)
- experiment (hypothesis, tested, result)
- proof-point (social proof, customer quote, metric)
- competitive (competitor intel)
- strategic (shapes GTM decisions)

Grow tags as needed. Do not pre-design a 50-tag taxonomy.

### Step 5. Create Ontology (Relationships)

Define how concepts connect. Examples:
- "CompetitorA competesFor SegmentB"
- "ValueDriver X affectsSegment Y"
- "RegulatoryChange Z requires UpdateToProduct W"

These relationships help you navigate when things change.

### Step 6. Seed With First Content

Take one piece of existing content (positioning doc, customer notes, competitive research). Transform it into the Layer 1 + Layer 2 structure.

Show the before/after. Let the user see how the system works.

### Step 7. Verify It Works

Ask the user to query the new knowledge. "Who are our competitors?" "What regulatory issues affect healthcare segment?" "What have we learned about pricing?"

The system should answer these without the user knowing where to look. If it does, the structure works.

---

## Examples

### Worked Example 1: Scattered Knowledge (Context OS Failure)

**Current state:** Positioning statement in Notion. Competitive analysis in a spreadsheet. Customer archetype in email notes. Meeting notes scattered across Slack and Google Drive.

**The problem:** When competitive landscape changes, where is it updated? Positioning reads old numbers. Launch plan quotes outdated info.

**Fix:** Layer 1 node: "Competitor A Profile" with date, source, confidence. Layer 2: Positioning statement links to that node. When the node updates, positioning automatically reflects the change.

### Worked Example 2: Synthesis Node That Makes Decisions (Context OS Success)

**Synthesis doc:** "ICP Summary", two pages, the most important facts about the customer. Name, role, company size, budget authority, decision criteria, typical sales cycle.

**Reality:** This gets read every week. Positioning uses it. Launch planning uses it. Sales deck pulls numbers from it. One document as the single source of truth.

**Update:** New quarter, discovery updates the ICP based on latest customer conversations. Every downstream work automatically reflects the change because they all link to this node.

**Outcome:** No surprise misalignments. All work stays synchronized.

### Worked Example 3: Ontology That Catches Changes (Context OS Success)

**Relationship:** "RegulatoryChange X (a new state telehealth licensing rule) requires UpdateToProductY (license checks for every provider who sees patients in that state)."

**When:** New regulatory news arrives, the system flags which products are affected, which customers need notification, which GTM documents need updating.

**Without ontology:** The update exists somewhere. Nobody connects the dots. A customer discovers the gap in April. The impact spreads for months.

**With ontology:** The connection is explicit. When the trigger is pulled, the system broadcasts the impact.

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| "The knowledge base is perfect but nobody uses it" | Structure is too complex or nodes are too long | Simplify. Shorten. Add the 5% that answers 95% as a synthesis layer. People will use it if it answers their question in one page. |
| "We are duplicating content across Layer 1 and Layer 2" | Semantic linking is not established | Layer 2 should NOT restate Layer 1. Layer 2 should reference: "See customer archetype for profile details." That is it. If Layer 2 is restating facts, the connection is broken. |
| "Nobody knows what tag to use" | Taxonomy is too large or undefined | Reduce to 3-5 core tags. Define each one in writing. Let tags grow organically. Do not pre-design. |
| "When facts change, nobody knows" | No breaking-change protocol | Add a process: if an atomic fact changes significantly, update it AND announce the change. Broadcast to the team. Otherwise updates are silent and dangerous. |

---

## Best Practices

- **Short nodes, dense synthesis.** Layer 1 nodes should be 300-500 words. Layer 2 synthesis docs should be 1-2 pages. If you cannot fit your knowledge in that space, you have not synthesized it yet.
- **Metadata on everything.** Every node needs: date created, last updated, source (where did this come from), confidence (high/medium/low/untested), owner (who maintains this).
- **Document the discipline.** Write a one-page guide on how to add knowledge. Make it simple enough that anyone on the team can do it without creating chaos.
- **Quarterly review.** Once a quarter, read the knowledge base. What is stale? What changed in the market that needs updating? Refresh before information debt accumulates.
- **Start small.** Do not try to catalog everything. Start with discovery findings + positioning + competitive landscape. Grow from there.

---

## Integration With Other Skills

- **`O15-gtm-discovery`** writes customer archetype, competitive landscape, assumptions to Layer 1
- **`O14-gtm-positioning`** writes positioning statement, messaging house to Layer 2. Reads customer + competitive from Layer 1
- **`O13-gtm-launch`** writes launch plan to Layer 2. Reads positioning, customer, competitive from Layer 1 and Layer 2
- **`O12-gtm-engine`** writes retrospectives, narratives, growth backlogs to Layer 2. Reads everything from Layer 1 to avoid re-deriving

All four read from this foundation. When it works, the system compounds. When it does not, each cycle rediscoveres the market.

---

## Changelog

- **1.0.0 (2026-09-28):** Initial release. Two-layer architecture (atomic + strategic), taxonomy and ontology, synthesis nodes, metadata requirements. Adapted from Jacob Dietle's GTM Context OS framework (https://taste.systems).
