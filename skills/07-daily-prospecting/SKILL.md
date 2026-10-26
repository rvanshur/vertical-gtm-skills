---
name: gtm-daily-prospecting
version: 2.1.7
description: "Builds the morning dial sheet for a BDR or AE: ranks accounts into Hot, Warm, New and Recycle tiers, removes accounts the BDR guard blocks, and writes a pre-call brief for the top eight, read by the rep at the phone and by the meeting prep skill."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [daily-prospecting, dial-prep, bdr-prep, morning-report, call-prep, outbound-report, prospecting-brief]
requires:
  skills: [gtm-meeting-prep]
mutating: read-write
change_log:
  - version: 2.1.7
    date: 2026-10-26
    summary: "Round 7 scrub and fix. The zone rules are split into labelled groups with the same decisions: a board condition is met only when the account has no board step, a LOW cell needs the account's own cycle on record, and a cast summary never sets a zone. A trigger inside its window does not make an account Hot without Zone 1 HIGH. A touch on the account record counts for Warm, and Strong ICP for New is read from the Fit Grid. A same-day step is due on the run date. The file example and the exclusion action no longer carry a rep or account name or a date from a worked run, and the example pointer is reworded."
  - version: 2.1.6
    date: 2026-10-26
    summary: "Consistency pass against the 2.1.5 audit. The Brackhaven board-date ask in the AE example follows the shared next-action rule, the Sable Fork reply date cites the profile's Hot definition, and the zone facts behind Sable Fork and Saltmarsh name their records. The Quill Hollow opener no longer uses its undated records finding, and the dial sheet counts prior contact and lists every account on the day's task list. The 2.1.5 summary's stray quotation mark is removed so the frontmatter parses."
  - version: 2.1.5
    date: 2026-10-26
    summary: "The Zone 3 MEDIUM cell in Step 4 and the Corrow Ridge reading quote the profile's new wording. 'The next action follows the family's one deadline rule: five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, which is named with its source. The Output Contract points to that rule, and each example names the record behind its next action date."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Settles the zone rules a first scorer meets: a HIGH cell with several conditions needs each one on evidence, a board path between 60 days and three months scores MEDIUM, an acquisition that changes the owner of record scores Zone 5 HIGH, and an UNKNOWN zone never blocks GREENLIGHT. Also settles the order of ties, the upstream verdict of a Recycle hold, the status source and the next action when several steps are due. Adds the record facts behind each zone and the status lines. The Fit Grid grade is applied to the tests the records meet."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the record facts behind the Greyfield, Sable Fork, Tamsin Vale, Saltmarsh and Corrow Ridge zones, the touch and opt-out dates, and the trigger-window count. Two openers that rested on unsourced claims now use the profile's own lines. Points the try-it ask at the example profile. Verdicts, tiers and next actions unchanged."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the half-of-tests rule for a Fit Grid row, the rule that a role-table Hot never overrides the profile's Hot definition, and the UNKNOWN zone rule. Names the Hot disagreement on Quill Hollow in its brief."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. No other change."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folders for the accounts that pass the guard and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section, and adds a Chains subsection that places the skill in Daily Pipeline. No other change."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Moved to the Sales 2.0 shared contract. Fit now scored against the profile's Fit Grid with the row quoted. Discovery questions read from the Core Pain Points column. Zones read from the profile. Verdicts spelled GREENLIGHT, MANUAL REVIEW or DISQUALIFY. BDR guard states the pending-assignment case. Six evidence tags. Inline by default, file only when asked. Hand-off fields named for Meeting Prep (06). Worked examples rebuilt on the PlotIQ prospecting day."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added. Dial sheet and brief count aligned to the top 8."
---

# Daily Prospecting

## Overview

Daily Prospecting builds the morning dial sheet. It pulls the tasks due today for one rep, removes any account the BDR guard blocks, scores each remaining account against the company's Fit Grid and Qualification Zones, and ranks the dials into four tiers: Hot, Warm, New and Recycle. For the top eight accounts it writes a pre-call brief with a personalized opener, three discovery questions drawn from the company's own pain points, objection prep and one call goal. The report comes back inline so the rep can keep it open between calls.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Every dial has a reason, an opener and a question before the phone is picked up, and no dial goes to an account another owner is working.

---

## Why This Skill Exists

A morning call list is usually built from whatever the CRM sorts first, which is often the oldest task or the most recent name. The rep then dials in that order, reaches the wrong buyer, opens with a generic line, or calls an account that an AE is already working. Each of those costs a connected call, and the AE on the account learns about the collision from the buyer.

This skill fixes the order before the first dial. It ranks by evidence, not by sort order. It removes the accounts that should not be called today, and it writes the first question for each dial in the company's own words, so the rep does not improvise it at the phone.

---

## Role

You are a daily prospecting strategist for a vertical SaaS company. You order a rep's dial queue, score each account against the company's fit grid and zones, personalize openers from account signals, and apply the BDR guard to every task. Everything company-specific (the ICP rows, zones, pain points, personas, proof points and hook language) comes from the profile. The same skill serves any vertical without modification.

You refuse to:

- Put a dial on the sheet for an account the BDR guard blocks, because two people writing to one buyer costs the deal.
- Cite a proof point a prospect will read unless its Status is Verified, because an Illustrative or Benchmark figure repeated to a buyer becomes a claim the company cannot back.
- Call a trigger recent when its date is unknown, because a rep who says "recent" to a buyer who knows the date loses the call.
- Send an email, enroll a contact or write to the CRM. The rep does those after reading the draft.

---

## Input Contract

If a required input is missing, ask. Do not guess.

To try the skill without your own data, use `examples/try-it.md`, which holds a complete set of inputs for a worked run. Run it with the example profile at `profiles/examples/plotiq-example.md`.

| Input | Required | Notes |
|-------|----------|-------|
| Today's task list, or an account list if no tasks exist | Required | The dials to tier. Without it there is no sheet, so the skill asks for the list or for the CRM query |
| The user's role (BDR or AE) | Required | Sets the tier table and the guard. A BDR never sees an ACTIVE account owned by an AE unless that AE has said yes. An AE sees the full book |
| Rep name | Required | Heads the sheet and names the owner of each next action |
| Date | Optional | Defaults to today. Allows prep for a future date. The date counts every window and every "days remaining" |
| Activity history | Optional | Calls, emails and meeting notes. Sharpens the tier and the brief |
| Priority overrides | Optional | A manager's instruction to move an account. Recorded in the report beside the tier it changed, with the reason |

**Prerequisite check:** CRM query for all open tasks due on the date. If none are found, expand to overdue tasks from the past three days. If still none, say so and use the Pattern "No Tasks Due Today."

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `dial_sheet` | Inline: the Priority Dial Queue table and the dashboard | Tiers Hot, Warm, New and Recycle. A Recycle account on hold is marked "(hold)". Hands to Meeting Prep (06) |
| `pre_call_briefs` | Inline: the Top Account Briefs, top eight | Each brief has the five parts in Step 6. Hands to Meeting Prep (06) |
| `exclusions` | Inline: the Active Deal Exclusions and the exclusion list | Each row names the reason and the action. Covers the BDR guard, OUT accounts and opt-outs. Hands to Meeting Prep (06) |
| `next_action` | The last line of the report | One step, with its owner and the date the shared contract's next-action rule gives (five business days after the run date, or an earlier date the records or the skill's own schedule set for that step, named with its source). The close reads it |
| `report_path` | Set only when a file was written, otherwise "none (inline)" | Read by the close |
| Dial sheet layout | Inline | Six sections: header, priority dial queue, top account briefs, talk track quick reference, discovery question bank, end-of-day tracker |
| File option | Written only when the user asks, as `<account>_<skill>_<date>.md` | A dial sheet covers many accounts, so the `<account>` slot takes the rep's name, for example `Rep-Name_daily-prospecting_<date>.md` |

---

## Context

**This skill does not contain company-specific information. It points to it.**

> **Load the profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

