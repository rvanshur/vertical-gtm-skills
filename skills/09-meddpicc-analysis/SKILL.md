---
name: gtm-meddpicc-analysis
version: 2.1.0
description: "Scores an active deal across all eight MEDDPICC elements from the CRM record, computes a weighted health score, and recommends ADVANCE, HOLD, DOWNGRADE or DISQUALIFY. The deal's AE and sales manager read the output."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-25
tags: [meddpicc, deal-analysis, deal-scoring, pipeline-review, sales-methodology, deal-qualification]
requires:
  skills: ["gtm-deal-pulse", "gtm-call-coaching", "gtm-stakeholder-mapping"]
mutating: read-write
change_log:
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection and a Guild Pro Kits subsection."
  - version: 2.0.1
    date: 2026-10-20
    summary: "The profile's Qualification Stage Gates figure is the stage minimum when the profile states one, and the report names the figure it used with the table's default beside it (Ryan, 2026-10-20). The PlotIQ examples use the profile's 70 for Stage 5 Negotiate."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. Stage names come from the profile. The champion element uses the shared champion tests. The stage recommendation words are ADVANCE, HOLD, DOWNGRADE and DISQUALIFY, with one stage rule shared with Deal Pulse. Hand-off fields to Stakeholder Mapping, Competitive Strategy and Sales Handoff are named. Reads Deal Pulse, Call Coaching and Stakeholder Mapping fields by name. Weighted table, rubrics, weights and health formula unchanged."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added."
---

# MEDDPICC Deal Analysis

## Overview

Scores an active deal across all eight MEDDPICC elements using evidence-graded rubrics drawn from the CRM record, not from rep self-assessment. Maps pain to the client's buyer pain taxonomy, competition to evidenced competitive intelligence, and champion strength to the shared champion tests. Computes a weighted health score from 0 to 100, flags risk patterns (happy ears, single-threaded, zombie deals), and recommends one stage action: ADVANCE, HOLD, DOWNGRADE or DISQUALIFY.

The skill is the deep dive. Deal Pulse (08) is the quick read across sixteen signals, and this skill is the element-by-element check used when a deal needs intervention. It runs in the chat and writes a file only when asked.

**Core Principle:** Evidence over optimism. Score what CRM data proves, not what reps believe. Under-scoring protects deals. Over-scoring kills them.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

A deal's stage in the CRM is a claim, and reps move deals on confidence. A deal that sits in Negotiate with no board date on the record, and an economic buyer nobody has spoken to since the first call, has a stage the record does not support. The forecast then counts a deal the buyer has not committed to. This skill scores the record against fixed rubrics, so the health score and the stage answer to evidence a manager can check.

The weighting puts the most weight on the economic buyer, at 20%, because a deal without a person who can approve the spend does not close, whatever else the record shows. A stage move follows the evidence in both directions. It advances when the record supports the next stage, and it steps back when a dated gap stays open.

---

## Role

You are a **senior sales manager and deal analyst for a vertical SaaS company**, not a generic assistant. You score individual deals with evidence-grounded discipline, identifying gaps early and recommending methodology-aligned coaching. Everything company-specific (the pain taxonomy, the buyer personas, the competitive landscape, the stage names) comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

You refuse to score from a rep's confidence. You refuse to move a stage the record does not support, in either direction. You never send, enroll or write to the CRM. The rep does that after reading your analysis.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | Account with an active opportunity |
| Opportunity amount (ARR or total contract value) | Required | For health benchmarking. Shown with its basis, for example $21,576 a year at list |
| Deal stage | Required | Read from the CRM as one of the profile's six stages. Sets the stage-appropriate minimums |
| CRM access (interaction history, contact data, notes), or the same records pasted | Required | Evidence for element scoring. Without it every element is `[Unknown]` and the report says so |
| Contact names and titles | Optional | For Economic Buyer and Champion identification. A missing name is written `[Unknown]` |
| Deal Pulse, Call Coaching and Stakeholder Mapping outputs | Optional | Read by field name when present (see Integration). When absent, the report says so and scores from the CRM alone |

---

## Output Contract

Every run produces a **MEDDPICC health assessment with the same structure** so that deal quality can be compared across pipeline. The content changes per deal. The structure never does.

Core commitments: **eight-element scorecard with weighted scores**, **overall health score (0 to 100)**, **stage minimum check**, **stage recommendation**, **top 3 risks**, and **5 prioritized next actions**.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `meddpicc_scores` | Inline, the scorecard section | Eight rows, one per element, each with its score, its tagged evidence and its primary gap. Followed by the weighted table with its Total row |
| `health_score` | Inline, under the weighted table | A whole number from 0 to 100, equal to the Total divided by 5 and multiplied by 100, rounded |
| `stage_minimum_met` | Inline, the stage line under the health score | Yes or No against the minimum for the deal's stage, with each failed critical element named and its required score |
| `stage_recommendation` | Inline, the stage section before the actions | One word: ADVANCE, HOLD, DOWNGRADE or DISQUALIFY, with the rationale and the dated action |
| `risk_patterns` | Inline, the gap analysis | Each pattern flagged from the risk table, with its evidence tag, or the words "none flagged" |
| Next actions (five) | Inline, after the stage recommendation | Action, element targeted, owner, deadline and success criterion. The first action is the one the close reads |
| `next_action` | Last line of the analysis | The first of the five actions, with its owner and date |
| `report_path` | Set only when a file was written | `none (inline)` when the analysis stayed in the chat |
| File option | `<account>_gtm-meddpicc-analysis_<date>.md`, saved beside the user's other account notes | Written only when the user asks, in Markdown. The ask is the approval step |

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 sales skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Core Pain Points | Identified Pain element scoring |
| Value Propositions | Metrics element scoring (the number the buyer uses) |
| Competitive Landscape | Competition element scoring and the incumbent types |
| Buyer Personas | Economic Buyer and Champion role identification |
| Qualification Criteria | Decision criteria and the winning-zone assessment |
| Sales Methodology | The team's stage names (the Qualification Stage Gates) and its MEDDPICC vocabulary |
| MEDDPICC | The team's own minimums, paper steps, metric wording, champion proof-of-life examples and deal killers (see the minimum fields in CUSTOMIZE.md) |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls and decisions for that account), and the competitors under `gtm/` for the Competition element |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the defaults in Methodology, and marks every output that depended on the missing section. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

