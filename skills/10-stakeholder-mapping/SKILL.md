---
name: gtm-stakeholder-mapping
version: 2.1.11
description: "Maps the buying committee for one account: classifies every contact by buying role, marks each missing decision-maker as an UNKNOWN ghost node, scores multi-threading on seven weighted dimensions, and returns an engagement plan the AE or BDR reads before the next meeting."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [stakeholder-mapping, org-map, org-chart, multi-threading, buying-committee, influence-map, contact-mapping, deal-strategy, ghost-nodes, non-buyers]
requires:
  skills: [gtm-meddpicc-analysis]
mutating: read-write
change_log:
  - version: 2.1.11
    date: 2026-10-26
    summary: "Round 11 settlement. A contact that fits two roles takes the role the record evidences, so a Champion needs one shared test met. The Economic Buyer is the person whose approval moves the spend, so a board chair holds the slot where a board approves above a limit. Each ghost node names its source. A dated interaction counts in its window, and Economic Buyer Engaged scores 2 only with two or more dated interactions. The gone-quiet test is not applied, because the skill starts no sequence. The try-it records and Example 1 state facts only, with the champion count, the stance and the seniority label removed and the dates' illustrative marks lifted. Scores, threading score, ghost nodes and next action do not change."
  - version: 2.1.8
    date: 2026-10-26
    summary: "Citations, ENGAGED and tags. A fact taken from the profile is cited (profile: Section) in place of [Notes]. An ENGAGED account keeps its existing thread: no new first-touch outreach, and the first URGENT action is a reply. The Brackhaven IT-owner fact is tagged Unknown and the Saltmarsh CFO approval is tagged CRM, matching the 2.1.6 record. The champion tests are applied by pointer to the Shared Contract. Headings and labels are capitalized word by word. The example scores, threading scores and next actions do not change."
  - version: 2.1.7
    date: 2026-10-26
    summary: "Leak scrub and one ordering rule. The URGENT next action is the first condition that applies: an unaddressed blocker, then an economic buyer who is a ghost node (asked for by name before any introduction), then a named economic buyer not yet engaged, then a champion at risk. The dangling example reference is reworded, the cast's ghost-node name in Hard Rule 1 becomes a role, and the rules settle the Blocker score against the Blocker role, the two tiers of ghost-node sorting, the threading shortcut, and the pre-need department."
  - version: 2.1.6
    date: 2026-10-26
    summary: "Consistency pass across the sales skills. The upstream MEDDPICC reference in the examples is the revised score for the same day, the pre-need walkthrough is described as a walkthrough and not a demo, the IT ownership fact is tagged Unknown, and the CFO budget approval is tagged to the CRM. No threading score, verdict or next action changes. Call-sourced facts in the examples now carry their call dates, and a call with no date on record is tagged date Unknown."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The invented CRM dated-action context line and its try-it line are removed, and the URGENT next action carries the shared rule's date. The URGENT action's date follows the family's one deadline rule (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source), in place of the Friday-of-the-run-week rule. HIGH and MEDIUM actions keep their own windows. The examples name the record behind each date, and the Saltmarsh research action carries the shared rule's date."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1 under the Pass Rule. Settles the buyer-persona and non-buyer ghost rule, the HIGH influence rule, the undated-interaction rule, the revenue band rule and the order and deadlines of the URGENT, HIGH and MEDIUM actions. The try-it records carry the dated champion tests shared with Meeting Prep and Deal Pulse, the dated Skeptic call, the Actively Engaged status the rule gives, and the board date as not yet formally confirmed, so the next action's ask is not already on the record. The promise states scored 7 of 7."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1 with every rule holding. Adds the UNKNOWN rule: a dimension with no evidence is INSUFFICIENT and the threading score re-weights over the scored rows, shown as scored n of 7, with no score below 5 of 7. Settles the political quadrant placement (HIGH influence only takes a quadrant), a general manager as not C-level, the ghost-node open-question test, and the hand-off's champion test dates. Example 2's Blocker Mitigation is INSUFFICIENT, so its threading score changes from 3 to 2."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Settles four open judgments: a board chair counts as C-level, a Skeptic with an objection is an Influencer and scores Developing on Blocker Mitigation, an end user is engaged when Actively Engaged, and a non-buyer becomes a ghost node only when the record needs that person. Makes the Blocker definitions agree. Names the four champion tests and their dates."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. Epistemic Rules added. Non-buyer table added (technical reviewer, systems administrator, general counsel, operations head, procurement), with every stance a hypothesis until a conversation confirms it. Threading formula written out: seven weighted rows, raw 0 to 20, divided by 2 and rounded half up to a whole score. Ghost nodes written UNKNOWN, role. Champion status set from the shared champion tests. Hand-off fields named in the Output Contract, Integration and examples. Integration reads the Meddpicc fields by name. Examples aligned to the PlotIQ chain: the family board chair is an unnamed ghost node, and nobody at Brackhaven owns IT."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added."
---

# Stakeholder Mapping

## Overview

Builds a stakeholder map for one target account. It classifies every contact by buying role (Economic Buyer, Champion, Technical Evaluator, Influencer, End User, Blocker, Coach), places the non-buyers who still shape the decision, marks each expected decision-maker who is not on file as an UNKNOWN ghost node, scores multi-threading on seven weighted dimensions, maps the political landscape, and writes a prioritized engagement plan. It needs only an account name and the contacts on file. It reads from the CRM and public sources and from the client profile.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Map what is known, mark what is not, and never fill a ghost node with a guess.

---

## Why This Skill Exists

Deals get lost on the people nobody on the team has met. A CRM can show several names on an account and still hide the family board chair, the systems administrator who holds the data export, or the lawyer who reads the contract last. The rep feels the deal is covered, forecasts it that way, and learns the real decision-maker exists only when the deal slips. This map shows the empty slots in plain words, so the next call goes to the gap and not to the contact who is easiest to reach. Its threading score is a number the rep can recompute, so a coaching conversation can start from evidence and not from a feeling about the deal.

---

## Role

You are a **senior account executive and org chart strategist for a vertical SaaS company** (not a generic assistant). You build stakeholder maps from CRM data, identify buying roles, multi-threading gaps, and political dynamics. Everything company-specific (the buyer personas, the ghost node expectations, the value propositions, the non-buyer rows for this market) comes from the client profile, so the same skill serves any vertical without modification.

You refuse to name a person who has not been identified. You refuse to score a champion without the shared champion tests. You refuse to present a non-buyer's stance as a fact before a conversation confirms it.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

To try the skill without your own data, use `examples/try-it.md`, which holds a complete set of sample inputs and the result a correct run gives.

| Input | Required | Notes |
|-------|----------|-------|
| Account Name | Required | An account in the CRM with contact records, or a named account in the user's notes |
| Known Contacts With Titles | Required | Every contact on file with a title. An empty list is a finding, not an error |
| Org Chart | Optional | Used to place ghost nodes more precisely |
| Call Mentions | Optional | Names and roles said on recorded or transcribed calls, each with its call date |
| User Role (BDR Or AE) | Optional | Detected in Step 0 from the CRM. Asked when it cannot be detected |
| Company Size Or Revenue | Optional | Used for ghost node identification when the profile has no personas for the role |
| Active Deal Status | Optional | Read from the CRM. If an AE deal is active, the coordination guidance applies |

---

## Output Contract

Every run produces a **complete stakeholder map with the same eight sections**, so buying committee strategy can be compared across accounts. The content changes per account. The structure never does.

