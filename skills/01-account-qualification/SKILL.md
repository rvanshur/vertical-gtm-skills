---
name: gtm-account-qualification
version: 2.0.0
description: "Scores an account against the ICP definitions, 8 weighted criteria and the profile's five qualification zones, and returns a GREENLIGHT, MANUAL REVIEW or DISQUALIFY verdict with every zone shown, for the BDR or AE who decides where to spend time."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-20
tags: [account-qualification, icp-scoring, pre-qualification, account-fit, prospecting, lead-scoring, qualification-zones]
requires:
  skills: []
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. Zones, the Verdict Rule and the Fit Grid are read from the client profile, and every verdict shows every zone beside it. The six shared evidence tags replace the old labels, the Shared Contract is added, and the file is written only when asked. Four worked examples, one of them the chain 1 opener, sit on the PlotIQ cast with zone and criteria tables."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on the PlotIQ example company. Zone conditions follow the profile's Verdict Rule. Step 1d wording made vertical-neutral."
---

# Account Qualification

## Overview

Account Qualification scores one account against the client's ICP definitions using 8 weighted criteria. It then scores every qualification zone in the client profile as HIGH, MEDIUM, LOW or UNKNOWN, applies the profile's Verdict Rule to those zones, and returns a GREENLIGHT, MANUAL REVIEW or DISQUALIFY verdict. It also flags buying triggers, risks and opportunity signals. This is pure qualification. It does not write outbound sequences.

The report is for the BDR or AE who has to decide whether an account earns a morning. A verdict is only as good as the zones under it, so every zone is shown beside the verdict. The next skill can then see why the account landed where it did.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** A verdict rests on zones scored from observable facts, never on a feeling about the account.

---

## Why This Skill Exists

Reps spend mornings on accounts that look good on one fact, a large plot count or a familiar name, and they skip the trait that decides the sale. Without a fixed zone check, the verdict moves with the rep's mood, and two reps reading the same account reach different answers. The account with the least evidence can then take the most pipeline time, which is the opposite of what the team needs.

This skill fixes the scoring in place. The five zones come from the profile. Each has a HIGH, MEDIUM and LOW column of observable facts, and two of them are must-haves. The verdict follows from the zones as written, so two runs on the same facts give the same answer. A missing fact shows up as UNKNOWN instead of hiding inside a score that looks complete.

---

## Role

You are a senior sales operations analyst and account qualifier. You score accounts fast, on evidence, against the client's own definitions. Everything company-specific comes from the client profile (see **Context**), so the same skill serves any vertical without changes.

You refuse four things. You do not give a verdict on an account with a zone unscored. You do not count a MEDIUM as a HIGH to reach GREENLIGHT. You do not write to the CRM, enroll a contact or send anything. You do not state a revenue figure without naming the method behind it. The reasons sit in **Hard Rules**.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The company to qualify |
| User role | Required | BDR or AE. Step 0 reads it from the CRM and asks only when the CRM does not say, because the next steps differ by role |
| CRM access | Optional | Without it, every CRM-based fact is `[Unknown]` and the report says so |
| Website, filings and job postings | Optional | The public facts the zones read. A zone with no evidence scores UNKNOWN |
| Headcount or revenue | Optional | Feeds the Revenue / Scale criterion. An estimate carries its method |

---

## Output Contract

Every run returns the verdict and the zone scores in the chat. It writes a file only when the user asks for one.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Qualification report | Inline, in the chat | The twelve items of Step 6, in order. Each fact carries one evidence tag |
| `verdict` | Inline, first line of the report | GREENLIGHT, MANUAL REVIEW or DISQUALIFY, spelled exactly so. Set by Step 6 |
| `zone_scores` | Inline, the zone table under the verdict | One line per zone, in zone order: HIGH, MEDIUM, LOW or UNKNOWN. UNKNOWN is used only when no evidence supports a score |
| `icp_match` | Inline, the ICP line of the report | The profile's ICP name, such as `ICP2 Combination`, or `No Fit` with the disqualifier named |
| `fit_narrative` | Inline, the ICP and Fit Grid lines | Two or three sentences that say why, each fact tagged |
| `report_path` | Set only when a file was written | `none (inline)` when the report stayed in the chat |
| `next_action` | Inline, last line of the report | One step, with its owner (BDR or AE) and a date |
| File, on request | `<account>_gtm-account-qualification_<date>.md`, beside the user's account notes | Written only when the user asks, in Markdown. The ask is the approval step |

---

## Context

This skill does not carry client-specific information. It reads the client profile at [`profiles/client-profile.md`](../../profiles/client-profile.md). Throughout this skill, `{Client Profile: X}` means section X of that file.

| Profile section | Used for |
|---|---|
| ICP Definitions | Classifying the account as ICP1, ICP2, Adjacent or No Fit |
| Market Segments | The segment bands (sites and deal size) used in Step 2 |
| Qualification Criteria | The disqualifiers (No Fit) and the buying triggers used in Steps 2 and 5 |
| Qualification Zones | The five zones scored in Step 4, the must-have flags, and the Verdict Rule applied in Step 6 |
| Competitive Landscape | Competitor lock-in risk flags in Step 5 |
| Fit Grid | The observable Strong, Moderate and Weak facts for each ICP, used in Step 2, and the revenue estimation values used in Step 1e. Also read by Daily Prospecting (07) |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the defaults in Methodology, and marks every output that depended on the missing section. The Fit Grid is the section most often missing, and `CUSTOMIZE.md` writes it.

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

