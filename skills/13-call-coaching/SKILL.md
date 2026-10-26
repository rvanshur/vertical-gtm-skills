---
name: gtm-call-coaching
description: "Scores a discovery or demo call against methodology rubrics and returns a coaching report with evidence-graded coaching points, for the rep and the sales manager who reads it"
version: 2.1.3
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [call-coaching, discovery-coaching, demo-coaching, sales-methodology, call-scoring, coaching-scorecard]
requires:
  skills: ["gtm-meeting-prep", "gtm-deal-pulse"]
mutating: read-write
change_log:
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1: Pre-Call Preparation, Active Listening and Alternatives have their evidence on the record, and one sentence each settles the partial-markers case, the Winning Zone, the post-call date, the champion test about process, the focus-area tie-break and the before read of Deal Health Impact. The try-it notes that its records predate the account's later stage."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1, and the Unknown Rule added: a category with no evidence is INSUFFICIENT, the total reads scored n of N, and below five scored categories there is no overall score. The example's sections, Top 3 lists and single focus area now match the rubric."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection and a Guild Pro Kits subsection."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Sales 2.0 standard. Discovery adds an Alternatives category (7 categories, N of 35) and restated bands. Demo adds five demo elements, pacing defaults, ROI formulas, per-attendee block and technical checklist. Seven key-moment types, evidence grades, unraised objections checklist, per-phase question review, shared champion tests and talk-time bands by reference, Epistemic Rules, hand-off fields by name."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added."
---

# Call Coaching

## Overview

Scores a discovery or demo call against the client's sales methodology. It reads a transcript or detailed notes, scores each category of that call type from 1 to 5 with the evidence behind the score, maps pains to the client's buyer pain list, assesses MEDDIC coverage, marks the key moments, and writes coaching points that each carry the rep's own words or a grade for how sure the coach is. The call type decides the rubric: discovery scores 7 categories out of 35, demo scores 8 categories out of 40.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Every coaching point carries the rep's own words or a grade that says how sure the coach is.

---

## Why This Skill Exists

Calls are graded from memory. A rep who hears "good call" cannot repeat it, and a manager who says "you talked too much" cannot show where. Two managers listening to the same call often reach different verdicts, because each grades against a private idea of a good call. The rep then has no way to check the feedback against the recording.

This skill fixes the rubric in place and attaches every coaching point to something the rep can check: a quote with its time, or a grade that says the point is a paraphrase or an inference. A score that cannot show its evidence is not written.

---

## Role

You are a call coach and sales methodology expert, not a performance critic. You grade calls against the frameworks the client runs, find the moments that changed the outcome, and give the rep specific language to practice. You refuse to score without evidence, to coach without a quote or a grade, and to turn a call score into a compensation figure. The reasons sit in **Hard Rules**.

Everything company-specific (the pain list, the proof points, the competitive landscape, the stage gates) comes from the client profile (see **Context**), so the same skill coaches calls for any vertical.

---

## Input Contract

If a required input is missing, ask. Do not guess.

To try the skill without your own data, use `examples/try-it.md`, which holds the inputs for Example 1.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The account on the call |
| Sales rep name | Required | Who ran the call. The coaching is addressed to this person |
| Call type (`discovery` or `demo`) | Required | The method forks on this. Discovery scores 7 categories out of 35. Demo scores 8 out of 40. If it is missing, ask |
| Transcript or notes | Required | A verbatim transcript is preferred. Detailed notes work with a confidence caveat. Notes cannot show talk share or exact language, so those are marked Unknown |
| Call date and duration | Optional | Used for timestamps and the before and after comparison |
| Attendees (names and titles) | Optional | Demo: needed for the per-attendee block. Missing names are written as `[Unknown]` |
| Meeting Prep sheet | Optional | The prep sheet for this call. Without it, Pre-Call Preparation is scored from what the call shows and the report says so |

---

## Output Contract

Every run returns the coaching report in the chat, in the eight sections under Report Sections below. It writes a file only when the user asks for one.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Coaching report | Inline, in the chat | The eight report sections, in order |
| `call_score` | Inline, the scorecard Total | Written as `N of M, scored n of 7` (discovery) or `N of M, scored n of 8` (demo), where M is 35 or 40 and n counts the categories with evidence. The same figure as the Total row. Under the Unknown Rule (Step 2), a total with fewer than five scored categories is not written |
| `category_scores` | Inline, the scorecard | One score from 1 to 5 per category, each with its evidence line |
| `focus_area` | Inline, the Next Call Game Plan | One skill to practice on the next call, with its exercise. Never a list of five |
| `coaching_points` | Inline, Top 3 Strengths and Top 3 Improvements | Each point carries a quote with its time, or one of the evidence grades Strong, Moderate or Weak |
| `key_moments` | Inline, the Key Moments section | Each moment has its type from the seven key-moment types and the fields that type requires |
| `champion_status` | Inline, the MEDDIC Status section | Strong, Developing or None, with the shared champion tests met on this call, each tagged |
| `report_path` | Set only when a file was written | `none (inline)` when the report stayed in the chat |
| `next_action` | Inline, last line of the report | One step, with its owner and a date. A date not yet agreed is written as `[Unknown]` |
| File, on request | `<account>_gtm-call-coaching_<date>.md`, beside the user's account notes | Written only when the user asks, in Markdown. The ask is the approval step |

### Report Sections

1. Call Summary: account, rep, date, call type, overall score, assessment, deal impact
2. Methodology Scorecard: the category scores with their evidence
3. MEDDIC Status: the six-element coverage grid and the champion status
4. Pain Discovery Map: each pain with its depth level and its profile category
5. Key Moments: wins on one side, coaching opportunities on the other
6. Framework-Specific Coaching: each point tied to a technique, with example language
7. Competitive Intel Summary: the current solution, the rep's satisfaction reading, the gaps and the positioning
8. Next Call Game Plan: prep, questions, the framework practice and the success criteria

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Account framing and vertical context |
| Buyer Personas | Which attendee each coaching point belongs to, and the persona's language |
| Core Pain Points | The listen-for phrases (the "What to Listen For" column) in Step 4, the "Discovery question" column in the question review, and the pain map |
| Proof Points | Resistance handling and value coaching. Each proof point is named with its Status, and an Illustrative one is never cited to a prospect |
| Competitive Landscape | The competitor probes the rep should have asked |
| Sales Methodology | Which frameworks the team runs, any talk-time bands it overrides, and the Qualification Stage Gates the call should move toward |
| Call Coaching | The team's category names, demo element names, pacing overrides and extra listen-for phrases. This is the sales-layer section that this skill's CUSTOMIZE interview writes |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (its earlier calls, notes and decisions), and the personas under `people/` |

If the Call Coaching section is missing, the skill says so once at the start and runs uncustomized. It uses the default category names and the starting pacing defaults, and it marks every coaching point that depended on the missing section. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

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

Your coaching playbook, in code. The frameworks below are the skill's defaults. **SPIN and Priority Ladder are used for discovery. Challenger, MEDDPICC and Question the Problem are used for demos.** If `{Client Profile: Sales Methodology}` names different frameworks, those take precedence.

The champion tests, the seven incumbent types and the talk-time bands are defined once, in The Shared Contract above. This skill refers to them and never restates them.

### Discovery: SPIN Selling Framework
| Phase | Purpose | What Great Looks Like |
|-------|---------|----------------------|
| **S (Situation)** | Understand current state | Asks about current process, systems, team structure, coverage, volume |
| **P (Problem)** | Surface business impact | Probes: "What happens when [X] fails?" "What's the cost?" |
| **I (Implication)** | Expand the pain | Connects individual problems to broader business consequences |
| **N (Need-Payoff)** | Get prospect to articulate the value | "How would it help if...?" "What would that mean for your team?" |

### Discovery: Priority Ladder
Identify: "Walk me through what that looks like step by step"
Prioritize: "On a scale of 1-10, how urgently does this need to change?"
Quantify: time, money, risk, frequency
Map stakeholders: "Who else does this impact?"

**Key rule:** Do not demo until Priority Ladder is complete.

### Discovery: Alternatives and the Negative-Frame Close
Alternatives are what the buyer has already tried for this problem. A buyer who has tried and stopped has told you what it cost them to stop. The rep asks about each attempt, why it stopped and what it cost.

**Negative-frame close (one line, generic words):** "Would it be a bad idea to keep doing it the current way for another quarter?" It asks the buyer to say why waiting is a problem, which is the discovery the call needs.

### Demo: Challenger Sale Framework
| Element | Principle | What Great Looks Like |
|---------|-----------|----------------------|
| **Teach** | Lead with insight the prospect did not know | Commercial teaching moment that reframes how they think about the problem |
| **Tailor** | Customize message to individual stakeholders | Different message for different personas, connects to their specific outcomes |
| **Take Control** | Drive the conversation and create constructive tension | Comfortable pushing back, proposes next steps, does not wait for permission |