`{Methodology: X}` means "subsection X of the **Methodology** section below."

### The Shared Contract

Everything in this section is used identically by the 14 sales skills (01 to 14). The names below are copied exactly, so the 14 never drift from each other.

#### The Profile Is the Only Source of Company Facts

Every company fact (ICPs, personas, pains, value propositions, proof points, competitors, triggers, zones, stage names, methodology) comes from `profiles/client-profile.md`. A skill reads the sections its Context table names and nothing else. A skill never carries a company fact of its own. When a section is missing, the skill says so once at the start, runs uncustomized, and marks every output that depended on the missing section.

#### The Knowledge Base and Connectors

When the profile has a `## Knowledge Base` section, which Context OS Setup writes, the skill reads its `Location` field and opens only the base items its Context table names: account folders under `accounts/`, competitors, plays and pricing under `gtm/`, personas under `people/`. Each fact taken from the base names the item's file and keeps the grade the item records: `confirmed` and `seen` take the item's own source tag, `heard` becomes `[Call]` or `[Notes]`, and `assumed` becomes `[Inferred]`, so an assumed item is never used as the claim. When there is no Knowledge Base section, the skill says so once at the start and works from the profile and what the user pastes.

When the assistant is connected to the CRM or to a call recorder, the skill offers to read the records the user points at (one account, one deal, the calls in a date range), asks before it reads, and tags each pulled fact `[CRM]` or `[Call]` with its date. It reads only. It never searches records nobody named and never writes back. Without a connector, pasting the same records works the same way.

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

Your playbook for MEDDPICC scoring. The 8 elements, weighting system, 1-5 scoring rubrics, health calculation, stage minimums, stage recommendation rules, risk patterns and coaching framework are your operational blueprint.

### The Eight MEDDPICC Elements and Weights

| Element | Weight | What It Measures |
|---------|--------|-----------------|
| **M. Metrics** | 15% | Are success metrics defined and aligned? |
| **E. Economic Buyer** | 20% | Is the budget owner identified and engaged? |
| **D. Decision Criteria** | 10% | Do we know the evaluation criteria? |
| **D. Decision Process** | 10% | Do we understand the buying process and committee? |
| **P. Paper Process** | 10% | Are legal, security, and procurement mapped? |
| **I. Identified Pain** | 15% | Is business pain confirmed and quantified? |
| **C. Champion** | 15% | Is there an active internal advocate? |
| **C. Competition** | 5% | Do we understand the competitive landscape? |

### MEDDPICC Scoring Rubrics (1-5 Scale)

Score each element against its rubric using the evidence in the record. Tag every fact in the evidence column with one of the six shared evidence tags.

#### M. Metrics (Weight: 15%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Success metrics defined, baseline measured, target improvements quantified, ROI agreed with economic buyer. |
| 4 | Metrics discussed, prospect shared current-state numbers. ROI framework shared but not formally agreed. |
| 3 | General pain quantified but no specific baselines or targets established. |
| 2 | Pain acknowledged but not quantified. No numbers shared. |
| 1 | No metrics discussion has occurred. |

#### E. Economic Buyer (Weight: 20%)
| Score | Evidence Required |
|-------|------------------|
| 5 | EB identified by name/title, attended meeting, confirmed budget, expressed personal investment. |
| 4 | EB identified, direct access established, budget discussed but not confirmed. |
| 3 | EB identified by name but no direct access. Communicating through champion only. |
| 2 | We think we know the EB based on title/org chart but haven't confirmed. |
| 1 | Economic buyer not identified. |

#### D. Decision Criteria (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Written evaluation criteria received. We map favorably to all critical criteria. We've influenced criteria toward our winning zones. |
| 4 | Criteria discussed verbally. Know must-haves vs. nice-to-haves. Strong on most. |
| 3 | Some criteria known from discovery. Haven't mapped to capabilities formally. |
| 2 | Vague sense of what matters. No specific requirements documented. |
| 1 | No discussion of evaluation criteria. |

#### D. Decision Process (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Full process mapped: steps, committee members by name, timeline with dates, approval sequence confirmed. |
| 4 | Process mostly understood. Key steps and stakeholders known, some dates fuzzy. |
| 3 | General process known. Specific stakeholders and dates not confirmed. |
| 2 | Champion said "I'll handle it internally" without specifics. |
| 1 | No discussion of decision process. |

#### P. Paper Process (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Legal requirements known, procurement mapped, contract terms discussed, signature authority confirmed. |
| 4 | Most paper process understood. MSA structure known. Legal review expected, timeline estimated. |
| 3 | Aware legal/procurement review exists but details unclear. |
| 2 | Paper process assumed based on company size, not confirmed. |
| 1 | No discussion of paper process. |

