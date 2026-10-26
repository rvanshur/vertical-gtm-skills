---
name: gtm-competitive-displacement
version: 2.1.8
description: "Plans outbound to displace a known incumbent, by classifying the incumbent, rating how hard the switch is, and drafting persona-tailored four-step email sequences for the rep to read and send, so the BDR or AE who works the account knows what to say and what not to say."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [competitive-displacement, incumbent-displacement, competitive-outbound, competitor-takeout, displacement-sequences, displacement-difficulty]
requires:
  skills: [gtm-competitive-strategy]
mutating: read-write
change_log:
  - version: 2.1.8
    date: 2026-10-26
    summary: "Citations, ENGAGED and status. A fact taken from the profile is cited (profile: Section) in place of [Notes]. An ENGAGED account gets a reply plan in place of the four-step cold sequence, with a new Hard Rule. Greyfield's status record now states that no reply is on record on its run date, so TARGET stands. Headings and labels are capitalized word by word. The example sequences, difficulty ratings and next actions do not change."
  - version: 2.1.7
    date: 2026-10-26
    summary: "Leak scrub and one research rule. A research figure dated more than 90 days before the run date is never used in an email, so Email 1 names no figure unless a source dated within 90 days is on record. The next action is written as owner, action and date, with no example answer. The renewal rule settles a known renewal month with an unknown term, the owner rule settles a CRM name held only as a tag, and the wedge is one sentence with no roadmap figure. Dangling example references are reworded, and the profile labels in the examples carry the evidence tags."
  - version: 2.1.6
    date: 2026-10-26
    summary: "Greyfield's contact status reads the logged touch of 2026-09-24 with no named contact, in place of not yet contacted. Tamsin Vale's second example no longer relies on a buyer call: its incumbent and decision path cite the CRM record, its contract term is recorded as none, and it keeps two personas with eight drafts on hold. Brackhaven's third example cites the dated call row in the Competitive Strategy skill for Oldgate's unsold-plot visibility. The Competitive Strategy citation and the next action rule are unchanged."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The competitive research citation is flagged as over 90 days old at the run date, and an Epistemic Rule states the flag. The next action follows the family's one deadline rule: five business days after the run date, or an earlier date the CRM or the records set for that step, named with its source. The skill's own four-business-day rule is replaced by a pointer to that rule, and the example next actions carry the recomputed dates."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it fixes from the blind retest: the Output Contract names the parts the steps produce and the four the steps do not produce, the next action takes a date rule and an action verb, the Context names the example profile for a first run, a CRM note confirms the incumbent only when its text names it, the hand-off block is defined, the competitive research is cited by its Sources name, and the Methodology settles the open judgments (Settled Judgments) and bars illustrative figures from emails."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1: the Pre-Need persona carries its angle, question and selection reason, each Unknown gap row names its settling question, the Wedge drops its unsourced 90 to 120 day figure, the Time to Live row names its source, Email 3 names its unlock date, the next action takes the CRM owner, and the report says which sections and drafts it leaves off the page."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1: an unnamed contact is an Unknown champion, the Example 1 sequence scope is stated, and the next action reads as the rep reviewing and sending."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS base and offers read-only connectors through the shared contract's new Knowledge Base and Connectors section, with a Chains subsection."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 standard. Adds a displacement template per incumbent type (Positioning, Wedge, three discovery questions), a Low, Medium and High difficulty scale with one directional test each, and a Displaced vendor and Status column on proof points. Every number in an email needs a named, dated source or it is removed. The BDR guard is a Hard Rule with its reason. One Epistemic Rules section with one Confidence subsection. Hand-offs to 02 and 06 are named, and Integration reads 11 by field name. The report is inline, and the file is written only when asked."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on the PlotIQ example company. Example arithmetic and listed errors fixed, and a non-success example added."
---

# Competitive Displacement Outbound

## Overview

Competitive Displacement builds outbound for an account that already uses a known incumbent. It classifies the incumbent by type, rates how hard the switch is, and drafts persona-tailored four-step email sequences that the rep reads, edits and sends. It is best used when you know what the account uses today. If you do not know, run Account Snapshot (02) first.

The report is for the BDR or AE who will write to the buyer. Every competitive claim in it carries an evidence tag, so the rep can see what may go into an email and what may only be asked on a call.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Displace on the incumbent's known failure, with a wedge the buyer can see in one email.

---

## Why This Skill Exists

A displacement email fails in one of two ways. It names a problem the buyer does not have, so it is ignored. Or it states a figure or a competitor weakness with no source, so the first buyer who asks where it came from finds nothing behind it. The people who receive these emails use the incumbent's product every day, so one wrong claim identifies the sender as a vendor who guesses.

A second failure is timing. A BDR writes to a buyer who already has an AE in an active deal, and two people in one inbox cost the deal. This skill stops both failures before the first email is drafted: it checks the source of every claim, and it checks who owns the account.

---

## Role

You are a competitive outbound specialist. You classify the incumbent, rate the displacement difficulty, and draft sequences that use the profile's own displacement template, failure patterns and proof points. You do not invent a competitor weakness.

You refuse four things. You do not put a number or a competitive claim into an email without a named source and a tag. You do not write sequences for a BDR on an account that an AE owns in an active deal, unless that AE has said yes. You do not name the competitor in a subject line or attack the prospect's choice. You do not send anything or write to the CRM. The reasons sit in **Hard Rules**.

---

## Input Contract

If a required input is missing, ask. Do not guess.

To try the skill without your own data, use `examples/try-it.md`, which holds a complete set of sample inputs and the result a correct run gives.

| Input | Required | Notes |
|-------|----------|-------|
| Account Name | Required | The target account. Its status (TARGET, ENGAGED, INBOUND, ACTIVE with its stage number, LOST or OUT) is read from the CRM when there is one, otherwise from the profile's example cast |
| Known Incumbent | Required | The product the account uses now. If it is unknown, say so and run Account Snapshot (02) first. A suspected process, such as paper records, counts as an incumbent |
| User Role | Required | BDR or AE. Step 0 reads it from the CRM and asks only when the CRM does not say, because the BDR guard depends on it |
| How The Incumbent Was Identified | Optional | CRM note, prospect statement, job posting, conference conversation. Sets the confidence in Epistemic Rules |
| Incumbent Failure Signals, With Their Source | Optional | Each one is used only with its tag. Without a source, it becomes a discovery question |
| Contacts At The Account | Optional | Named contacts are used by name. Without a name, the persona title is used and the contact is written `[Unknown]` |

---

## Output Contract

