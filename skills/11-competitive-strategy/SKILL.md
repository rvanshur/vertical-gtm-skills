---
name: gtm-competitive-strategy
version: 2.0.0
description: "Builds a deal-specific competitive strategy for one open opportunity: the incumbent filed under a shared type, a gap matrix, a displacement playbook and a win plan with a battlecard. The AE who owns the deal runs it, and the sales manager reviews the output."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-20
tags: [competitive-strategy, battlecard, competitive-analysis, win-plan, competitive-positioning, incumbent-classification, compete]
requires:
  skills: [gtm-meddpicc-analysis]
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. The incumbent is filed under one of the seven shared incumbent types, failure patterns and trends are read from the profile's Competitive Patterns and Trends section with their counts and dated sources, and each proof point carries a Status that decides where it may appear. The three old evidence grades become the six shared tags, the two Epistemic Rules sections become one, jurisdiction deadlines must cite their rule and the date checked, and the HTML and PDF card options are removed. The Stonemark example is rebuilt on the chain fact that no buyer preference has been stated, and every example ends with a hand-off block."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on the PlotIQ example company, with a non-success example added and the example arithmetic corrected."
---

# Competitive Strategy

## Overview

Deal-specific competitive strategy for one open opportunity against an incumbent or a rival. It files the incumbent under one of the seven incumbent types, scores the threat, builds a competitive gap matrix, writes a displacement playbook with gap-exposing discovery questions, objection handling and talk tracks, and assembles a win plan with a battlecard. Unlike Competitive Displacement (12), which prospects outbound, this skill is for the AE who owns an active deal.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Win on the gaps the buyer cares about, with proof that is Verified, and never by trashing the competitor.

---

## Why This Skill Exists

Reps lose active deals to incumbents they never characterized. Some attack the competitor, which implies parity and makes the buyer defend the incumbent. Others repeat a gap the buyer can disprove with one question, such as a claim that a rival cannot do something it already does. Both failures start in the same place: the battlecard was written from memory and folklore, not from evidence. Nothing in the deal says which gap matters to this buyer, so the rep pitches the features that are easiest to demonstrate.

This skill makes the battlecard a checked document. The incumbent is filed under one of seven shared types, so the same competitor reads the same way across deals. Every claim carries a tag and every proof point carries its Status, and only Verified proof reaches a talk track. The gap matrix is built around what this buyer has said on the calls, so the win plan starts from the buyer's own criteria.

---

## Role

You are a competitive strategist for one open deal. You profile the incumbent or rival, map the gaps this buyer has actually named, and write a win plan the AE can run. Everything company-specific (the competitors, the proof points, the patterns and trends, the zones) comes from the client profile (see **Context**), so the same skill serves any market without changes.

You refuse four things. You do not put a proof point that is not Verified into a talk track, a battlecard line the rep reads aloud, or an email. You do not trash a competitor, because that implies parity and gives the buyer a reason to defend the incumbent. You do not call a failure pattern a pattern below five cases. You do not send anything, write to the CRM or enroll a contact. The reasons sit in **Hard Rules**.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The account with an open opportunity. Its status is one of TARGET, INBOUND, ACTIVE (with its stage number), LOST or OUT. An account pending AE assignment is not ACTIVE, and the output says it is pending |
| Competitor or incumbent | Required | The incumbent or rival by name. If it is unknown, the skill stops and runs discovery first (see Common Patterns, Unknown Incumbent) |
| Deal stage and amount | Optional | Read from the CRM when there is one. Stage names come from the profile's Qualification Stage Gates |
| How the incumbent was identified | Optional | CRM notes, a discovery call, a job posting. Each one is tagged |
| Satisfaction, contract status and renewal date | Optional | Frustrated, Neutral, Satisfied or Unknown. Active, expiring, month-to-month or Unknown, with the renewal date when one is known |
| Primary contact (name and title) | Optional | Persona matching drives the positioning |
| Prospect feedback and competitor intelligence | Optional | Each item with its source. Unsourced intelligence is treated as a claim, not a fact |

---

## Output Contract

Every run returns the battlecard in the chat, in its eight sections. It writes a file only when the user asks for one.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `incumbent_type` | Battlecard section 1, first line | One of the seven incumbent types in the Shared Contract, with the competitor's name and its evidence tag. A competitor that fits no type is filed under the nearest one, and the reason is written |
| `threat_level` | Battlecard section 1 | HIGH, MEDIUM or LOW, with the five factors and their average shown beside it |
| `gap_matrix` | Battlecard section 2 | One row per capability: the incumbent's status, our status, why it matters for this buyer, and the tag on each claim |
| `battlecard` | The full reply, in the chat | Eight sections in this order: account and incumbent summary, competitive gap matrix, winning zone strategy with landmines, discovery questions, displacement talk tracks, objection handling, proof points and reference stories, win plan checklist |
| `win_plan` | Battlecard section 8 | The checklist by stage (pre-meeting, discovery, demo, post-meeting), each item with an owner and a date where one is known |
| `report_path` | Last line of the battlecard | `none (inline)` unless a file was written |
| `next_action` | Last line of the battlecard | One step, with its owner and a date. Wrap-Up reads this line |
| File, on request | `<account>_gtm-competitive-strategy_<date>.md`, beside the user's account notes | Written only when the user asks, in Markdown. The ask is the approval step |

---

## Context

This skill does not carry client-specific information. It reads the client profile at [`profiles/client-profile.md`](../../profiles/client-profile.md). Throughout this skill, `{Client Profile: X}` means section X of that file.

| Profile section | Used for |
|---|---|
| Company | Account framing and vertical context |
| Buyer Personas | Persona-specific positioning and objection handling |
| Competitive Landscape | The competitor rows (type, pitch, advantage, weakness, pain reported after 6 to 12 months and the proof that answers it) and the Competitive Discovery Questions |
| Competitive Patterns and Trends | Failure patterns, each with its cases counted and source, the trend rows, each with its dated source, the Status of each proof point, and any jurisdiction deadline. Written by the interview in CUSTOMIZE.md |
| Value Propositions | Differentiation matrix and positioning statements |
| Proof Points | Displacement stories, each with its Status |
| Qualification Criteria | Buying triggers and disqualifiers |
| Qualification Zones | Zone alignment in Step 3a |
| Sales Methodology | Overrides framework defaults, including the stage names from the Qualification Stage Gates |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the defaults in Methodology, and marks every output that depended on the missing section.

### The Shared Contract

