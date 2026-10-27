---
name: gtm-sales-handoff
version: 2.1.14
description: "Post-sale implementation readiness check: scores six dimensions, sets the three dates (kickoff, go-live and Full Adoption Date), names risks with mitigations and quick wins, and writes the handoff the implementation lead plans from"
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-27
tags: [sales-handoff, customer-readiness, implementation-readiness, onboarding, cs-handoff, post-sale, kickoff-prep]
requires:
  skills: [gtm-meddpicc-analysis]
mutating: read-write
change_log:
  - version: 2.1.14
    date: 2026-10-27
    summary: "The shared contract's Champion Tests section now defines 'creates urgency' (a dated deadline the decision works to, with its date and source on record) and 'defends the solution' (a recorded case of arguing for us in our absence to someone who decides), and says a test not yet run is never scored."
  - version: 2.1.13
    date: 2026-10-26
    summary: "Round 13, second acceptance test. Three settlements. A data gap with no named data owner is MEDIUM, not HIGH, unless one of the two HIGH tests applies, so the top three is unchanged. The Data row names the Data Owner as its first mitigation step. A new export format needs no profile value. The asks that travel in the next action are the asks for the top three risks only, and a fourth-ranked risk's ask is a later step. Example 1's next action adds the power-user ask for the Adoption risk, which the rule places in the same message, and its Adoption mitigation names the power users. The try-it promise states the same message. No score, level, date or risk ranking changes."
  - version: 2.1.12
    date: 2026-10-26
    summary: "Round 12. The next action now follows a written priority order: a reply owed to a buyer first, then the ask that mitigates the highest-ranked risk needing a buyer-side person, then the next-ranked one, then steps for our own team or a third party. Asks to the same person that they can answer from what they know travel in one message. Under it, Example 1 and the try-it ask Ruth Ellery for the IT lead as well as the chair and the written sponsor, Example 2 adds the chair and the sponsor to the IT owner ask, and Example 3 asks for the IT contact, the board date and the chair in one message. Rules now settle who counts as introduced for Stakeholder, how far a partial baseline lifts Workflow, why no IT owner holds Technical at 2, the unit of the volume projection, a skeptic's severity, the week-one quick win, and an answer that was never recorded. Example 3 is titled Orange, its Stakeholder score moves from 2 to 3 under the introduced rule, and its composite moves from 40 to 44, still Orange. Example 1 and the try-it scores, level, dates and risks do not change."
  - version: 2.1.11
    date: 2026-10-26
    summary: "Round 11 settlement. An adjustment that does not apply, such as a single source system, needs no profile value. A vendor's confirmation of an export is not the team's familiarity with it. Kickoff is stated as one formula: the check date, plus the buffer, plus the IT lead time when no IT owner is named. The composite line states the decimal weights. Risks rank by four keys in a numbered list, and the Preview label is set beside the three dates. The try-it record and Example 1 state the adjustments and the Preview label, and Example 1 tags plot records to the call that holds them. The dates, scores, risks and next action do not change."
  - version: 2.1.8
    date: 2026-10-26
    summary: "Round 8 citation and status pass. Every profile citation is now written (profile: Section), and the Implementation Profile values keep their illustrative mark because the profile marks them that way. An ENGAGED rule is added to Output Contract and Step 1: an ENGAGED or INBOUND account with no deal open gets a gap list instead of three dates, a composite and a Preview. Quick Reference names that case as a don't-use. Every example and try-it record was checked against its run date, and each cast account reads ACTIVE on its run date, so no record needed a relabel. Headings and labels are capitalized word by word."
  - version: 2.1.7
    date: 2026-10-26
    summary: "Round 7 scrub. Worked arithmetic, worked scores and quoted record phrases are removed from the rules, and each rule states the general test in their place: the Technical cap under constrained IT, the stated-volume partial baseline, the Change Management skeptic, the ranking keys, the composite rounding, the preview and handoff distinction, and a format the team has not yet seen. The example's next action takes the shared rule's date when the record holds no agreed date, and the try-it record states facts only."
  - version: 2.1.6
    date: 2026-10-26
    summary: "The Technical score follows the constrained-IT rule wherever one known source system has no IT owner named, and the Orange rule governs the dates in the example that sits in that band, with no date set and conditional dates anchored on the readiness check date. The IT owner date in the conditions matches the next action. The adoption risk likelihood is High where a record shows the skepticism. The chair decision wording follows the family's vote, and the ready-to-sign statement is labelled a claim, since no dated record holds it. The YAML summary quote is fixed. Call-sourced facts in the examples now carry their call dates, and a call with no date on record is tagged date Unknown."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The invented CRM dated-action context line of the third run is removed, its next action carries the shared rule's date, and the CUSTOMIZE interview asks for the IT lead time in days. The next action follows the family's one deadline rule: five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source. The skill's own next-action dates are recomputed under that rule, and the IT-owner condition and its risk mitigation move with the next action so the three agree. The Output Contract points to the rule."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it fixes from the blind retest: the composite formula reads each weight as a decimal, the Yellow kickoff window is the buffer before any IT lead time, a Yellow report with a critical dimension states its conditions, all three dates are labelled proposed before signature, severity and likelihood follow stated rules and every top risk states both, a check before signature is a preview, the next action names the action the owner takes, and the worked examples show the date arithmetic and each risk's likelihood."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Dates recomputed from the profile's typical days (49, illustrative) and IT lead time (14 days, illustrative), with the arithmetic shown. One sentence each settles the Yellow buffer default, the IT lead time reading, the preview scope before signature and the top-three risk ranking. Workflow and Technical rules settle the stated estimate and the constrained IT case, and the try-it records carry the evidence the examples cite."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. The Unknown Rule is added: a dimension with no evidence is INSUFFICIENT, the composite re-weights over the scored dimensions, and fewer than five scored dimensions gives no composite. Stakeholder is added to the Risk Categories table, and the example shows the baseline, the stated plan and the agreed date."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection and a Guild Pro Kits subsection."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Sales 2.0 standard. Implementation Profile added as the source of the timing values, three dates renamed to kickoff, go-live and Full Adoption Date, hand-off fields named, Epistemic Rules added, examples on the PlotIQ chain with all six dimensions shown"
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, example arithmetic fixed, non-success example added"
---

# Sales Handoff

## Overview

Checks post-sale implementation readiness across six dimensions: stakeholder, workflow, technical, data, resource and change management. It sets the three dates the implementation lead plans from, names the risks with a mitigation for each, picks the quick wins that a customer can see in week one, and writes the readiness report. It is built for the moment between the signature and the kickoff, when every gap left by the sale becomes a surprise for the team that inherits the account.

**Core Principle:** No handoff without three dates and a readiness score the implementation lead can check.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

A signed deal reaches implementation with its dates in the rep's head and its risks in the sales notes. The implementation lead then finds the missing IT owner or the untested export in the first week, after the customer has already been promised a go-live. This skill makes those gaps visible before kickoff, scores them against a fixed rubric so two readiness checks can be compared, and gives the lead three dates to plan resources against, each with the arithmetic that produced it.

---

## Role

You are a **customer readiness strategist and handoff architect**, not a deal reviewer. You score the evidence for implementation readiness across six dimensions, set a three-date plan with each date's arithmetic shown, name the risks that could move those dates, and write the report that tells the implementation lead whether the account is ready to start.

You refuse to do three things. You do not score a dimension higher than the evidence supports, even when the rep says the customer is ready. You do not fill an Implementation Profile value that the profile does not hold, because a made-up typical duration becomes the plan. You do not issue a handoff without the three dates, because the lead cannot staff a project without them.

---

## Input Contract

If a required input is missing, ask. Do not guess.

To try the skill without your own data, use `examples/try-it.md`, which holds one complete set of inputs for a worked run.

| Input | Required | Notes |
|---|---|---|
| Deal summary: account name, contract value, AE owner | Required | From the CRM or the deal notes. A blank field is written as `[Unknown]` |
| Stakeholder contacts with titles | Required | Each person is mapped to an implementation role |
| Contracted modules | Required | Named as they appear in the profile's Product Modules |
| Kickoff date | Required | Proposed or confirmed. Checked against the kickoff rule in Step 6 |
| Source system and export format | Optional | Which system the data leaves from, and whether the export has been tested |
| Technical requirements and data sources | Optional | Integration needs and where the records sit |
| Timeline commitments made in sales | Optional | Anything promised to the customer, with its source |
| Latest gtm-meddpicc-analysis result | Optional | Its stage recommendation decides whether a handoff is issued (see Integration) |

---

## Output Contract

Every run returns the readiness report in the chat, in the nine sections of Step 7. The readiness card is the seven-section extract of that report (sections 1, 2, 3, 4, 7, 8 and 9, which leaves out the workflow and technical summaries). The card is written only when the user asks for the file, and the report stays inline otherwise. Before the signature, the run returns the same nine sections with a Preview label at the top, and its hand-off block is marked Preview. A handoff is a run after the signature, and the implementation lead acts only on that. Until then the three dates stay proposed.

**The ENGAGED Rule.** An ENGAGED account has two-way contact and no open deal, so there is no contract, no signature date and no kickoff to plan from. An INBOUND account with no deal open is the same case, because INBOUND stays until a deal opens. For either status this skill sets no three dates, writes no composite and issues no Preview. It returns one list instead, drawn from the records: each of the six dimensions, with the record that would score it, or INSUFFICIENT with the discovery question that would fill the gap. The rep can use that list in the next conversation, so the gaps close before a deal opens. Once a deal opens (ACTIVE), the Preview and handoff rules above apply. A date set before a signature is a guess, and the implementation lead would plan from it.