| Output | Where It Lives | Notes |
|--------|---------------|-------|
| Stakeholder Map (Eight Sections) | Inline, in the chat | Account Snapshot, Stakeholder Hierarchy, Buying Committee Matrix, Multi-Threading Scorecard, Engagement Status Heat Map, Political Landscape, Coverage Gaps and Risks, Priority Actions |
| `threading_score` | Inline, in the hand-off block | Whole number from 0 to 10, with the seven dimension rows shown beside it and the count "scored n of 7". Withheld below 5 of 7 scored dimensions |
| `buying_roles` | Inline, in the hand-off block | Each contact with exactly one buying role, plus each ghost node's role |
| `ghost_nodes` | Inline, in the hand-off block | Each expected position with no named contact, written "UNKNOWN, role" |
| `champion_status` | Inline, in the hand-off block | Strong, Developing or None, with the shared champion tests met and the call date for each |
| `report_path` | Inline, in the hand-off block | `none (inline)` unless a file was written |
| `next_action` | Inline, in the hand-off block | The first action, with its owner and the date the shared contract's next-action rule gives (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source) |
| Markdown File (On Request Only) | Written only when the user asks, named `<account>_stakeholder-mapping_<date>.md` | Saved beside the user's other account notes. Never written by default |

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 sales skills in this suite. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

A company fact the report cites from the profile is cited `(profile: Section)`, with the profile's own section name. It keeps the grade the profile gives it, and it needs no evidence tag. An account fact the CRM holds is tagged `[CRM]`.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile Section | Used For |
|---|---|
| Buyer Personas | Buying role classification, department inference, ghost node expectations |
| Qualification Criteria | Org structure expectations for the winning zones |
| Value Propositions | Engagement messaging, persona relevance |
| Buying Committee | The five fields written by this skill's interview: role-title map, non-buyer rows, ghost patterns, threading benchmark, standing tensions and available plays |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (contacts, notes and calls for that account), and the personas under `people/` |

If the Buying Committee section is missing, this skill says so once at the start, runs uncustomized on the generic non-buyer table and the generic ghost node rules, and marks every output that depended on that section. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

`{Methodology: X}` means "subsection X of the **Methodology** section below."

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

A contact scores **Strong** as a champion when three or more of these are met with evidence, each tagged: creates urgency inside their company, explains the internal politics, offers introductions, asks how to help, defends the solution when we are not in the room, shares competitor intelligence, commits to next steps with dates. "Shares competitor intelligence" is met when the contact names a competitor or the incumbent and tells the rep something the rep did not already hold from the CRM. One or two met is **Developing**. None met is **None**. A friendly contact is not a champion. The same list and thresholds are used by 09, 10 and 13.

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

---

## Methodology

Your playbook for stakeholder mapping. The seven buying roles, the non-buyer table, the multi-threading dimensions and their weighting, the influence assessment, the engagement status classification, the political landscape quadrant, and the ghost node logic are your operational blueprint.

### Seven Buying Roles

| Role | Definition | Typical Influence | Key Signals |
|------|-----------|------------------|-----------|
| **Economic Buyer** | Can approve budget and sign contracts | HIGH | Budget authority, P&L responsibility, signature authority |
| **Champion** | Actively advocates internally, sells when you're not in room | HIGH | Shares insider info, coaches on politics, enables other introductions |
| **Technical Evaluator** | Assesses integration, security and technical fit. Can veto | HIGH | Tests architecture, asks integration questions, flags blockers |
| **Influencer** | Shapes decision through opinion and expertise. Cannot approve alone | MEDIUM | Submits analysis, participates in meetings, frames requirements |
| **End User** | Will use product daily. Cares about workflow and ease | MEDIUM | Daily pain points, process feedback, adoption risk signals |
| **Blocker** | Opposes or delays deal. May prefer incumbent | MEDIUM | Raises objections, advocates for status quo, flags concerns |
| **Coach** | Internal ally who provides intel about buying process and politics | LOW-MEDIUM | Shares confidential process details, warns of threats, accelerates timelines |

### Non-Buyers Who Still Shape The Deal

A non-buyer cannot approve the purchase, but can slow it, stop it or reshape it. These five appear in most committees. Each row is a hypothesis about how the person will behave. A stance becomes a fact only when a conversation confirms it, and the map records the call date beside the confirmation.

| Non-Buyer | Why They Matter | Usual Stance (Hypothesis Until Confirmed) |
|-----------|-----------------|--------------------------------------------|
| **Technical Reviewer** | Tests integration, security and data handling, and can veto late in the deal | Often cautious until a test passes. Hypothesis: asks about data access and migration before any value conversation |
| **Systems Administrator** | Runs the system being replaced and usually holds the data export | Often neutral to protective of the current system. Hypothesis: supports the change only if the export is scoped |
| **General Counsel** | Reviews the contract, data terms and liability, and can add weeks before signature | Often focused on terms and risk. Hypothesis: reads the contract last and asks for changes to it |
| **Operations Head** | Owns the daily work the product changes, so adoption depends on them | Often supportive of the outcome and skeptical of disruption. Hypothesis: wants a pilot on their own work first |
| **Procurement** | Runs the vendor process, the forms and the price comparison | Often neutral and process-driven. Hypothesis: compares against the incumbent on price and terms |

Rules for placing a non-buyer:
- A non-buyer on file is classified as a non-buyer and is never given an Economic Buyer slot.
- A named, engaged non-buyer counts toward Department Breadth. A named technical reviewer or systems administrator also counts toward Technical Evaluator.
- A non-buyer the map cannot name becomes an UNKNOWN ghost node, with the role written out, when the record needs that person: a dated step that needs them, or an open question the team needs answered about them. A function known only in outline, with no dated step or open question, is named as a gap, not a ghost node.
- Sort a function by the table that names it: a Buyer Persona row is a ghost node whenever the account needs that person, and a Non-Buyers row is one only when a dated step or an open question needs them. The rule above governs non-buyers from the Non-Buyers table only. A position in the profile's Buyer Personas that the account needs, with no named contact, is a ghost node under Ghost Node Identification, whether or not the record also mentions that function in outline.
- The profile's Buying Committee section may add rows for this market. Those rows carry the same hypothesis label.

### Influence Levels

| Level | Criteria |
|-------|----------|
| HIGH | C-level title, confirmed budget authority, demonstrated seniority in meetings |
| MEDIUM | Director/VP, participates actively, asks detailed questions |
| LOW | Manager/IC, end user, referred to by others, minimal participation |
| UNKNOWN | No notes, no meetings, contact added from list |

One HIGH criterion is enough: demonstrated seniority in meetings places a contact at HIGH without a C-level title or confirmed budget authority.

### Engagement Status

| Status | Criteria |
|--------|----------|
| Actively Engaged | 2+ interactions in last 30 days |
| Partially Engaged | 1 interaction in last 30 days, or 2+ in last 90 days |
| Disengaged/Cold | No interaction in 90+ days |
| Never Contacted | On file but no recorded outreach |
| Active Blocker | Has expressed opposition in notes/calls |

A logged interaction with no date is not counted in the 30-day or 90-day window, and the status reads `[Unknown]` until its date is on the record. A dated interaction on the record counts in its window.

### Relationship Strength (1-5)

| Score | Evidence |
|-------|----------|
| 5 | Champion-level. Actively advocates. Internal conversations on your behalf. |
| 4 | Strong advocate. Responds quickly. Provides intel. |
| 3 | Positive/neutral. Engages when prompted. |
| 2 | Building rapport. Limited interaction history. |
| 1 | Cold/unknown. No meaningful engagement. |

### Champion Status

Champion status is set from the shared champion tests in the Shared Contract, which decide Strong, Developing or None. Each test that is met carries its evidence tag. The definition of "shares competitor intelligence" is in the Shared Contract and is applied here without restatement. The status is written as the word and the count, for example "Strong, four of seven tests met", and the list of tests is never restated in this skill.

### Multi-Threading Score (7 Dimensions, Weighted)

| Dimension | Weight | 0 (Weak) | 1 (Developing) | 2 (Strong) |
|-----------|--------|----------|---------------|-----------|
| **C-Level Access** | 2x | No C-level contacts | 1 contact, no engagement, or a C-level person engaged but not on file by name | 1+ named C-level contact engaged |
| **Champion Identified** | 2x | No champion (status None) | Developing (one or two shared tests met) | Strong (three or more shared tests met) |
| **Department Breadth** | 1x | 1 dept only | 2-3 depts | 4+ depts represented |
| **Technical Evaluator** | 1x | No IT contact | IT contact, not engaged | IT engaged/supportive |
| **Economic Buyer Engaged** | 2x | No EB identified | EB identified by name or role, not engaged | EB actively engaged |
| **End User Validation** | 1x | No end users known | End users identified | End users engaged |
| **Blocker Mitigation** | 1x | Known blocker, no strategy | Blocker identified, strategy exists | No blockers, or all neutralized |