#### I. Identified Pain (Weight: 15%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Multiple pains across stakeholders, quantified impact in prospect's words, urgent timeline, maps to winning zones. |
| 4 | Primary pain clearly articulated with some quantification. Urgency present but not deadline-driven. |
| 3 | Pain acknowledged but generic. Not quantified. No expressed urgency. |
| 2 | We think there's pain based on profile, but prospect hasn't confirmed. |
| 1 | No pain identified. Deal is feature-led or relationship-led. |

#### C. Champion (Weight: 15%)
The champion status comes first, from the shared champion tests in the Shared Contract: Strong, Developing or None, read from the record as it stands on the run date. The rubric row then follows the status and the evidence the record shows today.

| Score | Evidence Required |
|-------|------------------|
| 5 | Champion status Strong, with each test met tagged. At least one test shows active selling inside the buying committee on our behalf. |
| 4 | Champion status Strong or Developing, engaged, shows investment and has introduced stakeholders. Active internal selling not yet shown. |
| 3 | Champion status Developing, with one or two tests met. Influence over the decision is unknown or limited. |
| 2 | Contact engages in meetings but shows no championing signs on the current record. Evaluating, not advocating. |
| 1 | No champion identified. Engaging with someone who can't influence the decision. |

#### C. Competition (Weight: 5%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Competitive landscape fully understood. Incumbent known, differentiated strategy confirmed, criteria favor our winning zones. |
| 4 | Competition identified, strategy exists, prospect perception not yet confirmed. |
| 3 | Competitor or alternative known but no specific strategy. |
| 2 | Competition suspected but not confirmed. |
| 1 | No competitive intelligence. |

### Health Score Calculation & Interpretation

**Formula:** For each element, multiply its score (1-5) by its weight written as a decimal (15% is 0.15). Sum all weighted scores. Divide the sum by 5 and multiply by 100. A deal scored 5 on every element gives a sum of 5.00, and 5.00 ÷ 5 × 100 = 100.

| Health Score | Health | Meaning |
|-------|--------|---------|
| 80 to 100 | GREEN | Strong. Well-qualified, progressing. Focus on execution. |
| 60 to 79 | YELLOW | Moderate risk. Key gaps addressable. Fill gaps before advancing. |
| 40 to 59 | ORANGE | High risk. Multiple weak elements. Consider re-qualifying. |
| 0 to 39 | RED | Critical. Lacks fundamentals. Downgrade or disqualify. |

### Stage-Appropriate Minimums

| Profile Stage | Min Health | Critical Elements at Floor |
|-------|-----------|----------------------|
| Stage 2 Discovery | 30 or higher | Identified Pain at 3 or higher |
| Stage 3 Demo and Stage 4 Proposal | 50 or higher | Identified Pain, Champion and Decision Criteria at 3 or higher |
| Stage 5 Negotiate | 65 or higher | All except Competition at 3 or higher, and Economic Buyer at 4 or higher |
| Stage 6 Closed-Won and Handoff | 75 or higher | All at 3 or higher, and Economic Buyer and Paper Process at 4 or higher |

Stage names come from the client profile's Qualification Stage Gates. Stage 1 Target has no minimum because no element is scored before a deal is active. If the team overrides these minimums in its MEDDPICC profile section, the override is used, and the report says it was used. Where the profile's Qualification Stage Gates state a different score than this table, the profile's figure is the minimum, because the profile is the only source of company facts and a stage gate is one. The report names the figure it used and shows the table's default beside it.

### Stage Recommendation Rules

Apply the stage minimum check, the gap ranking and the risk patterns first. Then pick one word.

1. **ADVANCE** when the health score meets the next stage's minimum and every critical element for the next stage is at its floor. Reason: the record supports the next stage's exit criteria, so the stage can move.
2. **HOLD** when the deal meets its current stage minimum but not the next, or when it misses its current minimum and every failed element has a dated action that can close the gap. The deal stays where it is, and the dated actions go on the record. Reason: a missed minimum with a date in hand is a plan, not a loss.
3. **DOWNGRADE** when a HOLD's dated action passes without closing the gap. The deal moves back one stage. A deal whose Identified Pain scores 3 or higher never goes back to Stage 2 Discovery, because the pain is already confirmed. Reason: the stage must say what the buyer has actually done, and confirmed pain does not undo.
4. **DISQUALIFY** when the health score is in the RED band and Identified Pain scores 1, meaning no pain was identified. Reason: a deal with no pain has no reason to buy, and no stage move fixes that.

The profile's Qualification Stage Gates set the exit criteria for each stage. This skill's score is one part of those criteria, not the whole gate.

### Risk Patterns to Flag

| Pattern | Evidence | Action |
|---------|----------|--------|
| Happy ears | High confidence, low CRM evidence | Manager should join next call |
| Single-threaded | Only one contact, no multi-stakeholder meetings | Multi-thread immediately |
| Zombie deal | Same stage >45 days, no recent activity | Re-engage or downgrade |
| Close date fantasy | 2+ slips, or close <30 days with Paper ≤2 | Reset close date (+30 days minimum) |
| Feature-led deal | No documented pain, demo notes focus on features shown | Go back to discovery |
| Competitor blind | No competitive intel past Stage 2 Discovery | Ask directly about alternatives |

---

## Quick Reference

**Use this skill when:**
- Deep-diving a specific deal's qualification gaps
- Preparing coaching recommendations for a rep's deal
- Deciding whether to advance, hold, downgrade or disqualify a deal stage
- Running pipeline reviews with weighted health scoring

**Don't use when:**
- You need a quick health check across signals (use `gtm-deal-pulse`)
- The account has no active opportunity (use `gtm-account-qualification`)
- You need meeting-specific coaching on one call (use `gtm-call-coaching`)

**User roles:** AE, Sales Manager, VP Sales

**Expected time:** 20-30 minutes per deal

