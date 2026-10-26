---
name: gtm-deal-pulse
version: 2.1.6
description: "Scores one open deal across 16 signals in 4 pillars and produces a 0 to 100 health score, a risk level and named next actions. The AE and the sales manager read it, and the MEDDPICC, Call Coaching and Meeting Prep skills take its fields by name."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [deal-scoring, pipeline-health, signal-scorecard, opportunity-assessment, sales-methodology]
requires:
  skills: ["gtm-call-coaching"]
mutating: read-write
change_log:
  - version: 2.1.6
    date: 2026-10-26
    summary: "Consistency pass across the sales skills. The close-date moves, the demo date, the Evidence Confidence count, the champion test list and the quantified pain quote are now dated to their records. Example 2 states how a Strong champion status relates to its YELLOW Champion Strength signal, and it reads the pre-need walkthrough as a walkthrough, not a demo. No health score, verdict, band or risk level changes."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The example's invented CRM dated-action context line is removed, and its next actions carry the shared rule's date. The next action follows the family's one deadline rule: five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, which is named with its source. The Output Contract points to that rule, and each example names the record behind its next action date. No score, verdict, band or risk level changes."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Settles the champion who is also the buyer contact for Signal 1, the decision influence a champion needs for Signal 4, the rule for an unnamed economic buyer on Signals 9 and 14, and the owner of the IT question on Technical Readiness. The hand-off block is written out in the Output Contract instead of pointing at the examples. Example 1 gains a second stakeholder on pain. No score, verdict, band or risk level changes."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Records now show the dated commitments, meeting attendance and champion tests that GREEN Signals 4, 13 and 15 rest on. Example 1 names the champion tests and adds the header, the Overall Assessment and an evidence line for each YELLOW. Three rubric sentences settle the boundaries Example 1 decided. Example 2 dates are made consistent with Example 1. No score, verdict, band or risk level changes."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Pain Clarity, Product Alignment and Timeline Alignment gain the facts their GREEN rubrics need, Strategic Initiative and Multi-Threaded Engagement each gain one rubric sentence, Example 1 adds Evidence Confidence, and the Recommended Actions Framework names a method for Strategic Initiative and Technical Readiness. No score, verdict or risk level changes."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. Unknown signals are left out of the health math: a signal with no evidence is scored INSUFFICIENT and counted in neither the sum nor the count, and the health score is shown only when 12 or more of the 16 signals are scored."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection and a Guild Pro Kits subsection."
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

To try the skill without your own data, use `examples/try-it.md`, which holds the inputs for Example 1.

| Input | Required | Notes |
|-------|----------|-------|
| Account name with an open opportunity | Required | The deal must be ACTIVE with its stage number. For a prospect with no opportunity, use Account Qualification (01) |
| CRM access (interaction history, notes and activity), or the same records pasted | Required | The evidence every signal is scored from |
| Opportunity stage, deal amount, close date and primary contact | Required | Read from the CRM. If the CRM is silent on one, ask the user rather than guess |
| Days in current stage | Optional | Used for stalled-deal detection. Calculated from the stage change date when the CRM has it |
| Call notes and emails | Optional | Extra evidence, tagged `[Call]` with the call date, or `[Notes]` |

---

## Output Contract

Every run produces one Deal Pulse Report with the same sections in the same order, so deal health can be compared across the pipeline. The content changes per deal. The structure never does.

Core commitments: **a 16-signal scorecard across 4 pillars**, **a health score from 0 to 100**, **a risk level with the pillar averages**, **the top risks**, and **a specific recommended action for each RED signal**.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `health_score` | Header and Health line of the report, and the hand-off block | A whole number from 0 to 100: the sum of the scored values ÷ the number of signals scored, rounded half up, shown with "scored n of 16". With fewer than 12 signals scored there is no health score, and the report reads "Not scored: n of 16 signals have evidence" |
| `risk_level` | Header of the report, and the hand-off block | Low Risk, Medium Risk or High Risk, after the pillar step. Not set when fewer than 12 signals are scored |
| `pillar_scores` | Pillar averages line of the report, and the hand-off block | Four values, one decimal place: Why Anything, Why Us, Why Now, Execution. A pillar with fewer than 2 scored signals reads insufficient |
| `signal_scores` | Score column of the scorecard, and the hand-off block | Sixteen entries in signal order: 100 (GREEN), 50 (YELLOW), 0 (RED), or INSUFFICIENT, which has no value and is left out of the sum and the count |
| `next_actions` | Recommended Actions section, and the hand-off block | One numbered action for each RED signal, the evidence needed for each YELLOW, and the evidence that would score each INSUFFICIENT signal |
| `next_action` | Last line of the report | The owner and the date the shared contract's next-action rule gives (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source). Wrap-Up reads this line |
| `report_path` | Hand-off block | `none (inline)` unless a file was written |
| File option | Written only when the user asks | Named `<account>_<skill>_<date>.md`, saved beside the user's other account notes. Never written by default |

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

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
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls and decisions for that account) |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the plain method names in Methodology, and marks every output that depended on the missing section. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

### The Shared Contract

Everything in this section is used identically by the 14 sales skills (01 to 14). The names below are copied exactly, so the 14 never drift from each other.