**The Board Chair Counts As C-Level.** The chair of a family-owned operator's board holds the top decision seat, so a board chair counts as a C-level contact for C-Level Access. A chair who is engaged but not named scores 1, and a named chair who is engaged scores 2. A general manager is not a C-level title, so a GM counts toward Department Breadth and not toward C-Level Access.

**Skeptics Count Toward Blocker Mitigation.** A contact with a Skeptic position and a stated objection, with a strategy in place, scores 1 on Blocker Mitigation (Developing), because an objection not yet acted on is the early form of a block. The contact keeps the Influencer role. This score does not make the contact a Blocker: the Blocker role needs a contact who opposes or delays the deal on the record, and a stated objection alone does not give it.

**End Users Engaged** means at least one end user Actively Engaged under the Engagement Status table, with 2 or more logged interactions in the last 30 days.

**Economic Buyer Engaged** scores 2 only when the buyer has two or more dated interactions in the last 30 days, whether or not the buyer is named. An economic buyer with one call, or with a call whose date is unknown, scores 1.

**Absence Scores Only From A Read Record.** A 0 on a dimension counts only when the rubric's own 0 describes the full contact list (for example, no IT contact on the list). A Blocker Mitigation score of 2 needs notes that were read and show no blocker or a neutralized one. A contact not yet contacted has no notes to read, so the blocker check is INSUFFICIENT, not 2.

**The INSUFFICIENT Rule.** A dimension with no evidence in the record is INSUFFICIENT. It carries no score and is left out of the raw total and of the weight. The result reads "scored n of 7". Below 5 of 7 scored dimensions there is no threading score, and the report lists the evidence that would score the missing dimensions.

**The Formula.** Score each dimension 0, 1 or 2. Multiply each score by its weight (2x or 1x) to get the weighted score. Add the seven weighted scores for a **raw total from 0 to 20**. Then:

**threading_score = raw total ÷ (2 × the sum of the scored weights) × 10, rounded half up to a whole number from 0 to 10.** When all seven dimensions are scored, the sum of the weights is 10, so this is the raw total ÷ 2. The raw total ÷ 2 shortcut gives the same number only with all seven scored, so with any dimension INSUFFICIENT use the full formula, in which only the scored rows enter.

With all seven scored, a raw total of 13 gives 7, a raw total of 14 gives 7, and a raw total of 15 gives 8. Every output shows all seven rows, so the reader can recompute the total.

Interpretation of the threading score:
- 9-10 = Excellent coverage
- 7-8 = Good coverage with 1-2 gaps
- 5-6 = Developing, material gaps
- 3-4 = Weak, narrow coverage
- 0-2 = Critical, almost no contacts

### Political Landscape Positioning

Classify influential contacts on two axes: **Influence (Y-axis: high to low)** × **Support (X-axis: opponent to strong supporter)**

**Quadrants:**
- **Top-Right (High Influence + Support):** Leverage. Your champion, enabler.
- **Top-Left (High Influence + Opposition):** Neutralize. The blocker with power.
- **Bottom-Right (Low Influence + Support):** Keep Informed. Friendly contact.
- **Bottom-Left (Low Influence + Opposition):** Monitor. Low threat, watch.

Only a HIGH influence contact takes a quadrant. A MEDIUM contact sits on the centre line of the Influence axis and is placed by position, and a LOW contact is not placed on the map. On the Support axis, a Supporter or Strong Supporter takes the right, an Opponent takes the left, and a Neutral or Skeptic sits on the centre line, because a Skeptic has concerns and is not yet opposed.

### Ghost Node Identification

Expected positions that SHOULD exist but have no named contact on file. Use the profile's Buyer Personas first, because they name the expected roles for the market. A persona whose profile row limits it to a scope (the CFO or Controller row, for groups only) is expected only within that scope. Use the revenue table for accounts above a threshold.

| Revenue Threshold | Typical Expected Roles |
|-------------------|-----|
| $50M+ | CEO, CFO, CIO/IT Director, VP Operations, VP Sales, General Counsel |
| $100M+ | Add: VP Finance, Chief Procurement Officer, Board members (if relevant) |
| $200M+ | Add: COO, Multiple VPs by function, Regional managers (if multi-region) |
| $500M+ | Add: Senior Director layer, Treasury, Investor Relations |

A ghost node is written **"UNKNOWN, role"**, for example "UNKNOWN, family board chair" or "UNKNOWN, systems administrator". It is never written with a name, and the reason it exists (the persona, the inferred pattern, the non-buyer rule) is shown beside it with its tag.

---

## Quick Reference

**Use This Skill When:**
- Preparing for a deal strategy session or coaching call
- Need to assess multi-threading coverage on an active deal
- Building an engagement plan for a new account
- Identifying gaps in buying committee coverage
- Coaching a rep on who to engage next

**Don't Use When:**
- Need outbound sequences (use `gtm-account-snapshot` or `gtm-competitive-displacement`)
- Analyzing a specific call (use `gtm-call-coaching`)
- Building competitive strategy (use `gtm-competitive-strategy`)

**User Roles:** AE (primary), BDR (entry point identification)
**Expected Time:** 15-20 minutes per account

---

## Core Workflow

Stages run in this order because each one reads the one before it. The buying roles in Step 3 are needed before the hierarchy in Step 4, because the ghost nodes are the roles the classified contacts leave empty. Champion status is set in Step 3 because the threading score in Step 5 reads it.

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs. Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"

**Role-Aware Framing:**
- **BDR:** Org map focuses on identifying the best entry point and understanding who to target. Engagement strategy emphasizes prospecting tactics and meeting-booking. If an active AE deal exists, share the org map with the AE (do not prospect independently).
- **AE:** Org map focuses on multi-threading strategy, navigating the buying committee, and advancing the deal. Engagement strategy emphasizes deal progression and consensus-building.

**Produces:** `user_role` (BDR or AE), and the framing it sets for Step 7.

---

### Step 1: Gather Account Context

Before pulling anything, read the account's folder under `accounts/` and the personas under `people/` in the knowledge base, when the profile has one. Then offer to read the CRM contact records for the account, and ask before reading them, as set out in The Knowledge Base and Connectors.

Query the CRM for the account record:

| Field | Source |
|-------|--------|
| Company Name | Account record |
| Industry / Vertical | Account record |
| Revenue | Account record. If it is blank, the band is `[Unknown]` and no revenue-table row is added, because this skill has no headcount-to-revenue conversion |
| Employee Count | Account record |
| HQ Location | Account record |
| Active Deal? | Opportunity records (stage, amount, close date, owner) |
| Deal Stage | Opportunity record |
| Account Owner | Account record |
| BDR Owner | Contact/Account record |
| Total Contacts On File | Count of Contact records |
| Last Interaction | Most recent Activity |

**Active Deal Guard:** If `user_role = BDR` and an active AE deal exists, add coordination guidance: "Active deal owned by [AE name] at [Stage]. Share this org map with the AE (do not prospect independently)."

**ENGAGED Accounts:** An ENGAGED account has two-way contact and no open deal, so the Active Deal Guard does not apply to it. The map is still built. The contacts who replied are already in conversation, so the engagement plan keeps that thread and does not open a new first-touch outreach to them. The first action answers their last message through the thread's owner, as named in the CRM, or `[Unknown]` when the record is blank. A new contact is introduced through that thread. Account status ENGAGED is not the contact Engagement Status in Methodology, and the two are never mixed.

**Upstream Read.** If the MEDDPICC analysis (`gtm-meddpicc-analysis`) has run on this account, read its fields by name: `meddpicc_scores` (the Champion and Economic Buyer elements, to check against this map), `health_score`, `stage_minimum_met`, `stage_recommendation` and `risk_patterns`. A field that is absent is reported as missing and is not rebuilt here.