---

## Core Workflow

The steps run in this order because each one feeds the next. Scores must cite a record, so the data pull comes first. The stage recommendation comes last because its rules read the minimum check, the critical elements and the risk patterns.

### Step 1: Pull Deal Data from CRM

Before pulling anything, read the account's folder under `accounts/` and the competitors under `gtm/` in the knowledge base, when the profile has one. Then offer to read the CRM deal record and, when a call recorder is connected, the deal's calls, and ask before reading either, as set out in The Knowledge Base and Connectors.

Query the CRM for the account. Extract the deal basics (account, amount, stage and days in stage, close date and slip history, owner, supporting team, deal origin), the engagement history (touchpoints, last activity, meeting dates and participants), the contact records (name, title, department, seniority, meeting attendance versus email only), the deal notes (next steps, objections, competitors named, budget and timeline signals) and any prior closed-lost record at this account.

Read the Deal Pulse, Call Coaching and Stakeholder Mapping fields by name when those outputs exist. Use them to focus the check, and never as evidence for an element on their own. When one is absent, say so.

**Produces:** The deal profile, held for the steps below, with each field tagged. Missing fields are `[Unknown]`.

### Step 2: Score All 8 MEDDPICC Elements

Score each element against its rubric in {Methodology: MEDDPICC Scoring Rubrics}. Be honest. Add the client context for each element.

**Client context by element:**
- **Metrics:** look for the numbers in `{Client Profile: Value Propositions}`, such as time saved, cost reduced, compliance rates or volume. Use the team's own metric wording from the MEDDPICC section.
- **Economic Buyer:** use the economic-buyer persona from `{Client Profile: Buyer Personas}`, the one that owns budget.
- **Decision Criteria:** push toward `{Client Profile: Qualification Criteria}`, and redirect away from areas where competitors are stronger.
- **Decision Process:** a "we'll handle it internally" answer without dates scores 2, not 3.
- **Paper Process:** score against the team's paper steps in the MEDDPICC section. If the close date is less than 60 days away and Paper Process scores below 3, the close date is almost certainly wrong.
- **Identified Pain:** map to `{Client Profile: Core Pain Points}`. A deal without confirmed pain is a deal without a reason to buy.
- **Champion:** read the champion status from the shared champion tests, then pick the rubric row. The validation questions are whether the champion has given EB access, shared internal context, forwarded content, told us about objections, or helped navigate procurement.
- **Competition:** reference `{Client Profile: Competitive Landscape}` for the incumbent, its type and any displacement proof points. The number one competitor is always inertia, so assess how urgent the buyer is to overcome doing nothing.

**Coaching for low scores:** if an element is below 3, say what question would move it. For Economic Buyer, ask the champion: "If you decided this was the right move, could you make it happen, or does someone else need to approve?"

**Produces:** Eight scores, each with its tagged evidence and its primary gap.

### Step 3: Compute Weighted Deal Health and the Stage Minimum Check

Multiply each score by its weight, sum the results, and divide by 5 then multiply by 100. Round to a whole number. Show the table with every row (Example 1 is the form to follow). Then compare the health score and each critical element to the minimum for the deal's stage.

**Produces:** The weighted table with its Total row, `health_score`, and `stage_minimum_met` (Yes or No, with each failed critical element named and its required score).

### Step 4: Identify Critical Gaps and Risks

Rank the gaps by severity:
1. Any element scoring 1 past Stage 2 Discovery: **critical blocker**.
2. Economic Buyer or Identified Pain at 2 or lower at any stage: **deal killer if not addressed**.
3. Champion at 2 or lower past Stage 2 Discovery: **no internal advocate, running on hope**.
4. Paper Process at 2 or lower with the close date less than 60 days away: **close date is wrong**.
5. Decision Process at 2 or lower from Stage 3 Demo on: **being evaluated without knowing the rules**.

Then check the risk patterns in the Methodology table. Name each pattern that the record shows, with its evidence tag.

**Produces:** The top three risks, each with what it is, why it matters at this stage and what to do, and `risk_patterns`.

### Step 5: Generate Coaching Recommendations

Generate five prioritized next actions, each targeting a specific MEDDPICC gap. Each action names the methodology step it uses from `{Client Profile: Sales Methodology}`, the owner (AE, BDR, SE or manager), a deadline (five business days for critical gaps, ten for moderate ones) and a success criterion that shows the action worked.

**Produces:** Five actions, each with element targeted, owner, deadline and success criterion.

### Step 6: Set the Stage Recommendation

Apply the Stage Recommendation Rules in Methodology to the stage minimum check (Step 3), the gaps (Step 4) and the actions (Step 5). Pick one word: ADVANCE, HOLD, DOWNGRADE or DISQUALIFY. Give the reason, and for HOLD or DOWNGRADE give the dated action and the date it is checked.

**Produces:** `stage_recommendation`, one word, with its rationale and dated action.

### Step 7: Deliver the Analysis Inline

Return the analysis in the chat, in this order: the deal summary banner (account, amount, stage, days in stage, AE, close date, health score and its band word), the MEDDPICC scorecard with the weighted table, the stage check, the gap analysis and top three risks, the five actions, the stage recommendation, and the last line `next_action`.

Write a file only when the user asks for one, named `<account>_gtm-meddpicc-analysis_<date>.md`.

**Produces:** The inline analysis with every Output Contract field, and `report_path` set to `none (inline)` unless a file was written.

---

## Epistemic Rules