Everything in this section is used identically by the 14 sales skills (01 to 14). The names below are copied exactly, so the 14 never drift from each other.

#### The Profile Is the Only Source of Company Facts

Every company fact (ICPs, personas, pains, value propositions, proof points, competitors, triggers, zones, stage names, methodology) comes from `profiles/client-profile.md`. A skill reads the sections its Context table names and nothing else. A skill never carries a company fact of its own. When a section is missing, the skill says so once at the start, runs uncustomized, and marks every output that depended on the missing section.

#### Account Status, Five Words

Every account carries one status: **TARGET** (researched, not yet contacted), **INBOUND** (they asked us), **ACTIVE** with its stage number (open deal), **LOST** (closed-lost, eligible for reactivation), **OUT** (disqualified). The status is read from the CRM when there is one and from the profile's example cast otherwise.

#### The Verdict Words and the Zone Rule

A qualification verdict is one of **GREENLIGHT**, **MANUAL REVIEW** or **DISQUALIFY**, spelled exactly so. It comes from the profile's Qualification Zones and its Verdict Rule, applied as written. MEDIUM never counts as HIGH. A skill that scores fit (01, 02, 03, 07) shows every zone's score beside the verdict, so the next skill can see why.

#### Stage Names Come From the Profile

Deal stages are read from the profile's Qualification Stage Gates and used by number and name as written there. No skill carries its own stage list. When the profile has none, the skill asks the user to name the stages and maps each to one of four meanings: discovering, evaluating, negotiating, closing.

#### Evidence Tags, One Set

Every fact in a report carries one tag naming where it came from:

| Tag | Meaning |
|---|---|
| `[CRM]` | A field or note in the CRM |
| `[Call]` | Said on a recorded or transcribed call, with the call date |
| `[Notes]` | A rep's or AE's written notes |
| `[Public: source]` | A public document, page or filing, with the source named |
| `[Inferred]` | Reasoned from other facts, with the reasoning shown and the method named |
| `[Unknown]` | Not known. Written as unknown, never left blank |

A fact with no tag is removed. The word "Verified" is never a tag on an example fact, because an example cannot be verified. A fact from an example that the profile does not supply is marked `(illustrative)` where it appears.

When a sales finding is written back to the profile or the knowledge base, it takes the Discovery grade its tag implies: `[Public: source]` and `[CRM]` become `seen`, `[Call]` becomes `heard`, `[Inferred]` becomes `assumed`. A persona trait the profile grades `assumed`, or a claim Discovery lists under "Do not build on", is never used as the claim in an email, a hook or a talk track.

#### Numbers

Every rate carries its n ("4 of 7 criteria", never "57%" alone). A pattern needs five cases. A blank CRM field is unknown, not a no. "No difference found" is a finding and is reported. A benchmark needs a named, dated source or it is removed. Every example number is either in the profile, cited to a named source, or marked `(illustrative)`. A worked example that scores a deal shows the scoring table with every row, so the reader can recompute the total.

#### Report First, File When Asked

Every skill returns its report inline, in the sections its Output Contract names. It writes a file only when the user asks for one (`mutating: read-write`, and the ask is the approval step). The file is Markdown, named `<account>_<skill>_<date>.md`, saved beside the user's other account notes.

#### Nothing Sends, Nothing Writes to the CRM

A skill drafts emails, call openers and sequences. The rep sends them. A skill never sends, never enrolls a contact, and never writes to the CRM. The user does those, after reading the draft.

#### The BDR Guard

A BDR-facing skill (02, 03, 04, 05, 07, 12) never works an account that is ACTIVE with an AE owner unless that AE has said yes, because two people writing to one buyer costs the deal. An account pending AE assignment is not ACTIVE. It is worked, and the output says it is pending.

#### Champion Tests, One List

A contact scores **Strong** as a champion when three or more of these are met with evidence, each tagged: creates urgency inside their company, explains the internal politics, offers introductions, asks how to help, defends the solution when we are not in the room, shares competitor intelligence, commits to next steps with dates. One or two met is **Developing**. None met is **None**. A friendly contact is not a champion. The same list and thresholds are used by 09, 10 and 13.

#### Incumbent Types, One List

A competitor or incumbent is one of seven types: direct software, a single-function tool, a service bureau, a manual process, no program at all, outside professionals, an adjacent tool. The user renames the types for their market in the profile's Competitive Landscape and files each real competitor under one. The same seven are used by 11 and 12.

#### Talk-Time Bands, One Table

Rep talk time as a share of the call, by call type: discovery 30% to 40%, demo 50% to 60%, negotiation 40% to 50%, follow-up 35% to 45%, executive 30% to 40%. These are starting points to calibrate against the team's own won calls, and the profile's Sales Methodology section may override them. The same table is used by 06 and 13.

#### What the Close Reads

Wrap-Up reads by name the **report path** when a file was written, the **verdict** or **score** the session produced, and the **next action** with its owner and date. Ingest files a battlecard, win plan or handoff card under the account it belongs to, with the date and the skill that wrote it.

#### Guild Disciplines, Restated

1. **Evidence over optimism.** Score what the record proves, not what the rep believes. Under-scoring protects a deal. Over-scoring kills it.
2. **Silence is not a no.** An empty field is unknown and is counted in no denominator.
3. **One cast, one story.** Every example uses the profile's example company and its cast. An example never presents an invented number as a real result.
4. **The profile is upstream.** Strategy skills write it. Sales skills read it. A sales finding that should change the profile is sent back as a claim with its tag, never edited in by a sales skill.
5. **Published numbers only.** A figure from a published Guild article may be cited to it. Any other figure in an example is marked illustrative.
6. **Names as roles** in anything shared. No vendor, tool or model names in a free skill beyond the platform line. The CRM is "the CRM".
7. **Draft, never send.** A rep reads before anything leaves.

---

## Methodology

Your competitive playbook, in code. The frameworks below are the defaults, and they adapt to the team's sales methodology when the profile says so. The evidence tags, claim standards and threat calibration are defined once, in the Epistemic Rules section below.

### Start From the Seven Types

Every competitor or incumbent is filed under one of the seven incumbent types in the Shared Contract, and the profile's Competitive Landscape holds the rows. Classify before you build anything, because the type decides which failure patterns, proof points and objections apply. A rival that fits two types is filed under the type that describes the buyer's current spend, and the battlecard says which one it chose and why.

### Failure Patterns and the Template Row