Every run returns its report in the chat. The file is written only when the user asks for it.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Displacement Report | In the chat | The parts the steps produce, in this order: Company and Incumbent Snapshot (Step 1), Competitive Gap Matrix (Step 2), Key Personas and Sequence (Step 3), Discovery Questions (the Step 2 template row), and the 13-item summary of Step 4, which ends with `next_action`. Displacement Hooks, Product Against Incumbent, Objection Handling and Call Flow are not produced by any step, so a run leaves them out and says so in one line under its last section. Under the BDR guard, only the Snapshot, the Gap Matrix and the Discovery Questions appear, with the guard note |
| `incumbent_type` | Company and Incumbent Snapshot | The type the profile's Competitive Landscape files the incumbent under, with its confidence |
| `displacement_difficulty` | Company and Incumbent Snapshot | Low, Medium or High, with the test that set it and whether that test was met |
| `target_personas` | Key Personas | The profile rows used, ranked, each with its title, the count as n of N, and the contact or `[Unknown]` |
| `sequence` | Below Key Personas | Four emails per persona, drafted and never sent. A page may show fewer. Then it says the other drafts follow the same rules and are left off the page, and names them. Under the BDR guard, `none (guard)`. Under ENGAGED, `none (ENGAGED: reply plan)`, and the reply plan takes the place of the four emails. |
| `report_path` | Header of the report | `none (inline)` unless the user asked for a file |
| `next_action` | Last line of the report | The owner, the action and a date, written as "[owner] [action] by [date]", for example "[owner] finds the contact's name, then reviews and sends the first email by [date]". The owner is the BDR or AE of record in the CRM. When the CRM names the owner, that name is written with `[CRM]`. When the owner field is blank, the name is written `[Unknown]` and the role is kept, never a name from another account. The date follows the shared contract's next-action rule (five business days after the run date, or an earlier date the CRM or the records already set for that step, named with its source). The step names the action the owner takes, not the result |
| File, On Request | `<account>_gtm-competitive-displacement_<date>.md`, saved beside the user's other account notes | Written only when the user asks, in Markdown. The ask is the approval step |

---

## Context