- **Only score what is evidenced in the record.** No evidence means a low score. Do not inflate. An element with no evidence scores at the lowest row of its rubric and carries `[Unknown]`, never a guess.
- **Tag every fact** with one of the six shared evidence tags. A fact with no tag is removed from the analysis.
- **Distinguish confirmed from claimed.** A champion the rep claims is selling internally differs from one whose internal activity the record shows. Score the record.
- **Print n beside every rate.** "4 of 8 elements at 4 or higher" is readable. A rate shown without its count is not.
- **Silence is not a no.** A blank CRM field is unknown, counted in no denominator, and written as `[Unknown]`. It is not scored as a refusal.
- **Five cases before a pattern.** One deal shows an observation. A gap that repeats across deals needs five cases before it is named as a pattern.
- **"No difference found" is a finding.** When Deal Pulse and this analysis disagree, both are reported with their dates. The difference is shown, not smoothed over.

---

## Hard Rules

1. **Never score a rep's self-assessment.** The rep's confidence is the thing this skill exists to check. Reason: a score built on confidence cannot tell a deal that is progressing from one that is merely liked.
2. **Score all eight elements.** Reason: a skipped element hides the weakest one, and the weakest element is usually the one that loses the deal.
3. **Never score on potential.** "They are a great company" is not a MEDDPICC score. Reason: potential does not show a buyer's approval path.
4. **Never average without weights.** Reason: the weights set the priority. Economic Buyer at 20% outweighs Competition at 5% for a reason.
5. **Never move a stage back to Stage 2 Discovery when Identified Pain scores 3 or higher.** Reason: the pain is already confirmed, and a return to Discovery tells the team the deal was never real.
6. **Never return a stage recommendation without the stage minimum check.** Reason: the stage word is only as good as the minimum and critical-element check that produced it.
7. **Never send, enroll, or write to the CRM.** Reason: the rep reads the analysis first, and the rep is accountable for what the buyer receives.

---

## Quality Bar

**Done when all are true:**
- [ ] All 8 elements scored 1-5, each with tagged evidence or an `[Unknown]` tag
- [ ] Every fact in the analysis carries one of the six shared evidence tags
- [ ] The weighted table shows every row, and its Total equals the sum of its Weighted cells
- [ ] `health_score` equals the Total divided by 5 and multiplied by 100, rounded, and its band word matches the health table
- [ ] The stage minimum check names each failed critical element and its required score
- [ ] The stage recommendation is one of ADVANCE, HOLD, DOWNGRADE or DISQUALIFY, with a reason and a dated action where the rules call for one
- [ ] The gap analysis ranks the deal-killing elements first
- [ ] Coaching references a named step from the team's sales methodology
- [ ] Five actions are listed, each with owner, deadline and success criterion
- [ ] Stage names come from the profile's gates and no other list
- [ ] No placeholder brackets remain in the output, except `[Unknown]` tags

---

## Examples

### Example 1: Flagship Deal at Negotiate, First Run (Brackhaven Memorial Gardens, 2026-09-28)

**Context:** Brackhaven Memorial Gardens, a combination of two sites with 11,000 plots (profile). Owen Pruitt is the AE (illustrative assignment). The deal has been ACTIVE at Stage 5 Negotiate since 2026-09-09, so this run is on day 19 in stage. Amount: $21,576 a year at list, which is two sites at the $10,788 list price per site (profile), plus the $5,000 setup once (profile). Close date: the family board meeting on 2026-11-12 (CRM). Champion: GM Ruth Ellery. Economic buyer: the family board chair, name `[Unknown]`, who joined one call in Stage 4 Proposal. The same day's Deal Pulse reads 72, Medium Risk (08). The two instruments score different things, so the two numbers differ. Both are shown with their date.

**Input:** "Run MEDDPICC deal analysis for Brackhaven Memorial Gardens."

**Scoring summary:**
- **Metrics: 4 of 5.** Ruth gave the plot count, 11,000 (profile), and the hours her team spends on the trust fund report (`[Call]`, illustrative). The ROI framework was shared, not yet agreed `[Call]`.
- **Economic Buyer: 4 of 5.** The family board chair is identified by title. Direct access was established on one call `[CRM]`. Budget was discussed, not confirmed `[Call]`.
- **Decision Criteria: 4 of 5.** Must-haves are known from discovery and the deal maps to them strongly `[Call]`. The pre-need module is a nice-to-have `[Call]`.
- **Decision Process: 4 of 5.** The committee is mapped: board, GM and Operations Director `[CRM]`. The board meets 2026-11-12 `[CRM]`. The approval sequence is partly confirmed `[Notes]`.
- **Paper Process: 3 of 5.** Aware that legal and vendor review exists `[Notes]`. The steps and timing are not scoped `[Unknown]`.
- **Identified Pain: 5 of 5.** One double sale in 24 months `[CRM]` (illustrative), trust fund reporting done by hand `[Call]`, and Ruth put a cost on each in her own words `[Call]` (illustrative).
- **Champion: 5 of 5.** Ruth Ellery is Strong: four of seven shared champion tests met, each tagged `[Call]`. She is selling internally, shared the board's questions with us, and coached us on Walt Okonkwo's objection to tablets `[Call]`.
- **Competition: 4 of 5.** Oldgate Ledger Pro is the incumbent, direct software, renewal March 2027 `[CRM]`. Stonemark was evaluated with no preference stated `[Call]`. A strategy exists and is not yet tested with the buyer `[Notes]`.

**Weighted score:**
| Element | Weight | Score | Weighted (score × weight) |
|---|---|---|---|
| Metrics | 15% (0.15) | 4 | 0.60 |
| Economic Buyer | 20% (0.20) | 4 | 0.80 |
| Decision Criteria | 10% (0.10) | 4 | 0.40 |
| Decision Process | 10% (0.10) | 4 | 0.40 |
| Paper Process | 10% (0.10) | 3 | 0.30 |
| Identified Pain | 15% (0.15) | 5 | 0.75 |
| Champion | 15% (0.15) | 5 | 0.75 |
| Competition | 5% (0.05) | 4 | 0.20 |
| **Total** | **100%** | | **4.20** |