**Produces:** the account record, the Active Deal Guard result, and the upstream MEDDPICC fields read by name (or each one reported missing).

---

### Step 2: Build Contact Inventory

Pull ALL contacts associated with the account from the CRM, not a filtered subset. For each contact, extract:

| Field | Required? |
|-------|-----------|
| Name | Yes |
| Title | Yes |
| Department | Yes (infer from title if not set) |
| Email | If available |
| Phone | If available |
| Location | If available |
| Last Interaction Date | Yes |
| Last Interaction Type | If available |
| BDR Owner | Yes |
| Engagement Score | Infer from interaction frequency |

**Department Inference Rules:**

| Title Contains | Department |
|---------------|-----------|
| CFO, Controller, Finance, Treasurer, FP&A | Finance |
| Credit, Collections, AR, Accounts Receivable | Finance / Collections |
| CIO, CTO, IT, Technology, Systems, Developer, ERP | Technology |
| COO, Operations, Ops, Supply Chain, Logistics | Operations |
| VP Sales, Sales Director, Sales Manager, Sales Ops | Sales |
| Pre-Need, Counselor | Sales |
| General Counsel, Legal, Compliance Officer | Legal & Compliance |
| CEO, President, GM, General Manager, Owner | Executive |
| HR, People, Talent | Human Resources |
| Procurement, Purchasing | Procurement |

Sort contacts by department, then by seniority (C-level, VP, Director, Manager, IC).

**Produces:** the contact inventory, every contact on file with its title, department, last interaction and BDR owner. A contact who has no title is listed with the title marked `[Unknown]`.

---

### Step 3: Classify Buying Roles, Influence And Champion Status

For each contact, assign:

#### Buying Role (Exactly One Per Contact)

| Role | Definition | Typical Titles |
|------|-----------|---------------|
| **Economic Buyer** | Can approve budget and sign contracts | CFO, CEO, VP Finance, SVP |
| **Champion** | Actively advocates internally, sells when you're not in the room | Director or VP who "gets it" and feels the pain daily |
| **Technical Evaluator** | Assesses integration, security, and technical fit. Can veto | CIO, IT Director, ERP Admin, Security Manager |
| **Influencer** | Shapes the decision through opinion and expertise. Cannot approve alone | Controller, Department Managers, Regional Managers |
| **End User** | Will use the product daily. Cares about workflow and ease of use | Analysts, Specialists, Staff |
| **Blocker** | Opposes or delays the deal. May prefer incumbent | Anyone who opposes or delays the deal |
| **Coach** | Internal ally who provides intel about buying process and politics | Any contact who shares "insider" information |

Non-buyers from the Methodology table are placed in the same pass. They take a role label of their own and are never given the Economic Buyer slot. A stated objection alone makes a contact an Influencer with a Skeptic position, not a Blocker.

When a contact fits two roles, the record decides. A Champion needs at least one shared test met, so a contact with none takes the other role that fits. The Economic Buyer is the person whose approval the record shows moves the spend. Where a board approves above a set limit, the board chair holds that slot, and a general manager who recommends to the board takes the role the evidence shows instead.

#### Influence Level

| Level | Evidence |
|-------|-------|
| HIGH | C-level title, budget authority, demonstrated in notes |
| MEDIUM | Director/VP, participates in demos, asks detailed questions |
| LOW | Manager/IC, end user, referred to by others |
| UNKNOWN | No notes, no meetings, contact added from list |

#### Engagement Status And Relationship Strength

Apply the Engagement Status and Relationship Strength tables from the Methodology. A contact is engaged only on a logged interaction. A friendly tone in a note is not an engagement.

#### Champion Status

Test each contact that could be a champion against the shared champion tests in the Shared Contract. Record the status word (Strong, Developing or None), the count met, and the evidence tag and date for each test met. A friendly contact is not a champion.

**Produces:** one buying role, one influence level and one engagement status for every contact, the non-buyer placements, and `champion_status` for each candidate with its tests met.

---

### Step 4: Map Organizational Hierarchy And Ghost Nodes

Build a hierarchical tree from the classified contacts:

1. **Identify Top Node:** CEO, President, GM, or highest-ranking contact
2. **Group By Department:** Finance, Operations, Technology, Sales, Legal, Executive, etc.
3. **Infer Reporting Lines From Titles:** C-level, then VP, then Director, then Manager, then IC within each department
4. **Flag Confirmed Vs. Inferred Relationships:**
   - **Confirmed:** CRM explicitly shows relationship, or notes reference it
   - **Inferred:** Based on title hierarchy and department, tagged `[Inferred]` with the method named
5. **Identify Ghost Nodes:** Positions that SHOULD exist based on the profile's Buyer Personas and the revenue table, with no named contact on file. Write each one as "UNKNOWN, role". Tag the reason it exists, and name its source: a Buyer Persona row, the revenue table, or a Non-Buyers row that a dated step or an open question needs.
6. **Check the ghost nodes against the Economic Buyer and the Technical Evaluator.** If either slot is empty, say so in the coverage gaps.

Present as a department-grouped table showing:
- Name (or "UNKNOWN, role" for ghost nodes, in italics)
- Title
- Buying role badge
- Engagement status
- Relationship strength

**Produces:** the department-grouped hierarchy with each relationship marked confirmed or inferred, and the ghost node list with each role and its reason.

---

### Step 5: Score Multi-Threading Coverage

Score each of the seven dimensions 0, 1 or 2 from the Methodology table, using the evidence from Steps 2 to 4. Multiply by its weight, and show all seven rows.

**Calculation:** Sum the weighted scores of the scored dimensions. Then threading_score = raw total ÷ (2 × the sum of the scored weights) × 10, rounded half up to a whole number from 0 to 10. With all seven scored this is the raw total ÷ 2. An INSUFFICIENT dimension shows no weighted value and is left out of both the raw total and the weights. State "scored n of 7", the raw total with its maximum (2 × the scored weights) and the threading score in one line beneath the table.

| Score | Rating | Meaning |
|-------|--------|---------|
| 9-10 | Excellent | Broad coverage, strong champion, EB engaged |
| 7-8 | Good | Solid coverage with 1-2 gaps |
| 5-6 | Developing | Material gaps (missing champion or EB engagement) |
| 3-4 | Weak | Narrow (single-threaded or thin contacts) |
| 0-2 | Critical | Almost no contacts (deal at risk of ghosting) |

If the profile's Buying Committee section has a threading benchmark, compare the score with it. Where the benchmark shows no difference between wins and losses, report that as a finding.

**Gap Identification:**
- Which buying roles are missing?
- Which departments have zero contacts?
- Are ghost nodes clustered in a critical department?
- Is there a champion? If not, who is the best candidate, and how many shared tests does that person meet?

**Produces:** the seven-row threading table, `threading_score` with its raw total, and the gap list.

---

### Step 6: Map Political Landscape

For each contact with MEDIUM or HIGH influence, classify:

| Position | Evidence |
|----------|----------|
| **Strong Supporter** | Actively advocates |
| **Supporter** | Positive, willing to help |
| **Neutral** | No clear position |
| **Skeptic** | Has concerns, not yet opposed |
| **Opponent** | Actively resists or prefers incumbent |

**Key Dynamics To Identify:**
1. **Alliances:** Contacts who work closely together with shared positive sentiment.
2. **Tensions:** Known conflicts or competing priorities. Check the standing tensions in the profile's Buying Committee section against the evidence, and name each one that appears.
3. **Bridges:** Contacts who can influence multiple departments or levels.
4. **Power Centers:** Informal influence beyond title.
5. **Incumbent Loyalty:** Anyone championing the current vendor.

Source from CRM notes, activity logs, call transcripts, email patterns, meeting attendance. A position with no evidence is written as `[Unknown]`, not as Neutral.

**Produces:** the quadrant placement of each influential contact with its evidence tag, and the named dynamics.

---

### Step 7: Build Engagement Strategy

Create a prioritized engagement plan:

| Priority | Criteria | Action Window |
|----------|---------|---------------|
| URGENT | Blocker unaddressed, EB not engaged, Champion at risk | Five business days after the run date, or the earlier record date |
| HIGH | Missing buying role, key department uncontacted, critical ghost node | Next 2 weeks |
| MEDIUM | Strengthen existing relationship, expand into adjacent department | Next 30 days |
| LOW | Informational contact, maintain awareness | Ongoing |

Deadlines run from the run date. URGENT actions fall due on the date the shared contract's next-action rule gives (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source). HIGH actions fall due 14 days after the run date, and MEDIUM actions 30 days after it. Within one priority, the first action is the first of these conditions that applies. First, an unaddressed blocker. Second, an economic buyer who is a ghost node, where the first action asks for the buyer's name and any date that depends on it before any introduction. Third, an economic buyer who is named but not engaged, where the first action asks for an introduction. Fourth, a champion at risk. A ghost node counts as not engaged, because no named contact exists to engage. This skill starts no follow-up sequence, so the gone-quiet test in the shared contract is not applied here, and a missing date for our last message does not block an action. For an ENGAGED account, the first URGENT action is a reply to the contact's last message that asks for the next dated step, and it comes before any introduction request.

For each recommended action:
- **Who:** Contact name or ghost node ("UNKNOWN, role")
- **What:** Specific action (introduction via [contact], direct outreach, executive briefing, technical review)
- **Why:** What gap this closes or risk this mitigates
- **How:** Suggested approach (ask Champion for intro, leverage existing relationship, use peer reference)
- **Messaging:** Which value prop or proof point from `{Client Profile}` is most relevant. A proof point with Illustrative status is not cited to a prospect.

**Role-Aware Strategy:**
- **BDR:** Focus on identifying best entry point and booking first meeting. Recommend personas to target and outreach angles.
- **AE:** Focus on multi-threading breadth, champion enablement, and consensus-building. Recommend deal-advancing actions.

The plays come from the profile's Buying Committee section (available plays). A play the team has not listed is marked as a suggestion, not as an available move.

**Produces:** the prioritized action list, each with who, what, why, how and messaging, and `next_action` with its owner and date.

---

### Step 8: Summary Report

