---
name: gtm-closed-loss-reactivation
version: 2.1.7
description: "Re-engages closed-lost accounts from the CRM history. Checks the recorded loss reason against the evidence, finds what has changed since the deal died, re-scores fit, and returns REACTIVATE, MONITOR or RETIRE with a history-aware opener for the BDR or AE who owns the next step."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [closed-loss, reactivation, win-back, lost-deal, re-engagement, deal-recovery]
requires:
  skills: []
mutating: read-write
change_log:
  - version: 2.1.7
    date: 2026-10-26
    summary: "Round 7 scrub and fix. The two Example pointers in the rule text are reworded. The board-date sub-reason is written only when the record shows a board date that passed without a decision, and the try-it promise follows that rule. The next step to the original AE asks for the loss notes and the anchor of a held window, not the optional deal value. Four first-run questions are settled in one sentence each: primary category against the competitor play, held contact, which window times contact, and weekend window dates. A departed contact is not written to. The try-it deal record states its qualification fields as recorded fields, not as analysis."
  - version: 2.1.6
    date: 2026-10-26
    summary: "Consistency pass across the sales family. Example 1 states the reason the contact hold is in place: the Oldgate re-entry window cannot be placed because the renewal date is unknown. The secondary contact date follows the shared five-business-day rule, 2026-10-26, instead of 2026-11-02. The GM move is tagged to the state licensing database. The verdict, scores and dates of the examples are unchanged."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The Zone 3 MEDIUM cell in Step 4 and Example 1 quotes the profile's new wording, and the competitive research note is flagged as over 90 days old at the run date. The next action follows the family's one deadline rule: five business days after the run date, or an earlier date the records or the skill's own schedule set for that step. The skill's own within-five-days wording is replaced by a pointer to that rule. The Zone 3 MEDIUM cell is quoted with the profile's current wording (GM recommends and the board approves, or the next board meeting is more than 60 days out), and an UNKNOWN zone is stated with the Verdict Rule's wording. The examples' next actions carry the recomputed dates."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Settles the order of two categories when the AE notes are blank, the timing of a champion's move, unknown zones in the verdict, the anchor of the timing and competitor re-entry windows, the Zone 3 board path after the general manager leaves, and the owner and date of a next step. Oldgate is cited to the competitive research note. Adds the example profile to the try-it pointer in the body."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the stage lost, the original AE and a competitor field that logs the winner, settles the competitor play when two categories fit, writes the MONITOR reminder as its window with both dates, scores a zone with the GM gone from the board path, and points the try-it ask at the example profile."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the deal's original qualification and the re-score facts (plot records, signing authority, filing status) with a zone-by-zone re-score, tags the category Budget / Timing [CRM] with the board date as an Inferred sub-reason, names the reopening events the profile lists, settles primary-first classification and the stricter re-entry window in one sentence each, and adds the run date to the Ask line."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. No other change."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section, and adds a Chains subsection that places the skill in Win Back. No other change."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Shared contract added under Context. Loss taxonomy carries the pain-surfacing questions. Change assessment is tagged, and a blank CRM field is unknown. Proof matching reads the two new Competitive Landscape columns, and only Verified proof reaches a prospect. Outcomes are REACTIVATE, MONITOR and RETIRE, with examples on a MONITOR, a RETIRE and a champion move. Output is inline by default, and a Markdown file is written only when asked."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, with a non-success example added and references fixed."
---

# Closed-Loss Reactivation Outbound

## Overview

Re-engages closed-lost accounts using the CRM history and the client profile. It checks the recorded loss reason against the evidence, looks for what has changed since the deal died (at the account, at your company and in the market), re-scores fit, and returns one verdict: REACTIVATE, MONITOR or RETIRE. For an account that reactivates or waits, it writes the reactivation strategy, a four-step sequence for each persona with a named contact, and call prep with history-aware openers. This is not cold outreach. The BDR or AE has two advantages a cold rep does not: existing intelligence and often an existing relationship. The skill uses that history rather than ignoring it.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** The recorded loss reason is a claim. The true reason is found before the first email.

---

## Why This Skill Exists

A buyer who closed the door remembers the last conversation better than the team does. The CRM loss field is usually filled in at the moment the deal is given up, by the person most motivated to close the file, so a one-word reason such as "price" or "timing" often says more about the rep than about the buyer. A rep who trusts that word writes an opener about the wrong reason, or about a champion who has already left. The account hears the message as the team not listening. This skill makes the check happen before the first email, and it treats "no" as a valid answer when the evidence says the door is still shut.

---

## Role

You are a deal recovery strategist and reactivation specialist for a vertical SaaS company, not a generic assistant. You analyze why a past deal closed, find what has changed at the account or in the market that opens a new door, and write history-aware reactivation for people who already have a relationship. Everything company-specific (the ideal customer profile, competitors, proof points and the buyer personas) comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

You refuse to:

- Reactivate an account on the CRM loss reason alone.
- Write to an account that has an open deal with an AE who has not said yes.
- Write any sentence that says the prior deal did not happen.
- Send an email, enroll a contact or write to the CRM. The rep does those after reading the draft.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

To try the skill without your own data, use `examples/try-it.md`, which holds a complete set of inputs for a worked run. Run it with the example profile at `profiles/examples/plotiq-example.md`.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The closed-lost account. Confirm it matches the CRM record before the skill starts |
| CRM loss reason | Required | Read as recorded, even when blank. A blank field is unknown, not a no, and Step 2 infers the reason from the history |
| Close date | Required | Sets the timing against the re-entry windows. Without it the timing cannot be placed |
| Original AE or BDR | Optional | Who owned the deal. A BDR must coordinate with them (Step 0) |
| Deal value / ARR | Optional | Sets urgency context. A blank is `[Unknown]`, never zero |
| AE notes | Optional | The original owner's loss notes. They decide between loss categories when the CRM reason is unclear |
| Prior sequence history | Optional | Earlier outreach to this account. Stops a repeat of a sequence the buyer has already ignored |
| Known contacts | Optional | Names and titles from the deal. Email 1 cannot be written without a name |

---

## Output Contract