A failure pattern is a recurring reason that customers of one incumbent type end up unhappy. The profile's Competitive Patterns and Trends section holds them. Each row carries three things: the pattern, the number of cases behind it with their source, and the discovery question that tests the pattern on this buyer.

| Pattern | Cases counted and source | Discovery question |
|---------|--------------------------|--------------------|
| _____ | _____ cases (5 needed to call it a pattern), and the source | _____ |
| _____ | _____ cases (5 needed to call it a pattern), and the source | _____ |

The rows are left blank for your own deals. A row with fewer than five cases is written as an observation, and the battlecard says so in the same sentence.

### Trends

A trend is a dated shift in the market that changes what an incumbent's customers will feel. Each row names the trend, its dated source, and what it means for that incumbent's customers. A number appears in a trend row only when its source is named and dated. A trend with no source is removed.

| Trend | Dated source | What it means for the incumbent's customers |
|-------|--------------|---------------------------------------------|
| _____ | _____, with its date | _____ |

### Proof Point Status

Every proof point carries one Status from the profile's Proof Points table. **Verified** means the customer confirmed the number and agreed to be named. **Benchmark** means a published figure with its source and date. **Illustrative** means invented for an example. Only a Verified row may be quoted in a talk track, a battlecard line the rep reads aloud, or an email. A Benchmark may be used as context, and it is labelled as a benchmark. An Illustrative row is marked "do not cite" and is never quoted to a prospect.

### Jurisdiction Deadlines

When a competitive claim depends on a deadline set by a state or federal rule, the claim cites the rule and the date the rule was checked. A deadline with no cited rule is not written into the battlecard. The date checked is the date someone read the rule, not the date the profile was written.

---

## Quick Reference

**Use this skill when:**
- You have an open deal and know, or suspect, the incumbent or rival
- You are preparing a competitive deal review or coaching a competitive call
- You need a battlecard for one deal, not generic market intelligence
- An incumbent is entrenched and the deal needs a displacement strategy