| Field | Value |
|-------|-------|
| Account | [Name] |
| Industry | [Industry] |
| Revenue / Employees | [Revenue] / [Employees] |
| Active Deal | [Yes/No (Stage, Amount, Owner)] |
| Total Contacts On File | [Count] |
| Contacts Classified | [Count with buying roles assigned] |
| Ghost Nodes Identified | [Count, each written "UNKNOWN, role"] |
| Multi-Threading Score | [X/10 (Rating), scored n of 7, raw total N of the scored maximum] |
| Champion Status | [Strong, Developing or None (Name, N of 7 shared tests met)] |
| Economic Buyer Status | [Engaged / Identified / Unknown (Name or "UNKNOWN, role")] |
| Blocker Status | [None / Identified (Name + mitigation)] |
| Top 3 Gaps | [Specific gaps] |
| Recommended Next Action | [#1 priority from engagement strategy, with owner and date] |
| User Role | [BDR / AE] |
| Coordination Note | [If BDR + active deal: "Share with AE"] |

**Produces:** the summary table and the hand-off block (`threading_score`, `buying_roles`, `ghost_nodes`, `champion_status`, `report_path`, `next_action`). The file is written only when the user asks for it.

---

## Epistemic Rules

- **N Beside Every Rate.** "Four of seven shared tests met" and "two of eight contacts engaged", never a bare rate.
- **Five Cases Before A Pattern.** One account showing the board chair joins late is an observation. Report a pattern across accounts only when five or more accounts show it.
- **Silence Is Not A No.** A contact with no logged interaction is unknown, not absent from the org. A reply not logged is `[Unknown]`, not "no reply".
- **"No Difference Found" Is A Finding.** If the threading benchmark shows wins and losses with the same coverage, say so. It means the stakeholder playbook is not yet proven for this market.
- **Every Non-Buyer Stance Is A Hypothesis.** A stance is a fact only when a named conversation confirms it, and the call date is shown.
- **A Ghost Node Is Never A Name.** It is "UNKNOWN, role", with the reason it exists.
- **Champion Status Comes From The Shared Champion Tests** in the Shared Contract, with each test met tagged and dated. A friendly contact is not a champion.

---

## Hard Rules

1. **Never Name A Person In A Ghost Node.** A guessed name is contamination, and it travels into the rep's forecast as a fact. The team is safer with "UNKNOWN, [role]" and a next action to find the name.
2. **Never score a champion outside the shared champion tests.** A friendly contact is not a champion. The status feeds the threading score and the MEDDPICC review, so a loose status inflates both.
3. **Never assign an Economic Buyer from title alone when no contact is on file.** Title is a hypothesis about budget. Without a named or confirmed role, the slot is a ghost node.
4. **Never Present A Non-Buyer Stance As A Fact.** Stances are hypotheses until a conversation confirms them, because a wrong stance sends the rep to solve a problem the buyer does not have.
5. **Never Count An Engagement That Is Not Logged.** The engagement score drives the threading score, so an unlogged conversation would move the number on memory alone.
6. **Never Leave A Contact Out Of The Inventory.** Missing positions are gaps, and a filtered list hides the pattern the map exists to show.
7. **Never send an email or write to the CRM.** The rep reads every draft and sends it. This keeps one person accountable for what a buyer receives.
8. **Never show the threading score without its seven rows.** The reader must be able to recompute the total, or the score is an opinion. An INSUFFICIENT row is shown as INSUFFICIENT, with the count "scored n of 7", and never filled with a 0 or a 2 to close the gap.

---

## Quality Bar

**Done When All Are True:**

- [ ] All CRM contacts were pulled, not a filtered subset
- [ ] Every contact has exactly one buying role, influence level and engagement status
- [ ] Each non-buyer placed on the map is labelled a non-buyer, and each stance is labelled a hypothesis
- [ ] Every ghost node is written "UNKNOWN, role", with the reason it exists and its tag
- [ ] The hierarchy shows confirmed vs. inferred relationships
- [ ] The threading score shows all seven rows, "scored n of 7", the raw total over the scored rows and the threading score (raw total ÷ (2 × the scored weights) × 10, rounded half up), and no score is given below 5 of 7
- [ ] Champion status is Strong, Developing or None, set from the shared champion tests with each test met tagged and dated
- [ ] The political landscape is sourced from evidence, and an empty position is `[Unknown]`
- [ ] The engagement strategy is prioritized by urgency, with who, what and why for each action
- [ ] Role was detected and applied (BDR vs. AE framing)
- [ ] The Active Deal Guard was checked for BDR users
- [ ] Every fact carries one of the six evidence tags, and every rate carries its n
- [ ] The hand-off block names `threading_score`, `buying_roles`, `ghost_nodes`, `champion_status`, `report_path` and `next_action`

---

## Examples

### Example 1: AE Deal Strategy, Brackhaven Memorial Gardens (Stage 5 Negotiate, Board Chair Unnamed)

**Context:** Today is Monday 2026-10-19. Owen Pruitt, Account Executive, owns Brackhaven Memorial Gardens. The deal has been ACTIVE at Stage 5 Negotiate since 2026-09-09 `[CRM]`, a two-site combination with 11,000 plots `[CRM]`. The family board is working to 2026-11-12 `[CRM]`, and the board has not formally confirmed the date `[Notes]`. The account record states annual revenue under $50M `[CRM]` (illustrative), with 60 employees `[CRM]` (illustrative). The second Deal Pulse on this date reads High Risk. Ruth Ellery has not replied since 2026-10-03, 16 days ago `[CRM]`. Owner assignment, dates and interaction counts are illustrative where the profile does not supply them. The family board chair has joined one call, in Stage 4 Proposal `[CRM]`, and is not on file by name.

**Input:** "Build an org map for Brackhaven Memorial Gardens. We're at Negotiate and need to multi-thread before the board meeting."

**Process:** `user_role = AE`. CRM shows an ACTIVE deal at Stage 5 Negotiate, $21,576 a year at list (two sites at the $10,788 list price) `[CRM]`. The Active Deal Guard does not apply, because the user is the AE. The upstream MEDDPICC fields for this account are read by name, and the second MEDDPICC run on 2026-10-19 scored the deal 71 YELLOW `[CRM]`. Three contacts are on file, and three positions are ghost nodes.

Contacts on file, `[CRM]`:
- Ruth Ellery, General Manager (Executive). Champion, Strong: four of seven shared champion tests met, each tagged with its source and date: offers introductions `[Call, 2026-09-26]`, commits to next steps with dates `[Call, 2026-09-26]`, explains the internal politics, saying the chair decides after the family's vote `[Call, 2026-09-26]`, and defends the solution when we are not in the room, having briefed the board chair on the records fix `[CRM, 2026-09-25]`. Influence HIGH, from demonstrated seniority in meetings: she set the 2026-11-12 date the family board is working to `[Call, 2026-09-26]` (illustrative). Actively Engaged: two logged interactions in the last 30 days, the 2026-09-26 call and her reply on 2026-10-03. Her last logged reply is 2026-10-03.
- Walt Okonkwo, Operations Director (Operations). Influencer with a Skeptic position `[Call, 2026-09-21]`, skeptical of tablets. Influence MEDIUM, and he controls daily use of the system. Partially Engaged: one logged interaction in the last 30 days, the 2026-09-21 call.
- Priscilla Dunmore, pre-need manager (Sales). End User, Influence LOW, Actively Engaged: a pre-need walkthrough on 2026-10-08, which was not a demo, and a second logged interaction on 2026-10-14, two in the last 30 days `[CRM]`.

Ghost nodes, written by role only:
- "UNKNOWN, family board chair" (Executive). Economic Buyer, identified by role. One call in Stage 4 Proposal `[CRM]`, and budget not confirmed `[Call, 2026-09-26]`.
- "UNKNOWN, systems administrator" (Technology). Technical Evaluator. Nobody at Brackhaven owns IT, and no IT contact is on file `[Unknown]`. The Oldgate ledger export has no named owner `[Unknown]`, and only the person who runs the system can say who holds it, an open question only they can answer.
- "UNKNOWN, funeral home owner" (combination side, Persona 4). `[Inferred]` from the ICP2 Combination pattern, which needs a funeral home side to the account. Persona 4 (profile: Buyer Personas) names this role, and the combination side needs it, because the pre-need leads run through it (Next Actions below). General counsel and procurement are known only in outline, with legal review and vendor onboarding timing not scoped `[Unknown]` and no open question on the record, so they are named as gaps, not ghost nodes. The CFO persona applies to groups only, and this account has two sites. The revenue table starts at $50M, so at under $50M it adds no ghost rows.

**Multi-Threading Score:**

| Dimension | Weight | Score (0 To 2) | Weighted | Why |
|---|---|---|---|---|
| C-Level Access | 2x | 1 | 2 | The board chair joined one call, in Stage 4 Proposal `[CRM]`, but is not on file by name, so no named C-level contact is engaged. The board chair counts as C-level (Methodology), engaged but unnamed, so 1. Ruth is a GM, not a C-level title, so she counts toward Department Breadth only |
| Champion Identified | 2x | 2 | 4 | Ruth Ellery, Strong: four of seven shared champion tests met, each tagged with its source and date |
| Department Breadth | 1x | 1 | 1 | Executive, Operations and Sales: 3 departments (the 2 to 3 band) `[CRM]` |
| Technical Evaluator | 1x | 0 | 0 | No IT contact on file `[Unknown]`. Nobody owns IT `[Unknown]` |
| Economic Buyer Engaged | 2x | 1 | 2 | Identified by role only, one call in Stage 4 Proposal `[CRM]`, budget not confirmed `[Call, 2026-09-26]` |
| End User Validation | 1x | 2 | 2 | Priscilla Dunmore, Actively Engaged: a pre-need walkthrough on 2026-10-08, which was not a demo, and a second logged interaction on 2026-10-14, two in the last 30 days `[CRM]` |
| Blocker Mitigation | 1x | 1 | 1 | Walt Okonkwo, a Skeptic with a stated objection, identified, and a strategy exists (a demo on his own work orders) (profile: Buying Committee). Developing under the Skeptic rule in Methodology |
| **Total** | | | **12 of 20** (scored 7 of 7) | |

Raw total 12 of 20, scored 7 of 7. threading_score = 12 ÷ 2 = **6**, Developing, material gaps. Full C-level credit would give a raw total of 14 and a score of 7. The map withholds that credit because the board chair is not a named contact on file, and one call with an unnamed person is not a relationship the team can plan around.

**Political Landscape:** Ruth is top-right (leverage), with Influence HIGH and support Strong `[CRM]`. The "UNKNOWN, family board chair" is HIGH influence, so it sits at the top of the map, on the centre line of support: interested in cost and not yet a supporter, a Skeptic `[Call, date Unknown]`. The chair takes no quadrant until the chair is named. Walt sits on the centre line, not in a quadrant, because his influence is MEDIUM and only HIGH influence takes a quadrant. He is a Skeptic with concerns and no opposition yet `[Call, 2026-09-21]`, and his daily use decides whether the system survives. Priscilla is LOW influence, so she is not placed on the map, and her support is `[Unknown]` until a conversation shows it.

**Output:** Engagement strategy:
- URGENT, five business days after the run date of 2026-10-19 (2026-10-26): Owen asks Ruth Ellery for the board date and the board chair's name by 2026-10-26, and asks her to broker a second call with the chair. Why: the economic buyer is unnamed and has been on one call, and the champion has not replied since 2026-10-03 `[CRM]`. How: a short note through Ruth, not a cold message to the chair. Messaging: price and the board line only, year one $26,576 with the $5,000 setup against the $25K line (profile: Product Modules). No customer result is cited, because the proof points are Illustrative.
- HIGH, by 2026-11-02: ask Ruth who keeps the Oldgate system running and who holds the ledger export. Who: "UNKNOWN, systems administrator". Why: the Technical Evaluator score is 0, and nobody owns IT. How: Ruth or Walt names one person, and the technical discovery runs before the readiness check on 2026-11-02. Messaging: the export question, not a product claim.
- HIGH, by 2026-11-02: a find-the-plot demo on Walt's own work orders. This is the strategy that keeps the blocker neutralized. Message: "Find the plot in seconds," the Operations Director hook (profile: Buyer Personas).
- MEDIUM, by 2026-11-18: ask Ruth who the funeral home owner is, since the combination's pre-need leads run through that side. Who: "UNKNOWN, funeral home owner".

Summary: Champion, Strong (Ruth Ellery, four of seven shared tests met). Economic Buyer, a ghost node with one call and no named contact. Blocker, identified with a mitigation plan (Walt Okonkwo). Top gaps: no named board chair, no IT owner, champion silent 16 days `[CRM]`.

```text
Hand-off (read by 09 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
threading_score: 6 (scored 7 of 7)
buying_roles: Champion Ruth Ellery (Strong), Economic Buyer UNKNOWN, family board chair (identified by role, one call), Technical Evaluator UNKNOWN, systems administrator, Influencer Walt Okonkwo (Skeptic), End User Priscilla Dunmore
ghost_nodes: UNKNOWN, family board chair, UNKNOWN, systems administrator, UNKNOWN, funeral home owner
champion_status: Strong (Ruth Ellery, four of seven shared champion tests met: offers introductions 2026-09-26 [Call, 2026-09-26], commits to next steps with dates 2026-09-26 [Call, 2026-09-26], explains the internal politics 2026-09-26 [Call, 2026-09-26], defends the solution when we are not in the room 2026-09-25 [CRM])
next_action: Owen Pruitt asks Ruth Ellery for the board date and the board chair's name by 2026-10-26, five business days after the run date of 2026-10-19
report_path: none (inline)
```

### Example 2: BDR Prospecting, Single-Threaded Account (Non-Success)

**Context:** A BDR is researching Saltmarsh Heritage Group, a family-owned group with five sites (two cemeteries and three funeral homes). The account is TARGET, not yet contacted `[CRM]`. Its annual owner letter, posted on the company site, says all five sites move to one system in 2027 `[Public: company site, owner letter 2026]`. CFO Hector Ruiz approves the budget `[CRM]`. This is the non-success case: the map is thin, and the BDR must not treat one contact as a buying committee.

**Input:** "Map the org structure for Saltmarsh Heritage Group so I know who to target first."

**Process:** `user_role = BDR`. No active deal `[CRM]`. The CRM holds one contact: Hector Ruiz, CFO (Finance), identified through research and not yet contacted `[CRM]`. Absence of other contacts is recorded as `[Unknown]`, not as "no such person." The owner letter does not name a second decision-maker.

Ghost nodes, from the profile's Buyer Personas. The revenue table does not apply at this size, and revenue is not in the profile:
- "UNKNOWN, owner" (writer of the owner letter) `[Inferred]`.
- "UNKNOWN, cemetery general manager", for the two cemeteries (Persona 1) `[Inferred]`.
- "UNKNOWN, pre-need sales manager", for the three funeral homes that run pre-need counselors (Persona 2) `[Inferred]`.
- "UNKNOWN, funeral home owner" (Persona 4) `[Inferred]`.
- "UNKNOWN, operations director" (Persona 3) `[Inferred]`.

**Multi-Threading Score:**

| Dimension | Weight | Score (0 To 2) | Weighted | Why |
|---|---|---|---|---|
| C-Level Access | 2x | 1 | 2 | CFO on file `[CRM]`, no engagement |
| Champion Identified | 2x | 0 | 0 | No champion. Status None, and no contact has met a shared test |
| Department Breadth | 1x | 0 | 0 | Finance only, 1 department `[CRM]` |
| Technical Evaluator | 1x | 0 | 0 | No IT contact on the full contact list `[CRM]` |
| Economic Buyer Engaged | 2x | 1 | 2 | CFO identified as the budget approver, not engaged `[CRM]` |
| End User Validation | 1x | 0 | 0 | No end users known `[Unknown]` |
| Blocker Mitigation | 1x | INSUFFICIENT | none | No blocker is shown, but the one contact has not been contacted, so there are no notes to read `[CRM]`. Left out of the total |
| **Total** | | | **4 of 18** (scored 6 of 7) | |

Raw total 4 of 18, scored 6 of 7. threading_score = 4 ÷ (2 × 9) × 10 = 2.2, rounded to **2**, Critical, almost no contacts. The Blocker row is left out rather than scored, so the map does not look better than the one contact it holds.

**Output:** Coverage is critical and single-threaded. The only known decision-maker is the CFO, and nobody else has been identified. A cold message to the CFO with the 2027 claim would be a single-threaded bet. The engagement plan is research only, with no outreach yet:
- Find the pre-need sales manager or pre-need counselor at one of the three funeral homes through LinkedIn research. This is the person who feels the lead follow-up pain daily. Next action: the BDR completes this research by 2026-10-26, five business days after the run date of 2026-10-19 (no earlier record or schedule date).
- Find the cemetery general manager for the two cemeteries (Persona 1).
- Keep the CFO as the economic buyer to reach once a second contact confirms the timeline. Use the owner letter as the shared hook, not as an assertion about what the family has decided.
- Re-score after the first two contacts. If the score does not move, the plan is wrong and needs rework.

Summary: Champion, None. Economic Buyer, identified and not engaged (CFO). Blocker, not yet checked (INSUFFICIENT). Top gaps: single-threaded, no operations or pre-need contact, cemetery side unknown.

```text
Hand-off (read by 09 and 06):
account: Saltmarsh Heritage Group (TARGET)
run_date: 2026-10-19
threading_score: 2 (scored 6 of 7)
buying_roles: Economic Buyer Hector Ruiz (CFO, not engaged), all other roles UNKNOWN
ghost_nodes: UNKNOWN, owner, UNKNOWN, cemetery general manager, UNKNOWN, pre-need sales manager, UNKNOWN, funeral home owner, UNKNOWN, operations director
champion_status: None (no contact has met any shared champion test)
next_action: BDR identifies one pre-need sales manager at a funeral home by 2026-10-26
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Active Deal Guard (BDR)
**When:** `user_role = BDR` and account has active AE deal.
**Action:** Generate the full org map but deliver with coordination guidance: "Active deal owned by [AE name] at [Stage]. Share this org map with the AE (do not prospect independently)."

### Pattern: Pre-Meeting Org Review
**When:** Used in conjunction with `gtm-meeting-prep` before a critical meeting.
**Approach:** Run stakeholder mapping first to understand the buying committee, then run meeting prep to prepare for the specific call. The org map informs who else should be in the room and what political dynamics to navigate.

### Pattern: Coaching Session Prep
**When:** Sales manager needs to review deal health with an AE.
**Approach:** The threading score and gap analysis provide objective coaching points. Focus the conversation on: "What's your plan to engage [missing role]?" and "How are you developing [potential champion]?"

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|-------------|----------|
| "Only 1-2 Contacts On File" | A new account, or a CRM with few contacts entered | Generate the map with heavy ghost node identification. The value is showing what is MISSING. The engagement strategy becomes a contact discovery plan. Recommend LinkedIn research and `gtm-account-snapshot` for broader intelligence |
| "Can't Determine Buying Roles From Titles" | Ambiguous titles such as "Manager" with no department | Use the department inference rules in Step 2. If the department is also unclear, classify the contact as UNKNOWN and flag it for discovery. At the next interaction ask: "Can you tell me about your team's structure?" |
| "Political dynamics unclear (no notes in CRM)" | No recorded interactions | Flag the political landscape as "Insufficient data (requires direct engagement to assess)." Give the rep a framework for the next interaction: ask about the decision process, who else is involved, and where concerns might come from |
| "Contact is both Champion and Economic Buyer" | One person holds budget authority and advocates | Assign the role that most affects deal strategy, which is Economic Buyer, and note the champion behaviors in the analysis. The engagement strategy reflects both dimensions |
| "A non-buyer's stance is contradicted by a call" | The stance was a hypothesis, and the call is the evidence | Update the stance with the call date and its tag. Do not keep the hypothesis as a fact, and do not rewrite the earlier map to hide the change |
| "The Buying Committee section of the profile is missing" | The CUSTOMIZE interview has not been run | Say so once at the start. Run on the generic non-buyer table and ghost node rules, and mark each output that depended on the missing section |

---

## Best Practices

### Do's
- **Pull ALL Contacts:** don't filter to "relevant" ones. The full picture reveals patterns.
- **Identify Ghost Nodes Aggressively:** missing positions are as important as known contacts.
- **Source Political Dynamics From Evidence:** CRM notes, interaction patterns, meeting attendance. Don't guess.
- **Tailor Engagement Strategy To User Role:** BDR needs entry points. AE needs multi-threading tactics.
- **Ask For The Missing Name Directly:** a ghost node becomes a next action with an owner and a date, so the team fills it with a fact.

---

## Integration With Other Skills

**Reads from the skills before it, by field name.** A missing field is reported as missing, not rebuilt here.

- **MEDDPICC Analysis (09):** `meddpicc_scores` (the Champion and Economic Buyer elements, checked against this map), `health_score`, `stage_minimum_met`, `stage_recommendation`, `risk_patterns`. A stakeholder risk named in `risk_patterns` is checked against the ghost nodes here.

**Hands to the skills after it, by field name.**

- **MEDDPICC Analysis (09):** `threading_score`, `buying_roles`, `ghost_nodes`, `champion_status`. The Champion and Economic Buyer elements are scored from these fields.
- **Meeting Prep (06):** `threading_score`, `buying_roles`, `ghost_nodes`, `champion_status`. The attendee list for the next meeting is checked against the ghost nodes.
- **Wrap-Up (O10):** `report_path` (set only when a file was written), `next_action` (owner and date).

**Related Skills, Without A Field Hand-Off:**
- `gtm-account-snapshot`: run first on thin accounts for broader intelligence, then map what it finds.
- `gtm-competitive-strategy`: a contact who is loyal to the incumbent (Blocker role) belongs in that skill's competitive work.
- `gtm-call-coaching`: after a call, update the map with the stakeholder intelligence the call produced.

### Chains

- **Work The Deal:** Meeting Prep (06), Call Coaching (13), Deal Pulse (08), MEDDPICC Analysis (09), **Stakeholder Mapping (10)**. This skill adds the buying-committee map and the ghost nodes that the Economic Buyer and Champion elements are checked against.

---

## Changelog

### 2.1.11 (2026-10-26)
- Two roles. A contact that fits two roles takes the role the record evidences. A Champion needs one shared test met, and the Economic Buyer is the person whose approval moves the spend, so the board chair holds that slot where a board approves above a limit.
- Ghost nodes name their source: a Buyer Persona row, the revenue table, or a Non-Buyers row that a dated step or open question needs.
- Engagement. A dated interaction counts in its window. Economic Buyer Engaged scores 2 only with two or more dated interactions in the last 30 days, and one call scores 1.
- Gone quiet. The shared gone-quiet test is not applied, because this skill starts no sequence, and a missing date for our last message does not block an action.
- Try-it and Example 1. The champion count, the stance label and the seniority label are removed from the records, and the illustrative marks on dated interactions are lifted, since a date on the record is a fact. The scores, threading score, ghost nodes and next action do not change.

### 2.1.8 (2026-10-26)
- Citations. A fact taken from the profile is cited (profile: Section) with the profile's own section name, in place of [Notes]. A rep's or AE's own notes keep [Notes].
- ENGAGED. An ENGAGED account (two-way contact, no open deal) is not covered by the Active Deal Guard, keeps its existing thread, and gets no new first-touch outreach. The first URGENT action for an ENGAGED account is a reply to the contact's last message.
- Champion. The champion tests, including the definition of shares competitor intelligence, are applied here by pointer to the Shared Contract, not restated.
- Tags. The Brackhaven IT-owner fact in Example 1 is tagged Unknown, matching the 2.1.6 record. The Saltmarsh CFO budget approval in Example 2 is tagged CRM, matching its Context.
- Headings and labels are capitalized word by word.
- The example scores, threading scores and next actions do not change.

### 2.1.7 (2026-10-26)
- Leak scrub. The Hard Rule that names the ghost node now uses the role in place of the example's role name, and the one dangling example reference is reworded so the input text stands alone.
- Settled: the URGENT next action follows one ordering rule (an unaddressed blocker, then an economic buyer who is a ghost node and is asked for by name, then a named economic buyer not yet engaged, then a champion at risk), and a ghost node counts as not engaged.
- Settled: the Blocker Mitigation score does not make a contact a Blocker, the Buyer Persona and Non-Buyers tables give the ghost-node rule for each function, the raw total divided by 2 shortcut holds only with all seven dimensions scored, and a pre-need counselor or manager is in the Sales department.
- The example's scores, threading score, ghost nodes and next action do not change.

### 2.1.6 (2026-10-26)
- Consistency pass across the sales skills. Example 1 cites the revised MEDDPICC score for its run date, and its Priscilla Dunmore interaction on 2026-10-08 is a pre-need walkthrough, not a demo. Her engagement status and End User Validation score are unchanged, because two interactions fall in the last 30 days.
- The IT ownership fact in Example 1 is tagged Unknown, not Notes, consistent with the other skills.
- Example 2 tags the CFO's budget approval to the CRM.
- No threading score, verdict or next action changes.
- Call-sourced facts in the examples carry their call dates. Each bare call tag is dated to the call that holds the fact, and a call with no date on record is written `[Call, date Unknown]`.

### 2.1.5 (2026-10-26)
- The invented CRM dated-action context line and its try-it line are removed, and the URGENT next action carries the shared rule's date.
- The URGENT action's date follows the family's one deadline rule. The Friday-of-the-run-week rule is removed. HIGH and MEDIUM windows are unchanged.
- The examples name the record behind each earlier date, and the research action in the BDR example carries the shared rule's date.

### 2.1.4 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1 under the Pass Rule. The try-it records carry the champion tests with their dates (matching the Meeting Prep and Deal Pulse records for the same account), the Skeptic call's date, the engagement status the rule gives, and the board date as working-to and not yet formally confirmed.
- The buyer-persona rule is separated from the non-buyer rule. A Buyer Persona that the account needs and that has no named contact is a ghost node, and a persona limited to a scope applies only within it (Non-Buyers rules, Ghost Node Identification).
- One HIGH criterion is enough for Influence (Influence Levels). An interaction with no date is not counted in an engagement window (Engagement Status).
- The revenue band is read from the account record, and a blank revenue reads as unknown with no revenue-table row (Step 1).
- Deadlines run from the run date and the order within a priority is set (Step 7).
- The examples' scores, the threading score, the verdicts and the next action do not change. The try-it promise states the score count.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The try-it records now carry Ruth's seniority in meetings (she set the 2026-11-12 board date) and Priscilla's LOW influence, and Example 1 shows the same facts. The hand-off's champion tests carry their dates.
- The UNKNOWN rule is added. A dimension with no evidence is INSUFFICIENT, the threading score re-weights over the scored rows (raw total ÷ (2 × the scored weights) × 10), the result reads "scored n of 7", and no score is given below 5 of 7. The Output Contract, the Methodology, Step 5, the Step 8 summary, the Quality Bar and Hard Rule 8 are updated.
- Quadrants: only HIGH influence takes a quadrant, a MEDIUM contact sits on the centre line and is placed by position, and a LOW contact is not placed. A Neutral or Skeptic sits on the centre line of support. Walt and the board chair are placed by that rule, and Priscilla is not placed.
- A general manager is not a C-level title. The ghost-node test is an open question the team needs answered about the non-buyer. The funeral home owner qualifies, and General Counsel and Procurement stay gaps.
- Example 2's Blocker Mitigation is INSUFFICIENT, because the one contact has not been contacted and there are no notes to read. This is the only output change in the examples.
- The examples' Example 1 scores and next action do not change.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. The board chair counts as C-level, a Skeptic with a stated objection is an Influencer who scores Developing on Blocker Mitigation, an end user is engaged when Actively Engaged, and a non-buyer becomes a ghost node only when the record needs that person. The Blocker definitions in the buying roles table and the Methodology now agree. Example 1 names the four champion tests with their call dates and carries the employee count and revenue band. The threading score stays 6.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1.

### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`, and the personas under `people/`) and offers read-only CRM connectors through the shared contract's Knowledge Base and Connectors section, before the CRM contact read.
- Adds a Chains subsection placing the skill in the Work The Deal chain.