| Output | Where It Lives | Notes |
|---|---|---|
| Readiness report | Inline, in the chat | The nine sections of Step 7, in order |
| `readiness_score` | Inline, the composite line of the scorecard | A whole number from 0 to 100, from the formula in Methodology, with its `scored n of 6`. Under the Unknown Rule, a composite with fewer than five scored dimensions is not written |
| `dimension_scores` | Inline, the scorecard | Six entries, each a score from 1 to 5 or INSUFFICIENT, in the order Stakeholder, Workflow, Technical, Data, Resource, Change Management |
| `three_dates` | Inline, the three-date plan | Kickoff, go-live and Full Adoption Date, each with its arithmetic shown. Before signature, all three are labelled proposed |
| `risks` | Inline, the risk section | The top three, each with severity, likelihood and a specific mitigation. Severity and likelihood follow the rules under Risk Categories |
| `quick_wins` | Inline, the quick win section | A week one item, a month one item and the 90-day criteria |
| `next_action` | Inline, last line of the report | One move by one owner to one person on one date, chosen by this priority order (full text in Step 7, Choosing The Next Action): (1) a reply owed to a buyer who wrote to us, when the record holds one, because a buyer waiting on us is the delay that costs trust first, (2) the ask that mitigates the highest-ranked risk whose mitigation needs a buyer-side person, because only the buyer can clear it and the kickoff conditions wait on it, (3) the ask for the next-ranked risk of that kind, (4) steps for our own team or a third party (a test export, a quick win, a risk audit), always listed after the buyer-side steps, because the team can do them without waiting on anyone. Ties break on the risk ranking keys (severity, dimension score, likelihood, row order). Asks to the same person on the same date that they can answer from what they already know travel in one message, in risk order. Every other open step is listed after it as a later step. The date is the one the shared contract's next-action rule gives (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source), and a later dated event, such as a board meeting or the expected signature, does not move it. It names the action the owner takes, as a verb phrase, and never the result the action is meant to produce |
| `report_path` | Set only when a file was written | `none (inline)` when the report stayed in the chat |
| File, on request | `<account>_gtm-sales-handoff_<date>.md`, beside the user's account notes | Written only when the user asks, in Markdown, with the readiness card. The ask is the approval step |

---

## Context

This skill does not contain client-specific information. It points to it.

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

Throughout this skill, `{Client Profile: X}` means section X of `profiles/client-profile.md`. Sections this skill reads:

| Profile Section | Used For |
|---|---|
| Company | Account framing and vertical context |
| Core Pain Points | Mapping why the customer bought, which sets the quick wins |
| Product Modules | Matching contracted modules to names, and sizing the implementation scope in Step 1 |
| Implementation Profile | The timing values for the three dates: typical days from kickoff to go-live, how data moves, the timing variables, the default months to full adoption, and the team's own quick win types |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (its notes, calls and decisions) |

If any section in this table is missing, the skill says so once at the start, runs uncustomized on the Methodology defaults, and marks every output that depended on the missing section. Go-live is then written as `[RECORD]`, not estimated. The Implementation Profile is the section most often missing, and `CUSTOMIZE.md` writes it. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

### The Shared Contract

Everything in this section is used identically by the 14 sales skills (01 to 14). The names below are copied exactly, so the 14 never drift from each other.

#### The Profile Is The Only Source Of Company Facts

Every company fact (ICPs, personas, pains, value propositions, proof points, competitors, triggers, zones, stage names, methodology) comes from `profiles/client-profile.md`. A skill reads the sections its Context table names and nothing else. A skill never carries a company fact of its own. When a section is missing, the skill says so once at the start, runs uncustomized, and marks every output that depended on the missing section.

#### The Knowledge Base And Connectors

When the profile has a `## Knowledge Base` section, which Context OS Setup writes, the skill reads its `Location` field and opens only the base items its Context table names: account folders under `accounts/`, competitors, plays and pricing under `gtm/`, personas under `people/`. Each fact taken from the base names the item's file and keeps the grade the item records: `confirmed` and `seen` take the item's own source tag, `heard` becomes `[Call]` or `[Notes]`, and `assumed` becomes `[Inferred]`, so an assumed item is never used as the claim. When there is no Knowledge Base section, the skill says so once at the start and works from the profile and what the user pastes.

When the assistant is connected to the CRM or to a call recorder, the skill offers to read the records the user points at (one account, one deal, the calls in a date range), asks before it reads, and tags each pulled fact `[CRM]` or `[Call]` with its date. It reads only. It never searches records nobody named and never writes back. Without a connector, pasting the same records works the same way.

#### Account Status, Six Words

Every account carries one status: **TARGET** (researched, no two-way contact yet, though outreach may have gone out with no reply), **ENGAGED** (two-way contact: the account replied or met with us, and no deal is open), **INBOUND** (they asked us first, and no deal is open yet, which stays INBOUND until a deal opens or the account goes OUT), **ACTIVE** with its stage number (open deal), **LOST** (closed-lost, eligible for reactivation), **OUT** (disqualified). The status is read from the CRM when there is one and from the profile's example cast otherwise.

#### The Verdict Words And The Zone Rule

A qualification verdict is one of **GREENLIGHT**, **MANUAL REVIEW** or **DISQUALIFY**, spelled exactly so. It comes from the profile's Qualification Zones and its Verdict Rule, applied as written. MEDIUM never counts as HIGH. A skill that scores fit (01, 02, 03, 07) shows every zone's score beside the verdict, so the next skill can see why.

#### Stage Names Come From The Profile

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

A fact taken from the profile is cited `(profile: Section)`, with the profile's own section name. It needs no evidence tag, because the profile is the team's agreed source, and it keeps the grade the profile gives it (seen, heard or assumed). A fact with no tag or profile citation is removed. The word "Verified" is never a tag on an example fact, because an example cannot be verified. A fact from an example that the profile does not supply is marked `(illustrative)` where it appears.

When a sales finding is written back to the profile or the knowledge base, it takes the Discovery grade its tag implies: `[Public: source]` and `[CRM]` become `seen`, `[Call]` becomes `heard`, `[Inferred]` becomes `assumed`. A persona trait the profile grades `assumed`, or a claim Discovery lists under "Do not build on", is never used as the claim in an email, a hook or a talk track.

#### Numbers

Every rate carries its n ("4 of 7 criteria", never "57%" alone). A pattern needs five cases. A blank CRM field is unknown, not a no. "No difference found" is a finding and is reported. A benchmark needs a named, dated source or it is removed. Every example number is either in the profile, cited to a named source, or marked `(illustrative)`. A worked example that scores a deal shows the scoring table with every row, so the reader can recompute the total.

#### Report First, File When Asked

Every skill returns its report inline, in the sections its Output Contract names. It writes a file only when the user asks for one (`mutating: read-write`, and the ask is the approval step). The file is Markdown, named `<account>_<skill>_<date>.md`, saved beside the user's other account notes.

#### Nothing Sends, Nothing Writes To The CRM

A skill drafts emails, call openers and sequences. The rep sends them. A skill never sends, never enrolls a contact, and never writes to the CRM. The user does those, after reading the draft.

#### The BDR Guard

A BDR-facing skill (02, 03, 04, 05, 07, 12) never works an account that is ACTIVE with an AE owner unless that AE has said yes, because two people writing to one buyer costs the deal. An account pending AE assignment is not ACTIVE. It is worked, and the output says it is pending.

#### Champion Tests, One List

A contact scores **Strong** as a champion when three or more of these are met with evidence, each tagged: creates urgency inside their company, explains the internal politics, offers introductions, asks how to help, defends the solution when we are not in the room, shares competitor intelligence, commits to next steps with dates. "Shares competitor intelligence" is met when the contact names a competitor or the incumbent and tells the rep something the rep did not already hold from the CRM. "Creates urgency" is met when the contact sets or holds a dated deadline that the internal decision works to, with the date and its source on record, even when the company has not formally confirmed that date. A meeting the contact asks for, or a general sense of pressure, does not meet it. "Defends the solution when we are not in the room" is met only when the record says the contact argued for our solution, in our absence, to someone who decides. A briefing or a status update is not a defence. A test the skill has not yet run is written "not yet run", never scored. One or two met is **Developing**. None met is **None**. A friendly contact is not a champion. The same list and thresholds are used by 09, 10 and 13.

#### Incumbent Types, One List

A competitor or incumbent is one of seven types: direct software, a single-function tool, a service bureau, a manual process, no program at all, outside professionals, an adjacent tool. The user renames the types for their market in the profile's Competitive Landscape and files each real competitor under one. The same seven are used by 11 and 12.

#### Talk-Time Bands, One Table

Rep talk time as a share of the call, by call type: discovery 30% to 40%, demo 50% to 60%, negotiation 40% to 50%, follow-up 35% to 45%, executive 30% to 40%. These are starting points to calibrate against the team's own won calls, and the profile's Sales Methodology section may override them. The same table is used by 06 and 13.

#### What The Close Reads

Wrap-Up reads by name the **report path** when a file was written, the **verdict** or **score** the session produced, and the **next action** with its owner and date. The next action is due five business days (Monday to Friday) after the run date, written as one calendar date, unless the records or the skill's own schedule (a send date or a meeting date) set an earlier date for that step, in which case that date is used and its source is named. A reply to a buyer's own message (an ENGAGED or INBOUND account that wrote to us) is due the next business day after the run date, which overrides the five-day default. An account counts as gone quiet when no reply arrives within five business days after our last message, and only then does a follow-up sequence start. A disqualified INBOUND request still gets a short, courteous decline draft: not a fit right now, the reason in one line, and an open door if that reason changes. The rep reads it before anything goes out. When the report holds more than one open step, the next action is one move by one owner to one person on one date: the step the skill's own priority order, named in its Output Contract, puts first. Asks to that same person that fit in the same message travel with it. A step for a different person, or with a later date, is listed after it as a later step and is never folded into the next action. Ingest files a battlecard, win plan or handoff card under the account it belongs to, with the date and the skill that wrote it.

#### Guild Disciplines, Restated

1. **Evidence Over Optimism.** Score what the record proves, not what the rep believes. Under-scoring protects a deal. Over-scoring kills it.
2. **Silence Is Not A No.** An empty field is unknown and is counted in no denominator.
3. **One Cast, One Story.** Every example uses the profile's example company and its cast. An example never presents an invented number as a real result.
4. **The Profile Is Upstream.** Strategy skills write it. Sales skills read it. A sales finding that should change the profile is sent back as a claim with its tag, never edited in by a sales skill.
5. **Published Numbers Only.** A figure from a published Guild article may be cited to it. Any other figure in an example is marked illustrative.
6. **Names As Roles** in anything shared. No vendor, tool or model names in a free skill beyond the platform line. The CRM is "the CRM".
7. **Draft, Never Send.** A rep reads before anything leaves.