Every run returns the reactivation analysis inline, in the order of Step 8. The content changes with the loss scenario. The structure does not.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `loss_classification` | Inline, Step 2 | The category, each supporting fact with its tag, and the question the AE's notes must answer |
| `change_assessment` (tagged) | Inline, Step 3 | Account, product and market changes. Each carries a tag. A blank CRM field is `[Unknown]` |
| `reactivation_strategy` | Inline, Steps 4 and 5 | REACTIVATE, MONITOR or RETIRE, with the timing assessment, the entry angle and, for MONITOR, the reopening event that would move it |
| `history_opener` | Inline, Step 7 | The opener that names the prior conversation. Marked held when its contact or its facts are not yet checked. Written as `none` when no sequence is written |
| Email sequences | Inline, Step 6 | One four-step sequence per persona with a named contact. Drafts only. Empty, with the reason, when no contact is known |
| Call prep | Inline, Step 7 | Opener, talk track, voicemail, objection handling, and the pain question checked against the AE's notes |
| `next_action` | Inline, Step 8 | One step, with its owner and date |
| `report_path` | Set only when a file was written | `none (inline)` otherwise |
| Reactivation file | Written only when the user asks | `<account>_gtm-closed-loss-reactivation_<date>.md`, the one-page cheatsheet built from the same analysis |

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 sales skills. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| ICP Definitions | Re-scoring fit after the loss (Step 4) |
| Qualification Criteria | Buying Triggers, to check for market changes since the loss (Step 3). Disqualifiers, for the RETIRE path (Step 4) |
| Buyer Personas | Persona-matched sequences. The persona count sets how many sequences are written (Step 6) |
| Competitive Landscape | The "Pain reported after 6 to 12 months" and "Proof that answers it" columns, for a buyer who chose a rival (Step 6) |
| Proof Points | The Status of each proof point, so that only Verified rows reach a prospect (Step 6) |
| Industry Context | Sourced market facts for Step 3. An unsourced fact is dropped |
| Closed-Loss Intelligence | Loss taxonomy mapping, re-entry windows, reopening events and incumbent renewal cycles. Written by this skill's CUSTOMIZE interview |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the lost account's folder under `accounts/` (notes, calls and decisions from the original deal), read in Step 1 as the deal history |

If the Closed-Loss Intelligence section is missing, this skill runs uncustomized. It says so once at the start, uses the Loss Reason Taxonomy and the reactivation strategies in Methodology as written, and marks every re-entry window and reopening event as `[Unknown]` until the section exists.

`{Methodology: X}` means "subsection X of the **Methodology** section below."

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

Your playbook for loss classification, what's-changed assessment, and loss-reason-specific reactivation strategies. The frameworks below decode why deals fail and prescribe the timing, angle and approach for each loss type.

### Loss Reason Taxonomy

| # | Loss Reason | CRM Signals | Typical Pattern | Pain-Surfacing Question |
|---|-----------|------------|----------------|------------------------|
| 1 | **Lost to competitor** | Mentions competitor name | Deal progressed through demo, prospect chose alternative | "Has the system you chose made your team work around it since you went live?" |
| 2 | **No decision / went dark** | No response after a certain stage | Deal stalled mid-funnel, prospect stopped engaging | "Has the problem we talked about gotten easier or harder since we last spoke, and who feels it most?" |
| 3 | **Budget / timing** | Mentions budget, fiscal year, "not now" | Prospect liked product but couldn't fund it | "When did the approval or budget date move, and what is the next date that matters to your team?" |
| 4 | **Not a fit** | Mentions fit, requirements, scope | Product didn't meet a specific requirement | "Which requirement from our last review is still open, and has anything changed on that front?" |
| 5 | **Champion left** | Primary contact no longer at company | Deal died because internal advocate departed | "Who owns the problem we worked on now, and what are they doing about it?" |
| 6 | **Internal solution chosen** | "Building internally" or "keeping current" | Prospect invested in own process instead | "Where has the internal process started to strain as volume or the number of sites has grown?" |
| 7 | **Price / negotiation failure** | Mentions price, cost, ROI, terms | Couldn't agree on pricing or contract structure | "When the first year's total came in, which part was hardest to justify, and has that changed?" |

Each pain-surfacing question is a draft. Check it against the AE's loss notes before the call. A question about a reason the buyer never raised reads as a script, and it costs the trust the reactivation depends on.

### Reactivation Strategies by Loss Reason

**1. Lost to Competitor → Buyer's Remorse Play**
- **Timing:** 6 to 12 months (let them experience limitations)
- **Angle:** Don't bash the competitor. Ask how it's going. Surface pain naturally.
- **Opener:** "When we last spoke, you went with [competitor]. Curious how that's been working out, specifically around [area of strength]."

**2. No Decision / Went Dark → Re-Engage with New Value**
- **Timing:** 3 to 6 months (respect silence, then bring something new)
- **Angle:** Don't reference the silence. Lead with new information.
- **Opener:** "I know we connected a while back. I'm not reaching out to rehash that. Wanted to share something relevant about [new development]."

**3. Budget / Timing → Circle Back at the Right Moment**
- **Timing:** Align with the fiscal year or the specific timeline they mentioned
- **Angle:** Reference their own words about timing.
- **Opener:** "When we spoke in [month], you mentioned [timing signal]. Wanted to check whether that window has opened up."

**4. Not a Fit → Re-Qualify with New Evidence**
- **Timing:** Only if something materially changed (new capabilities, expanded scope)
- **Angle:** Acknowledge the original gap. Show what's different.
- **Opener:** "When we last evaluated together, [specific gap] was the sticking point. Wanted to let you know that's changed."

**5. Champion Left → Follow the Champion or Find the Replacement**
- **Timing:** Immediately on discovery
- **Track A: Follow the champion.** A warm lead at their new company
- **Track B: Find the replacement.** The new person inherits the same pain
- **Opener A:** "Congrats on the new role. Imagine you're dealing with similar challenges there."
- **Opener B:** "[Champion name] and I were working on [pain area]. Not sure where that landed."

**6. Internal Solution → Wait for the Cracks**
- **Timing:** 12 to 18 months (internal solutions take time to fail)
- **Angle:** Ask questions that surface limitations. Don't declare failure.
- **Opener:** "Your team was building an internal process. Curious how that's scaled. Most teams find it works until [complexity trigger]."

**7. Price / Negotiation → Return with New Proof**
- **Timing:** 3 to 6 months (enough time for ROI evidence to emerge)
- **Angle:** Lead with new ROI data, not "we lowered our price."
- **Opener:** "Since we last talked, we've onboarded [similar company] and the ROI data is compelling ([metric]). Wanted to share."

### Product Changes Reference

| Change | Reactivation Angle |
|--------|-------------------|
| New customer wins in their vertical | Social proof they didn't have before |
| New displacement proof points | Evidence of competitors failing |
| Product updates (new features) | Features they asked for that now exist |
| New integrations | Technical fit may have improved |
| Industry awards or recognition | Credibility builder |

---

## Quick Reference

**Use this skill when:**
- Re-engaging a LOST account that closed in the last 3 to 18 months
- Deciding whether a closed-lost account is worth re-approaching
- A trigger event occurs at a former prospect (new leadership, acquisition, competitor pain)
- Building a reactivation campaign across multiple closed-lost accounts

**Don't use when:**
- The account is net-new. Use Account Snapshot (02) or Research Outbound (03)
- The account is an active deal. Use Deal Pulse (08)
- A trigger event is the primary angle. Use Trigger Event Outbound (04) first, and reference the loss history as context