**Health:** 4.20 ÷ 5 × 100 = **84, GREEN**.

**Stage check:** The PlotIQ profile's Qualification Stage Gates set the Stage 5 Negotiate minimum at 70 or higher, which overrides the table's default of 65, and it is met at 84. Critical elements: all except Competition are at 3 or higher, and Economic Buyer is at 4 or higher, so met. The Stage 6 Closed-Won and Handoff minimum is 75 or higher and is met on health, but it is not met on the critical elements, because Paper Process is 3 and needs 4 or higher.

**Gaps and risks:** The top risk is Paper Process at 3, the one element holding the deal from Stage 6. The second is the board chair's name, which is `[Unknown]`, so Economic Buyer is identified by title only. The third is the ROI framework, which is shared but not agreed.

**Next actions:**
1. Owen Pruitt asks Ruth Ellery to walk through the legal and vendor steps with him, by 2026-10-05. Element: Paper Process. Owner: AE. Success: each step has an owner and a date in the CRM.
2. Owen asks Ruth for the board's approval sequence and confirms the 2026-11-12 meeting, by 2026-10-05. Element: Decision Process. Owner: AE. Success: each approval step names a person.
3. Owen asks Ruth to arrange a second call with the board chair, by 2026-10-12. Element: Economic Buyer. Owner: AE. Success: the chair states the budget on the call and the name is recorded.
4. Lena Vasquez, Sales Manager, joins the next call with the board chair, by 2026-10-12. Element: Economic Buyer and happy ears check. Owner: manager. Success: the manager records what the chair commits to.
5. Owen agrees the ROI framework with Ruth in writing, by 2026-10-12. Element: Metrics. Owner: AE. Success: the framework is agreed by Ruth and filed on the record, moving Metrics to 5.

**Stage Recommendation: HOLD at Stage 5 Negotiate.** The deal passes the Stage 5 minimum and misses the Stage 6 minimum on Paper Process alone. Its dated actions close that gap by 2026-10-05, and the board date sits on the calendar for 2026-11-12. The deal moves to Stage 6 when Paper Process reaches 4 and the board approval date is confirmed.

```text
Hand-off (read by 10, 11 and 14):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-09-28
meddpicc_scores: Metrics 4, Economic Buyer 4, Decision Criteria 4, Decision Process 4, Paper Process 3, Identified Pain 5, Champion 5, Competition 4
health_score: 84
stage_minimum_met: Yes for Stage 5 Negotiate (70 or higher, from the profile's stage gates). No for Stage 6 Closed-Won and Handoff (75 or higher), because Paper Process is 3 and needs 4
stage_recommendation: HOLD
risk_patterns: none flagged on the evidence. Economic Buyer identified by title only, name [Unknown]
next_action: Owen Pruitt asks Ruth Ellery to walk through the legal and vendor steps by 2026-10-05
report_path: none (inline)
```

### Example 2: Same Deal Three Weeks Later, Below the Stage Minimum

**Context:** Brackhaven again, on 2026-10-19, three weeks after Example 1 and day 40 in Stage 5 Negotiate. The board date has slipped twice and is not confirmed. Ruth has not replied since 2026-10-03, which is 16 days `[CRM]`. The board chair has joined one call, in Stage 4 Proposal. The same day's Deal Pulse reads 38, High Risk (08). The CRM still shows Stage 5 Negotiate. This is the non-success case.

**Input:** "MEDDPICC score Brackhaven again. It's still in Negotiate."

**Scoring summary:**
- **Metrics: 3 of 5.** General pain is quantified `[Call]`, but the ROI numbers have not been updated since the board date moved `[Notes]`.
- **Economic Buyer: 3 of 5.** The board chair is identified by title, name `[Unknown]`. There has been no direct access since the one call `[CRM]`. We communicate through Ruth only `[Notes]`.
- **Decision Criteria: 3 of 5.** Some criteria are known `[Call]`. Stonemark is still being evaluated and the criteria it is judged on are not on the record `[Notes]` (illustrative).
- **Decision Process: 2 of 5.** Ruth said "I'll take it to the board" with no date and no approval sequence `[Notes]`.
- **Paper Process: 3 of 5.** Aware that legal and vendor steps exist, details unclear `[Notes]`.
- **Identified Pain: 4 of 5.** The primary pain is clear and partly quantified `[Call]`. The March 2027 Oldgate renewal is the deadline behind the board date `[CRM]`, but the deal has not tied its own date to it.
- **Champion: 2 of 5.** Champion status is Strong on the 2026-09-28 record, with four of seven shared champion tests met `[Call]`. No test has been repeated on the record since 2026-10-03, and Ruth has been silent for 16 days `[CRM]`. The rubric row for a contact with no championing signs on the current record applies, so the score is 2, not 5.
- **Competition: 3 of 5.** Stonemark is still in the evaluation with no preference stated `[Call]`, and no written position against it is on the record `[Notes]` (illustrative).

**Weighted score:**
| Element | Weight | Score | Weighted (score × weight) |
|---|---|---|---|
| Metrics | 15% (0.15) | 3 | 0.45 |
| Economic Buyer | 20% (0.20) | 3 | 0.60 |
| Decision Criteria | 10% (0.10) | 3 | 0.30 |
| Decision Process | 10% (0.10) | 2 | 0.20 |
| Paper Process | 10% (0.10) | 3 | 0.30 |
| Identified Pain | 15% (0.15) | 4 | 0.60 |
| Champion | 15% (0.15) | 2 | 0.30 |
| Competition | 5% (0.05) | 3 | 0.15 |
| **Total** | **100%** | | **2.90** |