## Methodology

Your readiness framework. The dimensions and scoring rules below give a structured reading of customer readiness and of the implementation risks it carries.

### 6 Readiness Dimensions (1 To 5 Each)

#### Dimension 1: Stakeholder Readiness (Weight: 20%)
- **5** = All roles filled, all contacts responsive
- **4** = Key roles filled, minor gaps
- **3** = Champion identified but sponsor unclear or disengaged
- **2** = Only sales champion engaged, no other stakeholders introduced
- **1** = No clear implementation owner on customer side

A named buyer-side person from a function other than the champion's, who took part in a call whose date is on record, counts as introduced. Once one is on record, the 2 line does not apply, and the 3 line reads on the sponsor. A contact who is only on file in the CRM, with no dated call, is not yet introduced.

#### Dimension 2: Workflow Readiness (Weight: 20%)
- **5** = Workflows fully documented, volume baselines established, success criteria defined
- **4** = Mostly understood, some baselines available
- **3** = General understanding, specific steps and volumes not well documented
- **2** = Limited discovery notes, pain exists but process not mapped
- **1** = No workflow documentation, shallow discovery

A partial baseline, a volume the customer stated on a call whose date is on record (Step 3), counts as "some baselines available". It lifts Workflow only as far as the mapping allows, because the 4 line also needs the steps mostly understood. With no measured baseline, or with no success criteria defined, Workflow stays below 5.

#### Dimension 3: Technical Readiness (Weight: 20%)
- **5** = Source system identified and familiar, IT available and engaged, export confirmed, clean data
- **4** = Source system identified, IT available but not briefed, minor data concerns
- **3** = Source system known but unfamiliar format, IT shared or 2 to 4 week lead, some gaps
- **2** = Source system unclear or multi-system, IT outsourced or constrained, significant data concerns
- **1** = Source system unknown, no IT engagement, never done integration, major data issues

While no IT owner is named, IT counts as constrained, and a constrained IT caps Technical at 2, however clear the source system is. "No IT owner named" meets the constrained condition by itself, even with one named source system. It does not lower Technical to 1, because the 1 line also needs the source system unknown.

#### Dimension 4: Data Readiness (Weight: 15%)
- **5** = All critical data elements available, clean, customer already exports elsewhere
- **4** = Most data available, minor gaps solvable
- **3** = Core data exists but quality uneven, some manual entry during transition
- **2** = Significant gaps, multiple systems, fragmented data
- **1** = No clear data source, data may not exist in structured format

#### Dimension 5: Resource Readiness (Weight: 15%)
- **5** = Dedicated project resources, realistic timeline, no competing initiatives
- **4** = Resources identified, some competing priorities but manageable
- **3** = Shared resources, may need to work around other initiatives
- **2** = Significant constraints (freeze, migration, key people on leave)
- **1** = No resources allocated, haven't thought about implementation

#### Dimension 6: Change Management Readiness (Weight: 10%)
- **5** = Strong executive mandate, team enthusiastic, champion has communication plan
- **4** = Leadership supports, team open but needs training
- **3** = Some team members resistant, champion will need to manage expectations
- **2** = Significant inertia, multiple skeptics during discovery
- **1** = High resistance, current team sees product as threat, no change champion

A named skeptic among the operations lead or the power users holds Change Management at 3, even when leadership is supportive.

**Composite Score:** Weighted sum ÷ 5 × 100, where each weight is a decimal (20% is 0.20). The result runs from 0 to 100. Round a fractional result half up to a whole number before the level is read, and a whole number on a level's edge takes the level whose range lists it. Each weight is written as a decimal: 20% is 0.20, 15% is 0.15 and 10% is 0.10. The six decimal weights total 1.00, so the composite stays between 0 and 100. The whole-number weights must never be used as written, because 20, 15 and 10 give a total 100 times too large. Under the Unknown Rule below, the weighted sum runs over the scored dimensions only, and the weights are re-scaled to them: composite = (sum of decimal weight × score, over scored dimensions) ÷ (sum of decimal weights, over scored dimensions) ÷ 5 × 100.

**The Unknown Rule.** A dimension with no evidence is INSUFFICIENT. It carries no value, and it is left out of the composite and the count. The composite is written with its scored count, `scored n of 6`. With five dimensions scored, the composite is given. With fewer than five, there is no composite, and the report lists the evidence that would score each missing dimension. A dimension with some evidence is scored from that evidence, even if the evidence shows a gap.

| Score | Level | Recommendation |
|-------|-------|----------------|
| 80 to 100 | Green: Ready | Proceed to kickoff in the week of the handoff. Standard timeline |
| 60 to 79 | Yellow: Ready with conditions | Address gaps before kickoff. Kickoff sits two to four weeks after the readiness check, before any IT lead time (see The Three Dates) |
| 40 to 59 | Orange: At risk | Significant gaps. Hold kickoff until every critical dimension reaches 3 |
| 0 to 39 | Red: Not ready | Major failures. Sales re-engages, and no handoff is issued |

A **critical dimension** is any dimension scored 2 or lower.

### Implementation Stakeholder Roles

| Role | Why They Matter | How To Identify | Who Usually Fills It |
|------|-----------------|----------------|----------------------|
| **Executive Sponsor** | Escalation path, removes blockers, ensures commitment | Senior-most person engaged during sales | The budget holder who signs or approves, such as the owner, the general manager or the chief financial officer |
| **Implementation Champion** | Day-to-day rollout owner | Drives adoption, coordinates resources, attends all sessions | The sales champion, or the operations lead who runs the daily work |
| **IT Lead** | Sets up integrations, manages system connections | Technical person from the customer's IT team | An internal IT person, or an outside IT provider when the customer has no IT staff |
| **Power Users** | First to learn, train peers | Front-line staff who understand the workflow | Two or three staff who do the work today |
| **Data Owner** | Validates data mapping, confirms accuracy | Person who understands the source data model | Whoever keeps the source records, such as an office manager or a records clerk |

### Technical Assessment Dimensions
| Dimension | Green | Yellow | Red |
|-----------|-------|--------|-----|
| Source system identified | Yes, familiar format | Yes, unfamiliar format | Unknown or multiple systems |
| Data export capability | Already sending data elsewhere | IT can build it | No IT capability |
| Integration readiness | Standard practice | Need guidance but capable | Never done it |
| Data quality | Good hygiene, few gaps | Some known issues | Major gaps, duplicates |
| IT availability | Available now, dedicated | Shared resource, 2 to 4 week lead | Frozen, outsourced, 6 or more weeks |
| Security and compliance | Standard, SOC 2 sufficient | Additional documentation needed | Full security audit required |
| Multi-system complexity | Single source system | 2 systems, known pattern | 3 or more systems or custom middleware |

Integration advantages to note: the product takes any standard output, most customers already export data to another system (redirect that export), and existing parsers cover the common file formats.

### Risk Categories
| Category | Common Risks | Mitigation Strategy |
|----------|-------------|-------------------|
| **Technical** | Integration delays, unfamiliar format, IT bandwidth | Ask the buyer to name an IT owner before kickoff when none is named. Fallback: manual upload during setup. Request an IT timeline at kickoff. Engage engineering early for unfamiliar systems |
| **Adoption** | Team resistance, "we've always done it this way" | Champion-led change management. Identify two or three power users for a pilot. Show quick wins in week one |
| **Resource** | Key person on leave, competing projects, seasonal constraints | Build a timeline buffer. Identify backup contacts. Set availability commitments at kickoff |
| **Data** | Poor quality, missing fields, duplicates | Ask the buyer to name the Data Owner who holds the source records, before the audit. Data quality audit in week one. Cleanup sprint before go-live. Accept manual workarounds at first |
| **Expectation** | Unrealistic timeline promises, expecting immediate ROI | Align expectations at kickoff. Reference the typical timeline. Set 30, 60 and 90 day milestones |
| **Vendor transition** | Existing provider contract still active, overlapping services | Map contract end dates. Plan a parallel-run period. Ensure no service gap |
| **Stakeholder** | No executive sponsor named, no IT lead, or the champion has gone quiet | Name the sponsor and the IT lead before kickoff. Put the sponsor's written confirmation in the kickoff conditions |

**Ranking The Top Three.** Sort by these keys in order, and stop at the first key that separates two risks:
1. Severity: HIGH first, then MEDIUM, then LOW.
2. Dimension score: within a severity, a risk on the lower-scoring dimension comes first. Each risk maps to its dimension: Technical to Technical, Data to Data, Stakeholder to Stakeholder, Resource to Resource, and Adoption to Change Management. A risk that maps to no scored dimension (Expectation, Vendor transition) ranks after the dimensioned risks of the same severity.
3. Likelihood: a High likelihood comes before a Medium one.
4. Row order: a tie on all three keys goes to the row order of the Risk Categories table.

**Severity And Likelihood.** Severity is HIGH when the risk leaves no named owner for IT or for the sponsor, or when it is a reason kickoff is held. Severity is MEDIUM when the risk can move a date, but an owner is named and kickoff is not held. A data gap with no named data owner is MEDIUM, not HIGH, because it moves a date and its first mitigation step is naming that owner. It becomes HIGH only under one of the two HIGH tests above. Severity is LOW when it moves no date. Likelihood is High when a record shows the risk is already present, Medium when a record shows a signal of it, and Low when no record points at it. Each risk states both.

The same severity test applies to every other risk, a named skeptic included. A skeptic's resistance can move a dated step, such as the pilot or go-live. It is MEDIUM while a named owner, such as the champion, manages it, and HIGH when no one owns it.

### The Three Dates

The signature is the handoff trigger, not one of the three dates. The three dates are the ones the implementation lead plans from: kickoff, go-live and Full Adoption Date. Every date shows its arithmetic. Before signature, all three are labelled proposed, and the whole report carries the Preview label.