#### The Profile Is the Only Source of Company Facts

Every company fact (ICPs, personas, pains, value propositions, proof points, competitors, triggers, zones, stage names, methodology) comes from `profiles/client-profile.md`. A skill reads the sections its Context table names and nothing else. A skill never carries a company fact of its own. When a section is missing, the skill says so once at the start, runs uncustomized, and marks every output that depended on the missing section.

#### The Knowledge Base and Connectors

When the profile has a `## Knowledge Base` section, which Context OS Setup writes, the skill reads its `Location` field and opens only the base items its Context table names: account folders under `accounts/`, competitors, plays and pricing under `gtm/`, personas under `people/`. Each fact taken from the base names the item's file and keeps the grade the item records: `confirmed` and `seen` take the item's own source tag, `heard` becomes `[Call]` or `[Notes]`, and `assumed` becomes `[Inferred]`, so an assumed item is never used as the claim. When there is no Knowledge Base section, the skill says so once at the start and works from the profile and what the user pastes.

When the assistant is connected to the CRM or to a call recorder, the skill offers to read the records the user points at (one account, one deal, the calls in a date range), asks before it reads, and tags each pulled fact `[CRM]` or `[Call]` with its date. It reads only. It never searches records nobody named and never writes back. Without a connector, pasting the same records works the same way.

#### Account Status, Five Words

Every account carries one status: **TARGET** (researched, no open deal yet, whether or not contacted), **INBOUND** (they asked us), **ACTIVE** with its stage number (open deal), **LOST** (closed-lost, eligible for reactivation), **OUT** (disqualified). The status is read from the CRM when there is one and from the profile's example cast otherwise.

#### The Verdict Words and the Zone Rule

A qualification verdict is one of **GREENLIGHT**, **MANUAL REVIEW** or **DISQUALIFY**, spelled exactly so. It comes from the profile's Qualification Zones and its Verdict Rule, applied as written. MEDIUM never counts as HIGH. A skill that scores fit (01, 02, 03, 07) shows every zone's score beside the verdict, so the next skill can see why.

#### Stage Names Come From the Profile

Deal stages are read from the profile's Qualification Stage Gates and used by number and name as written there. No skill carries its own stage list. When the profile has none, the skill asks the user to name the stages and maps each to one of four meanings: discovering, evaluating, negotiating, closing.

#### Evidence Tags, One Set

Every fact in a report carries one tag naming where it came from:

| Tag | Meaning |
|---|---|
| `[CRM]` | A field or note in the CRM |
| `[Call]` | Said on a recorded or transcribed call, with the call date. A call whose date is not on record is written `[Call, date Unknown]`, and it places no fact in time |
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

Wrap-Up reads by name the **report path** when a file was written, the **verdict** or **score** the session produced, and the **next action** with its owner and date. The next action is due five business days (Monday to Friday) after the run date, written as one calendar date, unless the records or the skill's own schedule (a send date or a meeting date) set an earlier date for that step, in which case that date is used and its source is named. Ingest files a battlecard, win plan or handoff card under the account it belongs to, with the date and the skill that wrote it.

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

A champion who is also the buyer contact, the persona the profile names as the buyer, speaks for the buyer on this signal, so her own quantified account, with examples, scores GREEN. A champion who is not the buyer contact keeps this signal YELLOW until the buyer or a second stakeholder confirms the pain. A quantified account counts only when it was given within 14 days of the score, the same window Buyer Responsiveness uses.

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
| RED | No known connection to strategic initiatives. Driven by individual interest only. A goal the champion states for their own team, with no company-wide confirmation, is YELLOW, not RED. |

#### Signal 4: Champion Strength
| Score | Criteria |
|-------|----------|
| GREEN | Identified champion with decision influence who is actively selling internally, sharing insider information and coaching us on how to win. |
| YELLOW | Friendly contact who supports us but has limited influence or has not demonstrated internal advocacy. |
| RED | No champion identified, or primary contact is purely informational or transactional. |

A contact has decision influence when she briefs the economic buyer before the decision and forwards the evidence the buyer decides on. Being liked, or offering one introduction, does not show influence.

### Signal Scoring Rubrics (Why Us Pillar)

#### Signal 5: Solution Fit
| Score | Criteria |
|-------|----------|
| GREEN | Capabilities directly address identified pain. Buyer has confirmed fit ("this solves our problem"). Feature requirements mapped and validated. |
| YELLOW | General fit acknowledged but specific use case mapping incomplete. |
| RED | Significant gaps between buyer needs and capabilities, or fit has not been validated at all. |

Feature requirements count as mapped and validated when the demo covered at least 80% of them and the buyer confirmed the fit, the same line Signal 8 uses.

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

A close date is buyer-validated when the buyer names it on a call, even before the buyer's approval body confirms it.

#### Signal 12: Procurement Awareness
| Score | Criteria |
|-------|----------|
| GREEN | Legal, security review and vendor onboarding requirements identified. Procurement timeline scoped. |
| YELLOW | Procurement steps exist but details are unclear. |
| RED | Procurement process completely unknown. Potential for surprise 30 to 60 day delays. |

