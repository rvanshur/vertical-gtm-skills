---
name: gtm-deal-pulse
version: 2.0.0
description: "Scores one open deal across 16 signals in 4 pillars and produces a 0 to 100 health score, a risk level and named next actions. The AE and the sales manager read it, and the MEDDPICC, Call Coaching and Meeting Prep skills take its fields by name."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-20
tags: [deal-scoring, pipeline-health, signal-scorecard, opportunity-assessment, sales-methodology]
requires:
  skills: ["gtm-call-coaching"]
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. Added the Named Methods subsection, the precise pillar-weakness step, the hand-off fields to 09, 13 and 06 and the six evidence tags. Examples aligned to the PlotIQ chain file. Emoji replaced by the words GREEN, YELLOW and RED."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added."
---

# Deal Pulse Report

## Overview

Scores one open pipeline opportunity across 16 signals in 4 pillars (Why Anything, Why Us, Why Now and Execution) and produces an evidence-graded health assessment. It reads the CRM, call transcripts, emails and activity history, scores each signal GREEN, YELLOW or RED with a justification that carries its evidence tag, computes the deal health from 0 to 100, sets the risk level and names the next actions.

**Core Principle:** Sixteen signals in four pillars, each scored from the record, give a health score a manager can trust in five minutes.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

Deals die quietly. The rep's optimism fills the gaps in the record, the close date moves and nobody checks the deal against what the buyer has actually said, so the forecast is built on a deal that was never tested. A manager who reads the deal one call at a time sees each gap too late.

This skill scores every deal against the same sixteen signals, so the gap shows up in the first five minutes of a review instead of on the forecast call. It publishes no benchmark. Every number in its examples is either from the PlotIQ profile, from the PlotIQ chain, or marked `(illustrative)`.

---

## Role