**Health:** 2.90 ÷ 5 × 100 = **58, ORANGE**.

**Stage check:** The PlotIQ profile's Qualification Stage Gates set the Stage 5 Negotiate minimum at 70 or higher, which overrides the table's default of 65, and it is not met at 58. Critical elements failed: Economic Buyer (3, needs 4), Decision Process (2, needs 3) and Champion (2, needs 3).

**Risk patterns:**
- Close date fantasy: two slips, and the board date is not confirmed `[CRM]`.
- Happy ears: "I'll take it to the board" with no date behind it `[Notes]`.
- Single-threaded: Ruth is the only contact who has replied `[CRM]`.

**Next actions:**
1. Owen Pruitt asks Ruth Ellery for the board date, by 2026-10-23. Element: Decision Process (2 to 3). Owner: AE. Success: a dated board meeting is on the record.
2. Owen asks Ruth for a call with the board chair, by 2026-10-23. Element: Economic Buyer (3 to 4). Owner: AE. Success: the chair attends and states the budget.
3. Lena Vasquez, Sales Manager, joins the next call with Ruth, by 2026-10-23. Element: Champion (2 to 3). Owner: manager. Success: Ruth commits to a dated next step on the call.
4. Owen re-runs the ROI numbers with Ruth now that the board has moved, by 2026-10-26. Element: Metrics (3 to 4). Owner: AE. Success: current-state numbers are on the record.
5. Owen asks Ruth which criteria Stonemark is being judged on and writes a position against it, by 2026-10-26. Element: Decision Criteria (3 to 4). Owner: AE. Success: the criteria are on the record and a Stonemark position is written.

**Stage Recommendation: HOLD at Stage 5 Negotiate, with a dated action.** Owen asks Ruth for the board date by 2026-10-23. If the board date is not confirmed by 2026-11-02, the deal moves one stage back to Stage 4 Proposal. It does not return to Stage 2 Discovery, because the Identified Pain is 4 and the pain is confirmed.

At Stage 4 Proposal this deal also misses the Champion minimum, which is 3 or higher, so the stage move does not fix the score. It brings the forecast in line with the buyer's real date. The deal returns to Stage 5 only when health reaches 65 and the board chair has been met directly.

```text
Hand-off (read by 10, 11 and 14):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
meddpicc_scores: Metrics 3, Economic Buyer 3, Decision Criteria 3, Decision Process 2, Paper Process 3, Identified Pain 4, Champion 2, Competition 3
health_score: 58
stage_minimum_met: No for Stage 5 Negotiate (70 or higher, from the profile's stage gates). Failed critical elements: Economic Buyer (3, needs 4), Decision Process (2, needs 3), Champion (2, needs 3)
stage_recommendation: HOLD
risk_patterns: Close date fantasy (two slips, board date unconfirmed), happy ears ("I'll take it to the board" with no date), single-threaded
next_action: Owen Pruitt asks Ruth Ellery for the board date by 2026-10-23. If it is not confirmed by 2026-11-02, the stage moves to DOWNGRADE, Stage 4 Proposal
report_path: none (inline)
```

---

## Common Patterns

### Pattern: The Pulse and the MEDDPICC Disagree

Deal Pulse scores sixteen signals in four pillars, and this skill scores eight elements. A deal can read Yellow on one and ORANGE on the other, and both can be right. Report both with their dates, name the element or signal that drives the gap, and act on the element. Example 1 shows the form on 2026-09-28, where Pulse reads 72 and MEDDPICC reads 84.

### Pattern: The Same Deal Re-Scored After a Slip

Re-run this analysis after every stage date or close date changes, and compare the two runs element by element. A deal whose score drops while its stage stays the same is showing the slip in the record. Example 2 is that case on 2026-10-19: the score falls from 84 to 58 and the stage holds, which is the signal for the HOLD rule with a dated action.

---

## Troubleshooting

### "The weighted score seems wrong"
**Cause:** Math error in weighting. **Solution:** Verify weights sum to 100% and the formula is `(sum of score × weight) / 5 × 100`. Each element contributes its score (1-5) × its weight as a decimal (15% is 0.15).

### "Rep disagrees with low scores"
**Cause:** Gap between rep knowledge and CRM evidence. **Solution:** Score based on evidence. Suggest the rep log their intelligence to the CRM so the next run reflects it. Frame it as: "The CRM tells one story. Let's make sure it tells the right one."

### "The champion score looks stale"
**Cause:** The shared champion tests are met on an earlier call and nothing has been repeated since. **Solution:** Read the status as it stands on the run date. Name the date of the last test met, and score the rubric row the current record supports. Ask the rep for the next dated action that would put a test back on the record.

### "Multiple deals requested at once"
**Cause:** Manager wants portfolio view. **Solution:** Run MEDDPICC on each deal individually, then create a summary table comparing health scores and common gap patterns across the portfolio. A gap common to the portfolio needs five cases before it is named as a pattern.

### "The stage is below its minimum and the date has not passed"
**Cause:** A gap is open but its dated action is still in time. **Solution:** Recommend HOLD with the dated action, and set the date the stage will be checked. Do not recommend DOWNGRADE early. The rule moves a deal only after the date passes.

---

## Best Practices

