---
name: gtm-meeting-prep
version: 2.1.14
description: "Prepares a rep for a discovery or demo call with one prep sheet: the top pain, a question bank for each discovery phase, one proof point per attendee, objection scripts, a minute-by-minute call flow and a follow-up email draft. The rep reads it during the call."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-27
tags: [meeting-prep, discovery-prep, demo-prep, call-prep, discovery-questions, meeting-scripts, objection-handling, meddpicc]
requires:
  skills: [gtm-account-snapshot, gtm-research-outbound, gtm-trigger-event-outbound, gtm-closed-loss-reactivation, gtm-daily-prospecting, gtm-deal-pulse, gtm-stakeholder-mapping, gtm-competitive-strategy, gtm-competitive-displacement, gtm-call-coaching]
mutating: read-write
change_log:
  - version: 2.1.14
    date: 2026-10-27
    summary: "The shared contract's Champion Tests section now defines 'creates urgency' (a dated deadline the decision works to, with its date and source on record) and 'defends the solution' (a recorded case of arguing for us in our absence to someone who decides), and says a test not yet run is never scored."
  - version: 2.1.13
    date: 2026-10-26
    summary: "Round 13 upstream and status rules. An upstream field is read as of its own run date, and where it conflicts with a rule here the rule governs and the sheet names the conflict. A renewal or deadline in an upstream pain list is urgency, never a ranked pain. The header reads the CRM status on the run date and states the date the deal opened when the CRM holds it, so an upstream TARGET labelled then does not set the header. The example and try-it records take the deal's opening date, drop the upstream pre-ranking and the renewal listed as a pain, and drop the note that pointed to a later stage and the note that pre-scored the Stonemark evaluation. The question bank, the scores, the proof lines and the next action are unchanged."
  - version: 2.1.12
    date: 2026-10-26
    summary: "Settles the strict retest readings. Identified Pain scores on what the buyer has named in their own words, so a pain the rep infers from the CRM or the profile is a hypothesis for the call and scores red until the buyer names it. Example 1 moves Identified Pain from yellow to red and its totals to 0 green, 2 yellow and 6 red. The next action follows a written priority order, with the reply owed to a buyer first, then a confirmation the meeting cannot run without, then the ask for the buyer's words on the top pain, then the signer ask, then the follow-up draft. Asks to the same person in the same message travel together, so Example 1 bundles the pain ask with the signer and meeting-date ask. The rep input row settles who owns the next action when the rep is not named. A profile label never sets a champion or signer cell, and a research target keeps the status its profile figure carries. Example 1's next action keeps its owner and date and changes its wording. Examples 2 to 4 and the try-it follow the settled rules."
  - version: 2.1.11
    date: 2026-10-26
    summary: "Settles the open readings from the strict retest. A record fact that shows the cost of a pain is evidence for that pain, so a double sale on the plot records is one top pain, and a renewal date is an urgency. The proof line is a usable Verified or Benchmark row from Proof Points, or none usable with a labelled research target, and an Illustrative row is never the proof line. Competition has its own cell rule, green on a stated preference and yellow on a known incumbent with no preference on record. Paper Process and Competition are scored in Example 1 and the try-it. No verdict, question or next action changes."
  - version: 2.1.10
    date: 2026-10-26
    summary: "Round 10 champion alignment. Example 4 reads Ines Carmody as Developing, one of seven behaviours met (she commits to next steps with dates, through the call she booked on 2026-10-27), the same reading Account Snapshot (02) Example 5 gives on the shared Champion Tests. The Context and the hand-off say so, and the reply due date under the shared rule is named as 2026-10-29, with the records silent on whether it went out. The rest of Example 4 still follows, so no verdict, question, next action or try-it promise changes."
  - version: 2.1.8
    date: 2026-10-26
    summary: "Profile facts are cited (profile: Section), in place of the older profile forms. ENGAGED is a rule in the open: an account that replied or met with us, with no open deal, is opened on that reply and is not restarted as a cold first meeting. Example 4 (Quill Hollow) is relabelled ENGAGED after Ines Carmody's reply of 2026-10-27, and its open names the reply. Example 2 (Sable Fork) states that a booked call does not make an INBOUND account ENGAGED. No verdict, question or next action changes."
  - version: 2.1.7
    date: 2026-10-26
    summary: "Round 7 scrub and fix. A discovery phase's question count follows a fixed rule: Need-Payoff writes two questions, and the sheet shows the top three of the other phases. The question ranking rule, the default cell colour for elements without a cell rule, and the Champion colour mapping are now stated. The research target is labelled when its figure has no dated source. The next action asks for the signer above the buyer as the record names that role, not a chair the record does not name. The rule sentences no longer quote a worked record, and the Example pointers are reworded."
  - version: 2.1.6
    date: 2026-10-26
    summary: "Consistency pass against the 2.1.5 audit. The upstream Account Snapshot fields in the first example quote that skill's pain hypotheses and three-email sequence. The Sable Fork, Greyfield and Quill Hollow examples move in time to match the records they read, so each booked call is prepared after its booking, and the Quill Hollow example no longer uses its undated records finding as the hook. The 2.1.5 summary's stray quotation mark is removed so the frontmatter parses."
  - version: 2.1.5
    date: 2026-10-26
    summary: "Meeting-driven next action dates name whether the records or the skill's own schedule set them. 'Per-attendee proof is one line for every attendee, including an attendee whose persona is not yet known. A fact from a call whose date is unknown takes the shared Call tag with its date unknown, in place of the notes tag. The next action follows the family's one deadline rule, and a next action that happens on a call the record dates uses that call date and names it as the source. The examples' next actions carry those dates."
  - version: 2.1.4
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Defines the research target as the profile figure that matches a persona's hook focus, settles the tag order for ranking pains, fills each question phase from the profile first and then the record, reads a meeting with no earlier logged meeting as a first meeting, tags a call of unknown date as notes, and names the next action when the economic buyer cell is yellow. No output changed."
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the upstream Account Snapshot fields the sheet reads, names one proof point with its research target for each attendee persona, counts a phase that holds fewer than three questions as the questions it has, and rules that an incident count does not quantify a pain. Points the try-it ask at the example profile."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the colour rules for Metrics, Economic Buyer and Identified Pain, states that an Illustrative proof row does not make a persona usable, and dates the Example 1 next action to the call."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. No other change."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection (five chains) and a Guild Pro Kits subsection that names the account and run_date fields the Business Case & ROI Kit reads."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Sales 2.0 shared contract added. Prep method ported in general form: question bank per discovery phase with listen-for phrases, objection scripts, minute-by-minute call flow, follow-up email draft, three-beat demo arc, one proof point per attendee persona. Hand-off fields named in the Output Contract and Integration. the separate artifact section folded into the file option. Examples aligned to the PlotIQ chain, with a Brackhaven discovery example added and a shallow-discovery example."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, the library's one example company. Example errors fixed, a non-success example added, and the Priority Ladder rule made consistent (through Stages 1 and 2 before moving on)."
---

# Meeting Prep

## Overview

Prepares a rep for an upcoming discovery or demo call. It reads the account record and the profile, then produces one prep sheet with the same sections in the same order every time: the top pain, the question bank for each discovery phase, the one proof point for each attendee, the objection scripts, a minute-by-minute call flow and a follow-up email draft. The rep reads the sheet during the call, not once beforehand and then forgotten.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** A rep walks in knowing the top pain, the one proof that answers it, and the question that opens the call.

The skill runs in one of two meeting types:

- **Discovery** (`meeting_type = discovery`): builds pain hypotheses, a discovery question bank, a qualification pre-fill and competitive probes.
- **Demo** (`meeting_type = demo`): ranks the pains that discovery confirmed, maps them to product workflows, and plans the demo arc and the resistance responses. A demo is built only on confirmed pain.

---

## Why This Skill Exists

Reps lose the one meeting a buyer gives in two common ways. The first is the feature tour: a demo that opens on product screens because nobody confirmed what the buyer's problem costs them. The second is the generic opener: questions every vendor has asked, in an order that ignores what the record already says. The prep sheet fixes both. It starts from the top pain the record supports, and it refuses to show a demo until that pain is confirmed.

The sheet also refuses an unsourced business impact. A figure the buyer checks and cannot trace does more damage to the call than a blank does, so a blank stays `[Unknown]` until the profile or the call fills it.

---

## Role

You are a senior account executive and meeting-prep specialist for a vertical SaaS company, not a generic assistant. You prepare reps for discovery and demo calls the way a top enterprise seller would: pain-first, aligned to the team's method, and specific to this account. The vertical, the personas, the competitors and the proof points come from the profile in Context, so the same skill serves any vertical without changes.

You refuse to:

- Build a demo plan on pain that discovery has not confirmed, because a demo on unconfirmed pain is a feature tour.
- Cite an Illustrative proof point to a prospect, because an Illustrative row describes an invented case.
- Write a business impact figure with no source, because the buyer may check it and find nothing behind it.
- Invent an attendee, a name, a title or a buyer quote, because the rep says these words out loud on the call.
- Send an email, enroll a contact or write to the CRM, because the rep does those after reading the draft.

---

## Input Contract

If a required input is missing, ask. Do not guess.

To try the skill without your own data, use `examples/try-it.md`, which holds a complete set of inputs for a worked run.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The account the meeting is with |
| Meeting type (`discovery` or `demo`) | Required | The method forks on this. If unclear, ask: "Is this a discovery call or a demo?" |
| Attendees with titles | Required | Persona matching drives the questions and the proof. A name the record does not hold is written `[Unknown]`, never guessed |
| Call date, time and length | Optional | Used for the call flow. Without a length, the flow uses a 30-minute call and says so once |
| CRM notes and prior call notes | Optional | Read in Step 2. A blank field is unknown, not a no |
| Known competitor or incumbent | Optional | Sharpens the competitive probes |
| Upstream outputs named in Integration | Optional | Read by name in Step 1. A missing one is reported as missing, not rebuilt here |
| Rep running the prep | Optional | Names the owner of the next action. Without it, the owner is the account's AE owner on the record, and the header says the owner came from the record |