An economic buyer with no name cannot score GREEN on this signal, because GREEN needs the name and title.

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
| GREEN | Three or more contacts engaged across different roles or departments. Relationships at multiple org levels. GREEN also needs the economic buyer engaged in at least two meetings, so three or more contacts with the economic buyer absent or in one meeting scores YELLOW. |
| YELLOW | Two contacts engaged, concentrated in one department or level. |
| RED | Single-threaded: only one contact engaged. |

#### Signal 15: Follow-Through on Commitments
| Score | Criteria |
|-------|----------|
| GREEN | Both buyer and rep consistently deliver on agreed next steps. Commitments completed before the next meeting. |
| YELLOW | Some follow-through but occasional missed commitments on either side. |
| RED | Pattern of missed commitments. "Happy ears" risk. |

A commitment is a dated next step that the person agreed to, on a call or in writing. An offer with no agreed date, such as a meeting that is only proposed, does not count.

#### Signal 16: Meeting Progression
| Score | Criteria |
|-------|----------|
| GREEN | Meetings progress through stages with increasing stakeholder seniority. Each meeting advances the deal. |
| YELLOW | Meetings occur but do not clearly advance the deal. Same topics, same attendees. Lateral movement. |
| RED | No meetings in the last 30 days, stalled progression, or only intro-level conversations after months. |

An unnamed economic buyer counts as engaged only when that person has attended a meeting, and GREEN needs two such meetings.

### Health Score Calculation

**Numeric mapping:** GREEN = 100, YELLOW = 50, RED = 0. A signal with no evidence is INSUFFICIENT and has no numeric value.

1. **Unknown signals are left out.** An INSUFFICIENT signal is left out of both the sum and the count. It is never scored 0, because 0 would record a finding that the thing is absent.
2. **Health score** = the sum of the scored signal values ÷ the number of signals scored, rounded half up to a whole number, shown with its count as "scored n of 16". Example: 14 signals scored with a sum of 1,000 gives 1,000 ÷ 14 = 71.4, shown as 71, scored 14 of 16.
3. **Minimum to score.** With fewer than 12 of the 16 signals scored, there is no health score and no risk level. The report says "Not scored: n of 16 signals have evidence" and lists the evidence that would score the missing signals.
4. **Pillar averages** = the average of each pillar's scored signal values, shown to one decimal place. A pillar with fewer than 2 scored signals reads "insufficient" and has no average.

### Risk Level Assignment

| Health Score | Risk Level |
|-------------|------------|
| 85 to 100 | Low Risk |
| 46 to 84 | Medium Risk |
| 0 to 45 | High Risk |

**Pillar weakness step.** If one or more pillar averages is below 30, the risk level rises one step (Low Risk to Medium Risk, or Medium Risk to High Risk). The step is taken once, however many pillars are below 30, and High Risk stays High Risk. A pillar average of exactly 30 does not trigger it. A pillar that reads insufficient is not compared with 30. The step exists to catch a deal that looks healthy overall but has a catastrophic weakness in one pillar.

### Recommended Actions Framework

For each RED signal, recommend a specific action mapped to the team's methodology:

| Red Signal Area | Recommended Action |
|----------------|-------------------|
| Business Pain Clarity | Run discovery to probe and quantify the pain. Ask "What happens if you do nothing for 12 months?" |
| Compelling Reason to Change | Use the urgency method to create timeline pressure. Explore contract renewals, compliance deadlines and incidents. |
| Strategic Initiative Alignment | Use the rapport method. Ask the champion: "Where does this sit on your company's priority list this year?" Seek executive validation. |
| Champion Strength | Use the rapport method to develop an internal advocate. Identify who has the most to gain. |
| Solution Fit | Schedule a tailored demo against specific use cases. Use the Day in the Life walkthrough, not a feature walkthrough. |
| Technical Readiness | Use the urgency method. Request a technical discovery with IT. Identify the key integration variables. If nobody owns IT, ask who should. The rep asks the champion, and the IT contact stays [Unknown] until she names one. |
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

Before pulling anything, read the account's folder under `accounts/` in the knowledge base, when the profile has one, for its notes, calls and decisions. Then offer to read the CRM deal record and, when a call recorder is connected, the deal's calls, and ask before reading either, as set out in The Knowledge Base and Connectors.

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

Once you say yes, query the CRM for the interaction history of the deal you named:

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

1. Assign the numeric value to each signal: GREEN = 100, YELLOW = 50, RED = 0. A signal with no evidence is INSUFFICIENT and has no value
2. Count the scored signals. If fewer than 12 of the 16 are scored, set no health score and no risk level, report "Not scored: n of 16 signals have evidence", and go on to steps 6 to 8
3. If 12 or more are scored, calculate the health score as the sum of the scored values ÷ the number scored, rounded half up, and show it with "scored n of 16"
4. Calculate each pillar average as the mean of its scored values. A pillar with fewer than 2 scored signals reads insufficient
5. If 12 or more are scored, read the risk level from the health band, then apply the pillar weakness step once if any scored pillar average is below 30
6. For each RED signal, take the action from `{Methodology: Recommended Actions Framework}` and name the method it uses
7. For each YELLOW signal, state the evidence needed to move it to GREEN
8. For each INSUFFICIENT signal, state the evidence that would score it