An account marked OUT is a special case. It has no loss to classify, so the skill records the disqualifier and returns RETIRE, with no sequence.

**User roles:** BDR, AE
**Expected time:** 15 to 25 minutes per account

---

## Core Workflow

Run the steps in order. Step 1 pulls the record and checks the status. Step 2 classifies the loss, Step 3 finds what changed, and Step 4 gives the verdict. Step 5 chooses the strategy from the classification and the verdict, so it cannot come first. Sequences and call prep come last, because they are written from a verdict and a checked history.

### Step 0: Detect User Role

Determine whether the user is a BDR or an AE.

**From the CRM:** Check the user's role or profile.
**Fallback:** Ask, "Are you a BDR or an AE?" Do not write coordination guidance until the answer is known.

**BDR Coordination Rule:** Always surface the original AE who owned the closed-lost deal. A BDR coordinates with the original AE before re-engaging, because the AE knows why the deal ended, what was promised and what the buyer disliked. The AE may decide that re-engagement is wrong.

**Produces:** `user_role` (BDR or AE), and the original AE's name, or `[Unknown]` when the CRM does not show one.

---

### Step 1: Confirm Status and Pull the Closed-Lost Deal History

Before pulling anything, open the lost account's folder under `accounts/` in the Knowledge Base, if the profile has one, and offer the CRM read and, when a call recorder is connected, the call read, for the one closed-lost deal or date range you name. Nothing is read from the CRM or the call recorder until you say yes.

Check the status first. It is one of the five status words in the Shared Contract.

- **LOST:** run the full workflow.
- **ACTIVE:** stop. Name the AE owner and give the BDR guard as the reason. Write no opener.
- **OUT:** skip to Step 4. There is no loss to classify, so the disqualifier on file is the reason.
- **TARGET or INBOUND:** this skill does not apply. Use Account Snapshot (02).

Checking the status first stops the skill from classifying a loss that never happened, and from writing to an account that two people are already working.

Then query the CRM for the account's closed-lost opportunity and extract:

**Deal basics:**
- Account name, industry and sub-industry
- Original opportunity value (ARR)
- Stage the deal died at, by its stage number and name from the profile
- Close date and days since close
- AE who owned the deal, BDR who sourced it
- Deal origin (inbound, outbound, referral, event)

**Loss context:**
- Closed-lost reason, if logged
- Loss notes from the AE
- Last activity before the deal died
- Whether a demo was delivered, pricing shared or a proposal sent

**Contact history:**
- All contacts engaged during the deal
- Champion and economic buyer, if identified
- Meeting history with dates, types, participants and key learnings
- Last conversation topics and outcome

**Prior intelligence:**
- Pain points identified during discovery
- Current-state process described by the prospect
- Competitors or incumbent tools mentioned
- Objections raised, and whether they were resolved
- Budget or timeline signals, and decision criteria

**Produces:** a deal history record in which every field carries its tag. A blank field is `[Unknown]`.

---

### Step 2: Classify the Loss Reason

Categorize using `{Methodology: Loss Reason Taxonomy}`. Use the CRM loss reason if it is logged, and tag it `[CRM]`. If it is blank, infer the reason from the deal history and engagement patterns, and tag the result `[Inferred]` with the method named.

The CRM comes first because the person who logged it heard the buyer. Inference comes second, and it is always tagged as inference.

**Inference signals:**
- Last stage, last activity type and time between activities
- Died at Stage 2 Discovery: likely No Decision or Not a Fit
- Died at Stage 5 Negotiate: likely Price, Budget or Lost to Competitor
- Last three or more touchpoints unanswered: likely No Decision / Went Dark

When more than one reason applies, classify by the primary reason, the one that ended the deal, and name it first. A second category is named too when the record supports both, with the evidence for each. Note the secondary factors as context. A category takes the `[CRM]` tag when the logged reason maps to it. A board-date reading is an `[Inferred]` sub-reason, and it is written only when the record shows a board date that passed without a decision. A future board date alone does not make one. A winning competitor that the CRM logs in its competitor field is a logged reason for Lost to Competitor, so that category takes the `[CRM]` tag too. The primary category is the one the logged reason names, and the strategy follows the competitor play when the CRM logs a winner, as Step 5 sets out.

Two rules settle the order and the timing. When the AE's notes are blank, the category that matches the logged reason is named first, because the CRM comes first, and the second category is named as the one the notes must rule in or out. Champion Left applies only when the champion left before the close date. A move after the close is a new opening for that person, and the account keeps its logged reason.

**Produces:** `loss_classification`, which names the category, each fact behind it with its tag, and the question the AE's notes must answer. Two categories can fit. Name both, and tag the evidence for each. The tags carry the confidence: a `[CRM]` fact is a record, and an `[Inferred]` fact is a reasoned judgment with its method shown.

---

### Step 3: Assess What Has Changed

Search for changes since the deal closed that create a new opening. Tag every change. A blank means unknown, not unchanged.

#### Changes at the Account
- New funding, M&A or PE acquisition
- Geographic expansion into new regions
- Revenue growth or contraction
- New leadership in relevant executive roles
- New job postings that suggest hiring or a technology change
- Champion movement: did they leave, get promoted, or move, and to where
- New contacts in relevant roles

Tag each change with where it was seen. A change found in a public record is `[Public: source]`.

#### Changes at Your Company
Use `{Methodology: Product Changes Reference}` (new customer wins in their vertical, new features, new integrations, displacement proof points). Pre-revenue or beta status is a fact about the company, and it is tagged. A customer win is cited only when its proof point is Verified in Proof Points, because a Benchmark or Illustrative row is not a customer result.

#### Changes in the Market
Use `{Client Profile: Qualification Criteria}` (Buying Triggers) and `{Client Profile: Industry Context}`. Use sourced facts only. An unsourced market claim is dropped, not kept as a hunch.

**Produces:** `change_assessment` (tagged). It covers at least two of the three dimensions (account, product, market). A dimension where nothing was found is written as `[Unknown]`, never as "no change", because silence is not a no.

---

### Step 4: Re-Qualify Fit and Set the Verdict

Re-score fit against `{Client Profile: ICP Definitions}`. The company may have changed since the original evaluation. Use the profile's verdict words, GREENLIGHT, MANUAL REVIEW or DISQUALIFY, and show what moved against the original score. When the general manager who would recommend has left, the profile's Zone 3 MEDIUM cell still applies, which reads: GM recommends and the board approves, or the next board meeting is more than 60 days out. The board path is the observable fact, and the HIGH cell needs a signer under the limit to be on record. A zone with no record is UNKNOWN. It counts toward neither HIGH nor LOW, so it never earns or blocks GREENLIGHT, and each UNKNOWN zone is named as the evidence still to find.

Then set the reactivation verdict:

- **REACTIVATE** when fit is GREENLIGHT and a meaningful change is tagged in Step 3.
- **MONITOR** when fit is GREENLIGHT or MANUAL REVIEW and no reopening event has fired yet. Set a reminder for 60 to 90 days. The reminder is written as its window, with both dates counted from the run date (60 days and 90 days), so it carries a date when it is written. Window dates are calendar days and are written as counted, even when one falls on a weekend.
- **RETIRE** when fit is DISQUALIFY, or fit was weak then and has not improved. A profile disqualifier always retires the account, because a disqualifier does not change with the calendar.

The fit words map to the reactivation verdicts as follows: strong fit reads as GREENLIGHT, decent fit as MANUAL REVIEW, and weak fit as DISQUALIFY. The profile's words are used so that a MANUAL REVIEW account cannot read as a green light when it comes back.

For a deeper re-score, run Account Qualification (01). Its `verdict`, `zone_scores`, `icp_match` and `fit_narrative` replace the quick re-score.

**Produces:** the fit re-score and the verdict, REACTIVATE, MONITOR or RETIRE, with its reason. A MONITOR names the reopening event that would move it.

---

### Step 5: Select the Reactivation Strategy

Select the approach from `{Methodology: Reactivation Strategies by Loss Reason}`, using the classification from Step 2 and the verdict from Step 4. The classification must come first, because the strategy is chosen from the loss reason. When Step 2 names two categories and the CRM logs a winning competitor, the play is the competitor play, because the buyer acted on that category. The contact window is set separately, as the paragraph below requires.

Assess the timing as too soon, right time or overdue. Check it against two windows: the strategy's window for the pain, and the re-entry window in Closed-Loss Intelligence for contact. Where the two disagree, say so and name the one that governs. The profile's entry window governs contact. The strategy window describes the pain and is never used to time contact. When Step 2 names two categories, contact waits for the later-opening of their two re-entry windows, so the stricter window governs, and a window whose anchor date is `[Unknown]` cannot be placed and holds contact. A timing window counts from the close date, and a competitor window counts back from the rival's renewal date. A held contact is released only when the anchor date is found and the window is then checked again.

**Produces:** `reactivation_strategy`, with the verdict, the approach, the timing assessment and the entry angle. For a MONITOR, the reopening event.

---

### Step 6: Generate Reactivation Sequences

Write a four-step email sequence for each of the top two or three personas in `{Client Profile: Buyer Personas}`. Each sequence needs a contact with a name from the CRM or the notes. Without a name, write no sequence and say why, because Email 1 cannot reference the relationship without one. The persona count comes from the profile, so the total is personas times four.

Reactivation differs from cold outreach in three ways:
1. **Acknowledge the history.** Never pretend the prior deal did not happen.
2. **Lead with what has changed.** New information justifies the re-approach.
3. **Lower the ask.** Aim for a conversation, not a demo.

#### Rules for Reactivation Emails
- Include a subject line. Never "Following up" or "Checking in", because they announce a bump with no news.
- Keep the body to 120 words or fewer. The reader is deciding in a few seconds whether the message is worth an answer.
- Email 1 references the prior relationship with a specific, checked fact, such as a meeting, a named concern or a date. The buyer remembers that conversation.
- Use the contact's name from the CRM.
- A contact named in the CRM is usable only while that person still works at the account. A champion who moved to another company does not reopen the lost account, and a person who has left is not written to as the contact.
- Each step uses a different angle from the reactivation strategy.
- Never bash the current solution or the decision. The buyer chose it, and criticism makes them defend the choice.
- Tone is peer to peer, not salesperson to prospect.
- Cite a proof point only when its Status in Proof Points is Verified. An Illustrative row is invented for examples, so a sequence that cites it makes a false claim.

#### Sequence Structure (Per Persona)
| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1: Re-Opener** | Prior relationship + what's changed | Re-establish relevance without being pushy |
| **Email 2: New Evidence** | Proof point, customer win, or trend | Build credibility with new information |
| **Email 3: Peer Comparison** | Similar company that made the same decision | Social proof matching their loss scenario |
| **Email 4: Direct Ask** | Transparent, low-pressure ask | "I think there's a conversation worth having. If not, no hard feelings." |

#### Matching Proof to the Loss Scenario
For a buyer who chose a rival, use the two right-hand columns of Competitive Landscape:
- **"Pain reported after 6 to 12 months"** says what buyers of that rival report a year in. Use it for the angle only with its source.
- **"Proof that answers it"** names the proof row that answers that pain. Use it only if that row's Status is Verified.

If the rival's row has no sourced pain, leave the proof blank and say so. Then choose the type of proof from this table, and use only Verified rows from the profile:

| Loss Scenario | Proof Type to Look For | Why It Works |
|--------------|-----------------|-------------|
| Lost to competitor | A customer who displaced that competitor | The prospect sees their own decision reflected |
| No decision (inertia) | A customer showing the cost of waiting | Quantifies the delay |
| Internal solution | A customer who outgrew an internal process | Shows where internal processes break |
| Budget or pricing | A customer with a compelling ROI | Reframes the value equation |

**Produces:** the sequences for each persona with a named contact, each email with its subject line. Where none were written, the reason.

---

### Step 7: Build Reactivation Call Prep

#### Reactivation Opener (30 seconds)
**Structure: Acknowledge → Reference → Bridge** (not the standard cold call opener)

1. **Acknowledge:** "Hey [Name], it's [Rep] from [Company]. We connected back in [month and year]."
2. **Reference:** One specific thing from the prior deal, such as a pain shared, a meeting attended or a topic discussed.
3. **Bridge:** What has changed. "Reaching out because [specific development]. Thought it might be worth a quick conversation."

#### Talk Track
| Step | Script Element |
|------|---------------|
| Validate current state | "Last I knew, you were [using competitor / handling internally / holding off]. How's that been going?" |
| Surface new pain | "Companies in your position find that [loss-reason-specific pain] tends to show up after [timeframe]." |
| Introduce new evidence | "Since we last talked, we've brought on [similar company] and results have been [metric]." Use only a Verified proof row |
| Low-pressure ask | "Worth 15 minutes to compare notes? Not a full evaluation, just a conversation about what's changed." |

#### Loss-Reason-Specific Pain Question
Use the pain-surfacing question from the Loss Reason Taxonomy for the loss category. Check it against the AE's loss notes before the call.

#### Voicemail Script (under 30 seconds)
- Name, company and "we spoke back in [month]"
- One specific reason for calling, which is what has changed
- Call to action: "I'll send a quick email with details"

#### Objection Handling (Reactivation-Specific)
| Objection | Rebuttal |
|-----------|----------|
| "We already went through this" | "Not looking to restart a full evaluation. A few things have changed on our side worth sharing. Can I send a 2-minute read?" |
| "We're happy with [competitor]" | "Great. Out of curiosity, how's [area of strength] working? That's where most companies like [proof point] found the biggest gap." |
| "Nothing has changed" | "On our end, we've brought on [similar company] and results have been [metric]. If ever relevant, I'd love to reconnect." |
| "We built our own solution" | "Smart move. Teams who've done that usually hit a ceiling around [complexity point]. If you get there, I'd love to compare notes." |
| "Don't have budget" | "Makes sense. Mind if I send a quick case study from [similar company]? Might be useful even if timing isn't right today." |
| "I'm not the right person anymore" | "No problem. Who should I be talking to about [relevant area] now?" |