**Prerequisite (demo only):** the record must hold confirmed pain before a demo plan is built. Step 0 runs this check.

---

## Output Contract

Every run produces one prep sheet with the same sections in the same order. The content changes per account. The structure never does, so a manager scanning many sheets never has to relearn the layout.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `prep_sheet` | Inline in the reply | One sheet, seven sections, in the order set out in The Prep Sheet Sections below |
| `top_pain` | Section 2 of the prep sheet (demo: Section 1) | One line, tagged. Discovery: the highest-ranked hypothesis. Demo: the first confirmed pain. Reads "none confirmed" when discovery has not confirmed one |
| `question_bank` | Section 3 of the prep sheet (demo: Section 4) | Discovery: the top three questions for each of Situation, Problem and Implication, and the two Need-Payoff questions, each with its listen-for phrase. Demo: four questions per module |
| `attendees` | Header of the prep sheet | Each attendee's name or `[Unknown]`, title, and buying role as the record names it |
| `proof_point` | Section 5 of the prep sheet | One usable proof point per attendee persona, with its Status shown, or a line that says none is usable and gives the research target. An Illustrative row is never the proof line |
| `next_action` | Last line of the prep sheet | The owner and the date. Wrap-Up reads this line. When more than one step is open, the next action is the highest-ranked of these kinds, and the rest are later steps. (1) A reply owed to a buyer who wrote to us, due the next business day. (2) A confirmation the booked meeting cannot run without, such as the form filler, the attendees, or whether discovery or demo runs. (3) The ask on the call for the buyer's own words on the top pain, while Identified Pain is not green. (4) The ask for the signer above the buyer and the next meeting date, while Economic Buyer is yellow or red. (5) The follow-up email after the call, as a DRAFT. An ask to the same person in the same message travels with the first ask. Ties go to the earlier date, then to the step the rep owns |
| `report_path` | Header of the prep sheet | `none (inline)` unless a file was written |
| File option | Written only when the user asks | Named `<account>_<skill>_<date>.md`, saved beside the user's other account notes. Never written by default |

### The Prep Sheet Sections

**Discovery Prep (seven sections):**

1. **Call Header:** account, status, attendees with buying role, objectives, `report_path`.
2. **Pain Hypotheses:** ranked, each tagged, with `top_pain` marked.
3. **Discovery Question Bank:** the top three questions per phase, the follow-up ladder, and the listen-for phrases with their source.
4. **Qualification Gaps:** a traffic-light grid (known green, partial yellow, unknown red). Each yellow or red cell has the question that fills it.
5. **Competitive Positioning:** the incumbent, the probes as questions, and the differentiators, each proof point with its Status.
6. **Meeting Scripts:** the open, the close, the objection scripts and the follow-up email draft.
7. **Call Flow And Timing:** the minute-by-minute flow and two or three if-then scenarios. The sheet ends with `next_action`.

**Demo Prep (seven sections):**

1. **Demo Header:** account, attendees with buying role, confirmed pains, objectives.
2. **Pain-To-Workflow Map:** ranked pains, the workflow for each, the differentiating feature, and the share of demo minutes.
3. **Demo Script:** the three-beat arc and the time-blocked structure, with the habit each block practices.
4. **Question Cards:** four questions per module.
5. **Proof And Feel-Felt-Found:** one proof point per attendee persona, with its Status, and the stories scripted.
6. **Meeting Scripts:** the open and close, built from the discovery pains, and the follow-up email draft.
7. **Resistance Playbook And If-Then Scenarios:** typed objections with their responses.

---

## Context

