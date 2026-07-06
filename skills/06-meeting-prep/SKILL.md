---
name: gtm-meeting-prep
description: "Prepares reps for discovery or demo calls by pulling CRM data, building pain hypotheses or ranking confirmed pains, structuring the call around discovery/demo frameworks, preparing methodology-aligned question banks, selecting social proof, scripting meeting open/close, and generating a single-page prep sheet"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [meeting-prep, discovery-prep, demo-prep, call-prep, discovery-questions, demo-framework, meeting-scripts, meddpicc, interrogate-the-problem]
requires:
  skills: []
---

# Meeting Prep

## Overview

Prepares a rep for an upcoming discovery or demo call. Pulls CRM data, analyzes interaction history, builds the call structure around your sales methodology, prepares question banks with follow-up sequences, selects persona-matched social proof, scripts meeting open and close, and generates a single-page prep sheet. Replaces 30-45 minutes of manual prep with structured, methodology-aligned intelligence.

**Core Principle:** Every meeting prep must be pain-first, methodology-aligned, and actionable within minutes. The prep sheet is designed to be referenced during the call — not read beforehand and forgotten.

**Meeting Types:**
- **Discovery** (`meeting_type = discovery`): Build pain hypotheses, prepare discovery question bank, pre-fill qualification framework, prepare competitive probes
- **Demo** (`meeting_type = demo`): Rank confirmed pains from discovery, map pains to product workflows, plan demo structure with engagement questions, prepare resistance handling

---

## Role

You are a **senior account executive and meeting-prep specialist for a vertical SaaS company** — not a generic assistant. You prepare reps for discovery and demo calls the way a top-performing enterprise seller would: pain-first, methodology-aligned, and specific to this account. Everything company-specific — the vertical, the personas, the competitors, the proof points — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | The account the meeting is with |
| Meeting type (`discovery` / `demo`) | ✅ Required | **The method forks on this.** If unclear from context, ask: "Is this a discovery call or a demo?" |
| Primary contact (name + title) | ✅ Required | Persona-matching drives questions and proof |
| Call date, time, duration | Optional | Used for call-flow timing |
| Known competitor | Optional | Sharpens competitive probes |
| Prior notes / attendees | Optional | Demo: attendee list strongly recommended |

**Prerequisite check (demo only):** if `meeting_type = demo`, verify discovery findings exist in CRM. If none found, recommend running discovery prep first — or build 5-10 minutes of targeted discovery into the demo opening.

---

## Output Contract

Every run produces a **single-page prep sheet with the same sections, in the same order** — the content changes per account; the structure never does. That is what makes it reviewable: a manager scanning fifteen prep sheets never has to relearn the layout.

Core commitments of every prep sheet: the **meeting objective**, the **question sequence** (SPIN discovery or Challenger-style demo), **competitive landmines**, **persona-matched proof points**, and **persona priorities** — organized into seven fixed sections (see *Artifact Generation* below for the discovery and demo layouts).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Framing, meeting scripts |
| Buyer Personas | Persona-matching questions and proof |
| Core Pain Points | Pain hypotheses (discovery) / pain ranking (demo) |
| Value Propositions | Differentiators and value framing |
| Proof Points | Social proof selection, Feel-Felt-Found stories |
| Competitive Landscape | Competitor probes and landmines |
| Sales Methodology | Which frameworks your team runs (overrides the defaults below) |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your playbook, in code. The frameworks below are the skill's defaults — **SPIN for discovery, Challenger-style structure for demos**. If `{Client Profile: Sales Methodology}` names different frameworks, those take precedence.

### Discovery: SPIN / Challenger Question Framework
| Phase | Goal |
|-------|------|
| **Situation** | Understand how they operate today: process, tools, team, volume |
| **Problem** | Surface financial, operational, and personal impact of current state |
| **Implication** | Understand cascading consequences and what they've tried |
| **Need-Payoff** | Use value framing to invite the buyer to articulate the benefit of solving |

### Discovery: Priority Path Follow-Ups
| Stage | Follow-Up |
|-------|-----------|
| **1. Identify** | "Can you walk me through what that actually looks like step by step?" |
| **2. Prioritize** | "On a scale of 1 to 10, how urgently does this need to change?" |
| **3. Quantify** | "How much time / money / risk does this represent per [period]?" |
| **4. Map Stakeholders** | "Who else does this impact? Whose responsibility is it to solve this?" |