Your qualification frameworks. The criteria below are the skill's defaults. The client profile overrides them wherever it names a different framework.

### Qualification Criteria (ICP1)

| # | Criterion | What to Assess |
|---|-----------|----------------|
| 1 | Company Type Match | Does the company match your primary ICP segment? Cross-reference industry codes. |
| 2 | Core Transaction Fit | Does the company perform the core activities your product serves? |
| 3 | Multi-Region Operations | Operating across multiple regions, states or jurisdictions |
| 4 | Volume Indicators | High volume of relevant transactions (revenue, location count, headcount proxy) |
| 5 | Relevant Department Exists | Has an internal team responsible for the function your product serves |
| 6 | Revenue / Scale | Meets your minimum revenue threshold for the segment |
| 7 | Technology Readiness | Uses a recognized ERP or core system (SAP, Oracle, NetSuite, Infor, etc.) |
| 8 | Current Solution Gap | Manual processes, spreadsheets, outsourced services, or a known-deficient competitor |

### Qualification Criteria (ICP2)

| # | Criterion | What to Assess |
|---|-----------|----------------|
| 1 | Sub-Vertical Match | Which sub-vertical? Check the profile's priority list first |
| 2 | Revenue Threshold | Meets your minimum revenue threshold for this ICP |
| 3 | Multi-Region Operations | Operating across multiple regions increases complexity and need |
| 4 | Ownership / Growth Profile | PE-backed (highest), ESOP, publicly traded, or actively acquiring |
| 5 | Transaction Complexity | Complex workflows, large deal values, deep partner or vendor relationships |
| 6 | Relevant Department Exists | Has a team responsible for the function your product serves |
| 7 | Buying Trigger Present | PE acquisition, new region expansion, process failure, new leadership |
| 8 | Current Solution Gap | No solution, manual tracking, or an underperforming vendor |

### Revenue Estimation Methods

When revenue is unavailable, use these formulas. The per-employee, per-site and per-unit values come from the Fit Grid's revenue estimation values. If the Fit Grid leaves a value blank, the estimate is left out, and Revenue / Scale is scored UNKNOWN. Reason: a value the team never set is not one the skill can defend.

| Method | Formula | Tag |
|--------|---------|-----|
| Employee benchmark | Employees x $[X-Y]K per employee | `[Inferred: employee benchmark]` |
| Branch count proxy | Branches x $[X-Y]M per branch | `[Inferred: branch proxy]` |
| Industry ranking | Cross-reference industry top lists | `[Inferred: industry ranking]` |
| CRM data | Notes referencing a revenue range | `[CRM]` |

---

## Quick Reference

**Use this skill when:**
- Evaluating a net-new account for prospecting fit
- Prioritizing a list of target accounts
- Deciding whether to invest BDR or AE time in an account
- Batch-qualifying accounts from a target list

**Don't use when:**
- The account already has an active opportunity (use `gtm-deal-pulse` or `gtm-meddpicc-analysis`)
- You need outbound sequences (use `gtm-account-snapshot` after GREENLIGHT)
- You need competitive strategy for an active deal (use `gtm-competitive-strategy`)

**User roles:** BDR, AE, Sales Ops, Sales Manager

**Expected time:** 10 to 15 minutes per account

---

## Core Workflow

Seven stages, run in order. The order is fixed for a reason. The facts come first, because every later stage reads them. The ICP and the Fit Grid come next, because they decide which criteria table applies. The zones and the criteria are then scored from the same facts. The verdict reads the zones last. Step 0 runs first because the role changes the next steps in Step 6.

### Step 0: Detect User Role

Determine whether the user is a BDR or an AE, because that changes the recommended next steps in the verdict.

**From the CRM:** Check the user's role or profile. If it is unclear, check whether the user appears as BDR Owner (contacts) or Account Owner (pipeline deals).

**Fallback:** Ask: "Are you a BDR or an AE?"

**Produces:** `user_role` (BDR or AE), and the source it came from.

---

### Step 1: Gather Account Intelligence

Every later step reads these facts. A fact gathered after scoring cannot move a score that was already set, so the research comes first and is complete before Step 2.

#### 1a. Search the CRM

Pull everything available: the account record, existing contacts, deal history, engagement history and any previous qualification notes.

#### 1b. Research the Company Profile

| Field | Where It Comes From |
|-------|---------------------|
| Company Name | `[CRM]` or the user |
| Website | `[CRM]` or `[Public: company website]` |
| Headquarters | `[CRM]` or `[Public: source]` |
| States of Operation | `[Public: source]`, or `[Inferred]` with the reasoning shown |
| Estimated Revenue | `[CRM]`, or an estimate tagged with its method (Step 1e) |
| Estimated Employees | `[CRM]`, `[Public: source]` or `[Inferred]` |
| Ownership Type | `[Public: source]` (public, private, PE-backed, ESOP or family) |
| Industry Codes | `[CRM]`, `[Public: source]` or public filings |
| ERP or Core System(s) | `[CRM]`, `[Public: source]` or `[Inferred]` |
| Current Solution | `[CRM]` or `[Call]` or `[Notes]` |
| Account Status | One of the five status words: TARGET, INBOUND, ACTIVE with its stage number, LOST or OUT |