**Don't use when:**
- You need prospecting outbound against an incumbent (use Competitive Displacement (12))
- You do not yet know what the buyer uses, because discovery has not happened (use Meeting Prep (06))
- You need generic competitive intelligence across the market (keep the profile's Competitive Patterns and Trends section current instead)

**User roles:** AE (primary)
**Expected time:** 20 to 30 minutes per account

---

## Core Workflow

### Step 1: Gather CRM and Competitive Intelligence

#### 1a. Search the CRM

Pull everything available:
- The account record: name, headquarters, segment, sites
- The open deal: stage, amount, close date, owner
- Contact records: roles, engagement level, competitive mentions
- Interaction history: discovery calls, demos, emails
- Notes: competitive context, incumbent mentions, switching barriers
- Deal health signals: the Deal Pulse "Why Us" pillar when one exists, and the MEDDPICC output from Step 2

#### 1b. Identify the Incumbent

From the CRM, the interaction history and the discovery notes:
- **Current solution:** what they use today, and how it was identified, each with its tag
- **Contract status:** active (since when), expiring (when), month-to-month or unknown. A renewal date held in the CRM is tagged `[CRM]`
- **Satisfaction level:** frustrated, neutral, satisfied or unknown
- **Switching barriers:** contract terms, data lock-in, process dependency, politics
- **Internal champion for the incumbent:** is someone an advocate for the current tool

If the incumbent is unknown, flag it as the critical discovery gap and provide the questions that identify it. Step 2 does not start until the incumbent is named or the gap is flagged.

**Produces:** The account record, the open deal and the incumbent identification, each fact tagged, with every unknown written as `[Unknown]`. Step 1 comes first because the classification in Step 2 depends on what the CRM and the calls already say.

### Step 2: Profile the Incumbent

#### 2a. Classify the Incumbent

Map the incumbent to one of the seven incumbent types in the Shared Contract, using `{Client Profile: Competitive Landscape}`. Record the competitor row it matches.

#### 2b. Load the Competitor's Failure Patterns and Trends

From `{Client Profile: Competitive Landscape}` and `{Client Profile: Competitive Patterns and Trends}`, load:
- The failure patterns for this type, each with its cases counted and its source. A pattern under five cases is labelled an observation.
- The trend rows that bear on this incumbent's customers, each with its dated source.
- The gap-exposing discovery questions from the competitor row.
- The proof points that match the scenario, each with its Status.

#### 2c. Assess the Competitive Threat Level

Using the calibration in Epistemic Rules, score the five factors. LOW is 1, MEDIUM is 2 and HIGH is 3.

| Factor | Assessment | Score |
|--------|-----------|-------|
| Prospect satisfaction with incumbent | [Frustrated / Neutral / Satisfied / Unknown] | [LOW / MEDIUM / HIGH / MEDIUM] |
| Contract status | [Expiring / Active / Month-to-month / Unknown] | [LOW / MEDIUM-HIGH / LOW / MEDIUM] |
| Switching barriers | [Minimal / Moderate / Significant] | [LOW / MEDIUM / HIGH] |
| Internal champion for incumbent | [None / Suspected / Confirmed] | [LOW / MEDIUM / HIGH] |
| Incumbent product advantage | [None / Niche / Broad] | [LOW / MEDIUM / HIGH] |

**Overall Threat Level:** Average the five scores and round to the nearest level. Show the average and the sum. Then apply the calibration. The calibration can raise the level above the average when the rival holds a genuine product advantage in one area, and the battlecard says which rule applied.

**Produces:** `incumbent_type` and `threat_level`, with the five factors and the average shown, and each failure pattern labelled as a pattern or an observation. The classification comes before the threat score because the threat factors depend on which type the incumbent is.

### Step 3: Build the Positioning Strategy

#### 3a. Qualification Zone Alignment

Rank `{Client Profile: Qualification Zones}` by relevance to this deal:

| # | Zone | Relevance to This Deal | Positioning Strategy |
|---|------|----------------------|---------------------|
| 1 | [Zone] | [Assessment] | [How to position] |
| ... | ... | ... | ... |

#### 3b. Competitive Gap Matrix

Build a capability comparison for this deal only, against the identified incumbent:

| Capability | Incumbent | Your Product | Why It Matters for This Buyer |
|------------|-----------|-------------|-------------------------------|
| [Capability the buyer named, or a failure pattern predicts] | [Status, with its tag] | [Status, with its tag] | [Tied to a stated pain or to the buyer's criteria] |

Include only capabilities that matter to this buyer, not a generic feature matrix. A row whose claim is `[Unknown]` is a discovery question, not a gap.

#### 3c. Identify Positioning Landmines

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| [Topic where the incumbent is strong] | [What could happen] | [How to redirect] |
| [Feature you lack] | [The prospect may ask] | [Honest response and a bridge] |

Being ready for landmines is worth more than perfect positioning. An AE who is surprised by a competitor's strength loses credibility.

**Produces:** `gap_matrix` and the landmine table. The matrix comes before the playbook because the talk tracks in Step 4 are built from its rows.

### Step 4: Create the Displacement Playbook

#### 4a. Discovery Questions

Provide five or six questions drawn from the competitor row and the failure patterns. Each exposes a gap without attacking the incumbent. For each question:
- **Question:** the exact words to ask
- **What it exposes:** the gap or limitation it surfaces
- **If they confirm the gap:** how to pivot to the product's strength
- **If they deny the gap:** how to probe deeper, or move on gracefully

#### 4b. Objection Handling

**Universal objections (any incumbent):**

| Objection | Response Framework | Script | Status |
|-----------|-------------------|--------|--------|
| "We already use [the incumbent]" | Positive frame, then discovery | "That's good. It means you already understand the value. What's working well, and what would you change?" | Field-tested |
| "Switching cost is too high" | Quantify the cost of staying | "What does staying cost each year? Put a number on [metric] for twelve months, from your own records, and we can compare." | Field-tested |
| "We'll build it ourselves" | Core versus context | "That makes sense for what sets you apart. Is [your domain] where you want to spend your team's time?" | Test and refine |
| "Send me information" | Bridge to a meeting | "Happy to. Which would help most: the benchmarks, or the overview for your situation?" | Field-tested |
| "The timing isn't right" | Cost of waiting | "What does one more month of [pain] cost you? Use your own count, and tell me where the number came from." | Test and refine |

**Objections keyed to the situation.** The incumbent types are in the Shared Contract, so these rows are keyed to what the buyer says, not to the type:

| If the Buyer Says | Likely Objection | Response |
|-------------------|-----------------|----------|
| The incumbent is integrated with the systems they already run | "We're integrated" | "Many customers keep [their ecosystem] for [its job] and use us for [our job]. The two are complementary." |
| The buyer has spent years and money on the incumbent | "We've invested too much to switch" | "Reference customers who moved off a long-standing system describe the switch as a planned project. Ask us for the reference, once it is Verified." |
| An outside firm does the work for a fee | "We trust our provider" | "Trust matters. How do you check what they process is right, and what is the backup if they have a staffing problem?" |
| A spreadsheet or paper process runs the job | "It works fine for us" | "It often does, until it doesn't. What happens if the person who keeps it is out for two weeks?" |
| Nothing owns the job today | "We don't need a program" | "That is a bet worth counting. What is exposed if the job goes wrong, and what would it cost to find out after the fact?" |

#### 4c. Displacement Talk Tracks

Write three or four talk tracks in this form: "When [prospect situation], [product] [specific capability]. For example, [Verified customer and metric]."

Each talk track must:
- Name the buyer's situation, not a generic one
- Name a capability tied to the competitive gap
- Name a Verified proof point with its customer and metric. If no Verified row fits the scenario, the talk track has no example clause, and the rep shows the capability in the demo instead
- Be readable aloud in under 20 seconds

#### 4d. Match Proof Points

| Proof Point | Status | Why It Matches This Deal | How to Use It |
|------------|--------|------------------------|---------------|
| [Customer: metric] | [Verified / Benchmark / Illustrative] | [Similarity to this buyer] | [Where it goes in the conversation, or "do not cite"] |

**Produces:** The playbook. That is the discovery questions, the objection table, the talk tracks and the matched proof points, which become battlecard sections 4 to 7.

### Step 5: Build the Win Plan

Build a checklist for this competitive scenario:

**Pre-meeting:**
- [ ] Review the gap matrix
- [ ] Prepare three gap-exposing discovery questions
- [ ] Know the two best Verified proof points cold, or know that none exists
- [ ] Prepare a mitigation for each landmine
- [ ] Review the objection handling for this incumbent type

**During discovery:**
- [ ] Ask the gap-exposing questions with genuine curiosity, not as an interrogation
- [ ] Listen for pain signals about the incumbent: frustration, workarounds, complaints
- [ ] Confirm the contract status and the renewal date with the buyer, rather than assuming it
- [ ] Ask the buyer to state the criteria the decision will use, in their own words, before any demo
- [ ] Note the exact words the buyer uses for the pain, and mirror them back

**During demo:**
- [ ] Lead with the capabilities that address the stated gaps, not a feature tour
- [ ] Show Verified proof from comparable customers only
- [ ] Demonstrate the workflow the incumbent does poorly
- [ ] Address the known objections before they are raised
- [ ] End with "How does this compare to your current experience?"

**Post-meeting:**
- [ ] Send a follow-up that uses the buyer's own words for the pain
- [ ] Include the most relevant Verified proof point, if the customer gave permission
- [ ] Propose the next step with a dated timeline
- [ ] If several people are involved, send each one a follow-up that fits their role
- [ ] Update the CRM with the competitive intelligence learned

**Produces:** `win_plan`, the checklist above with an owner and a date on each item where one is known. The plan comes after the playbook because its items point at the questions and proof points built in Step 4.

### Step 6: Competitive Strategy Summary

1. **Account:** name, status, deal stage, amount, owner
2. **Incumbent:** the current solution, its incumbent type, and its tag
3. **Competitive threat level:** HIGH, MEDIUM or LOW, with the factor scores and the average
4. **Primary positioning:** the zone that is strongest for this deal
5. **Top three competitive gaps to exploit:** the gaps the incumbent cannot close, each tied to a buyer criterion
6. **Positioning landmines:** where the conversation could go badly, with mitigations
7. **Displacement proof point:** the most relevant Verified proof point, or a note that none exists, with its Status shown
8. **Critical discovery gap:** what is still unknown about the buyer's current solution
9. **Win strategy summary:** two or three sentences on how to win this deal competitively
10. **Risk assessment:** where the competitor could win, stated honestly
11. **Recommended next steps:** specific actions with a timeline

**Produces:** The battlecard in its eight sections, with `battlecard`, `incumbent_type`, `threat_level`, `next_action` and `report_path`. The summary comes last because it draws on every step above it.

---

## Modes

This skill has one mode. The default is the battlecard for one open deal.

---

## Epistemic Rules

- **Every rate carries its n.** Write "2 of 5 cases", never a bare rate.
- **Five cases before a pattern.** A failure pattern needs five cases with a named source behind it. Fewer than five is an observation, and the battlecard says so in the same sentence.
- **Silence is not a no.** A blank CRM field or an unanswered question is `[Unknown]`. It is counted in no denominator and is never read as a negative about the incumbent.
- **"No difference found" is a finding.** If the buyer's criteria do not separate the incumbent from the rival, the battlecard says the deal is open on those criteria. It does not invent a winning gap.
- **Every claim carries one of the six evidence tags.** The tags are `[CRM]`, `[Call]`, `[Notes]`, `[Public: source]`, `[Inferred]` and `[Unknown]`. A claim with no tag is removed. Verified is a proof point Status, never a tag.
- **Only Verified proof reaches a talk track.** The Status rule in Methodology decides this, however good the story is.
- **A benchmark needs a named, dated source.** Otherwise it is removed.
- **A jurisdiction deadline cites its rule and the date checked.** Otherwise it is not written.
- **An inferred claim is a hypothesis.** A claim tagged `[Inferred]` is tested on the buyer before it is used. It never appears as fact in a talk track.
- **Discovery questions are genuine.** If the AE already knows the answer, the question is a setup. Rewrite it as a positioning statement.
- **Objection scripts show their status.** Each script is marked Field-tested or Test and refine. A script not yet tested with a buyer is never presented as tested.
- **Risk assessments are honest.** If the rival has a real advantage, the battlecard names it and the criterion it wins on.

### Competitive Threat Assessment Calibration

- **HIGH:** The prospect is satisfied with the incumbent, the incumbent is entrenched (2 years or more), the contract is active, there is no switching-cost concern from the prospect, or the incumbent has a genuine product advantage in one area.
- **MEDIUM:** The prospect has expressed some dissatisfaction and the contract timing is favorable, but the incumbent has strong relationships or the switching costs are real.
- **LOW:** The prospect is actively frustrated, the incumbent is manual or absent, the switching barriers are minimal, or the prospect is already evaluating alternatives.

---

## Hard Rules

1. **Only a Verified proof point goes into a talk track, a battlecard line the rep reads aloud, or an email.** Reason: a prospect can ask for the customer and the number, and an Illustrative row fails that check in front of the buyer.
2. **Never trash a competitor.** Reason: it implies parity, and it makes the buyer defend the incumbent. Describe what the buyer can do with your product instead.
3. **A failure pattern needs five cases with a named source.** Reason: fewer cases is a coincidence that looks like a pattern, and a rep who repeats it is repeating a coincidence.
4. **No unsourced number in a talk track, an email or a battlecard line.** Reason: any figure without a named, dated source becomes folklore the moment a buyer asks where it came from.
5. **A jurisdiction deadline cites its rule and the date checked.** Reason: a deadline without a cited rule cannot be checked, and a wrong one can cost the deal its timing.
6. **Every competitor is filed under one of the seven incumbent types.** Reason: a battlecard that cannot be compared with the others cannot be reviewed, and a type that is avoided hides the classification error.
7. **Never state a preference the buyer has not stated.** Reason: an assumed preference writes the battlecard for a buyer who did not say it, and the gap matrix then argues against the wrong case.
8. **Never send, never write to the CRM and never enroll a contact.** Reason: the AE owns the outreach and the record, and the rep reads every draft first.

---

## Quality Bar

Done when all are true:

- [ ] The incumbent is filed under one of the seven incumbent types, or flagged as unknown with a discovery plan
- [ ] Every claim carries one of the six evidence tags, and every blank is written as `[Unknown]`
- [ ] Every failure pattern shows its cases counted and its source, and any pattern under five cases is labelled an observation
- [ ] Every proof point shows its Status, and no talk track, email or battlecard line cites a row that is not Verified
- [ ] The threat level shows all five factors and the average, and the calibration rule applied is named
- [ ] Each discovery question is genuine and has a pivot for both answers
- [ ] Each objection script shows its status, Field-tested or Test and refine
- [ ] Any jurisdiction deadline cites its rule and the date checked
- [ ] Any rival advantage is named, with the criterion it wins on
- [ ] The win plan has actions for each stage, and `next_action` is last, with an owner and a date
- [ ] No file was written unless the user asked for one

---

## Examples

Two worked examples, both on the PlotIQ cast and the chain file. The first is the flagship deal against its incumbent. The second is the rival in the same deal, where the buyer has not stated a preference, so the battlecard says what it cannot yet claim. Every figure is in the profile, sourced, or marked (illustrative). Each example ends with its hand-off block.

### Example 1: Incumbent Renewal, Oldgate Ledger Pro at Brackhaven Memorial Gardens

**Context:** Owen Pruitt, Account Executive (illustrative), has an open deal at Stage 5 Negotiate with Brackhaven Memorial Gardens, a two-site combination with 11,000 plots. Stage 5 began on 2026-09-09 `[CRM]`, which is 40 days in stage today, 2026-10-19. At the profile's list price of $10,788 a year per site, the two sites come to $21,576 a year. The incumbent is Oldgate Ledger Pro, a legacy on-premise system with a renewal in March 2027 `[CRM]`, under six months away. Stonemark was also evaluated, and it has its own example below. Account Qualification (01) scored the account GREENLIGHT.

**Input:** "Build a competitive strategy for Brackhaven Memorial Gardens. They run Oldgate, and the renewal is in March 2027."

**Step 1: CRM Intelligence:**
- Account: Brackhaven Memorial Gardens, combination, 2 sites, 11,000 plots, paper plot maps `[CRM]` (illustrative)
- Deal: Stage 5 Negotiate, $21,576 a year at list, owned by Owen Pruitt, 40 days in stage `[CRM]`
- Contacts: Ruth Ellery, GM, champion `[Call]`. Walt Okonkwo, Operations Director, skeptical of tablets `[Call]`. Priscilla Dunmore, pre-need manager `[CRM]`. Family board chair, the economic buyer, on one call `[CRM]`, name `[Unknown]`
- Discovery note (illustrative quote): Ruth: "We can't tell which plots are sold without going to the binder." `[Call]` (illustrative)
- Incumbent: Oldgate Ledger Pro `[CRM]`. Ruth named it on the first call, and the call was logged

**Step 2: Incumbent Profile:**
- Classification: direct software, the legacy on-premise row in the profile's Competitive Landscape `[Inferred: profile row match]`
- Their pitch: "Mature, deep accounting." Research weaknesses: $10,000 to $50,000 upfront, plus maintenance at 20% a year, poor mobile, and no AI `[Public: deathcare research, 2026-03-27]`. Not yet checked with this buyer, so these are discovery targets
- Satisfaction: Neutral. Ruth tolerates it, and Walt works from paper `[Call]` (illustrative)
- Contract status: renewal in March 2027 `[CRM]`
- Switching barriers: moderate. Two sites of plot records and a trust fund ledger to export `[Inferred: scope of the two-site records (illustrative)]`
- Internal champion for the incumbent: none identified `[Inferred: no call on file defends Oldgate]`
- Failure pattern check: "Maintenance is charged every year, and the grounds crew stays on paper work orders" is a legacy on-premise pattern from the research. The PlotIQ record holds [RECORD] of 5 cases, so until five are counted it is an observation only, and the battlecard does not call it a pattern

**Step 2c: Threat Assessment:**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Neutral | MEDIUM |
| Contract | Renewal in March 2027, a favorable window | LOW |
| Switching barriers | Moderate (two sites of records, a ledger export) | MEDIUM |
| Internal champion for incumbent | None identified | LOW |
| Incumbent product advantage | Niche (accounting depth) | MEDIUM |

**Overall: MEDIUM threat.** The five scores are 2, 1, 2, 1 and 2, a sum of 8, so the average is 8 ÷ 5 = 1.6 on the 1 (LOW) to 3 (HIGH) scale, which rounds to MEDIUM. The calibration agrees, because the incumbent's advantage is niche and no one has argued for keeping it. The main risk is inertia: Walt's paper process has no one pushing for change.

**Step 3b: Gap Matrix:**

| Capability | Oldgate Ledger Pro | PlotIQ | Why It Matters for Brackhaven |
|-----------|---------|--------|----------------------|
| Mobile use by the grounds crew | Poor mobile `[Public: deathcare research, 2026-03-27]` | Mobile field app `[Public: PlotIQ product modules]` | Walt needs work orders in the field, so the crew can find a plot in seconds `[Call]` (illustrative) |
| Unsold-plot visibility | `[Unknown]`. Ask in discovery (question 1 below) | Plot inventory digitization shows unsold plots `[Public: PlotIQ product modules]` | Ruth's unsold-plot count depends on this, and it is not among Oldgate's known features |
| Trust fund records | Deep accounting, their pitch `[Public: deathcare research, 2026-03-27]` | Records and Trust Compliance module `[Public: PlotIQ product modules]` | A state auditor has to accept the record. Show the output side by side with the filing format |
| Cost | $10,000 to $50,000 upfront, plus maintenance at 20% a year `[Public: deathcare research, 2026-03-27]` | $899 a month per site, plus $5,000 setup once `[Public: PlotIQ price list]` | Year one at list for two sites is $26,576 with setup (illustrative), above the $25K board line |
| Time to live | 120 to 180 days `[Public: deathcare research, 2026-03-27]` | 6 weeks `[Public: PlotIQ profile]` | The March 2027 renewal leaves room to go live before the window closes |

**Step 3c: Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| "Oldgate has deep accounting" | Ruth or the board chair hears depth as safety | "Oldgate is strong on accounting. Our trust records are built for what a state auditor reads, and we can show you the output next to your current ledger." |
| Moving two sites of records | Staff fear losing the paper binders | "We start with the plot map, the first module. The implementation team digitizes the maps and deeds in weeks 2 to 3 `[Public: PlotIQ profile]`." |
| Stonemark was also evaluated | The board compares two new tools | Keep the comparison to the buyer's criteria, and cover Stonemark in its own battlecard (Example 2) |

**Step 4a: Discovery Questions (from the profile's Competitive Discovery Questions):**
1. "Where does the plot map live today, and when was it last updated?" Exposes: how old the plot map is, and whether sales can see it. If confirmed (a binder, years old): pivot to plot inventory digitization, which runs in weeks 2 to 3. If denied (a current digital map exists): probe whether it shows sold and unsold plots.
2. "Which system runs the funeral side, and who maintains it?" Exposes: a second system and a key-person dependency. If confirmed: pivot to the combined records view. If denied: ask how pre-need leads are tracked today.
3. "When does your software contract renew, and what did the last quote include for support?" Confirms the March 2027 date and the support cost. If confirmed: align the evaluation to the renewal decision. If denied: ask who makes the renewal decision.

**Step 4c and 4d: Talk Tracks and Proof Points:** No talk track is written here, and that is the rule working. The Brackhaven scenario has no Verified proof point yet. The two customer rows in the profile, Holloway Hills and Fennick Gardens, are Illustrative and are marked do not cite. The battlecard names the capability, and the demo shows it on Brackhaven's own counts.

**Step 5: Win Plan highlights:**
- Ask Ruth to pull the count of plots with no recorded sale, and to bring her own number. Do not estimate it.
- Confirm the renewal notice date with Ruth. Do not assume it.
- Plan the evaluation to finish before the March 2027 renewal decision. The 60 to 90 day evaluation window is an illustrative assumption to calibrate with Ruth.
- The demo leads with an unsold-plot list drawn from Brackhaven's own records, not a feature tour.
- Economic buyer: the family board chair, who has been on one call `[CRM]`. Ruth builds the case.
- Risk: the "deep accounting" argument lands with the board chair. Mitigation: show the trust report output next to the state filing format.

**Output:** Full eight-section battlecard. Threat level MEDIUM. The strongest competitive lever is unsold-plot visibility, and records a state auditor accepts, both shown in Brackhaven's own counts. The honest risk is Oldgate's accounting depth, and the chance that the paper process stays the default.

```text
Hand-off (read by 06 and 12):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
incumbent_type: direct software, Oldgate Ledger Pro [CRM]
threat_level: MEDIUM (five factors 2, 1, 2, 1, 2, average 1.6)
gap_matrix: 5 rows, mobile use, unsold-plot visibility, trust fund records, cost, time to live
battlecard: 8 sections, inline
win_plan: 5 groups, pre-meeting to post-meeting, owners on each item
next_action: Owen Pruitt asks Ruth Ellery for the board date and the Oldgate renewal notice date by 2026-10-23
report_path: none (inline)
```

---

### Example 2: Stonemark, the Evaluated Rival With No Preference Stated (Brackhaven Memorial Gardens)

**Context:** The same deal as Example 1, on the same day. Ruth named Stonemark as one of the options they looked at `[Call]`, and no one has said which tool they prefer `[Call]`. Stonemark has not been ruled out, and Oldgate still renews in March 2027 `[CRM]`. This is the non-success case in a quieter form: the buyer has not chosen a criterion, so the battlecard cannot claim a win, and it must say so.

**Input:** "Build the Stonemark battlecard for Brackhaven. Ruth says they also looked at Stonemark, and nobody has said which one they prefer."

**Step 1: CRM Intelligence:**
- Deal: Stage 5 Negotiate, $21,576 a year at list, owned by Owen Pruitt, 40 days in stage `[CRM]`
- Contacts: Ruth Ellery, champion, no reply since 2026-10-03, 16 days `[CRM]`. Walt Okonkwo, Operations Director `[Call]`. Family board chair, one call `[CRM]`, name `[Unknown]`
- Competitors: Oldgate Ledger Pro, the incumbent, renews March 2027 `[CRM]`. Stonemark, evaluated `[Call]`

**Step 2: Rival Profile:**
- Stonemark is enterprise cemetery mapping, and its pitch is "The best mapping in the category" `[Public: deathcare research, 2026-03-27]`
- Research estimates: about $1,500 to $2,500 a month, 90 to 120 days to live, no AI `[Public: deathcare research, 2026-03-27]`
- Its advantage is the depth of its mapping `[Public: deathcare research, 2026-03-27]`
- Its gap is that records and trust compliance are not part of its positioning `[Inferred: profile positioning, not yet tested with the buyer]`

**Step 2c: Threat Assessment (Stonemark, the rival in the deal):**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Buyer's stated preference | None stated `[Call]` | MEDIUM |
| Contract | No contract with Stonemark. The evaluation is open, and Oldgate renews in March 2027 `[CRM]` | MEDIUM |
| Switching barriers | A new load of Brackhaven's map data `[Inferred: scope of a new load]` | MEDIUM |
| Internal champion for the rival | None identified `[Inferred: no call on file argues for Stonemark]` | LOW |
| Product advantage | Broad: mapping depth is the rival's core pitch | HIGH |

**Overall: HIGH threat.** The five scores are 2, 2, 2, 1 and 3, a sum of 10, so the average is 2.0, which reads MEDIUM. The calibration gives HIGH anyway, because the rival holds a genuine product advantage in one area, mapping depth, and no buyer criterion yet says that area matters less. The battlecard shows both the average and the rule that raised the level.

**Step 3b: Gap Matrix:**

| Capability | Stonemark | PlotIQ | Why It Matters for Brackhaven |
|-----------|-----------|--------|-------------------------------|
| Mapping depth | Enterprise mapping, their core pitch `[Public: deathcare research, 2026-03-27]` | Plot inventory digitization of paper maps and deeds `[Public: PlotIQ product modules]` | The buyer has not said how much map depth decides it. Their strength is real, and the battlecard says so |
| Records and trust compliance in one system | Not in their positioning `[Inferred: profile positioning]` | Records and Trust Compliance module `[Public: PlotIQ product modules]` | A state auditor reads the trust record. Ask Ruth whether the board will judge on it |
| Pre-need leads in the same system | `[Unknown]`. Ask | Pre-Need CRM and Lead Scoring `[Public: PlotIQ product modules]` | The pre-need manager's leads land in one place, with a named follow-up owner |
| Time to live | 90 to 120 days `[Public: deathcare research, 2026-03-27]` | 6 weeks `[Public: PlotIQ profile]` | The timing decides whether a decision can finish before the March 2027 renewal |
| Price | About $1,500 to $2,500 a month `[Public: deathcare research, 2026-03-27]` | $899 a month per site `[Public: PlotIQ price list]` | Shows the monthly gap without claiming their total cost |

**Step 3c: Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| "Stonemark's mapping is better" | The buyer agrees, and the decision goes to the map | "You're right that their mapping is built for enterprise. Ask them whether one system holds the trust record and the pre-need leads. Ask us the same question, and we'll show you the answer." |
| The board compares monthly cost only | The board decides on the lower monthly figure | Put the cost of an unsold plot and of a missed trust filing in Brackhaven's own counts. Do not put a dollar figure on a risk Brackhaven has not counted |
| No criteria are set | The decision drifts to whichever tool was demonstrated last | Ask Ruth to write the criteria the board will use, in her words, before any demo |

**Step 4a: Discovery Questions (for the open preference question):**
1. "What would the board need to see before it can say yes to a new system?" Exposes: the buyer's criteria, which no one has stated. If confirmed (specific criteria): build the demo around them. If denied (no criteria yet): ask Ruth to write them with you.
2. "Which records would you need on day one, and where do they live?" Exposes: the migration load. If confirmed (paper binders): start with the plot map. If denied: ask who maintains the current records.
3. "Would the board also want to see the trust fund report, or only the map?" Exposes: whether the trust record is part of the decision. If confirmed: run the trust report in the evaluation. If denied: ask what the state auditor requires.

**Step 5: Win Plan:**
- Ask Ruth to put the decision criteria in writing before any demo, in the board's terms.
- Put the family board chair on the call where the criteria are set. The economic buyer has been on one call `[CRM]`.
- Offer no pilot until the buyer asks for one. If asked, scope it to the written criteria only.
- Finish the decision before the Oldgate renewal in March 2027. Ask Ruth for the renewal notice date. Do not assume it.
- Re-score the threat once the criteria are written.

**Risk Assessment:** Stonemark could win if the board judges on the map alone. Oldgate renews by default if the decision stalls. Until the buyer states a criterion, the battlecard cannot claim that we beat Stonemark on the map, and it does not.

**Output:** Full battlecard, HIGH threat. The win strategy is to test records and trust compliance on the buyer's own criteria, before the renewal date. If the criteria test only the map, the battlecard says so, and the deal is reassessed.

```text
Hand-off (read by 06 and 12):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
incumbent_type: direct software, Oldgate Ledger Pro [CRM]. Rival evaluated: Stonemark, also direct software
threat_level: HIGH by calibration (five factors 2, 2, 2, 1, 3, average 2.0 reads MEDIUM)
gap_matrix: 5 rows, Stonemark against PlotIQ, no preference stated
battlecard: 8 sections, inline, the rival's advantage named
win_plan: 5 groups, criteria in writing before any demo
next_action: Owen Pruitt asks Ruth Ellery to put the board's decision criteria in writing by 2026-10-23
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Unknown Incumbent

**When:** The incumbent has not been identified through discovery.
**Action:** Flag it as the critical gap, and give the discovery questions that identify it. Build a strategy only for the most likely incumbent types, and mark it as provisional. Recommend Meeting Prep (06) for discovery. Reason: a battlecard for an unknown incumbent is a guess with a battlecard's layout.

### Pattern: Dual-Tool Pain

**When:** The account uses two separate tools, one for each part of the job.
**Action:** Build the strategy around the unification angle. Reference Verified proof points where one product replaced both tools at once. The gap matrix shows the gap between the two tools as the primary pain.

### Pattern: Renewal Window

**When:** A renewal date is known from the CRM or from discovery.
**Action:** Plan the timeline to finish the decision well before the renewal date. Start from 60 to 90 days before renewal (illustrative), and calibrate it with the buyer. Reason: the renewal date is the one fixed point the rep can plan against.

### Pattern: Incumbent Champion (Blocker)

**When:** Someone in the prospect's organization advocates for the current tool and may resist change.
**Action:** Identify the blocker's concerns, such as job security, familiarity, or the political capital already spent on the choice. Build positioning that neutralizes the concern without confronting it: "The platform doesn't replace your team's expertise. It amplifies it." Consider multi-threading around the blocker to the economic buyer.

### Pattern: Evaluated Rival, No Preference Stated

**When:** The buyer names a rival as one of the options and states no preference.
**Action:** Build a rival battlecard that names the rival's real advantage, and set the buyer's criteria before the demo. Reason: silence on preference is not a preference for the incumbent, and the gap matrix must not assume one. Example 2 shows this pattern.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| "We don't have competitive intelligence for this specific competitor" | The competitor is not yet filed in the profile | File it under the closest incumbent type in the Shared Contract, use category-level gaps, and tag each claim `[Inferred]` with the category as its basis. Send the new competitor as a tagged claim for the profile owner. A sales skill does not edit the profile itself |
| The prospect is satisfied with the incumbent | No dissatisfaction signal yet | Treat it as HIGH threat. Do not create dissatisfaction. Ask the discovery questions, and use only trend rows with dated sources to show what changes over time |
| The incumbent is an internal build | The buyer's own team does the job | File it under the closest incumbent type in the Shared Contract, and use the build-versus-buy objection in Step 4b. Ask what the team would stop doing if the build were not theirs |
| Multiple competitors in play (a bake-off) | Two or more rivals are on the shortlist | Build the strategy against the strongest one first, and add a section for the second. Name in the win plan which one carries more threat |
| The buyer likes the incumbent but is evaluating out of obligation | A procurement requirement, not a preference | Treat it as HIGH threat. The incumbent is the default winner, so the strategy must create a real preference. Multi-thread to a stakeholder who is not invested in the incumbent |
| The buyer names a rival and states no preference | Silence on criteria, not a preference for the incumbent | Use the Evaluated Rival pattern. Build the rival battlecard, set the criteria in writing, and do not claim a win |
| No proof point is Verified for this scenario | No customer has confirmed a number and agreed to be named | Use no proof point in a talk track. Show the capability in the demo, and log a request for a Verified reference |

---

## Best Practices

### Do's
- **Respond positively to competitor mentions.** The budget is already allocated, and no new capital outlay is needed.
- **Lead with enablement, not criticism.** "Here is what becomes possible" lands better than "here is what is broken."
- **Use competitor-specific discovery questions.** Genuine curiosity exposes gaps better than accusations.
- **Include an honest risk assessment.** Naming where the competitor could win is what makes the rest of the battlecard credible.
- **Match proof points to the scenario, with their Status shown.** Displacement stories go to displacement deals, and only Verified ones are spoken.
- **Prepare for landmines.** Knowing where the conversation could go badly is worth more than perfect positioning.
- **Tag every claim.** A reader should see where each fact came from without asking.

---

## Integration With Other Skills

**Reads from the skill before it, by field name:**
- **MEDDPICC Analysis (09), `gtm-meddpicc-analysis`:** `meddpicc_scores`, `health_score`, `stage_minimum_met`, `stage_recommendation`, `risk_patterns`. Use `risk_patterns` to find the element where the deal is weakest, and aim the gap matrix there. Read the competition element in `meddpicc_scores` before writing Step 1. Use `stage_recommendation` (ADVANCE, HOLD, DOWNGRADE or DISQUALIFY) to set how urgent the win plan is. When a field is missing, say it is missing, and do not rebuild it here.

**Hands to the skills after it, by field name:**
- **Meeting Prep (06):** `incumbent_type`, `threat_level`, `gap_matrix`, `battlecard`, `win_plan`. Meeting Prep builds its Competitive Positioning section from `gap_matrix` and keeps each proof point's Status as written.
- **Competitive Displacement (12):** `incumbent_type`, `threat_level`. Both skills file the incumbent from the same Shared Contract list, so the two battlecards agree.
- **Wrap-Up (O10):** `report_path` (set only when a file was written), `threat_level`, and `next_action` (owner and date).

---

## Changelog

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, Core Workflow with a Produces line per step, one Epistemic Rules section, Hard Rules with reasons, Quality Bar, and Integration with named hand-off fields.
- The incumbent is filed under the seven shared incumbent types, which the Shared Contract holds and this skill refers to without restating.
- Failure patterns, trends and jurisdiction deadlines are read from the profile's Competitive Patterns and Trends section. Each carries its cases counted, its dated source, or its rule and the date checked.
- Proof points carry a Status. Only Verified proof reaches a talk track, a battlecard line the rep reads aloud, or an email.
- The three old evidence grades are replaced by the six shared tags, and the two Epistemic Rules sections are merged into one.
- The HTML and PDF card options and the threat colour codes are removed. The file option is Markdown, written only when asked.
- The Stonemark example is rebuilt on the chain fact that the buyer has stated no preference. The pilot request is removed. Both examples carry tags and end with hand-off blocks.
- Hand-off fields to Meeting Prep (06) and Competitive Displacement (12) are named. The skill reads the MEDDPICC Analysis (09) fields by name.

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around one example company. Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy. Client-specific data moved to the shared client profile. Framework machinery moved to a Methodology section.

### 1.0.0 (2026-03-04)
- Initial release, migrated from the competitive strategy builder. Generalized through a client profile block, with the never-trash philosophy and the win plan checklist preserved.