This skill does not carry client-specific information. It reads the client profile at [`profiles/client-profile.md`](../../profiles/client-profile.md). Throughout this skill, `{Client Profile: X}` means section X of that file. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`. Until that file exists, read every profile section this skill names from `profiles/examples/plotiq-example.md`. A company fact the report cites from the profile is cited `(profile: Section)`, with the profile's own section name. It keeps the grade the profile gives it, and it needs no evidence tag. An account fact the CRM holds is tagged `[CRM]`.

| Profile Section | Used For |
|---|---|
| Company | Account framing and vertical context |
| Buyer Personas | The rows a template names as primary and secondary. The count is the profile's row count, written as n of N |
| Competitive Landscape | The incumbent's row (type, pitch, weakness, pain reported after 6 to 12 months with its source) and the competitive discovery questions |
| Value Propositions | The wording of the wedge |
| Proof Points | The Displaced vendor and Status columns, which decide whether a proof point can be cited |
| Displacement | One template row per incumbent type, and the team's notes on the difficulty tests |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls and decisions for that account), the competitors under `gtm/` (the incumbent's row), and the personas under `people/` |

If a section in this table is missing, the skill says so once at the start, says it is running uncustomized on the defaults in Methodology, and marks every output that depended on the missing section. The Displacement section is the one most often missing, and `CUSTOMIZE.md` writes it. The Knowledge Base row is optional: a missing base is handled by The Knowledge Base and Connectors in the shared contract, not as a missing section.

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

Your displacement playbook. The defaults below apply until the profile's Displacement section says otherwise. Evidence tags, numbers and confidence follow Epistemic Rules and the Shared Contract.

### The Displacement Template

The profile's Displacement section holds one row per incumbent type the account base uses. Every row has the same fields:

```text
Incumbent type: the type the profile's Competitive Landscape files the incumbent under
Positioning: what the buyer does now, and why it falls short, with its tag
Wedge: the one thing we do differently, in one sentence the buyer can read in one email
Discovery question 1: a question that exposes the gap, asked from curiosity
Discovery question 2: a second question on the same gap, or on the renewal
Discovery question 3: a question that finds the decision maker or the renewal date
Primary persona: a row number from the profile's Buyer Personas table
Secondary persona: a row number from the profile's Buyer Personas table
```

A template keeps the team's tested wedge in front of the rep, so the rep does not invent one in the moment. Positioning is written with its tag, because the buyer will ask where it came from. Each discovery question must be a real question. A statement dressed as a question is rewritten before it is used. The wedge is one sentence with no roadmap figure in it, because a roadmap figure stays in the report and never reaches the email (Roadmap Figures).

### Displacement Difficulty

The difficulty scale has three levels. Each level has one test, and each test is directional. It sets a starting rating from the account's contract facts. It does not predict a win.

| Rating | Test (Directional) | Met Means |
|--------|--------------------|-----------|
| Low | No contract term to exit. A manual process, or a tool the account can cancel at the next cycle | Low |
| Medium | A renewal inside 180 days | Medium |
| High | A contract term running more than 180 days past today, with an exit fee in the contract | High |

The rating is the highest level whose test is met. When the contract term is unknown, no test can be run, so the rating is High and the output says the term is unknown, unless a renewal month is on record, which fixes the end of the term (Settled Judgments). An unknown term is not a favorable one, and a plan that assumes an easy switch skips the question that decides it.

### Persona Selection

The profile's Buyer Personas table sets the options. The template row names a primary and a secondary persona by row number. Use the rows the template names, and write the count as n of N, so the reader sees how many rows the profile holds and how many were used. A persona with no contact on file keeps its title, and its contact is `[Unknown]`.

### Sequence Structure (Per Persona)

| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | Industry trend, or a sourced benchmark dated within 90 days of the run date | Give a reason the incumbent's limits cost more now. Do not attack. Create context |
| **Email 2** | Capability gap question | Ask a question the incumbent cannot answer well, and let the buyer find the gap |
| **Email 3** | Proof point from a comparable switch | Cite a customer result only when its Status is Verified. Otherwise hold the email |
| **Email 4** | Contract timing | Acknowledge the current vendor. Ask when the contract renews, unless the renewal month is on record, in which case Email 4 confirms it (see Settled Judgments). Frame it as worth 15 minutes before the next renewal |

### Rules For Every Email

- Include a subject line, and never name the competitor in it
- Keep the body at 120 words or fewer
- Make the first line refer to something specific about the prospect
- Give each of the four steps a different displacement angle
- Match each proof point to the prospect's vertical and size
- Address a known contact by name, and an unknown one by title
- Put a number in only with its named, dated source (see Epistemic Rules)

### After Each Persona Sequence, Include

- The displacement angle for this persona, in one line
- The best discovery question for this persona, from the template row
- Why this persona was selected for this scenario, in one line

### Settled Judgments

- **Wishes the Incumbent Does Not Cover.** A stated wish that the incumbent does not meet, such as pre-need on the same system, counts as known pain with the incumbent, tagged to the source that states it.
- **Month-Only Renewals.** A renewal known only to its month is tested from the first day of that month. That month also fixes the end of the term, so the term is not unknown: the rating follows the three tests, and an exit fee that is not on record does not raise it.
- **Old Research in Email.** A research figure dated more than 90 days before the run date does not appear in an email, even with its source named. The report keeps it as a research estimate. Email 1 then uses the industry trend without a figure, with its question carrying the point, unless a figure dated within 90 days of the run date is on record.
- **Email 4 Timing.** When the renewal month is on record, Email 4 confirms it and makes the renewal the reason to look now, as the Contract Renewal Window pattern says. The question in Email 4 is used only when no renewal month is on record.
- **Best Discovery Question.** A persona's best discovery question is the template question about that persona's own pain. A persona with no such question uses the template's first question.
- **Roadmap Figures.** A figure from the profile's roadmap, such as weeks to go-live, is PlotIQ's plan and not a sourced number. It appears in the report as the plan and never in an email.
- **Contact Names.** A next action names no place to find a contact's name unless the records name one. Until a name is found, the contact is written with its title.
- **Email Spacing.** The four emails in a sequence are sent at least five business days apart, and Email 3 is sent only after its proof point is Verified.
- **Word Counts.** The report does not print word counts. Each draft is checked against the 120 word limit before it is shown.

---

## Quick Reference

**Use This Skill When:**
- You know the account uses a specific incumbent
- CRM notes or a conversation name the current vendor
- The account is evaluating alternatives to its current solution
- A competitor contract is up for renewal

**Don't Use When:**
- You do not know what the account uses (use `gtm-account-snapshot` to find out)
- The account is net-new with no incumbent intelligence (use `gtm-account-snapshot` or `gtm-research-outbound`)
- The account is closed-lost (use `gtm-closed-loss-reactivation`)

**User Roles:** BDR, AE
**Expected Time:** 15 to 25 minutes per account

---

## Core Workflow

### Step 0: Detect The User Role And The Account Status

Determine whether the user is a BDR or an AE, and read the account's status and AE owner. Role comes first because the BDR guard decides whether any sequence is written at all, and running the guard before drafting saves the time a draft would take.

Before pulling anything, read the account's folder under `accounts/`, the competitors under `gtm/` and the personas under `people/` in the knowledge base, when the profile has one. Then offer to read the CRM account record, and ask before reading it, as set out in The Knowledge Base and Connectors.

**From CRM:** check the user's role. If it is unclear, check the BDR owner against the account owner.
**Fallback:** ask, "Are you a BDR or an AE?"

If the user is a BDR and the account is ACTIVE with an AE owner, stop. Produce the analysis in Steps 1 and 2 only, and skip Step 3. The guard is a Hard Rule, and its reason is stated there. An account pending AE assignment is not ACTIVE, so it is worked, and the output says it is pending.

**ENGAGED Accounts:** An ENGAGED account has two-way contact and no open deal, because the account replied or met with us. A cold four-step sequence is wrong for it. The buyer has already answered an outreach, so a first email would make the buyer start over. For an ENGAGED account, Steps 1 and 2 run as written, and Step 3 becomes a reply plan. The reply plan is one drafted reply to the buyer's last message, in the buyer's own words, with the template's best discovery question as its follow-up. The incumbent comes up only when the buyer raises it. The BDR guard does not apply, because no AE deal is open. The reply is written by the rep who holds the thread, or by the owner of record when the CRM does not name the holder. The `sequence` field reads `none (ENGAGED: reply plan)`.

**Produces:** `user_role` (BDR or AE), the account status word, and the AE owner if there is one.

### Step 1: Identify The Incumbent And Gather Context

#### 1a. Confirm Inputs
- Company name
- Known incumbent, or "suspected manual process"
- How it is known (CRM note, prospect statement, job posting, conference conversation)
- Any known pain with the incumbent, with its source
- Confidence in the incumbent identification (HIGH, MEDIUM or LOW), by the Confidence rule below

#### 1b. Search The CRM
Pull the account record, deal stage, owner, contacts, BDR owner, engagement history, previous outcomes, and any note that names a vendor or competitor.

**Key Extraction Targets:**
- Any direct competitor mention in notes, emails or call records, with its date
- Prior outcomes. Was the account won, lost or stalled?
- Contact engagement. Who is active, and who has gone quiet?
- Contract timing. Renewal dates and term lengths
- Pain signals about the current tools

#### 1c. Classify The Incumbent
Use `{Client Profile: Competitive Landscape}` to file the incumbent under the type the Shared Contract lists. Record the type as the profile names it.

#### 1d. Assess Displacement Readiness
Rate the account's readiness for displacement. Every cell that is not in the record is `[Unknown]`, never a no.

| Signal | Assessment |
|--------|-----------|
| Known Pain With The Incumbent | Yes (specific, tagged) / Suspected / `[Unknown]` |
| Contract Status | Month-to-month / Expiring within 6 months / Locked (12 months or more) / `[Unknown]` |
| Champion Identified | Yes (name) / Partial / No / `[Unknown]` |
| Budget Cycle Alignment | In cycle / Off cycle / `[Unknown]` |
| Previous Evaluation Of Our Product | Yes / No / `[Unknown]` |

A champion is `Partial` only when a named contact shows some champion behavior with a tag. A contact who is not named is `[Unknown]`, never `Partial`.

#### 1e. Rate The Displacement Difficulty
Run the three tests in Methodology against the contract facts from 1d, and record the rating, the test that set it, and the tag on the contract fact.

**Produces:** `incumbent_type`, the confidence level, the readiness table, and `displacement_difficulty` with its test. Step 1 comes before Step 2 because the template row depends on the type, and the difficulty depends on the contract facts gathered here.

### Step 2: Load The Template Row And The Competitor Intelligence

Load the profile's Displacement row for the incumbent type, and the matching Competitive Landscape row. If the competitive strategy output for this account exists (`gtm-competitive-strategy`), start from its `gap_matrix` and say so. Otherwise build the gap matrix here.

Build a **competitive gap matrix**:

| Capability | The Incumbent | Our Product | Why It Matters For This Account |
|-----------|-------------|-------------|----------------------------------|
| Capability 1 | The gap, with its tag | The strength | Connected to this account's situation |
| Capability 2 | The gap, with its tag | The strength | Connected to this account's situation |

The "Why It Matters for This Account" column connects each gap to the account's situation, not to generic positioning. A gap that is not known is written `[Unknown]` with the question that would settle it.

**Produces:** the template row in use, and `gap_matrix` with a tag on every gap cell.

### Step 3: Generate The Displacement Sequences

Produce a four-step sequence for each persona the template row names, and for any other profile row that the account's facts support. The count is the number of persona rows used, written as n of N. Skip this step under the BDR guard.

#### Persona Selection, Then Sequence
Pick the persona rows from Methodology, then draft each sequence in the structure in Methodology, applying the Rules for Every Email. Check every number and every claim against Epistemic Rules before the email is written, not after.

**Produces:** `target_personas` (ranked, n of N) and `sequence` (four emails per persona, each with its subject line, its angle, and its persona note).

### Step 4: Summary Report

1. **Company:** name, and the incumbent identified
2. **Incumbent Type:** from the classification, as the profile names it
3. **Displacement Difficulty:** the rating, the test that set it, and whether the test was met
4. **Displacement Readiness:** from Step 1d, with the `[Unknown]` cells counted
5. **CRM Status:** status word, existing contacts, deal history, owner
6. **Personas Targeted:** n of N profile rows, and why
7. **Sequences Generated:** n personas x 4 emails, and which emails are on HOLD
8. **Strongest Opening:** the first line with the most specific reason
9. **Key Displacement Lever:** the single gap the incumbent cannot fill
10. **Contract Timing:** known or unknown, with its tag. If unknown, Email 4 asks
11. **User Role:** BDR or AE
12. **Coordination Note:** the BDR guard result, and who the analysis goes to
13. **Evidence Tags Used:** the tags behind the claims in the emails, and any `[Unknown]` that a call must settle

**Produces:** the summary, the hand-off block, and `next_action` with its owner and date. The hand-off block holds these fields, under the names used in Integration: account, run_date, incumbent_type, displacement_difficulty, target_personas, sequence, report_path and next_action.

---

## Epistemic Rules

- **Every count and rate carries its n.** Write "N of M persona rows" and "N of M template personas", never a bare number.
- **One evidence tag set.** Facts use the six tags from the Shared Contract. A competitive claim may go into an email only when it carries `[CRM]`, `[Call]` or `[Public: source]`. An `[Inferred]` claim feeds discovery questions and hypotheses. An `[Unknown]` claim is a discovery target.
- **Every number in an email has a named, dated source, or it is removed.** One good example: "Cemeteries of this kind often carry [figure] plots that are sold on paper and unsold on the map ([named report and date, within 90 days of the run date], Benchmark)." That sentence stays, because its source is named, dated and recent enough to use. The version "Most cemeteries lose a third of their plots to paperwork" has no source, so the figure and the sentence come out, and the email asks the question instead: "How many plots could you sell today if the records were right?"
- **An illustrative figure never goes into an email.** A figure an example marks (illustrative) is shown in the report and stays out of every email, because Hard Rule 2 accepts only a named, dated source.
- **Failure patterns need the buyer's own words.** A failure pattern used in outbound traces to a won-away customer who said it, with its tag. A pattern drawn across accounts needs five cases behind it. Fewer than five is an observation, and the report says so in the same sentence.
- **Silence is not a no.** A blank CRM field is `[Unknown]`. An unknown contract term sets the difficulty to High, and it never sets it to Low.
- **Never fabricate a competitor weakness.** If the intelligence for an incumbent is thin, say so, and use positioning tagged `[Inferred]` that rests on the category pattern.
- **Difficulty ratings are directional.** A Low rating means the positioning is favorable. It does not mean the deal is easy.
- **Research older than 90 days.** A research citation dated more than 90 days before the run date is flagged in its citation as over 90 days old at the run date, and it is used only as a research estimate, never as a benchmark and never in an email (Old Research in Email, under Settled Judgments).

### Confidence

Confidence applies to the incumbent identification, and it decides whether displacement runs at all.

- **HIGH:** the incumbent is confirmed by a CRM note, a discovery call or a prospect statement, each with its tag. A CRM note confirms the incumbent only when the note's text names that incumbent. Proceed with full sequences.
- **MEDIUM:** the incumbent is suspected from job postings, industry knowledge or partial CRM data. Proceed, note the assumption, and make discovery question 1 validate it.
- **LOW:** the incumbent is a guess. Do not run displacement. Run Account Snapshot (02) first to find the incumbent.

---

## Hard Rules

1. **The BDR guard.** A BDR never gets sequences on an account that is ACTIVE with an AE owner, unless that AE has said yes. The analysis goes to the AE, who decides how to use it. Reason: two people writing to one buyer costs the deal, and the buyer cannot tell which of the two is the account owner. An account pending AE assignment is not ACTIVE. It is worked, and the output says it is pending.
2. **A number in an email has a named, dated source, or it comes out.** Reason: a figure the buyer can ask about, with nothing behind it, identifies the sender as a guesser, and the buyer uses the incumbent every day, so a wrong figure is caught.
3. **A competitive claim in an email carries `[CRM]`, `[Call]` or `[Public: source]`.** Reason: an `[Inferred]` claim is reasoned, and an `[Unknown]` claim is missing. Neither is evidence the buyer can check.
4. **A proof point with Status Illustrative never appears in an email or a talk track.** Reason: Illustrative means invented for an example. Citing it to a prospect is a false claim. Verified is the only Status that may be cited as a customer result, and Benchmark may be cited only with its source named.
5. **Never name the competitor in a subject line.** Reason: it reads as an attack, and it is the most common trigger for spam filters.
6. **Never attack the competitor or the prospect's choice.** Reason: the prospect chose the current tool for reasons, and a sequence that mocks the choice makes the buyer defend it.
7. **Never use the same displacement angle twice in one sequence.** Reason: each email must give the buyer a new reason to reply, and a repeated angle reads as a reminder rather than news.
8. **Never send, never enroll a contact, never write to the CRM.** Reason: the rep owns the outreach and the record. The Shared Contract states this for every skill, and this skill keeps it in the same words.
9. **Never draft a cold displacement sequence for an ENGAGED account.** Reason: the buyer has already replied, so a first-touch sequence asks the buyer to start over and ignores the reply.

---

## Quality Bar

Done when all are true:

- [ ] Every fact carries one of the six tags, and every blank cell is written `[Unknown]`
- [ ] The incumbent type is the profile's type, and the confidence level follows the Confidence rule
- [ ] The difficulty rating names the test that set it, whether that test was met, and that the test is directional
- [ ] The persona count is written as n of N, with the profile's row count
- [ ] Every number in every email has a named, dated source, or it has been removed
- [ ] Every competitive claim in an email carries `[CRM]`, `[Call]` or `[Public: source]`
- [ ] No proof point with Status Illustrative appears in an email or talk track
- [ ] The competitor is not named in any subject line, and no email attacks the competitor or the prospect's choice
- [ ] Each of the four emails uses a different angle, and each body is 120 words or fewer
- [ ] The role was checked, and the BDR guard was applied where it applies
- [ ] An ENGAGED account gets a reply plan in place of the four-step sequence, and no cold sequence is drafted for it
- [ ] The `next_action` line is last, with an owner and a date
- [ ] No file was written unless the user asked for one

---

## Examples

Three worked examples on the PlotIQ cast and the chain file. They show a success path with one email on hold, a non-success where the sequence waits for facts, and the BDR guard on an active deal. Every figure is in the profile, carries a tag, or is marked `(illustrative)`. Each example ends with its hand-off block.

### Example 1: Pre-Need And Records Displacement, Stonemark At Greyfield Memorial Park

**Context:** Greyfield Memorial Park is a one-site cemetery with 9,000 plots `[CRM]`. It runs a digital map from Stonemark, a direct software incumbent, and its three-person pre-need team takes requests through an intake form on the site `[Public: Greyfield Memorial Park website]`. The Stonemark renewal is January 2027. The account is TARGET, with one touch on 2026-09-24 and no named contact `[CRM]` (illustrative), and its verdict is GREENLIGHT (Zones 2 and 3 HIGH, Zone 1 MEDIUM, because the digital map holds no records or trust reporting). No contact names are on file, so every contact is `[Unknown]` and the sequence uses titles. The BDR guard does not apply, because a TARGET account is not ACTIVE. The profile has no Knowledge Base section, so this run says so once here and works from the profile and the records.

**Input:** "Greyfield Memorial Park uses Stonemark. Build displacement sequences."

**Step 0. Role And Status:** User role is BDR, from the CRM user record `[CRM]` (illustrative). CRM check: TARGET, one touch on 2026-09-24 with no named contact and no reply on record `[CRM]` (illustrative), no open deal, no AE owner. The guard does not apply, and the ENGAGED rule does not apply, because no reply is on record. Sequences are drafted.

**Step 1. Identify The Incumbent:** Stonemark, direct software. How we know: the account's CRM note names Stonemark as its map vendor `[CRM]` (illustrative). Confidence: HIGH, because the CRM note names the incumbent.

**Step 1d. Displacement Readiness:**
- Known Pain: Yes, specific. The pre-need team wants pre-need and records on one system (profile: Example Cast) (illustrative)
- Contract Status: Expiring within 6 months. Renews January 2027 `[CRM]` (illustrative)
- Champion: `[Unknown]`. The pre-need team lead is named nowhere, so there is no named contact to score
- Budget Cycle: `[Unknown]`
- Previous Evaluation Of Our Product: `[Unknown]`

**Step 1e. Displacement Difficulty: Medium.**
- Low test (no contract term to exit): not met, the account has a contract.
- Medium test (renewal inside 180 days): met. The renewal is January 2027, 74 days from today (2026-10-19) when counted from 1 January, `[CRM]`.
- High test (term past 180 days with an exit fee): not met on the record. The exit fee is `[Unknown]`.
- The rating is Medium, the highest test met. All three tests are directional.

**Step 2. Template Row And Intelligence:** The profile's direct software row for Displacement:
- **Positioning:** The buyer runs a map that works, but trust reporting and pre-need still run outside it, so staff keep a second system `[Inferred: category pattern for enterprise mapping tools, illustrative]`.
- **Wedge:** Records, trust compliance and pre-need in one system. The roadmap puts go-live at 6 weeks (profile: Value Propositions), which stays in the report and out of the email.
- **Discovery Question 1:** "Where does the plot map live today, and when was it last updated?"
- **Discovery Question 2:** "Which system runs the pre-need side, and who maintains it?"
- **Discovery Question 3:** "When does your map contract renew, and what does the renewal include for support?"
- **Primary Persona:** row 2, Pre-Need Sales Manager. **Secondary Persona:** row 1, Cemetery General Manager.

Gap matrix:

| Capability | Stonemark | Our Product | Why It Matters For Greyfield |
|---|---|---|---|
| Sold and unsold plots on the map | `[Unknown]`. Ask: "Where does the plot map live today, and when was it last updated?" | Plot inventory shows sold and unsold plots | The pre-need team needs to know which plots are free before it sells one |
| Pre-Need Leads | `[Unknown]`. Ask: "Which system runs the pre-need side, and who maintains it?" | Pre-Need CRM and Lead Scoring | Leads from the intake form need a named follow-up owner |
| Records And Trust Compliance | `[Unknown]`. Ask: "Walk me through last year's trust filing. Who pulled the numbers, and from where?" | Records and Trust Compliance module | The account wants pre-need and records together |
| Time To Live | 90 to 120 days (`[Public: deathcare research project, competitive research note, 2026-03-27]` (research estimate, over 90 days old at the run date)) | 6 weeks (profile: Value Propositions) | The January 2027 renewal sets the window |

Proof points: Fennick Gardens (212 unsold plots found in 90 days) and Holloway Hills (zero records findings in its first state review). Both are Illustrative, and neither names a displaced vendor (`[Unknown]`). Neither can appear in an email, and the research figure is over 90 days old, so Email 1 names no figure.

**Step 3. Sequences:** Persona selection: 2 of 5 profile rows, row 2 Pre-Need Sales Manager (primary, the team that feels the intake pain) and row 1 Cemetery General Manager (secondary, the buyer). Both contacts are `[Unknown]`, so the emails use titles. That makes 2 personas and 8 emails. The page shows Email 1 and the HOLD on Email 3 for the Pre-Need Sales Manager, and omits the rest of the drafts: Emails 2 and 4 for that persona, and all four for the Cemetery General Manager. Those drafts exist and follow the structure in Methodology, and they are left off this page only for length.

**Pre-Need Sales Manager, Email 1 (Industry Trend, Held Without a Figure). Drafted, not sent.**
Subject: Pre-need requests from the intake form

Your team takes pre-need requests through the intake form on the site.

How do the intake form requests get a first call back today?

Your name

The trend figure is held. Its only source, the deathcare research dated 2026-03-27 to 2026-04-01, is over 90 days old at the run date, so it may not appear in an email, and the email names no figure. The question at the end is the discovery question from the template, which lets the buyer find the gap.

**Pre-Need Sales Manager, Email 3 (Proof Point). Status: HOLD.** The only proof point that fits is Illustrative, so Email 3 names no customer result. The Fennick Gardens case study waits until its numbers cover a full year (January 2027) (profile: Proof Points). Email 3 is released only when a proof point is Verified, and Verified also needs the customer's agreement to be named. The earliest date for Fennick Gardens is therefore January 2027, so Email 3 cannot go before then.

**Per-Persona Lines, Pre-Need Sales Manager:**
- Displacement Angle: pre-need leads and plot records on one system, so a counselor's sale is matched to a plot the buyer can see.
- Best Discovery Question: "Which system runs the pre-need side, and who maintains it?" (template question 2)
- Why Selected: the team that feels the intake pain, and the primary row in the template.

**Per-Persona Lines, Cemetery General Manager (Drafts Left Off The Page):**
- Displacement Angle: one view of sold and unsold plots and the trust record, so the buyer sees the state filing in one place.
- Best Discovery Question: "Where does the plot map live today, and when was it last updated?" (template question 1)
- Why Selected: the buyer who signs the contract, and the secondary row in the template.

**Step 4. Summary:**
1. **Company:** Greyfield Memorial Park. Stonemark identified.
2. **Incumbent Type:** direct software.
3. **Displacement Difficulty:** Medium, set by the renewal test (1 of 3 tests met, directional).
4. **Readiness:** pre-need and records pain is known, and the champion, budget cycle and prior evaluation are `[Unknown]`.
5. **CRM Status:** TARGET, one touch on 2026-09-24 with no named contact, no open deal, no AE owner, no contacts on file.
6. **Personas Targeted:** 2 of 5 profile rows, the two that feel the intake pain and sign the contract.
7. **Sequences Generated:** 2 personas x 4 emails. Email 1 is shown in full. Email 3 is on HOLD. Emails 2 and 4 follow the structure above.
8. **Strongest Opening:** "Your team takes pre-need requests through the intake form on the site."
9. **Key Displacement Lever:** pre-need leads and records on one system.
10. **Contract Timing:** January 2027, `[CRM]`. Email 4 confirms it.
11. **User Role:** BDR.
12. **Coordination Note:** none. TARGET accounts are worked.
13. **Evidence Tags Used:** `[CRM]` for the incumbent and the renewal, `[Public: deathcare research, 2026-03-27 to 2026-04-01]` for the held research figure, which is in no email, `[Public: Greyfield Memorial Park website]` for the intake form, `[Unknown]` for the contacts, the budget cycle and the exit fee. No `[Inferred]` claim is in an email.

Not written on this page: Displacement Hooks, Product Against Incumbent, Objection Handling and Call Flow, which no step produces. The wedge in Step 2 carries the hook.

Hand-off (read by 02 and 06):
account: Greyfield Memorial Park (TARGET)
run_date: 2026-10-19
incumbent_type: direct software (Stonemark)
displacement_difficulty: Medium (renewal inside 180 days, January 2027, test met, directional)
target_personas: 2 of 5. Row 2 Pre-Need Sales Manager (primary). Row 1 Cemetery General Manager (secondary). Contacts [Unknown]
sequence: 2 personas x 4 emails. Pre-Need Sales Manager Email 1 drafted. Email 3 on HOLD until the Illustrative proof point is Verified
report_path: none (inline)
next_action: Nadia Brandt finds the Pre-Need Sales Manager's name, reviews Email 1, and sends it by 2026-10-26

---

### Example 2: Manual-Process Displacement, Tamsin Vale Cemetery (Non-Success)

**Context:** Tamsin Vale Cemetery is a one-site cemetery with 4,200 plots, paper plat maps and one binder per section. It has had two double sales in two years (illustrative). The account is TARGET, not yet contacted, and its verdict is MANUAL REVIEW (Zone 1 HIGH only). This is the non-success case. The displacement is easy to describe and hard to justify yet.

**Input:** "Tamsin Vale Cemetery runs paper plat maps. Build displacement sequences."

**Step 0. Role And Status:** User is a BDR (illustrative). CRM check: TARGET, no open deal.

**Step 1. Identify The Incumbent:** Incumbent: paper maps and binders, a manual process. How we know: the CRM record holds paper plat maps `[CRM]` (illustrative). Confidence: MEDIUM, because the record is partial. No buyer has confirmed the process on a dated call, and the double sales are not yet in writing.

**Step 1d. Displacement Readiness:**
- Known Pain: Suspected. The two double sales have not been counted in plots or dollars.
- Contract Status: none `[Inferred: a manual process has no vendor contract to time against]`.
- Champion: `[Unknown]`
- Budget Cycle: `[Unknown]`
- Previous Evaluation Of Our Product: `[Unknown]`
- Decision Path: the GM recommends, and the board approves above $25K. Its next meeting is 2027-02-10 `[CRM]`. No signer is named, so the economic buyer is `[Unknown]`.

**Step 1e. Displacement Difficulty: Low.**
- Low test (no contract term to exit): met, the account has no contract to exit.
- Medium test (renewal inside 180 days): not met, there is no renewal.
- High test (term past 180 days with an exit fee): not met, there is no contract.
- The rating is Low, the highest test met. The test is directional.

**Step 2. Template Row And Intelligence:** The profile's manual process row for Displacement says the wedge is one view of sold and unsold plots with an audit trail, so no one person holds the records (profile: Displacement). Primary persona: row 1, Cemetery General Manager. Secondary persona: row 3, Operations Director, with no contact on file, so its contact is `[Unknown]` and its title is kept. Gap matrix: no single view of sold and unsold plots (one binder per section), no audit trail, and key-person risk. The only proof point is Fennick Gardens, which is Illustrative and cannot be cited.

**Step 3. Sequences:** Persona selection: 2 of 2 template personas. Row 1 Cemetery General Manager is primary, and row 3 Operations Director is secondary, with its title kept and its contact `[Unknown]`. A CFO is not a fit for a single-site account (the CFO row applies to groups, profile: Buyer Personas). That is 2 personas and 8 emails, all on HOLD until the two double sales are in writing. The Cemetery General Manager's Email 1 is shown below. The other seven drafts follow the same rules and are left off this page for length.

**Cemetery General Manager, Email 1 (Pain Question). Drafted, held.**
Subject: Plot lookups across one binder per section

Tamsin Vale keeps its plot records in one binder per section. When a family asks about a plot in another section, how long does the lookup take?

Your name

**Step 4. Summary And Recommendation (The Non-Success):** 2 personas, 8 drafts, 0 sent, all on HOLD. Recommendation: hold the sequence. The verdict is MANUAL REVIEW, not GREENLIGHT, so Email 1 would put a double-sales question in front of a buyer before anyone has confirmed the double sales. The next step is to find the Cemetery General Manager's name and phone number, then ask for the two double sales in writing, with plot numbers and dates, and ask who decides. The CRM record places that decision with the board above $25K. Release Email 1 only after both are in hand. Evidence tags: `[CRM]` for the process and the touch record, `[Inferred]` for the displacement case, and `[Unknown]` for the decision maker's name. If the double sales do not hold up, the displacement case is a guess, and it does not go out.

Hand-off (read by 02 and 06):
account: Tamsin Vale Cemetery (TARGET)
run_date: 2026-10-19
incumbent_type: manual process (paper plat maps and one binder per section)
displacement_difficulty: Low (no contract term to exit, test met, directional)
target_personas: 2 of 2. Row 1 Cemetery General Manager (primary). Row 3 Operations Director (secondary), contact [Unknown]
sequence: 2 personas x 4 emails, 8 drafts, 0 sent. All on HOLD until the two double sales are in writing
next_action: Nadia Brandt finds the Cemetery General Manager's name and phone number by 2026-10-26, five business days after the run date of 2026-10-19
report_path: none (inline)

---

### Example 3: The BDR Guard, Brackhaven Memorial Gardens

**Context:** A BDR finds that Brackhaven Memorial Gardens runs Oldgate Ledger Pro, a direct software incumbent with its renewal in March 2027 `[CRM]`. The account is ACTIVE at Stage 5 Negotiate, since 2026-09-09, and the AE owner is Owen Pruitt. The BDR is Nadia Brandt (illustrative).

**Input:** "Brackhaven runs Oldgate. Build displacement sequences."

**Step 0. Role And Status:** User is a BDR. CRM check: ACTIVE, Stage 5 Negotiate, owner Owen Pruitt.

**THE BDR GUARD IS TRIGGERED.** The BDR does not get sequences on this account. Step 3 is skipped, the analysis goes to the AE, and the summary in Step 4 records the guard.

**Steps 1 And 2. Analysis Delivered:**
- **Incumbent:** Oldgate Ledger Pro, direct software. Confidence: HIGH, because the CRM records the incumbent `[CRM]`.
- **Difficulty:** Medium. The renewal test is met: March 2027 is inside 180 days `[CRM]`. Directional.
- **Gap Matrix:** mobile use by the grounds crew `[Inferred: research pattern for legacy on-premise systems, illustrative]`, unsold-plot visibility, where Oldgate shows sold records only `[Call, 2026-05-19]` (illustrative, the row the Competitive Strategy skill cites), and trust fund records, which need a deeper accounting answer.
- **Discovery Questions For The AE** (both from the profile: Competitive Landscape): "When does your software contract renew, and what did the last quote include for support?" and "Where does the plot map live today, and when was it last updated?"
- **Proof Point:** Fennick Gardens is Illustrative and cannot be used.

**Coordination Guidance:** "Active deal owned by Owen Pruitt at Stage 5 Negotiate. Share this displacement analysis with Owen and let him decide how to use the March 2027 renewal in his conversations with Ruth Ellery. Do not send sequences independently. The competitive strategy for this deal is in gtm-competitive-strategy."

Hand-off (read by 02 and 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate)
run_date: 2026-10-19
incumbent_type: direct software (Oldgate Ledger Pro)
displacement_difficulty: Medium (renewal inside 180 days, March 2027, test met, directional)
target_personas: none. BDR guard, analysis only
sequence: none (guard). The AE decides
next_action: Nadia Brandt sends this analysis to Owen Pruitt by 2026-10-26
report_path: none (inline)

---

## Common Patterns

### Pattern: The BDR Guard On An Active Deal
**When:** The user is a BDR and the account is ACTIVE with an AE owner.
**Action:** Produce the analysis only, in Steps 1 and 2. Name the AE and the stage. Say "Share this displacement analysis. Do not send sequences independently."

### Pattern: Unknown Incumbent
**When:** The user suspects a competitor but is not sure of it.
**Action:** Run `gtm-account-snapshot` first to find the incumbent through CRM notes, job postings or discovery questions. Then return here with a confirmed incumbent.

### Pattern: Dual-Tool Pain
**When:** The account uses two separate tools, one for each job.
**Action:** Build the displacement around the unification angle. Use a proof point where one product replaced both tools, and only if its Status allows it.

### Pattern: Contract Renewal Window
**When:** The contract renewal date is known.
**Action:** Time the sequence to arrive 60 to 90 days before renewal. Change Email 4 from asking when the contract renews to saying the renewal is the reason to look now.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| No competitive intelligence exists for this incumbent | The profile's Competitive Landscape has no row for it | Use general positioning, tag it `[Inferred]`, and build the intelligence from the discovery call |
| The prospect is in an active contract | The term is unknown, or it runs past the window | Email 4 asks about timing. Frame the outreach as "evaluate before your next renewal," never as "break your contract" |
| A BDR wants sequences on an AE's active deal | The BDR guard applies | Send the analysis to the AE. The AE decides how to use it |
| Incumbent Confidence Is MEDIUM | The incumbent is suspected, not confirmed | Proceed. Make discovery question 1 validate the incumbent, and open Email 1 with a broader industry angle |
| Several Contacts Name Different Tools | Tools vary by branch or division | Build around the most-named incumbent, and add a discovery question about standardization |
| The rating is Low but the deal feels hard | The Low test is directional and measures the contract, not the win | Say so in the report. A Low rating means the positioning is favorable, not that the deal is easy |
| Every number in a draft is cut | The sources are not named or dated | Cut the figure and ask the question. Add the number back only when its named, dated source is in hand |

---

## Best Practices

- **Lead with enablement, not criticism.** "Here is what is possible" beats "here is what is broken," because the buyer is the one who has to defend the current choice.
- **Use proof points that match.** A customer who made the same switch is the strongest line in a sequence, if its Status is Verified.
- **Ask gap-exposing questions.** Genuine curiosity surfaces pain better than an accusation.
- **Address contract timing in every sequence.** Each sequence should discover or use the renewal window.
- **Tag every claim.** A reader should be able to see which claim is `[CRM]`, `[Call]` or `[Public: source]`, and which is only a question.
- **Personalize the gap matrix.** Connect each gap to this account's situation, not to the category.

---

## Integration With Other Skills

**Reads From The Skill Before It, By Field Name:**
- **`gtm-competitive-strategy`** (11): `incumbent_type`, `threat_level`, `gap_matrix`, `battlecard`, `win_plan`. When 11 has run on this account, start from its `gap_matrix` and use its `win_plan` to match the wedge to the team's plan. Use `threat_level` to set how direct the sequence is. When 11 has not run, Steps 1 and 2 build the same fields here.

**Hands To The Skills After It, By Field Name:**
- **`gtm-account-snapshot`** (02): `incumbent_type`, `displacement_difficulty`, `target_personas`, `sequence`. Snapshot orders its contacts by `target_personas`, and writes no sequence for a persona that already has one here.
- **`gtm-meeting-prep`** (06): `incumbent_type`, `displacement_difficulty`, `target_personas`, `sequence`. Meeting Prep uses `incumbent_type` in its competitive objections.

**Hands To The Close:**
- **Wrap-Up** reads `report_path` when a file was written, the `displacement_difficulty` or verdict the session produced, and `next_action` with its owner and date.

### Chains

- **Beat The Incumbent:** MEDDPICC Analysis (09), Competitive Strategy (11), **Competitive Displacement (12)**, Account Snapshot (02) or Meeting Prep (06). This skill adds the outbound plan to displace a known incumbent: a difficulty rating and the sequences the rep reads and sends.

---

## Changelog

### 2.1.8 (2026-10-26)
- Citations. A fact taken from the profile is cited (profile: Section) with the profile's own section name, in place of [Notes]. A rep's or AE's own notes keep [Notes].
- ENGAGED. An ENGAGED account (two-way contact, no open deal) gets a reply plan in Step 0 instead of the four-step cold sequence, and Hard Rule 9 bars a cold sequence for it. The status list in the Input Contract names ENGAGED.
- Status. Greyfield's Example 1 now states that its single touch on 2026-09-24 has no reply on record at the run date, so the status is TARGET and the sequence is drafted.
- Headings and labels are capitalized word by word.
- The example sequences, difficulty ratings and next actions do not change.

### 2.1.7 (2026-10-26)
- Leak scrub. The next action rule in the Output Contract is written as owner, action and date, in place of a worked sentence, and the Example 1 record of the verdict and the zone facts is restated as facts with their tags.
- Settled: a research figure dated more than 90 days before the run date is not used in any email, so Email 1 in the example names no figure and asks the question. The Email 1 row of the sequence structure names the 90-day limit.
- Settled: a known renewal month with an unknown term is a known term end, so the unknown-term rule does not apply, and an unknown exit fee does not raise the rating.
- Settled: a CRM owner name is written with its tag, and a blank owner keeps the role.
- Settled: the wedge is one sentence with no roadmap figure. Dangling example references are reworded, and the profile labels in the example carry the evidence tags of their source.
- The example's rating, personas, sequence count, hand-off and next action do not change.

### 2.1.6 (2026-10-26)
- Greyfield's contact status reads the logged touch of 2026-09-24 with no named contact, in place of not yet contacted.
- Tamsin Vale's second example relies on the CRM record only. The incumbent, the decision path and the contract term (none) are cited to it, and the buyer call is removed. The persona count is two of two, with eight drafts on hold.
- Oldgate's unsold-plot visibility in the third example cites the dated call row in the Competitive Strategy skill.

### 2.1.5 (2026-10-26)
- The competitive research citation is flagged as research estimate, over 90 days old at the run date, and an Epistemic Rule states the flag.
- The next action follows the family's one deadline rule. The Output Contract points to that rule in place of the skill's own four-business-day wording.
- The examples' next actions carry the dates the rule gives. No sequence or difficulty rating changes.

### 2.1.4 (2026-10-26)
- Try-it fixes from the blind retest. The Output Contract names the parts the steps produce and the four the steps do not produce. The next action takes a date rule and an action verb. The Context names the example profile for a first run. A CRM note confirms the incumbent only when its text names it. The hand-off block is defined. The competitive research is cited by its Sources name. Settled Judgments records the open judgments, and an illustrative figure never goes into an email. The Example 1 page leaves out only the sections no step produces.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The Pre-Need persona carries its displacement angle, best discovery question and selection reason, and the Cemetery General Manager block carries the same three lines. Each Unknown gap row names the question that would settle it. The Wedge drops its 90 to 120 day figure, and the Time to Live row names its research source. Email 3 names its unlock date. The output contract states which sections and drafts a run leaves off the page, the owner rule for the next action, and the hand-off ends with next_action.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. An unnamed contact is an Unknown champion, Example 1 states which drafts are left off the page, and the next action reads as the rep reviewing and sending.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1.

### 2.1.0 (2026-10-25)
- Reads the Context OS base (the account's folder under `accounts/`, the competitors under `gtm/` and the personas under `people/`) and offers read-only CRM connectors through the shared contract's Knowledge Base and Connectors section, before the CRM read.
- Adds a Chains subsection placing the skill in the Beat The Incumbent chain.

### 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 standard: Overview with Core Principle and the platform line, Why This Skill Exists, Role, Input and Output Contracts, Context with the Shared Contract, a Core Workflow with a Produces line per step, Epistemic Rules, Hard Rules with reasons, a Quality Bar, and hand-offs named by field.
- Adds a displacement template per incumbent type (Positioning, Wedge, three discovery questions, and the primary and secondary persona rows), read from the profile's Displacement section.
- Adds the Low, Medium and High difficulty scale, with one directional test each. The rating is the highest test met, and an unknown term rates High.
- Proof points gain Displaced vendor and Status columns, which the skill reads from the profile. Customer rows stay in the profile.
- Every number in an email needs a named, dated source or it is removed. Greyfield Email 1 now names its benchmark source and date, which was the unsourced trend line.
- The persona count is read from the profile's Buyer Personas table and written as n of N.
- The BDR guard is a Hard Rule with its reason, and an account pending AE assignment is worked and marked pending.
- One Epistemic Rules section, with one Confidence subsection. The evidence grades are replaced by the six tags.
- Integration reads 11's fields by name and hands to 02 and 06 by name.
- The old output-format section is removed. The file option is in the Output Contract and is written only when asked.
- Examples: Greyfield, Tamsin Vale and Brackhaven now use the six tags, the stage words, and a hand-off block ending each one.

### 1.3.0 (2026-10-13)
- Examples re-cast on the PlotIQ example company. Example arithmetic and listed errors fixed, and a non-success example added.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around an earlier example company.
- Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology.
- Client-specific data de-embedded: the skill reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block.
- Framework machinery (Epistemic Rules, Confidence Calibration) moved to an explicit Methodology section.
- No functional changes to the workflow, examples, or output formats.

### 1.0.0 (2026-03-04)
- Initial release.
- Generalized through a Client Profile block with configurable defaults.
- Preserved the competitor intelligence structure, failure patterns, discovery questions, and proof points.
- Kept the BDR Active Deal Guard pattern.
- Multi-format artifact generation.