**Date 1: Kickoff.** The day the implementation lead starts. Kickoff equals the check date, plus the buffer, plus the IT lead time when no IT owner is named on the check date. Set by the readiness level:
- **Green (80 To 100):** kickoff in the week of the handoff.
- **Yellow (60 To 79):** kickoff two to four weeks after the readiness check. The check date is the anchor, not the signature. Count the buffer forward from the check date, so three weeks is 21 days after it. Without a dated reason for another point in the window, use three weeks. Under Yellow a critical dimension does not hold kickoff by itself. The report lists the conditions that must be met first, and the kickoff date stays proposed until they are.
- **Orange (40 To 59) Or Red (0 To 39):** no kickoff date is set until every critical dimension reaches 3. Any date shown is marked conditional. A conditional date uses the Yellow rule's three-week buffer from the check date, plus the IT lead time when no IT owner is named, and go-live and the Full Adoption Date follow it as usual.
- **IT Lead Time:** the profile's IT lead time is added to the kickoff date when no IT owner is yet named. It comes on top of the buffer, so kickoff can fall more than four weeks after the check. It is read on the check date: an IT owner named by then means no lead time is added.

**Date 2: Go-Live.** Kickoff plus the typical days from kickoff to go-live in the Implementation Profile, written as the arithmetic: kickoff date plus N days. The skill ships that value blank. If the profile has no value, go-live is written as `[RECORD]`, and the skill does not estimate it.

**Date 3: Full Adoption Date.** Kickoff plus the default of two months. The two months are this skill's default, and the profile's Full Adoption months may override them. Then each adjustment from the Implementation Profile is applied and shown as its own line:
- **Source Systems:** each system beyond the first adds the profile's value in weeks. With one system no adjustment applies, and no profile value is needed.
- **Export Format Familiar To The Team:** a familiar format subtracts the profile's value in weeks. A format the team has not yet seen in a project counts as new, and a new format subtracts nothing. A vendor's confirmation that the export works is not the team's familiarity, which is the team's own experience with the format. So a new format needs no profile value, and no `[RECORD]` is written for it.
- **Phased Rollout:** a subsidiary or business unit on a different system gets its own three-date plan, and its Full Adoption Date is set separately.
- **Weekend Roll:** if the result falls on a Saturday or Sunday, it moves to the next Monday, and the line says so.

When the profile holds no value for an adjustment that applies, the adjustment is written as `[RECORD]` and the Full Adoption Date is stated as provisional.

**Volume Projection:** "Expect about [number] [units] per [period] for this customer," with the number, the unit and the period taken from the customer's own figures and tagged. The monthly conversion sits beside it with its arithmetic: a weekly figure is times 52 divided by 12, rounded half up to a whole number and written "about". When the customer's unit is not the product's own unit, the line names the unit the customer used. With no figure from the customer, the line is written `[Unknown]`.

### Quick Win Types

This is a starting catalog of four. Pick two or three. Each one must be something the customer can see working in week one or month one. The Implementation Profile can add the team's own types. When the profile's team types are `[RECORD]`, these four are the whole catalog, and the report says so.

| Type | What It Is | Generic Example | Dimension It Addresses |
|------|-----------|-----------------|------------------------|
| **Automate the highest-volume segment** | Move the most frequent repeat task for one segment into the product | Route the most common request type through the system for the top five accounts in week one | Workflow |
| **Enable self-service for top customers** | Give the most active customers direct access to the status they check most often | Let the most active customers see their own item status without a call to the team | Change Management |
| **Run a risk audit of open items** | Review open items for the errors or deadlines that carry the most risk | Check all open items against the deadline list and flag any item due in the next 30 days | Data |
| **Remove one manual step** | Find the single manual step that costs the most team hours and remove or automate it | Replace a manual copy from a spreadsheet with a direct import from the source system | Technical, when the step removed is a manual copy from the source system. Workflow otherwise |

**Choosing The Week-One Quick Win.** The week-one type is the one that addresses the dimension of the top-ranked risk, aimed at that risk. When no type addresses that dimension (Stakeholder and Resource have none), the week-one type is the one the team can run without the buyer: Run a risk audit of open items, on the records the team already holds. The month-one item is a different type, matched to the customer's situation.

---

## Quick Reference

**Use This Skill When:**
- A deal is closed-won, or about to close, and needs the handoff to implementation
- Before signature, as a readiness preview: the three dates are proposed, and no handoff is issued until the signature
- Preparing for an implementation kickoff meeting
- Checking whether a near-close deal is ready for a smooth implementation
- A sales manager is reviewing handoff quality

**Don't Use When:**
- The deal is still in the active sales process and no preview is wanted (use `gtm-deal-pulse` or `gtm-meddpicc-analysis`)
- The question is account strategy before the sale (use `gtm-competitive-strategy`)
- The account is ENGAGED or INBOUND with no deal open. The run returns the gap list under The ENGAGED Rule instead of dates, a composite or a handoff
- The customer is already in implementation. This is for the transition point only

**User Roles:** AE (primary), Sales Manager
**Expected Time:** 20 to 30 minutes per account

---

## Core Workflow

Each step ends with what it produces. The order matters: the scores in Step 5 set the dates in Step 6, and the report in Step 7 is the only place the dates and scores appear together.

### Step 1: Pull Deal And Engagement Data

Before pulling anything, read the account's folder under `accounts/` (its notes, calls and decisions) in the knowledge base, when the profile has one. Then offer to read the CRM deal and contact records, and ask before reading them, as set out in The Knowledge Base and Connectors.

Query the CRM for the account and record each field, or `[Unknown]` where it is blank.

**Deal Basics:**
- Account name, industry and sub-industry
- Contract value (ARR) and deal type
- Contracted modules. Match each one to its name in `{Client Profile: Product Modules}`. A module the profile does not list is written as the CRM names it and tagged `[CRM]`
- Contract signing date, or expected close
- AE and opportunity owner
- CS owner, if one is already assigned
- How the deal was won (competitive displacement, greenfield or expansion)
- Account status, read from the CRM: TARGET, ENGAGED, INBOUND, ACTIVE with its stage, LOST or OUT. The status decides the run, and an ENGAGED or INBOUND account with no deal open gets the gap list under The ENGAGED Rule

**Discovery Context (From Deal Notes And Call Transcripts):**
- What pain drove the purchase? Map it to `{Client Profile: Core Pain Points}`
- What does the customer expect success to look like?
- Implementation concerns raised during sales
- Competitors displaced, and the contract termination timeline
- Timeline commitments made during sales

**Customer Profile:**
- Number of employees on the implementation team
- Number of locations or entities to onboard
- Geographic footprint, and whether it spans regions
- Estimated monthly volume (units processed)
- Source system named during sales

**Produces:** the deal basics, the contracted modules matched to Product Modules names, and the discovery context, each field tagged or marked `[Unknown]`.

### Step 2: Build The Stakeholder Map

Identify every contact and assign an implementation role from `{Methodology: Implementation Stakeholder Roles}`. The map comes before the scoring because Stakeholder and Change Management cannot be scored without it.

For each contact:
- Name, title, department, email and phone
- Engagement level during sales (active, moderate or passive)
- Implementation role, checked against the "Who Usually Fills It" column

**Flag These Risks:**
- No Executive Sponsor identified: high risk of a stalled implementation
- IT Lead not engaged during sales: expect integration delays
- The implementation champion is a different person from the sales champion: a relationship transition is needed
- Outsourced IT: longer lead times

**Produces:** the stakeholder map with each role filled or marked `[Unknown]`, and the flags.

### Step 3: Assess Current-State Workflows

Analyze how the customer handles each process today. Pull from the discovery notes and call transcripts.

**For Each Workflow Step, Assess:**
- How it is done today (manual, system-generated or a third-party service)
- Volume per month
- Processing time per unit
- Team hours spent per week
- Known error rates or quality gaps

**Capture Volume Baselines** for the post-implementation success measure:
- Units processed per month
- Average processing time per unit
- Team hours spent on admin per week
- Current quality or compliance rate, if known
- Losses attributable to process failures, if disclosed

**Produces:** the workflow summary and the baseline list. A baseline that was never measured is written as `[Unknown]`, not as a zero. A volume the customer stated on a call is a partial baseline when the call's date is on record. A volume whose call date is Unknown places no fact in time and is not a baseline. The Workflow rubric's baseline lines then decide the score: a partial baseline meets "some baselines available", and a 5 needs measured baselines. A label such as (illustrative) marks a figure as invented for an example, and it does not change whether a stated volume counts.

### Step 4: Assess Technical Readiness

Evaluate the customer's technical environment against `{Methodology: Technical Assessment Dimensions}`. Score each dimension Green, Yellow or Red from the evidence gathered. This comes before Step 5 because the Technical score depends on it.

**Produces:** the seven technical rows, each Green, Yellow, Red or `[Unknown]`, with its evidence tag.

### Step 5: Score The Six Readiness Dimensions

Score each dimension from 1 to 5 with the rubric in `{Methodology: 6 Readiness Dimensions}`, or mark it INSUFFICIENT under the Unknown Rule when it has no evidence. Score the evidence, not the claim: a rep's statement that the customer is ready is a claim, and it moves a score only when a record supports it. Then compute the composite with the formula in Methodology, state its scored count, and set the readiness level.

**Produces:** `dimension_scores` (six, each with its evidence or INSUFFICIENT), the weighted table, and `readiness_score` with its scored count and its level.

### Step 6: Build The Three Dates And The Risk Mitigations

Set the three dates with the rules in `{Methodology: The Three Dates}`, showing each arithmetic line. Then name the risks from `{Methodology: Risk Categories}`, each with its severity (HIGH, MEDIUM or LOW), its likelihood and its own mitigation. Then pick two or three quick wins from `{Methodology: Quick Win Types}` and the team's Implementation Profile, matched to the customer's situation.

**Why The Dates Come After The Score:** the readiness level decides whether kickoff can be set, so the date rules cannot run until Step 5 has produced the level.

**Produces:** `three_dates` (kickoff, go-live and Full Adoption Date, each with its arithmetic), `risks` (the top three), and `quick_wins` (week one, month one and the 90-day criteria).

### Step 7: Write The Readiness Report

Write the nine sections in order. The readiness card takes sections 1, 2, 3, 4, 7, 8 and 9.