The risk step is applied after the health band, never before, so the band is always read from the honest score.

**Produces:** The health score, the risk level, the four pillar averages, the RED actions and the YELLOW evidence list.

---

### Step 8: Deliver the Pulse Report

Present the complete report in this order.

**Header:**

```
# Deal Pulse Report: [Account Name]

**Scored:** [date] | **Health:** [score] of 100, scored [n] of 16 | **Risk:** [risk level, or Not scored]
**Opportunity:** [stage number and name] | **Amount:** $[amount] | **Close:** [date] | **Owner:** [rep]
**Primary Contact:** [name, title] | **Deal Age:** [N days] | **Days in Stage:** [N]
```

**Scorecard:** One table with a row for each of the 16 signals, in pillar order. An INSUFFICIENT signal shows INSUFFICIENT in Colour and a dash in Score. The Total row sums the scored values and states the count beside it:

```
| Pillar | Signal | Colour | Score |
|---|---|---|---|
| Why Anything | 1. Business Pain Clarity | GREEN | 100 |
| ... one row for each of the 16 signals ... |
| **Total** | | | **[sum]** |
```

**Pillar averages line:** One line, in this form. A pillar that reads insufficient shows the word insufficient in place of its average:

```
Pillar averages: Why Anything [x], Why Us [x], Why Now [x], Execution [x]
```

**Health line:** One line, in this form, with the sum shown:

```
Health = [sum] ÷ [n scored] = [unrounded], shown as [rounded] (scored [n] of 16)
```

**Pillar bands:** One line naming each pillar's band. A pillar average of 75 or more is GREEN, 26 to 74 is YELLOW and 25 or less is RED. A pillar that reads insufficient has no band.

**Overall Assessment:** Two to three sentences, the top three risks and the top three positive indicators, each with its evidence tag.

**Recommended Actions:** Numbered. Each RED signal gets its specific action and the method it uses. Each YELLOW signal gets the evidence needed to move it.

**Evidence Confidence:** Name the intelligence quality: "Strong" (more than 10 recent interactions), "Moderate" (5 to 10), "Limited" (fewer than 5), or "Stale" (most recent interaction more than 30 days ago). Give the count with it. A figure the record marks (illustrative) counts as the record states it, and the line repeats the marking.

**Hand-off block:** the block below, with these fields in this order, so 09, 13 and 06 can read it by name. Each field sits on its own line. A health score appears only when 12 or more signals are scored, and otherwise the line reads "not scored".

```text
Hand-off (read by 09, 13 and 06):
account: [Account Name] ([STATUS], Stage [n] [Stage Name])
run_date: [YYYY-MM-DD]
health_score: [n] (scored [n] of 16)
risk_level: [Low Risk, Medium Risk or High Risk]
pillar_scores: Why Anything [x], Why Us [x], Why Now [x], Execution [x]
signal_scores: Pain [v], Reason [v], Strategic [v], Champion [v], Fit [v], Technical [v], Competitive [v], Product [v], Budget [v], Decision [v], Timeline [v], Procurement [v], Responsiveness [v], Multi-Threading [v], Follow-Through [v], Progression [v]
next_actions: [numbered list, one for each RED signal and each YELLOW evidence need]
next_action: [owner] [what they do] [with whom], by [date]
report_path: none (inline)
```

Each [v] is 100 for GREEN, 50 for YELLOW, 0 for RED, or INSUFFICIENT, which has no value.

**Produces:** The Deal Pulse Report in the sections above, with the hand-off block, returned inline.

---

## Epistemic Rules

- **Score the record, not the rep.** Evidence comes from the CRM, call transcripts, emails and notes. Each fact carries one of the six shared tags, and a fact with no tag is removed.
- **Silence is not a no.** An empty field is written as `[Unknown]` and named in the justification. A signal with no evidence at all is scored INSUFFICIENT: it has no value, it is left out of both the sum and the count, and its justification reads "Insufficient data to score", so the reader sees a gap and not a finding that the thing is absent.
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

- [ ] Each of the 16 signals is scored GREEN, YELLOW, RED or INSUFFICIENT on its own rubric. None is combined or weighted
- [ ] Every justification cites its evidence with one of the six shared tags
- [ ] The scorecard has 16 signal rows, and its Total row equals the sum of the scored values, with the count of scored signals beside it
- [ ] The health score is the sum of the scored values ÷ the number scored, rounded half up, shown with its count, and the same figure appears in the header, the Health line and the hand-off block. With fewer than 12 scored there is no health score
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

**Context:** Brackhaven Memorial Gardens is a combination of two sites with 11,000 plots (illustrative). It has been ACTIVE at Stage 5 Negotiate since 2026-09-09 `[CRM]`, so this pulse is on day 19 in stage. Owner: Owen Pruitt, Account Executive `[CRM]`. Amount: $21,576 a year at list (2 sites at $10,788 each) `[CRM]`. Close date: 2026-11-12, the family board's meeting `[CRM]`. Champion: GM Ruth Ellery. Skeptic: Operations Director Walt Okonkwo. Economic buyer: the family board chair, whose name is `[Unknown]`. The board chair has joined one call, in Stage 4 `[CRM]`. Each `[Call]` fact in this example is from the 2026-09-26 contract terms call unless its sentence gives another date.