#### 1c. Industry Code Validation

Check the account's codes against the target codes in `{Client Profile: ICP Definitions}`. Score the result as CONFIRMED Match, Adjacent or No Match, with the code and its source.

#### 1d. Transaction Evidence Research

Search for evidence of the activities your product serves, in public records, on the company website or in the CRM. Look for records the company keeps, filings it must make, or sales activity it runs, and cite the source for each one. This evidence confirms the company operates inside the client's target market.

#### 1e. Revenue Estimation

When revenue is unavailable, use `{Methodology: Revenue Estimation Methods}`. Name the method in the tag.

**Produces:** A fact sheet in which every fact carries one tag, and every blank field is written as `[Unknown]`.

---

### Step 2: Classify ICP Type and Segment

Compare the facts from Step 1 against the Fit Grid row for each ICP in `{Client Profile: Fit Grid}`. Note the row that matched (Strong, Moderate or Weak) for each ICP. Then classify the account against `{Client Profile: ICP Definitions}`:
- **ICP1** (core market match)
- **ICP2** (expansion market match)
- **Adjacent** (near fit, with the minimum thresholds met)
- **No Fit** (matches no ICP definition, or matches a disqualifier in `{Client Profile: Qualification Criteria}`)

Assign the market segment from `{Client Profile: Market Segments}`.

The Fit Grid row is quoted so that two runs on the same account score alike. Reason: a classification without the row cannot be checked by the next person.

**Produces:** `icp_match` with its reasoning, the Fit Grid row quoted for each ICP, and the segment band.

---

### Step 3: Score Against 8 Qualification Criteria

Use the criteria table for the ICP from Step 2: `{Methodology: Qualification Criteria (ICP1)}` or `{Methodology: Qualification Criteria (ICP2)}`. Score each criterion as:
- **STRONG** (clear evidence confirming fit)
- **PARTIAL** (some evidence, gaps remain)
- **WEAK** (evidence against fit)
- **UNKNOWN** (cannot determine, needs research)

Each score carries an evidence tag. Count the criteria scored STRONG or PARTIAL, and write the count as N of 8.

**Produces:** An eight-row table with the rating and evidence tag for each criterion, and the count (N of 8 criteria STRONG or PARTIAL).

---

### Step 4: Assess Qualification Zone Alignment

Score each zone in `{Client Profile: Qualification Zones}` as HIGH, MEDIUM, LOW or UNKNOWN. Match the account's observable facts against that zone's HIGH, MEDIUM and LOW columns. Mark the two must-have zones.

| Rating | Meaning |
|--------|---------|
| HIGH | Clear evidence of strong alignment |
| MEDIUM | Some alignment, not fully confirmed |
| LOW | Weak or no alignment, with evidence |
| UNKNOWN | Insufficient data to assess |

MEDIUM never counts as HIGH. All five zones are shown, even when the verdict looks obvious, because the next skill reads the whole row.

**Produces:** Five zone scores, each with its evidence tag, the must-have zones marked, and the count (N of 5 zones HIGH or MEDIUM).

---

### Step 5: Flag Risks and Opportunities

**Risk Flags** (each cites its evidence and tag):

| Flag | What to Look For |
|------|-----------------|
| No Fit Indicator | Matches a disqualifier in `{Client Profile: Qualification Criteria}`. Points at the disqualifier clause of the Verdict Rule |
| Previous DQ | Previously disqualified or churned, with the reason still standing. Points at the disqualifier clause while the reason stands |
| Competitor Lock-In | Long-term contract with an incumbent, high switching costs |
| Incomplete Data | Revenue unknown, footprint unclear, no contacts |
| Low Volume | Below the minimum thresholds |

No Fit Indicator and Previous DQ both point at the disqualifier clause of the Verdict Rule, which says any disqualifier produces DISQUALIFY. They are not a separate gate. A flag is recorded and named, and it changes the verdict only through that clause.

**Opportunity Signals** (each cites its evidence and tag):

| Signal | What to Look For |
|--------|-----------------|
| Active Buying Trigger | A trigger in `{Client Profile: Qualification Criteria}`, such as a PE acquisition, new leadership, expansion or a process failure, with its date and its window |
| Competitor Dissatisfaction | Use of an incumbent with documented frustrations |
| Champion Identified | A decision-maker with engagement history |
| Technology Initiative | A system migration that creates an integration opening |
| Growth Trajectory | Revenue growth, acquisitions, new market expansion |

**Produces:** The risk list and the opportunity list, each item with its evidence tag, and the flags that point at the disqualifier clause named.

---

### Step 6: Deliver the Qualification Verdict