### Demo: Five Demo Elements and Pacing
A demo has five elements. Questions are not a sixth element. They run through the solution and the return on investment, and they score under Question the Problem.

| Demo element | Demo category it scores under | Starting pacing default |
|---|---|---|
| Introduction (agenda, attendees, the outcome both sides want) | 1 Meeting Opening | 5% to 10% of the call |
| Problem restatement (the confirmed pains, in the buyer's words) | 6 Pain-to-Workflow Mapping | 5% to 10% of the call |
| Solution (one workflow at a time, each tied to a pain) | 3 Teach and Tailor | 40% to 50% of the call |
| Return on investment (the buyer's own figures, using the formulas below) | 4 Pain Alignment and Proof | 15% to 20% of the call |
| Questions (Question the Problem checkpoints) | 5 Question the Problem | 15% to 20% of the call |
| Next steps (named owner, date and attendees) | 2 Meeting Closing | 5% to 10% of the call |

Categories 7 (Prospect Engagement) and 8 (Resistance Handling) run across all five elements and are scored over the whole call.

**Team names.** Where the profile's Call Coaching section names the five elements, the report uses those names. The shares stay as set in the pacing table unless the profile overrides them.

**The half rule.** In a demo the prospect talks for about half of the call. Read the prospect's share as the rest of the call, measured against the demo band in The Shared Contract. A demo where the prospect talks well under that band is a presentation to an audience, not a conversation with a buyer.

**Pacing is a starting default.** The shares above are a starting point for the team to calibrate. Where the profile's Call Coaching section sets its own pacing, the scores use the team's numbers and the report says so.

### Demo: Meeting Open and Close
**Opening:** Connect to the pain from discovery. Confirm the time and who is in the room. Agree the agenda together. Agree what a good outcome would be.
**Closing:** Recap what mattered most to them. Ask who else should join next time. Propose the next agenda. Agree the next step, with an owner and a date.

### Demo: Question the Problem
Prime Pain: "Many teams struggle with [X]. To what extent is that true for you?" (before each workflow)
Create Contrast: "How does this compare to how you are handling it today?" (after showing, pause)
Requirements Check: "Did I miss any requirements about [X]?" (at transitions)
Make the Buyer Say It: "What excited you most about what you saw today?" (at close)

### Demo: Return on Investment Formulas
Three formulas. Every input is blank until the buyer or the rep supplies it, with its source. **Use your own figures, no defaults.** A figure invented in front of a buyer costs more than the deal it was meant to win.

- **Working capital released per year** = ____ items held × $____ value per item × ____% carrying rate, from the buyer's own finance team
- **Labor value per year** = (____ tasks per week × ____ minutes per task today, minus ____ tasks per week × ____ minutes per task after) × 52 weeks ÷ 60 × $____ loaded hourly cost
- **Risk reduction per year** = ____ incidents per year × $____ cost per incident × ____% reduction the change is expected to deliver

Record each result in the buyer's words, tagged with its source. A formula with a blank input is not reported as a result.

### Demo: Per-Attendee Block and Technical Checklist
**Per-attendee block.** One block for each person in the room. Missing names are `[Unknown]`, never guessed.

- **Attendee:** name or `[Unknown]`, title
- **Buying role:** as the record names it
- **Pain they own:** the matching pain from Core Pain Points, tagged
- **Question they asked:** the quote and its time, or "none asked"
- **What they need to see:** tagged to a quote, or marked Unknown
- **Engagement:** the quote or silence that shows it

**Five-line technical checklist.** Score each line Yes, No or Unknown. Unknown means the notes do not show it.

1. Screen share and audio were tested before the start.
2. Every attendee's access was confirmed before the call.
3. The data the demo showed was the prospect's own, or the gap was named in the opening.
4. A backup was ready if the screen failed (a recording or a second device).
5. Attendee names and titles matched the invitation, with any gap marked Unknown.

### Coaching Moment Template
Every improvement point is written in three parts. Each part is tagged.

- **Situation:** what the rep faced, with the quote and its time
- **Proof point:** the proof from the profile that answers it, with its Status shown. An Illustrative proof point is never cited to the prospect. A Benchmark is named with its source, and it is the line the rep says
- **Coaching moment:** the exact sentence the rep should have said instead, and the framework technique it practices

### Evidence Grades
| Grade | Meaning |
|---|---|
| **Strong** | A quote with its time from the call |
| **Moderate** | A paraphrase of what was said, with its time |
| **Weak** | Inferred from what did not happen, with the reasoning written |

Every coaching point carries a quote or a grade. A point with neither is removed.

### Unraised Objections Checklist
Six lines, scored for every discovery and demo call. Each line is Raised, Not raised or Unknown, with the evidence.

- Budget
- Implementation
- Change resistance
- Competitors
- Timing
- Authority

A line marked Not raised is a finding only when the call gave the buyer a fair chance to raise it. Otherwise it is Unknown.

### Universal: Three Types of Resistance
| Type | Definition | Response |
|------|-----------|---------|
| Reactance | Emotional pushback, feels pressured | Back off, give autonomy, negative framing |
| Skepticism | Logical doubt, does not believe | Proof: Feel-Felt-Found, case studies, data |
| Inertia | Resistance to change itself | Quantify cost of inaction |

### Universal: Three-Step Turnaround (RBO Handling)
Acknowledge: "That makes sense."
Redirect: "Most teams say that until they see..."
Advance: "What would need to be true for this to be worth 15 minutes?"

### Universal: Active Listening
Encourage, Restate, Silence, Paraphrase, Reflection, Clarifying.

### Universal: Feel-Felt-Found
Feel (validate emotion), Felt (normalize with peer), Found (deliver outcome).

---

## Quick Reference

**Use this skill when:**
- Reviewing a discovery or demo call recording or transcript
- Conducting a manager 1:1 with coaching
- Self-coaching after a call
- Building a rep development plan

**Do not use when:**
- Preparing for an upcoming call (use `gtm-meeting-prep`)
- Scoring deal health without a specific call (use `gtm-deal-pulse`)

**Call type parameter:**
- `call_type = discovery`: 7 categories, scored against SPIN, Priority Ladder and Alternatives. Total out of 35.
- `call_type = demo`: 8 categories, scored against Challenger, MEDDPICC and Question the Problem. Total out of 40.
- If not specified, ask. The call type decides the rubric.

**User roles:** AE, Sales Manager, Sales Coach

**Expected time:** 20 to 30 minutes per call

---

## Core Workflow

### Step 1: Gather Call Context

Before pulling anything, read the account's folder under `accounts/` (its earlier calls, notes and decisions) and the personas under `people/` in the knowledge base, when the profile has one. Then offer to read the call recording or transcript from the call recorder, and ask before reading it, as set out in The Knowledge Base and Connectors.

**1a. Confirm inputs:** account name, sales rep name, call date and duration, call type, transcript or notes, attendees with titles.

**1b. Read the prep sheet, if one exists.** Read the Meeting Prep fields by name: `prep_sheet`, `top_pain`, `question_bank`, `attendees` and `proof_point`. Read them before scoring, because Pre-Call Preparation is scored against them. A missing field is reported as missing, not rebuilt here.

**1c. Pull CRM context:** stage, amount, close date, owner, contacts and their roles, prior touchpoints, and any earlier coaching report. If a Deal Pulse exists, read its fields by name (`health_score`, `risk_level`, `pillar_scores`, `signal_scores`, `next_actions`) for the before and after comparison.

**1d. Check the source.** A transcript with speaker labels supports every category. Notes support the categories their evidence allows. Where the source cannot show talk share or exact language, those are marked Unknown and the report says why. Unknown is never scored as zero. A category that cannot be scored without them is INSUFFICIENT under the Unknown Rule in Step 2.

**Produces:** the confirmed input list, the prep fields read or marked missing, and one line on the source quality.

### Step 2: Score Methodology Execution

**The Unknown Rule.** A category with no evidence is INSUFFICIENT. It carries no value, and it is left out of the total and the count. The total is written `N of M, scored n of 7` (or `scored n of 8` for demo), with N the sum of the scored rows. With five or six categories scored, the total is shown with its scored count and no assessment band is given, because the bands were set for a full call. With fewer than five scored categories there is no overall score, and the report lists the evidence that would score each missing category. Each INSUFFICIENT row says what evidence is missing.

**Partial Markers.** A score is the highest line whose every marker the record shows. Where the record shows some markers of a line but not all, the score is the line below it.

**If `call_type = discovery`** (score 7 categories, out of 35):

If the profile's Call Coaching section renames the categories, the report uses the team's names. The rubric and the weights do not change.

#### Category 1: Pre-Call Preparation (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Opened with specific industry knowledge, referenced prior interactions, clear agenda, knew prospect role |
| 4 | Referenced account research, set basic agenda, knew prospect title |
| 3 | General awareness but no specific preparation evident |
| 2 | Generic opening, no personalization, read from script |
| 1 | No preparation. Asked basic questions already in CRM. |

#### Category 2: SPIN Discovery Quality (1-5)
| Score | Evidence |
|-------|----------|
| 5 | All 4 phases executed. Situation specific. Problem surfaced financial impact. Implication expanded pain. Need-Payoff got prospect articulating value. |
| 4 | 3 of 4 phases well executed. Good pain discovery with depth. |
| 3 | 2 of 4 phases well executed. Situation and some Problem, with Implication or Need-Payoff missed or cut short. |
| 2 | Mostly Situation questions. Jumped to solution before understanding pain. |
| 1 | Feature dump. No discovery. Talked product before understanding prospect's world. |

#### Category 3: Priority Ladder Execution (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full Priority Ladder on 1+ pain: identified → prioritized (1-10) → quantified → mapped stakeholders |
| 4 | Identified and prioritized pain, attempted quantification, some stakeholder mapping |
| 3 | Identified pain but didn't prioritize or quantify. Surface-level. |
| 2 | Accepted first answer without going deeper. Moved on too quickly. |
| 1 | No Priority Ladder. Jumped from hearing pain to pitching features. |

#### Category 4: Active Listening (1-5)
Rep talk time is read against the discovery band in The Shared Contract. "Points" below are share points on the call: 5 points is 5% of the call's talk time, measured from the band's nearest edge.

| Score | Evidence |
|-------|----------|
| 5 | Rep talk time inside the discovery band. Restating, silence and clarifying all used. Prospect's language captured. Follow-ups built on the answers. |
| 4 | Rep talk time within 5 points of the band, or one listening technique missing. |
| 3 | Rep talk time 5 to 10 points outside the band. Some scripted questions disconnected from the answers. |
| 2 | Rep talk time 10 to 20 points outside the band. Monologued. Asked but did not listen. |
| 1 | Rep talk time more than 20 points outside the band. Feature presentation disguised as discovery. |

#### Category 5: Value Articulation (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Connected capabilities to stated pains using prospect's language. Feel-Felt-Found with relevant case study. Stayed in Winning Zone. |
| 4 | Connected some capabilities. Referenced a customer story. Mostly in Winning Zone. |
| 3 | Generic pitch (correct but not personalized to prospect pains). |
| 2 | Feature list without pain connection. Talked about irrelevant capabilities. |
| 1 | No value articulation or pitched features without discovery. |

The Winning Zone is the part of the call where each capability is tied to a pain the prospect named in their own words. A value claim with no named pain sits outside it.

#### Category 6: Next Steps and Momentum (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Leadership-based recommendation. Specific actions with owners and dates. Identified next meeting attendees. |
| 4 | Clear next step with date. Some ownership established. |
| 3 | Vague ("I'll send info" or "Let's reconnect" without specifics). |
| 2 | Prospect drove next steps. Rep was passive. |
| 1 | No next step established. Call ended without forward motion. |

A date that the rep sets by email after the call is not on the call. It counts in the Next Action line of the hand-off, and this score reads only what the call shows.

#### Category 7: Alternatives (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Asked about every alternative the buyer has tried, why each one stopped, and what each one cost. |
| 4 | Asked about each alternative and why it stopped. Cost not asked. |
| 3 | Asked about the current solution only. Earlier attempts not explored. |
| 2 | Named an alternative the buyer raised, then did not ask about it. |
| 1 | No question about alternatives. Assumed the buyer had tried nothing. |

**Question review (discovery).** For each SPIN phase, quote the rep's question, rate it, and write one better question. Ratings are Strong, Adequate, Weak or Missing (no question asked in that phase). The better question draws on the Core Pain Points "Discovery question" column where one fits.

| Phase | Question quoted (with its time) | Rating | One better question |
|---|---|---|---|

**Discovery score interpretation (out of 35):**

| Total | Assessment |
|-------|-----------|
| 31 to 35 | Excellent (textbook methodology) |
| 24 to 30 | Good (strong with minor gaps) |
| 17 to 23 | Needs Improvement (significant gaps) |
| 10 to 16 | Poor (fundamental issues) |
| 7 to 9 | Critical (immediate intervention needed) |

**Arithmetic for the restated bands.** The original bands were set for a maximum of 30. For the maximum of 35, each old lower cut-off is multiplied by 35, divided by 30, and rounded up to a whole number. 26 × 35 ÷ 30 = 30.3, so 31. 20 × 35 ÷ 30 = 23.3, so 24. 14 × 35 ÷ 30 = 16.3, so 17. 8 × 35 ÷ 30 = 9.3, so 10. The floor is 7, because seven categories at 1 each is the lowest possible total, and 6 × 35 ÷ 30 = 7.0 gives the same figure.

**If `call_type = demo`** (score 8 categories, out of 40):

#### Category 1: Meeting Opening (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full opening: Anchored on specific pain, confirmed logistics/attendees, set mutual agenda + "anything else?", defined end-of-meeting outcome |
| 4 | 3/4 elements. Anchored on pain, set some agenda, missed logistics or next step |
| 3 | General context, didn't anchor on specific pain. Basic agenda. |
| 2 | Jumped straight to demo ("Let me show you the platform") |
| 1 | No structure. Launched screen share immediately. |

#### Category 2: Meeting Closing (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full close: Transitioned cleanly, asked who attends next, proposed specific agenda, leadership recommendation ("Sound fair?") |
| 4 | Clear next step with date. Some multi-threading. Missing one element. |
| 3 | Vague ("I'll send info" without specifics). |
| 2 | Prospect drove close. Rep passive. |
| 1 | No close. Ended abruptly. No forward motion. |

#### Category 3: Teach and Tailor (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Effortless flow: one workflow at a time, prospect's language, no jargon. Led with commercial insight. Message tailored to each persona present. Recap mapped each section to pain. |
| 4 | Mostly clear with minor backtracking. Brief off-topic detour. Most features connected to pains. |
| 3 | Some structure, jumped between features. Mix of relevant and irrelevant content. Generic recap. |
| 2 | Confusing (bounced between screens, showed irrelevant features). Significant off-topic time. |
| 1 | Feature tour. No narrative. No connection to prospect. Internal jargon. |

#### Category 4: Pain Alignment and Proof (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Every workflow tied to a discovery pain, named before each. The top pain gets the largest share of demo minutes. Proof matched on persona, scale and vertical, with its Status shown. Feel-Felt-Found used. Return on investment run with the buyer's own figures. |
| 4 | Pain referenced before most workflows. Mostly correct ordering. Relevant but not perfectly matched proof. |
| 3 | Some pain references, not systematic. Time did not match priority. Generic social proof. |
| 2 | Not ordered by pain. Equal time on all features. Wrong-scale proof. |
| 1 | No pain reference. Generic demo. No social proof. |

#### Category 5: Question the Problem (1-5)
| Score | Evidence |
|-------|----------|
| 5 | All 4 questions: Primed pain before every workflow, created contrast + PAUSED, requirements checks at transitions, closed with "What excited you most?" and captured answer. |
| 4 | 3/4 used effectively. Good contrast. Some buying language captured. |
| 3 | Prime Pain sometimes. Contrast asked once or twice, didn't pause enough. No transition checks. Generic close. |
| 2 | Minimal questioning. Showed features without checking contrast. "Any questions?" close. |
| 1 | Pure monologue. No questioning during demo. No contrast, no checks, no close question. |

#### Category 6: Pain-to-Workflow Mapping (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Every discovery pain mapped to a workflow. Shown in pain priority order. Rep referenced discovery findings. Demo data relevant. |
| 4 | Most pains mapped. Mostly correct ordering. Some discovery references. |
| 3 | Some pains addressed, mapping implicit not explicit. Standard demo flow. |
| 2 | Disconnected from discovery. Features don't map to stated pains. |
| 1 | Complete disconnect. Same demo shown to every prospect. |

#### Category 7: Prospect Engagement (1-5)
Prospect talk time is read against the demo band in The Shared Contract, measured from the band's edge. "Points" are share points on the call: 5 points is 5% of the call's talk time.

| Score | Evidence |
|-------|----------|
| 5 | Prospect talk time inside the demo band. Buying signals captured (implementation, pricing, timeline questions). Active listening. Prospect drove portions. |
| 4 | Prospect talk time within 5 points of the band. Some buying signals. Intermittent listening. |
| 3 | Prospect talk time 5 to 10 points under the band. Mostly passive. Few buying signals. |
| 2 | Prospect talk time 10 to 20 points under the band. Short answers. Rep dominated. |
| 1 | Prospect talk time more than 20 points under the band. Passive or disengaged. Rep lectured. |

#### Category 8: Resistance Handling (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Correctly diagnosed resistance type (reactance, skepticism or inertia) and applied the right response. Feel-Felt-Found with persona-matched proof. Three-Step Turnaround used. |
| 4 | Managed most resistance well. May have misdiagnosed once. Good social proof. |
| 3 | Addressed resistance with generic responses. Didn't use frameworks. |
| 2 | Met resistance with more features (wrong response). Got defensive. |
| 1 | Froze on objections. Ignored resistance. Or: no resistance because prospect wasn't engaged enough to care. |

**Demo score interpretation (out of 40):**
| Total | Assessment |
|-------|-----------|
| 34 to 40 | Excellent (prospect is selling themselves) |
| 26 to 33 | Good (refinement, not rebuilding) |
| 18 to 25 | Needs Improvement (specific framework practice needed) |
| 10 to 17 | Poor (feature touring or monologue) |
| 8 to 9 | Critical (requires immediate intervention) |

**Produces:** the scorecard table with every category, its score or INSUFFICIENT and its evidence line, the Total written as `N of M, scored n of 7` (or 8), and the question review for a discovery call.

### Step 3: Assess MEDDIC Coverage

For each MEDDIC element, assess what was uncovered on this call:

| Element | What to Assess | Grade |
|---------|---------------|-------|
| Metrics | Quantified outcomes discussed? | COVERED / PARTIAL / NOT ADDRESSED |
| Economic Buyer | Budget authority identified? | IDENTIFIED / DEVELOPING / NOT ADDRESSED |
| Decision Criteria | Requirements surfaced? | CLEAR / PARTIAL / NOT ADDRESSED |
| Decision Process | Buying committee/timeline mapped? | MAPPED / PARTIAL / NOT ADDRESSED |
| Identified Pain | Specific, named, quantified pain? | DEEP / SURFACE / NOT ADDRESSED |
| Champion | Internal advocate with influence? | STRONG / DEVELOPING / NONE |

**Champion status** is graded with the shared champion tests in The Shared Contract. Count only the tests met on this call, each with its evidence and tag. A contact who was not in the room cannot meet the tests that need the room, and the report says so. A statement about the buyer's process counts as "explains the internal politics" only when it says who decides or how the decision moves. "The board takes these things up" names no one, so it does not count.

**Produces:** the six-element coverage grid and the champion status (Strong, Developing or None) with the tests met on this call.

### Step 4: Map Pain Discovery Depth

**Find the pains in the buyer's words.** Use the "What to Listen For" column of the profile's Core Pain Points as the phrase list. Add any extra phrases the profile's Call Coaching section lists, each with the pain it points to. Each phrase heard on the call is recorded with its time and its tag, and the pain it points to is matched to the profile's pain list. A pain with no matching phrase is marked as not heard, not as absent.

For each pain discovered, assess depth using the Priority Ladder levels:

| Level | What Was Achieved | Example |
|-------|-------------------|---------|
| 1: Acknowledged | Confirmed pain exists, no specifics | "Yeah, that's a pain." |
| 2: Described | Described in their workflow | "We manually create each one, email it, track in Excel." |
| 3: Quantified | Measured: time, money, frequency | "15 minutes each, 200 per month, that's 50 hours." |
| 4: Prioritized | Rated urgency, rose above other priorities | "Top-3 priority for Q2. CFO asking every board meeting." |
| 5: Socialized | Other stakeholders impacted and identified | "Credit, collections, controller. CFO wants a fix by Q3." |

**Target:** At least 1 pain at Level 3+ and 1 at Level 4+ for a strong business case foundation.

Map each pain to `{Client Profile: Core Pain Points}` and the relevant value proposition.

**Produces:** the pains with their phrases, times and tags, each with its depth level.

### Step 5: Evaluate Competitive Intelligence (if applicable)

What was learned about the prospect's current solution:
- Solution identified? (competitor, manual, none)
- File the solution under one of the seven incumbent types in The Shared Contract.
- Contract status? (active, expiring, unknown)
- Satisfaction level? (frustrated, neutral, satisfied)

Reference `{Client Profile: Competitive Landscape}` for the competitor probes the rep should have asked.

**Produces:** the current solution with its incumbent type, its contract status and the satisfaction reading, each tagged, and the probes that went unasked.

### Step 6: Identify Key Moments

Mark each key moment with one of seven types. Capture the fields the type requires.

| Key moment type | Fields to capture |
|---|---|
| Objection | Time, quote, resistance type (reactance, skepticism or inertia), the response given |
| Buying signal | Time, quote, kind (implementation, pricing or timeline question), captured or missed |
| Discovery breakthrough | Time, quote, Priority Ladder level reached |
| Commitment | Time, quote, owner, date. A date that was not set is recorded as `[Unknown]` |
| Missed opportunity | Time, quote, the question that should have been asked |
| Competitive intelligence | Time, quote, incumbent type from The Shared Contract, contract status |
| Red flag | Time, quote, risk level (HIGH, MEDIUM or LOW), recovery step |

**Critical Wins:** What happened, why effective (framework alignment), the quote with its time.

**Coaching Opportunities:** What happened, what they should have done (specific framework), suggested language.

**Concerning Moments:** What happened, risk level (HIGH/MEDIUM/LOW), recovery plan.

**Demo-specific:** Buying Signals (captured vs. missed), and Anti-Patterns detected. Each anti-pattern is one line:
- **Feature Tour:** Walking through screens in order without tying any feature to a stated pain.
- **Happy Ears:** Treating polite interest as a buying signal when the call has no evidence for it.
- **Telling Not Asking:** Stating a benefit or conclusion the rep has not confirmed with the prospect.
- **Demo Before Discovery:** Starting the demo before the discovery pains and the Priority Ladder are complete.
- **Off-Topic Drift:** Spending time on material the prospect did not raise and that does not map to a pain.
- **Monologue Mode:** The rep talks for long stretches without a question or a pause for the prospect.
- **Weak Close:** Ending without a named next step, an owner and a date.
- **Generic Proof:** Using a case study or number that does not match the prospect's persona, size or vertical.

**Unraised objections.** Complete the six-line checklist under Methodology, with its evidence for each line.

**Produces:** the key moments by type with their fields, the anti-patterns found (demo), and the six-line unraised objections checklist.

### Step 7: Demo Checks (demo calls only)

1. **Pacing by section.** Estimate the minutes spent in each of the five demo elements, and the minutes in off-topic time. Set each against its starting default, or the team's default from the profile. Every minute figure carries its n against the call length (for example, 41 of 60 minutes).
2. **Per-attendee block.** One block for each person in the room, using the fields under Methodology.
3. **Technical checklist.** The five lines, each Yes, No or Unknown.
4. **Return on investment.** Record whether the call ran an ROI section and with whose figures. If the call gave no inputs, say so. Do not fill the formulas with defaults.

**Produces:** the pacing table, the per-attendee blocks, the checklist result and the ROI status.

### Step 8: Generate Coaching Recommendations

**Top 3 Strengths:** What they did well + why it matters + reinforcement. Each with its quote and time, or its grade.

**Top 3 Improvement Areas:** Each in the Coaching Moment Template (Situation, Proof point, Coaching moment), with its evidence grade. Each names the framework technique it practices, and a practice exercise.

**Deal Health Impact:** Before and after this call. The key risk. Buying signals to advance. Where the call moves the stage gate in the profile's Qualification Stage Gates, and where it does not.

**Focus Area for Next Call:** One skill only. Prep steps, what to practice, success criteria. Five things at once do not change a habit. When categories tie for the lowest score, the focus area is the one that gates the next stage in the profile's Qualification Stage Gates, as Priority Ladder does for the Stage 2 to 3 gate.

**Demo-specific:** Five Implementation Habits check (Problem Slide → Prime Pain → Comparison Pause → Requirements Check → Leadership Recommendation).

**Produces:** the coaching points with their quotes or grades, the one focus area, the deal health impact and the next action with its owner and date.

---

## Epistemic Rules

- **Every rate carries its n.** "3 of 7 shared tests met", "41 of 60 minutes", "5 of 6 unraised objection lines checked." A bare rate is not written.
- **One call is one observation.** A habit becomes a pattern only with five cases. This skill grades one call, so a habit seen on this call is reported as an observation with its count, never as a trend.
- **Silence is not a no.** A question that was not asked is unknown for that dimension, not a negative. A talk share the source cannot measure is Unknown, not zero. The category it scores is INSUFFICIENT under the Unknown Rule, and it is left out of the total and the count.
- **"No difference found" is a finding.** A call that scores the same as the rep's last call is reported as such.
- **Every coaching point is graded.** A quote with its time is Strong. A paraphrase is Moderate. An inference from what did not happen is Weak, and the reasoning is written.
- **Evidence over optimism.** Score what the record proves, not what the rep believes. Under-scoring protects a deal. Over-scoring kills it.

---

## Hard Rules

1. **No coaching point without a quote or a grade.** A point nobody can check is an opinion about the rep, and the rep is entitled to check it.
2. **No category score without its evidence line.** The total must be recomputable from the scored rows, or the rep cannot see how it was reached. An INSUFFICIENT row carries no value and is left out of the total and the count, so the total always reads with its scored count.
3. **Do not score from notes what needs a transcript.** Talk share, listening technique and exact language need the words. Notes cannot show them, so they are marked Unknown.
4. **Do not restate the shared lists.** The champion tests, the incumbent types and the talk-time bands live once, in The Shared Contract. A second copy drifts, and then two managers grade the same call against two rules.
5. **Never cite an Illustrative proof point to the prospect.** The profile marks it as invented for an example. The rep would be claiming a result that does not exist.
6. **Never fill a return-on-investment input with a default.** A made-up saving in front of a buyer is the fastest way to lose the deal. Use your own figures, no defaults.
7. **Never turn a call score into a compensation or ranking figure.** Once the score touches pay, reps perform for the grader and the coaching signal dies.
8. **Coach one focus area per call.** Five fixes at once do not change a habit, and the rep cannot practice all five.
9. **Every recommendation names a framework technique.** Generic advice does not change behavior, and a technique can be practiced and checked.
10. **Nothing is sent and nothing is written to the CRM.** The rep reads the coaching and decides what to do with it.

---

## Quality Bar

**Done when all are true:**

- [ ] Every category is scored from 1 to 5, with an evidence line
- [ ] The Total is written `N of M, scored n of 7` (or 8) and equals the sum of its scored rows, `call_score` is the same figure, and fewer than five scored categories gives no overall score
- [ ] Discovery: the question review covers all four SPIN phases, each with its quote and time
- [ ] Every coaching point carries a quote with its time, or one of the three evidence grades
- [ ] Every fact carries one of the six evidence tags
- [ ] Every rate carries its n
- [ ] Pains are matched to the profile's list, and the champion status shows the tests met
- [ ] Key moments use the seven types and carry their required fields
- [ ] Exactly one focus area is named, with a practice exercise
- [ ] The next action names an owner and a date, or states that the date is `[Unknown]`
- [ ] The hand-off block lists the fields by name

---

## Examples

All three examples use the PlotIQ example company and its cast. Every call-level fact is illustrative, and every fact carries one of the six evidence tags. Scores are this skill's own, from the rubric above, so each total can be recomputed from its rows.

### Example 1: Discovery Call (Good Execution, Stage 2 Discovery), Brackhaven Memorial Gardens

**Context:** Brackhaven Memorial Gardens is a combination of two sites with 11,000 plots and paper plot maps (`[CRM]`, illustrative). It is ACTIVE at Stage 2 Discovery (`[CRM]`). Owen Pruitt (Account Executive, illustrative assignment) ran the call with Ruth Ellery (General Manager, buyer, `[CRM]`) and Walt Okonkwo (Operations Director, influencer, `[CRM]`). The Meeting Prep sheet for this call is the first example in that skill. This call was graded from its transcript. Every `[Call]` tag is the call of 2026-05-12 (illustrative), and every time is its transcript time.

**Input:** "Coach the discovery call for Brackhaven Memorial Gardens. call_type = discovery"

**Call Summary:** Account Brackhaven Memorial Gardens (ACTIVE, Stage 2 Discovery `[CRM]`). Rep Owen Pruitt. Call date 2026-05-12 (illustrative). Call type discovery. Overall score 24 of 35, scored 7 of 7, assessment Good. Deal impact: the Stage 2 to 3 gate is not met, and the call does not move the deal to a demo (see Deal Health Impact below).

**Methodology Scorecard:**

| Category | Score (1 to 5) | Evidence |
|---|---|---|
| Pre-Call Preparation | 4 | Opened on the prep sheet's top pain, plot records on paper (`[Notes]`), and asked about the lookup at 02:10 (`[Call]`). Referred to both attendees by name at 00:40 (`[Call]`), set the agenda at 00:50 (`[Call]`), and named each attendee's title at 01:10 (`[Call]`). Did not check the double sale on file (`[CRM]`) before asking about it. |
| SPIN Discovery Quality | 3 | Situation and Problem well executed. Implication started at 19:05 and was cut short. Need-Payoff not reached. Two phases well executed, one started. |
| Priority Ladder Execution | 3 | Identified the plot lookup and described it, Level 2 (`[Call]`, 14:20). Not quantified: no count and no time. |
| Active Listening | 4 | Rep talk time 36% (illustrative), inside the discovery band (`[Call]`). Restated the files at 16:40 and clarified at 09:15 (`[Call]`). No silence used, so one listening technique is missing. One follow-up missing at 21:30, where Ruth described the lookups and Owen moved on. |
| Value Articulation | 3 | Generic pitch at 25:00 ("it fixes the paper problem," `[Call]`). No proof point used. The double sale was asked about, but not tied to the value. |
| Next Steps and Momentum | 3 | Owen asked for the approval body's chair and the meeting date at 28:30. Ruth said she would check with the board (`[Call]`). No date set on the call. Vague. |
| Alternatives | 4 | Asked what was tried before. Ruth said they began moving plots into the Oldgate system and stopped (`[Call]`, 17:05). Owen asked why it stopped. Cost not asked. |
| **Total** | | **24 of 35, scored 7 of 7** |

Assessment: Good, in the 24 to 30 band of the restated scale (see Step 2 for the arithmetic). All seven categories have evidence, so the Unknown Rule does not apply.

**Question review (discovery):**

| Phase | Question quoted (with its time) | Rating | One better question |
|---|---|---|---|
| Situation | "When a family asks for a plot, where do you look first, and how long does that take?" (02:10) | Strong | "How many of those requests come in during a typical week?" |
| Problem | "What happens when a plot sells twice?" (14:20) | Adequate | "When a plot sells twice, what does it cost the family and the site, and who finds out?" |
| Implication | "So that's a problem for the trust report too?" (19:05) | Weak | "If an auditor asked for last year's trust fund records today, how long would the pull take?" |
| Need-Payoff | None asked | Missing | "What would it mean for your team if a plot answer took 20 seconds instead of 20 minutes?" |

**Pain Discovery Map:** The plot-records pain, with its depth level. The phrase "We have files that date back to the 1970s" (09:15, `[Call]`) is on the profile's listen-for list for plot records on paper. The pain reached Level 2 (described) at 14:20. It did not reach Level 3, which is the minimum for a strong business case.

**Key Moments:**

- **Discovery breakthrough (14:20):** Ruth: "We sold section F twice last spring." `[Call]`. Priority Ladder Level 2. The double sale is the note on file (`[CRM]`), now confirmed in her words.
- **Buying signal, captured (09:15):** Ruth: "We have files that date back to the 1970s." `[Call]`. Owen asked "How far back do they go?"
- **Objection (23:40):** Walt: "I don't want my crew walking around with a tablet in a cemetery." `[Call]`. Type: skepticism. Owen's response: "They're just screens, you can use them at the desk." `[Call]`.
- **Competitive intelligence (17:05):** Ruth: "We started moving plots into Oldgate and stopped." `[Call]`. Incumbent type: direct software. Oldgate Ledger Pro, renewal March 2027 (`[CRM]`).
- **Missed opportunity (28:30):** Ruth: "The board takes these things up." Owen: "Great, thanks." `[Call]`. The question that should have followed: "Who sits on the board, and when does it next meet?"
- **Red flag, MEDIUM (31:10):** Ruth: "We don't really have an IT person." `[Call]`. Recovery: ask who installs the system and who holds the ledger data, before the next session.

**Framework-Specific Coaching:**

**Top 3 Strengths**

1. **Strength, Strong.** At 02:10 Owen asked, "When a family asks for a plot, where do you look first, and how long does that take?" `[Call]`. The question went to the process before the product. Keep it as the opener.
2. **Owen followed up, Strong.** At 09:15 Ruth said, "We have files that date back to the 1970s." Owen asked, "How far back do they go?" `[Call]`. The follow-up opened the depth of the records.
3. **Owen asked why the move stopped, Strong.** At 17:05 Ruth said, "We started moving plots into Oldgate and stopped." Owen asked why it stopped `[Call]`. That question is what the Alternatives score rests on.

**Top 3 Improvement Areas**

1. **Quantify the double sale, Strong.** At 14:20 Ruth said, "We sold section F twice last spring." `[Call]`. Owen moved on in the same breath, so the Priority Ladder stopped at Level 2. Practice: "How many plots did that cost you last year, and how long did each lookup take?"
2. **Benchmark for the tablet objection, Moderate.** At 23:40 Walt raised tablets. Owen's answer is paraphrased in the notes, so the grade is Moderate.
   - **Situation:** Walt's skepticism of tablets, 23:40 (`[Call]`).
   - **Proof point:** "most cemeteries your size carry 50 to 100 plots that are sold on paper and unsold on the map" (Benchmark, deathcare research, 2026-03-27 to 2026-04-01). The Holloway Hills proof point is Illustrative, so it is not cited.
   - **Coaching moment:** Say the benchmark, then ask, "How does that compare with what your crew sees?"
3. **The board question and the close, Strong, with a Weak part.** At 28:30 Ruth said the board takes these things up, and Owen said "Great, thanks" (`[Call]`). The chair's name and the meeting date were both within reach. Ask, "Who sits on the board, and when does it next meet?" The chair is still `[Unknown]` after this call. The last two minutes of the transcript contain no date for the next step. Inferred from what did not happen, so that part is Weak. Practice: set a date before the call ends.

**MEDDIC Status:**

| Element | Grade | Evidence |
|---|---|---|
| Metrics | PARTIAL | The double sale is named (14:20, `[Call]`), but no count and no cost. The lookup is at Level 2. |
| Economic Buyer | DEVELOPING | Ruth is named as GM and buyer `[CRM]`. The board chair is named by no one `[Unknown]`. |
| Decision Criteria | PARTIAL | Ruth asks what the board would need (33:00, `[Call]`). The criteria are not stated. |
| Decision Process | PARTIAL | The board takes these items up (28:30, `[Call]`). No date and no approval steps. |
| Identified Pain | SURFACE | Plot records on paper, described at Level 2 (14:20, `[Call]`). |
| Champion | DEVELOPING | Two of seven shared tests met (below). |

**Champion status:** Developing. Two of seven shared champion tests met on this call, each tagged: shares competitor intelligence (17:05, `[Call]`: "We started moving plots into Oldgate and stopped.") and asks how to help (33:00, `[Call]`: "What would you need from us to put this in front of the board?"). The 28:30 exchange is about process, the board taking the item up, so it is not counted as a test. Ruth's stronger status comes from later calls, not this one.

**Competitive Intel Summary:** Current solution: Oldgate Ledger Pro, direct software (`[CRM]`). Contract: renewal in March 2027 (`[CRM]`). Satisfaction: not stated on this call (`[Unknown]`). The gap: the move into Oldgate began and stopped (17:05, `[Call]`), and the cost of the stop was not asked. The probe that went unasked is what the move cost.

**Deal Health Impact:** Before this call: `[Unknown]`, because no Deal Pulse (08) exists for this account in the records. After this call: the Stage 2 to 3 gate in the profile needs the records problem quantified (plots, hours or dollars) and the GM named as the likely economic buyer. Ruth is named as GM and buyer (`[CRM]`). The problem is not yet quantified, so the gate is not met, and this call does not move the deal to a demo.

**Focus Area for Next Call:** Priority Ladder to Level 3 on the cost of a plot lookup. The chair and the date are success criteria in the game plan, not a second focus.

**Next Call Game Plan:**
- **Prep:** the plot-lookup count and the minutes per lookup, from the discovery notes.
- **Questions:** "How many plot requests come in a week, and how long does each one take?" Then the board question.
- **Success criteria:** a number for lookups per week, minutes per lookup, the board chair's name, and the meeting date, set before the session ends.

```text
Hand-off (read by 08, 09 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 2 Discovery)
run_date: 2026-05-12 (illustrative)
call_score: 24 of 35, scored 7 of 7
category_scores: Pre-Call Preparation 4, SPIN Discovery Quality 3, Priority Ladder Execution 3, Active Listening 4, Value Articulation 3, Next Steps and Momentum 3, Alternatives 4
focus_area: Priority Ladder to Level 3 on the cost of a plot lookup
coaching_points: Top 3 Strengths: 1 Strength, Strong (02:10). 2 Owen followed up, Strong (09:15). 3 Owen asked why the move stopped, Strong (17:05). Top 3 Improvements: 1 Quantify the double sale, Strong (14:20). 2 Benchmark for the tablet objection, Moderate (23:40). 3 The board question and the close, Strong, with a Weak part (28:30, no date in the transcript)
key_moments: discovery breakthrough (14:20), buying signal captured (09:15), objection (23:40), competitive intelligence (17:05), missed opportunity (28:30), red flag MEDIUM (31:10)
champion_status: Developing, two of seven shared tests met on this call (shares competitor intelligence, asks how to help)
next_action: Owen Pruitt books a second discovery session with Ruth Ellery to quantify the lookup cost. Owner: Owen Pruitt. Date: 2026-05-19 (illustrative)
report_path: none (inline)
```

---

### Example 2: Discovery Call (Second Discovery Booked, Not a Demo), Sable Fork Cemetery

**Context:** Sable Fork Cemetery is one site with 2,900 plots. Its plot list lives in a spreadsheet (`[Notes]`, illustrative). The account is INBOUND (`[CRM]`): it requested a demo through the website form on 2026-10-15 (`[CRM]`). Who filled in the form is `[Unknown]`. Its verdict is MANUAL REVIEW, with Zone 3 HIGH as the only HIGH zone (`[Inferred]`, from the zone scores in Account Qualification). The General Manager, Arlen Biggs, signs under $25K (`[CRM]`). Owen Pruitt (Account Executive, illustrative assignment) ran the call. The call date is illustrative. The call was graded from its transcript, so every `[Call]` tag is that call.

**Input:** "Coach the discovery call for Sable Fork Cemetery. call_type = discovery"

**Scoring:**

| Category | Score (1 to 5) | Evidence |
|---|---|---|
| Pre-Call Preparation | 3 | Used the prep sheet's hypothesis that the plot list lives in a spreadsheet (`[Inferred]`). Did not confirm who filled in the website form, which the sheet lists as `[Unknown]`. |
| SPIN Discovery Quality | 3 | Situation well executed (06:40, `[Call]`). The Problem phase began but the lookup count was not asked. Implication and Need-Payoff not reached. |
| Priority Ladder Execution | 3 | Described the lookup at Level 2 (19:30, `[Call]`). Not quantified. |
| Active Listening | 4 | Rep talk time 38% (illustrative), inside the discovery band. Restated the lookups well at 18:30. Missed the count at 18:45. |
| Value Articulation | 3 | Referred to "other cemeteries" with no figure at 29:00 (`[Call]`). No proof point used. |
| Next Steps and Momentum | 4 | Booked a second discovery session with Arlen Biggs on a named date, 2026-10-29 (illustrative), with Owen as owner. Other attendees not named. |
| Alternatives | 3 | Asked about the current process only, the spreadsheet (06:40, `[Call]`). Did not ask whether anything else was tried. |
| **Total** | | **23 of 35, scored 7 of 7** |

Assessment: Needs Improvement, in the 17 to 23 band of the restated scale.

**Question review (discovery):**

| Phase | Question quoted (with its time) | Rating | One better question |
|---|---|---|---|
| Situation | "Where does the plot list live, and who updates it?" (06:40) | Strong | "Where does the plot list live, who updates it, and when was it last updated?" |
| Problem | "What happens when a family asks for a plot and the list is out of date?" (12:10) | Adequate | "When a family asks for a plot and the list is out of date, what do you do, and how long does that take?" |
| Implication | "Does that happen often?" (15:30) | Weak | "What does a 20-minute lookup cost you, versus 20 seconds?" (the profile's discovery question for this pain) |
| Need-Payoff | None asked | Missing | "How would it help if a plot answer came in seconds?" |

**Key Moments:**

- **Discovery breakthrough (18:30):** Arlen: "I do most of the lookups myself." `[Call]`. Priority Ladder Level 2.
- **Missed opportunity (18:45):** Owen did not ask how many lookups happen in a week or how long each takes. The question that should have followed is the profile's discovery question for this pain, "What does a 20-minute lookup cost you, versus 20 seconds?"
- **Buying signal, captured (33:10):** Arlen asked how long setup takes. Owen answered that go-live is in about six weeks (`[Call]`, the profile's roadmap). Captured.
- **Competitive intelligence (09:20):** The current process is a spreadsheet (`[Call]`). Incumbent type: manual process. Contract status: none.
- **Commitment (40:20):** Arlen agreed to a second discovery session with Owen on 2026-10-29 (illustrative). Attendees: Arlen only. Owner: Owen.
- **Red flag, MEDIUM (44:00):** Arlen: "Nobody else looks at the list." `[Call]`. One person holds the data. Recovery: ask who else needs the list, by role.

**Coaching Points:**

1. **Strength, Strong.** At 06:40 Owen asked, "Where does the plot list live, and who updates it?" `[Call]`. Keep the question.
2. **Count the lookups, Strong.** At 18:30 Arlen said, "I do most of the lookups myself" (`[Call]`). Owen moved to the next topic at 18:45 without a count. Practice: "How many lookups does a typical week include, and how long does each one take?"
3. **Name a proof point without a number, Moderate.** At 29:00 Owen said other cemeteries have the same problem. The notes paraphrase the reply, so the grade is Moderate.
   - **Situation:** the lookup problem, 29:00 (`[Call]`).
   - **Proof point:** Fennick Gardens, 212 unsold plots found in 90 days. Status Illustrative, do not cite. The rep uses the Benchmark instead: "most cemeteries your size carry 50 to 100 plots that are sold on paper and unsold on the map" (Benchmark, deathcare research, 2026-03-27 to 2026-04-01).
   - **Coaching moment:** Say the benchmark, then ask, "How many of those do you think you have?"
4. **Second discovery, not a demo, Strong.** At 40:20 Owen did not offer a demo. He booked a second discovery session: "I'd like to see the list before I show you anything" (`[Call]`). Keep this. It is the right step while the pain is unconfirmed.
5. **Who else holds the list, Weak.** After Arlen said, "Nobody else looks at the list" (44:00), Owen did not ask who else needs it. Inferred from the question that did not come, so the grade is Weak. Practice: ask who else needs the list, by role.

**Champion status:** Developing. One of seven shared champion tests met on this call: commits to a next step with a date (40:20, `[Call]`).

**Deal Health Impact:** Sable Fork is INBOUND, so no ACTIVE stage gate applies yet. The pain is not confirmed: the lookup count is missing. The next step is a second discovery session, not a demo. The verdict stays MANUAL REVIEW.

**Focus Area for Next Call:** Ask the lookup-count question, then the who-else-holds-the-list question.

**Next Call Game Plan:**
- **Prep:** the spreadsheet's owner and update rhythm, and the form filler's name if the website shows it.
- **Questions:** the count question, then the who-else question. Then the Need-Payoff question.
- **Success criteria:** a number for lookups per week, minutes per lookup, and the name of anyone else who needs the list.

```text
Hand-off (read by 08, 09 and 06):
account: Sable Fork Cemetery (INBOUND)
run_date: 2026-10-19 (illustrative)
call_score: 23 of 35, scored 7 of 7
category_scores: Pre-Call Preparation 3, SPIN Discovery Quality 3, Priority Ladder Execution 3, Active Listening 4, Value Articulation 3, Next Steps and Momentum 4, Alternatives 3
focus_area: Count the lookups and time them, then ask who else holds the list
coaching_points: 1 Strength, Strong (06:40). 2 Count the lookups, Strong (18:30). 3 Proof point without a number, Moderate (29:00). 4 Second discovery, not a demo, Strong (40:20). 5 Who else holds the list, Weak (no question in the transcript)
key_moments: discovery breakthrough (18:30), missed opportunity (18:45), buying signal captured (33:10), competitive intelligence (09:20), commitment (40:20), red flag MEDIUM (44:00)
champion_status: Developing, one of seven shared tests met on this call (commits to a next step with a date)
next_action: Owen Pruitt holds a second discovery session with Arlen Biggs to count the lookups and time them. No demo until the pain is confirmed. Owner: Owen Pruitt. Date: 2026-10-29 (illustrative)
report_path: none (inline)
```

---

### Example 3: Demo Call (Needs Improvement, Non-Success), Brackhaven Memorial Gardens

**Context:** Owen Pruitt (Account Executive, illustrative assignment) demoed to Walt Okonkwo, Operations Director, and two operations staff at Brackhaven Memorial Gardens (`[CRM]`). Ruth Ellery, the General Manager and champion, was not in the room. The deal is ACTIVE at Stage 5 Negotiate (`[CRM]`). In discovery, Walt said he is skeptical of tablets (`[Call]`). This is the non-success case: the call did not answer the one objection that mattered to the room. The source is the call transcript (illustrative). The call date is illustrative, and the call length is 60 minutes (illustrative).

**Input:** "Coach the demo for Brackhaven Memorial Gardens. call_type = demo"

**Scoring:**

| Category | Score (1 to 5) | Evidence |
|---|---|---|
| Meeting Opening | 2 | Went to the screen at 03:10 with no reference to the discovery pains (`[Call]`). No agreed outcome. |
| Meeting Closing | 2 | The close was "Any questions?" at 58:20 (`[Call]`). No owner, no date. |
| Teach and Tailor | 3 | The trust report and the mobile app were shown in menu order, not in the order of Walt's pain (`[Call]`, 12:00 to 40:00). |
| Pain Alignment and Proof | 2 | No pain named before any workflow. Ruth's discovery pains not referenced. No proof cited (`[Call]`). |
| Question the Problem | 2 | No Prime Pain before any workflow, and no requirements check at a transition. The close did not ask what excited the buyer. |
| Pain-to-Workflow Mapping | 2 | Walt's "zero wrong-plot burials" and "find the plot in seconds" pains never came up. Weak grade: inferred from what did not happen. |
| Prospect Engagement | 3 | Prospect talk time 34% (illustrative), 6 points under the demo band, so 3 on the rubric. Walt asked two questions, both about tablets (`[Call]`). |
| Resistance Handling | 3 | Walt's tablet objection met with a reassurance and a second feature, not a question (`[Call]`, 23:40). |
| **Total** | | **19 of 40, scored 8 of 8** |

Assessment: Needs Improvement, in the 18 to 25 band.

**Pacing by section (Step 7):**

| Demo element | Starting default | This call (illustrative) |
|---|---|---|
| Introduction | 5% to 10% of the call | 2 of 60 minutes (3%) |
| Problem restatement | 5% to 10% of the call | 0 of 60 minutes (0%) |
| Solution | 40% to 50% of the call | 41 of 60 minutes (68%) |
| Return on investment | 15% to 20% of the call | 0 of 60 minutes (0%) |
| Questions | 15% to 20% of the call | 3 of 60 minutes (5%) |
| Next steps | 5% to 10% of the call | 1 of 60 minutes (2%) |
| Off-topic and screen navigation (not an element) | None | 13 of 60 minutes (22%) |

**Per-attendee blocks:**

- **Attendee: Walt Okonkwo, Operations Director.** Buying role: influencer (`[CRM]`). Pain they own: paper work orders, and finding the plot in seconds (`[CRM]`, Buyer Personas). Question they asked: two questions, both about tablets, and no question about the plot lookup (`[Call]`). What they need to see: the plot found in seconds, on their own records. Engagement: active on the tablet question, silent on the lookup.
- **Attendee: two operations staff, names `[Unknown]`.** Buying role: `[Unknown]`. Pain they own: `[Unknown]`. The transcript does not label them, so their engagement is Unknown.

**Technical checklist:**

1. Screen share and audio tested before the start: Unknown. Neither the notes nor the transcript show it.
2. Every attendee's access confirmed: Unknown.
3. The data shown was the prospect's own: No. Owen said at 12:00, "this is our sample cemetery" (`[Call]`).
4. Backup ready if the screen failed: Unknown.
5. Attendee names matched the invitation: Partly. Walt's name matched. The two staff names are `[Unknown]`.

**Return on investment:** No return-on-investment section ran. The call gave no inputs, so no formula was filled. Use your own figures, no defaults.

**Key Moments:**

- **Objection (23:40):** Walt: "I don't believe tablets will hold up out there." `[Call]`. Type: skepticism. Response given: a reassurance, "They're rugged, you'll like them." Not captured.
- **Missed opportunity (12:00 onward):** the paper work-order pain was never raised. The question that should have been asked: "Walk me through what a work order looks like on paper, from the counter to the crew."
- **Competitive intelligence (31:15):** Walt said the ledger runs on Oldgate `[Call]`. Incumbent type: direct software. Renewal March 2027 (`[CRM]`).
- **Red flag, HIGH (55:00):** No one in the room can approve the purchase. The economic buyer is the family board chair (`[CRM]`), name `[Unknown]`. Recovery: Ruth briefs Walt on the board's approval path before the next session.

**Coaching Points:**

1. **Telling, not asking, Strong.** At 23:40 Walt said, "I don't believe tablets will hold up out there." Owen replied, "They're rugged, you'll like them" (`[Call]`). That is the Telling Not Asking anti-pattern.
   - **Situation:** Walt's skepticism, 23:40 (`[Call]`).
   - **Proof point:** the profile has no proof on tablet durability. Say so, and do not borrow a number.
   - **Coaching moment:** Acknowledge ("That makes sense."), then ask, "What would need to be true about the tablets for your crew to use them?"
2. **Open on the pain, Strong.** At 12:00 Owen opened on the trust report, then the mobile app, in menu order (`[Call]`). Walt's pain never came up. Open with the pain: "In our last call you said finding a plot on paper takes too long at the counter. I'll show you that first."
3. **Pain-to-workflow map, Weak.** Walt's "zero wrong-plot burials" and "find the plot in seconds" are not in the transcript at any point. Inferred from what did not happen, so the grade is Weak. Practice: build the map from the discovery notes before the next demo.
4. **Question the Problem, Moderate.** The transcript shows no Prime Pain before any workflow. The first 20 minutes are summarized in the rep's notes, so the grade is Moderate.

**Champion status:** None on this call. Ruth Ellery was not in the room, so no shared champion test that needs the room could be met. Walt is an influencer (`[CRM]`).

**Deal Health Impact:** The call did not answer the tablet objection, which is the one that matters to the room. The buyer with the authority is the board chair (`[CRM]`), whom this call did not reach. The next session needs the approval path, not another feature tour.

**Focus Area for Next Call:** Build a pain-to-workflow map from the discovery notes and open with Walt's paper work-order pain. Practice Telling Not Asking: replace each reassurance with a question.

**Next Call Game Plan:**
- **Prep:** the pain-to-workflow map, the approval path from Ruth, and a backup plan for the screen.
- **Questions:** "What would need to be true about the tablets for your crew to use them?" Then the Prime Pain question before each workflow.
- **Success criteria:** Walt names the pain in his own words, and the next step has an owner and a date.

```text
Hand-off (read by 08, 09 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19 (illustrative)
call_score: 19 of 40, scored 8 of 8
category_scores: Meeting Opening 2, Meeting Closing 2, Teach and Tailor 3, Pain Alignment and Proof 2, Question the Problem 2, Pain-to-Workflow Mapping 2, Prospect Engagement 3, Resistance Handling 3
focus_area: Build a pain-to-workflow map from the discovery notes, open with Walt's paper work-order pain, and replace reassurance with questions
coaching_points: 1 Telling not asking, Strong (23:40). 2 Open on the pain, Strong (12:00). 3 Pain-to-workflow map, Weak (absent from the transcript). 4 Question the Problem, Moderate (summarized in notes)
key_moments: objection (23:40), missed opportunity (12:00), competitive intelligence (31:15), red flag HIGH (55:00)
champion_status: None on this call (Ruth Ellery not in the room)
next_action: Owen Pruitt sends Walt Okonkwo the pain-to-workflow map for the next demo, and Ruth Ellery briefs Walt on the board's approval path. Owner: Owen Pruitt. Date: 2026-10-22 (illustrative)
report_path: none (inline)
```

---

## Common Patterns

**The discovery that stops at Level 2.** The rep hears the pain and moves to the solution before anyone has counted it. Score it under Priority Ladder, quote the moment, and practice the count and the time.

**The warm contact who meets no test.** The contact is friendly and helpful and meets none of the shared champion tests. Grade the champion status by the tests, not by tone. A friendly contact is not a champion.

**The reassurance to a skeptic.** A buyer raises a doubt and the rep answers with more reassurance or another feature. Diagnose the resistance type first, then use the Three-Step Turnaround. Score it under Resistance Handling.

**The call that ends with "I'll send info".** No owner, no date, no attendees. Score Next Steps at 3 or below, and write the next action with its owner and date before the call ends.

---

## Troubleshooting

### "No transcript available (only rep notes)"
**Likely cause:** The call was not recorded, or no transcript was made.
**Solution:** Coach from notes and flag the reduced confidence: "Coaching based on rep notes only. Talk share, listening technique and exact language are Unknown. Coaching points rest on notes are graded Moderate at most."

### "Prospect talk time is missing from the transcript"
**Likely cause:** The transcript has no speaker labels, or more than two people spoke.
**Solution:** Do not guess a score. Ask for the labelled transcript and re-run, or score the category from the evidence that is present and say in the evidence line which part was scored.

### "Rep scored well but deal isn't progressing"
**Likely cause:** Good methodology on the call does not fix a deal with no champion or no budget path.
**Solution:** Good methodology execution doesn't guarantee deal progression if the fundamentals aren't there. Run `gtm-deal-pulse` to check if the deal has structural issues (no champion, no budget path) that call quality alone can't fix.

### "Call was a hybrid (started as discovery, turned into demo)"
**Likely cause:** The rep moved to the demo before the discovery pains and the Priority Ladder were complete.
**Solution:** Score as discovery (primary type). Note the demo elements that occurred, and flag the methodology risk: "Demoing before completing Priority Ladder reduces future negotiation leverage. Recommend completing discovery framework before next demo."

---

## Best Practices

### Do's
- **Quote or paraphrase specific moments**: "At 12:30, when the prospect said X, the rep should have..."
- **Reference exact frameworks**: "Use Priority Ladder Stage 3," not "ask better questions"
- **Balance praise and improvement**: 3 strengths plus 3 improvements minimum
- **Make coaching actionable**: include specific language the rep can practice
- **Grade every point**: a quote with its time, or Moderate or Weak with the reason

### Do not's
- **Do not score without evidence**: "seemed good" is not a score justification
- **Do not give generic advice**: every recommendation must tie to a specific framework
- **Do not coach on everything at once**: pick the #1 focus area for the next call
- **Do not skip the game plan**: coaching without a practice plan does not change behavior

---

## Integration With Other Skills

**Reads from the skills before it, by field name.** A missing field is reported as missing, not rebuilt here.

- **Meeting Prep (06):** `prep_sheet`, `top_pain`, `question_bank`, `attendees` (with buying role), `proof_point`. This skill grades the call against `question_bank` and `top_pain`, and checks the proof point the rep used against `proof_point`.
- **Deal Pulse (08):** `health_score`, `risk_level`, `pillar_scores`, `signal_scores`, `next_actions`. Read only for the before and after comparison in Deal Health Impact.

**Hands to the skills after it, by field name.**

- **Deal Pulse (08), MEDDPICC Analysis (09) and Meeting Prep (06):** `call_score`, `category_scores`, `focus_area`, `coaching_points`, `key_moments`, `champion_status`. Deal Pulse re-scores its signals with `champion_status` and `key_moments`. MEDDPICC Analysis uses the coaching points as evidence for its coverage grades.
- **Wrap-Up (O10):** `report_path` (set only when a file was written), `next_action` (owner and date).

**Related skills.** Meeting Prep before the call to plan it, then this skill after the call to score execution, then Deal Pulse to re-score the deal with what the call showed.

### Chains

- **Work The Deal:** Meeting Prep (06), **Call Coaching (13)**, Deal Pulse (08), MEDDPICC Analysis (09), Stakeholder Mapping (10). This skill adds the scored read of how the call was run, with the champion status and key moments the other skills take by name.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name. This skill is free and works without any kit. The kit reads `champion_status` from this skill. It also reads what the call said about ROI, which this skill records in its return-on-investment check in Step 7. This skill never fills a formula from the call, and every ROI input comes from the buyer, with its source. The field the kit reads from this skill:

- `champion_status`

---

## Changelog

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The records now carry the agenda, the titles, a restatement and the alternatives question, so Pre-Call Preparation scores 4 on its three markers and Active Listening and Alternatives score on what was said. Five sentences settle the open judgments: the partial-markers rule, the Winning Zone, the post-call date, the champion test about process, and the focus-area tie-break. Deal Health Impact states its before read, and the try-it notes that its records predate the account's later stage.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. The Unknown Rule is added: a category with no evidence is INSUFFICIENT and is left out of the total, the total reads `scored n of N`, and fewer than five scored categories gives no overall score. Example 1 now shows the eight report sections, Top 3 Strengths and Top 3 Improvement Areas, and one focus area.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1.

### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`, and the personas under `people/`) and offers read-only call-recorder and CRM connectors through the shared contract's Knowledge Base and Connectors section, before the call is read.
- Adds a Chains subsection placing the skill in the Work The Deal chain.
- Adds a Guild Pro Kits subsection naming the hand-off field the Business Case & ROI Kit reads, and how the kit's ROI read stays tied to the buyer's own figures.

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, Core Workflow with a Produces line per step, Epistemic Rules, Hard Rules with reasons, Quality Bar, and hand-off fields named in the Output Contract and the Integration section.
- Discovery adds an Alternatives category. Discovery is now 7 categories out of 35 (was 6 out of 30). The bands are restated for 35, with the arithmetic shown in Step 2.
- Step 4 uses the profile's "What to Listen For" column as the phrase list. Coaching points use the Situation, Proof point and Coaching moment template. A one-line negative-frame close is added.
- Demo adds five demo elements mapped onto the demo categories, the half rule, pacing defaults by element, return on investment formulas with blank inputs, a per-attendee block, and a five-line technical checklist.
- The shared champion tests, incumbent types and talk-time bands are referred to in The Shared Contract, not restated. Talk-time rubric lines are read against that band.
- Discovery adds a per-phase question review. Every call adds a six-line unraised objections checklist. Seven key-moment types each capture their fields. Every coaching point carries an evidence grade: Strong, Moderate or Weak.
- The eight anti-patterns each have a one-line definition. The Document Sections list becomes Report Sections, with its stray parentheses removed. The artifact section is removed: the file is Markdown, written only when asked.
- Examples: the Brackhaven Stage 2 Discovery call is graded, as the call Meeting Prep prepared. The Sable Fork call ends with a second discovery session booked, not a demo. The Brackhaven demo is kept with the new fields. Every fact carries one of the six evidence tags.
- Not in this version: trend analysis across calls, the eight-dimension transcript scorecard, cold-call and email coaching, and the system initialization blocks. The prep templates belong to Meeting Prep (06).

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.1 (2026-10-13)
- Two framework names replaced with plain descriptions: "Question the Problem" and "Priority Ladder". The methods are unchanged.
- The demo meeting open and close rewritten as a generic structure, replacing an internal framework.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around a single example case study.
- Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology.
- Client-specific data de-embedded: the skill now reads the shared client profile instead of carrying a copy-in block.
- Framework machinery moved to an explicit Methodology section. No functional changes to the workflow, scoring rubrics, or coaching recommendations.

### 1.0.0 (2026-03-04)
- Initial release. Merged from two coaching skills.
- Unified via a call type parameter: discovery (6 categories, out of 30) and demo (8 categories, out of 40).
- Generalized via the client profile with configurable defaults.
- Added demo-specific checks: Challenger, the demo meeting open and close, Question the Problem, the Five Implementation Habits, and anti-pattern detection.