### Demo: Demo Framework
| Element | Purpose | What Great Looks Like |
|---------|---------|----------------------|
| **Simple** | Easy to follow, one concept at a time | Prospect's language, no jargon, logical flow |
| **Highlight** | Stay in Winning Zone, open with #1 pain | 80%+ time on differentiating features |
| **Acute** | Demo ordered by pain severity | Most time on most important pain |
| **Relevant** | Persona-matched social proof | Feel-Felt-Found stories matching vertical and persona |
| **Engaging** | Prospect talks 50%+, questions throughout | What/how questions after every workflow |

### Demo: Interrogate the Problem — 4-Question Sequence
| # | Question | When | Purpose |
|---|----------|------|---------|
| 1 | **Prime Pain** — "Many teams struggle with [X]. To what extent is that true for you?" | Before showing the feature | Activates the pain |
| 2 | **Create Contrast** — "How does this compare to how you're handling it today?" | After showing the feature | Forces side-by-side comparison |
| 3 | **Requirements Check** — "Did I miss any requirements about [X] that are important?" | At transition between modules | Surfaces hidden needs |
| 4 | **Make the Buyer Say It** — "What excited you most about what you saw today?" | At the close | Captures buying reasons in their words |

### Meeting Structure (Both Types)
| Element | Purpose |
|---------|---------|
| **Pivot** | Transition into the meeting with context |
| **Logistics** | Confirm time, attendees, roles |
| **Agendas** | Set expectations, invite additions |
| **Next Steps** | Define what success looks like for this meeting |

### Qualification Framework (Discovery)
Default: MEDDPICC (Metrics, Economic Buyer, Decision Criteria, Decision Process, Paper Process, Identified Pain, Champion, Competition). Replace with your qualification framework if different.

### Demo Story Arc
Every demo follows a narrative arc: **[Problem Category 1] → [Problem Category 2] → [Business Impact]**

### Resistance Types (Demo)
| Type | Signal | Response Strategy |
|------|--------|------------------|
| **Reactance** | Feels pressured, defensive, one-word answers | Back off. Give autonomy. Use negative framing. |
| **Skepticism** | "Too good to be true," asks for proof, compares | Provide proof. Feel-Felt-Found. Data. References. |
| **Inertia** | "We've always done it this way," "Let's look later" | Quantify cost of inaction. Show what staying costs. |

---

## Quick Reference

**Use this skill when:**
- Preparing for a discovery call (first meeting, follow-up, re-engagement)
- Preparing for a demo (product demonstration after discovery)
- Need a single-page call prep sheet for during-call reference
- Rep needs methodology-aligned meeting structure

**Don't use when:**
- Need outbound sequences for cold accounts (use `gtm-account-snapshot`)
- Building competitive strategy for a deal (use `gtm-competitive-strategy`)
- Analyzing a call that already happened (use `gtm-call-coaching`)

**User roles:** AE (primary), BDR (discovery only)
**Expected time:** 15-25 minutes per account

---

## Core Workflow

### Step 0: Detect Meeting Type

Determine `meeting_type` from user input or context:

**Discovery indicators:** "discovery," "disco," "first meeting," "initial call," "re-engagement"
**Demo indicators:** "demo," "demonstration," "show them," "product walk-through"

If unclear, ask: "Is this a discovery call or a demo?"

**Prerequisite check (demo only):** If `meeting_type = demo`, verify discovery findings exist in CRM. If no discovery data found, recommend running discovery prep first or building 5-10 minutes of targeted discovery into the demo opening.

---

### Step 1: Gather Intelligence

#### 1a. Confirm Inputs
- Account name
- Primary contact name and title
- Call date and time
- Call duration (scheduled)
- Meeting type (discovery / demo)
- Other team members attending (if any)
- **Demo only:** Attendees (names, titles, roles in decision)

#### 1b. Search CRM
Pull everything available:
- Account record: industry/vertical, size, locations, states of operation
- Opportunity record: stage, amount, close date, owner, competitors
- Contact records: all known contacts, titles, engagement history
- Activity history: calls, emails, meetings — with dates and key notes
- AI summaries: deal intelligence, pulse signals
- **Discovery:** Previous discovery notes, documented pain points
- **Demo:** Discovery findings, confirmed pains, Priority Path results, MEDDPICC fields

#### 1c. Build Account Profile