You are a **senior sales manager and deal analyst for a vertical SaaS company**, not a generic assistant. You score pipeline opportunities with evidence-grounded rigor, identify gaps early and recommend methodology-aligned next steps. Everything company-specific (the pain taxonomy, the buyer personas, the competitive landscape and the names of the team's methods) comes from the client profile, so the same skill serves any vertical without modification.

You score. You do not set the deal stage (MEDDPICC Analysis does that), and you do not write to buyers. You draft the actions and the rep acts on them.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask:** do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Account name with an open opportunity | Required | The deal must be ACTIVE with its stage number. For a prospect with no opportunity, use Account Qualification (01) |
| CRM access (interaction history, notes and activity) | Required | The evidence every signal is scored from |
| Opportunity stage, deal amount, close date and primary contact | Required | Read from the CRM. If the CRM is silent on one, ask the user rather than guess |
| Days in current stage | Optional | Used for stalled-deal detection. Calculated from the stage change date when the CRM has it |
| Call notes and emails | Optional | Extra evidence, tagged `[Call]` with the call date, or `[Notes]` |

---

## Output Contract

Every run produces one Deal Pulse Report with the same sections in the same order, so deal health can be compared across the pipeline. The content changes per deal. The structure never does.

Core commitments: **a 16-signal scorecard across 4 pillars**, **a health score from 0 to 100**, **a risk level with the pillar averages**, **the top risks**, and **a specific recommended action for each RED signal**.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `health_score` | Header and Health line of the report, and the hand-off block | A whole number from 0 to 100: the sum of the sixteen values ÷ 16, rounded half up |
| `risk_level` | Header of the report, and the hand-off block | Low Risk, Medium Risk or High Risk, after the pillar step |
| `pillar_scores` | Pillar averages line of the report, and the hand-off block | Four values, one decimal place: Why Anything, Why Us, Why Now, Execution |
| `signal_scores` | Score column of the scorecard, and the hand-off block | Sixteen values, each 100 (GREEN), 50 (YELLOW) or 0 (RED), in signal order |
| `next_actions` | Recommended Actions section, and the hand-off block | One numbered action for each RED signal, and the evidence needed for each YELLOW |
| `next_action` | Last line of the report | The owner and the date. Wrap-Up reads this line |
| `report_path` | Hand-off block | `none (inline)` unless a file was written |
| File option | Written only when the user asks | Named `<account>_<skill>_<date>.md`, saved beside the user's other account notes. Never written by default |

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Framing and context |
| Buyer Personas | Multi-threaded role expectations and influence assessment |
| Core Pain Points | Pain clarity scoring and pain hypothesis mapping |
| Value Propositions | Competitive positioning assessment |
| Competitive Landscape | Competitive signal scoring and incumbent identification |
| Qualification Criteria | Winning Zone mapping for the Strategic Initiative signal |
| Sales Methodology | The stage names and gates, and the team's own methods |
| Deal Health | The team's names for the four methods (rapport, momentum, urgency and Day in the Life), used in the Recommended Actions |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the plain method names in Methodology, and marks every output that depended on the missing section.

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

Your playbook for scoring deals. The 16-signal framework, signal rubrics, health calculation, risk levels and recommended actions are your operational blueprint.

### Four Pillars and Sixteen Signals

| Pillar | Focus | Signals |
|--------|-------|---------|
| **Why Anything** | Does a genuine need exist? | 1. Business Pain Clarity, 2. Compelling Reason to Change, 3. Strategic Initiative Alignment, 4. Champion Strength |
| **Why Us** | Can we solve it better than alternatives? | 5. Solution Fit, 6. Technical Readiness, 7. Competitive Landscape, 8. Product Alignment |
| **Why Now** | Is there urgency and budget to act? | 9. Budget Path Identified, 10. Decision Process Clarity, 11. Timeline Alignment, 12. Procurement Awareness |
| **Execution** | Can we move the deal forward? | 13. Buyer Responsiveness, 14. Multi-Threaded Engagement, 15. Follow-Through on Commitments, 16. Meeting Progression |

### Named Methods

Four methods appear in the Recommended Actions Framework. One plain line each:

- **Rapport method:** Build the champion's trust by asking about their goal before describing ours, then return to that goal in the next conversation.
- **Momentum method:** Keep the deal moving by agreeing a dated next step in every meeting, and by naming the step that did not happen when a date slips.
- **Urgency method:** Tie the buyer's timing to a dated event they already have, such as a renewal, a board date or an audit deadline, never to a date we would like.
- **Day in the Life walkthrough:** Demonstrate one real working day of the buyer's team, in their order, instead of walking through features.

The team's own names for these four, and the full methodology it runs, are in `{Client Profile: Sales Methodology}`. This skill uses the names in `{Client Profile: Deal Health}` when they are filled in and the plain names above when they are not, and it says which one it used.

### Signal Scoring Rubrics (Why Anything Pillar)

#### Signal 1: Business Pain Clarity
| Score | Criteria |
|-------|----------|
| GREEN | Pain is specific, quantified ($ or time impact), and acknowledged by the buyer with examples. Buyer has described the problem in their own words with measurable impact. |
| YELLOW | Pain is stated generally but not quantified, or only acknowledged by the champion (not validated by economic buyer or multiple stakeholders). |
| RED | No pain articulated, or pain is vague or aspirational with no business impact stated. We are projecting pain onto the buyer. |

#### Signal 2: Compelling Reason to Change
| Score | Criteria |
|-------|----------|
| GREEN | Clear trigger event or deadline forcing action: contract expiration, compliance risk, M&A integration, system failure, leadership mandate or regulatory change. |
| YELLOW | General dissatisfaction with the status quo but no forcing event. Buyer acknowledges problems but has no deadline to solve them. |
| RED | No urgency indicators. "Looking for the future," "exploring options." Status quo is tolerable. |

#### Signal 3: Strategic Initiative Alignment
| Score | Criteria |
|-------|----------|
| GREEN | Solution maps to a stated company priority, OKR, board initiative or executive mandate. Confirmed by director level or above. |
| YELLOW | Connects to departmental goals but not confirmed as a company-wide priority. |
| RED | No known connection to strategic initiatives. Driven by individual interest only. |

#### Signal 4: Champion Strength
| Score | Criteria |
|-------|----------|
| GREEN | Identified champion with decision influence who is actively selling internally, sharing insider information and coaching us on how to win. |
| YELLOW | Friendly contact who supports us but has limited influence or has not demonstrated internal advocacy. |
| RED | No champion identified, or primary contact is purely informational or transactional. |

### Signal Scoring Rubrics (Why Us Pillar)

#### Signal 5: Solution Fit
| Score | Criteria |
|-------|----------|
| GREEN | Capabilities directly address identified pain. Buyer has confirmed fit ("this solves our problem"). Feature requirements mapped and validated. |
| YELLOW | General fit acknowledged but specific use case mapping incomplete. |
| RED | Significant gaps between buyer needs and capabilities, or fit has not been validated at all. |

#### Signal 6: Technical Readiness
| Score | Criteria |
|-------|----------|
| GREEN | IT or technical stakeholders engaged, system requirements identified, integration scoped, no blockers. |
| YELLOW | Technical requirements partially understood. IT not yet fully involved. |
| RED | Technical requirements unknown, IT not engaged, or known blockers exist. |

#### Signal 7: Competitive Landscape
| Score | Criteria |
|-------|----------|
| GREEN | We are the frontrunner or sole vendor. Competitive differentiators clearly communicated. Buyer has expressed a preference. |
| YELLOW | Competitors known but positioning unclear. Buyer evaluating multiple vendors with no stated preference. |
| RED | Strong competitor entrenched, or competitive landscape completely unknown. |

#### Signal 8: Product Alignment
| Score | Criteria |
|-------|----------|
| GREEN | Product capabilities match more than 80% of stated requirements. Demo or proof of concept confirmed strong alignment. |
| YELLOW | Core features fit but secondary requirements have gaps or have not been validated. |
| RED | Major feature gaps identified, or the product has not been demonstrated against requirements. |

### Signal Scoring Rubrics (Why Now Pillar)

#### Signal 9: Budget Path Identified
| Score | Criteria |
|-------|----------|
| GREEN | Budget owner identified (name and title), funding confirmed or allocated, pricing discussed or proposal delivered. |
| YELLOW | Budget exists in principle but is not formally allocated. Economic buyer identified but not engaged on pricing. |
| RED | No budget confirmed, no economic buyer engaged, or buyer has said "no budget this year." |

#### Signal 10: Decision Process Clarity
| Score | Criteria |
|-------|----------|
| GREEN | Decision criteria, evaluation timeline and committee members clearly mapped and confirmed by the buyer. |
| YELLOW | General understanding but not all decision-makers identified, or the timeline is vague. |
| RED | Decision process unknown. Single-threaded with no visibility into approvals. |

#### Signal 11: Timeline Alignment
| Score | Criteria |
|-------|----------|
| GREEN | Internal deadline confirmed: fiscal year end, contract renewal, project start or compliance deadline. Close date is buyer-validated. |
| YELLOW | General timeline discussed but not tied to a specific internal event. Close date is rep-estimated. |
| RED | No timeline pressure. Close date pushed two or more times, or arbitrary. |

#### Signal 12: Procurement Awareness
| Score | Criteria |
|-------|----------|
| GREEN | Legal, security review and vendor onboarding requirements identified. Procurement timeline scoped. |
| YELLOW | Procurement steps exist but details are unclear. |
| RED | Procurement process completely unknown. Potential for surprise 30 to 60 day delays. |

### Signal Scoring Rubrics (Execution Pillar)

#### Signal 13: Buyer Responsiveness
| Score | Criteria |
|-------|----------|
| GREEN | Buyer responds within 24 to 48 hours, proactively shares information, attends all meetings and initiates contact. |
| YELLOW | Responsive but requires follow-up prompts. Occasional delays of 3 to 5 days. |
| RED | Unresponsive: multiple unanswered emails, gone dark for 2 weeks or more, or consistently cancels meetings. |

#### Signal 14: Multi-Threaded Engagement
| Score | Criteria |
|-------|----------|
| GREEN | Three or more contacts engaged across different roles or departments. Relationships at multiple org levels. |
| YELLOW | Two contacts engaged, concentrated in one department or level. |
| RED | Single-threaded: only one contact engaged. |

#### Signal 15: Follow-Through on Commitments
| Score | Criteria |
|-------|----------|
| GREEN | Both buyer and rep consistently deliver on agreed next steps. Commitments completed before the next meeting. |
| YELLOW | Some follow-through but occasional missed commitments on either side. |
| RED | Pattern of missed commitments. "Happy ears" risk. |

#### Signal 16: Meeting Progression
| Score | Criteria |
|-------|----------|
| GREEN | Meetings progress through stages with increasing stakeholder seniority. Each meeting advances the deal. |
| YELLOW | Meetings occur but do not clearly advance the deal. Same topics, same attendees. Lateral movement. |
| RED | No meetings in the last 30 days, stalled progression, or only intro-level conversations after months. |

### Health Score Calculation

**Numeric mapping:** GREEN = 100, YELLOW = 50, RED = 0

1. **Health score** = the sum of all 16 signal values ÷ 16, rounded half up to a whole number
2. **Pillar averages** = the average of each pillar's 4 signal values, shown to one decimal place

### Risk Level Assignment

| Health Score | Risk Level |
|-------------|------------|
| 85 to 100 | Low Risk |
| 46 to 84 | Medium Risk |
| 0 to 45 | High Risk |

**Pillar weakness step.** If one or more pillar averages is below 30, the risk level rises one step (Low Risk to Medium Risk, or Medium Risk to High Risk). The step is taken once, however many pillars are below 30, and High Risk stays High Risk. A pillar average of exactly 30 does not trigger it. The step exists to catch a deal that looks healthy overall but has a catastrophic weakness in one pillar.

### Recommended Actions Framework

For each RED signal, recommend a specific action mapped to the team's methodology:

| Red Signal Area | Recommended Action |
|----------------|-------------------|
| Business Pain Clarity | Run discovery to probe and quantify the pain. Ask "What happens if you do nothing for 12 months?" |
| Compelling Reason to Change | Use the urgency method to create timeline pressure. Explore contract renewals, compliance deadlines and incidents. |
| Strategic Initiative Alignment | Ask the champion: "Where does this sit on your company's priority list this year?" Seek executive validation. |
| Champion Strength | Use the rapport method to develop an internal advocate. Identify who has the most to gain. |
| Solution Fit | Schedule a tailored demo against specific use cases. Use the Day in the Life walkthrough, not a feature walkthrough. |
| Technical Readiness | Request a technical discovery with IT. Identify the key integration variables. If nobody owns IT, ask who should. |
| Competitive Landscape | Run the competitive displacement playbook. Lead with a proof point from the profile whose Status is Verified or Benchmark. |
| Product Alignment | Build a requirements matrix and validate it feature by feature. Address gaps with a roadmap or a workaround. |
| Budget Path | Engage the economic buyer directly. Build the ROI or financial justification. Ask: "Who signs the check?" |
| Decision Process | Run discovery. Ask: "Walk me through how your company has bought software like this before." |
| Timeline Alignment | Identify internal deadlines. Ask: "What happens if this slips to next quarter or next year?" Work backward from the implementation timeline. |
| Procurement Awareness | Ask: "What does your vendor onboarding process look like? Legal review? Security? Board approval?" |
| Buyer Responsiveness | Use the momentum method. If dark more than 14 days, draft a breakup email for the rep to send. |
| Multi-Threaded Engagement | Request introductions: "To build the right solution, I would like the perspective of [other stakeholder]." |
| Follow-Through | Address it directly with the champion. Propose a mutual action plan to keep things on track. |
| Meeting Progression | Propose a clear next step with a specific agenda and a new stakeholder. Avoid "check-in" meetings. |

---

## Quick Reference

**Use this skill when:**
- Reviewing pipeline deal health before a forecast call
- Preparing for a manager 1:1 or deal review
- Identifying which deals need intervention and which are on track
- Building an evidence-based case for a deal stage change

**Don't use when:**
- The account has no active opportunity (use Account Qualification (01) instead)
- You need competitive strategy (use Competitive Strategy (11))
- You need meeting prep (use Meeting Prep (06))

**User roles:** AE, Sales Manager, VP Sales

**Expected time:** 15 to 25 minutes per deal

---

## Core Workflow

### Step 1: Pull Deal Data

Query the CRM for the account's current opportunity data:

- **Opportunity name, stage, amount, close date and owner**
- **Primary contact and role** (economic buyer, champion, end user)
- **Account details:** industry, employee count, annual revenue, HQ location
- **Opportunity history:** stage progression dates, amount changes, close date changes
- **Days in current stage:** calculated from the stage change date to today

Organize the deal context into a structured summary:

```
Account: [name] | Industry: [industry] | Revenue: [annual revenue]
Opportunity: [name] | Stage: [stage number and name] | Amount: $[amount] | Close: [date]
Owner: [rep name] | Primary Contact: [name, title]
Days in stage: [N] | Total deal age: [N days]
Stage history: List each stage transition with date
```

If the close date has been pushed more than twice, flag it as a pattern for scoring.

**Produces:** The deal summary block, with the stage number and name taken from the profile, the days in stage, and the close date history, each fact tagged.

**Why this step comes first:** Step 5 reads the close date history, so the history has to be in hand before the pillars are scored.

---

### Step 2: Pull Activity and Interaction History

Query the CRM for all available interaction intelligence:

- **Call transcripts:** recorded calls with key quotes and topics
- **Email threads:** sequences, direct exchanges and reply patterns
- **Meeting history:** scheduled and completed meetings with attendees
- **Tasks and notes:** activity log, rep notes and next steps
- **Contact engagement map:** all contacts touched, their roles and recency

Organize chronologically with emphasis on the most recent 90 days. Count:

- Total interactions in the last 30 days: [N]
- Total interactions in the last 90 days: [N]
- Unique contacts engaged: [N]
- Departments represented: [list]
- Most recent interaction: [date] | [type] | [summary]

**Produces:** The interaction counts, the unique contacts and the most recent interaction, each tagged with its source.

**Why this step comes before scoring:** The four pillars cite these counts. Counting once keeps every signal working from the same numbers.

---

### Step 3: Score "Why Anything" Pillar

Score the 4 signals in the Why Anything pillar using the rubrics in `{Methodology: Signal Scoring Rubrics (Why Anything Pillar)}`. For each signal, assign GREEN, YELLOW or RED and write a 2 to 3 sentence justification that cites the specific evidence with its tag.

**Signals 1 to 4:** Business Pain Clarity, Compelling Reason to Change, Strategic Initiative Alignment, Champion Strength

If Call Coaching (13) has run on this deal, its `champion_status` is evidence for Signal 4 and is tagged `[Call]` with the call date.

**Produces:** Four signal values, each with its colour, its justification and its tags, and the pillar average.

---

### Step 4: Score "Why Us" Pillar

Score the 4 signals in the Why Us pillar using the rubrics in `{Methodology: Signal Scoring Rubrics (Why Us Pillar)}`. For each signal, assign GREEN, YELLOW or RED with specific evidence citations.

**Signals 5 to 8:** Solution Fit, Technical Readiness, Competitive Landscape, Product Alignment

**Produces:** Four signal values with their justifications and tags, and the pillar average.

---

### Step 5: Score "Why Now" Pillar

Score the 4 signals in the Why Now pillar using the rubrics in `{Methodology: Signal Scoring Rubrics (Why Now Pillar)}`. For each signal, assign GREEN, YELLOW or RED with specific evidence citations.

**Signals 9 to 12:** Budget Path Identified, Decision Process Clarity, Timeline Alignment, Procurement Awareness

**Scoring note:** If the close date has been pushed more than twice (from Step 1), Timeline Alignment can be no better than YELLOW.

**Produces:** Four signal values with their justifications and tags, and the pillar average.

---

### Step 6: Score "Execution" Pillar

Score the 4 signals in the Execution pillar using the rubrics in `{Methodology: Signal Scoring Rubrics (Execution Pillar)}`. For each signal, assign GREEN, YELLOW or RED with specific evidence citations.

**Signals 13 to 16:** Buyer Responsiveness, Multi-Threaded Engagement, Follow-Through on Commitments, Meeting Progression

**Scoring notes:**
- If the most recent buyer-initiated contact is more than 14 days ago, Buyer Responsiveness can be no better than YELLOW. If more than 30 days, it is RED.
- Multi-threading targets the roles in `{Client Profile: Buyer Personas}`: Champion, Evaluator, Technical and Economic Buyer.

**Produces:** Four signal values with their justifications and tags, and the pillar average.

---

### Step 7: Compute Health Score and Recommended Actions

Using `{Methodology: Health Score Calculation}` and `{Methodology: Risk Level Assignment}`:

1. Assign the numeric value to each of the 16 signals: GREEN = 100, YELLOW = 50, RED = 0
2. Calculate the health score as the sum of the 16 values ÷ 16, rounded half up
3. Calculate each pillar average as the mean of its 4 values
4. Read the risk level from the health band, then apply the pillar weakness step once if any pillar average is below 30
5. For each RED signal, take the action from `{Methodology: Recommended Actions Framework}` and name the method it uses
6. For each YELLOW signal, state the evidence needed to move it to GREEN

The risk step is applied after the health band, never before, so the band is always read from the honest score.

**Produces:** The health score, the risk level, the four pillar averages, the RED actions and the YELLOW evidence list.

---

### Step 8: Deliver the Pulse Report

Present the complete report in this order.

**Header:**

```
# Deal Pulse Report: [Account Name]

**Scored:** [date] | **Health:** [score] of 100 | **Risk:** [risk level]
**Opportunity:** [stage number and name] | **Amount:** $[amount] | **Close:** [date] | **Owner:** [rep]
**Primary Contact:** [name, title] | **Deal Age:** [N days] | **Days in Stage:** [N]
```

**Scorecard:** One table with a row for each of the 16 signals, in pillar order:

```
| Pillar | Signal | Colour | Score |
|---|---|---|---|
| Why Anything | 1. Business Pain Clarity | GREEN | 100 |
| ... one row for each of the 16 signals ... |
| **Total** | | | **[sum]** |
```

**Pillar averages line:** One line, in this form:

```
Pillar averages: Why Anything [x], Why Us [x], Why Now [x], Execution [x]
```

**Health line:** One line, in this form, with the sum shown:

```
Health = [sum] ÷ 16 = [unrounded], shown as [rounded]
```

**Pillar bands:** One line naming each pillar's band. A pillar average of 75 or more is GREEN, 26 to 74 is YELLOW and 25 or less is RED.

**Overall Assessment:** Two to three sentences, the top three risks and the top three positive indicators, each with its evidence tag.

**Recommended Actions:** Numbered. Each RED signal gets its specific action and the method it uses. Each YELLOW signal gets the evidence needed to move it.

**Evidence Confidence:** Name the intelligence quality: "Strong" (more than 10 recent interactions), "Moderate" (5 to 10), "Limited" (fewer than 5), or "Stale" (most recent interaction more than 30 days ago). Give the count with it.

**Hand-off block:** The block in the Examples section, in the same fields, so 09, 13 and 06 can read it by name.

**Produces:** The Deal Pulse Report in the sections above, with the hand-off block, returned inline.

---

## Epistemic Rules

- **Score the record, not the rep.** Evidence comes from the CRM, call transcripts, emails and notes. Each fact carries one of the six shared tags, and a fact with no tag is removed.
- **Silence is not a no.** An empty field is written as `[Unknown]` and named in the justification. A signal with no evidence at all reads "Insufficient data to score" in its justification, so the reader sees a gap and not a finding that the thing is absent.
- **Claimed is not confirmed.** What the rep says on a call is `[Call]` with its date. The same point visible in the CRM activity is `[CRM]`. A signal that the rubric grades on confirmed behaviour needs the second.
- **Every rate carries its n.** "16 of 16 signals scored" and "4 of 7 champion tests met", never a rate without its count.

---

## Hard Rules

These rules are never broken. Each one has its reason.

1. **Never score a signal GREEN on the rep's say-so alone.** A claim with no record behind it is the "happy ears" pattern, and it hides a stalled deal until the forecast call. Only the record earns GREEN.
2. **Never combine or weight the sixteen signals.** Each signal is scored on its own rubric and counts the same. A weighted total hides the one weak signal that kills the deal, which is the reason the pillar step exists.
3. **Never raise or lower a score to avoid a hard conversation.** Under-scoring protects a deal and over-scoring kills it, and either way the manager is working from a number that is not true.
4. **Never send, enroll a contact or write to the CRM.** The rep reads the drafted actions and sends them. Nothing reaches a buyer or changes a record without a person deciding it.
5. **Never leave a RED signal without a named action.** A RED with no action tells the rep what is wrong and nothing about what to do next, so the deal sits.
6. **Never name a stakeholder who is not in the record.** A guessed name becomes the buyer on the map and the next email goes to the wrong person. An unknown buyer is written as `[Unknown]` with the role.
7. **Never cite an Illustrative proof point to a buyer.** The profile marks it Illustrative, and an unverified claim that reaches a buyer costs credibility. Lead with a Verified or Benchmark proof point only.

---

## Quality Bar

**Done when all are true:**

- [ ] All 16 signals are scored, each on its own rubric. None is combined or weighted
- [ ] Every justification cites its evidence with one of the six shared tags
- [ ] The scorecard has 16 signal rows, and its Total row equals the sum of the Score column
- [ ] The health score is the sum ÷ 16, rounded half up, and the same figure appears in the header, the Health line and the hand-off block
- [ ] The pillar averages line matches the four pillar averages in the scorecard
- [ ] The risk level comes from the health band, and the pillar step is applied at most once
- [ ] Every RED signal has a named action from the Recommended Actions Framework
- [ ] Every YELLOW signal has the evidence needed to move it to GREEN
- [ ] The hand-off block's first line names the account with its status and stage
- [ ] Every rate carries its n, and no emoji appear anywhere

---

## Examples

All figures are from the PlotIQ profile and the PlotIQ chain file, or marked `(illustrative)`. Facts carry the six shared tags. The first and second pulses are on the same deal, so each example's dates matter: the first pulse is 2026-09-28 and the second is 2026-10-19.

### Example 1: First Pulse, Medium Risk (Brackhaven Memorial Gardens, 2026-09-28)

**Context:** Brackhaven Memorial Gardens is a combination of two sites with 11,000 plots (illustrative). It has been ACTIVE at Stage 5 Negotiate since 2026-09-09 `[CRM]`, so this pulse is on day 19 in stage. Owner: Owen Pruitt, Account Executive `[CRM]`. Amount: $21,576 a year at list (2 sites at $10,788 each) `[CRM]`. Close date: 2026-11-12, the family board's meeting `[CRM]`. Champion: GM Ruth Ellery. Skeptic: Operations Director Walt Okonkwo. Economic buyer: the family board chair, whose name is `[Unknown]`. The board chair has joined one call, in Stage 4 `[CRM]`.

**Input:** "Run the deal pulse for Brackhaven Memorial Gardens. Today is 2026-09-28."

**Process:**

1. **Pull deal data.** Stage 5 Negotiate since 2026-09-09, 19 days in stage `[CRM]`. Amount $21,576 a year at list `[CRM]`. Close date 2026-11-12 with no change on record `[CRM]`. Primary contact Ruth Ellery, General Manager `[CRM]`.
2. **Pull activity.** 11 interactions in the last 90 days `[CRM]` (illustrative): a discovery call, a demo on Brackhaven's own plot records and two contract calls. Three contacts engaged: Ruth Ellery, Walt Okonkwo and Priscilla Dunmore, pre-need manager `[CRM]`. Most recent interaction: a contract terms call with Ruth on 2026-09-26 `[Call]` (illustrative).
3. **Score Why Anything, pillar average 87.5.** Pain Clarity is GREEN. The one double sale in the last 24 months is a note in the CRM `[CRM]` (illustrative), and Ruth describes the paper plot records as the reason it happened `[Call]`. Reason to Change is GREEN. Ruth named the March 2027 Oldgate renewal as the deadline `[Call]`, and the renewal date is in the CRM `[CRM]`. Strategic Initiative is YELLOW. The owner's retirement within three years is not a company priority the board has confirmed `[Unknown]`. Champion Strength is GREEN. Ruth meets four of the shared champion tests, four of seven, each tagged `[Call]`, and she offered to introduce the board chair `[Call]`. (100 + 100 + 50 + 100) ÷ 4 = 87.5.
4. **Score Why Us, pillar average 62.5.** Solution Fit is GREEN. Ruth confirmed the records fix answers her double-sale problem `[Call]`. Technical Readiness is RED. No IT contact is on file and nobody at Brackhaven owns IT `[Unknown]`, and the Oldgate ledger export is unscoped `[Unknown]`. Competitive Landscape is YELLOW. Stonemark mapping was also evaluated, and no preference has been stated `[Call]`. Product Alignment is GREEN. The demo ran on Brackhaven's own plot records `[CRM]`. (100 + 0 + 50 + 100) ÷ 4 = 62.5.
5. **Score Why Now, pillar average 62.5.** Budget Path is YELLOW. The family board chair is the economic buyer, but the chair's name is `[Unknown]`, pricing was delivered in Stage 4 `[CRM]`, and the budget is not yet allocated `[Notes]`. Decision Process is YELLOW. The board chair has joined one call `[CRM]`, and the approval steps after the board are not mapped `[Unknown]`. Timeline Alignment is GREEN. The March 2027 renewal is a confirmed internal deadline `[Call]`, and the close date of 2026-11-12 sits ahead of it `[CRM]`. The board date is proposed and not yet confirmed by the buyer, so this is the closest call in the pulse. It holds at GREEN because the deadline it answers to is confirmed. Procurement Awareness is YELLOW. Legal review and vendor onboarding are known in outline `[Call]`, and their timing is not scoped `[Unknown]`. (50 + 50 + 100 + 50) ÷ 4 = 62.5.
6. **Score Execution, pillar average 75.0.** Buyer Responsiveness is GREEN. Ruth replies within a day `[CRM]` (illustrative). Multi-Threaded Engagement is YELLOW. Three contacts are engaged `[CRM]`, but the board chair has joined only one call and no second meeting is booked `[CRM]`. Follow-Through is GREEN. Ruth sent the trust fund ledger sample she promised `[Notes]` (illustrative). Meeting Progression is YELLOW. The last two calls covered the same contract terms with the same attendees `[CRM]`. (100 + 50 + 100 + 50) ÷ 4 = 75.0.
7. **Health.** There are 8 GREEN, 7 YELLOW and 1 RED. The sum is 800 + 350 + 0 = 1,150. Health = 1,150 ÷ 16 = 71.9, shown as 72. A score of 72 falls in the 46 to 84 band, so the risk is **Medium Risk**. The lowest pillar average is 62.5, which is not below 30, so the pillar step does not apply.

| Pillar | Signal | Colour | Score |
|---|---|---|---|
| Why Anything | 1. Business Pain Clarity | GREEN | 100 |
| Why Anything | 2. Compelling Reason to Change | GREEN | 100 |
| Why Anything | 3. Strategic Initiative Alignment | YELLOW | 50 |
| Why Anything | 4. Champion Strength | GREEN | 100 |
| Why Us | 5. Solution Fit | GREEN | 100 |
| Why Us | 6. Technical Readiness | RED | 0 |
| Why Us | 7. Competitive Landscape | YELLOW | 50 |
| Why Us | 8. Product Alignment | GREEN | 100 |
| Why Now | 9. Budget Path Identified | YELLOW | 50 |
| Why Now | 10. Decision Process Clarity | YELLOW | 50 |
| Why Now | 11. Timeline Alignment | GREEN | 100 |
| Why Now | 12. Procurement Awareness | YELLOW | 50 |
| Execution | 13. Buyer Responsiveness | GREEN | 100 |
| Execution | 14. Multi-Threaded Engagement | YELLOW | 50 |
| Execution | 15. Follow-Through on Commitments | GREEN | 100 |
| Execution | 16. Meeting Progression | YELLOW | 50 |
| **Total** | | | **1,150** |

Pillar averages: Why Anything 87.5, Why Us 62.5, Why Now 62.5, Execution 75.0

Health = 1,150 ÷ 16 = 71.9, shown as 72

Pillar bands: Why Anything GREEN, Why Us YELLOW, Why Now YELLOW, Execution GREEN

**Output:** Medium Risk at a health of 72, with one RED signal (Technical Readiness) and seven YELLOW signals, each with the evidence that would move it. Recommended actions:

1. Technical Readiness (RED): Owen asks Ruth who runs IT at Brackhaven, if anyone, and books a technical discovery on the Oldgate export by 2026-10-02.
2. Multi-Threaded Engagement (YELLOW): Owen asks Ruth for a second call with the board chair, so the economic buyer is on the record.
3. Competitive Landscape (YELLOW): Owen asks Walt what would make the tablet question a non-issue, since his concern is how the team uses it, not the product `[Call]` (illustrative).

```text
Hand-off (read by 09, 13 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-09-28
health_score: 72
risk_level: Medium Risk
pillar_scores: Why Anything 87.5, Why Us 62.5, Why Now 62.5, Execution 75.0
signal_scores: Pain 100, Reason 100, Strategic 50, Champion 100, Fit 100, Technical 0, Competitive 50, Product 100, Budget 50, Decision 50, Timeline 100, Procurement 50, Responsiveness 100, Multi-Threading 50, Follow-Through 100, Progression 50
next_actions: 1. Owen Pruitt asks Ruth Ellery who runs IT and books a technical discovery on the Oldgate export by 2026-10-02. 2. Owen Pruitt asks Ruth Ellery for a second call with the board chair. 3. Owen Pruitt asks Walt Okonkwo what would make the tablet question a non-issue.
next_action: Owen Pruitt asks Ruth Ellery for a technical discovery session on the Oldgate export by 2026-10-02
report_path: none (inline)
```

---

### Example 2: Second Pulse, High Risk (Brackhaven Memorial Gardens, 2026-10-19)

**Context:** Brackhaven again, on 2026-10-19, three weeks after Example 1. The deal is still ACTIVE at Stage 5 Negotiate, now on day 40 in stage `[CRM]`. Ruth Ellery has not replied since 2026-10-03, which is 16 days `[CRM]`. The board meeting is still set for 2026-11-12, but the board has not confirmed the date `[Notes]`. This is the non-success case: a deal that looked close and is now stalling in Stage 5. The same day's MEDDPICC scores 58 (ORANGE), a different instrument on the same deal, so the two numbers are not meant to match. Compared with the first pulse, health falls 34 points, from 72 to 38.

**Input:** "Run the deal pulse for Brackhaven again and compare it to last time."

**Process:**

1. **Pull deal data.** Still Stage 5 Negotiate, $21,576 a year at list `[CRM]`. The close date has been pushed three times `[CRM]` (illustrative). 40 days in stage `[CRM]`.
2. **Pull activity.** 4 interactions in the last 30 days `[CRM]` (illustrative), with two contacts active. Ruth's last reply was on 2026-10-03, 16 days ago `[CRM]`, so the last buyer-initiated contact is past 14 days.
3. **Score Why Anything, pillar average 62.5.** Pain Clarity is YELLOW. Ruth still names the problem `[Call]`, but the economic buyer has not validated it `[Unknown]`. Reason to Change is GREEN. The March 2027 renewal is still a dated trigger `[CRM]`. Strategic Initiative is YELLOW, unchanged from the first pulse `[Unknown]`. Champion Strength is YELLOW. Ruth has shown no internal advocacy since the board meeting moved `[Notes]` (illustrative). (50 + 100 + 50 + 50) ÷ 4 = 62.5.
4. **Score Why Us, pillar average 37.5.** Solution Fit is YELLOW. The use case is confirmed by Ruth `[Call]`, but the mapping for Walt's concerns is not finished `[Notes]`. Technical Readiness is RED. IT is not engaged and nobody at Brackhaven owns the Oldgate data question `[Unknown]`, which is a known blocker. Competitive Landscape is YELLOW. Stonemark is still in the evaluation, and no preference has been stated `[Call]`. Product Alignment is YELLOW. Walt's tablet question is open `[Call]`. (50 + 0 + 50 + 50) ÷ 4 = 37.5.
5. **Score Why Now, pillar average 37.5.** Budget Path is YELLOW. The board has not allocated the budget `[Notes]`. Decision Process is YELLOW. The board chair has joined one call, in Stage 4 `[CRM]`, and no second meeting is booked. Timeline Alignment is RED. The close date has been pushed three times `[CRM]` (illustrative), and the board date is not confirmed. Procurement Awareness is YELLOW. The steps are known, but their details are unclear `[Unknown]`. (50 + 50 + 0 + 50) ÷ 4 = 37.5.
6. **Score Execution, pillar average 12.5.** Buyer Responsiveness is RED. Ruth has been silent for 16 days `[CRM]`, which is more than two weeks, and the buyer-initiated contact is past 14 days. Multi-Threaded Engagement is YELLOW. Three contacts are on record, but only two are active `[CRM]`. Follow-Through is RED. Ruth agreed to send the trust ledger sample by a date and it did not arrive `[Notes]` (illustrative). Meeting Progression is RED. The last meeting was 33 days ago and no next meeting is booked `[CRM]` (illustrative). (0 + 50 + 0 + 0) ÷ 4 = 12.5.
7. **Health.** There is 1 GREEN, 10 YELLOW and 5 RED. The sum is 100 + 500 + 0 = 600. Health = 600 ÷ 16 = 37.5, shown as 38. The score falls in the 0 to 45 band, so the risk is **High Risk**. The pillar step applies because Why Us is at 37.5 (not below 30) and Execution is at 12.5 (below 30). The step would raise the risk by one level, but the deal is already at High Risk, so the rating does not change.

| Pillar | Signal | Colour | Score |
|---|---|---|---|
| Why Anything | 1. Business Pain Clarity | YELLOW | 50 |
| Why Anything | 2. Compelling Reason to Change | GREEN | 100 |
| Why Anything | 3. Strategic Initiative Alignment | YELLOW | 50 |
| Why Anything | 4. Champion Strength | YELLOW | 50 |
| Why Us | 5. Solution Fit | YELLOW | 50 |
| Why Us | 6. Technical Readiness | RED | 0 |
| Why Us | 7. Competitive Landscape | YELLOW | 50 |
| Why Us | 8. Product Alignment | YELLOW | 50 |
| Why Now | 9. Budget Path Identified | YELLOW | 50 |
| Why Now | 10. Decision Process Clarity | YELLOW | 50 |
| Why Now | 11. Timeline Alignment | RED | 0 |
| Why Now | 12. Procurement Awareness | YELLOW | 50 |
| Execution | 13. Buyer Responsiveness | RED | 0 |
| Execution | 14. Multi-Threaded Engagement | YELLOW | 50 |
| Execution | 15. Follow-Through on Commitments | RED | 0 |
| Execution | 16. Meeting Progression | RED | 0 |
| **Total** | | | **600** |

Pillar averages: Why Anything 62.5, Why Us 37.5, Why Now 37.5, Execution 12.5

Health = 600 ÷ 16 = 37.5, shown as 38

Pillar bands: Why Anything YELLOW, Why Us YELLOW, Why Now YELLOW, Execution RED

**Output:** High Risk at a health of 38, down from 72 on 2026-09-28. Ruth's silence, the unconfirmed board date and the three close date pushes are the top risks, and the only GREEN signal is the renewal deadline.

The stage rule the team uses after a second slip, which 09 applies to the same evidence: HOLD at Stage 5 Negotiate with a dated action, which is Owen asking Ruth for the board date by 2026-10-23. If the board date is not confirmed by 2026-11-02, DOWNGRADE to Stage 4 Proposal. Never back to Stage 2 Discovery, because the pain is confirmed.

Recommended actions:

1. Buyer Responsiveness (RED, momentum method): Owen asks Ruth for the board date by 2026-10-23. A breakup email is drafted for Owen to send, framed around the March 2027 renewal, because the 16 days of silence are past the 14 day line.
2. Technical Readiness (RED, Urgency method): Owen asks Ruth who, if anyone, owns IT and the Oldgate data question, and books a technical discovery. Nobody at Brackhaven owns it on the record, so the first answer may be no one.
3. Timeline Alignment (RED): Lena Vasquez, Sales Manager, joins the next call, so the board date is set with a manager present.
4. Competitive Landscape (YELLOW): keep the Stonemark comparison ready and ask Walt what he would need to see before he states a preference. No proof point with Verified or Benchmark status exists in the profile yet, so the team cites none to Walt.

```text
Hand-off (read by 09, 13 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
health_score: 38
risk_level: High Risk
pillar_scores: Why Anything 62.5, Why Us 37.5, Why Now 37.5, Execution 12.5
signal_scores: Pain 50, Reason 100, Strategic 50, Champion 50, Fit 50, Technical 0, Competitive 50, Product 50, Budget 50, Decision 50, Timeline 0, Procurement 50, Responsiveness 0, Multi-Threading 50, Follow-Through 0, Progression 0
next_actions: 1. Owen Pruitt asks Ruth Ellery for the board date by 2026-10-23, and the stage HOLDs at Stage 5 Negotiate. 2. Owen Pruitt drafts a breakup email framed around the March 2027 renewal. 3. Owen Pruitt asks Ruth Ellery who owns IT and books a technical discovery. 4. Lena Vasquez joins the next call. 5. Keep the Stonemark comparison ready for Walt Okonkwo.
next_action: Owen Pruitt asks Ruth Ellery for the family board date by 2026-10-23, and the board date decides between HOLD and DOWNGRADE to Stage 4 Proposal on 2026-11-02
report_path: none (inline)
```

---

## Common Patterns

### Pattern 1: Role-Aware Delivery

**When:** The user is a manager reviewing multiple deals, or an AE reviewing their own deal.

**For managers:** Lead with the portfolio-level risk summary, flag the deals that need intervention and compare health scores across the pipeline.

**For AEs:** Lead with the actionable next steps, focus on what to do before the next meeting and give specific talk tracks for the gaps.

### Pattern 2: Data Sufficiency Fallback

**When:** The CRM record is sparse (fewer than 5 interactions, or no call transcripts).

**Approach:**
- Score what the record can evidence
- Score each data-sparse signal on its rubric, with the justification "Insufficient data to score (no [type] available)"
- Add a "Data Enrichment Priority" list naming the information that would change each score
- Name the intelligence quality as "Limited" or "Stale"

---

## Troubleshooting

### "Most signals are scoring RED but the rep says the deal is strong"

**Likely cause:** A gap between what the rep knows and what the record holds. This is the "happy ears" pattern.

**Response:** Score the record, not the claim. Add the note: "Rep confidence is high but the record is thin. The manager should join the next call to check." Suggest logging more detail, so the next pulse can see it.

### "The account has no opportunity record"

**Likely cause:** The deal has not been created in the CRM yet, or this is a prospect that is not in the pipeline.

**Response:** Stop. This skill needs an open opportunity. Use Account Qualification (01) for an account before the pipeline, or Account Snapshot (02) for prospecting prep.

### "The close date keeps changing but the deal is still active"

**Likely cause:** The close date has been pushed more than twice, which is a key risk indicator.

**Response:** Flag the slip pattern. Timeline Alignment can be no better than YELLOW. Ask the AE to check the date with the buyer: "Is [date] still realistic, or should we reset expectations?"

---

## Best Practices

### Do's
- **Score on evidence, not intuition.** If the CRM does not hold it, the score does not credit it.
- **Cite specific dates and interactions.** Write "2026-10-03 call with Ruth," not "recent conversation."
- **Use the pillar step.** It catches deals that hide a catastrophic gap behind a healthy average.
- **Compare to stage-appropriate expectations.** A Discovery deal should not be scored on procurement.

---

## Integration With Other Skills

### Reads From

**Call Coaching (13)** hands these fields to this skill by name: `call_score`, `category_scores`, `focus_area`, `coaching_points`, `key_moments`, `champion_status`. The `champion_status` field is evidence for Signal 4 and is tagged `[Call]`.

### Hands To

**MEDDPICC Analysis (09), Call Coaching (13) and Meeting Prep (06)** receive these fields by name: `health_score`, `risk_level`, `pillar_scores`, `signal_scores`, `next_actions`. The RED signals in `signal_scores` name what the next call has to test.

**Wrap-Up (O10)** reads `report_path` (set only when a file was written) and `next_action` (owner and date).

### Works Well With

- **MEDDPICC Analysis:** Pulse gives the 30,000-foot health view. MEDDPICC provides the deep element scoring. Run Pulse first, then MEDDPICC on deals flagged as Medium or High Risk.
- **Meeting Prep:** After Pulse identifies gaps, use Meeting Prep to plan the next call around filling them.
- **Call Coaching:** After a call, run Call Coaching to score how well the method was executed, then re-Pulse the deal to see whether the signals moved.
- **Competitive Strategy:** When Competitive Landscape scores RED, run Competitive Strategy to build a displacement plan.

### Workflow Example

```
1. Run Deal Pulse, identify a Medium Risk deal with RED in Champion and Budget
2. Run Meeting Prep, plan a discovery call focused on champion development and economic buyer access
3. Conduct the call
4. Run Call Coaching, score how well the method was executed
5. Re-Pulse, verify the signals improved
```

---

## Changelog

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, a Produces line on every workflow step, Epistemic Rules, Hard Rules with reasons, a Quality Bar, and Integration with the hand-off fields named on both sides.
- Methodology adds a Named Methods subsection: one plain line each for the rapport, momentum and urgency methods and the Day in the Life walkthrough, with a pointer to the profile's Sales Methodology.
- The pillar-weakness step is stated precisely: it applies once, only when a pillar average is below 30, and never lifts High Risk.
- The evidence labels are replaced by the six shared tags. The CRM is "the CRM" throughout.
- The emoji are replaced by the words GREEN, YELLOW and RED, in the rubrics, the scorecard and the pillar bands.
- The scorecard has one table in the shape the checker recomputes: sixteen rows, a Total row, a pillar averages line and a Health line.
- Example 2: Competitive Landscape moves from RED to YELLOW, because the chain file records Stonemark as evaluated with no preference stated. The health is 38 (600 ÷ 16 = 37.5, rounded half up), still High Risk. The stage rule after the second slip is stated as the team's rule shared with MEDDPICC (HOLD, then DOWNGRADE to Stage 4 Proposal). The old "DOWNGRADE to Discovery" wording is removed.
- Example 1: the board chair has joined one call, in Stage 4, and is not named. Dates are set to the chain file: first pulse 2026-09-28, second 2026-10-19.
- Requires now lists Call Coaching only. Meeting Prep and MEDDPICC read this skill's output and are not upstream of it.
- The Input Contract matches the spec: the account with an open opportunity and the CRM access are required.
- Hand-off fields to 09, 13 and 06 are named in the Output Contract, the examples and the Integration section.

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around a single example company
- Em dashes removed from prose

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill reads the shared profile instead of carrying a copy-in Client Profile block
- Signal scoring methodology moved to an explicit Methodology section
- No functional changes to the workflow, scoring logic, examples or output formats

### 1.0.0 (2026-03-04)

- Initial release
- Client-configurable via Client Profile block
- Vendor-agnostic CRM instructions
- Multi-format artifact generation
- All 16 signals, 4 pillars, scoring rubrics and methodology mapping preserved