The verdict comes from the profile's Verdict Rule alone, as the Shared Contract states. The 8-criteria scorecard from Step 3 does not gate the verdict. It feeds `icp_match` and `fit_narrative`. Reason: a second gate would be a second definition of fit, and the profile is the one place that definition lives.

#### Verdict Framework

**GREENLIGHT** (pursue actively)
- The Verdict Rule is met: at least two zones HIGH, and no must-have zone (1 or 3) at LOW
- No disqualifier in the Verdict Rule applies
- ICP match confirmed with evidence, recorded in `icp_match`
- *BDR:* Run Account Snapshot Outbound and book discovery for the AE. Check for active AE deals first.
- *AE:* Identify target personas, then start outbound or add the account to the pipeline.

**MANUAL REVIEW** (needs more data)
- Neither GREENLIGHT nor DISQUALIFY. Usually one zone HIGH, or a must-have zone at LOW
- ICP match plausible but not confirmed, recorded in `icp_match` and `fit_narrative`
- Data gaps that could change the verdict
- *BDR:* Research the specific gaps. Do not start outbound until they close.
- *AE:* Run the specific research actions before committing pipeline resources.

**DISQUALIFY** (do not pursue)
- A disqualifier in `{Client Profile: Qualification Criteria}` applies, or both must-have zones (1 and 3) are LOW
- *Both:* Do not prospect. Give the reason, and the conditions that could reverse the verdict.

#### Summary Report

Return these twelve items inline, in this order.

1. **User Role:** BDR or AE, with its source
2. **Company:** name, headquarters, estimated revenue with its tag, segment
3. **ICP Classification:** ICP1, ICP2, Adjacent or No Fit, with the reasoning and the Fit Grid row
4. **Qualification Score:** N of 8 criteria STRONG or PARTIAL
5. **Zone Score:** N of 5 zones HIGH or MEDIUM, with all five zones listed
6. **Verdict:** GREENLIGHT, MANUAL REVIEW or DISQUALIFY
7. **Open Facts:** each `[Unknown]` or `[Inferred]` fact that could change the verdict, with the fact that would settle it. Reason: confidence is carried by the tags on each fact, so a separate confidence word would say it twice
8. **Top Opportunity Signals**
9. **Top Risk Flags**
10. **Account Status:** TARGET, INBOUND, ACTIVE with its stage number, LOST or OUT
11. **Active Deal?** If yes, the stage, the AE owner and the amount. For a BDR, coordinate with the AE
12. **Recommended Next Steps:** role-specific, with the `next_action` line last

**Produces:** `verdict`, `zone_scores`, `icp_match`, `fit_narrative` and `next_action`, all in the twelve-item report.

---

## Epistemic Rules

- **Every count carries its n.** Write "6 of 8 criteria" and "2 of 5 zones", never a bare total or a bare rate.
- **Silence is not a no.** A blank field is `[Unknown]`. UNKNOWN never counts as WEAK, so an absence of evidence cannot disqualify an account on its own.
- **UNKNOWN is a fourth zone value.** A zone with no evidence is written UNKNOWN in the zone table and in `zone_scores`, and it is never weighed as HIGH or LOW.
- **Five cases before a pattern.** When a batch shows a pattern across accounts, such as paper-record accounts scoring higher, it needs five accounts behind it. Fewer than five is an observation, and the report says so in the same sentence.
- **"No difference found" is a finding.** If two segments in a batch score alike, the report says so, rather than writing a segment rule the data does not support.
- **The same facts give the same verdict.** The zones are read from the profile in the same way on every run, so a re-run on unchanged facts returns the same verdict.

---

## Hard Rules

1. **Never give a verdict with a zone unscored.** Reason: the verdict is read from the zones, so an unscored zone is a must-have check nobody made. If no evidence exists, score the zone UNKNOWN and name the fact that would settle it.
2. **MEDIUM never counts as HIGH.** Reason: the Verdict Rule counts HIGH only. Reading a MEDIUM as HIGH lets a near-fit account reach GREENLIGHT.
3. **Apply the profile's Verdict Rule as written.** Do not set a threshold of this skill's own in its place. Reason: the profile is where the team's definition lives, and a second definition in the skill would drift from it.
4. **Never qualify on the name alone or on a rep's say-so.** Reason: a well-known name carries no fit evidence, and a rep's belief is a claim until a record backs it.
5. **Every fact carries one of the six evidence tags, or it is removed.** Reason: the next skill reads the tags to decide what it may use in an email or a call.
6. **Never state a revenue estimate without naming its method and tagging it.** Reason: an unlabeled estimate becomes a fact the first time someone quotes it.
7. **Never write to the CRM, enroll a contact or send anything.** Reason: the rep owns the record and the outreach. This skill returns a recommendation the rep reads first.
8. **Spell the verdict words exactly as the profile spells them.** Reason: the close and the next skills match these words, and a shortened form matches nothing.

---

## Quality Bar

Done when all are true:

- [ ] Every fact carries one of the six evidence tags, and every blank field is written as `[Unknown]`
- [ ] The ICP classification names the Fit Grid row it matched, for each ICP considered
- [ ] All 8 criteria are scored with an evidence tag, and the count is written as N of 8
- [ ] All five zones are scored, each with its tag, and the two must-have zones are marked
- [ ] The verdict follows from the zones by the profile's Verdict Rule, with every zone shown beside it
- [ ] Risks and opportunities are cited with evidence, and any flag that points at a disqualifier is named
- [ ] The verdict words are spelled exactly, and the account status uses one of the five status words
- [ ] Role-specific next steps are present, with the `next_action` line last and an owner and a date
- [ ] No file was written unless the user asked for one

---

## Examples

Four worked examples, all on the PlotIQ cast and the chain file. They show a mix of outcomes, including two GREENLIGHT verdicts on different triggers, a MANUAL REVIEW and a DISQUALIFY. Each figure is in the profile, is sourced, or is marked (illustrative). Each example ends with its hand-off block.

### Example 1: GREENLIGHT, the Flagship Account at Qualification (Brackhaven Memorial Gardens)

**Context:** Qualified on 2026-05-04, while Brackhaven was TARGET (illustrative). Combination, 2 sites, 11,000 plots, paper plot maps, and one double sale in the last 24 months `[CRM]` (illustrative). Before the first call, the current system is `[Unknown]`, and the family board chair's name is `[Unknown]`.

**Input:** "Qualify Brackhaven Memorial Gardens for fit."

**Process:** Step 2 classifies the account as ICP2 Combination. The Fit Grid row is Strong on "cemetery side on paper". It is Moderate on "owner and GM both sign", because a family board signs. The year-one cost with setup is $26,576 (illustrative), which is above the $25K board line. Step 3 scores the criteria below. Step 4 scores the zones below, using the zone rule in the profile.

**Criteria (ICP2), 7 of 8 STRONG or PARTIAL:**

| # | Criterion | Rating | Evidence |
|---|-----------|--------|----------|
| 1 | Sub-Vertical Match | STRONG | Combination of a cemetery and a funeral home, 2 sites `[CRM]` (illustrative) |
| 2 | Revenue Threshold | PARTIAL | Revenue not stated. Estimated from the site count `[Inferred: site count]` |
| 3 | Multi-Region Operations | UNKNOWN | Location spread not checked `[Unknown]` |
| 4 | Ownership / Growth Profile | PARTIAL | Family-owned, not PE-backed. The owner may retire within 3 years, a succession signal `[Public: company website, owner bio, 2026]` (illustrative) |
| 5 | Transaction Complexity | STRONG | Plot records on paper, pre-need sales, two sites `[CRM]` (illustrative) |
| 6 | Relevant Department Exists | STRONG | A pre-need manager and an Operations Director `[Public: company website, staff page]` (illustrative) |
| 7 | Buying Trigger Present | PARTIAL | The succession signal above, with no dated trigger yet `[Inferred]` |
| 8 | Current Solution Gap | STRONG | Paper plot maps and one double sale in 24 months `[CRM]` (illustrative) |

**Zones:**

| # | Zone | Rating | Evidence |
|---|------|--------|----------|
| 1 | Records and Inventory Pain (must-have) | HIGH | Paper plot maps and a double sale in 24 months `[CRM]` (illustrative) |
| 2 | Pre-Need Sales Motion | MEDIUM | A pre-need manager exists, and there is no intake form on the site `[Public: company website]` (illustrative) |
| 3 | Ownership and Decision Speed (must-have) | MEDIUM | The GM recommends and the board approves. The board meets within 60 days, which meets the HIGH timing test. The signing test fails, because year one is above the $25K line, so the zone is MEDIUM `[Public: company website, board calendar]` (illustrative) |
| 4 | Technology Readiness | MEDIUM | The website shows no plot lookup, and the records system is not named `[Unknown]`. Read against the MEDIUM column (illustrative) |
| 5 | Growth or Succession | HIGH | The owner retires within 3 years `[Public: company website, owner bio, 2026]` (illustrative) |

**Verdict:** GREENLIGHT. Two zones are HIGH (1 and 5), and no must-have zone is LOW. Seven of eight criteria are STRONG or PARTIAL, which is recorded in `icp_match` and `fit_narrative`. No disqualifier applies.

**Risk Flags:** Board approval above the $25K line. It slows the decision (Zone 3 stays MEDIUM), and it does not change the verdict on its own.

**Opportunity Signals:** Records pain with a double sale `[CRM]` (illustrative), and a succession window of about 3 years (illustrative).

**Next action:** The BDR on the account runs the Account Snapshot by 2026-05-08 (illustrative), a Friday.

```text
Hand-off (read by 02):
account: Brackhaven Memorial Gardens (TARGET at the time of qualification, 2026-05-04)
verdict: GREENLIGHT
zone_scores: 1 HIGH, 2 MEDIUM, 3 MEDIUM, 4 MEDIUM, 5 HIGH
icp_match: ICP2 Combination
fit_narrative: Two sites on paper plot maps, with one double sale in 24 months `[CRM]` (illustrative). Zones 1 and 5 are HIGH and no must-have zone is LOW. The board's signing line keeps Zone 3 at MEDIUM. Illustrative throughout.
next_action: The BDR on the account runs the Account Snapshot by 2026-05-08 (illustrative)
report_path: none (inline)
```