**Input:** "Run the deal pulse for Brackhaven Memorial Gardens. Today is 2026-09-28."

**Process:**

1. **Pull deal data.** Stage 5 Negotiate since 2026-09-09, 19 days in stage `[CRM]`. Amount $21,576 a year at list `[CRM]`. Close date 2026-11-12 with no change on record `[CRM]`. Primary contact Ruth Ellery, General Manager `[CRM]`.
2. **Pull activity.** 10 interactions in the last 90 days `[CRM]` (illustrative), including a demo on 2026-09-17 on Brackhaven's own plot records and two contract calls. The discovery call of 2026-05-12 falls before the window opens on 2026-06-30, so it is not counted. Three contacts engaged: Ruth Ellery, Walt Okonkwo and Priscilla Dunmore, pre-need manager `[CRM]`. Most recent interaction: a contract terms call with Ruth on 2026-09-26 `[Call]` (illustrative).
3. **Score Why Anything, pillar average 87.5.** Pain Clarity is GREEN. The one double sale in the last 24 months is a note in the CRM `[CRM]` (illustrative), and Ruth describes the paper plot records as the reason it happened `[Call]`. Ruth puts the staff time to unwind one double sale at about 40 hours `[Call]` (illustrative), a time impact. Walt Okonkwo, the Operations Director, puts a double-sale search at half a day, and lookups at two a week `[Call, 2026-09-17]` (illustrative). Ruth is the buyer contact and the champion, so her account counts for the buyer under the rule above, and Walt's account is the second stakeholder. Reason to Change is GREEN. Ruth named the March 2027 Oldgate renewal as the deadline `[Call]`, and the renewal date is in the CRM `[CRM]`. Strategic Initiative is YELLOW. Ruth's stated goal for the cemetery side is one system for plot records before the owner retires `[Call]` (illustrative), a departmental goal. The owner's retirement within three years is not a company priority the board has confirmed `[Unknown]`. Champion Strength is GREEN. Ruth meets four of the shared champion tests, four of seven, each tagged with its date: she offers introductions to the board chair `[Call, 2026-09-26]`, explains the internal politics `[Call, 2026-09-26]`, commits to next steps with dates `[Call, 2026-09-26]`, and defends the solution when we are not in the room `[CRM, 2026-09-25]`. The CRM note of 2026-09-25 records that she briefed the board chair on the records fix and forwarded the ledger comparison `[CRM]` (illustrative), which is the decision influence the GREEN rubric needs, because she briefs the board chair and forwards the evidence the chair decides on. (100 + 100 + 50 + 100) ÷ 4 = 87.5.
4. **Score Why Us, pillar average 62.5.** Solution Fit is GREEN. Ruth confirmed the records fix answers her double-sale problem `[Call]`. Technical Readiness is RED. No IT contact is on file and nobody at Brackhaven owns IT `[Unknown]`, and the Oldgate ledger export is unscoped `[Unknown]`. Owen proposed Friday 2026-10-02 for a technical discovery on the export `[Notes]` (illustrative), which is the earlier date the records set for that step. Competitive Landscape is YELLOW. Stonemark mapping was also evaluated, and no preference has been stated `[Call]`. Product Alignment is GREEN. The CRM note lists 12 requirements, and the demo covered 10 of them, or 83% `[CRM]` (illustrative). The demo ran on 2026-09-17 on Brackhaven's own plot records, with Ruth in the room `[CRM]`. (100 + 0 + 50 + 100) ÷ 4 = 62.5.
5. **Score Why Now, pillar average 62.5.** Budget Path is YELLOW. The family board chair is the economic buyer, but the chair's name is `[Unknown]`, pricing was delivered in Stage 4 `[CRM]`, and the budget is not yet allocated `[Notes]`. Decision Process is YELLOW. The board chair has joined one call `[CRM]`, and the approval steps after the board are not mapped `[Unknown]`. Timeline Alignment is GREEN. The March 2027 renewal is a confirmed internal deadline `[Call]`, and the close date of 2026-11-12 sits ahead of it `[CRM]`. Ruth confirmed 2026-11-12 as the date she is working to on the 2026-09-26 call `[Call]` (illustrative), so the close date is buyer-validated. The board itself has not formally confirmed it, so this is the closest call in the pulse. It holds at GREEN because the close date is buyer-validated and the deadline it answers to is confirmed. Procurement Awareness is YELLOW. Legal review and vendor onboarding are known in outline `[Call]`, and their timing is not scoped `[Unknown]`. (50 + 50 + 100 + 50) ÷ 4 = 62.5.
6. **Score Execution, pillar average 75.0.** Buyer Responsiveness is GREEN. Ruth replies within a day, started the 2026-09-22 call request, and attended all four meetings on the calendar `[CRM]` (illustrative). Multi-Threaded Engagement is YELLOW. Three contacts are engaged `[CRM]`, but the board chair has joined only one call and no second meeting is booked `[CRM]`. Follow-Through is GREEN. Both sides kept their dated commitments before the next meeting. Ruth sent the trust fund ledger sample on 2026-09-24 and returned the markup on 2026-09-25 `[Notes]` (illustrative). Owen sent the revised terms on 2026-09-17 and called Walt on 2026-09-21 `[CRM]` (illustrative). Meeting Progression is YELLOW. The last two calls covered the same contract terms with the same attendees `[CRM]`. (100 + 50 + 100 + 50) ÷ 4 = 75.0.
7. **Health.** There are 8 GREEN, 7 YELLOW and 1 RED. The sum is 800 + 350 + 0 = 1,150. Health = 1,150 ÷ 16 = 71.9, shown as 72. A score of 72 falls in the 46 to 84 band, so the risk is **Medium Risk**. The lowest pillar average is 62.5, which is not below 30, so the pillar step does not apply.