| Field | Data |
|-------|------|
| Company | [Name] |
| Industry/Vertical | [Specific vertical] |
| Size | [Employees / Revenue / Branches] |
| States | [Where they operate] |
| Current Stage | [Deal stage] |
| Deal Amount | [If known] |
| Primary Contact | [Name, Title] |
| Additional Contacts | [Names, Titles] |
| Rep | [Rep name] |

---

### Step 2: Analyze Interaction History

#### 2a. Extract Key Findings
From CRM history, identify:
- **Pain points already mentioned** — Don't re-ask what they've already told you
- **Questions the prospect asked** — Reveals priorities and concerns
- **Objections or resistance raised** — What pushback has surfaced?
- **Stakeholders referenced** — Who else is involved or impacted?
- **Competitor mentions** — Current solution or vendor references?
- **Trigger events** — What prompted the initial engagement?

#### 2b. Identify Gaps
Flag what is NOT yet known — these become meeting objectives:
- Pains mentioned but not quantified
- Stakeholders referenced but not engaged
- Decision process not yet mapped
- Budget/timeline unknown
- Current solution details unclear

---

### Step 3: Build Pain Intelligence

**Branch by `meeting_type`:**

#### Discovery Mode: Generate Pain Hypotheses

Based on account profile, industry, and interaction history, build 3-5 ranked pain hypotheses using `{Client Profile: Core Pain Points}`.

For each hypothesis:
| Field | Content |
|-------|---------|
| **Pain Hypothesis** | Specific pain statement |
| **Pain Category** | Which of the core pain points |
| **Evidence** | Why you believe this — industry data, previous mentions, company signals |
| **Estimated Business Impact** | Time, money, or risk |
| **Urgency Indicators** | Why now — trigger event, fiscal year, growth |
| **Confidence** | HIGH (mentioned directly) / MEDIUM (industry-typical) / LOW (hypothesis only) |

**Ranking rule:** Lead with the highest-confidence hypothesis. Use medium/low confidence hypotheses as negative framing opportunities.

#### Demo Mode: Rank Confirmed Pains

From discovery findings, list every confirmed pain and rank by demo priority:
1. **Business impact** — Largest quantified impact first
2. **Product differentiation** — Pains where your product has strongest competitive advantage
3. **Attendee relevance** — Pains that matter to the people in the room

Assign time allocation:
| Priority | Pain | % of Demo Time |
|----------|------|---------------|
| #1 | [Highest priority] | 40-50% |
| #2 | [Second priority] | 25-35% |
| #3 | [Third, if time] | 15-20% |

**Rule:** The #1 ranked pain is the first thing shown. This is non-negotiable.

---

### Step 4: Prepare Question Bank

**Branch by `meeting_type`:**

#### Discovery Mode: Discovery Question Bank

Build tailored questions for each discovery phase connected to pain hypotheses:

**Situation (4-6 questions):** Process, tools, team, volume. What to listen for: manual vs. automated, team size, tech stack gaps.

**Problem (4-6 questions):** Financial, operational, personal impact of current state. Tied to each pain hypothesis.

**Implication (3-4 questions):** What they've tried, past evaluations, why previous attempts failed.

**Need-Payoff (2-3 questions):** Value framing for medium/low confidence hypotheses. Example: "Most [teams] at companies your size tell us they spend 15+ minutes per [task]. That's probably not your experience though, right?"

**Priority Path Follow-Ups:** Prepare the 4-stage follow-up sequence from `{Methodology: Priority Path}` for when a prospect confirms a pain. Rule: Do not move past a confirmed pain without running Priority Path through at least Stages 1-2.

#### Demo Mode: Interrogate the Problem Questions

For each demo module (mapped to a pain), prepare the 4-question sequence from `{Methodology: Interrogate the Problem}`:

| Question | Script | What to Capture |
|----------|--------|----------------|
| Q1: Prime Pain | "[Tailored to specific pain and vertical]" | Specific examples, who's affected |
| Q2: Create Contrast | "How does this compare to how you're handling it today?" | Their exact words — champion script material |
| Q3: Requirements Check | "Did I miss any requirements about [topic] that are important?" | Hidden needs, integration requirements |
| Q4: Make the Buyer Say It | Asked at close, not per module | Buying reasons in their words |

**TED Follow-Up Probes** (for vague answers): Tell me, Explain to me, Describe to me — don't accept the first answer.

---

### Step 5: Framework Pre-Fill / Demo Structure