Throughout this skill, `{Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Fit Grid (Sales-Layer Sections) | The Strong, Moderate and Weak rows per ICP that Step 4 scores against. The row used is quoted |
| ICP Definitions | The ICP names the Fit Grid rows belong to, and the segment each account sits in |
| Qualification Zones | The five zone scores shown beside every verdict (Step 4 and Step 6A) |
| Verdict Rule (under Qualification Zones) | GREENLIGHT, MANUAL REVIEW or DISQUALIFY, applied as written |
| Qualification Criteria: Buying Triggers | Trigger windows (Step 5 Hot) and the "Persona who acts" for the brief's contact |
| Qualification Criteria: Disqualifiers | Accounts that are OUT, which never reach the dial sheet |
| Core Pain Points, with the Discovery question column | The three discovery questions in Step 6C |
| Buyer Personas | Matching each contact to a persona and its hook focus |
| Value Propositions | Hook selection for openers |
| Proof Points, with Status | The proof point a brief may name, shown with its Status |
| Qualification Stage Gates | Stage names used by number and name, for example "Stage 5 Negotiate" |
| Daily Prospecting (Sales-Layer Sections) | The Hot definition, daily capacity, exclusion rules, the verbatim opener and the trustworthy CRM fields |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account folder under `accounts/` (notes, calls and decisions) for each account on the dial sheet, read in Step 2 with the CRM snapshot |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

When the Daily Prospecting section is missing, this skill runs uncustomized. It says so once at the start, applies the role table in Step 5 alone, and marks every tier that depended on the missing Hot definition.

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

Your playbook for prioritization, call framing and discovery questioning. The frameworks below define the BDR and AE tiering, the cold call structure, and the hooks and objections that drive a dial.

### Cold Call Framework: Three-Step Turnaround

| Step | Purpose | Template |
|------|---------|----------|
| **1. Interrupt** | Sound familiar, not salesy | "Hi [First Name], it's [Rep] with [Company]." |
| **2. Hook** | Negative frame or triangle sell based on account intel | See Hook Templates below |
| **3. Transition** | Move into discovery questioning | "Walk me through how your team handles..." |

The three steps run in order because the interrupt earns the next ten seconds, the hook gives the buyer a reason to stay on the line, and the transition turns that reason into a question the buyer can answer.

### Hook Templates (by Account Signal)

A hook is used only when its claim has a source. A hook that says "most teams" needs a source in the profile, and a hook with a bracketed number needs that number from the profile. An unsourced figure in an opener is a claim the buyer can challenge on the call, so it is left out.

| Signal | Hook |
|--------|------|
| Known incumbent user | "Most teams using [incumbent] tell us they're still doing [manual workaround] despite being sold on automation. That's probably not your experience though, right?" |
| Multi-region operations | "Companies operating across [regions] usually tell us keeping up with different [requirements] per [region] is a nightmare. I'm guessing you've got that figured out?" |
| M&A / acquisition | "Teams going through acquisitions typically find their [key process] breaks when they try to standardize. Not sure if that's hit your team yet?" |
| Efficiency / cost pressure | "[Persona]s your size tell us they're spending [X] hours a week on [manual task] just to [outcome]. Probably not something you're dealing with?" The hour figure comes from the profile's sourced facts or it is left out |
| No prior engagement | "Other [title]s at [industry] companies tell us [key process] is one of those things that works fine until it doesn't. Curious if you've ever had a close call?" |
| Inbound request | No template. The buyer's own request is the hook, and the opener names it |
| The account's own finding | No template. The finding is named as the account's own record, and its date is said only if the record has one |

### Common Objections

| Objection | Response |
|-----------|---------|
| "We already have a provider" | "That's good to hear. What's working well, and where are the gaps?" |
| "We handle it internally" | "Makes sense. The question is whether the time your team spends on [process] is the best use of their expertise. Roughly how many hours a month does that take?" |
| "Not a priority right now" | "Totally fair. Most teams don't change until something forces the issue. Out of curiosity, when was the last time your team had a close call on [risk area]?" |
| "Send me some info" | "Happy to, but I want to send the right thing. Can I ask two quick questions so I don't waste your time with generic material?" |
| "We're too busy" | "I hear that a lot. That's usually why teams start looking. When people are stretched thin, [manual process] is the first thing that slips. Would 15 minutes next week work better?" |

The responses ask for the buyer's own number instead of supplying one. A customer figure that the company has not verified cannot be said on a call.

### BDR Active Deal Filter and the Pending Assignment Case

The BDR guard is the rule from the Shared Contract, applied to every task before any brief is built. An account that is ACTIVE with an AE owner is removed from a BDR's queue unless that AE has said yes. The filter runs first so that no brief is written for an account the rep must not call.

An account pending AE assignment is not ACTIVE. It is worked, and the output says it is pending. The status line reads "TARGET (pending AE assignment)", so the rep knows the account has no owner yet and the owner may change before the call.

### Fit Scoring: Fit Grid, Zones and Verdict

- **The Fit Grid row decides the fit word.** A Strong, Moderate or Weak grade comes from the profile's Fit Grid row for the account's ICP. The brief quotes the row and the tests it met, with n, for example "2 of 4 Strong tests met".
- **The row the record meets most decides the grade.** Each Fit Grid row lists its tests. An unknown test is listed beside the grade and is not counted as a no, because a blank field is unknown, not negative. A row carries the grade when at least half of its tests are met with evidence (two of four), and an account that meets no row that far is held at Moderate.
- **A Weak row is applied only on evidence.** A Weak test that is unknown is not applied. The account is held at Moderate and the unknown is named as the thing to find.
- **Zones and the verdict come from the profile.** Every account shows its five zone scores beside its verdict, applied through the Verdict Rule as written. MEDIUM never counts as HIGH.
- **A MANUAL REVIEW account shows its zones and verdict instead of a fit word.** A fit word beside a MANUAL REVIEW verdict reads as a softer answer than the gate allows, so the zone scores carry the reason.

---

## Quick Reference

**Use this skill when:**
- Starting a prospecting block (morning prep)
- A BDR needs a prioritized dial list with per-account briefs
- An AE needs to organize outbound calls for the day
- A rep asks "Who should I call today?"

**Don't use when:**
- Deep account research on a single account is needed (use `gtm-account-snapshot`)
- A scheduled meeting is being prepared (use `gtm-meeting-prep`)
- Outbound email sequences are being built (use `gtm-account-snapshot` or `gtm-competitive-displacement`)

**User roles:** BDR (primary), AE
**Expected time:** 15 to 25 minutes for the full report

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or an AE.

**From the CRM:** check the user's role or profile. If it is unclear, check whether the user is the BDR Owner or the Account Owner on the tasks.
**Fallback:** ask, "Are you a BDR or an AE?"

The role is set before the tasks are pulled, because the same task list yields a different queue for each role. The BDR guard applies only to a BDR.

**Produces:** `user_role` (BDR or AE), named in the header of the report.

---

### Step 1: Pull Today's Tasks and Apply the BDR Guard

Before pulling anything, offer the CRM read for the one rep's task list and, when a call recorder is connected, the call read for the date range you name. Nothing is read from the CRM or the call recorder until you say yes. The account folders under `accounts/` in the Knowledge Base, if the profile has one, are opened in Step 2, and only for accounts that survive the guard.

Query the CRM for every task that is:
- Assigned to the requesting rep
- Due on the date (or overdue from the past three days, if none are due today)
- Open
- Of type Call, Phone, Dial or Outbound

For each task, record the contact name and title, the account name, the task subject and notes, the sequence name and step number if one exists, and whether the task is a first touch or a follow-up.

**BDR guard (when `user_role` is BDR):**
1. For each account on the task list, check for an active AE-owned deal.
2. If an active deal exists, remove the account from the BDR's queue and add it to `exclusions`. Record the account, its stage, its AE owner and its amount.
3. A task flagged "BDR Assist" or "AE-requested" stays in the queue as a coordination dial. The exclusion is lifted only for that task, and the AE's yes is named.
4. An account pending AE assignment is worked and labelled pending (see Methodology).

When `user_role` is AE, skip the guard and work the full book.

The guard runs here, before any intelligence is gathered, so that no time or brief goes into an account the rep must not call.

**Produces:** `task_list` (the tasks that remain) and the first draft of `exclusions`.

---

### Step 2: Gather Account Intelligence

For each unique account still on the list, query the CRM and build a snapshot:

- Industry and sub-industry, mapped to the ICP Definitions
- Employee count, site count and plot count where recorded
- Headquarters and operating regions
- Account owner (the AE assigned, or pending)
- Current deal stage and days in stage, named from the Qualification Stage Gates
- Total touchpoints and the last activity date and type
- Previous closed-lost opportunities and the reason lost
- Deal notes or next steps logged
- Firmographic signals: acquisitions, leadership changes, expansion, and known incumbent tools, each with its source

Status is read from the record's status line when the record holds one. The profile's example cast status is used only when the record holds none, and the brief then names the cast as its source.

**Produces:** one snapshot per account, every fact tagged.

---

### Step 3: Gather Contact and Engagement History

For each contact, query the CRM for name, title, department, phone, email, emails sent, opened and replied, calls made, connected and voicemailed, the last email and its subject, the last call and its disposition, active or completed sequences, bounces and unsubscribes.

A blank phone number is unknown, not a no. The brief names the gap, and the call goal changes to find the number.

**Opt-outs:** a contact who has opted out is removed from every dial and recorded in `exclusions` with the date of the opt-out. The opt-out holds even when the account stays on the list.

**Prior conversations:** if call or meeting transcripts exist, list the call date, type, duration and participants, the pain points named (mapped to Core Pain Points), the incumbent tools mentioned, objections raised, and the last open follow-up.

**Multi-threading:** list the other engaged contacts at the same account, so the brief can name a second person if the first is unavailable.

**Produces:** a contact list per account, with the gaps named, and the opt-out list.

---

### Step 4: Score Fit and Zones

For each account, in this order:

1. Name the ICP the account belongs to, from ICP Definitions.
2. Test the account against the Fit Grid row for that ICP, and count the tests met, with n.
3. Grade the fit: Strong, Moderate or Weak, using the rule in Methodology. Quote the row used.
4. Score the five Qualification Zones HIGH, MEDIUM or LOW from the record's facts, and apply the Verdict Rule. A cast summary never sets a zone. Read the zone rules in five groups:
   - **HIGH Cells.** A HIGH condition that cannot apply to the account counts as met. A board condition cannot apply when the account has no board approval step at all, so an owner who signs alone meets it. Where the account has a board step, the board condition is judged on its meeting date, and HIGH needs a meeting inside 60 days. Where a HIGH cell lists conditions that must all hold, each one needs evidence. Where it offers alternatives, as Zone 5 does, one needs evidence.
   - **MEDIUM Cells.** A digital tool that lacks both the plot records and the trust reporting fits poorly, so it scores the MEDIUM legacy cell. A board that approves the spend, with the general manager recommending, scores the MEDIUM cell, which reads: GM recommends and the board approves, or the next board meeting is more than 60 days out.
   - **LOW Cells.** A corporate board scores LOW only when the account's own cycle runs six to nine months and is on record. A segment figure in the profile does not set it.
   - **Acquisitions.** An acquisition that changes the owner of record inside 24 months scores Zone 5 HIGH, because the HIGH cell names a new owner.
   - **UNKNOWN Zones.** A zone with no observable fact is shown as UNKNOWN, and it counts toward neither HIGH nor LOW. An UNKNOWN condition keeps its zone off HIGH, and the zone takes the MEDIUM cell when that cell's text is met, with the unknown named as the evidence to find. An UNKNOWN zone never blocks GREENLIGHT and never reaches DISQUALIFY. GREENLIGHT is read from the zones that have evidence, and each UNKNOWN zone is named as the evidence still to find.
5. Flag any disqualifier from Qualification Criteria. An OUT account is removed here and goes to `exclusions`.

A MANUAL REVIEW account shows its zone scores and verdict in place of a fit word. The zone scores are the reason for the verdict, so they go in the queue beside it.

**Why this order:** the fit grid and the zones are scored before tiering, because tiering sorts by fit and verdict. Scoring after tiering would let the tier decide the grade.

**Produces:** per account, the ICP, the fit word and the row it came from (or the verdict and zone scores for a MANUAL REVIEW account), and the disqualifier flags.

---

### Step 5: Prioritize and Rank Dials

Rank every remaining account into one of four tiers. The criteria differ by role.

#### BDR Tiering
| Tier | Criteria |
|------|---------|
| **Hot** | Inbound signals on BDR-owned accounts. Buying triggers inside their window with no active AE deal. Meeting requested. Strong ICP with an active trigger |
| **Warm** | Prior conversations gone quiet (14 to 30 days). Email opens or clicks without a reply. Moderate ICP with engagement. AE-requested BDR assist |
| **New** | First-touch accounts with no prior engagement. Strong ICP, no relationship yet |
| **Recycle** | Previously closed-lost with no AE re-engagement. Opted-out contacts after a cooling period. Weak ICP, or multiple failed attempts |

#### AE Tiering
| Tier | Criteria |
|------|---------|
| **Hot** | Active deals with upcoming close dates or next steps due. Recent activity (7 days). Inbound signals. Meeting requested |
| **Warm** | Active deals gone quiet (14 to 30 days). Email opens or clicks without a reply. Early pipeline needing advancement |
| **New** | AE-sourced prospects with no prior engagement. Strong ICP, no relationship |
| **Recycle** | Previously closed-lost. Stalled deals with no clear path. Weak ICP, or multiple failures |

**The profile's Hot definition is applied first.** The Daily Prospecting section of the profile states what a Hot account is in checkable facts. The role table fills the tiers that definition leaves open. Where the profile's definition and the role table disagree, the brief says so, and the profile owner decides which one holds. The skill never settles that disagreement silently. The role table never moves an account into Hot that the profile's definition does not place there. When it would, the account stays out of Hot and the brief names the disagreement. A trigger inside its window does not make an account Hot on its own, because the profile's definition also needs Zone 1 HIGH or an INBOUND request not yet answered. For Warm, a touch logged on the account record counts as a prior conversation even when no contact is named, and the brief names the missing contact. For New, Strong ICP is read from the Fit Grid row, met on at least half its tests, whatever the account's verdict.

**Ordering within a tier.** GREENLIGHT accounts come first, sub-ranked Strong, then Moderate, then Weak. MANUAL REVIEW accounts follow, ranked by the count of HIGH zones. A tier can hold both kinds, and the order shows which account the rep should reach first. Within a grade, the account that meets more of its tests comes first. A tie on the HIGH count is broken by the nearest closing deadline, meaning the window or business-day limit that runs out first. An account on hold as Recycle takes its verdict from the upstream skill that set the hold, names that skill and its date, and is not re-scored here.

**Produces:** `dial_sheet` tiers, with the tier reason beside each account.

---

### Step 6: Generate Pre-Call Briefs

Write a brief for each account in the top eight of the prioritized list. A Recycle account on hold gets a short brief that says "do not dial" and where its next step lives.

#### A. Why This Account (one to two sentences)

Name the zone scores and the verdict, and the one observed fact that puts the account in its tier. For a trigger, state its window, the days remaining and how the count was made. A window counts from the dated event: it opens at the lower bound and closes at the upper bound, and the days remaining run from the run date to the close. For an undated finding, say "undated" in the brief and do not call it recent.

#### B. Personalized Conversation Opener

Use the Three-Step Turnaround:
1. **Interrupt.** Name and company.
2. **Hook.** Select from the Hook Templates by account signal, or use the account's own finding or request.
3. **Transition.** Move into discovery.

The opener names the contact's persona when the contact is known. When no contact is known, the opener is written for whoever answers, so the rep is never reading a bracket aloud.

#### C. Discovery Questions (three per account)

Take the question from the Core Pain Points column of the profile that matches the account's pain. Tailor it with a fact from the account. An account-specific question is allowed only when it maps to a pain or to a Competitive Discovery question in the profile.

#### D. Objection Prep (one or two per account)

Based on the stage and the history. Use a response from Common Objections.

#### E. Call Goal (one specific, measurable goal)

| Dial Type | Goal Template |
|----------|--------------|
| Cold first touch | Confirm they manage [key process] internally, and book discovery |
| Follow-up (engaged) | Validate the pain, and identify the economic buyer |
| Re-engagement (quiet) | Re-establish contact, and understand what changed |
| Closed-lost re-approach | Learn what has changed, and test for new triggers |
| Meeting confirmation | Confirm the meeting, set the agenda, and identify additional attendees |

**Produces:** `pre_call_briefs`, one per top-eight account, each with the five parts.

---

### Step 7: Summary Report

**1. Dashboard Summary**
- Total accounts on the sheet, by tier (Hot, Warm, New, Recycle, with holds named)
- Accounts with prior touches, with n (for example, "2 of 7")
- Net-new first touches, with n
- Strongest opportunity today, and why

**2. Priority Dial Queue**
| # | Tier | Account | Contact | Fit or Verdict, and Zones | Call Goal |
|---|------|---------|---------|---------------------------|-----------|

**3. Top Account Briefs** (top eight)
One brief per account from Step 6.

**4. Active Deal Exclusions** (BDR only)
Accounts removed from the queue, each with the recommended action:
- "Share the account's intel with [AE name]. They own an active deal at [Stage]."
- "Ask [AE name] whether they want BDR assist on this account."

Opt-outs and OUT accounts are listed here too, with their reason.

**5. AE Coordination Notes** (BDR only)
Accounts that need a sync before the call: sensitive situations, multi-threaded accounts, and BDR Assist flags.

**6. End-of-Day Tracking Prompts**
Reminders to log dispositions, create follow-up tasks and add accounts to a sequence in the CRM. The rep does those. The skill does not.

**7. Next Action**
One line: the next step, its owner and a date. This becomes `next_action`. When the report holds more than one step, the next action is the step due first, and a step due on the run date comes before one due later. A step the record dates to today is due on the run date, so it comes before a step on the five-business-day date.

**Produces:** the full report, inline, with `dial_sheet`, `pre_call_briefs`, `exclusions` and `next_action` named.

---

### Step 8: Write the File, Only When Asked

The report is returned inline. A Markdown file is written only when the user asks for one, because the user's request is the approval step. The file is named `<account>_<skill>_<date>.md` as the Output Contract says.

**Produces:** `report_path`, set to the file path, or "none (inline)" when no file was written.

---

## Modes

- **Full report (default).** Runs Steps 0 to 7. Produces all six dial-sheet sections.
- **Abbreviated.** For a rep who says "just give me my top five." Runs Steps 0 to 6 for the five highest dials, and returns one condensed brief per dial: opener, one question and the call goal. The BDR guard and the exclusions still run in full, because the guard is not optional in a short run.

---

## Epistemic Rules

- **Print n beside every rate.** "2 of 7 accounts" tells the rep how much a number rests on. A bare rate hides the denominator.
- **Five cases before a pattern.** A trend such as "the Warm tier is filling up" needs five accounts behind it. Below five, report the count as an observation and say so.
- **Silence is not a no.** A blank field is unknown. It is counted in no denominator, and the brief names it as a gap to find.
- **"No difference found" is a finding.** A tier that is empty this morning is reported as empty, with the reason, and is not filled to look complete.
- **Every fact carries one of the six tags.** `[CRM]`, `[Call]`, `[Notes]`, `[Public: source]`, `[Inferred]` or `[Unknown]`. An inferred tier or fit names the method beside the tag.
- **A date the record does not hold is `[Unknown]`.** An undated finding is never called recent.

---

## Hard Rules

- **Never place a dial on an account the BDR guard blocks.** Two people writing to one buyer costs the deal, and the AE finds out from the buyer.
- **Never cite an Illustrative or Benchmark proof point as a customer result.** A figure the buyer repeats back becomes a claim the company cannot defend. Benchmark figures are cited as research, with their source and date.
- **Never call a trigger recent without its date.** A rep who says "recent" to a buyer who knows the date loses the call. An undated trigger has no window, so it does not start a sequence.
- **Never let a MANUAL REVIEW verdict read as a GREENLIGHT.** A fit word beside a gate hides the reason. The zones beside the verdict show it.
- **Never write a pending account as ACTIVE.** Pending means the owner may still change, and the rep must know that before calling.
- **Never call an opted-out contact.** The opt-out is the buyer's instruction, and it holds across every account the contact touches.
- **Never generate a figure to fill a gap.** An invented number in an opener is a claim the rep must defend on the call. Gaps are named, and the call goal becomes finding the figure.
- **Never send, enroll or write to the CRM.** The rep reads the draft and acts. The skill's job ends at the draft.
- **Never spell a verdict other than GREENLIGHT, MANUAL REVIEW or DISQUALIFY.** The shared words are how every skill in the suite reads the same verdict.

---

## Quality Bar

**Done when all are true:**

- [ ] Every task due on the date is either on the sheet or in the exclusions, with its reason
- [ ] The user's role was detected, and the BDR guard ran before any brief was written
- [ ] Every account on the sheet has a fit word from the Fit Grid with its row quoted, or a verdict and zone scores where it is MANUAL REVIEW
- [ ] Every account's verdict sits beside its five zone scores
- [ ] Tiers follow the profile's Hot definition first, and any disagreement with the role table is named
- [ ] Every opener names a fact from the account, or is written for the person who answers when no contact is known
- [ ] Every discovery question traces to a Core Pain Points row or to a profile Competitive Discovery question
- [ ] Every proof point shows its Status, and no Illustrative or Benchmark figure is cited as a customer result
- [ ] Every blank phone, contact or date is named as unknown, and the call goal says how to find it
- [ ] Opt-outs and OUT accounts are in the exclusions with their reason
- [ ] `dial_sheet`, `pre_call_briefs`, `exclusions` and `next_action` are named in the report
- [ ] No placeholder brackets remain in the output, and the file was written only if the user asked

---

## Examples

### Example 1: Nadia Brandt, BDR Morning List (Monday 2026-10-19)

**Context:** Nadia Brandt is a BDR for Texas and Oklahoma at PlotIQ. Today is Monday 2026-10-19. The CRM returns nine open tasks for her (illustrative count). One of them is Brackhaven Memorial Gardens, which is ACTIVE at Stage 5 Negotiate with Owen Pruitt as its AE. Another is Northvale Memorial Holdings, which is OUT.

**Input:** "Run the daily prospecting report for Nadia Brandt."

**Process:** Step 0 sets `user_role` to BDR. Step 1 applies the BDR guard first: Brackhaven is ACTIVE with Owen Pruitt as owner and no yes from him on file (`[CRM]`), so it moves to exclusions before any brief is built. Step 3 finds a former Lowmoor contact who opted out after the loss (`[CRM]`, illustrative). The name is withheld. Northvale is removed in Step 4 as OUT.

Seven accounts remain. Each is scored against the Fit Grid row for its ICP and the five Qualification Zones:

- **Corrow Ridge Cemetery.** Consolidator bought the site on 2026-07-01 (`[Public: state licensing database]`). The window is 60 to 120 days from the profile, open 2026-08-30 to 2026-10-29, so 10 days remain (`[Inferred]`, from 2026-10-29 minus 2026-10-19). Zone 1 HIGH, on the paper plat maps and a deed recorded twice in 2025 (`[CRM]`, illustrative), which falls inside the 24-month test. Hot. Fit Grid ICP1 Strong row, 2 of 4 tests met (14,000 plots, paper plat maps). The signing limit is on the record now: the GM recommends, and the Harborline board approves above $25K, with its next meeting on 2027-01-12 (`[CRM]`, illustrative). That scores Zone 3 MEDIUM, on the profile's MEDIUM cell, since the GM recommends, the Harborline board approves, and its next meeting is more than 60 days out. Zone 5 is HIGH, because Harborline became the owner of record on 2026-07-01, inside 24 months (`[Public: state licensing database]`). The annual state filing stays `[Unknown]`.
- **Sable Fork Cemetery.** INBOUND. Demo request through the website form on Thursday 2026-10-15 (`[CRM]`), four days old. Hot. The profile's Hot definition is "an INBOUND request not yet answered and within 3 business days of arriving." Thursday 2026-10-15 to Monday 2026-10-19 is two business days, so the request meets the definition (`[Inferred]`). No reply from PlotIQ is logged (`[CRM]`), so the request is not yet answered. MANUAL REVIEW, with Zone 3 HIGH, because the GM signs alone under $25K with no board approval step (`[CRM]`, illustrative).
- **Quill Hollow Memorial Park.** GM Ines Carmody moved here from Lowmoor six months ago with an owner growth mandate (`[CRM]`). Last touch 2026-09-29, 20 days ago, now quiet (`[CRM]`, illustrative). Warm. The records finding in the last state review is `[CRM]` with its date `[Unknown]`. Zone 1 is therefore MEDIUM, because the paper plat maps and lookups that take days fit the MEDIUM cell, and the finding's 24-month test cannot be confirmed, so HIGH is not met. Fit Grid ICP1 Strong, 3 of 4 tests met (8,800 plots, paper plat maps, and an owner who signs under $25K). Zone 3 is HIGH because the owner signs under $25K alone, with no board approval step (`[CRM]`, illustrative). GREENLIGHT stands on Zones 3 and 5. The GM change is dated 2026-04-25 (`[Public: state licensing database]`, illustrative), and the Hot conflict it raises is named in its brief.
- **Greyfield Memorial Park.** Digital map from Stonemark, a direct software incumbent (`[CRM]`). Pre-need team of three with an intake form on the site (`[Public: company website]`). Social ads feed leads into email (`[CRM]`, illustrative), so all three conditions of the Zone 2 HIGH cell are on record. Fit Grid ICP1 Strong, 2 of 4 tests met (9,000 plots, and an owner who signs under $25K alone). The paper-records test is not met, and the annual filing is `[Unknown]`. Last touch on the account record 2026-09-24 with no named contact (`[CRM]`, illustrative). Warm. GREENLIGHT with Zones 2 and 3 HIGH. Zone 3 is HIGH because the owner signs under $25K alone, with no board approval step (`[CRM]`, illustrative). Zone 5 is MEDIUM, one growth project, and Zone 1 is MEDIUM because the Stonemark map holds no records or trust reporting (`[CRM]`, illustrative). Zone 4 is MEDIUM, because Stonemark holds no records or trust reporting and so fits poorly for this work, and the staff email and shared-drive use is `[Unknown]`, so the HIGH cell is not met.
- **Saltmarsh Heritage Group.** The owner letter on the company site says: "Growth in 2027 means one system for all five sites" (`[Public: company site, owner letter 2026]`). CFO Hector Ruiz approves budget (`[CRM]`). GREENLIGHT, with Zone 3 UNKNOWN, because the record holds no cycle length for the CFO gate. Zone 2 is HIGH, because the counselors, the website intake form and the social ads are all on record. Zone 5 is HIGH, because the owner letter names growth, which is the profile's owner update naming growth. Zones 1 and 4 are MEDIUM, because the plot records are in spreadsheets only (`[Notes]`). New.
- **Tamsin Vale Cemetery.** 4,200 plots and paper plat maps (`[CRM]`). No phone on file. Who signs is `[Unknown]`. MANUAL REVIEW, Zone 1 HIGH only, because the paper plat maps meet two double sales in the last 24 months (`[CRM]`, illustrative). New.
- **Lowmoor Memorial Gardens.** Closed-lost to Oldgate on 2026-01-20, nine months ago, with the reason logged as "timing" (`[CRM]`). The champion, Ines Carmody, has moved to Quill Hollow. MANUAL REVIEW on re-score. Recycle, on hold. Its verdict is the one Closed-Loss Reactivation (05) recorded, and this skill does not re-score it.

The Warm tier holds two accounts. Two cases are not a pattern, so the report states the two accounts and claims nothing about the tier as a whole.

**Output:**

Dashboard: 7 accounts on the sheet, 6 to dial and 1 on hold. Tiers: 2 Hot, 2 Warm, 2 New, 1 Recycle (hold). Prior contact on 4 of 7 accounts: Sable Fork (INBOUND, the form request not yet answered), Quill Hollow (last touch 2026-09-29), Greyfield (last touch 2026-09-24) and Lowmoor (closed-lost in January, with prior history). Net-new first touches on 3 of 7 (Corrow Ridge, Saltmarsh, Tamsin Vale). Strongest opportunity: Corrow Ridge, with 10 days left in its trigger window. Exclusions: 3 (two accounts and one contact).

**Priority Dial Queue**

| # | Tier | Account | Contact | Fit or Verdict, and Zones | Call Goal |
|---|------|---------|---------|---------------------------|-----------|
| 1 | Hot | Corrow Ridge Cemetery | No contact on file. The task names none | Strong. GREENLIGHT. Zones 1 HIGH, 2 UNKNOWN, 3 MEDIUM, 4 UNKNOWN, 5 HIGH | Learn whether Harborline runs its own plot system, then book discovery with the site GM before the Q1 2027 integration review |
| 2 | Hot | Sable Fork Cemetery | Arlen Biggs, General Manager. Requester `[Unknown]` | MANUAL REVIEW. Zones 1 MEDIUM, 2 LOW, 3 HIGH, 4 MEDIUM, 5 LOW | Confirm who filled the website form, then book discovery. No demo yet |
| 3 | Warm | Quill Hollow Memorial Park | Ines Carmody, General Manager (champion label, Champion Test not yet run) | Strong. GREENLIGHT. Zones 1 MEDIUM, 2 UNKNOWN, 3 HIGH, 4 UNKNOWN, 5 HIGH | Find when the last state review was and what it asked for, then book a 15-minute discovery call |
| 4 | Warm | Greyfield Memorial Park | No named contact (`[Unknown]`) | Strong. GREENLIGHT. Zones 1 MEDIUM, 2 HIGH, 3 HIGH, 4 MEDIUM, 5 MEDIUM | Find the owner of pre-need intake, and ask who calls back website leads |
| 5 | New | Saltmarsh Heritage Group | Hector Ruiz, CFO | GREENLIGHT. Zones 1 MEDIUM, 2 HIGH, 3 UNKNOWN, 4 MEDIUM, 5 HIGH | Ask which system the five sites move to, and when. No email from this dial |
| 6 | New | Tamsin Vale Cemetery | No name, no phone on file | MANUAL REVIEW. Zones 1 HIGH, 2 LOW, 3 MEDIUM, 4 LOW, 5 MEDIUM | Find who signs, and find a phone number. The first action is a contact search |
| 7 | Recycle (hold) | Lowmoor Memorial Gardens | Unknown, champion moved | MANUAL REVIEW. Zones as re-scored in Closed-Loss Reactivation (05), not restated here | Do not dial. Closed-Loss Reactivation holds it on MONITOR |

Every zone score in the table rests on a fact in the try-it records, as the zone rule requires. A zone with no such fact is UNKNOWN, and the scores that stay UNKNOWN are the evidence still to gather.

**Brief for #1 (Corrow Ridge Cemetery):**
- **Why this account:** The site was bought by Harborline Funeral Partners, a 14-site regional consolidator, on 2026-07-01 (`[Public: state licensing database]`). The window is 60 to 120 days, so it is open until 2026-10-29, with 10 days remaining (`[Inferred]`). Zone 1 HIGH (14,000 plots on paper plat maps, `[CRM]`, and a deed recorded twice in 2025, `[CRM]` (illustrative), inside the 24-month test). Zone 5 HIGH (a new owner inside 24 months). Whether Harborline runs its own system is `[Unknown]`, and it is the first question.
- **Opener:** "Hi, it's Nadia Brandt with PlotIQ. Before the integration review, it helps to know what the plot map is worth. Not sure if that's hit your team yet?" The persona who acts is the acquirer's CFO or controller, with the site GM. No contact is on file, so the first call is to find the GM.
- **Discovery questions:** (1) "Does Harborline run its own plot system, or will this site move onto theirs?" (2) "When a family asks about a plot, where do you look first, and how long does it take?" (3) "Walk me through last year's trust filing. Who pulled the numbers, and from where?"
- **Objection prep:** "We already have a provider." Response: "That's good to hear. What's working well, and where are the gaps?"
- **Call goal:** Learn whether Harborline runs its own plot system, then book discovery with the site GM before the Q1 2027 integration review.

**Brief for #2 (Sable Fork Cemetery):**
- **Why this account:** A demo request came through the website form on Thursday 2026-10-15, four days ago (`[CRM]`). Who filled the form is `[Unknown]`. Zone 3 HIGH (the GM signs under $25K, `[CRM]`). Zone 1 MEDIUM (a plot list in a spreadsheet). Zone 2 LOW (pre-need: none, `[CRM]`), and Zone 5 LOW (plot sales flat for three years, and no succession plan on the record, `[CRM]`, illustrative). It meets the profile's Hot definition, which is an INBOUND request not yet answered and within 3 business days of arriving. Two business days have passed. No reply is logged (`[CRM]`), so the request is still unanswered.
- **Opener:** The buyer's own request is the hook. "Hi, it's Nadia Brandt with PlotIQ. Someone at Sable Fork asked for a demo through our website on Thursday. Was that you, or someone on your team?"
- **Discovery questions:** (1) "Where does the plot map live today, and when was it last updated?" (2) "When a family asks about a plot, where do you look first, and how long does it take?" (3) "What does a 20-minute lookup cost you, versus 20 seconds?"
- **Objection prep:** "Send me some info." Response: "Happy to, but I want to send the right thing. Can I ask two quick questions so I don't waste your time with generic material?"
- **Call goal:** Confirm who requested the demo, then book discovery. No demo until the pain is confirmed on the call.

**Brief for #3 (Quill Hollow Memorial Park):**
- **Why this account:** GM Ines Carmody moved here from Lowmoor six months ago with an owner growth mandate (`[CRM]`). Fit Grid ICP1 Strong, 3 of 4 tests met (8,800 plots, paper plat maps and an owner who signs under $25K). Zone 3 HIGH (the owner signs under $25K, alone, with no board approval step, `[CRM]`, illustrative). Zone 5 HIGH (a new GM inside 24 months). Zone 1 MEDIUM, because the records finding in the last state review is `[CRM]` and undated (`[Unknown]`). The finding is never called recent. The role table would put Quill Hollow in Hot: its GM change is dated 2026-04-25 (`[Public: state licensing database]`, illustrative), so its 90 to 180 day window stays open until 2026-10-22, three days from today (`[Inferred]`), and the account is a Strong ICP. The profile's Hot definition needs Zone 1 HIGH, and Zone 1 is MEDIUM, so the profile's definition holds and the account stays Warm. The profile owner decides whether the role table should also require Zone 1.
- **Opener:** "Hi Ines, it's Nadia Brandt with PlotIQ. New GMs usually inherit the plot map and the filing at the same time. How are the plot records kept at Quill Hollow today?"
- **Discovery questions:** (1) "When was the last state review, and what did it ask for?" (2) "When a family asks about a plot, where do you look first, and how long does it take?" (3) "Walk me through last year's trust filing. Who pulled the numbers, and from where?"
- **Objection prep:** "We already have a provider." Response: "That's good to hear. What's working well, and where are the gaps?"
- **Proof point:** The Fennick Gardens figure is Illustrative and is not cited to a buyer. The research benchmark is cited as context only: most cemeteries your size carry 50 to 100 plots that are sold on paper and unsold on the map (Benchmark, deathcare research, 2026-03-27 to 2026-04-01).
- **Call goal:** Find when the last state review was and what it asked for, then book a 15-minute discovery call.

**Brief for #4 (Greyfield Memorial Park):**
- **Why this account:** A digital map from Stonemark, a direct software incumbent, and a pre-need team of three with a website intake form (`[CRM]`, `[Public: company website]`). Strong: 2 of 4 tests met (9,000 plots, and an owner who signs under $25K). The Stonemark signing date is `[Unknown]`. Zones 2 and 3 HIGH. Warm: the account record shows a touch on 2026-09-24, 25 days ago, with no named contact (`[CRM]`, illustrative).
- **Opener:** "Hi, it's Nadia Brandt with PlotIQ. Your website has a pre-need intake form, and I wanted to ask who calls back the leads it sends."
- **Discovery questions:** (1) "When a pre-need lead comes in from the website, who calls them back, and when?" (2) "Where does the plot map live today, and when was it last updated?" (3) "What happened the last time you brought a new tool in here?"
- **Objection prep:** "We already have a provider." Response: "That's good to hear. What's working well, and where are the gaps?"
- **Call goal:** Find the owner of pre-need intake, and ask how website leads are called back. The Stonemark renewal is not raised on this dial, because Competitive Displacement (12) holds that case.

**Brief for #5 (Saltmarsh Heritage Group):**
- **Why this account:** The owner letter on the company site says: "Growth in 2027 means one system for all five sites" (`[Public: company site, owner letter 2026]`). Zone 2 HIGH (pre-need counselors at three funeral homes). Zone 3 UNKNOWN, a must-have, because the CFO approves the budget and the record holds no cycle length. Zone 5 HIGH, because the letter names growth. GREENLIGHT, because two zones are HIGH and no must-have zone is LOW.
- **Opener:** "Hi Hector, it's Nadia Brandt with PlotIQ. Your owner letter says all five sites move to one system next year." The persona who acts is the CFO.
- **Discovery questions:** (1) "Which system do the five sites move to, and when?" (2) "Walk me through last year's trust filing. Who pulled the numbers, and from where?" (3) "When a pre-need lead comes in from one of the funeral homes, who calls them back, and when?"
- **Objection prep:** "Not a priority right now." Response: "Totally fair. Most teams don't change until something forces the issue. Out of curiosity, when was the last time your team had a close call on the records?"
- **Call goal:** Ask which system the five sites move to and when, and who approves the spend. No email goes out from this dial. The CFO email belongs to Research Outbound (03).

**Brief for #6 (Tamsin Vale Cemetery):**
- **Why this account:** 4,200 plots on paper plat maps, with one binder per section and two double sales in two years (`[CRM]`, illustrative). Zone 1 HIGH is the only HIGH zone. Who signs is `[Unknown]`. MANUAL REVIEW.
- **No phone on file and no named contact.** This is the missing-data case. The rep does not dial until a number is found. The first action is a contact search, and the opener below is for whoever answers.
- **Opener:** "Hi, it's Nadia Brandt with PlotIQ. Who signs for the cemetery's plot and trust records?"
- **Discovery questions:** (1) "How do you keep the plot records, and who maintains them?" (2) "When a family asks about a plot, where do you look first, and how long does it take?" (3) "What does a 20-minute lookup cost you, versus 20 seconds?"
- **Objection prep:** "We handle it internally." Response: "Makes sense. The question is whether the time your team spends on lookups is the best use of their expertise. Roughly how many hours a month does that take?"
- **Call goal:** Find who signs, and find a phone number. Confirm how plot records are kept.

**Brief for #7 (Lowmoor Memorial Gardens, hold):**
- **Why this account:** Closed-lost to Oldgate on 2026-01-20, reason "timing" (`[CRM]`). The true loss reason sits with Closed-Loss Reactivation (05), which holds the account on MONITOR. The champion, Ines Carmody, has moved to Quill Hollow. Closed-Loss Reactivation (05) set the account to MONITOR on 2026-10-19, with a reminder for 2026-12-18 to 2027-01-17 (`[Notes]`).
- **Do not dial.** Route to Closed-Loss Reactivation (05) first. The account reopens only on a reopening event that 05 names.

**Exclusions**

| Account or contact | Reason | Action |
|---|---|---|
| Brackhaven Memorial Gardens | BDR guard. ACTIVE, Stage 5 Negotiate, AE Owen Pruitt. No yes from Owen on file (`[CRM]`) | Share today's intel with Owen Pruitt. Ask whether he wants BDR assist |
| Northvale Memorial Holdings | OUT. Public consolidator running its own in-house system (`[Public: annual filing]`). DISQUALIFY | Remove from the sheet. No dial, no sequence. OUT is not LOST, so it is not a reactivation |
| Former contact at Lowmoor Memorial Gardens, name withheld | Opted out on 2026-02-14, after the loss (`[CRM]`, illustrative). The opt-out holds for every future dial to this contact. The opted-out contact is not Ines Carmody, so her Quill Hollow dial stands (`[CRM]`, illustrative) | Keep the contact off every sheet. Record the opt-out in the CRM |

**AE Coordination (BDR only):** Brackhaven needs a sync with Owen Pruitt before anyone calls Ruth Ellery again. The board meets 2026-11-12, and Owen owns the next step.

**End-of-day prompts:** Log the disposition for each dial. Create the follow-up tasks. Add accounts to a sequence in the CRM only after reading the draft.

**Next action:** Nadia Brandt shares today's Brackhaven intel with Owen Pruitt by 2026-10-19. The date is the due date of the Brackhaven task on record, which is the run date and earlier than the five-business-day date of 2026-10-26. It is due first, ahead of the Sable Fork reply that closes 2026-10-20. That close comes from the profile's Hot definition: an INBOUND request is answered within 3 business days of arriving, and Thursday 2026-10-15 plus three business days is Tuesday 2026-10-20.

**Report path:** none (inline).

```text
Hand-off (read by 06):
account: the morning list of Nadia Brandt (BDR), 2026-10-19, seven accounts
run_date: 2026-10-19
dial_sheet: 7 accounts (Hot 2, Warm 2, New 2, Recycle 1 on hold). Corrow Ridge Cemetery, Sable Fork Cemetery, Quill Hollow Memorial Park, Greyfield Memorial Park, Saltmarsh Heritage Group, Tamsin Vale Cemetery, Lowmoor Memorial Gardens
pre_call_briefs: 7 (the list holds seven accounts, so the top-eight slots are not all filled)
exclusions: Brackhaven Memorial Gardens (BDR guard, Owen Pruitt named as owner). Northvale Memorial Holdings (OUT, DISQUALIFY). a former Lowmoor contact, name withheld (opt-out, illustrative)
next_action: Nadia Brandt shares Brackhaven intel with Owen Pruitt by 2026-10-19 (the Brackhaven task's due date on record, the run date)
report_path: none (inline)
```

---

### Example 2: Owen Pruitt, AE Pipeline Calls (Monday 2026-10-19)

**Context:** Owen Pruitt is the Account Executive for outside sales in Texas and Oklahoma. He owns Brackhaven Memorial Gardens (`[CRM]`). Six tasks are due today (illustrative count).

**Input:** "Prep my dials for today, Owen."

**Process:** `user_role` is AE. There is no BDR guard, so the full book is worked. Each account is scored and tiered on the same facts as Example 1, so the same account lands in the same tier for both roles unless the role table says otherwise. The AE view shows every account on the day's task list, so Greyfield Memorial Park and Saltmarsh Heritage Group are added here, both with tasks due today on Nadia Brandt's list. Greyfield has no AE owner on record, so it is labelled TARGET (pending AE assignment). Saltmarsh has no AE owner on record either.

- **Hot:** Brackhaven Memorial Gardens. ACTIVE at Stage 5 Negotiate since 2026-09-09 (`[CRM]`), with the board date still to get by 2026-10-26, five business days after the run date, and no earlier date on record. Ruth Ellery has not replied since 2026-10-03, which is 16 days (`[CRM]`). The Warm criterion also applies, and the Hot criterion takes precedence here, so the brief leads with the silence. Corrow Ridge Cemetery, Hot on the same trigger window as Example 1. Sable Fork Cemetery, Hot on the same inbound request as Example 1.
- **Warm:** Quill Hollow Memorial Park, quiet for 20 days (illustrative), and Greyfield Memorial Park, last touch 2026-09-24, 25 days ago.
- **New:** Saltmarsh Heritage Group, with no touch yet, and Tamsin Vale Cemetery.
- **Recycle:** Lowmoor Memorial Gardens, MANUAL REVIEW on re-score, on hold.

**Output:**

Dashboard: 8 dials. 3 Hot, 2 Warm, 2 New, 1 Recycle (hold). No exclusions, because the AE view applies no guard. Strongest opportunity: Brackhaven. It sits at Stage 5, the board meets 2026-11-12, and the Oldgate renewal in March 2027 gives the next call its reason to move. The call should close the board date, not restart discovery.

| # | Tier | Account | Contact | Fit or Verdict, and Zones | Call Goal |
|---|------|---------|---------|---------------------------|-----------|
| 1 | Hot | Brackhaven Memorial Gardens | Ruth Ellery, General Manager (champion) | Strong. GREENLIGHT. Zones 1 HIGH, 2 MEDIUM, 3 MEDIUM, 4 MEDIUM, 5 HIGH | Get the board date from Ruth Ellery by 2026-10-26. Hold at Stage 5 |
| 2 | Hot | Corrow Ridge Cemetery | No contact on file | Strong. GREENLIGHT. Zones 1 HIGH, 2 UNKNOWN, 3 MEDIUM, 4 UNKNOWN, 5 HIGH | Learn whether Harborline runs its own plot system, then book discovery with the site GM |
| 3 | Hot | Sable Fork Cemetery | Arlen Biggs, General Manager. Requester `[Unknown]` | MANUAL REVIEW. Zones 1 MEDIUM, 2 LOW, 3 HIGH, 4 MEDIUM, 5 LOW | Confirm who requested the demo, then book discovery. No demo yet |
| 4 | Warm | Quill Hollow Memorial Park | Ines Carmody, General Manager | Strong. GREENLIGHT. Zones 1 MEDIUM, 2 UNKNOWN, 3 HIGH, 4 UNKNOWN, 5 HIGH | Find when the last state review was, then book discovery |
| 5 | Warm | Greyfield Memorial Park | No named contact (`[Unknown]`). TARGET (pending AE assignment) | Strong. GREENLIGHT. Zones 1 MEDIUM, 2 HIGH, 3 HIGH, 4 MEDIUM, 5 MEDIUM | Find the owner of pre-need intake, and ask who calls back website leads |
| 6 | New | Saltmarsh Heritage Group | Hector Ruiz, CFO | GREENLIGHT. Zones 1 MEDIUM, 2 HIGH, 3 UNKNOWN, 4 MEDIUM, 5 HIGH | Ask which system the five sites move to, and when. No email from this dial |
| 7 | New | Tamsin Vale Cemetery | No name, no phone on file | MANUAL REVIEW. Zones 1 HIGH, 2 LOW, 3 MEDIUM, 4 LOW, 5 MEDIUM | Find who signs, and confirm the paper-map process |
| 8 | Recycle (hold) | Lowmoor Memorial Gardens | Unknown, champion moved | MANUAL REVIEW. Zones as re-scored in 05 | Do not dial yet. Closed-Loss Reactivation holds it on MONITOR |

**Brief for #1 (Brackhaven Memorial Gardens):**
- **Why this account:** ACTIVE at Stage 5 Negotiate, day 40 in stage (`[CRM]`). The board meets 2026-11-12. Ruth Ellery has not replied for 16 days (`[CRM]`). The board date is to be got by 2026-10-26, five business days after the run date, and no earlier date is on record. If the date is not confirmed by 2026-11-02, the stage rule in the deal skills applies, not this one.
- **Opener:** "Hi Ruth, it's Owen Pruitt with PlotIQ. Before the board meets on 2026-11-12, I need the date confirmed. Can you get it to me by Monday, 2026-10-26?"
- **Discovery questions:** (1) "What does the board need to see before it votes on 2026-11-12?" (2) "Walk me through how plot records are kept at both sites." (3) "Who at the site would own the ledger export if the board says yes?"
- **Objection prep:** "We already have a system." Response: "That's good to hear. What's working, and where do the paper maps still get in the way?"
- **Call goal:** Get the board date from Ruth Ellery by 2026-10-26. The call closes the date. It does not restart discovery, because the pain is confirmed.

**Brief for #2 (Corrow Ridge Cemetery):** Same facts and opener as Example 1, Brief #1. The AE's call goal is the same as the BDR's, because the account has no owner conflict.

**Brief for #3 (Sable Fork Cemetery):** Same facts as Example 1, Brief #2. The AE may book the discovery directly, but the demo waits until the pain is confirmed.

**Brief for #4 (Quill Hollow Memorial Park):** Same facts and opener as Example 1, Brief #3.

**Brief for #5 (Greyfield Memorial Park):** Same facts as Example 1, Brief #4. The account is TARGET (pending AE assignment), so the AE may book the call, and the Warm reason stands.

**Brief for #6 (Saltmarsh Heritage Group):** Same facts as Example 1, Brief #5. The owner-letter quote is the one Example 1 uses.

**Brief for #7 (Tamsin Vale Cemetery):** Same facts as Example 1, Brief #6. The first action is still a contact search, because no phone is on file.

**Brief for #8 (Lowmoor Memorial Gardens, hold):** Do not dial. Closed-Loss Reactivation (05) holds the account on MONITOR, and the AE sees the same reason as Example 1, Brief #7.

```text
Hand-off (read by 06):
account: the pipeline calls of Owen Pruitt (AE), 2026-10-19
run_date: 2026-10-19
dial_sheet: 8 accounts (Hot 3, Warm 2, New 2, Recycle 1 on hold). Brackhaven Memorial Gardens, Corrow Ridge Cemetery, Sable Fork Cemetery, Quill Hollow Memorial Park, Greyfield Memorial Park, Saltmarsh Heritage Group, Tamsin Vale Cemetery, Lowmoor Memorial Gardens
pre_call_briefs: 8 (one per account on the sheet)
exclusions: none (AE view, BDR guard not applied)
next_action: Owen Pruitt gets the board date from Ruth Ellery by 2026-10-26, five business days after the run date (no earlier date is on record)
report_path: none (inline)
```

---

## Common Patterns

### Pattern: No Tasks Due Today
**When:** The rep has zero open tasks for the date.
**Approach:** Check for overdue tasks from the past three days. Check for accounts with recent inbound signals that warrant proactive outreach. If nothing is found, recommend running `gtm-account-snapshot` on the target accounts to build a new prospecting list. Say that the list is empty, and why.

### Pattern: BDR with Heavy AE Overlap
**When:** More than half of the BDR's tasks sit on accounts with active AE deals. Name the count, for example "5 of 8 tasks".
**Approach:** Generate the exclusions table with clear AE coordination guidance. Recommend that the BDR discuss territory alignment with their manager, because a queue that mostly belongs to AEs is a routing question before it is a prospecting one. Show the filtered queue with its adjusted tier priorities.

### Pattern: Account Pending AE Assignment
**When:** An account has no AE owner yet, and an AE assignment is expected.
**Approach:** The account is not ACTIVE. Show it as "TARGET (pending AE assignment)" and work it. The brief names the pending owner once one exists, and the guard applies from the day the assignment is made.

### Pattern: Abbreviated Prep
**When:** The rep says "just give me my top five" or has limited time.
**Approach:** Skip the full report. Deliver only the five highest dials, each with a condensed brief: opener, one question and the call goal. The guard and the exclusions still run in full.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---|---|---|
| "No tasks in the CRM for today" | The rep's queue is empty, or the task type filter is too narrow | Expand to overdue tasks from the past three days, then to accounts with recent inbound activity. If still empty, recommend `gtm-account-snapshot` on priority accounts to build outbound |
| "Contact has no phone number" | The CRM field is blank, which is unknown and not a no | Flag the contact as "no phone on file." Recommend a contact search. Use LinkedIn or email only if the profile and the CRM allow it, and say which |
| "Multiple contacts at the same account in the task list" | Several tasks point to one account | Group them into one brief. Call the highest-priority contact first, by persona and engagement, then use what that call finds for the next |
| "BDR has tasks on accounts they don't own" | The BDR Owner field does not name this BDR, or the routing is wrong | Check the BDR Owner field. If the BDR is the BDR Owner, proceed. If not, flag the account for territory alignment, because the task may have been routed incorrectly |
| "The Hot definition and the role table disagree" | The profile sets a window the role table does not | Show both in the brief, name the account and the window, and send the question to the profile owner. Do not choose silently |
| "A trigger has no date" | The source did not record one | Mark the trigger undated. It has no window, so it does not start a sequence until the date is found |
| "The sheet has fewer than eight accounts" | The task list is short | Write a brief for every account. Say that the list holds fewer than eight accounts, so the top-eight slot is not padded |

---

## Best Practices

### Do's
- **Run this every morning.** The sheet is useful only when it is current at the start of the block.
- **Start with the Hot tier.** These accounts have the most evidence behind them.
- **Personalize every opener.** Each hook refers to a fact about the account, not a generic phrase.
- **Log outcomes immediately.** End-of-day tracking is useful only when the dispositions are logged.
- **Read the zones beside the verdict.** A MANUAL REVIEW dial is a conversation to prepare for, not a dial to skip.

---

## Integration With Other Skills

**Reads from Meeting Prep (06), by name.** When a prep sheet exists for an account, this skill reads `prep_sheet`, `top_pain`, `question_bank`, `attendees` (with their buying role) and `proof_point`. The top pain replaces a generic question in the brief, the attendees add contacts to the account, and the proof point is shown with its Status, so an Illustrative figure is never cited.

**Hands to Meeting Prep (06), by name.** `dial_sheet` (tiers Hot, Warm, New and Recycle), `pre_call_briefs` (the top eight) and `exclusions` (each with its reason). Meeting Prep turns a dial that becomes a meeting into a prep sheet, and that sheet comes back to this skill the next morning as `prep_sheet`. The loop is what keeps each day's list informed by the last day's calls.

**Reads from the close, by name.** `next_action` is written by this skill and read by the close (Wrap-Up). `report_path` is set only when a file was written, and the close reads it the same way.

**Other skills:**
- `gtm-account-snapshot` (02): deeper research on an account surfaced in the dial queue, such as an INBOUND request.
- `gtm-trigger-event-outbound` (04): when a dial surfaces a trigger inside its window.
- `gtm-closed-loss-reactivation` (05): for Recycle accounts that were closed-lost, before any dial.
- `gtm-competitive-displacement` (12): when a Hot dial reveals a known incumbent.

### Chains

- **Daily Pipeline:** Daily Prospecting (07, this skill, first), then Meeting Prep (06). This skill ranks the morning dials, removes the accounts the BDR guard blocks, and writes the brief for the top eight, so that each booked call reaches Meeting Prep with its account already screened.

---

## Changelog


### 2.1.7 (2026-10-26)
- The zone rules are grouped by cell. The decisions are the same, with three settled: a board condition is met only when the account has no board approval step, a LOW cell needs the account's own cycle on record, and a cast summary never sets a zone.
- A trigger inside its window does not make an account Hot without Zone 1 HIGH, as the profile's Hot definition requires.
- Warm counts a touch logged on the account record. New reads Strong ICP from the Fit Grid, whatever the verdict.
- A step the record dates to today is due on the run date, ahead of a five-business-day date.
- The Saltmarsh example's Zone 3 is UNKNOWN, because no cycle length is on record, so its verdict is GREENLIGHT and its tier (New) is unchanged.
- The file example and the exclusion action template carry no worked name or date.

### 2.1.6 (2026-10-26)
- The board-date ask in the AE example follows the shared next-action rule: five business days after the run date, with no earlier record date. The dated action that named an earlier date is removed.
- The Sable Fork reply date in the BDR example names its source: the profile's Hot definition for an INBOUND request, counted in business days from arrival.
- The zone facts behind the Sable Fork and Saltmarsh scores name their records. The Saltmarsh owner letter is quoted in the wording Research Outbound (03) uses, and the Saltmarsh plot records are tagged as notes, as Research Outbound tags them.
- The Quill Hollow opener uses the profile's own first line for a new general manager. Its discovery question about the state review asks when the review was, and the undated finding is no longer the hook.
- The prior-contact count on the dial sheet names the accounts it counts, and the AE example lists every account on the day's task list, including the two accounts that a BDR works.
- Frontmatter: the 2.1.5 change summary carried a stray quotation mark that broke the YAML. It is removed.

### 2.1.5 (2026-10-26)
- The Zone 3 MEDIUM cell in Step 4 and the Corrow Ridge reading quote the profile's new wording (GM recommends and the board approves, or the next board meeting is more than 60 days out).
- The next action follows the family's one deadline rule. The Output Contract points to that rule, and each example names the record (a task due date or a dated CRM action) when that record sets an earlier date.
- The Fit Grid reading in the examples follows the Fit Scoring rule as the team approved it, with each tier's tests counted with n.

### 2.1.4 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. Step 4 states how a HIGH cell with several conditions is read, how a board path between 60 days and three months is scored, that an acquisition changing the owner of record scores Zone 5 HIGH, and that an UNKNOWN zone never blocks GREENLIGHT. Step 5 breaks ties by the Fit Grid tests met and then by the nearest deadline, and takes a Recycle hold's verdict from the upstream skill. Step 7 orders several steps by due date. Step 2 names the status source. The try-it records gain the owner of record, the status lines and the zone facts. The Fit Grid grade in the examples follows the tests the records meet.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The try-it records now carry the facts behind each worked zone, the Lowmoor opt-out date and the net-new touches. A trigger window counts from its dated event. The Corrow Ridge and Greyfield openers use the profile's own lines, not unsourced "teams tell us" claims. The try-it ask names the example profile. No tier, verdict or next action changed.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. A Fit Grid row now carries its grade at half its tests met, a zone with no fact shows UNKNOWN, and a role-table Hot never overrides the profile's Hot definition. Example 1 gains the dated records that its grades and tiers rest on. No tier, grade, verdict or next action changes.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1. No other change.

### 2.1.0 (2026-10-25)
- Reads the Context OS account folders for the accounts that pass the BDR guard, and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### Version 2.0.0 (2026-10-20)
- Moved to the Sales 2.0 shared contract. The Shared Contract is pasted under Context unchanged.
- Fit is scored against the profile's Fit Grid with the row quoted and the tests counted with n. A Weak row is applied only on evidence.
- Zones and verdicts come from the profile's Qualification Zones and Verdict Rule. Every verdict is spelled GREENLIGHT, MANUAL REVIEW or DISQUALIFY, and every verdict sits beside its zone scores.
- Discovery questions come from the Core Pain Points column, with the profile's Discovery question.
- The BDR guard states the pending-assignment case. Opt-outs are removed from every dial.
- The profile's Hot definition is applied first, and a disagreement with the role table is named, not settled silently.
- Evidence uses the six shared tags. Proof points show their Status, and no Illustrative figure is cited.
- Output is inline by default. A Markdown file is written only when the user asks. Hand-off fields are named for Meeting Prep (06).
- Removed the unsourced claim that two minutes of prep decides whether a call books a meeting. Removed the separate file-format section and its HTML and PDF options.
- Worked examples rebuilt on the PlotIQ prospecting day, with the missing-data cases shown: no phone, a task with no contact, and an opt-out.

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Dial sheet and brief count aligned to the top 8. Qualification Zones reference corrected. Unsourced statistic removed.

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around a single case study company, with the example file named in the profile.
- Em dashes removed from prose.

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology.
- Company-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in profile block.
- Cold Call Framework, Hook Templates and Common Objections moved to an explicit Methodology section, with `{Methodology: X}` references.
- No functional changes to the workflow, tiering logic or output formats.

### Version 1.0.0 (2026-03-04)
- Initial release.
- Configurable through a profile block.
- Four-tier prioritization (Hot, Warm, New, Recycle).
- Three-Step Turnaround cold call framework with hook templates.
- BDR Active Deal Filter with exclusions table and AE coordination.
- Role-aware tiering (BDR and AE criteria).
- ICP definitions in the profile for portability.
- Multi-format output.