**Scored:** 2026-09-28 | **Health:** 72 of 100, scored 16 of 16 | **Risk:** Medium Risk

**Opportunity:** Stage 5 Negotiate | **Amount:** $21,576 | **Close:** 2026-11-12 | **Owner:** Owen Pruitt

**Primary Contact:** Ruth Ellery, General Manager | **Days in Stage:** 19

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

Health = 1,150 ÷ 16 = 71.9, shown as 72 (scored 16 of 16)

Pillar bands: Why Anything GREEN, Why Us YELLOW, Why Now YELLOW, Execution GREEN

**Overall Assessment:** The top three risks are Technical Readiness (RED, nobody owns IT `[Unknown]`), the economic buyer's name (`[Unknown]`) and the procurement timing (`[Unknown]`). The top three positives are the renewal deadline (the March 2027 Oldgate renewal `[Call]`, with its date in the CRM `[CRM]`), the buyer-validated close date (`[Call]`, 2026-11-12) and the confirmed fit (Ruth confirmed the records fix answers her double-sale problem `[Call]`).

**Output:** Medium Risk at a health of 72, with one RED signal (Technical Readiness) and seven YELLOW signals, each with the evidence that would move it. Recommended actions:

1. Technical Readiness (RED, urgency method): Owen asks Ruth who runs IT at Brackhaven, if anyone, and books a technical discovery on the Oldgate export by 2026-10-02, the Friday Owen proposed in his notes, which is earlier than the five-business-day date of 2026-10-05.
2. Multi-Threaded Engagement (YELLOW): Owen asks Ruth for a second call with the board chair, so the economic buyer is on the record.
3. Competitive Landscape (YELLOW): Owen asks Walt what would make the tablet question a non-issue, since his concern is how the team uses it, not the product `[Call, 2026-09-21]` (illustrative).

Evidence That Would Move Each YELLOW Signal To GREEN:

- Strategic Initiative Alignment: a director-level or board statement that the records fix is a company priority.
- Competitive Landscape: a stated buyer preference between Stonemark and PlotIQ.
- Budget Path Identified: the budget allocated in writing, with the board chair named.
- Decision Process Clarity: the approval steps after the board mapped and confirmed by Ruth on a call.
- Procurement Awareness: the legal review and vendor onboarding dates scoped on a call.
- Multi-Threaded Engagement: the board chair in a second meeting, so the economic buyer is engaged in two meetings.
- Meeting Progression: a next meeting booked with a new attendee and an agenda that advances the decision.

**Evidence Confidence:** Moderate, 10 interactions in the last 90 days `[CRM]` (illustrative). The count is 10, which is Moderate (5 to 10), and the most recent interaction, on 2026-09-26, is within 30 days, so the record is not Stale. This does not change the score.

```text
Hand-off (read by 09, 13 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-09-28
health_score: 72
risk_level: Medium Risk
pillar_scores: Why Anything 87.5, Why Us 62.5, Why Now 62.5, Execution 75.0
signal_scores: Pain 100, Reason 100, Strategic 50, Champion 100, Fit 100, Technical 0, Competitive 50, Product 100, Budget 50, Decision 50, Timeline 100, Procurement 50, Responsiveness 100, Multi-Threading 50, Follow-Through 100, Progression 50
next_actions: 1. Owen Pruitt asks Ruth Ellery who runs IT and books a technical discovery on the Oldgate export by 2026-10-02. 2. Owen Pruitt asks Ruth Ellery for a second call with the board chair. 3. Owen Pruitt asks Walt Okonkwo what would make the tablet question a non-issue.
next_action: Owen Pruitt asks Ruth Ellery for a technical discovery session on the Oldgate export by 2026-10-02 (the Friday Owen proposed in his notes, earlier than 2026-10-05)
report_path: none (inline)
```

---

### Example 2: Second Pulse, High Risk (Brackhaven Memorial Gardens, 2026-10-19)

**Context:** Brackhaven again, on 2026-10-19, three weeks after Example 1. The deal is still ACTIVE at Stage 5 Negotiate, now on day 40 in stage `[CRM]`. Ruth Ellery has not replied since 2026-10-03, which is 16 days `[CRM]`. The board meeting is still set for 2026-11-12, but the board has not confirmed the date `[Notes]`. This is the non-success case: a deal that looked close and is now stalling in Stage 5. The same day's MEDDPICC scores 71 (YELLOW), a different instrument on the same deal, so the two numbers are not meant to match. Compared with the first pulse, health falls 34 points, from 72 to 38.

**Input:** "Run the deal pulse for Brackhaven again and compare it to last time."