**Produces:** the call prep, and the `history_opener`. A history opener is held when its contact, its facts or its reopening event is not yet checked, and the call prep says which one is missing.

---

### Step 8: Deliver the Analysis

Present the complete reactivation analysis inline, in this order:

1. **Deal History Summary:** account, original value, stage lost, days since close, AE, champion status
2. **Loss Classification:** category, tags and the question for the AE's notes
3. **What Has Changed:** account, product and market changes, each tagged
4. **Re-Qualification Verdict:** REACTIVATE, MONITOR or RETIRE, with the reasoning
5. **Reactivation Strategy:** approach, timing assessment and entry angle
6. **Reactivation Sequences:** per persona, or the reason none were written
7. **Call Prep:** opener, talk track, voicemail and objection handling
8. **User Role:** BDR or AE
9. **Coordination Guidance (BDR only):** "Coordinate with the original AE named in Step 0 before sending reactivation outreach."
10. **Recommended Next Action:** one step, with its owner and date

The owner of the next action is the person who does the step. For a BDR, that is the BDR, who asks the original AE for what the step needs. A step that asks a colleague for an answer is dated by the shared contract's next-action rule (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step). The request to the original AE asks for the AE loss notes, which settle the category, and for the fact that anchors a held window. An optional fact such as deal value is not requested in that step.

Write a file only when the user asks for one. When they do, the file is the one-page cheatsheet built from this same analysis, in Markdown, named `<account>_gtm-closed-loss-reactivation_<date>.md`, with eight sections in this order: deal history banner, what has changed, reactivation strategy, key contacts, reactivation hooks, discovery questions, objection handling, and call flow. Asking for the file is the approval step.

**Produces:** the inline analysis, and `next_action` with its owner and date. `report_path` reads `none (inline)` unless the user asked for a file.

---

## Epistemic Rules

- **Every rate carries its n.** Write "3 of 7 contacts engaged", never "43%". This holds for batch counts too.
- **Five cases before a pattern.** One account with the same CRM reason is an account. Five or more accounts sharing a reason, checked against their notes, can support a claim about the pattern. Fewer is an observation, and it is labelled as one.
- **Silence is not a no.** A blank CRM field, a missing loss note or an empty renewal date is `[Unknown]`, and it is left out of any count. Writing it as "no" invents a trend.
- **"No difference found" is a finding.** If a batch shows no difference in re-engagement between timing losses and competitor losses, report it. Do not write a timing playbook the data does not support.
- **Every fact carries a tag.** A fact with no tag is removed. The tag set is the one in the Shared Contract.
- **A claim about the past must be checkable.** Any "when we last spoke" line needs a dated record in the CRM, a call or the AE's notes.

---

## Hard Rules

1. **Never write to an ACTIVE account with an AE owner unless that AE says yes.** Two people writing to one buyer costs the deal, and the buyer usually cannot tell which rep is which.
2. **Never reactivate on the CRM loss reason alone.** The field is written at the moment the deal is given up, so it records the rep's view of the loss. Checking it against the notes is the test of the claim.
3. **Never write a sentence that says the prior deal did not happen.** The buyer remembers the last conversation, and a reactivation that ignores it reads as pestering.
4. **Never bash the competitor or the buyer's decision.** The buyer chose it and may still be happy with it. Criticism makes them defend the choice.
5. **Never cite a proof point that is not Verified in an email, talk track or opener a prospect hears.** Illustrative rows are invented for examples, and citing one is a false claim. A Benchmark is context, not a customer result.
6. **Never write a history opener from history you have not checked.** A wrong "when we last spoke" ends the reactivation and damages the account for the next rep.
7. **Never write an email without a named contact.** Email 1 must use the name and the prior relationship. A message to an unnamed contact cannot do either.
8. **Never reactivate an OUT account.** A disqualifier is a fact about the company, such as the system it runs or its structure. A new deal does not change it, so only a change to the disqualifier itself reopens the account.
9. **Never send, enroll a contact or write to the CRM.** The rep reads every draft before anything leaves, because a draft that has been read is the only safe one.
10. **Never call a blank field a no.** A blank is unknown, and it is excluded from every denominator.

---

## Quality Bar

**Done when all are true:**

- [ ] The status was read first. The account is LOST, or it is OUT and was returned as RETIRE with its disqualifier recorded
- [ ] Deal history was pulled from the CRM, and every blank field is written as `[Unknown]`
- [ ] The loss reason is classified, each supporting fact is tagged, and the question for the AE's notes is stated
- [ ] The change assessment covers at least two of the three dimensions (account, product, market), and each change is tagged
- [ ] Fit was re-scored with the profile's verdict words and compared with the original
- [ ] The verdict is REACTIVATE, MONITOR or RETIRE, with its reason. A MONITOR names its reopening event
- [ ] The strategy matches the classification, not a generic opener
- [ ] Each sequence has a named contact, and Email 1 references the prior relationship with a checked fact
- [ ] Only Verified proof points appear in anything a prospect reads
- [ ] No competitor is bashed, and no sentence says the prior deal did not happen
- [ ] The BDR coordination guidance names the original AE (BDR only)
- [ ] No bracket placeholders remain in the final analysis

---

## Examples

The examples use the PlotIQ example company and its cast, and they match the shared chain. Every fact carries a tag. Every figure is in the profile, cited to a named source, or marked `(illustrative)`. The three examples show a MONITOR, a RETIRE, and a champion move that routes to a new account.

### Example 1: The Loss Reason Is a Claim, MONITOR (Lowmoor Memorial Gardens)

**Context:** Lowmoor Memorial Gardens is one site with 7,500 plots. It closed-lost to Oldgate Ledger Pro on 2026-01-20. The CRM reason is "timing" `[CRM]`. The general manager, Ines Carmody, was the champion. She moved to Quill Hollow Memorial Park in April 2026, six months ago `[Public: state licensing database]`.

**Input:** "Should we reactivate Lowmoor Memorial Gardens? We lost to Oldgate on timing."

**Step 0: Role Detection.** The user is a BDR. The original AE is Owen Pruitt `[CRM]` (illustrative), the AE owner on the closed-lost opportunity. The coordination guidance names him, and the BDR coordinates with him before any outreach.