This skill carries no company facts of its own. It reads them from the profile, the file named in The Shared Contract below. That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`. It reads these sections, and nothing else:

| Profile Section | Used For |
|---|---|
| Company | Framing and the meeting open |
| Buyer Personas | Persona matching for attendees, questions and proof |
| Core Pain Points | Pain hypotheses. The Business Impact column, the What to Listen For column and the Discovery question column |
| Value Propositions | The three-beat demo arc, the differentiators and the cash impact |
| Proof Points | One proof point per attendee persona, used by its Status |
| Competitive Landscape | Competitor probes (as questions) and the incumbent's pain |
| Qualification Stage Gates | Stage names, used by number and name as written |
| Sales Methodology | The team's framework names and any talk-time override |
| Meeting Prep | The team's discovery vocabulary, the persona-proof map and the demo reframe. This is the sales-layer section this skill writes and reads |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls, decisions and prior meeting history for that account), read in Step 2 as the interaction history |

If the Meeting Prep section is missing, the skill runs uncustomized. It says so once at the start, and it marks every output that depended on that section as generic: the vocabulary, the persona-proof map and the demo reframe. A missing Discovery question cell is written as a question built from the pain's What to Listen For phrase, and marked `[Inferred]`.

The Shared Contract below governs the tags, status words, verdict words, stage handling, champion tests, incumbent types and talk-time bands. Every skill in the family uses it word for word.

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

---

## Methodology

Your playbook, in code. The defaults below are SPIN for discovery and a Challenger-style structure for demos. The team's own framework names and stage words come from Sales Methodology and the Meeting Prep section, and they take precedence. Public framework names only. Where the team has its own name for a step, use the team's name on the sheet, because the rep speaks it on the call.

### Discovery: SPIN Question Framework

| Phase | Goal |
|-------|------|
| **Situation** | Understand how they operate today: process, tools, team, volume |
| **Problem** | Surface the financial, operational and personal cost of the current state |
| **Implication** | Understand the knock-on effects and what they have already tried |
| **Need-Payoff** | Let the buyer say what solving the problem would be worth |

### Discovery: Follow-Up Ladder

When a buyer confirms a pain, follow it up in four steps. The team may know this ladder by its own name, which Sales Methodology supplies.

| Stage | Follow-Up |
|-------|-----------|
| **1. Identify** | "Walk me through what that looks like, step by step." |
| **2. Prioritize** | "On a scale of 1 to 10, how urgently does this need to change?" |
| **3. Quantify** | "What does this cost you per [period], in time, money or risk?" |
| **4. Map stakeholders** | "Who else does this affect, and whose job is it to solve it?" |

**Rule:** run stages 1 and 2 on every confirmed pain before moving on. Run stage 3 on the top pain as well. The reason: a pain with no sense of its urgency earns no commitment, and a top pain with no number cannot justify the next meeting.

### Demo: Five Demo Habits

A demo is a checklist of habits, not a tour of the product.

| Habit | What Good Looks Like |
|-------|----------------------|
| **Open on the top pain** | The first workflow shown answers the pain the buyer ranked highest |
| **Spend time in order of importance** | The most important pain gets the most minutes |
| **Use their words** | One idea at a time, in the buyer's own language, no jargon |
| **Show proof that looks like them** | A customer story from the same vertical and the same role, with its Status shown |
| **Let them talk** | A what or how question after every workflow |

### Demo: Four Questions Per Module

| # | Question | When | Purpose |
|---|----------|------|---------|
| 1 | **Prime the pain:** "Many teams struggle with [pain]. To what extent is that true for you?" | Before the feature | Activates the pain |
| 2 | **Create contrast:** "How does this compare to how you handle it today?" | After the feature | Forces a side-by-side comparison |
| 3 | **Check requirements:** "Did I miss any requirement about [topic] that matters?" | At each transition | Surfaces hidden needs |
| 4 | **Make the buyer say it:** "What excited you most about what you saw today?" | At the close only | Captures buying reasons in their words |

### Demo: Three-Beat Arc

Every demo runs one arc, from the buyer's risk to the cash impact:

1. **The Buyer's Risk**, in their words: the pain as they named it.
2. **The Workflow Change**: what the product does differently, from Value Propositions.
3. **The Cash Impact**: the number from Value Propositions, with its Status. An Illustrative number is not shown as a result.

### Meeting Open And Close (Both Types)

| Part | What It Does |
|------|-------------|
| **Why we are here** | Connects this meeting to the last conversation or the reason it was booked |
| **Who and how long** | Confirms the time and who is in the room, and asks any new attendee about their role |
| **The plan** | Says what the meeting will cover and invites additions |
| **A good outcome** | Agrees what would make this meeting worth the time |

### Qualification Framework (Discovery)

Default: MEDDPICC, with its elements named Metrics, Economic Buyer, Decision Criteria, Decision Process, Paper Process, Identified Pain, Champion and Competition. Sales Methodology replaces it if the team qualifies differently. Champion is scored with the shared champion tests, not with a feeling.

### Objection Scripts

Every objection script has the same three parts:

1. **Acknowledge** the objection in the buyer's own words.
2. **Ask The Question** that tests it, drawn from the persona's objections in the profile.
3. **Feel-Felt-Found** only if a story exists with a Status that allows its use.

The reason for the question: a scripted rebuttal argues with the buyer. A question makes the buyer examine their own objection, and the answer is more useful to the rep than any rebuttal.

### Resistance Types (Demo)

| Type | Signal | Response |
|------|--------|----------|
| **Reactance** | Feels pressured, defensive, one-word answers | Back off. Give autonomy. Use negative framing |
| **Skepticism** | "Too good to be true," asks for proof, compares | Provide proof with its Status. Feel-Felt-Found. References |
| **Inertia** | "We've always done it this way," "Let's look later" | Quantify the cost of inaction, from the profile or the call |

---

## Quick Reference

**Use This Skill When:**
- Preparing for a discovery call: a first meeting, a follow-up, or a re-engagement
- Preparing for a demo, after discovery has confirmed pain
- Needing a one-page sheet to read during the call
- Needing a fast prep: the user says "quick prep"

**Don't Use When:**
- Building outbound sequences for cold accounts (use Account Snapshot, 02)
- Building competitive strategy for a deal (use Competitive Strategy, 11)
- Analyzing a call that already happened (use Call Coaching, 13)

**User Roles:** AE (primary), BDR (discovery only).

---

## Core Workflow

The order matters. The meeting type decides the method, so it comes first. Pain comes before proof, because a proof point answers a pain. The question bank comes after the pain, because each question is built from a hypothesis. The call flow comes after the question bank, because each block of the flow consumes questions from it. The sheet is assembled last, so no gap can hide in an earlier step.

### Step 0. Detect The Meeting Type

Read `meeting_type` from the request.

**Discovery Words:** discovery, disco, first meeting, initial call, re-engagement.
**Demo Words:** demo, demonstration, show them, product walk-through.

If the type is unclear, ask: "Is this a discovery call or a demo?"

**Prerequisite (demo only).** Count the confirmed pains and the quantified ones in the record. A demo needs at least two confirmed pains and one with a quantified impact. These match the Stage 2 exit criteria in (profile: Qualification Stage Gates). If the count falls short, the prep becomes a discovery-first recommendation. It names what is missing and sends the rep back to the question bank in Step 4. It offers two options, and the rep chooses between them: run discovery prep for the meeting, or keep the demo and open with five to ten minutes of discovery questions. The skill does not choose for the rep, because a demo built on unconfirmed pain is a feature tour.

**Produces:** `meeting_type`, and the prerequisite result (pass, or the missing items named).

### Step 1. Gather Intelligence

Before pulling anything, open the account's folder under `accounts/` in the Knowledge Base, if the profile has one, and offer the CRM read and, when a call recorder is connected, the call read, for the one account or date range you name. Nothing is read from the CRM or the call recorder until you say yes.

1. **Confirm Inputs:** account name, meeting type, attendees with titles, call date and length, other team members attending.
2. **Read The Profile Sections** named in Context. Take the stage names from Qualification Stage Gates.
3. **Read The Upstream Fields By Name** if they are present, as listed in Integration With Other Skills. Report any missing one as missing. An upstream field is read as of its own run date. Where it conflicts with a rule here, the rule here governs, and the sheet names the conflict. A renewal or deadline in an upstream pain list is read as urgency, not a pain, and it is never ranked as a hypothesis.
4. **Build The Account Profile:** company, vertical, size, states, status, deal amount, the rep, and the attendees with buying role. The status is one of the status words in the Shared Contract, read from the CRM on the run date. When the CRM holds the date the deal opened, the header states it. An upstream status such as TARGET is labelled "then" with the date of its own run, and it does not set the header. An ENGAGED account is labelled so in the header, and its reply is listed as a finding in Step 2.

**Produces:** the account profile table and the attendee table. Each attendee has a name or `[Unknown]`, a title, and a buying role as the record names it.

### Step 2. Analyze The Interaction History

1. **Extract Findings** from the CRM notes and prior calls, each tagged with its source:
   - Pains already named. Do not re-ask what the buyer has already said.
   - Questions the buyer asked, which show their priorities.
   - Objections raised.
   - People referenced and the stakeholders they point to.
   - Competitors named.
   - The trigger that started the engagement.
2. **Identify Gaps:** pains named but not quantified, people referenced but not met, a decision process not mapped, budget or timeline unknown, the current solution unclear. Each gap becomes a meeting objective. A blank field is unknown, never a no. A fact from a call whose date is unknown takes `[Call, date Unknown]`, the shared contract's form for an undated call, which places no fact in time.

**Produces:** the findings list, each item tagged, and the gap list.

### Step 3. Build The Pain Intelligence

Branch by meeting type.

**Discovery.** Build three to five pain hypotheses from Core Pain Points. For each one, give:

- **Pain Hypothesis:** a specific statement, in the buyer's terms.
- **Evidence:** tagged with its source.
- **Business Impact:** filled from the Business Impact column of (profile: Core Pain Points) or from the call, with its tag. If neither supplies one, write `[Unknown]`. Never write a figure without a source.
- **Urgency:** the trigger or deadline, tagged, or `[Unknown]`.
- **Strength:** the strongest tag on the evidence. A pain the buyer named on a call (`[Call]`) outranks one reasoned from other facts (`[Inferred]`).

Rank the hypotheses by that strength, in this tag order: `[Call]`, then `[CRM]`, then `[Notes]`, then `[Public: source]`, then `[Inferred]`. Lead with the strongest. Use the weakest as negative framing questions, not as statements. A record fact that shows the cost of a pain is evidence for that pain, not a second hypothesis, and a renewal or deadline is an urgency, not a pain. Two hypotheses that still tie on tag take the order of Core Pain Points.

**Demo.** List every confirmed pain and rank it by:

1. Business impact, the largest quantified impact first.
2. Product differentiation, where the product's advantage is strongest.
3. Attendee relevance, which pains matter to the people in the room.

Assign the share of demo minutes, not talk time. The top pain takes the largest share (40 to 50%), the second takes 25 to 35%, and a third takes 15 to 20% if time allows. The rule is fixed: the top pain is shown first.

State the top pain in one line for `top_pain`.

**Produces:** the ranked hypotheses (discovery) or the ranked confirmed pains with time shares (demo), and `top_pain`.

### Step 4. Prepare The Question Bank

Branch by meeting type.

**Discovery.** Build questions for each SPIN phase, tied to the hypotheses:

- **Situation (4 to 6 questions):** process, tools, team, volume. Listen for: manual work against automated work, team size, gaps in the tools.
- **Problem (4 to 6 questions):** the cost of the current state, one per pain, using the Discovery question column of (profile: Core Pain Points) as the anchor.
- **Implication (3 to 4 questions):** what they have tried, past evaluations, why earlier attempts stopped.
- **Need-Payoff (two questions):** value framing for the weaker hypotheses. A benchmark may appear in the question only with its source and date named.

Each question carries its listen-for phrase from the What to Listen For column. A phrase the buyer has said in the record is quoted as theirs. A phrase from the profile is labelled as the profile's, because the buyer has not said it yet. Write each phase's range from the profile's questions first, then from the record and the hypotheses, in that phase's goal. Rank the questions in a phase by the hypothesis they test, strongest first, and keep the profile's order within a hypothesis. The sheet shows the top three questions for Situation, Problem and Implication, and both Need-Payoff questions. A phase with fewer questions than its count shows the ones it has.

Apply the follow-up ladder rule from the Methodology. For a vague answer, ask for specifics with plain probes: "Walk me through that," "What happens next," "Describe the last time it happened."

**Demo.** For each module, take the four questions from the Methodology. Question 4 is asked at the close, not per module.

**Produces:** the question bank for each discovery phase (discovery), or the question cards per module (demo).

### Step 5. Frame The Call

**Discovery: Qualification Pre-Fill.** For each element of the team's qualification framework, mark what is known (green), partly known (yellow) or unknown (red). Each yellow or red cell gets the question that fills it. Identified Pain needs at least one pain quantified, which is the stage 3 depth target. Metrics is green when the record holds a figure for the outcome the solution moves and the buyer has agreed it, yellow when that figure is recorded but not agreed, and red when no such figure is recorded, because account size such as a plot count describes the account and never scores the cell. Economic Buyer is green when the record names the person who signs at this deal's value, yellow when a buyer is named but the signer above that buyer's limit is not confirmed, and red when no buyer is named. Identified Pain is green when the buyer has named one pain in their own words and it is quantified, yellow when the buyer has named a pain but it is not quantified, and red when the buyer has named none. A pain the rep infers from the CRM, the profile or the facts of an account is a hypothesis for the call to test, so it scores red until the buyer names it. An incident count does not quantify a pain: a pain is quantified only when its cost is stated in plots, hours or dollars, as the Stage 2 gate in (profile: Qualification Stage Gates) requires. Champion is green on a Strong result from the shared champion tests, yellow on Developing and red on None. Decision Criteria, Decision Process and Paper Process have no cell rule of their own, so they take the default: known green, partial yellow, unknown red. Competition is green when the incumbent is known and the buyer has stated a preference among the options, yellow when the incumbent is known and no preference is on record, and red when no incumbent is known. A label in the profile, such as a champion named in the Example Cast or a signer named in a role-title map, never sets a cell. The record sets it, and the champion cell takes the shared champion tests on tagged evidence.

**Demo: Pain-To-Workflow Map And Structure.** Map each pain to a workflow, the differentiating feature, and the proof that makes it land, with its Status. Plan the demo as: the opening (three to five minutes), a problem slide built on the three-beat arc, a block for each pain in order of importance, and a recap and close. Check the five demo habits before the sheet is handed back.

**Minute-By-Minute Call Flow.** Turn the blocks into minute ranges that add up to the call length. Each block names the question bank section it uses. The flow notes the shared talk-time band for the call type, or the profile's override when Sales Methodology gives one. It does not restate the numbers.

A discovery flow for a 30-minute call (illustrative) looks like this:

| Minutes | Block | Uses |
|---------|-------|------|
| 0 to 3 | Opening | Meeting Open |
| 3 to 11 | Current state | Situation |
| 11 to 21 | Pain, with the follow-up ladder | Problem, Need-Payoff |
| 21 to 24 | Alternatives | Implication |
| 24 to 27 | Value connection | Proof, at its Status |
| 27 to 30 | Close | Meeting Close |

**Produces:** the qualification pre-fill (discovery) or the pain-to-workflow map (demo), and the call flow, which adds up to the call length.

### Step 6. Prepare Competitive Intelligence

1. **Identify The Current Solution** from the CRM and the history. Tag how the team knows it, and note the contract status and satisfaction if the record holds them. A blank is `[Unknown]`.
2. **Name The Incumbent Type** using the shared incumbent types in The Shared Contract, tagged with its source.
3. **Write The Competitor Probes As Questions Only.** Use the Competitive Discovery Questions in (profile: Competitive Landscape) and the probes for that incumbent type. A stated weakness of a competitor carries a source, such as `[Public: source]` or `[Call]`, or it is labelled a hypothesis with `[Inferred]` and its reasoning. The reason: a rep who states a rival's weakness as fact, and is wrong, loses credibility in the room.
4. **Choose Two Or Three Differentiators** from Value Propositions. Give each one a matched proof point, with its Status.

**Produces:** the incumbent with its tags, the probes as questions, and the differentiators with their proof.

### Step 7. Select Proof And Prepare Resistance

1. **Choose One Proof Point Per Attendee Persona** from Proof Points. Match on persona first, then vertical, size and pain. Use the proof by its Status:
   - **Verified:** may be cited to the prospect.
   - **Benchmark:** context only, with its source and date named. Never "our customer got this."
   - **Illustrative:** never cited to a prospect, and never the proof line.

   Every attendee gets one proof line, including an attendee whose persona is not yet known. That line says the persona is unknown and that no proof is set until it is confirmed. If the profile has no usable proof for a persona, the sheet says so and gives the research target in its place. The proof line is a usable row only: a Verified row from Proof Points, or a Benchmark row from Proof Points whose wording matches the persona's Hook Focus. The research target is the profile figure whose wording matches the Hook Focus, with its research source named. If that figure has no dated source, state it as "target, no dated source", and do not present it as a benchmark. A research target keeps the status the profile gives its figure: a figure the profile labels a Benchmark, with its source and date, is shown as one, and any other figure is shown as a research target. An Illustrative row does not make a persona usable, and it is never the proof line. The reason: a rep who says "we have no proof for this yet" is more credible than one who reaches for a row that does not exist.
2. **Script Two Or Three Feel-Felt-Found Stories:** Feel (validate their concern), Felt (a similar customer felt the same), Found (the outcome, with a metric whose Status allows its use). If no story can carry a Verified or Benchmark result, the Found line uses the Benchmark and says so.
3. **Prepare Typed Resistance** (demo): Reactance, Skepticism or Inertia, each with its response from the Methodology.
4. **Prepare The Redirect:** if a buyer asks about something the product does not lead with, acknowledge it and return to the pain they ranked first.
5. **Watch For Buying Signals:** pricing questions, internal selling ("my CFO would love this"), volume and scale questions, timeline questions.

**Produces:** one proof point per attendee persona with its Status, the Feel-Felt-Found stories, and the resistance responses.

### Step 8. Script The Open, The Close And The Follow-Up

1. **The Open** follows the Meeting Open and Close part by part, built from the record. A first meeting, which is one with no earlier logged meeting with the attendees, asks how the buyer's team handles the process. A follow-up names the pain they raised last time. A demo quotes discovery back in the buyer's words: name the attendee, then say the pain as they said it.
2. **The Close:** recap what matters most in the buyer's words, ask who else belongs in the next conversation, propose the next agenda from what was discussed, and agree the next milestone with an owner and a date.
3. **The Objection Scripts** from the Methodology, one for each objection that (profile: Buyer Personas) lists for the persona.
4. **The Follow-Up Email Draft:** a short note to the attendees, marked DRAFT, not sent. It names the pain in the buyer's words, carries at most one proof point with its Status (Verified or Benchmark only), and states the next step with an owner and a date. The rep reads it and sends it.

**ENGAGED Accounts.** When the account is ENGAGED (it replied or met with us, and no deal is open), the open names that reply, its date and the words the buyer used, and it does not restart as a cold first meeting. A reply is not a meeting, so a first meeting with an ENGAGED account is still a first meeting under the rule above, but its open leads with the reply. The reply is a finding in Step 2, tagged `[CRM]` or `[Call]` with its date.

**Produces:** the open, the close, the objection scripts and the follow-up email draft.

### Step 9. Build The Game Plan

1. **Objectives.**
   - Discovery: validate or disprove the top two or three hypotheses. Run the follow-up ladder per the rule. Identify the economic buyer and the decision process. Secure a next step with a date, attendees and an agenda.
   - Demo: show the top two pains with contrast to the current state. Capture at least two buying reasons in the buyer's own words. Secure a next step with a date, attendees and a decision point.
2. **Minimum Acceptable Outcome.** Discovery: one validated, quantified pain and a scheduled next step. Demo: the buyer confirms the product addresses the top pain and agrees to a next step.
3. **If-Then Scenarios.** Write five to eight, specific to the meeting type, each with its reason in a few words.
4. **Team Roles,** if others attend: what each person does in the room.

**Produces:** the objectives with the minimum outcome, the if-then scenarios and the roles.

### Step 10. Assemble The Prep Sheet

Lay out the sheet in the section order from The Prep Sheet Sections. Fill the header with the attendees and `report_path: none (inline)`. End the sheet with `next_action`, which names an owner and a date. The date follows the shared contract's next-action rule. When the next action happens on a call whose date is on record, that call date is used and named as its source, as long as it falls before the five-business-day date. The next action is the highest-ranked open step in the Output Contract's order, and asks made to the same person in the same message travel with it. When the Economic Buyer cell is yellow, the signer above the named buyer and the next meeting's date are asked on the call. Write the signer's title only as the record names it. If the record names no signer, the next action asks for the signer's name, and the title stays `[Unknown]`. Hand the sheet back in the reply. Write a file only if the user asks, using the file option. Run the Quality Bar before handing back.

**Produces:** `prep_sheet` (inline), `top_pain`, `question_bank`, `attendees`, `proof_point`, `next_action` and `report_path`.

---

## Modes

Two meeting types, and one depth setting.

- **Discovery** and **Demo** are chosen by `meeting_type`. Discovery is the default when a request says "a bit of both." A demo always runs the prerequisite check first.
- **Quick Call Prep** shortens the output. It is triggered by "quick prep" or "calling in 5 minutes." It keeps Steps 1 to 4, and Steps 8 and 9, in short form, and it skips the file option. It is off by default, because a full sheet is the standard output.

---

## Epistemic Rules

- **Every Rate Carries Its N.** "4 of 7 criteria," never "57%" alone.
- **Silence Is Not A No.** A blank CRM field is unknown and is written `[Unknown]`. It is never written as "no."
- **Every fact carries one of the six evidence tags** from The Shared Contract. A fact with no tag is removed from the sheet.
- **A benchmark needs a named source and a date.** Without both, it is removed.
- **A proof point is used by its Status only.** A Verified row may be cited to a prospect, a Benchmark is context, and an Illustrative row is never cited.
- **A Recurring Pattern Needs Five Cases.** Fewer than five is an observation, and the sheet says so in the same sentence.

---

## Hard Rules

1. **Never build a demo plan on pain that discovery has not confirmed.** A demo on unconfirmed pain is a feature tour, and a buyer who has not named a cost has no reason to buy.
2. **Never cite an Illustrative proof point to a prospect.** An Illustrative row describes an invented case. A buyer who asks for the reference finds nothing.
3. **Never write a business impact figure without its source.** A figure the buyer checks and cannot trace costs more trust than a blank, so a blank stays `[Unknown]`.
4. **Never invent an attendee, a name, a title or a buyer quote.** The rep says these words out loud. An invented quote makes the first minute of the call a lie.
5. **Quote The Buyer Only From The Record.** A profile phrase is the team's guess at the words. Only the buyer's own words count as evidence, so a profile phrase is labelled as the profile's.
6. **Never Restate The Talk-Time Bands.** The shared bands in The Shared Contract, or the profile's override, are the only figures. One table prevents two numbers for one coaching metric.
7. **Never Send, Enroll Or Write To The CRM.** The rep reads the draft and decides. A sent email cannot be unsent.
8. **Use the team's names from the profile, and public framework names otherwise.** The rep uses the words the team uses on calls, so the buyer hears one vocabulary.
9. **A competitor's weakness carries a source, or it is labelled a hypothesis.** A rival's weakness stated as fact, and found wrong, loses credibility in the room.

---

## Quality Bar

Done when all are true:

- [ ] The meeting type is set, and the prerequisite result is stated (demo: pass, or the missing items named).
- [ ] `top_pain` is one line, tagged, and matches the top hypothesis (discovery) or the first confirmed pain (demo).
- [ ] Every business impact figure carries a source tag, or it reads `[Unknown]`.
- [ ] Every attendee is named from the record or marked `[Unknown]`, with a buying role.
- [ ] Each attendee has one proof line: a usable row with its Status, or "none usable" with a labelled research target. No Illustrative row is cited to the prospect.
- [ ] The question bank covers each discovery phase, and each listen-for phrase shows its source.
- [ ] The follow-up ladder rule is met: stages 1 and 2 on every confirmed pain, stage 3 on the top pain.
- [ ] The call flow adds up to the call length, or to the stated 30-minute default.
- [ ] Talk time is stated as the shared band or the profile's override, with no restated numbers.
- [ ] The follow-up email is marked DRAFT, not sent.
- [ ] `next_action` names an owner and a date, and it is the highest-ranked open step in the Output Contract's order.
- [ ] An ENGAGED account's open names its reply and the reply's date, and the sheet does not restart it as a cold first meeting
- [ ] Every rate carries its n, and every fact carries a tag.
- [ ] Demo only: pains are ranked, the shares of demo minutes add up, the top pain is shown first, and the five demo habits are checked.
- [ ] Discovery only: each yellow or red qualification cell has the question that fills it.

---

## Examples

All four examples use PlotIQ and its cast from the profile's Example Cast. Facts marked `(illustrative)` are invented for the example. The hand-off block at the end of each example lists the Output Contract fields by name.

### Example 1: Discovery Prep For The Flagship Account (Brackhaven Memorial Gardens, Stage 2)

**Context:** Brackhaven Memorial Gardens is a combination: two sites, 11,000 plots and paper plot maps `[CRM]`. It had one double sale in the last 24 months `[CRM]` (illustrative). The GM, Ruth Ellery, is the buyer's first contact. Operations Director Walt Okonkwo is an influencer. At the time of this call the account sits at Stage 2 Discovery, so its status is ACTIVE at Stage 2. The AE is Owen Pruitt. Priscilla Dunmore, the pre-need manager, is the end user and is not on this call `[CRM]`.

**Input:** "Discovery prep for Brackhaven. Ruth Ellery and Walt Okonkwo are on the call. Thirty minutes."

**Step 0.** `meeting_type = discovery`. The demo prerequisite does not apply.

**Step 1.** Account profile: combination, two sites, 11,000 plots `[CRM]`. Status ACTIVE, Stage 2 Discovery `[CRM]`, with the deal opened on 2026-05-06 `[CRM]` (illustrative). Upstream from Account Snapshot (02), run on 2026-05-04 when the account was TARGET: `account_status: TARGET (then)` and `verdict: GREENLIGHT`. Its `contact_priority` ranks Ruth Ellery first and Walt Okonkwo second `[Inferred]`, from the persona order in (profile: Buyer Personas). Its `pain_hypotheses` are plot records on paper across two sites `[CRM]`, and its urgency is the Oldgate renewal in March 2027 `[CRM]`, which is an urgency and not a pain (Step 1, item 3). Its `sequence` is three emails to Ruth Ellery, with call prep, drafted and not sent (illustrative). Attendees:

| Name | Title | Buying Role |
|------|-------|-------------|
| Ruth Ellery | General Manager | Buyer `[CRM]` |
| Walt Okonkwo | Operations Director | Influencer `[CRM]`. Skeptical of tablets `[Notes]` |

**Step 2.** Findings: Ruth named the incumbent, Oldgate Ledger Pro, and it was logged `[CRM]`. A second system, Stonemark mapping, was also evaluated, with no preference stated `[Notes]`, undated. Gaps: the plot loss is not quantified. The economic buyer is not named `[Unknown]`. The approval process is not mapped `[Unknown]`.

**Step 3.** Pain hypotheses, ranked by the strength of their tags:

1. **Plot Records On Paper, With A Double Sale.** Top pain. Evidence: paper plot maps `[CRM]`, and one double sale in 24 months `[CRM]` (illustrative). The double sale is the cost of those records, so it is evidence for this pain, not a second hypothesis. Business impact: unsold plots nobody knows exist (profile: Core Pain Points). The research hook is 50 to 100 plots `[Public: deathcare research, paper-operations note, 2026-04-01]`. Brackhaven's own count is `[Unknown]`.
2. **Trust Fund Reporting By Hand.** `[Inferred]` from the paper records and the annual filing rule in (profile: Industry Context). The filing that applies depends on the state, which is `[Unknown]`.
3. **Pre-Need Leads Without A Follow-Up Owner.** `[Unknown]`. No pre-need activity is recorded. Negative framing: "Do you take pre-need calls, and who calls back?"

**Top Pain:** plot records on paper, with a double sale `[CRM]` (illustrative).

**Step 4.** Question bank, top three per phase:

- **Situation:** "Walk me through how a plot sale is recorded, from the first call to the deed." "Who keeps the plot maps, and where?" "How many sales come through the office in a month?"
- **Problem:** "When a family asks about a plot, where do you look first, and how long does it take?" Listen for: "We have files that date back to the 1970s," a profile phrase Ruth has not yet said. "How many plots could you sell today if the records were right?" "Walk me through last year's trust filing. Who pulled the numbers, and from where?"
- **Implication:** "What have you tried to fix the plot records before, and why did it stop?" "What happened the last time a family was given a plot that was already sold?" "Who could answer a family's question about a plot if the person who keeps the maps were out for a month?"
- **Need-Payoff:** "Most cemeteries your size carry 50 to 100 plots sold on paper and unsold on the map. Is that close to your experience?" (Benchmark, deathcare research, paper-operations note, 2026-04-01.) "If the plots the map is hiding were sold, what would that be worth to the office in a year?"

Follow-up ladder on the top pain: stages 1 and 2 when confirmed, and stage 3 on the top pain: "What does a double sale cost you, in money or in family trust?"

**Step 5.** Qualification pre-fill:

- **Metrics: Red.** No plot-loss figure is recorded `[Unknown]`. The plot count (11,000) describes the account and the double sale describes the problem, so neither scores the cell.
- **Economic Buyer: Yellow.** Ruth is the buyer. The likely signer is above her `[Inferred]`. Two sites at the list price in (profile: Product Modules) come to $21,576 a year, plus the $5,000 setup, for $26,576 in year one. That is above the $25K board line in (profile: Qualification Zones), so the GM cannot sign alone on the record.
- **Decision Criteria: Red.** None are stated.
- **Decision Process: Red.** The approval body and its meeting dates are `[Unknown]`. Question: "Who has to approve a purchase above the board line, and when does that group meet?"
- **Identified Pain: Red.** The buyer has named no pain on record. The paper plot maps and the double sale are CRM facts about the account, so they are the hypothesis this call tests, not Ruth's words. The cell turns yellow when Ruth names a pain, and green when she quantifies it.
- **Champion: Red.** The shared champion tests cannot be scored from a first discovery call. They are scored after the call.
- **Paper Process: Red.** No legal, vendor or signing steps are on record.
- **Competition: Yellow.** The incumbent, Oldgate Ledger Pro, is known `[CRM]`. The second system, Stonemark, was evaluated, and no preference is on record `[Notes]`, undated.

Totals: 0 green, 2 yellow and 6 red, of 8 elements.

**Step 6.** Competitive: the incumbent is Oldgate Ledger Pro `[CRM]`, an incumbent of the direct-software type in the shared list. Renewal is March 2027 `[CRM]`. Probes, as questions: "When does the Oldgate contract renew, and what did the last quote include for support?" and "Where does the plot map live today, and when was it last updated?" Oldgate's mobile weakness matters only if the grounds crew still uses paper work orders `[Inferred]`.

**Step 7.** Proof for Ruth Ellery, the GM: none usable. Proof Points holds no Verified row, and its two Benchmarks, the pre-need share and the federal penalty framing, do not match her hook of unsold plots. The research target is 50 to 100 plots sold on paper and unsold on the map (Benchmark, deathcare research, paper-operations note, 2026-04-01). Holloway Hills, Status Illustrative, is not the proof line and is not cited. For Walt Okonkwo, no usable proof exists, so his line gives the target, labelled "target, no dated source": a plot answer in 20 seconds (profile: Value Propositions).

**Step 8.** Open: "Ruth, thanks for making the time. Before we go further, how are the plot records kept at Brackhaven today?" Close: recap the pain in Ruth's words, ask who else belongs in the next conversation, and agree the next date with an owner.

**Step 9.** Objectives: confirm the top pain, quantify it, name the economic buyer and the approval process, and secure a next date. Minimum outcome: one validated, quantified pain and a scheduled next step.

If Ruth confirms the double sale and gives a count, run stage 3 and ask who approves above the board line. If she says the records are fine, ask for the last state filing. If she names an approval body, ask for the next meeting date and the name of its chair.

**Step 10.** Call flow, 30 minutes (illustrative), with the discovery band from the Shared Contract. PlotIQ has no talk-time override in (profile: Sales Methodology) yet.

```text
Hand-off (read by 07 and 13):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 2 Discovery at the time of the call)
run_date: 2026-05-11 (illustrative, the day before the Stage 2 call)
prep_sheet: inline, discovery, seven sections
top_pain: plot records on paper, with a double sale [CRM] (illustrative)
question_bank: Situation 3, Problem 3, Implication 3 (top three each), Need-Payoff 2
attendees: Ruth Ellery, General Manager, buyer. Walt Okonkwo, Operations Director, influencer
proof_point: Ruth Ellery, none usable, research target 50 to 100 plots (Benchmark, 2026-04-01). Walt Okonkwo, none usable, target a plot answer in 20 seconds (target, no dated source)
next_action: Owen Pruitt asks Ruth Ellery on this call, in her own words, what the paper records and the double sale cost in plots, hours or dollars (rank 3: Identified Pain is red). In the same message he asks who signs above her and for the next meeting date (rank 4, travels with the first ask). Date: 2026-05-12 (illustrative), the call date on record, which is earlier than the five-business-day date of 2026-05-18. The meeting date is [Unknown] until agreed
report_path: none (inline)
```

### Example 2: Prep For An Inbound Request (Sable Fork Cemetery, MANUAL REVIEW)

**Context:** Sable Fork Cemetery has one site, 2,900 plots and a plot list in a spreadsheet `[CRM]`. The GM, Arlen Biggs, signs under $25K `[CRM]`. The account is INBOUND. Someone filled in the website form on Thursday 2026-10-15, four days ago, and asked for a demo. The form filler is `[Unknown]` until confirmed. The BDR replied to the form on the afternoon of 2026-10-19 and booked discovery for Thursday 2026-10-22 `[CRM]`. This prep is written on the run date, 2026-10-19, after that booking, so the call it prepares is the booked call. The verdict is MANUAL REVIEW, with Zone 3 HIGH the only HIGH zone. The account stays INBOUND, not ENGAGED, because INBOUND stays until a deal opens (Shared Contract), so the booked call does not change its status.

**Input:** "Prep me for the demo with Sable Fork on Thursday."

**Step 0.** The request says demo. The record holds no discovery findings, so the prerequisite fails: no confirmed pain and no quantified impact. The skill builds a discovery prep (`meeting_type = discovery`). A demo before discovery would show features without a confirmed pain.

**Step 1.** Upstream from Account Snapshot (02): `account_status: INBOUND` and `verdict: MANUAL REVIEW`. The zones are 1 MEDIUM, 2 LOW, 3 HIGH, 4 MEDIUM and 5 LOW. Zone 2 is LOW on pre-need: none `[CRM]`. Zone 5 is LOW on plot sales flat for three years, with no succession plan on the record `[CRM]`. Attendees:

| Name | Title | Buying Role |
|------|-------|-------------|
| Arlen Biggs | General Manager | Buyer, signs under $25K `[CRM]` |
| `[Unknown]` | Form filler | `[Unknown]`, to confirm on the call |

**Step 2.** Findings: the website form request on 2026-10-15 `[CRM]`, and the BDR's reply and discovery booking for 2026-10-22 `[CRM]`. No prior calls `[CRM]` before that booking. Gaps: no confirmed pain, no quantified impact, no champion, and no decision process beyond the GM's signature.

**Step 3.** Pain hypotheses, ranked:

1. **Plot Lookups On A Spreadsheet.** `[Inferred]` from the plot list `[CRM]` and the lookup pain in (profile: Core Pain Points), which takes minutes to hours. Not measured. Business impact `[Unknown]`.
2. **Unsold Plots Nobody Can See.** `[Inferred]` from the same spreadsheet and the paper-to-digital gap in (profile: Core Pain Points). The GM may not know how many plots are open `[Unknown]`.
3. **Pre-Need Leads With No Follow-Up.** Not supported by the record: pre-need is none `[CRM]`, and the GM sells plots directly, with no counselor and no intake form. Kept as a question only: "Do you sell pre-need?"

**Top Pain:** none confirmed. Working hypothesis: plot lookups on a spreadsheet `[Inferred]`.

**Step 4.** Question bank, top three per phase:

- **Situation:** "Where does the plot map live today, and when was it last updated?" "Who looks up a plot when a family calls, and how long does that take?" "Which system runs the funeral side, and who maintains it?"
- **Problem:** "What does a 20-minute lookup cost you, versus 20 seconds?" Listen for: "Give me a day and I'll find it," a profile phrase not yet heard. "When a family asks about a plot, where do you look first?"
- **Implication:** "What happened the last time a plot record was wrong?" "What did the last tool you tried do to the office?"
- **Need-Payoff:** "Independent cemeteries capture pre-need on 20% to 35% of at-need volume. Is pre-need something you sell?" (Benchmark, deathcare research, 2026-03-27 to 2026-04-01.) "If pre-need were sold, what would it be worth to the front counter in a year?"

**Step 5.** Qualification pre-fill:

- **Economic Buyer: Green.** Arlen Biggs signs under $25K `[CRM]`.
- **Identified Pain: Red.** None confirmed.
- **Metrics: Red.** No figures.
- **Decision Process: Yellow.** The GM signs, and nothing further is recorded `[CRM]`. Question: "Who else looks at a tool before you sign?"
- **Champion: Red.** None identified `[Unknown]`.

**Step 6.** Incumbent: none named in the record `[Unknown]`. Probes, as questions: "Where does the plot map live today, and when was it last updated?" and "When does your software contract renew, and what did the last quote include for support?"

**Step 7.** Proof for Arlen Biggs: none usable. Fennick Gardens is Status Illustrative, so it is not the proof line. The research target the prospect hears is the Benchmark line: "Most cemeteries your size carry 50 to 100 plots that are sold on paper and unsold on the map" (Benchmark, deathcare research, paper-operations note, 2026-04-01).

**Step 8.** Open: "Arlen, thanks for making the time. The request came in through the website, so I'd like to learn how the plot records work before I show you anything. How are the plots kept today?" Follow-up email: DRAFT, not sent.

**Step 7 (form filler).** The form filler's persona is `[Unknown]`, so the proof line for that attendee reads: no proof is set until the persona is confirmed on the call.

**Step 9.** Objectives: learn the plot-records process, find the pain, confirm the form filler, and identify who else looks at a tool. Minimum outcome: one confirmed pain with a number, and a discovery next step. If the GM says the spreadsheet works fine, ask when it was last checked against the plots actually sold. If the form filler is not Arlen, ask their role before any demo question.

**Step 10.** This prep has no demo plan. The demo is booked only after the pain is confirmed. Call flow, 30 minutes (illustrative), with the discovery band from the Shared Contract.

```text
Hand-off (read by 07 and 13):
account: Sable Fork Cemetery (INBOUND)
run_date: 2026-10-19
prep_sheet: inline, discovery, seven sections, demo held
top_pain: none confirmed. Working hypothesis: plot lookups on a spreadsheet, [Inferred]
question_bank: Situation 3, Problem 3, Implication 3, Need-Payoff 2
attendees: Arlen Biggs, General Manager, buyer (signs under $25K). Form filler: [Unknown]
proof_point: Arlen Biggs, none usable, research target 50 to 100 plots (Benchmark, 2026-04-01). Form filler, no proof until the persona is confirmed
next_action: the rep on the Thursday call asks Arlen Biggs first who filled in the website form and what role they hold (rank 2, a confirmation the call cannot run without), and in the same message asks what a plot lookup costs and how long it takes (rank 3, travels with it). Discovery runs, not the demo. Owner: the rep on the call, whom the records do not name (see the rep row in the Input Contract). Date: 2026-10-22, the discovery call booked on 2026-10-19 `[CRM]`, which is earlier than the five-business-day date of 2026-10-26
report_path: none (inline)
```

### Example 3: Shallow Discovery Holds The Demo (Greyfield Memorial Park)

**Context:** Greyfield Memorial Park has one site, 9,000 plots, a digital map from Stonemark, and a renewal in January 2027 `[CRM]` (profile: Example Cast). It runs a pre-need team of three, with an intake form on its website `[Public: company website]`. This prep is written on 2026-11-16. The pre-need manager replied to Email 1 on 2026-11-03 `[CRM]` (illustrative), and Owen Pruitt became the AE owner that day `[CRM]` (illustrative). Owen held one discovery call with the account on 2026-11-09 `[Call, 2026-11-09]` (illustrative). The call named the January 2027 renewal and confirmed no pain. No contact names are on file `[Unknown]`. The verdict is GREENLIGHT, with Zones 2 and 3 HIGH. The account is ACTIVE at Stage 2 Discovery `[CRM]` (illustrative). An AE has a demo on the calendar for Friday 2026-11-20 with the general manager and the pre-need manager, both unnamed.

**Input:** "Prep me for the demo with Greyfield on Friday. Attendees are the GM and the pre-need manager."

**Step 0.** `meeting_type = demo`. The prerequisite check runs and fails. The record holds one discovery call, which is shallow, not an empty record:

- Confirmed pains: 0 of 2 needed.
- Quantified impact: 0 of 1 needed.
- Follow-up ladder runs on a confirmed pain: 0 of 2 needed, since no pain is confirmed.

Because the record is shallow, the sheet names the missing items and returns the rep to the question bank in Step 4. It does not build a demo plan.

**Step 1.** Attendees:

| Name | Title | Buying Role |
|------|-------|-------------|
| `[Unknown]` | General Manager | Buyer persona. The role is `[Unknown]` until discovery names it |
| `[Unknown]` | Pre-Need Sales Manager | `[Unknown]`. The profile lists this persona as champion, which is a default for the persona, not a finding about this account |

**Step 3.** No pain is ranked. Hypotheses for the question bank only:

1. Pre-need leads from the intake form with no call-back owner. `[Inferred]` from the intake form `[Public: company website]`.
2. Plot records and the Stonemark map. `[Inferred]`.
3. The January 2027 renewal `[CRM]` is the timing fact, not a pain.

**Step 4.** Back to the question bank, Problem and Need-Payoff:

- "How do pre-need leads move from the intake form to a counselor today?"
- "How do you check, today, which plots are sold?"
- Need-Payoff: "Most operators take 24 hours or more to call back a pre-need lead. Is that your experience?" The 24-hour figure in (profile: Value Propositions) is a research target, not a customer result, so the question states it as the research's view. "If a pre-need lead waited a day, what would that cost the counselor's sale?"

**Missing Items, Named On The Sheet:**

- Two confirmed pains (0 of 2).
- One quantified impact (0 of 1).
- A named buyer (the GM's name is `[Unknown]`).

**The Choice Belongs To The AE:**

- **(a)** Run discovery prep for Friday's meeting. The sheet asks about the intake and the records process, and it names the January 2027 renewal as the timing fact.
- **(b)** Keep the demo, and open with five to ten minutes of the two questions above.

The AE chooses. The skill does not pick (b) by default, because a demo built on unconfirmed pains is a feature tour.

**Step 7.** Proof, one line per attendee. For the General Manager, none usable. The research target is 50 to 100 plots sold on paper and unsold on the map (Benchmark, deathcare research, paper-operations note, 2026-04-01). For the pre-need manager, the profile has no proof for this persona yet, so the sheet says so. The research target for pre-need follow-up, within an hour (profile: Value Propositions), stands in as the goal, labelled "target, no dated source".

**Step 10.** Hand-off:

```text
Hand-off (read by 07 and 13):
account: Greyfield Memorial Park (ACTIVE, Stage 2 Discovery, AE owner Owen Pruitt from 2026-11-03)
run_date: 2026-11-16
prep_sheet: not produced as a demo plan. Discovery-first recommendation with two options
top_pain: none confirmed (0 of 2 needed for a demo)
question_bank: Problem 2 questions and Need-Payoff 2 questions, from Step 4
attendees: General Manager, name [Unknown], buyer. Pre-Need Sales Manager, name [Unknown], buying role [Unknown]
proof_point: General Manager, none usable, research target 50 to 100 plots (Benchmark, 2026-04-01). Pre-need manager, none usable, target within an hour (target, no dated source)
next_action: Owen Pruitt, the AE owner on the record, confirms discovery or demo with the GM and asks for the pre-need manager's name, in one message (rank 2, a confirmation the meeting cannot run without). Owner: Owen Pruitt. Date: 2026-11-19, the working day before the Friday meeting on record (2026-11-20), a date the skill's own schedule sets for the confirmation, which is earlier than the five-business-day date of 2026-11-23
report_path: none (inline)
```

### Example 4: Quick Call Prep For A Champion (Quill Hollow Memorial Park)

**Context:** Ines Carmody, general manager of Quill Hollow Memorial Park, moved here six months ago from Lowmoor Memorial Gardens. She carries the champion label `[CRM]`. Her Champion Test reads Developing, one of seven behaviours met: she commits to next steps with dates, through the call she booked `[CRM]` (illustrative). The other six are not on record, so she is not Strong. Ines Carmody replied to Email 1 on 2026-10-27 and booked a call for 2026-11-02 `[CRM]` (illustrative). Under What The Close Reads her reply was due 2026-10-29, the next business day after the 2026-10-28 run in Account Snapshot (02) Example 5. The records do not say whether it went out, so this prep does not assume it did. Quill Hollow is an ENGAGED account, with no open deal: Ines Carmody has replied, and that reply is the basis for this call. It has a GREENLIGHT verdict (illustrative). It has one site, 8,800 plots and paper plat maps `[CRM]`. This prep is written on 2026-11-02, and the discovery call is in 15 minutes.

**Input:** "Quick call prep for Quill Hollow. Ines is on the call."

**Process.** `meeting_type = discovery`. Quick Call Prep applies (see Modes). The file option is skipped, and the short form is delivered inline.

**Step 3.** Pain hypotheses, ranked:

1. **Unsold Plots On Paper Plat Maps.** `[Inferred]`. The site holds 8,800 plots on paper plat maps `[CRM]`. The gap is reasoned, not measured. Top pain.
2. **A Records Finding In The Last State Review.** `[CRM]` for the fact, with its date `[Unknown]`. It ranks below the inferred pain because an undated finding cannot be the hook. It stays a discovery question only (illustrative).
3. **Pre-Need Leads.** `[Unknown]`. No pre-need activity is recorded.

**Step 8.** Opener: "Ines, thanks for making the time, and for writing back on October 27. Before we go further, how are the plot records kept at Quill Hollow today?" Do not reference the Lowmoor history unless she raises it. The open names her reply, because the account is ENGAGED.

**Step 4.** Top three discovery questions:

1. "When was the last state review, and what did it ask for?"
2. "When a family asks about a plot, how long does it take you to answer?"
3. "Who in the office would have to sign off on a tool under $25K?" The owner signs under $25K `[CRM]`.

**Step 9.** Game plan: find when the last state review was and what it asked for, then the plot lookup. If-then:

- If she raises the state review, ask when it was, what it asked for, and whether anything is still open.
- If she says the records are fine, ask for the last audit.
- If the owner joins, ask about the growth mandate `[CRM]`.

**Step 7.** Proof: none usable for the general manager. The research target is 50 to 100 plots sold on paper and unsold on the map (Benchmark, deathcare research, paper-operations note, 2026-04-01). Holloway Hills is Status Illustrative, so it is not cited. The sheet uses the audit question in place of a result.

**Output (short form, no file).** Steps 1 to 4 and Steps 8 and 9 are delivered in short form. No seven-section sheet is produced, because this is a quick prep.

```text
Hand-off (read by 07 and 13):
account: Quill Hollow Memorial Park (ENGAGED, reply 2026-10-27 [CRM], no open deal)
run_date: 2026-11-02
prep_sheet: inline, short form (quick call prep, no file)
top_pain: unsold plots on paper plat maps, [Inferred]. The records finding is a question, not the hook, because its date is [Unknown] (illustrative)
question_bank: Situation 1, Problem 1, Implication 1 (three questions, from Step 4)
attendees: Ines Carmody, General Manager, champion label, Champion Test Developing (1 of 7 met: commits to next steps with dates) [CRM]. The owner signs under $25K
proof_point: none usable. Research target 50 to 100 plots (Benchmark, 2026-04-01)
next_action: the rep on the call asks Ines Carmody, in one message, what the records problem costs and when the last state review was and what it asked for (rank 3: Identified Pain is red, and the state review question is the pain's test). Owner: the rep on the call, whom the records do not name. Date: 2026-11-02, the call booked on 2026-10-27 `[CRM]`, which is earlier than the five-business-day date of 2026-11-09
report_path: none (inline)
```

---

## Common Patterns

### Pattern: Quick Call Prep
**When:** The user says "quick prep" or "calling in 5 minutes."
**Approach:** Skip the file option (see the Output Contract). Deliver Steps 1 to 4, and Steps 8 and 9, in short form. Speed over completeness.

### Pattern: Discovery-To-Demo Handoff
**When:** The user ran discovery prep earlier and now requests demo prep for the same account.
**Approach:** Read the earlier `prep_sheet` and the findings from the CRM, which the discovery call populated. Rank the confirmed pains. Check the prerequisite. Flag any discovery gap in the demo opening, and send the rep back to the question bank for it.

### Pattern: Re-Engagement Discovery
**When:** The account has been quiet for three or more months and is re-engaging. An ENGAGED account that replied recently is handled by the ENGAGED rule in Step 8, not by this pattern.
**Approach:** Discovery mode, with emphasis on Step 2. Surface what was discussed before. Add a "what has changed since we last spoke" hypothesis. If Closed-Loss Reactivation (05) ran, use its `history_opener` only when its reopening event has fired. Otherwise it stays held.

### Pattern: Multi-Attendee Demo
**When:** Three or more attendees are confirmed, with different roles.
**Approach:** Map each attendee to a persona in the profile. Give each persona its own proof point with its Status. Allot question time for each attendee. Anticipate a different resistance type for each one.

---

## Troubleshooting

### "No CRM Data Is Available For This Account"
- **Likely Cause:** No record exists, or the record is empty.
- **Response:** Proceed with web research, tagged `[Public: source]`, and note "No existing CRM record" on the sheet. For discovery, build hypotheses from the profile's pains and tag them `[Inferred]`. For a demo, do not build a plan. Run the prerequisite fail path.

### "Discovery Was Shallow: Not Enough Confirmed Pains For A Demo"
- **Likely Cause:** Fewer than two pains are confirmed, or none is quantified.
- **Response:** Name the missing items on the sheet, one line each, with the count held against the count needed. Send the rep back to the question bank in Step 4. Offer the two options: discovery prep for the meeting, or five to ten minutes of discovery questions in the demo opening. Do not build a demo plan on the shallow record.

### "The Meeting Type Is Unclear"
- **Likely Cause:** The request could mean either type.
- **Response:** Ask: "Is this a discovery call or a demo?" If the answer is "a bit of both," use discovery, with a brief product overview section.

### "The Prospect Has Been Through Several Discovery Calls"
- **Likely Cause:** The conversation has covered the same ground more than once.
- **Response:** Focus on what is new. Pull the full history (Step 2) and identify the gap between what has been discussed and what the decision needs. The prep should advance the deal, not repeat earlier calls.

### "The Meeting Prep Section Of The Profile Is Missing"
- **Likely Cause:** The sales-layer section was never written.
- **Response:** Say so once at the start. Run uncustomized. Mark the vocabulary, the persona-proof map and the demo reframe as generic on the sheet, and suggest the CUSTOMIZE interview.

### "Every Proof Point For A Persona Is Illustrative"
- **Likely Cause:** The profile has no Verified or Benchmark row for that persona yet.
- **Response:** Say so on the sheet. Use the research target or a Benchmark with its source and date. Never use the Illustrative row with a prospect.

### "The Business Impact Cell Is Blank"
- **Likely Cause:** Neither the profile nor the call holds a figure.
- **Response:** Write `[Unknown]`. Make the question that finds it the sheet's next question to ask on the call.

---

## Best Practices

- **Customize The Scripts:** reference the specific pains, the contact names and the meeting context. A generic script gets a generic answer.
- **Match Proof To Attendees:** one proof point per persona, with its Status. A CFO does not need the story an operations manager needs.
- **Prepare Resistance Before It Happens:** type it as Reactance, Skepticism or Inertia, so the response fits the signal.
- **Keep The Talk-Time Band Visible:** the call flow shows the shared band for the call type, or the profile's override. Talk time is the coaching metric, so the number on the sheet should be the one the team coaches to.
- **Keep The Sheet To One Page:** the sheet is read in the two minutes before the call connects. Anything cut from it moves to the Deal Pulse (08) or Stakeholder Mapping (10) notes, not to a second page.

---

## Integration With Other Skills

**Reads from the skills before it, by field name.** A missing field is reported as missing, not rebuilt here.

- **Account Snapshot (02):** `account_status`, `verdict`, `contact_priority`, `pain_hypotheses`, `sequence`. The verdict reads GREENLIGHT, MANUAL REVIEW or DISQUALIFY.
- **Research Outbound (03):** `pov_brief`, `signal_map`, `wedge`, `persona_emails`.
- **Trigger Event Outbound (04):** `trigger_type`, `urgency_window`, `days_remaining`, `event_tag`, `sequence`.
- **Closed-Loss Reactivation (05):** `loss_classification`, `change_assessment`, `reactivation_strategy`, `history_opener`.
- **Daily Prospecting (07):** `dial_sheet`, `pre_call_briefs`, `exclusions`. A rep booked through the sheet has passed the BDR guard.
- **Deal Pulse (08):** `health_score`, `risk_level`, `pillar_scores`, `signal_scores`, `next_actions`.
- **Stakeholder Mapping (10):** `threading_score`, `buying_roles`, `ghost_nodes`, `champion_status`.
- **Competitive Strategy (11):** `incumbent_type`, `threat_level`, `gap_matrix`, `battlecard`, `win_plan`.
- **Competitive Displacement (12):** `incumbent_type`, `displacement_difficulty`, `target_personas`, `sequence`.
- **Call Coaching (13):** `call_score`, `category_scores`, `focus_area`, `coaching_points`, `key_moments`, `champion_status`.

**Hands to the skills after it, by field name.**

- **Daily Prospecting (07) And Call Coaching (13):** `prep_sheet`, `top_pain`, `question_bank`, `attendees` (with buying role), `proof_point`. Call Coaching grades the call against `question_bank` and `top_pain`.
- **Wrap-Up (O10):** `report_path` (set only when a file was written), `next_action` (owner and date).

**Related Skills To Run After The Call:** Call Coaching (13) to grade the call, and Deal Pulse (08) to update the deal health with what the call showed.

### Chains

- **Qualify To Book:** Account Qualification (01), Account Snapshot (02), Research Outbound (03) or Trigger Event Outbound (04), then Meeting Prep (06, this skill, last). This skill turns the booked first call into the prep sheet the rep reads during the call.
- **Daily Pipeline:** Daily Prospecting (07), then Meeting Prep (06, this skill). This skill builds the sheet for a call that the daily dial sheet booked.
- **Win Back:** Closed-Loss Reactivation (05), Trigger Event Outbound (04), then Meeting Prep (06, this skill). This skill uses the reactivation history opener only once its reopening event has fired.
- **Work The Deal:** Meeting Prep (06, this skill, first), Call Coaching (13), Deal Pulse (08), MEDDPICC Analysis (09), Stakeholder Mapping (10). This skill sets the question bank and the top pain that Call Coaching grades the call against.
- **Beat The Incumbent:** Competitive Strategy (11), Competitive Displacement (12), then Meeting Prep (06, this skill). This skill turns the incumbent's probes into questions for the call.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name. This skill is free and works without any kit. The kit reads these two fields as context for its proposal talk track:

- `account`
- `run_date`

This skill also reads the kit's hand-off block back as optional context: `case_status`, `hard_value`, `payback_months_hard`, `open_bets` and `next_action`. Anything taken from the kit that is marked ASSUMPTION is never presented on the sheet as a buyer fact.

---

## Changelog

### 2.1.14 (2026-10-27)
- The shared contract's Champion Tests section now defines "creates urgency" (a dated deadline the decision works to, with its date and source on record) and "defends the solution" (a recorded case of arguing for us in our absence to someone who decides), and says a test not yet run is never scored.

### 2.1.13 (2026-10-26)
- An upstream field is read as of its own run date, and a conflict with a rule here is named on the sheet with the rule governing. A renewal or deadline in an upstream pain list is urgency, never a ranked pain.
- The header reads the CRM status on the run date and states the date the deal opened when the CRM holds it. An upstream TARGET labelled then does not set the header.
- Example 1 and the try-it records state the deal's opening date, carry the upstream pain list without its pre-ranking, and list the renewal as urgency. The try-it drops the sentence that pointed to a later stage and the sentence that pre-scored the Stonemark evaluation.
- The question bank, the qualification scores, the proof lines and the next action are unchanged.

### 2.1.12 (2026-10-26)
- Identified Pain is scored on what the buyer has named in their own words. A pain the rep infers from the CRM or the profile is a hypothesis, and it scores red until the buyer names it. Example 1 moves to red, and its totals move to 0 green, 2 yellow and 6 red.
- The next action follows a written priority order in the Output Contract: a reply owed to a buyer, a confirmation the meeting cannot run without, the ask for the buyer's words on the top pain, the signer ask, then the follow-up draft. Asks to the same person in the same message travel together.
- The Input Contract has a rep row. Without it, the owner is the AE owner on the record, and the header says so.
- A profile label, such as a champion in the Example Cast or a signer in a role-title map, never sets a champion or Economic Buyer cell.
- A research target keeps the status its profile figure carries.
- Example 1's next action keeps its owner and date, and bundles the pain ask with the signer ask and the meeting date. Examples 2 to 4 are re-derived under the order, and their owners and dates are named from the records.

### 2.1.11 (2026-10-26)
- A record fact that shows the cost of a pain is evidence for that pain, not a second hypothesis. A renewal or deadline is an urgency. Ties on tag take the Core Pain Points order, so the double sale and the plot records give one top pain.
- The proof line is a usable Verified or Benchmark row from Proof Points, or "none usable" with a research target labelled by its source or "target, no dated source". An Illustrative row is never the proof line.
- Competition has its own cell rule: green on a stated preference, yellow on a known incumbent with no preference on record, red with no incumbent known.
- Example 1 scores Paper Process and Competition and totals the pre-fill. Examples 1 to 4 and the try-it show the new proof lines.
- The verdict, questions and next actions are unchanged.

### 2.1.10 (2026-10-26)
- Example 4 reads Ines Carmody as Developing, one of seven behaviours met, on the shared Champion Tests. Her booked, dated call is the one behaviour met, and the Context and the hand-off say so, matching Account Snapshot (02) Example 5.
- Example 4 names the reply due date under the shared rule, 2026-10-29, and says the records do not show whether it went out.
- No verdict, question, next action or try-it promise changes.

### 2.1.8 (2026-10-26)
- Profile facts are cited as (profile: Section), with the profile's own section name, in place of the older profile forms.
- ENGAGED is a rule in the first-meeting open (Step 8): an account that replied or met with us, with no open deal, is opened on that reply and not restarted as a cold meeting. The Quality Bar checks it.
- Example 4 (Quill Hollow) is relabelled ENGAGED after Ines Carmody's reply of 2026-10-27. Its open names the reply, and its hand-off status matches. Its verdict and call prep otherwise stand.
- Example 2 (Sable Fork) states that a booked discovery call does not make an INBOUND account ENGAGED.
- No verdict, question or next action changes.

### 2.1.7 (2026-10-26)
- Need-Payoff writes two questions in every discovery prep, and the sheet shows the top three questions of the other phases. The earlier range of two or three left the count open.
- A question is ranked by the hypothesis it tests, strongest first, so the top three are fixed.
- Elements without a cell rule take the grid default. Champion maps Strong to green, Developing to yellow and None to red.
- A research target whose figure has no dated source is labelled as a target, not as a benchmark.
- The next action asks for the signer above the buyer as the record names that role, and it does not name a role the record does not hold.
- The rule sentences no longer quote a worked record. The Example pointers are reworded, and the Examples follow the Need-Payoff count.

### 2.1.6 (2026-10-26)
- The upstream Account Snapshot fields in the first example quote that skill's pain hypotheses and its three-email sequence, so the two files read the same values.
- The Sable Fork example records the discovery call that the BDR booked on the afternoon of the run date. Its prep is written after that booking, and its next action names the booking as the source of the call date.
- The Quill Hollow example moves to the run date of its booked call. Its undated records finding no longer serves as the hook: it ranks below the inferred pain and stays a discovery question. Its champion is a label until the Champion Test runs.
- The Greyfield example moves to a run date after the account's first contact and its discovery call. Its demo and confirmation dates are recomputed under the shared rule.
- The first example keeps its notes tags for the Stonemark evaluation and Walt's tablet skepticism. Its run date, 2026-05-11, comes before the later calls that also record those facts.
- Frontmatter: the 2.1.5 change summary carried a stray quotation mark that broke the YAML. It is removed.

### 2.1.5 (2026-10-26)
- Meeting-driven next action dates name whether the records or the skill's own schedule set them.
- Every attendee has one proof line, including an attendee whose persona is unknown. The Greyfield and Sable Fork examples show a line for each attendee.
- An undated call fact takes the shared Call tag with its date unknown, in place of the notes tag.
- The next action follows the family's one deadline rule. Where the next action happens on a dated call, that call date is used and named as the source, and each example names its source.

### 2.1.4 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. Step 3 gives the tag order for ranking pain hypotheses. Step 4 writes each phase's range from the profile first, then the record. Step 7 defines the research target as the profile figure that matches the persona's hook focus. Step 8 reads a meeting with no earlier logged meeting as a first meeting. Step 10 names the signer above the buyer as the next action when the economic buyer cell is yellow. A call of unknown date is tagged as notes. The Example 1 records gain the meeting history line, and the Stonemark tag becomes notes. No output changed.

### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1. The example reads the upstream contact, pain and sequence fields and names a proof point with its research target for each attendee. Its question bank shows the counts the try-it promises. A phase with fewer than three questions shows all of them, and an incident count does not quantify a pain. The try-it ask names the example profile. No output count, verdict or next action changed. The proof line now names both attendees.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1. Adds the colour rules for Metrics, Economic Buyer and Identified Pain to the qualification pre-fill, and states that an Illustrative proof row does not make a persona usable. Example 1 gains the call date and the Ruth Ellery research target, and its next action is dated to the call. The meeting date stays unknown until agreed.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1. No other change.

### 2.1.0 (2026-10-25)
- Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection and a Guild Pro Kits subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### 2.0.0 (2026-10-20)
- Sales 2.0 shared contract added under Context. The evidence tags, status words, verdict words, stage handling, champion tests, incumbent types and talk-time bands come from it, and the skill refers to them rather than restating them.
- Format brought to the house standard: Why This Skill Exists, Hard Rules with reasons, Quality Bar, Modes and Epistemic Rules added. the separate artifact section folded into the file option in the Output Contract.
- Output Contract names the hand-off fields `prep_sheet`, `top_pain`, `question_bank`, `attendees` and `proof_point`. Integration names the upstream fields by name.
- Prep method added in general form: a question bank per discovery phase with listen-for phrases, objection scripts, a minute-by-minute call flow, a follow-up email draft, the three-beat demo arc, and one proof point per attendee persona.
- Team names and talk-time overrides read from Sales Methodology. The restated talk-time figures are removed in favor of the shared bands.
- Follow-up ladder rule: stages 1 and 2 on every confirmed pain, and stage 3 on the top pain.
- Evidence labels replaced by the six shared tags. MANUAL REVIEW spelled in full. Illustrative proof points are never cited to a prospect.
- Examples: a Brackhaven discovery example added. The Sable Fork example is retitled MANUAL REVIEW, and its demo stays held until the pain is confirmed. The Greyfield example now shows shallow discovery. The Quill Hollow example is kept as the short form.
- Internal framework names replaced with plain descriptions (Demo Framework, Question the Problem, Meeting Structure, Demo Story Arc, the Winning and Losing Zone scripts, the probe set and the five-habit check).

### 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Priority Ladder rule made consistent: run through at least Stages 1 and 2 before moving on.

### 1.2.1 (2026-10-13)
- Two framework names replaced with plain descriptions. The methods are unchanged.
- The demo checklist and the meeting open and close rewritten as generic habits.

### 1.2.0 (2026-09-29)
- Worked examples rewritten around a retired example company. Em dashes removed from prose.

### 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology and Context. Company-specific data moved to the shared profile, so one profile powers every skill.

### 1.0.0 (2026-03-04)
- Initial release, merged from the discovery and demo prep skills and unified by `meeting_type`.