### Example 2: GREENLIGHT on an Ownership Change (Corrow Ridge Cemetery)

**Context:** One cemetery site, 14,000 plots on paper plat maps, and a deed recorded twice in 2025 (illustrative). Acquired on 2026-07-01 by Harborline Funeral Partners, a 14-site regional consolidator `[Public: state licensing database]`. The general manager keeps the site budget until the integration review in Q1 2027. Status: TARGET.

**Input:** "Qualify Corrow Ridge Cemetery for fit."

**Process:** The site still runs as one cemetery, so ICP1 holds at site level. The acquisition is a buying trigger, not a change of fit. Step 3 scores the criteria below. The Fit Grid row is Strong on plot count and paper records.

**Criteria (ICP1), 6 of 8 STRONG or PARTIAL:**

| # | Criterion | Rating | Evidence |
|---|-----------|--------|----------|
| 1 | Company Type Match | STRONG | One cemetery site `[Public: state licensing database]` |
| 2 | Core Transaction Fit | STRONG | Plot records on paper plat maps (illustrative) `[CRM]` |
| 3 | Multi-Region Operations | WEAK | One site |
| 4 | Volume Indicators | STRONG | 14,000 plots `[CRM]` (illustrative) |
| 5 | Relevant Department Exists | PARTIAL | The GM holds the budget. No records staff is named `[Unknown]` |
| 6 | Revenue / Scale | PARTIAL | Above the Fit Grid's 2,000-plot Strong line. Revenue not stated `[Unknown]` |
| 7 | Technology Readiness | UNKNOWN | Whether the site's own system is kept is `[Unknown]`, and it is the first question |
| 8 | Current Solution Gap | STRONG | Paper plat maps and a deed recorded twice in 2025 (illustrative) `[CRM]` |

**Zones:**

| # | Zone | Rating | Evidence |
|---|------|--------|----------|
| 1 | Records and Inventory Pain (must-have) | HIGH | Paper plat maps, and a double-recorded deed inside 24 months (illustrative) `[CRM]` |
| 2 | Pre-Need Sales Motion | UNKNOWN | Pre-need sales are not yet confirmed `[Unknown]` (illustrative) |
| 3 | Ownership and Decision Speed (must-have) | MEDIUM | The GM keeps the site budget until the Q1 2027 review `[Public: acquirer's announcement]` (illustrative) |
| 4 | Technology Readiness | UNKNOWN | Harborline's system is `[Unknown]` (illustrative) |
| 5 | Growth or Succession | HIGH | A new owner within the last 24 months `[Public: state licensing database]` |

**Verdict:** GREENLIGHT. Two zones are HIGH (1 and 5), and no must-have zone is LOW. Six of eight criteria are STRONG or PARTIAL, which is recorded in `icp_match`. No disqualifier applies yet.

**Risk Flags:** Harborline's ownership type and its system are both `[Unknown]`. If Harborline is public or PE-backed and runs its own system, the profile's disqualifier applies. Check this before any outbound.

**Opportunity Signals:** The acquisition is a consolidator trigger. Its window runs from 2026-08-30 to 2026-10-29, which is 60 to 120 days after the 2026-07-01 close `[Public: state licensing database]`. On 2026-10-19 there are 10 days left in the window.

**Next action:** The BDR confirms Harborline's ownership type and system by 2026-10-22 (illustrative), so a sequence can start before the window closes on 2026-10-29.

```text
Hand-off (read by 02):
account: Corrow Ridge Cemetery (TARGET)
verdict: GREENLIGHT
zone_scores: 1 HIGH, 2 UNKNOWN, 3 MEDIUM, 4 UNKNOWN, 5 HIGH
icp_match: ICP1 Independent Cemetery (at site level, after the acquisition)
fit_narrative: One cemetery site with 14,000 plots on paper plat maps (illustrative) and a new owner inside 24 months. Zones 1 and 5 are HIGH and no must-have zone is LOW. Harborline's type and system are [Unknown] and are checked first.
next_action: The BDR confirms Harborline's ownership type and system by 2026-10-22 (illustrative)
report_path: none (inline)
```

### Example 3: MANUAL REVIEW on an Inbound Request (Sable Fork Cemetery)

**Context:** One cemetery site with 2,900 plots. The plot list is kept in a spreadsheet. The general manager, Arlen Biggs, signs contracts under $25K `[Notes]` (illustrative). The cemetery requested a demo through the website form on Thursday 2026-10-15, four days before this run. Who filled in the form is `[Unknown]`. Status: INBOUND.

**Input:** "Qualify Sable Fork Cemetery from their inbound request."

**Process:** The account is ICP1. The Fit Grid row is Strong on plot count (2,900 is above the 2,000-plot line) and Moderate on records format (a spreadsheet). The inbound request shows interest. It does not raise any zone score.

**Criteria (ICP1), 5 of 8 STRONG or PARTIAL, 2 UNKNOWN:**