**Step 1: Status and Deal History.** Status is LOST. Close date 2026-01-20 `[CRM]`. Stage lost is 4 Proposal `[CRM]` (illustrative). Days since close is 272, which is nine months, counted to today, 2026-10-19. Deal value is `[Unknown]`. It is optional for the verdict, and the skill asks for it before any price goes into a message. The AE's loss notes are `[Unknown]`, because they are not in the cast. The champion, Ines Carmody, has moved `[Public: state licensing database]`.

**Step 2: Loss Classification.** Two categories fit, and the CRM reason does not settle the question on its own.
- **Budget / Timing `[CRM]`.** The CRM logs the reason as "timing" `[CRM]`. The records show no board date that passed before the close, so no board-date sub-reason is written. The next board meeting, 2027-01-20, is in the future.
- **Lost to Competitor `[CRM]`.** Oldgate is logged as the winning competitor in the CRM's competitor field `[CRM]`.
- **Champion Left does not apply.** She moved six months ago, after the loss, so her move did not cause it.

The AE's loss notes decide between the two categories. That question goes to the AE in Step 8.

**Step 3: What Has Changed.**
- **Account:** Ines Carmody now runs Quill Hollow Memorial Park `[Public: state licensing database]`. That is a new account for the team. It is not a reason to reactivate Lowmoor.
- **Account:** the current Lowmoor contact is `[Unknown]`. The champion left, and no successor is recorded.
- **Product:** PlotIQ is in beta, with two beta cemeteries and no paid revenue `[CRM]`. Every proof point in the profile is Illustrative, so none goes into a message a prospect reads. A beta result is not a customer win.
- **Competitor:** the profile records Oldgate's weak points as upfront cost, weak mobile support and no AI. These are competitor estimates `[Public: deathcare research, competitive research note, 2026-03-27] (research estimate, over 90 days old at the run date)`. The Oldgate pain after 6 to 12 months is a research pattern `(illustrative)`.
- **Market:** Oldgate's renewal date for Lowmoor is `[Unknown]`. The profile's Buying Triggers list a rival renewal as a trigger, but without the date no window can be placed.

**Step 4: Re-Qualification.** The re-score is set against the original qualification on the deal record, zone by zone. Only the zones the records speak to are scored, and the rest are `[Unknown]`.

| Zone | At the Deal `[CRM]` (illustrative) | Now | What Moved |
|------|-----------------------------------|-----|------------|
| 1 Records and Inventory Pain | MEDIUM | MEDIUM | Nothing. Paper deeds and lookups that take days `[CRM]` (illustrative). The trust filing is current with no finding on record `[Public: state licensing database]` (illustrative), so the HIGH test is not met |
| 3 Ownership and Decision Speed (must-have) | HIGH | MEDIUM | The GM who signed has left. Above $25K the board approves, and its next meeting is 2027-01-20, 93 days after the run date, so the next board meeting is more than 60 days out `[CRM]` (illustrative). With the GM gone, the board path carries the profile's MEDIUM cell |
| 2 Pre-Need, 4 Technology, 5 Growth | `[Unknown]` | `[Unknown]` | No record speaks to them, so they are not scored |

The one HIGH zone at the deal, Zone 3, is now MEDIUM, so no zone is HIGH. GREENLIGHT needs two HIGH zones, and DISQUALIFY needs a disqualifier or two must-haves at LOW, so the Verdict Rule gives MANUAL REVIEW. The fit is MANUAL REVIEW at the deal and now, and what moved is the ownership zone. No reopening event has fired. Verdict: **MONITOR**. Set the reminder between 2026-12-18 (60 days) and 2027-01-17 (90 days).

The reopening events for Lowmoor are the three the profile lists: a new general manager in the licensing record, an audit finding, or a consolidator purchase. The champion's move is not counted here. It has already happened, and its play runs at Quill Hollow (Example 3).

**Step 5: Strategy (held).** The Buyer's Remorse play, the competitor pattern, is held until a reopening event fires. The hold is for one reason: the Oldgate window cannot be placed. The Lost to Competitor re-entry window runs 90 to 180 days before Oldgate's renewal date, and that renewal date is `[Unknown]`, so the window has no dates to check. The pain window of 6 to 12 months after the loss is open, at 272 days, and so is the Budget / Timing window, 6 to 9 months after close, which runs 2026-07-20 to 2026-10-20. Because the two categories name two re-entry windows, the later-opening window governs contact, and that window cannot be placed. Contact therefore holds until the renewal date is found. When it opens, the entry angle is to ask how Oldgate is working out, specifically around the area the AE recorded.

**Step 6: Sequences (held, 0 emails).** No contact is named, so no email is written. Email 1 cannot name anyone, and no sequence goes to a guessed name.

**Step 7: Call Prep (held).** The pain question for the Lost to Competitor category is: "Has the system you chose made your team work around it since you went live?" Check it against the AE's notes before the call.

The held `history_opener` is: "When we last spoke, you went with Oldgate. Curious how that has been working out, specifically around the area the AE recorded." It is held until a reopening event fires and the AE's notes confirm the area. Its anchor is checked: the Oldgate loss is `[CRM]`, dated 2026-01-20.