**Branch by `meeting_type`:**

#### Discovery Mode: Qualification Framework Pre-Fill

For each element of `{Methodology: Qualification Framework}`, document what is already known vs. must be uncovered:

- **Metrics:** Known quantifications + benchmarks to reference
- **Economic Buyer:** Identified? Budget range? Approval process?
- **Decision Criteria:** Must-haves, deal killers, evaluation criteria
- **Decision Process:** Buying committee, timeline, IT/legal involvement
- **Identified Pain:** Confirmed pains + depth target (at least 1 at Level 3)
- **Champion:** Who shows champion behaviors? Development questions

#### Demo Mode: Pain-to-Workflow Map + Demo Structure

Map each pain to a specific product workflow:
| Pain | Workflow to Show | Differentiating Feature | What Makes It Compelling |
|------|-----------------|----------------------|------------------------|
| [Pain #1] | [Specific workflow] | [Key capability] | [Proof point or metric] |

Plan the demo structure following `{Methodology: Demo Framework}`:
1. Meeting Open (3-5 min)
2. Problem Slide (2-3 min) — Follow `{Methodology: Demo Story Arc}`
3. Pain #1 Demo (40-50% of time) — ITP Q1 → Show → Q2 → Listen → Q3
4. Pain #2 Demo (25-35%) — Same structure
5. Pain #3 Demo (15-20%, if time)
6. Recap + Close (3-5 min) — ITP Q4 → Meeting close

**Five Implementation Habits Check (Demo):**
1. Open with Problem Slide
2. Ask Prime Pain before every module
3. Ask for Comparison after showing value, then PAUSE
4. Use Requirements Check at every transition
5. End with "What excited you most?" then recommend next steps

---

### Step 6: Prepare Competitive Intelligence

#### 6a. Identify Current Solution
From CRM and interaction history:
- Current solution (if known)
- Evidence for how we know
- Contract status
- Satisfaction level

#### 6b. Competitor-Specific Probes
Load probes from `{Client Profile: Competitive Landscape}` matched to the identified incumbent.

#### 6c. Product Differentiators
Based on likely competitor, prepare 2-3 key advantages from `{Client Profile: Value Propositions}` with matched proof points.

---

### Step 7: Select Social Proof & Prepare Resistance

#### 7a. Social Proof Selection
Select 2-3 customer stories from `{Client Profile: Proof Points}` matching on: vertical, company size, pain type, and persona of primary contact.

#### 7b. Feel-Felt-Found Stories
Script 2-3 stories ready to deploy:
- **Feel:** Validate their specific concern
- **Felt:** Peer normalization with similar customer
- **Found:** Specific outcome with metric

#### 7c. Resistance Preparation (Demo Mode)
Using `{Methodology: Resistance Types}`, anticipate likely resistance and prepare typed responses:
- **Reactance** → Back off, give autonomy
- **Skepticism** → Provide proof, Feel-Felt-Found
- **Inertia** → Quantify cost of inaction

**Demo: Winning Zone Redirection Scripts** — If prospect asks about a Losing Zone feature: Acknowledge → Redirect to Winning Zone → Reframe around their #1 pain.

**Demo: Buying Signals to Watch For** — Implementation questions, pricing questions, internal selling ("My CFO would love this"), comparison to current state, volume/scale questions, timeline questions.

---

### Step 8: Script Meeting Open and Close

Build customized scripts using `{Methodology: Meeting Structure}`:

#### Discovery Opening
- **Pivot:** Reference why they're meeting (if first: "learn more about your process"; if follow-up: reference specific pain from prior interaction)
- **Logistics:** Confirm duration, attendees
- **Agendas:** Set expectations: learn about current process, understand pain points, determine fit
- **Next Steps:** Define success: "clear sense of whether it's worth scheduling a [next step]"

#### Demo Opening
- **Pivot:** Reference discovery findings: "[Contact], in our last conversation you mentioned [Pain #1 — their exact words]"
- **Logistics:** Confirm duration, welcome new attendees, ask about their role
- **Agendas:** Set demo agenda based on their confirmed pains
- **Next Steps:** Define success: "we'll both know whether it makes sense to [next stage]"

#### Closing Script (Both Types)
- **Pivot:** Transition to next steps
- **Logistics:** Who else should be in the room? Calendar availability?
- **Agendas:** Recommend next meeting agenda based on what was discussed
- **Next Steps:** Define next milestone

---

### Step 9: Build Game Plan

#### 9a. Meeting Objectives

**Discovery Primary Objectives:**
1. Validate or disprove top 2-3 pain hypotheses
2. Run Priority Path on at least 1 confirmed pain (through Stage 3)
3. Identify the economic buyer and decision process
4. Secure a next step with specific date, attendees, and agenda

**Demo Primary Objectives:**
1. Show product solving #1 and #2 pains with clear contrast to current state
2. Capture at least 2 buying reasons in prospect's own words (ITP Q4)
3. Secure a next step with specific date, attendees, and decision point

**Minimum Acceptable Outcome:**
- Discovery: At least 1 validated, quantified pain + a scheduled next step
- Demo: Prospect confirms product addresses top pain + agrees to a next step

#### 9b. Call Flow & Timing

**Discovery:**
| Block | Duration | Activity | Framework |
|-------|----------|----------|-----------|
| Opening | 3-5 min | Meeting open | Meeting Structure |
| Current State | 8-10 min | Situation questions | Discovery (S) |
| Pain Discovery | 10-12 min | Problem + Need-Payoff; Priority Path | Discovery (P, N) + Priority Path |
| Alternatives | 3-5 min | What they've tried, vendor experience | Discovery (I) |
| Value Connection | 3-5 min | Feel-Felt-Found story | Social Proof |
| Close | 3-5 min | Meeting close | Meeting Structure |

**Talk-Time Target (Discovery):** Rep 30% / Prospect 70%

**Demo:**
| Block | Duration | Activity | Framework |
|-------|----------|----------|-----------|
| Opening | 3-5 min | Meeting open | Meeting Structure |
| Problem Slide | 2-3 min | Story Arc | ITP |
| Pain #1 Demo | 12-15 min | Prime Pain → Show → Contrast → Listen → Requirements | Demo Framework + ITP |
| Pain #2 Demo | 7-10 min | Same structure | Demo Framework + ITP |
| Pain #3 Demo | 4-6 min | Prime Pain → Show → Contrast | Demo Framework |
| Close | 3-5 min | "What excited you most?" → Meeting close | ITP Q4 + Meeting Structure |

**Talk-Time Target (Demo):** Rep <50% / Prospect 50%+

#### 9c. If-Then Scenarios

Prepare 5-8 if-then scenarios specific to the meeting type:

**Discovery scenarios:** Prospect confirms hypothesis → run Priority Path. Prospect denies all → deploy negative framing. Prospect asks for pricing → defer. Prospect says "send me info" → redirect. Prospect mentions competitor → probe satisfaction. EB not on call → ask for intro. Prospect seems guarded → diagnose resistance type.

**Demo scenarios:** Prospect asks about Losing Zone feature → acknowledge + redirect. New attendee arrives → Meeting Structure Logistics intro. Prospect goes quiet → pause + ask what they're thinking. Prospect challenges a claim → Feel-Felt-Found or data. Demo glitches → stay calm, backup ready. Prospect clearly ready to buy → stop demoing, move to close. New pains surface → pause, run quick discovery, capture, pivot.

#### 9d. Team Roles (If Applicable)
If other team members are attending, define role expectations for each person.

---

### Step 10: Summary Report

1. **Meeting Type**: Discovery / Demo
2. **Account**: Name, segment, vertical, size
3. **Call Date/Time**: Scheduled
4. **Primary Contact**: Name, Title
5. **Deal Stage**: Current stage, amount
6. **CRM Status**: Existing contacts, interaction history
7. **Discovery:** Top 3 pain hypotheses ranked | **Demo:** Top 3 confirmed pains ranked
8. **Competitive Context**: Known incumbent + approach
9. **Meeting Objectives**: Primary + minimum acceptable
10. **Prep Sheet Generated**: Yes/No + format

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_[Discovery|Demo]_Prep.md`
- **Option B: HTML** — Styled prep sheet with color-coded sections
- **Option C: PDF** — Python + reportlab, single page, letter size, two-column layout

### Prep Sheet Sections

**Discovery Prep (7 Sections):**
1. **Call Header** — Account, contact, date, objectives
2. **Pain Hypotheses** — Ranked with evidence and confidence
3. **Discovery Question Bank** — Top 3 questions per phase + Priority Path
4. **Qualification Gaps** — Traffic-light grid: known (green), partial (yellow), unknown (red)
5. **Competitive Positioning** — Current solution, probes, differentiators
6. **Meeting Scripts** — Opening + closing customized
7. **Call Flow & Timing** — Time-blocked agenda with top if-then scenarios

**Demo Prep (7 Sections):**
1. **Demo Header** — Account, attendees, pains, objectives
2. **Pain-to-Workflow Map** — Winning Zone plan with time allocation
3. **Demo Script** — Time-blocked structure with framework labels
4. **Interrogate the Problem Questions** — Per-module question cards
5. **Social Proof & Feel-Felt-Found** — Pre-scripted stories matched to attendees
6. **Meeting Scripts** — Opening + closing customized with discovery pains
7. **Resistance Playbook & If-Then Scenarios** — Typed objections with responses

---

## Examples

### Example 1: Discovery Prep — Enterprise Account

**Context:** AE prepping for first discovery call with a large enterprise prospect.

**Input:** "Prep me for the discovery call with [Enterprise Account] on Thursday."

**Process:** `meeting_type = discovery`. CRM shows existing account, no active deal. Company research: $8B+ revenue, PE-backed, 400+ locations across 40+ states. 3 contacts found (CFO, VP Operations, Operations Manager). Top pain hypothesis: fragmented processes across 400+ branches after PE rollup (Pain #5, HIGH confidence — PE rollup is documented).

**Output:** Full discovery prep with ranked pain hypotheses, discovery questions tailored to multi-branch complexity, MEDDPICC pre-fill showing gaps (EB unknown, decision process unknown), competitive probes (incumbent unknown — open probing), meeting scripts referencing PE consolidation, game plan with if-then scenarios. 7-section prep sheet generated.

### Example 2: Demo Prep — Competitive Displacement

**Context:** AE prepping for demo after successful discovery with a mid-market account.

**Input:** "Prep me for the demo with [Account] on Friday — attendees are the VP of Operations and Operations Manager."

**Process:** `meeting_type = demo`. CRM shows active deal at Demo stage, $180K. Discovery notes confirm: Pain #1 = manual processing (10-15 min each, 800/month), Pain #2 = inconsistent branch processes (22 locations, each does it differently), Pain #3 = incumbent service decline. VP Operations is champion candidate. Confirmed pains ranked by impact → demo plan built around process automation first (40%), standardization second (35%), visibility third (25%).

**Output:** Full demo prep with pain-to-workflow map, demo structure, Interrogate the Problem questions per module, Feel-Felt-Found stories from similar customers, meeting scripts referencing discovery pains verbatim, resistance prep (anticipate Inertia from long-term incumbent relationship), buying signals watch list. 7-section prep sheet generated.

### Example 3: Quick Call Prep — Inbound Discovery

**Context:** AE needs fast prep — prospect called in and discovery is in 15 minutes.

**Input:** "Quick call prep for [Account] — they called in."

**Process:** `meeting_type = discovery`. Quick Call Prep pattern activated — skip artifact generation, deliver Steps 1-4 + Step 8-9 (account profile, pain hypotheses, top discovery questions, meeting scripts, game plan) in abbreviated format.

**Output:** Abbreviated discovery prep with top 3 pain hypotheses, 5 best discovery questions, meeting opener, and 3 key if-then scenarios. No prep sheet — speed over completeness.

---

## Common Patterns

### Pattern: Quick Call Prep
**When:** User says "quick prep" or "calling in 5 minutes."
**Approach:** Skip artifact generation (Step 10 output). Deliver Steps 1-4 + Steps 8-9 only. Speed over completeness.

### Pattern: Discovery-to-Demo Handoff
**When:** User ran discovery prep previously, now requesting demo prep for the same account.
**Approach:** Pull discovery findings from CRM (populated from the discovery call). Auto-rank confirmed pains. Flag any discovery gaps that need to be addressed in the demo opening.

### Pattern: Re-Engagement Discovery
**When:** Account went cold for 3+ months and is re-engaging.
**Approach:** Discovery mode with emphasis on Step 2 (interaction history) — surface what was discussed before. Pain hypotheses include "what's changed since we last spoke" angle. Meeting open references the previous conversation.

### Pattern: Multi-Attendee Demo
**When:** 3+ attendees confirmed with different roles.
**Approach:** Map each attendee to a persona from `{Client Profile: Buyer Personas}`. Prepare persona-specific social proof for each. Adjust demo timing to allocate Q&A moments for each attendee. Anticipate different resistance types per attendee.

---

## Troubleshooting

### "No CRM data available for this account"
**Solution:** Proceed with web research only. Note "No existing CRM record" in the output. For discovery, build hypotheses from industry data and company profile. For demo, this should not happen — recommend running discovery first.

### "Discovery was shallow — not enough confirmed pains for demo"
**Solution:** Flag in the discovery completeness check. Recommend two approaches: (a) run a brief discovery re-engagement before the demo, or (b) build 5-10 minutes of targeted discovery questioning into the demo opening to fill gaps.

### "Meeting type is unclear — could be either"
**Solution:** Ask the user. If they say "it's a bit of both," default to discovery mode but include a brief product overview section. This is common for follow-up meetings where discovery is ongoing.

### "Prospect has been through multiple discovery calls"
**Solution:** Focus on what's NEW. Pull all previous interaction history (Step 2) and identify the gap between what's been discussed and what's needed. The prep should advance the deal, not repeat previous conversations.

---

## Best Practices

### Do's
- **Customize meeting scripts** — Reference specific pains, contact names, and meeting context
- **Match social proof to attendees** — A CFO doesn't care about the same proof points as an Operations Manager
- **Prepare for resistance before it happens** — Type it correctly (Reactance/Skepticism/Inertia) for the right response
- **Keep talk-time targets visible** — Discovery: 30/70. Demo: <50/50+. This is the single biggest coaching metric.

### Don'ts
- **Don't re-ask what was already answered** — Review interaction history before building questions
- **Don't show features without naming the pain first** — Every demo module starts with Prime Pain
- **Don't skip the meeting close** — Every meeting must end with a specific next step (date, attendees, agenda)
- **Don't use generic scripts** — Every meeting script must reference this specific account's context

### Quality Checklist — Discovery
- [ ] Pain hypotheses mapped to `{Client Profile: Core Pain Points}` (not generic)
- [ ] Discovery questions tailored to this account's vertical and size
- [ ] Priority Path follow-ups prepared for confirmed pains
- [ ] Negative framing questions ready for medium/low confidence hypotheses
- [ ] Qualification gaps identified with specific questions to fill them
- [ ] Meeting scripts customized (not template copy-paste)
- [ ] Call flow adds up to scheduled duration
- [ ] Talk-time target: 30/70

### Quality Checklist — Demo
- [ ] Discovery completeness verified (2+ confirmed pains, 1+ quantified)
- [ ] Pains ranked by impact + differentiation + attendee relevance
- [ ] Time allocation proportional to pain priority (#1 gets 40-50%)
- [ ] Interrogate the Problem questions scripted per module (not generic)
- [ ] Social proof matches attendee personas, vertical, and scale
- [ ] Feel-Felt-Found stories pre-scripted and ready to deploy
- [ ] Resistance anticipated and typed correctly
- [ ] Five Implementation Habits checked
- [ ] Meeting scripts reference discovery pains
- [ ] Talk-time target: <50/50+

---

## Integration with Other Skills

- **`gtm-account-snapshot`** — Run snapshot first for unknown accounts, then meeting prep for scheduled calls.
- **`gtm-call-coaching`** — After the meeting, run call coaching to grade methodology adherence and extract coaching insights.
- **`gtm-competitive-strategy`** — When competitive intelligence is critical, run competitive strategy for deeper battlecard before meeting prep.
- **`gtm-stakeholder-mapping`** — When multi-attendee dynamics are complex, run stakeholder mapping to understand the buying committee.
- **`gtm-deal-pulse`** — After the meeting, update deal health with new signal data captured during the call.
- **`gtm-meddpicc-analysis`** — After discovery, run MEDDPICC analysis for a comprehensive deal qualification assessment.

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (SPIN, Priority Path, Demo Framework, Interrogate the Problem, Meeting Structure, Resistance Types) moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release — merged from discovery prep and demo prep skills
- Unified via `meeting_type` parameter (discovery / demo)
- Generalized via Client Profile block with configurable defaults
- Preserved discovery framework, Priority Path, demo framework, Interrogate the Problem, meeting structure, and MEDDPICC frameworks as defaults
- Preserved Feel-Felt-Found social proof pattern
- Preserved resistance typing (Reactance/Skepticism/Inertia)
- Preserved Five Implementation Habits check (demo)
- Multi-format artifact generation replacing reportlab-only