**Process:**

1. **Pull deal data.** Still Stage 5 Negotiate, $21,576 a year at list `[CRM]`. The close date has moved twice since 2026-09-28, on 2026-10-07 and 2026-10-14 `[CRM]` (illustrative), each time after the board did not confirm. 40 days in stage `[CRM]`.
2. **Pull activity.** 5 interactions in the last 30 days `[CRM]` (illustrative): Ruth on 2026-09-26 and 2026-10-03, Walt on 2026-09-21, and Priscilla Dunmore on 2026-10-08 (a pre-need walkthrough, not a demo) and 2026-10-14. Ruth's last reply was on 2026-10-03, 16 days ago `[CRM]`, so the last buyer-initiated contact on her record is past 14 days.
3. **Score Why Anything, pillar average 62.5.** Pain Clarity is YELLOW. Ruth still names the problem `[Call]`, but her quantified account is from the 2026-09-26 call, 23 days before this pulse, and Walt's is from 2026-09-17, 32 days before. Neither is inside the 14-day window the signal uses `[Call]`. Reason to Change is GREEN. The March 2027 renewal is still a dated trigger `[CRM]`. Strategic Initiative is YELLOW, unchanged from the first pulse `[Unknown]`. Champion Strength is YELLOW. Ruth has shown no internal advocacy since the board meeting moved `[Notes]` (illustrative). The champion status stays Strong, because four of seven shared tests are on record and dated 2026-09-25 and 2026-09-26. Signal 4 is scored on its own rubric, which reads recent internal advocacy, and none is on record since 2026-10-03, so the signal is YELLOW while the status word is Strong. Silence is not a no, but the signal is scored on what is on record. (50 + 100 + 50 + 50) ÷ 4 = 62.5.
4. **Score Why Us, pillar average 37.5.** Solution Fit is YELLOW. The use case is confirmed by Ruth `[Call]`, but the mapping for Walt's concerns is not finished `[Notes]`. Technical Readiness is RED. IT is not engaged and nobody at Brackhaven owns the Oldgate data question `[Unknown]`, which is a known blocker. Competitive Landscape is YELLOW. Stonemark is still in the evaluation, and no preference has been stated `[Call]`. Product Alignment is YELLOW. Walt's tablet question is open `[Call]`. (50 + 0 + 50 + 50) ÷ 4 = 37.5.
5. **Score Why Now, pillar average 37.5.** Budget Path is YELLOW. The board has not allocated the budget `[Notes]`. Decision Process is YELLOW. The board chair has joined one call, in Stage 4 `[CRM]`, and no second meeting is booked. Timeline Alignment is RED. The close date has moved twice since 2026-09-28 `[CRM]` (illustrative), which meets the RED row for two or more moves, and the board date is not confirmed. Procurement Awareness is YELLOW. The steps are known, but their details are unclear `[Unknown]`. (50 + 50 + 0 + 50) ÷ 4 = 37.5.
6. **Score Execution, pillar average 12.5.** Buyer Responsiveness is RED. Ruth has been silent for 16 days `[CRM]`, which is more than two weeks, and the buyer-initiated contact on her record is past 14 days. Priscilla Dunmore's 2026-10-14 interaction does not record who started it, so it does not show a buyer-initiated contact. Multi-Threaded Engagement is YELLOW. Three contacts are on record, and each has an interaction in the last 30 days `[CRM]`, but the economic buyer has been in one meeting, so the GREEN condition is not met. Follow-Through is RED. Ruth agreed to send the Oldgate export sample by 2026-10-09, and it did not arrive `[Notes]` (illustrative). Meeting Progression is RED. The last meeting with the decision side was the 2026-09-26 call, 23 days ago. Priscilla Dunmore's 2026-10-08 pre-need walkthrough was with an end user and did not move the decision forward, and no next meeting is booked `[CRM]` (illustrative), so progression is stalled. (0 + 50 + 0 + 0) ÷ 4 = 12.5.
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

Health = 600 ÷ 16 = 37.5, shown as 38 (scored 16 of 16)

Pillar bands: Why Anything YELLOW, Why Us YELLOW, Why Now YELLOW, Execution RED

**Output:** High Risk at a health of 38, down from 72 on 2026-09-28. Ruth's silence, the unconfirmed board date and the two close date moves since 2026-09-28 are the top risks, and the only GREEN signal is the renewal deadline.

The stage rule the team uses after a second slip, which 09 applies to the same evidence: HOLD at Stage 5 Negotiate with a dated action, which is Owen asking Ruth for the board date by 2026-10-26, five business days after the run date of 2026-10-19. If the board date is not confirmed by 2026-11-02, DOWNGRADE to Stage 4 Proposal. Never back to Stage 2 Discovery, because the pain is confirmed.

Recommended actions:

1. Buyer Responsiveness (RED, momentum method): Owen asks Ruth for the board date by 2026-10-26. A breakup email is drafted for Owen to send, framed around the March 2027 renewal, because the 16 days of silence are past the 14 day line.
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
next_actions: 1. Owen Pruitt asks Ruth Ellery for the board date by 2026-10-26, and the stage HOLDs at Stage 5 Negotiate. 2. Owen Pruitt drafts a breakup email framed around the March 2027 renewal. 3. Owen Pruitt asks Ruth Ellery who owns IT and books a technical discovery. 4. Lena Vasquez joins the next call. 5. Keep the Stonemark comparison ready for Walt Okonkwo.
next_action: Owen Pruitt asks Ruth Ellery for the family board date by 2026-10-26, five business days after the run date of 2026-10-19 (no earlier record or schedule date), and the board date decides between HOLD and DOWNGRADE to Stage 4 Proposal on 2026-11-02
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
- Mark each data-sparse signal INSUFFICIENT, with the justification "Insufficient data to score (no [type] available)" and the evidence that would score it. If fewer than 12 of 16 signals are scored, the report sets no health score (see Health Score Calculation)
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

### Chains

- **Work The Deal:** Meeting Prep (06), Call Coaching (13), **Deal Pulse (08)**, MEDDPICC Analysis (09), Stakeholder Mapping (10). This skill adds the sixteen-signal health read, which the element-by-element scoring builds on.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name. This skill is free and works without any kit. This skill also reads the kit's hand-off block back as optional context (`case_status`, `hard_value`, `payback_months_hard`, `open_bets` and `next_action`), and it never presents an ASSUMPTION line from the kit as a buyer fact. The fields the kit reads from this skill:

- `account`
- `run_date`
- `health_score`
- `risk_level`
- `next_action` (the stage check, and the context for the Budget Path signal)

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

### 2.1.6 (2026-10-26)
- Consistency pass across the sales skills. Example 1's Evidence Confidence is recounted under the 90-day window, so the discovery call dated before the window is no longer counted. Its demo on Brackhaven's own plot records is dated, and its quantified pain is quoted from the call that holds it.
- Example 1's champion tests are one list, each tagged with its own date, and the Champion Strength reasoning uses that list.
- Example 2 dates the close-date moves, so the Timeline Alignment RED reads the two-or-more row. Its pain, responsiveness and engagement readings use the dated records, including the pre-need walkthrough, which is not a demo.
- Example 2 states in one sentence how a Strong champion status relates to a YELLOW Champion Strength signal, because each signal is scored on its own rubric. Its MEDDPICC reference is updated to the revised MEDDPICC score for the same day.
- No health score, verdict, band or risk level changes.

### 2.1.5 (2026-10-26)
- The invented CRM dated-action context line in the second pulse is removed, and its next actions carry the shared rule's date.
- The next action follows the family's one deadline rule. The Output Contract points to that rule, and each example names the record (a proposed date in the notes or a dated CRM action) when that record sets an earlier date.
- No score, verdict, band or risk level changes.

### 2.1.4 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. Signal 1 states how a champion who is also the buyer contact counts, and that a quantified account counts only within 14 days of the score. Signal 4 states what decision influence means. Signals 9 and 14 state how an unnamed economic buyer is scored. The Technical Readiness action states who asks about IT. The hand-off block is written out in the Output Contract, with its field order and the meaning of each value. Example 1 gains a second stakeholder on the pain and a note on the date of its call facts. Example 2 applies the 14-day rule to the pain. No score, verdict, band or risk level changes.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The try-it records carry the dated commitments, the meeting attendance and the four named champion tests that Signals 4, 13 and 15 grade GREEN on.
- Rubric: one sentence each on Signal 5 (validated requirements), Signal 11 (buyer-validated close date) and Signal 15 (what counts as a commitment). Each settles a boundary Example 1 already decided.
- Example 1 gains the report header, the Overall Assessment and an evidence line for each of its seven YELLOW signals. Example 2 dates are made consistent with Example 1. No score, verdict, band or risk level changes.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1.
- Example 1 gains the invented facts its GREEN and RED calls rest on: a time figure for the double sale (Pain Clarity), a requirements count (Product Alignment), the buyer's confirmed close date (Timeline Alignment), a stated departmental goal (Strategic Initiative), and a proposed date for the technical discovery (the next action's date). The try-it records carry the same facts. Example 1 also gains its Evidence Confidence line.
- Rubric: the Strategic Initiative RED row and the Multi-Threaded Engagement GREEN row each gain one sentence that settles the boundary Example 1 already decided.
- The Recommended Actions Framework names a method for Strategic Initiative Alignment (rapport) and Technical Readiness (urgency). Example 1's Technical Readiness action names the urgency method.
- No score, verdict, band or risk level changes.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1.
- Unknown signals are left out of the health math. A signal with no evidence is scored INSUFFICIENT, with no value, and counted in neither the sum nor the count. The health score is shown only when 12 or more of the 16 signals are scored, with its count beside it. Updated in the Output Contract, Health Score Calculation, Step 7, the report template, the Epistemic Rules, the Quality Bar and Data Sufficiency Fallback. Examples 1 and 2 score all 16 signals, so their numbers do not change. "Scored 16 of 16" is added to their Health lines.

### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`) and offers read-only CRM connectors through the shared contract's Knowledge Base and Connectors section, before the CRM deal read.
- Adds a Chains subsection placing the skill in the Work The Deal chain.
- Adds a Guild Pro Kits subsection naming the hand-off fields the Business Case & ROI Kit reads, and the kit's fields this skill reads back.

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