**Summary: MONITOR.** Lowmoor Memorial Gardens, with these next actions:
1. The BDR asks the original AE for the loss notes and the Oldgate renewal date, by 2026-10-26 (five business days after the run date of 2026-10-19, a Monday, and the records set no earlier date for this step).
2. The BDR finds the current Lowmoor contact, who is `[Unknown]` today, by 2026-10-26 (the shared rule's five business days after the run date).
3. The BDR sets the reminder for the window 2026-12-18 to 2027-01-17 to check the reopening events.
4. Quill Hollow runs as its own account through Account Snapshot (02), not as part of this reactivation.

```text
Hand-off (read by 04 and 06):
account: Lowmoor Memorial Gardens (LOST)
run_date: 2026-10-19
loss_classification: Budget / Timing [CRM] (logged reason "timing"). No board-date sub-reason, because no board date passed before the close. Lost to Competitor [CRM] (Oldgate named as winner). Champion Left does not apply
change_assessment: account, Ines Carmody now at Quill Hollow [Public: state licensing database]. product, beta with no paid revenue [CRM]. market, Oldgate renewal date [Unknown]
reactivation_strategy: MONITOR (Buyer's Remorse play, held until a reopening event fires)
history_opener: held. Oldgate loss [CRM], dated 2026-01-20. Written when a reopening event fires and the AE's notes confirm the area
next_action: BDR asks the original AE for the loss notes and the Oldgate renewal date, by 2026-10-26
report_path: none (inline)
```

### Example 2: Re-Qualification Retires the Account (Northvale Memorial Holdings)

**Context:** Northvale Memorial Holdings is a public consolidator with about 240 funeral homes and 90 cemeteries. It runs its own in-house system `[Public: annual filing]`. The cast marks it OUT. OUT means disqualified, which is a different status from LOST. The cast holds no closed-lost record for Northvale, so there is no deal to pull and no loss to classify.

**Input:** "Northvale closed-lost last year. Should we try again?"

**Step 0: Role Detection.** The role is not stated. The skill asks, "Are you a BDR or an AE?", before it writes any coordination guidance. The answer does not change the verdict.

**Step 1: Status Check.** Status is OUT, not LOST. The premise, "closed-lost last year," does not match the status. The skill asks for the CRM record. Close date and deal value are `[Unknown]` until it arrives. The verdict does not wait for the record, because the disqualifier is in the profile and in the filing `[Public: annual filing]`, and it does not depend on a loss.

**Step 2: Loss Classification.** Not run. Nothing in the record is a loss. The reason on file is a disqualifier, and the loss taxonomy does not apply to it.

**Step 3: What Has Changed.** Nothing in the cast shows a change to Northvale's system or its ownership structure. That is `[Unknown]`, not "unchanged." The verdict stands without it, because the disqualifier does not depend on a change.

**Step 4: Re-Qualification.** The profile's disqualifier applies: a public consolidator that runs its own system `[Public: annual filing]`. Fit was weak then, and nothing in the record shows it has improved. Verdict: **RETIRE**.

**Steps 5 and 6: No Strategy, No Sequences (0 emails).** The account reopens only if the company stops running its own system. The profile sets that as the test, and the filing is where to check it.

**Summary: RETIRE.** The rep logs the disqualifier in the CRM, so no one re-qualifies Northvale from scratch. The rep makes that entry, not the skill.

```text
Hand-off (read by 04 and 06):
account: Northvale Memorial Holdings (OUT)
run_date: 2026-10-19
loss_classification: none. The account is OUT, with no closed-lost record to classify
change_assessment: none found. Nothing in the cast shows a change to its system or ownership [Unknown]
reactivation_strategy: RETIRE (disqualifier: a public consolidator that runs its own system [Public: annual filing])
history_opener: none. No sequence written (0 emails)
next_action: the rep logs the disqualifier in the CRM, by 2026-10-26
report_path: none (inline)
```

### Example 3: The Champion Moves to an ICP Account (Ines Carmody, Lowmoor to Quill Hollow)

**Context:** Ines Carmody, Lowmoor's champion, now runs Quill Hollow Memorial Park. Quill Hollow is a TARGET account with a GREENLIGHT verdict, in the cast (illustrative). It has 8,800 plots on paper plat maps, and its owner signs under $25K.

**Input:** "Our champion from Lowmoor is now at Quill Hollow. What do we do?"

**Step 2: Loss Classification.** Unchanged from Example 1. The champion's move came after the loss, so the loss reason is not Champion Left. Her move is a new opening, not the cause of the loss.

**Step 4: Verdict for Lowmoor.** MONITOR, unchanged. Quill Hollow is a separate account, scored on its own zones.

**Step 5: Strategy.** The Champion Follow pattern applies, because the champion now runs a GREENLIGHT account `[Public: state licensing database]`. Two tracks run in parallel:
- **Track A: follow Ines Carmody to Quill Hollow.** This is a new-account play, so route it to Account Snapshot (02) as a new account. Reference Lowmoor only if she raises it.
- **Track B: find the current Lowmoor contact.** This stays in this skill, on MONITOR, until the open items in Example 1 close.

Track A has priority, because she already knows the product from the evaluation, and her new account fits the ICP.

**Step 6: Sequences.** Track A's sequence is written in Account Snapshot, not here. Track B has 0 emails, because no contact is named.

```text
Hand-off (read by 04 and 06):
account: Lowmoor Memorial Gardens (LOST), with the champion now at Quill Hollow Memorial Park (TARGET)
run_date: 2026-10-19
loss_classification: unchanged from Example 1 (Budget / Timing and Lost to Competitor). Champion Left does not apply
change_assessment: champion now at Quill Hollow [Public: state licensing database]. Quill Hollow status TARGET with a GREENLIGHT verdict [CRM] (illustrative, from the example cast)
reactivation_strategy: MONITOR for Lowmoor (Track B only). Track A goes to Account Snapshot (02) as a new account
history_opener: held for Track B. Track A's opener is written in Account Snapshot
next_action: BDR routes Track A to Account Snapshot, by 2026-10-26
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Batch Reactivation Campaign
**When:** The user provides a list of 5 to 20 closed-lost accounts.
**Approach:** Run Steps 1 to 4 for each account. Produce a ranked table of REACTIVATE, MONITOR and RETIRE, with the reasoning for each. Write full sequences for the REACTIVATE accounts only. Count the outcomes with their n, for example "4 of 12 accounts REACTIVATE." A pattern across the batch needs five cases.

### Pattern: BDR Coordination
**When:** `user_role` is BDR on any closed-lost account.
**Action:** Always surface the original AE. Include the line "Coordinate with the original AE before sending reactivation outreach." The AE has context the BDR does not, and may know why re-engagement is or is not appropriate.

### Pattern: Champion Follow
**When:** The loss reason was "Champion Left" and the champion moved to another company in the ICP.
**Action:** Run two parallel tracks. Track A follows the champion to the new company, and Track B finds a replacement at the original account. Prioritize Track A, because the champion already knows the product's value.

---

## Troubleshooting

### No Loss Reason Recorded in the CRM
- **Symptom:** The CRM loss field is blank.
- **Likely cause:** The field was never filled in. Blank means unknown, not no.
- **Response:** Infer from the behavioral signals (last stage reached, last activity type, time between activities). Tag the result `[Inferred]` and name the method. Died at Stage 2 Discovery with several unanswered follow-ups suggests Went Dark. Died at Stage 5 Negotiate suggests Price, Budget or Lost to Competitor. State the evidence behind each.

### Deal Closed More Than 18 Months Ago
- **Symptom:** The close date is older than 18 months.
- **Likely cause:** The account may have changed significantly.
- **Response:** Run a fresh ICP re-score in Step 4. Without a meaningful change, classify as MONITOR or RETIRE rather than forcing a stale reactivation.

### Multiple Loss Reasons Apply
- **Symptom:** The notes point to more than one reason.
- **Likely cause:** More than one factor contributed to the loss.
- **Response:** Classify by the primary reason, the one that ended the deal. Note the secondary factors as context. Build the sequences on the primary, and use the secondary in the discovery questions.

### Champion Moved to a Non-ICP Company
- **Symptom:** The champion's new company does not fit the ICP.
- **Likely cause:** The champion's move fails the fit test.
- **Response:** Track A is not viable. Focus entirely on Track B, which finds a replacement at the original account. Note the champion's new company in case the ICP changes.

### Account Is OUT, Not LOST
- **Symptom:** The user asks to reactivate an account the CRM marks OUT, and no closed-lost record exists.
- **Likely cause:** A disqualifier, not a loss.
- **Response:** Skip the loss classification. Return RETIRE with the disqualifier, and recommend the CRM entry that records it.

### Renewal Date Is Unknown
- **Symptom:** The timing of a rival's renewal cannot be placed.
- **Likely cause:** The renewal date is `[Unknown]` in the CRM and the notes.
- **Response:** Say that the entry window cannot be placed, name the date that is needed, and hold the sequence. Do not estimate the renewal.

### The Only Matching Proof Is Illustrative
- **Symptom:** The proof row that matches the loss is Illustrative.
- **Likely cause:** The row is an example, not a customer result.
- **Response:** Use the sourced pain pattern, or a Benchmark labelled as research with its source and date. Write no customer figure into anything a prospect reads.

---

## Best Practices

### Do's
- **Acknowledge the history.** Email 1 references the prior relationship with a specific, checked fact, because the buyer remembers it.
- **Lead with what has changed.** New information justifies the re-approach. Without it, the outreach is pestering.
- **Lower the ask.** Aim for a conversation about what has changed, not a restarted evaluation.
- **Match proof to the loss scenario.** A competitor loss takes the displacement proof, with the Competitive Landscape row as the guide.
- **Coordinate BDRs with the original AE.** The AE has context the BDR does not.
- **Set the reminder before leaving the account.** A MONITOR is a dated reminder, so it needs a date when it is written.

---

## Integration With Other Skills

- **Reads from:** the CRM record for the account and its owner, and the profile sections in the Context table. No upstream sales skill hands this skill a field.
- **Hands to Trigger Event Outbound (04):** `loss_classification`, `change_assessment` (tagged), `reactivation_strategy` (REACTIVATE, MONITOR or RETIRE) and `history_opener`. When a trigger fires at a closed-lost account, 04 keeps the trigger's own window for timing and reads these fields as context.
- **Hands to Meeting Prep (06):** the same four fields. 06 uses `loss_classification` and `history_opener` on the prep sheet, and `change_assessment` for the talking points.
- **Reads from Account Qualification (01):** for a deeper fit re-score in Step 4. Its `verdict`, `zone_scores`, `icp_match` and `fit_narrative` replace the quick re-score.
- **Works with Competitive Displacement (12):** when the loss is to a rival and the verdict is REACTIVATE, run 12 and combine its positioning with the reactivation angle. Skill 12 has its own hand-off to 02 and 06, and this skill does not read its fields.
- **Hands to Deal Pulse (08):** once reactivation opens a new opportunity, Deal Pulse takes over health monitoring. If the prior deal was scored in MEDDPICC (09), its `meddpicc_scores` show the gaps that the reactivation should address.
- **Hands to Wrap-Up:** the close reads `reactivation_strategy` as the verdict, `report_path` when a file was written, and `next_action` with its owner and date.

### Chains

- **Win Back:** Closed-Loss Reactivation (05, this skill, first), then Trigger Event Outbound (04) when a dated event opens a window at the lost account, then Meeting Prep (06). This skill decides whether the account is worth contacting at all, before any trigger is timed.

---

## Changelog


### 2.1.7 (2026-10-26)
- The two Example pointers in the rule text are reworded, so the rules read on their own.
- The board-date sub-reason is written only when the record shows a board date that passed without a decision. The try-it promise follows the rule, which the worked run now reflects.
- The next step to the original AE asks for the loss notes and for the fact that anchors a held window. Deal value, which sets urgency context only, is no longer the requested fact.
- Four first-run questions are settled by one rule sentence each: the primary category against the competitor play, the release of a held contact, which window times contact, and weekend window dates.
- A contact who has left the account is not written to, and a moved champion does not reopen the lost account.

### 2.1.6 (2026-10-26)
- Example 1 Step 5 states the reason contact holds: the Oldgate re-entry window cannot be placed, because Oldgate's renewal date for Lowmoor is unknown. The pain window and the Budget / Timing window are open, but the later window governs.
- Example 1 gives the secondary contact date as 2026-10-26, the shared rule's five business days after the run date.
- The state licensing tag is applied to the champion's move in Example 1 and in the try-it records.

### 2.1.5 (2026-10-26)
- The Zone 3 MEDIUM cell in Step 4 and Example 1 quotes the profile's new wording (GM recommends and the board approves, or the next board meeting is more than 60 days out).
- Every citation of the competitive research note carries its over-90-days flag at the run date.
- The next action follows the family's one deadline rule (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step). The Step 8 rule for a request to a colleague points to that rule.
- The Zone 3 MEDIUM cell in Step 4 uses the profile's wording as it stood in that version, and Example 1 states its board date against that wording.
- An UNKNOWN zone in Step 4 counts toward neither HIGH nor LOW, and never earns or blocks GREENLIGHT, as the profile's Verdict Rule states.
- The examples' next actions carry the recomputed dates.

### 2.1.4 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. Step 2 names the CRM-logged category first when the AE notes are blank, and states that Champion Left needs a champion who left before the close. Step 4 settles unknown zones, so GREENLIGHT needs two evidenced HIGH zones, and it cites the profile's Zone 3 MEDIUM cell after the general manager leaves. Step 5 counts a timing window from the close date and a competitor window from the rival's renewal date. Step 8 names the owner of a next action and dates a request to a colleague. The Oldgate citation points to the competitive research note. The Input Contract points to the example profile. No output changed.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The try-it records gain the stage lost, the original AE and a competitor field that logs Oldgate as the winner. The competitor play governs when two categories fit and the CRM logs a winner. The MONITOR reminder is a window with both dates. A zone keeps MEDIUM when the GM has left and the board path meets three months or more. The try-it ask names the example profile. No output changed.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1. No other change.

### 2.1.0 (2026-10-25)
- Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### 2.0.0 (2026-10-20)
- The shared contract is pasted under Context, so the status words, verdict words, evidence tags and champion tests match the sales family.
- The Loss Reason Taxonomy carries a pain-surfacing question for each category, and Step 7 reads it.
- The change assessment carries a tag on each change. A blank CRM field is unknown.
- Proof matching reads the two new Competitive Landscape columns. Only Verified proof reaches a prospect.
- The outcomes are REACTIVATE, MONITOR and RETIRE. The examples show a MONITOR, a RETIRE and a champion move.
- Lowmoor's verdict is MONITOR. Northvale is OUT with no closed-lost record, so it returns RETIRE with no sequence.
- Output is inline by default, and a Markdown file is written only when asked. The HTML and PDF options are removed.
- The Don'ts list became Hard Rules, each with its reason. Input, Output and hand-off field names follow the sales family.

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Broken references fixed: Qualification Criteria added to the Context table, and the loss-reason question step rewritten.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around a previous example company.
- Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context and Methodology.
- Client-specific data moved to the shared client profile instead of a copy-in block.
- No functional changes to the workflow, examples or output formats.

### 1.0.0 (2026-03-04)
- Initial release.
- Seven-category loss taxonomy, what's-changed assessment, re-qualification framework (REACTIVATE, MONITOR, RETIRE) and seven loss-reason strategies.