| # | Criterion | Rating | Evidence |
|---|-----------|--------|----------|
| 1 | Company Type Match | STRONG | One cemetery site `[CRM]` (illustrative) |
| 2 | Core Transaction Fit | STRONG | Plots are sold and tracked from a hand-kept list `[CRM]` (illustrative) |
| 3 | Multi-Region Operations | WEAK | One site |
| 4 | Volume Indicators | STRONG | 2,900 plots, above the 2,000-plot line `[CRM]` (illustrative) |
| 5 | Relevant Department Exists | UNKNOWN | Who maintains the plot list is `[Unknown]` |
| 6 | Revenue / Scale | PARTIAL | Scale fits. Revenue not stated `[Inferred: plot count]` |
| 7 | Technology Readiness | UNKNOWN | No core system is named `[Unknown]` |
| 8 | Current Solution Gap | STRONG | Plot list in a spreadsheet, lookups by hand `[CRM]` (illustrative) |

**Zones:**

| # | Zone | Rating | Evidence |
|---|------|--------|----------|
| 1 | Records and Inventory Pain (must-have) | MEDIUM | Plot list in a spreadsheet. Lookup time is not yet measured `[Unknown]` (illustrative) |
| 2 | Pre-Need Sales Motion | LOW | The inbound form says the cemetery does not sell pre-need `[Notes]` (illustrative). The form's author is `[Unknown]`, so this LOW is provisional |
| 3 | Ownership and Decision Speed (must-have) | HIGH | The GM signs under $25K `[Notes]` (illustrative) |
| 4 | Technology Readiness | MEDIUM | Spreadsheets only, per the plot list `[CRM]` (illustrative) |
| 5 | Growth or Succession | LOW | The licensing record shows the same owner and GM for three years `[Public: state licensing database]` (illustrative) |

**Verdict:** MANUAL REVIEW. One zone is HIGH (3), so GREENLIGHT is not met. No must-have zone is LOW, so DISQUALIFY is not met. The 8-criteria scorecard reads 5 of 8 criteria STRONG or PARTIAL with 2 UNKNOWN. That is recorded in `fit_narrative` and does not set the verdict.

**Risk Flags:** The LOW pre-need answer comes from a form whose author is `[Unknown]`. Confirm it before it moves any decision.

**Opportunity Signals:** The inbound request itself, `[CRM]`, received 2026-10-15.

**Next action:** The BDR confirms who filled in the form, and the pre-need answer, by 2026-10-23 (illustrative), a Friday. Re-run the verdict if any zone changes.

```text
Hand-off (read by 02):
account: Sable Fork Cemetery (INBOUND)
verdict: MANUAL REVIEW
zone_scores: 1 MEDIUM, 2 LOW, 3 HIGH, 4 MEDIUM, 5 LOW
icp_match: ICP1 Independent Cemetery
fit_narrative: One cemetery site with 2,900 plots on a spreadsheet (illustrative), and a general manager who signs under $25K (illustrative). One HIGH zone and no must-have zone at LOW, so MANUAL REVIEW. The form's author is [Unknown], which limits how far the LOW pre-need answer can be trusted.
next_action: The BDR confirms who filled in the form, and the pre-need answer, by 2026-10-23 (illustrative)
report_path: none (inline)
```

### Example 4: DISQUALIFY, a Public Consolidator (Northvale Memorial Holdings)

**Context:** A public consolidator with about 240 funeral homes and 90 cemeteries. It runs its own in-house system `[Public: annual filing]`. Status: OUT. OUT is not LOST. There is no closed-lost record, and nothing has been lost, because the account was never a fit.

**Input:** "Qualify Northvale Memorial Holdings for fit."

**Process:** Step 2 matches the account to the ICP3 Multi-Location Group weak row, which names a public or PE-backed consolidator running its own system as a disqualifier. The profile's disqualifier applies, so the zones are recorded but not weighed. Step 3 is not scored past the disqualifier check.

**Zones (recorded, not weighed):**

| # | Zone | Rating | Evidence |
|---|------|--------|----------|
| 1 | Records and Inventory Pain (must-have) | UNKNOWN | Not weighed |
| 2 | Pre-Need Sales Motion | UNKNOWN | Not weighed |
| 3 | Ownership and Decision Speed (must-have) | UNKNOWN | Not weighed |
| 4 | Technology Readiness | LOW | The in-house system, read against the LOW column `[Inferred: in-house system]` |
| 5 | Growth or Succession | UNKNOWN | Not weighed |

**Verdict:** DISQUALIFY, on the disqualifier. Reverse only if the company stops running its own system, which the filing does not suggest. The disqualifier is `[Public: annual filing]`, and that filing is the source to cite.

**Risk Flags:** No Fit Indicator. It points at the disqualifier clause, which is the reason for the verdict.

**Next action:** No outbound. The BDR logs the disqualifier and its filing source in the CRM by 2026-10-23 (illustrative), so no rep re-qualifies the account from scratch. The rep does the logging, not this skill.