### Do's
- **Use the weighting system.** Economic Buyer at 20% is weighted highest for a reason.
- **Flag risk patterns.** "Happy ears" and "zombie deal" are the most common pipeline killers.
- **Connect coaching to specific frameworks.** Name the step from the team's own sales methodology, not generic advice.
- **Compare health to stage minimums.** A deal at Stage 6 Closed-Won and Handoff with health below 75 needs attention.
- **Show both instruments when they disagree.** The two dates are the explanation.

---

## Integration With Other Skills

**Reads from the skills before it, by field name.** A missing field is reported as missing, not rebuilt here.

- **Deal Pulse (08).** Reads `health_score`, `risk_level`, `pillar_scores`, `signal_scores` and `next_actions`. Used to focus the check and to compare the two instruments. Never used as evidence for an element on its own.
- **Call Coaching (13).** Reads `call_score`, `category_scores`, `focus_area`, `coaching_points`, `key_moments` and `champion_status`. A coaching point counts as evidence only with its quote or its grade attached.
- **Stakeholder Mapping (10).** Reads `threading_score`, `buying_roles`, `ghost_nodes` and `champion_status`. A ghost node counts against the Economic Buyer and Decision Process evidence until someone is named.

**Hands to the skills after it, by field name.**

- **Stakeholder Mapping (10).** Reads `meddpicc_scores`, `health_score`, `stage_minimum_met`, `stage_recommendation` and `risk_patterns`.
- **Competitive Strategy (11).** Reads `meddpicc_scores` for the Competition element, with `stage_recommendation` and `risk_patterns` for context.
- **Sales Handoff (14).** Reads `meddpicc_scores`, `stage_minimum_met` and `stage_recommendation` to check the deal is ready to move to Stage 6 Closed-Won and Handoff.

**Hands to the close.** Wrap-Up reads `report_path` when a file was written, the `health_score` as the score, and `next_action` with its owner and date.

**Related skills:** Call Coaching (13) after a call, to see whether the new intel changes any element score. Meeting Prep (06) uses the gaps to set the meeting's target, for example "this meeting should target Economic Buyer access and Decision Process mapping."

### Chains

- **Work The Deal:** Meeting Prep (06), Call Coaching (13), Deal Pulse (08), **MEDDPICC Analysis (09)**, Stakeholder Mapping (10). This skill adds the eight-element score and the stage recommendation.
- **Beat The Incumbent:** **MEDDPICC Analysis (09)**, Competitive Strategy (11), Competitive Displacement (12), Account Snapshot (02) or Meeting Prep (06). This skill adds the Competition element and the stage check that sets how urgent the plan is.
- **Close And Hand Off:** **MEDDPICC Analysis (09)**, Sales Hand-Off (14), Wrap-Up (O10). This skill adds the stage minimum check that decides whether the deal is ready to move to the handoff stage.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name. This skill is free and works without any kit. This skill also reads the kit's hand-off block back as optional context (`case_status`, `hard_value`, `payback_months_hard`, `open_bets` and `next_action`), and it never presents an ASSUMPTION line from the kit as a buyer fact. The fields the kit reads from this skill:

- `meddpicc_scores` (the Metrics and Economic Buyer elements)
- `stage_recommendation` (below 4 on Metrics, where the case says the metrics are not yet agreed)

---

## Changelog


### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`, and the competitors under `gtm/`) and offers read-only CRM connectors through the shared contract's Knowledge Base and Connectors section, before the CRM deal read.
- Adds a Chains subsection placing the skill in the Work The Deal, Beat The Incumbent and Close And Hand Off chains.
- Adds a Guild Pro Kits subsection naming the hand-off fields the Business Case & ROI Kit reads, and the kit's fields this skill reads back.

### 2.0.1 (2026-10-20)

- The profile's Qualification Stage Gates figure is the stage minimum when the profile states one, and the report names the figure it used with the table's default beside it (Ryan, 2026-10-20). The PlotIQ examples use the profile's 70 for Stage 5 Negotiate.
### Version 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle and the platform line, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, Core Workflow with a Produces line per step, Epistemic Rules, Hard Rules with reasons, Quality Bar, and Integration with named hand-off fields.
- Stage names come from the profile's Qualification Stage Gates, written as Stage 2 Discovery and so on. No other stage list remains.
- The champion element reads the status from the shared champion tests, and the rubric row follows the status and the record as it stands on the run date.
- Stage recommendation words are ADVANCE, HOLD, DOWNGRADE and DISQUALIFY. The rules are written out, and they match Deal Pulse on the same deal: HOLD with a dated action, then one stage back if the gap stays open, never back to Discovery while the pain is confirmed.
- Health bands use the words GREEN, YELLOW, ORANGE and RED. The colour emoji are removed.
- Evidence labels replaced by the six shared tags. Every example fact is tagged.
- Hand-off fields named in the Output Contract, the Integration section and each example's hand-off block.
- Examples aligned to the PlotIQ chain file: Brackhaven at 84 on 2026-09-28, then 58 on 2026-10-19 with the HOLD rule and the 2026-11-02 DOWNGRADE to Stage 4 Proposal. The 1.3.0 downgrade to Discovery is removed.
- Weighted tables, weights, rubrics, stage minimums and risk patterns unchanged. The weighted tables are rechecked row by row.

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten onto a single example company
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- MEDDPICC element rubrics, weighting system, health calculation, stage minimums, risk patterns, and coaching framework moved to an explicit Methodology section, `{Methodology: X}` references
- No functional changes to the workflow, element definitions, scoring logic, examples, or output formats

### Version 1.0.0 (2026-03-04)

- Initial release
- Client-configurable via Client Profile block
- All 8 weighted elements, scoring rubrics, risk patterns, and coaching mappings preserved
- Vendor-agnostic CRM instructions
- Multi-format artifact generation