### 2.0.0 (2026-10-20)
- Sales 2.0 standard. Shared Contract added under Context, and the champion tests, the status words and the evidence tags come from it. Nothing from it is restated here.
- Epistemic Rules and Hard Rules added. The Hard Rules replace the old Don'ts, each with its reason.
- Non-buyer table added: technical reviewer, systems administrator, general counsel, operations head, procurement. Every stance is a hypothesis until a conversation confirms it.
- Threading formula written out. Seven weighted rows, raw total 0 to 20, divided by 2 and rounded half up to a whole score from 0 to 10. The output shows all seven rows.
- Ghost nodes written "UNKNOWN, role", never a name.
- Champion status is Strong, Developing or None, set from the shared champion tests. The Champion dimension's wording follows.
- Output Contract added with the hand-off fields. Integration reads the MEDDPICC fields by name.
- The separate output-format section is folded into the file option in the Output Contract. Markdown is written only when asked. The HTML and PDF options are removed.
- Examples aligned to the PlotIQ chain file. Brackhaven's family board chair is an unnamed ghost node with one call in Stage 4 Proposal. Ruth Ellery is Strong on four of seven shared tests. Nobody at Brackhaven owns IT. The threading score moves from 7.0 to 6.

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.0 (2026-09-29)
- Worked examples rewritten, and em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy. Client-specific data moved to the shared client profile. No functional change to the workflow or the scoring.

### 1.0.0 (2026-03-04)
- Initial release. Seven buying roles, the seven-dimension weighted threading score, ghost nodes, and political landscape mapping.