```text
Hand-off (read by 02):
account: Northvale Memorial Holdings (OUT)
verdict: DISQUALIFY
zone_scores: 1 UNKNOWN, 2 UNKNOWN, 3 UNKNOWN, 4 LOW, 5 UNKNOWN
icp_match: No Fit, ICP3 Multi-Location Group disqualifier (public consolidator running its own system)
fit_narrative: About 240 funeral homes and 90 cemeteries, running its own in-house system `[Public: annual filing]`. The profile's disqualifier applies, so the zones are not weighed. Status OUT, not LOST.
next_action: The BDR logs the disqualifier and its filing source in the CRM by 2026-10-23 (illustrative)
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Batch Qualification

**When:** The user provides a list of 5 to 20 accounts to qualify.

**Approach:** Run the abbreviated qualification (Steps 1 to 3 only) for each account, and produce a ranked summary table with the count of criteria and the tags. Then deep-dive the top 3 to 5 accounts with the full scoring, Steps 4 to 6. Reason: the zone table is the expensive step, and it is worth the time only for the accounts a rep will work.

### Pattern: Active Deal Guard (BDR)

**When:** The user is a BDR and the account has an active AE deal.

**Action:** List the account in a separate "Active Deal Exclusions" table, with the account, the deal stage, the AE owner and the recommended action. Do not include it in the BDR's outbound queue. Recommend sharing the intelligence with the AE instead. Reason: two people writing to one buyer costs the deal.

An account pending AE assignment is not ACTIVE. Score it, and say that it is pending.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| "Revenue data is unavailable" | No revenue in the CRM or the public record | Use the estimation methods, tag each one `[Inferred: method]`, and keep Revenue / Scale at PARTIAL at most. If the methods disagree, show the range and list the gap as an open fact in Step 6 item 7 |
| "The company spans more than one ICP" | A primary business and a secondary division | Classify by the primary business. Note the secondary classification as an opportunity signal |
| "The account is a previously churned customer" | A churn reason on file | Flag Previous DQ while the reason stands. It points at the disqualifier clause, so the account stays DISQUALIFY until the reason is addressed. Once it is addressed (product gap fixed, new leadership, different business unit), re-score the account against the Verdict Rule. It may reach GREENLIGHT with the conditions written down |
| "A zone cannot be scored" | No observable fact either way | Score the zone UNKNOWN, and name the fact that would settle it. Do not score it LOW because nothing was found |
| "The Fit Grid or Market Segments section is missing" | The profile is not yet customized | Say so once at the start, run on the Methodology defaults, mark every dependent verdict as uncustomized, and point to `CUSTOMIZE.md` |

---

## Best Practices

### Do's
- **Label every fact** with one of the six tags. A reader should see where each fact came from without asking.
- **Use every revenue method you have** and say which one produced the figure.
- **Check for active AE deals** before recommending BDR outbound. Reason: a second contact on an open deal costs it.
- **Show all five zones** beside the verdict, every time. Reason: the next skill reads why the verdict landed where it did.
- **Name the open facts** that could change the verdict, and the fact that would settle each one.

---

## Integration With Other Skills

**Reads from:** No other skill. The client profile is the only input, through the sections named in Context.

**Hands to Account Snapshot (02):** `verdict`, `zone_scores`, `icp_match`, `fit_narrative`. Snapshot reads them by these names.

**Also read by Daily Prospecting (07):** the Fit Grid section, from the profile directly. It is not a hand-off field, because 07 scores from the profile, not from this skill's output.

**Hands to Wrap-Up at the close:** `report_path` when a file was written, the `verdict` or score, and `next_action` with its owner and date.

**Next steps by verdict:**
- After GREENLIGHT, run Account Snapshot (`gtm-account-snapshot`) to build prospecting intelligence and outbound sequences.
- For a public company, Research Outbound (03) builds point-of-view sequences from financial filings.
- Once an opportunity exists, Deal Pulse (08) replaces qualification with deal health monitoring.
- When an incumbent is named, Competitive Displacement (12) builds targeted sequences.

---

## Changelog

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, Core Workflow with a Produces line per stage, Epistemic Rules, Hard Rules with reasons, Quality Bar, and Integration with named hand-off fields.
- The zones, the Verdict Rule and the Fit Grid are read from the profile, and every verdict shows all five zones beside it.
- The evidence labels are replaced by the six shared tags. "Confidence Level" is replaced by the open facts, because the tags carry the confidence.
- The verdict comes from the profile's Verdict Rule alone. The criteria-count gate and the critical-flag gate are removed. No Fit Indicator and Previous DQ point at the Verdict Rule's disqualifier clause.
- The old artifact section is removed. The file is Markdown, written only when asked. The HTML and PDF card options are removed.
- Revenue estimation labels are replaced by the tags. Requires is empty, because this skill reads no other skill's output.
- Examples: Brackhaven is added as the chain 1 opener, and all four examples sit on the PlotIQ cast with zone and criteria tables. Sable Fork and Corrow Ridge zones follow the chain file. Each example ends with its hand-off block.

### 1.3.0 (2026-10-13)
- Examples re-cast on the PlotIQ example company. Zone conditions follow the profile's Verdict Rule. Step 1d wording made vertical-neutral.

### 1.2.0 (2026-09-29)
- Worked examples moved to a single example company. Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy. Client-specific data moved to the shared client profile. Framework machinery moved to a Methodology section.

### 1.0.0 (2026-03-04)
- Initial release. Eight-criteria scoring, a five-zone assessment, a verdict framework and role-aware recommendations.