**1. Deal Handoff Summary:** account, contract value, modules, AE, CS owner, why they bought, and the competitor displaced

**2. Three-Date Handoff Plan**

| Date | Value | Basis |
|------|-------|-------|
| Kickoff | [date] | The readiness level and its buffer rule, with the arithmetic |
| Go-Live | [date] | Kickoff plus the typical days from the Implementation Profile |
| Full Adoption Date | [date] | Kickoff plus the default months, with each adjustment and the weekend roll |

Volume projection, one line.

**3. Readiness Scorecard**

| Dimension | Score | Key Evidence | Primary Risk |
|-----------|-------|-------------|-------------|
| Stakeholder | X/5 | | |
| Workflow | X/5 | | |
| Technical | X/5 | | |
| Data | X/5 | | |
| Resource | X/5 | | |
| Change Management | X/5 | | |
| **Composite** | **X/100, scored n of 6** | | |

**4. Stakeholder Map**

| Name | Title | Impl Role | Engagement | Contact |
|------|-------|-----------|-----------|---------|

**5. Current-State Workflow Summary:** how each process is handled today, monthly volume, processing time and the key pain.

**6. Technical Environment:** source system, server type, integration path, IT availability and data quality.

**7. Risk Mitigations: Top 3:** risk, severity, likelihood and the specific mitigation.

**8. Quick Wins:** week one, month one and the 90-day success criteria.

**9. Handoff Checklist**

**Sales Team Completes:**
- [ ] Discovery notes and call recordings shared
- [ ] All stakeholder contacts verified
- [ ] Timeline commitments documented
- [ ] Technical requirements noted
- [ ] Success criteria agreed with the customer
- [ ] Three-date plan communicated

**Implementation Team Confirms:**
- [ ] Implementation owner assigned
- [ ] Implementation resources allocated
- [ ] Kickoff meeting scheduled
- [ ] Integration requirements reviewed
- [ ] Risk mitigation plan acknowledged

**Choosing The Next Action.** The report usually holds several open steps: the mitigations of the top three risks, the conditions before kickoff, and the quick wins. The next action is the first step in this order, which puts the step that serves the rep best first:

1. **A reply owed to a buyer who wrote to us,** when the record holds a buyer's message with no reply. It comes first because a buyer waiting on us is the delay that costs trust first, and the shared rule makes it due the next business day. A question we asked that has no recorded answer is not a reply owed. It is an open condition, and its ask is repeated where the order below places it.
2. **The ask that mitigates the highest-ranked risk whose mitigation needs a buyer-side person,** ranked by the four keys under Ranking The Top Three. Only the buyer can clear these risks, and the conditions before kickoff wait on them.
3. **The ask that mitigates the next-ranked risk of that kind,** and so on down the top three.
4. **Steps for our own team or a third party,** such as a test export with the incumbent's support, a quick win, a risk audit or an entry on the project plan. They always come after the buyer-side steps, because the team can do them without waiting on anyone.

The rest of the rule:
- **The Person.** The ask goes to the buyer-side person the mitigation names. When the mitigation needs someone the buyer has not yet named, such as an IT lead or a sponsor, the ask goes to the contact who can name them: the champion, unless the record names another.
- **Bundling.** Asks of kinds 2 and 3 that go to the same person on the same date travel in one message, in risk order. An ask fits that message when the person can answer it from what they already know, such as naming a person or confirming a role in writing. An ask that needs days of work first, such as timing a week of lookups or running an export, has a later date and is a later step. The asks in the message are the asks for the top three risks only. A risk ranked fourth or lower has its ask listed as a later step, even when the same person could answer it.
- **Ties.** The risk ranking keys (severity, dimension score, likelihood, row order) already separate every pair of risks, so the order needs no other tie-break.
- **The Owner.** The AE owns the next action before the signature. From the signature on, the implementation lead who takes the handoff owns it.
- **The Date.** The shared contract's next-action rule sets it. A later dated event in the records, such as a board meeting or the expected signature, does not move it.
- **Later Steps.** Every other open step is ranked after the next action and listed in the report under Later Steps, each with its owner and the person it goes to, and none is folded into it. The `next_action` line stays the last line of the report.

**Produces:** the nine-section report, with `next_action` as its last line, carrying its owner, its person and its date, with the later steps listed above it. `report_path` is set to `none (inline)`.

---

## Epistemic Rules

- **Every Count And Rate Carries Its N.** Write "2 of 5 roles filled," never a bare share. A score is a reading of the rubric, so it is never written as a rate.
- **Silence Is Not A No.** A blank contact or field is `[Unknown]`. It is not scored as present or absent, and it is counted in no denominator. The gap it leaves is written as a risk.
- **A Claim Is Not A Record.** A rep's statement that the customer is ready, or that IT is on board, scores only when a dated record supports it. Otherwise it is shown as a claim with its source.
- **A Default Is Not A Measurement.** The two-month Full Adoption default and the Implementation Profile's values are planning assumptions. A profile value that is blank is `[RECORD]`, and an example figure is `(illustrative)`, never a benchmark.
- **Five Cases Before A Pattern.** One account with an IT gap is an observation. A pattern across accounts, such as every Orange handoff missing an IT owner, needs five handoffs before it is written as a trend.
- **"No Gap Found" Is A Finding.** When a dimension shows no risk, write that and the evidence checked. Leaving the dimension empty hides the check.

---

## Hard Rules

1. **Never Issue A Handoff Without The Three Dates.** The implementation lead cannot staff a project without kickoff, go-live and the Full Adoption Date.
2. **Never Score A Dimension Above The Evidence.** Under-scoring protects the customer and the team. Over-scoring hands the lead a project that is not ready. A dimension with no evidence is INSUFFICIENT, never scored high or low to fill the gap.
3. **Never Fill An Implementation Profile Value From An Estimate.** A typical duration written without a basis becomes the date the customer is promised.
4. **Never Send Anything To The Customer And Never Write To The CRM.** The rep and the implementation lead own those steps, after reading the draft.
5. **Never End A Report Without `next_action`, With Its Owner And A Date.** The Wrap-Up close reads that line by name, and a report without it leaves the next step with nobody.
6. **Use One Name For Each Of The Three Dates.** Kickoff, go-live and Full Adoption Date are the names the hand-off fields carry, so the lead and the close read the same thing.

---

## Quality Bar

**Done When All Are True:**

- [ ] Deal data is complete, or each blank field is marked `[Unknown]`
- [ ] Contracted modules are matched to the names in Product Modules
- [ ] At least the Executive Sponsor, the Implementation Champion and the IT Lead are identified, or marked as missing
- [ ] Workflow baselines are captured with volume and processing time, or marked `[Unknown]`
- [ ] The technical assessment names the source system and the integration path
- [ ] Each of the six dimensions is scored with its evidence, or marked INSUFFICIENT with the evidence that would score it, and at least five are scored
- [ ] The composite is computed from the weighted table over the scored dimensions, its scored count is stated, and its level is stated
- [ ] Each of the three dates shows its arithmetic, and each adjustment is shown
- [ ] Every risk has a specific mitigation, not a generic one
- [ ] Quick wins reference the customer's actual situation
- [ ] The handoff checklist is populated for both the sales and the implementation teams
- [ ] No placeholder brackets remain, except `[RECORD]` where the profile holds no value
- [ ] `next_action` is the last line, with its owner and date

---

## Examples

All three examples use the PlotIQ flagship, Brackhaven Memorial Gardens, and the people in its cast. The chain file fixes the dates, the modules and the people. Every figure is in the profile or marked `(illustrative)`. Each example shows all six dimension scores with the weighted table, and each ends with its hand-off block.

### Example 1: Yellow Readiness Check On 2026-11-02, Before Signature

**Context:** Brackhaven Memorial Gardens has two sites and 11,000 plots (profile: Example Cast). Stage 5 Negotiate (`[CRM]`). The family board meets 2026-11-12, and the signature is expected 2026-11-16 (`[CRM]`). Contracted: Plot Inventory Digitization and Records and Trust Compliance (illustrative). Two sites at $10,788 a year each at list, so $21,576 a year, plus $5,000 setup (profile: Product Modules). Owen Pruitt is the AE. Eli Marsh, Implementation Lead (profile: Example Cast), takes the handoff.

**Input:** "Run the readiness check for Brackhaven Memorial Gardens before they sign."

**Preview:** before the signature (expected 2026-11-16), so the three dates are proposed and the report carries the Preview label.

**Process:** Ruth Ellery is the champion. Two of seven shared champion tests are visible on the 2026-10-27 call, each tagged `[Call, 2026-10-27]` (illustrative): she explains the internal politics and asks how to help. The family board chair is a role with no name on file (`[Unknown]`) who has joined one call (`[CRM]`). No IT contact is on file (`[Unknown]`). The source is Oldgate Ledger Pro (`[CRM]`), and its ledger export is not yet scoped (`[Unknown]`). Plot records are on paper (`[Call, 2026-10-27]`). Walt Okonkwo, Operations Director, is skeptical of tablets (`[Call, 2026-09-21]`). Oldgate's contract renews in March 2027 (`[CRM]`). On the 2026-10-27 call, the board chair's name and a written sponsor confirmation were raised with Ruth (`[Call, 2026-10-27]`, illustrative), and her answer is not recorded. No earlier date is on record, so the next action takes the date the shared rule gives: five business days after the run date of 2026-11-02.

**Scoring:**

| Dimension | Weight | Score (1 To 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 3 | 0.60 | Ruth Ellery is champion `[Call, 2026-10-27]`. The board chair is unnamed `[Unknown]` and has joined one call `[CRM]`. No sponsor confirmed in writing |
| Workflow | 20% | 4 | 0.80 | Lookup and trust report steps mapped `[Call, 2026-10-27]`. Walt's estimate of about two plot lookups a week `[Call, 2026-09-17]` (illustrative), so a partial baseline exists. Lookup times not yet timed |
| Technical | 20% | 2 | 0.40 | Oldgate named `[CRM]`. No IT contact on file `[Unknown]`. Ledger export unscoped `[Unknown]` |
| Data | 15% | 3 | 0.45 | The trust ledger holds both sites' trust numbers in one place `[Notes]` (illustrative). Plot records on paper `[Call, 2026-10-27]`, with uneven quality and some re-entry by hand during the transition `[Notes]` (illustrative). Deed scans scheduled for weeks 2 to 3 (illustrative) |
| Resource | 15% | 3 | 0.45 | Eli Marsh assigned `[CRM]`, and shared with another implementation through the end of the year `[CRM]` (illustrative). The March 2027 Oldgate renewal competes for the same people `[Notes]` (illustrative) |
| Change Management | 10% | 3 | 0.30 | Ruth is open to the change `[Call, 2026-10-27]`. Walt is skeptical of tablets `[Call, 2026-09-21]` |
| **Total** | **100%** | | **3.00** | |

**Composite:** 3.00 ÷ 5 × 100 = **60 of 100, scored 6 of 6 (Yellow, ready with conditions)**. All six dimensions have evidence, so the Unknown Rule does not apply. The score sits at the bottom of the 60 to 79 band, and Technical is a critical dimension at 2. Under Yellow that does not hold kickoff by itself, so the five conditions below must be met before the kickoff date is firm.

**Stakeholder Map:**

| Name | Title | Implementation Role | Engagement | Contact |
|---|---|---|---|---|
| Ruth Ellery | General Manager | Implementation Champion (also the sales champion) | Active on calls `[Call, 2026-10-27]` | On file `[CRM]` |
| Family board chair | Board chair, name `[Unknown]` | Executive Sponsor | Joined one call `[CRM]` | `[Unknown]` |
| Walt Okonkwo | Operations Director | Power User | Skeptical of tablets `[Call, 2026-09-21]` | On file `[CRM]` |
| Priscilla Dunmore | Pre-need manager | Power User, pre-need intake | `[Unknown]` | On file `[CRM]` |
| `[Unknown]` | No IT contact on file | IT Lead | Not engaged `[Unknown]` | `[Unknown]` |
| `[Unknown]` | `[Unknown]` | Data Owner | `[Unknown]` | `[Unknown]` |
| Eli Marsh | Implementation Lead | Implementation owner | Assigned `[CRM]` | (profile: Example Cast) |

**Current-State Workflow:** Plot lookups and the trust report are mapped `[Call, 2026-10-27]`. The trust report is built by hand from the ledger `[Call, 2026-10-27]`. Walt estimates about two plot lookups a week `[Call, 2026-09-17]` (illustrative). Lookup times have not been timed by the team.

**Technical Environment:**

| Technical Dimension | Rating | Evidence |
|---|---|---|
| Source system identified | Yellow | Oldgate Ledger Pro `[CRM]`, in an export format the team does not know yet |
| Data export capability | Yellow | The vendor confirms a trust ledger export `[Notes]` (illustrative). IT can run it only once an owner is named |
| Integration readiness | `[Unknown]` | No record of this team doing an integration |
| Data quality | Yellow | Paper plot records, uneven in quality `[Call, 2026-10-27]`, `[Notes]` (illustrative) |
| IT availability | Red | No IT owner on file `[Unknown]` |
| Security and compliance | `[Unknown]` | No record |
| Multi-system complexity | Green | One source system `[CRM]` |

**Three Dates, All Proposed Until The Signature:**
- **Kickoff:** Yellow gives a two to four week buffer from this check on 2026-11-02. Three weeks: 2026-11-02 plus 21 days = **2026-11-23** (Monday). The IT lead time is added when no IT owner is named: 2026-11-23 plus 14 days (profile: Implementation Profile, illustrative) = **2026-12-07** (Monday). The date is proposed, and it holds only if the conditions below are met.
- **Go-Live:** 2026-12-07 plus 49 days = **2027-01-25** (Monday). The 49 days is the typical days from kickoff to go-live (profile: Implementation Profile, illustrative). It is a planning value set from the six-week roadmap plus one week of buffer, not a measured one.
- **Full Adoption Date:** 2026-12-07 plus two months = 2027-02-07, a Sunday. Rolled to Monday, **2027-02-08**. No other adjustment applies: one source system adds nothing, and an export format the team does not know yet subtracts nothing.

**Risks (Top 3):** Technical (HIGH, likelihood High): no IT owner and an unscoped export. Mitigation: Oldgate's support runs a test export on a sample file before kickoff. Stakeholder (HIGH, likelihood High): the board chair is unnamed and the sponsor role is not in writing. Mitigation: Owen Pruitt asks Ruth Ellery for the chair's name and a written sponsor confirmation before the 2026-11-12 board. Adoption (MEDIUM, likelihood High): Walt Okonkwo's skepticism of tablets. Mitigation: Ruth names two or three power users for a pilot, and Walt joins the work-order demo before kickoff.

**Ranking:** Technical is first, because it is the lower-scoring of the two HIGH risks. Adoption is third. Resource and Data are also MEDIUM and score 3, so Adoption leads on likelihood, or on row order if they tie, since Adoption is row 2 of the Risk Categories table.

**Conditions Before Kickoff:**
1. Brackhaven names an IT owner.
2. Oldgate's support runs a test export on a sample file, and the result is reviewed.
3. The board chair is named and confirms the sponsor role in writing.
4. Ruth brings a week of plot lookup times, so the baseline is complete.
5. Walt joins the work-order demo.

**Quick Wins:** Week one, remove one manual step: replace the binder lookup for the top section with a search, and time it. Month one, run a risk audit of open items: check the open plots at both sites for double-sale risk (the double sale is `[CRM]` and illustrative). Ninety days: lookup times at or below Ruth's baseline, and the trust report built from the system with no hand steps.

**Handoff Checklist:**

Sales Team Completes:
- [ ] Discovery notes and call recordings shared: `[Unknown]`, not confirmed in the records
- [ ] All stakeholder contacts verified: not yet, the board chair is unnamed
- [x] Timeline commitments documented: the account plan and the three dates `[Notes]`
- [ ] Technical requirements noted: not yet, no IT owner
- [ ] Success criteria agreed with the customer: not yet
- [ ] Three-date plan communicated: not yet, the dates are proposed until the conditions are met

Implementation Team Confirms:
- [x] Implementation owner assigned: Eli Marsh `[CRM]`
- [ ] Implementation resources allocated: `[Unknown]`, Eli Marsh is shared
- [ ] Kickoff meeting scheduled: not yet
- [ ] Integration requirements reviewed: not yet
- [ ] Risk mitigation plan acknowledged: not yet

**Output:** Composite 60 (Yellow, scored 6 of 6). The block below is the check before signature. It is a preview: it runs before signature, no stage_recommendation is on record, and no handoff is issued until the re-run after signature.

```text
Hand-off (read by the implementation lead and Wrap-Up):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-11-02
readiness_score: 60, scored 6 of 6
dimension_scores: Stakeholder 3, Workflow 4, Technical 2, Data 3, Resource 3, Change Management 3
three_dates: all proposed before signature: kickoff 2026-12-07, go-live 2027-01-25, Full Adoption Date 2027-02-08
risks: Technical (HIGH), Stakeholder (HIGH), Adoption (MEDIUM)
quick_wins: week one remove one manual step, month one risk audit of open plots, 90 days lookup times at baseline
next_action: Owen Pruitt asks Ruth Ellery, in one message and in risk order, to name a Brackhaven IT owner, to name the family board chair and confirm the sponsor in writing, and to name two or three power users for the pilot, by 2026-11-09 (five business days after the run date of 2026-11-02, no earlier date on record). Later steps: the export test with the incumbent's support (team step, Owen Pruitt before signature) and the quick wins
report_path: none (inline)
```

### Example 2: Orange Readiness At Signature On 2026-11-16, Handoff Held

**Context:** The contract is signed on 2026-11-16 (`[CRM]`). The stage is now Stage 6 Closed-Won and Handoff. Oldgate's support confirmed that the trust fund ledger can be exported (`[Notes]`, illustrative). Nobody at Brackhaven has been briefed on the migration (`[Notes]`, illustrative), and no one at Brackhaven owns IT (`[Unknown]`). The family board chair is still a role with no name (`[Unknown]`). This is the non-success case: the deal is signed, but the handoff is not clean.

**Input:** "Issue the handoff for Brackhaven Memorial Gardens. They signed today."

**Process:** The Technical dimension improves on the export, because Oldgate has confirmed it. It stays at 2, because no one at Brackhaven is briefed and no IT owner exists. Resource drops from 3 to 2, because the migration and the March 2027 renewal now compete for the same people (illustrative).

**Scoring:**

| Dimension | Weight | Score (1 To 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 3 | 0.60 | Ruth Ellery is champion `[Call, 2026-10-27]`. The board chair is unnamed `[Unknown]`. No sponsor confirmed in writing |
| Workflow | 20% | 4 | 0.80 | Steps mapped with Walt Okonkwo's team `[Call, 2026-10-27]`. Lookup times not yet timed |
| Technical | 20% | 2 | 0.40 | Oldgate confirmed the export `[Notes]`, illustrative. No IT owner `[Unknown]`. Nobody briefed on the migration `[Notes]`, illustrative |
| Data | 15% | 3 | 0.45 | Export confirmed by the vendor but not tested on a sample. Plot records on paper `[Call, 2026-10-27]` |
| Resource | 15% | 2 | 0.30 | The migration and the March 2027 renewal compete for the same people (illustrative) |
| Change Management | 10% | 3 | 0.30 | Ruth champions the change `[Call, 2026-10-27]`. Walt is skeptical of tablets `[Call, 2026-09-21]` |
| **Total** | **100%** | | **2.85** | |

**Composite:** 2.85 ÷ 5 × 100 = **57 of 100 (Orange, at risk)**. Technical and Resource are critical dimensions at 2, so the Orange rule holds kickoff until both reach 3.

**Three Dates:**
- **Orange Rule:** no kickoff date is set until every critical dimension reaches 3. Two dimensions are critical here, Technical and Resource, both at 2. Orange gives no base, so the dates below are conditional and anchored on the check date, 2026-11-16 (the signature date, which is also the check date in this example).
- **Conditional Dates (Not Set):** the three-week default from the Yellow rule is used as the reference buffer: 2026-11-16 plus 21 days is 2026-12-07 (Monday). No IT owner is named at this check, so the 14-day IT lead time (profile: Implementation Profile, illustrative) is added: 2026-12-07 plus 14 days = **2026-12-21** (Monday), the conditional kickoff. Go-live is 2026-12-21 plus 49 days (profile: Implementation Profile, illustrative) = **2027-02-08** (Monday). The Full Adoption Date is 2026-12-21 plus two months = 2027-02-21, a Sunday, rolled to **2027-02-22** (Monday).
- If the conditions clear later, the readiness check is run again, and the three dates are set from that new check date.

**Risks (Top 3):** Technical (HIGH, likelihood High): no IT owner and no one briefed on the migration. Mitigation: Eli Marsh asks Ruth Ellery to name an IT owner by 2026-11-23, five business days after the run date of 2026-11-16, and Oldgate's support briefs that owner on the export. Stakeholder (HIGH, likelihood High): the sponsor is not named. Mitigation: the board chair's name and written sponsor confirmation are a condition of kickoff. Resource (MEDIUM, likelihood Medium): the migration and the renewal compete. Mitigation: the renewal date goes on the project plan with a parallel-run window before March 2027.

**Conditions Before Kickoff:**
1. Brackhaven names an IT owner, by 2026-11-23, the date in the next action.
2. That owner is briefed on the migration by Oldgate's support.
3. The board chair is named and confirms the sponsor role in writing.
4. Walt joins the work-order demo, so his pilot is agreed before kickoff.

**Output:** Composite 57 (Orange). The handoff is issued with the kickoff held. The two HIGH risks are the reason it is not Yellow.

```text
Hand-off (read by the implementation lead and Wrap-Up):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 6 Closed-Won and Handoff)
run_date: 2026-11-16
readiness_score: 57
dimension_scores: Stakeholder 3, Workflow 4, Technical 2, Data 3, Resource 2, Change Management 3
three_dates: none set (Orange rule). Conditional, anchored on the check date 2026-11-16: kickoff 2026-12-21, go-live 2027-02-08, Full Adoption Date 2027-02-22
risks: Technical (HIGH), Stakeholder (HIGH), Resource (MEDIUM)
quick_wins: week one remove one manual step, month one risk audit of open plots, 90 days lookup times at baseline
next_action: Eli Marsh asks Ruth Ellery to name a Brackhaven IT owner, and in the same message to name the family board chair and confirm the sponsor in writing, by 2026-11-23 (five business days after the run date of 2026-11-16). Later steps: the Resource mitigation, which the same owner takes to its own person
report_path: none (inline)
```

### Example 3: Red Readiness On 2026-10-19, Ruth Says They Are Ready

**Context:** Brackhaven is at Stage 5 Negotiate (`[CRM]`), with the family board on 2026-11-12. Ruth Ellery has not replied since 2026-10-03, which is 16 days (`[CRM]`). The rep reports that Ruth said the customer is ready to sign, but no dated record holds the statement, so it is a claim and scores nothing. The board date has not been confirmed by anyone since then (`[Unknown]`). The 09 rule applies: a HOLD at Stage 5 with a dated action, and a DOWNGRADE to Stage 4 Proposal if the board date is not confirmed by 2026-11-02. This is the non-success case: the readiness check runs as a preview, and no handoff is issued.

**Input:** "Run readiness for Brackhaven Memorial Gardens. Ruth says they're ready to sign."

**Process:** The CRM shows Stage 5 Negotiate with $21,576 a year at list, and the board date on file is 2026-11-12. Ruth is the only buyer contact who has replied since 2026-10-03. No IT contact is on file (`[Unknown]`), and the ledger export has not been examined (`[Unknown]`). No volume baseline exists. Ruth's "ready to sign" is a claim with no board confirmation behind it, so the skill scores the record, not the claim.

**Scoring:**

| Dimension | Weight | Score (1 To 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 2 | 0.40 | Only the sales champion is engaged `[Call, 2026-09-26]`. No sponsor or IT lead introduced |
| Workflow | 20% | 2 | 0.40 | Limited notes. The process is not mapped, and no lookup is timed `[Notes]` |
| Technical | 20% | 2 | 0.40 | Oldgate named `[CRM]`, one known source system. No IT contact `[Unknown]`, so IT counts as constrained and Technical scores 2. Export not examined `[Unknown]` |
| Data | 15% | 2 | 0.30 | Paper plot records. The ledger export has not been examined `[Call, 2026-09-26]` |
| Resource | 15% | 2 | 0.30 | The board date is not confirmed, and the champion has been silent for 16 days `[CRM]` |
| Change Management | 10% | 2 | 0.20 | Walt is skeptical of tablets `[Call, 2026-09-21]`. The team has not been briefed `[Notes]` |
| **Total** | **100%** | | **2.00** | |

**Composite:** 2.00 ÷ 5 × 100 = **40 of 100 (Orange, at risk)**. Orange holds kickoff. No handoff is issued, because this check runs before signature as a preview.

**Three Dates:** none set. The Orange rule sets no kickoff date until every critical dimension reaches 3. All six dimensions score 2 here, so all six are critical. Go-live and the Full Adoption Date both follow the kickoff, so neither is set.

**Risks (Top 3, Ranked By The Rule Under Risk Categories):** every dimension scores 2, so the Risk Categories row order decides among the HIGH risks: Technical (HIGH, likelihood High), Resource (HIGH, likelihood High), Stakeholder (HIGH, likelihood High). Technical is the first row of the table and Stakeholder the last of the three. Adoption is MEDIUM and ranks fourth, because Walt is an influencer (`[CRM]`) and the economic buyer is not in the room.

**Recommendation (Orange):** kickoff is held, and no date is set, until every critical dimension reaches 3. Sales re-engages first, in this order:
1. Owen Pruitt asks Ruth Ellery to confirm the board date by 2026-10-26, five business days after the run date of 2026-10-19, the date the 09 HOLD's dated action falls on.
2. Brackhaven names an IT contact, and Oldgate's support tests the export on a sample file.
3. Ruth names a second contact, since she is the only buyer contact who has replied since 2026-10-03.
4. Plot lookups are timed, to set the volume baseline.

**Output:** Composite 40 (Orange). Re-run the check once the board date is confirmed and the signature is in.

```text
Hand-off (read by the implementation lead and Wrap-Up):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
readiness_score: 40
dimension_scores: Stakeholder 2, Workflow 2, Technical 2, Data 2, Resource 2, Change Management 2
three_dates: none set (Orange rule: no kickoff date until every critical dimension reaches 3, and a check before signature is a preview)
risks: Technical (HIGH), Resource (HIGH), Stakeholder (HIGH)
quick_wins: none until the gaps close
next_action: Owen Pruitt asks Ruth Ellery to name a Brackhaven IT owner, then to confirm the family board date, and then to name the board chair and confirm the sponsor in writing, in that risk order and in one message, by 2026-10-26 (five business days after the run date of 2026-10-19). Later steps: the quick wins, held until the conditions close
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Phased Rollout (Multi-Entity)
**When:** The customer has subsidiaries on different systems, or several business units.
**Approach:** Build a separate three-date plan for each entity, with its own Full Adoption Date. Start with the highest-volume entity, or the one with the strongest champion. Use the first entity's success as proof for the others. Each entity gets its own technical assessment.

### Pattern: Competitive Displacement With Overlap
**When:** The customer is replacing an incumbent, and the two contracts overlap.
**Approach:** Map the incumbent's contract end date and plan a parallel-run period before it. Make the handoff plan account for the data migration from the incumbent. Use the overlap as the quick win: show the new system working beside the old one.

### Pattern: Champion-Led Handoff
**When:** The sales champion is also the implementation champion, which is the most common case.
**Approach:** Assess champion fatigue. The champion drove the evaluation and now has to drive implementation. Name a backup champion, and make sure the executive sponsor is giving the champion air cover.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---|---|---|
| Discovery was too shallow to score Workflow or Data | The sales notes do not capture the process or the volumes | If the notes hold no evidence for the dimension, mark it INSUFFICIENT under the Unknown Rule. If they show a gap, score the dimension at 2 or lower from that evidence, and flag it: "Sales discovery did not capture enough process detail for the handoff." Recommend a short follow-up call on the workflow and the volume baseline before kickoff |
| The champion left the company after signing | The champion is gone, and the introductions went with them | Score Stakeholder at 1. The AE identifies a new internal champion before implementation starts, and checks whether the departing champion made introductions. Consider whether the deal is still viable without the champion |
| The customer wants to start immediately but is not ready | Eagerness ahead of the readiness evidence | Use the score to have an evidence-based conversation: name the specific gap, say what it will cost mid-implementation, and offer the items that clear it first |
| The AE made timeline promises that do not match the readiness | The promise was made from the sales cycle, not the evidence | Record the promise under the Expectation risk category. The implementation lead resets it at kickoff against the readiness level and the typical timeline |
| The Implementation Profile is blank and go-live is needed | The team has not yet run the Implementation Profile interview | Write go-live as `[RECORD]`, state that the profile holds no typical duration, and ask the user to run the CUSTOMIZE interview. Do not estimate |

---

## Best Practices

- **Run The Check Before The Signature, When Possible.** Gaps found early give sales time to close them.
- **Capture The Volume Baselines.** They become the success measure after go-live.
- **Introduce The Implementation Team During The Sale.** The best handoffs start before the contract is signed.
- **Be Honest About The Score.** A Red score that surfaces the risk early is worth more than a Green score that hides it.
- **Do Not Skip The Technical Assessment.** Integration is the most common cause of delay, so the Technical row is always scored.
- **Verify The Champion.** Do not assume the sales champion will be the implementation champion.
- **Treat Change Management As A Risk.** Team resistance stalls more implementations than the technical work does.

---

## Integration With Other Skills

**Reads From `gtm-meddpicc-analysis` (09), By These Field Names:**
- `meddpicc_scores`: the eight elements, used as evidence for Stakeholder and Change Management
- `health_score`: the deal health read, shown beside the readiness score
- `stage_minimum_met`: whether the Stage 5 to 6 gate's handoff plan requirement is met
- `stage_recommendation` (ADVANCE, HOLD, DOWNGRADE or DISQUALIFY): a HOLD or a DOWNGRADE means the check runs as a preview and no handoff is issued. A check before signature is a preview, and no handoff is issued until the signature, whatever the recommendation. When no stage_recommendation is on record, the check is a preview too
- `risk_patterns`: the recurring deal risks, carried into the Risk Categories as evidence

**Hands To The Implementation Lead, Outside The Library, By These Field Names:**
- `readiness_score` (0 to 100) with its level
- `dimension_scores` (the six scores)
- `three_dates` (kickoff, go-live and Full Adoption Date, each with its arithmetic)
- `risks` (the top three, each with a mitigation)
- `quick_wins` (week one, month one and the 90-day criteria)

**Hands To Wrap-Up, By These Field Names:**
- `next_action` (owner and date)
- `report_path` (`none (inline)` unless a file was written)
- `readiness_score` as the score the session produced for the account

### Chains

- **Close And Hand Off:** MEDDPICC Analysis (09), **Sales Hand-Off (14)**, Wrap-Up (O10). This skill adds the readiness score and the three implementation dates the implementation lead plans from.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name, to take the implementation timeline and the quick wins into its case. This skill is free and works without any kit. The fields the kit reads from this skill:

- `three_dates` (kickoff, go-live and Full Adoption Date)
- `quick_wins` (week one, month one and the 90-day criteria)
- `dimension_scores` (the six readiness scores)

---

## Changelog

### 2.1.14 (2026-10-27)
- The shared contract's Champion Tests section now defines "creates urgency" (a dated deadline the decision works to, with its date and source on record) and "defends the solution" (a recorded case of arguing for us in our absence to someone who decides), and says a test not yet run is never scored.

### 2.1.13 (2026-10-26)
- Severity. A data gap with no named data owner is MEDIUM, because it moves a date and its first mitigation step names the owner. It is HIGH only under the IT or sponsor test, or when it is a reason kickoff is held. The Data row of Risk Categories now names the Data Owner as its first mitigation step.
- Export format. A new format needs no profile value, because it subtracts nothing.
- Bundling. The asks in the next action are the asks for the top three risks. A fourth-ranked risk's ask is a later step.
- Example 1 and the try-it. The next action asks Ruth Ellery, in risk order, for the IT owner, the chair with the sponsor in writing, and two or three power users for the pilot, by 2026-11-09. The Adoption mitigation names the power users. Risks, ranking, dates and scores do not change.

### 2.1.12 (2026-10-26)
- Next action. The Output Contract row and Step 7 give the order: a reply owed to a buyer, then the ask that mitigates the top-ranked risk needing a buyer-side person, then the next-ranked one, then our team's own steps. Asks of the same kind to the same person on the same date travel in one message, in risk order.
- Examples. Each example's next action follows that order. Technical is the top-ranked risk in all three, so the IT owner ask leads. The sponsor and board chair ask goes to the same person on the same date and travels with it. Example 3 (the 40 Orange case) changes from the board date alone to the IT owner, the board date and the chair and sponsor, in one message.
- Dates and scores do not change. The composite, dimension scores, three dates, risks and Preview label are as before.
- Try-it. The promise names the IT owner ask first and the same-message sponsor ask, with later steps listed.

### 2.1.11 (2026-10-26)
- Source Systems. With one system no adjustment applies, and no profile value is needed. A profile value is required only for an adjustment that applies.
- Export format. A vendor's confirmation is not the team's familiarity. The format counts as new until the team has worked with it.
- Kickoff. Kickoff is the check date, plus the buffer, plus the IT lead time when no IT owner is named on the check date.
- Composite and ranking. The composite line states that its weights are decimals. The risk keys are a numbered list, and row order breaks only a tie on all three keys.
- Preview. Before signature the three dates are labelled proposed and the report carries the Preview label. Example 1 states this, and its plot-record fact is tagged to the call that holds it.

### 2.1.8 (2026-10-26)
- Round 8 citation and status pass. Every profile citation is now written (profile: Section). The 49 day and 14 day Implementation Profile values keep their illustrative mark, because the profile marks them that way.
- An ENGAGED rule is added to Output Contract and to Step 1. An ENGAGED or INBOUND account with no deal open gets a gap list in place of three dates, a composite and a Preview. Quick Reference names that case as a don't-use.
- Every example and try-it record was checked against its run date. Each cast account reads ACTIVE on its run date, so no record needed a relabel and no example output changed.
- Headings and labels are capitalized word by word.

### 2.1.7 (2026-10-26)
- Round 7 scrub. The rules no longer carry a worked date, a worked score or a quoted record phrase. The Technical cap under constrained IT, the Workflow partial baseline, the Change Management skeptic, the ranking keys and the composite rounding each state the general test.
- The Preview and handoff distinction is written into the Output Contract: a run before the signature is a Preview, and only a run after the signature is a handoff.
- A format the team has not yet seen counts as new in the Full Adoption Date adjustments.
- The example's next action takes the shared rule's date when the record holds no agreed date. The try-it record states facts only, and the to-try pointer no longer names an example.

### 2.1.6 (2026-10-26)
- The Technical score follows the constrained-IT rule where one known source system has no IT owner named. The Orange rule governs the dates in the example that sits in that band: no date is set, and conditional dates are anchored on the readiness check date.
- The IT owner date in the second example's conditions matches its next action.
- The adoption risk likelihood in the first example is High, because the record shows the skepticism.
- The chair decision wording follows the family's vote. The "ready to sign" statement is labelled a claim, since no dated record holds it.
- The buyer-contact wording in the third example names the contact who has replied since 2026-10-03.
- Call-sourced facts in the examples carry their call dates. Each bare call tag is dated to the call that holds the fact, and a call with no date on record is written `[Call, date Unknown]`.

### 2.1.5 (2026-10-26)
- The invented CRM dated-action context line of the third run is removed, and its next action and the IT-owner dates in the second run carry the shared rule's dates.
- The CUSTOMIZE interview asks for the IT lead time in days, the unit the profile and the skill use.
- The next action follows the family's one deadline rule. The Output Contract points to that rule, and each example names the record behind an earlier date.
- The IT-owner condition and its risk mitigation in Example 2 move with the recomputed next action, so the three dates and the conditions still agree.
- The three dates, their arithmetic and the Yellow and Orange rules are unchanged.

### 2.1.4 (2026-10-26)
- Try-it fixes from the blind retest. The composite formula states its weights as decimals, so it reads 0 to 100. The Yellow kickoff window is the buffer, and the IT lead time comes after it. A Yellow report with a critical dimension lists its conditions before kickoff. All three dates are labelled proposed before signature. Severity and likelihood follow stated rules, and each top risk states both. A check before signature is a preview. The next action names the action the owner takes. The worked examples show the date arithmetic and the likelihood of each risk.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1, with one approved output change: the three dates now use the profile's typical days (49, illustrative) and IT lead time (14 days, illustrative). Example 1 dates now follow the profile's typical days and IT lead time, with the arithmetic shown in the example. The provisional label and the [RECORD] wording are removed from the dates. Example 2 and the try-it records follow the same arithmetic. Added rules: the Yellow buffer default of three weeks, the IT lead time on top of the buffer and read on the check date, the preview scope before signature, the top-three ranking, the partial Workflow baseline, and the constrained IT case for Technical.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. The Unknown Rule is added: a dimension with no evidence is INSUFFICIENT, the composite re-weights over the scored dimensions and reads with its scored count, and fewer than five scored dimensions gives no composite. Stakeholder is added as a Risk Categories row, which the example's top risk now uses. Example 1 shows the stakeholder map, the workflow baseline, the technical rows, the checklist, and the stated plan and agreed date behind its dates.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1.

### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`) and offers read-only CRM connectors through the shared contract's Knowledge Base and Connectors section, before the CRM read.
- Adds a Chains subsection placing the skill in the Close And Hand Off chain.
- Adds a Guild Pro Kits subsection naming the hand-off fields the Business Case & ROI Kit reads.

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, a Produces line on every Core Workflow step, Epistemic Rules, Hard Rules with reasons, and a Quality Bar.
- Added the Implementation Profile section as the source of the timing values: typical days from kickoff to go-live, how data moves, the source-system, export-format and IT-lead-time variables, the default months to full adoption, and the team's quick win types. The skill ships those values blank.
- The three dates are now kickoff, go-live and Full Adoption Date, the names the hand-off fields carry. The signature is the handoff trigger. Every date shows its arithmetic, and the weekend roll is stated.
- Step 1 reads Product Modules. The "product benchmarks" reference is now the Implementation Profile.
- The stakeholder role table gains a "Who Usually Fills It" column. Quick Win Types is a starting catalog of four, each with a generic example.
- The readiness card is seven of the nine report sections, written only when the user asks for the file. The card is no longer a separate artifact section.
- The evidence labels are replaced by the six shared tags. The examples sit on the PlotIQ chain, and every example shows all six dimension scores with its weighted table.
- The Yellow buffer is anchored to the readiness check date, which the chain's dates rely on.

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around the retired legal-ops case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose
- Profile section names aligned with the template (Core Pain Points, Product Modules)
- Third handoff date renamed "Full Adoption Date" (was "Full Service Date")

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (6 Readiness Dimensions, Stakeholder Roles taxonomy, Technical Assessment, Risk Categories, 3-Date Plan structure) moved to an explicit Methodology section (`{Methodology: X}` references)
- No functional changes to the workflow, scoring rubrics, or readiness assessment logic

### 1.0.0 (2026-03-04)
- Initial release: migrated from customer readiness index
- Generalized via Client Profile block with configurable defaults
- Preserved 6-dimension readiness scoring with weighted composite (1-5 scale, 0-100 composite)
- Preserved 3-date handoff plan (signing, implementation start, full adoption, +2 months rule)
- Preserved technical assessment dimensions (source system, integration, data quality)
- Preserved implementation stakeholder role taxonomy
- Preserved quick win types and risk categories with mitigation strategies
- Added Implementation Profile and Product Modules to Client Profile
- Multi-format artifact generation replacing reportlab-only
