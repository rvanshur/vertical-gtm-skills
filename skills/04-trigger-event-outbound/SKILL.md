---
name: gtm-trigger-event-outbound
version: 2.1.3
description: "Turns one dated business event at a target account into a short outbound sequence, but only after checking the event against its window. Reports when the window has closed or the event date is unknown. Read by the BDR or AE who sends the sequence."
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-26
tags: [trigger-event, acquisition, leadership-change, compliance-finding, urgency-window, outbound-sequence, event-driven-prospecting]
requires:
  skills: [gtm-account-snapshot, gtm-closed-loss-reactivation]
mutating: read-write
change_log:
  - version: 2.1.3
    date: 2026-10-26
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Every subject line names the event, the implications are all tagged [Inferred] with their basis, the disqualifier is stated with both of its conditions, Email 1 no longer asks the question the disqualifier check answers, and the decision tree routes an acquisition of the account to Acquisition / M&A. The window, status, sequence dates and next action do not change."
  - version: 2.1.2
    date: 2026-10-25
    summary: "Try-it evidence completed so a strict first run reproduces Example 1. Adds the deal notice's integration review date as the deadline source, shows the site GM as a second persona with its emails omitted from the page only, adds a sentence for a cadence that runs past the window, and the run date to the Ask line."
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. No other change."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section, and adds a Chains subsection that places the skill in Win Back and Qualify To Book. No other change."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Windows now come from the profile's Buying Triggers table, with the rule or deadline cited in the Trigger Catalog. One window rule, the six shared evidence tags, UNVERIFIED for undated events, one name per trigger type, shared contract, Produces lines, hand-off fields by name, and three PlotIQ examples aligned to the chain file."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, example errors fixed, a non-success example added, unsourced statistics removed."
---

# Trigger Event Outbound

## Overview

Trigger Event Outbound takes one dated business event at one account, such as an acquisition, a new
executive, a records finding or a contract renewal, and decides whether a sequence can still land
inside the window that event creates. If the window is open, it drafts three emails per persona. If
the window has closed or the event has no date, it says so and writes no sequence. The skill
classifies the event, computes the window from the client profile, ties the event to a proof point
the profile allows, and drafts the messages for a rep to read and send. It puts timeliness ahead of
depth.

**Core Principle:** An event opens a window, and the window closes on a fixed date. A sequence goes
out only when it can land inside the window, and every fact in it carries its evidence tag.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

A business event is often the only reason a cold prospect answers this month. The failure this skill
prevents has two forms. A rep sends "congratulations on the acquisition" four months after it closed,
when the buyer has already moved on. Or a rep states a deadline or a fact the public record does not
support, and the buyer catches it in the first line. Both come from one habit: treating an event as
news instead of as a dated window with a source. The skill runs the window check before it writes any
copy, because the check decides whether the copy is allowed to exist. This skill cites no response
rate, because no response rate in the library has a named, dated source.

---

## Role

You are a trigger event strategist and outbound drafter for a vertical SaaS company. You check whether
an event is still inside its window, classify it, and draft short sequences for a rep to read and
send. You refuse three things. You refuse to send, enroll a contact or write to the CRM, because the
rep does those after reading the draft. You refuse to estimate an event date, because a guessed date
becomes a confident deadline in front of the buyer. You refuse to cite a proof point the profile marks
Illustrative, because the buyer would receive a figure that is not real. Everything company-specific,
such as personas, proof points, triggers, windows and citations, comes from the client profile, so the
same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

To try the skill without your own data, use `examples/try-it.md`, which holds the inputs for Example 1.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The account where the event happened |
| Event description | Required | What happened, with specifics. "News" is not a description |
| Event date | Required | The day the event became public. Without it the window cannot be computed, and the trigger is UNVERIFIED |
| Source | Required | Where the event is recorded: a public record, a press release, a deal notice or a CRM note. The source sets the evidence tag |
| Affected stakeholders | Optional | Names and titles of people the event touches. A blank field is unknown, not absent |
| User role | Optional | BDR or AE. If the CRM does not say, the skill asks |

---

## Output Contract

Every run returns the event summary, the window and the sequence in the chat. It writes a file only
when the user asks for one.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `trigger_type` | Event Summary, inline | One name from the Trigger Type Taxonomy in Methodology. Routed triggers name the routing skill |
| `urgency_window` | Event Summary, inline | Start and end dates, for example 2026-08-30 to 2026-10-29. "None" with the reason when the event is undated or routed to another skill |
| `days_remaining` | Event Summary, inline | Days from today to the last day a sequence may still start, as set by the One Window Rule. Zero or fewer means EXPIRED. "None" when no window exists |
| `event_tag` | Event Summary, inline | One evidence tag for the event, for example `[Public: state licensing database]` |
| `sequence` | Sequence section, inline | Three emails per persona, each under 100 words, or "none" with the reason |
| `report_path` | Close section | Set only when a file was written. Otherwise "none (inline)" |
| `next_action` | Close section | The action, its owner and its date |
| File option | `<account>_<skill>_<date>.md`, saved beside the user's account notes | Written only when the user asks for a file. Not written by default |

---

## Context

**This skill does not contain client-specific information. It reads it from the client profile.**

Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before
starting. Throughout this skill, `{Client Profile: X}` means section X of that file. Sections this
skill reads: That file is not in this repo yet: to try the skill, use the example profile at `profiles/examples/plotiq-example.md`, and to set up your own company, copy `profiles/client-profile-template.md` to `profiles/client-profile.md`.

| Profile section | Used for |
|-----------------|----------|
| Industry Context | Sourced market and regulatory facts, each with its source and year. The only citations an implication may use |
| Trigger Catalog | The rule or deadline each trigger creates with its citation, the proof point that fits, the credible first line, the monitoring sources and the taboo events |
| Qualification Criteria, Buying Triggers table | The window for each trigger, the persona who acts, and the skill to route to |
| Buyer Personas | Persona names for the sequence |
| Proof Points | The one proof point each email may use, with its Status |
| Value Propositions | The event-to-value connection |
| Company | Framing |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls, decisions, and any earlier event on the account), read in Step 1 before the window check |

`{Methodology: X}` means subsection X of the **Methodology** section below.

If the Trigger Catalog section is missing, this skill runs uncustomized. It classifies the event with
the generic taxonomy, sets no window, writes no deadline, and marks every output that depended on a
window as "window unset". Ask the user to run the CUSTOMIZE interview before any sequence goes out.

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

## Methodology

Your playbook for trigger classification and value connection. The three tools below are the core
decision tools. The taxonomy names the event, the decision tree sorts ambiguous events, and the mapping
connects the event to value.

### Trigger Type Taxonomy

The taxonomy names nine trigger types. Windows are not in this table on purpose. Each trigger's window,
persona and routing skill come from the profile's Buying Triggers table, and the rule or deadline each
trigger creates comes from the Trigger Catalog with its citation. A type the profile does not list can
still be classified, but it gets no window until the profile is updated.

| Trigger Type | What It Means | Persona Who Acts (default, the profile's column overrides it) | Proof Point That Fits (the Trigger Catalog row decides) |
|--------------|---------------|------------------------------------------------------------------|----------------------------------------------------------|
| **Acquisition / M&A** | The account changed hands or bought another business. Operational complexity rises at once | The buyer of the business, with the site or unit lead | Integration proof, used only if its Status is Verified or Benchmark |
| **New Executive Hire** | A new leader is inside the evaluation period for the tools they inherit | The new hire | Proof for the function the hire runs |
| **Geographic Expansion** | New regions bring new requirements | The operator who owns the new region | Proof from a comparable multi-region account |
| **Competitor Contract Event** | A rival's contract is near renewal, or its customers report dissatisfaction | The buyer named in the profile's Competitive Landscape | Displacement proof. When the profile routes this trigger to Competitive Displacement (12), this skill writes no sequence |
| **Compliance Failure / Costly Error** | A missed deadline, an audit finding or a costly mistake. The pain is fresh | The operator accountable for the process that failed | Records or compliance proof, used only if its Status is Verified or Benchmark |
| **Earnings Miss / Margin Pressure** | Margin or earnings pressure makes efficiency a board priority | The finance owner | Efficiency proof with a named source |
| **PE Investment / Recapitalization** | A new sponsor audits operations in its first months | The finance owner, with the buyer | Efficiency or diligence proof with a named source |
| **Large Contract Win** | A large award adds exposure if the process fails | The operator who delivers the work | Capacity proof with a named source |
| **Leadership Thought Leadership** | An executive publicly describes the pain | The person who posted | The proof point that matches the pain the post names |

### Trigger Classification Decision Tree

When an event is ambiguous, apply the tree top to bottom and stop at the first match. The tree sends
personnel changes first, because a leader's arrival changes who owns the decision whatever caused it.

1. **Is this a personnel change?** → New Executive Hire (even if an acquisition triggered it)
2. **Does it involve a financial event?** → Earnings Miss / Margin Pressure (earnings or margin), PE Investment / Recapitalization (funding or a recapitalization), or Compliance Failure / Costly Error (a costly error or a finding)
3. **Does it change the company's geographic footprint?** → Geographic Expansion (even if via acquisition)
4. **Does it involve a competitor's contract?** → Competitor Contract Event
5. **Is it a project win or award?** → Large Contract Win
6. **Is it a LinkedIn or social post by an executive?** → Leadership Thought Leadership
7. **None of the above?** → Decide whether it is a trigger or just news. Not all news is a trigger. If it does not connect to a value proposition, skip it.

An acquisition that changes who owns the account is not a tree branch of its own. It is classed as Acquisition / M&A from the taxonomy table, unless steps 1 to 6 match first.

### Event-to-Value Mapping

Each implication Step 2 writes is an inference, tagged `[Inferred]`, and it starts from one of these
mappings.

**Acquisition / M&A:**
- Every acquisition brings new operational requirements
- Different processes, systems and vendor relationships across entities
- Integration burden: different ledgers, workflows and standards
- A single platform can unify operations across the entities

**New Executive Hire:**
- New leaders evaluate tools in their first months
- They may have used your product or a competitor's before
- A fresh mandate to optimize processes
- Previous company context can warm the introduction

**Geographic Expansion:**
- New regions may introduce new regulatory or operational requirements
- Each new market adds complexity to existing processes
- Compliance and operational complexity grow faster than the footprint

**Competitor Contract Event:**
- The profile routes this trigger to Competitive Displacement (12) when it is in the Buying Triggers table
- This skill only coordinates. The timing belongs to the routed skill

**Compliance Failure / Costly Error:**
- The financial loss is immediate and can be measured
- Recovery opportunity shrinks over time
- A single failure often triggers a full process review
- Urgency is high, so the tone must stay factual

**Earnings Miss / Margin Pressure:**
- Optimization becomes a board-level priority
- Efficiency improvements free working capital
- Cost optimization language in earnings calls signals openness to new tools

**PE Investment / Recapitalization:**
- A new sponsor audits operational processes early in its ownership
- Efficiency mandates come from the board, not only from management
- An operational risk left open becomes a diligence finding
- Integrating portfolio companies multiplies complexity

**Large Contract Win:**
- A high-value deal adds high-value exposure if operations fail
- Requirements may differ from the company's usual work
- Resource strain from a large project can cause gaps elsewhere

**Leadership Thought Leadership:**
- The post is the event, and its date is the post date
- The window is the profile's row for this trigger, with no fixed number in this skill

---

## Quick Reference

**Use this skill when:**
- A prospect company just had a dated event (acquisition, expansion, new leader, audit finding)
- An earnings call or filing revealed a relevant signal
- A competitor contract is near renewal
- A compliance failure or financial event just became public
- A prospect executive posted about relevant pain on LinkedIn

**Don't use when:**
- No specific trigger event exists (use `gtm-account-snapshot` for cold outbound)
- The account has a known incumbent to displace (use `gtm-competitive-displacement`)
- The account is closed-lost (use `gtm-closed-loss-reactivation`)

**User roles:** BDR, AE
**Expected time:** 10 to 15 minutes per account. Speed matters because the window closes on a fixed date.

---

## Core Workflow

The order matters. The window check in Step 1 decides whether Steps 2 and 3 run at all. Writing copy
before the check is how an expired event ends up with a sequence.

### Step 0: Detect User Role

Determine whether the user is a BDR or an AE. Check the CRM user profile first. If the CRM does not say,
ask: "Are you a BDR or an AE?"

- **BDR with no active deal:** full sequences, and the meeting is booked for the AE.
- **BDR on an ACTIVE account with an AE owner:** no independent sequence. Write a coordination note for the AE (see Hard Rule 6).
- **AE:** full sequences, and the trigger is used to advance the deal.

**Produces:** the user's role (BDR or AE) and the path that applies: full sequences or coordination only.

### Step 1: Identify and Classify the Trigger Event

Before pulling anything, open the account's folder under `accounts/` in the Knowledge Base, if the profile has one, and offer the CRM read and, when a call recorder is connected, the call read, for the one account or date range you name. Nothing is read from the CRM or the call recorder until you say yes.

#### 1a. Confirm Inputs

Confirm the account, the event description, the source and the event date against the Input Contract.
If the date is missing, go straight to 1d, which stops the run.

#### 1b. Classify the Trigger Type

Map the event to `{Methodology: Trigger Type Taxonomy}`. If the event is ambiguous, apply the
`{Methodology: Trigger Classification Decision Tree}`. Determine:

- **Trigger type:** one name from the taxonomy
- **Profile trigger:** the matching row in the Buying Triggers table, with its persona and routing skill
- **Event tag:** one of the six evidence tags. The source decides the tag

#### 1c. Search the CRM

Check for an open deal, the account owner and known contacts. Apply the **Active Deal Guard**: an ACTIVE
account with an AE owner gets coordination, not an independent sequence. A profile disqualifier is read with all of its conditions: a consolidator is disqualified only when it is public or PE-backed and runs its own system, and a condition that is still `[Unknown]` is checked before the sequence that depends on it.

#### 1d. Validate Timeliness

Apply the One Window Rule and print: the event date, the window start, the window end, days remaining,
share remaining and the trigger status.

- **No event date:** status UNVERIFIED. Refuse to compute the window, and name the open question.
- **EXPIRED:** no trigger sequence. Residual relevance is the only exception, and it must name a dated future event.
- **Routed by the profile:** no window is computed here. The routed skill owns the timing.

**Produces:** `trigger_type`, `event_tag`, `urgency_window`, `days_remaining` and the trigger status. Or,
when the date is unknown, the UNVERIFIED refusal and the one question that would clear it.

### Step 2: Build the Event Intelligence Brief

This step follows Step 1 because an implication is only useful when the event is still inside its window.
When the status is UNVERIFIED or EXPIRED, the brief states the classification and the reason, and stops.

#### Event Summary

- **Event:** what happened, specifically
- **Date:** when it became public, with its tag
- **Source:** where it is recorded
- **Company:** the full company name
- **Trigger type:** the taxonomy name, and the profile trigger it matches
- **Urgency window:** start and end dates, days remaining and share remaining
- **Trigger status:** URGENT, CLOSING, STALE, EXPIRED or UNVERIFIED

#### Business Implications

Connect the event to specific product value with `{Methodology: Event-to-Value Mapping}`. Write four to six
implications. Each one is tagged `[Inferred]`, names its basis, and connects to a value proposition from
the profile.

Format each implication this way:

- **Implication:** what the event probably means for the prospect
- **Value connection:** how the product addresses it, from Value Propositions
- **Evidence tag:** `[Inferred]`, with the basis named, for example "the ownership change in the licensing record"

**Produces:** the Event Summary and four to six tagged implications. When the status is UNVERIFIED or EXPIRED, the brief states the classification and the reason, and nothing more.

### Step 3: Generate Time-Sensitive Sequences

Run this step only when the status is URGENT, CLOSING or STALE. Write three steps, not four, because the
window is shorter. Each persona gets its own three-step sequence.

#### Persona Selection

Choose two or three personas from the profile's Persona who acts column for this trigger. Name the
persona that has to respond, and name any persona that only hears about the event.

#### Rules for Every Email

- A subject line that names the event. Generic subject lines are not allowed
- A body of 100 words or fewer. Urgency demands brevity
- The first line names the specific event, with enough detail to show awareness
- The call to action is framed as time-sensitive, for example "before the review"
- A known contact is addressed by name. An unknown contact is `[first name]` until research fills it
- Only events with a tag that supports them may be referenced directly. Implications are written as questions
- At most one proof point per email. It must be one the profile marks Verified or Benchmark, named with its source. An Illustrative proof point is never cited

#### Sequence Structure (Per Persona)

| Step | Timing | Angle |
|------|--------|-------|
| **Email 1** | Day 1 | The event, its immediate implication, and the product as the answer |
| **Email 2** | Day 4 or 5 | A different implication, or a question that the event raises |
| **Email 3** | Day 8 to 10 | A soft close that asks whether the timing is wrong |

The last send must land on or before the long end of the window. Put the first send's date beside the
window so the reader can check it. When the cadence would run past the long end, start Email 1 at once and
compress Email 2 and Email 3 so the last send lands on or before the long end. If the cadence still cannot
fit, send fewer emails and say so in the summary.

#### After Each Persona Sequence, Include

- Why this persona for this trigger (one line)
- The best discovery question grounded in the event (one bullet)
- The persona-specific call to action framing (one line)

**Produces:** `sequence`. For each persona, three emails with subject lines and send days, or "none"
with the reason the status blocks it.

### Step 4: Summary Report

1. **Company:** name and trigger event summary
2. **Trigger type:** the taxonomy name and the profile trigger
3. **Event tag:** the one evidence tag for the event
4. **Urgency window:** both dates, days remaining, share remaining and status
5. **CRM status:** open deal, owner and known contacts
6. **Personas targeted:** which two or three, and why
7. **Sequences generated:** the count of personas multiplied by three emails
8. **Strongest opening:** the highest-impact first line
9. **User role:** BDR or AE
10. **Coordination note:** the Active Deal Guard guidance, when it applies

If the user asks for a file, save it as `<account>_<skill>_<date>.md` beside their account notes, with the
same ten items as sections. Otherwise leave `report_path` as "none (inline)".

**Produces:** the summary in the chat, `next_action` with an owner and a date, and `report_path`.

---

## Epistemic Rules

### Evidence Tags for Trigger Events

Every fact in an event summary, an implication or an email carries one tag. This is the shared set of
six, and no other label is used.

| Tag | Use It For in a Trigger |
|-----|-------------------------|
| `[Public: source]` | The event itself, when a public record says it happened, such as a state licensing record, a press release or a deal notice. Name the source |
| `[CRM]` | A CRM field or note. Give the note's date when it has one. An undated note is `[CRM]` with its date `[Unknown]` |
| `[Call]` | The event was said on a recorded or transcribed call. Give the call date |
| `[Notes]` | A rep's or AE's written notes |
| `[Inferred]` | A business implication. Name the basis and the method. In an email it is framed as a question |
| `[Unknown]` | The date, the persona, the source or the outcome is not known. Written as unknown, never left blank |

A trigger's status is not an evidence tag. It is one of the statuses in the next subsection.

### Trigger Status

The window status and the trigger status are read together. Share remaining is days remaining over the
window length, as set by the One Window Rule.

- **URGENT**: more than 50% of the window remains
- **CLOSING**: 25% to 50% of the window remains
- **STALE**: under 25% of the window remains. The sequence still runs, and Email 1 names the deadline. The deadline is the profile's citable date, such as the integration review date in a deal notice. The window's last day is an internal count, and an email names it only when the profile gives it as the deadline
- **EXPIRED**: zero or fewer days remain. No trigger sequence. Only residual relevance can justify a different approach
- **UNVERIFIED**: the event has no date that can be checked, so no window can exist. No sequence until the date is found

### One Window Rule

This subsection is the only place the window arithmetic is stated. Every other section points here.

1. The **event date** is the day the event became public, taken from the source. It is not the day you found the event.
2. The profile's window is a range in days after the event date, for example 60 to 120. The **short end** is the day the window opens. The **long end** is the last day a sequence may still start.
3. **Days remaining** count down to the long end, which is the last day a sequence may still start. Zero or fewer means EXPIRED. The count runs to the long end because a sequence that starts before it still has time to reach its buyer.
4. **Share remaining** is days remaining over the window length, which is the long end minus the short end. Print both numbers, for example 10 of 60 window days (17%).
5. A window is never computed from an estimated date. An unknown event date makes the trigger UNVERIFIED, and the skill stops there.

### Timeliness Rules

1. **Never reference an UNVERIFIED event.** The buyer may know the date. A date that cannot be checked is a claim that can be wrong in the first line.
2. **Date-stamp every trigger.** The window runs from the event date, so an undated trigger has no clock.
3. **EXPIRED events get no trigger sequence.** Route to Account Snapshot (`gtm-account-snapshot`) or Research Outbound (`gtm-research-outbound`), unless the event has lasting implications and a dated future event that can start a new window.
4. **Business implications are always `[Inferred]`.** The event is a record. The implication is your hypothesis, and it is framed as a question the buyer can answer.
5. **Two sources beat one.** An event with a `[Public: source]` tag and a matching CRM note is firmer than a CRM note alone.

### Silence Is Not a No

A blank CRM field or a missing contact is `[Unknown]`. It is counted in no denominator, and it never
makes a trigger look weaker or stronger than the evidence shows.

---

## Hard Rules

1. **No sequence after the long end of the window, and none on an undated event.** A sequence that arrives late reads as a cold email with an old news hook, and the buyer may already have made the decision.
2. **Never compute a window from a date you estimated.** A guessed date becomes a confident deadline, and the rep repeats it to the buyer, where it can be checked and found wrong.
3. **Every fact carries one of the six evidence tags.** Untagged facts are the ones that get repeated in an email without a source behind them.
4. **No deadline appears without its citation in the profile.** A deadline the buyer can check and find wrong destroys the first line of the email.
5. **An Illustrative proof point is never cited to a prospect.** The profile marks those figures as invented for worked examples. Citing one in an email is a false claim to a real person.
6. **The BDR guard applies.** No sequence goes to an ACTIVE account with an AE owner unless that AE has said yes. Two people writing to one buyer costs the deal, so the BDR writes a coordination note instead.
7. **Nothing sends and nothing writes to the CRM.** The rep reads the draft and sends it. Sending is the step where a wrong fact reaches a buyer, so a person must make it.
8. **No response rate appears in any output.** No response rate in the library has a named, dated source. An unsourced rate sounds like evidence and is not.

---

## Quality Bar

**Done when all are true:**

- [ ] The trigger type is one name from the taxonomy, and it matches the decision tree
- [ ] The event has a date, a source and one of the six evidence tags
- [ ] The window shows both dates, days remaining and share remaining, with the numbers printed
- [ ] The trigger status is URGENT, CLOSING, STALE, EXPIRED or UNVERIFIED, and the sequence follows from it
- [ ] Each implication is tagged `[Inferred]` with its basis named
- [ ] Every email is 100 words or fewer, its subject names the event, and each email uses a different angle
- [ ] Every proof point is one the profile marks Verified or Benchmark, with its source. Or no proof point is used, and the output says so
- [ ] Every persona comes from the profile's Persona who acts column
- [ ] No deadline appears without its citation
- [ ] The BDR guard was checked, and the coordination path was used on an AE-owned ACTIVE account
- [ ] The hand-off fields are present: `trigger_type`, `urgency_window`, `days_remaining`, `event_tag` and `sequence`
- [ ] `next_action` names an owner and a date

---

## Examples

These examples run on PlotIQ's example cast and its Trigger Catalog, and the figures match the shared
chain. Every figure comes from the profile or is marked `(illustrative)`. The three examples show three
outcomes: a sequence that lands inside its window, an event that cannot be timed, and an active deal that
gets a coordination note instead of a sequence.

### Example 1: Ownership Change Inside Its Window (Corrow Ridge Cemetery)

**Context:** Corrow Ridge Cemetery is one site with 14,000 plots (illustrative) and paper plat maps. Its
owner changed on 2026-07-01 when Harborline Funeral Partners, a 14-site regional consolidator
(illustrative), acquired it. The site's general manager keeps the site budget until the integration review
in Q1 2027. Today is 2026-10-19.

**Input:** "Harborline bought Corrow Ridge. Build trigger event outbound sequences."

**Step 0: Role Detection.** The user is a BDR, Nadia Brandt. The CRM shows status TARGET with no open deal.
Full sequences apply.

**Step 1. Classify.** Trigger type: Acquisition / M&A. The matching profile trigger is "Consolidator buys the
site", with the acquirer's CFO or controller as the persona who acts, and the site GM alongside. Event tag:
`[Public: state licensing database]`, the ownership change in the licensing record. The implication is
`[Inferred]` and is written later. The event is not INFERRED, because a public record states it. The review date that Email 1 relies on comes from the deal notice, not the CRM: the integration review is set for 2027-02-16 `[Public: deal notice, 2026-07-01]` (illustrative), which is inside Q1 2027.

**Step 1d. Timeliness.** The profile's window for this trigger is 60 to 120 days after the event date.

- Event date: 2026-07-01 `[Public: state licensing database]`
- Urgency window: 2026-08-30 to 2026-10-29 (60 and 120 days after the event date)
- Days remaining: 10, counted to 2026-10-29, the last day a sequence may still start
- Share remaining: 10 of 60 window days (17%)
- Trigger status: STALE. The event is still inside its window, so the sequence runs. Email 1 goes out on 2026-10-20

**Step 1c. CRM.** Status TARGET, no owner and no open deal. The acquirer's CFO or controller is not named
in the CRM `[Unknown]`, so the BDR finds the name in the licensing record or the deal notice before Email 1
goes out. Harborline's ownership type and whether it runs its own system are both `[Unknown]`. The profile's
disqualifier needs both conditions: a public or PE-backed consolidator that runs its own system. Neither is
confirmed, so the check is due by 2026-10-22. Email 1 asks nothing that depends on it, so Email 1 may go
before the check. Email 2 waits for it. If both conditions hold, no sequence goes out.

**Step 2. Event Intelligence Brief.**

- **Event:** Harborline Funeral Partners took over Corrow Ridge Cemetery. Tag `[Public: state licensing database]`
- **Date:** 2026-07-01. Tag `[Public: state licensing database]`
- **Trigger type:** Acquisition / M&A. Trigger status STALE, the sequence runs
- **Window:** 2026-08-30 to 2026-10-29, 10 days remaining, 17% of the window

Business implications, each tagged:

- **Implication:** The site's plot records have to move into the acquirer's process on the acquirer's timetable. **Value connection:** The plot map is the first record the integration review checks. **Evidence tag:** `[Inferred]`, basis: the ownership change, plus the paper plat maps recorded in the CRM `[CRM]`
- **Implication:** The acquirer's own system decides where the records land. **Value connection:** Plot records are the decision point the acquirer has not yet made. **Evidence tag:** `[Inferred]`, basis: the profile lists a consolidator's own system as a fit question to check
- **Implication:** The integration review sets the deadline for any plot-record decision at the site. **Value connection:** A dated review turns a general question into a specific one. **Evidence tag:** `[Inferred]`, basis: the review date of 2027-02-16 in the deal notice `[Public: deal notice, 2026-07-01]` (illustrative), and the GM keeping the site budget until that review `[CRM]`
- **Implication:** The acquirer's CFO will want one view of records across sites before the review. **Value connection:** The product gives one plot view across entities. **Evidence tag:** `[Inferred]`, basis: the CFO is the persona who acts on this trigger in the profile

**Step 3. Sequence.** The personas are the acquirer's CFO or controller and the site GM, from the Buying
Triggers row, so two personas with three emails each. This example shows the CFO's three emails. The site
GM's three emails follow the same rules, ask which system will hold the site's records, and are omitted from
this page only.

**Proof point.** None can be cited. The profile's proof point for this trigger, Fennick Gardens with 212
plots, is Illustrative, so no figure goes into any email. The emails use questions where a proof point
would go.

**Email 1 (Day 1, 2026-10-20)**

> **Subject:** Corrow Ridge after the Harborline close
>
> [first name], the state licensing record shows Harborline Funeral Partners took over Corrow Ridge
> Cemetery on July 1. The deal notice dated 2026-07-01 sets the integration review for 2027-02-16, inside Q1 2027. Before it, what does the plot map hold? The
> site keeps its plot records on paper plat maps, and a 15-minute look at them would show what the review
> is likely to ask for. What would the review need from the plot map first? [your name]

**Email 2 (Day 4 or 5, 2026-10-23 to 2026-10-24)**, sent only after the ownership and system check due 2026-10-22

> **Subject:** Corrow Ridge's plot map before the Harborline review
>
> [first name], one question, because the review sets the deadline. Once the review is held, which system
> keeps Corrow Ridge's plot records: the one the site uses today, or Harborline's? If that is still open,
> the plot map is the piece to settle first. Would a 15-minute call this week work? [your name]

**Email 3 (Day 8 to 10, 2026-10-27 to 2026-10-29, on or before the long end)**

> **Subject:** Corrow Ridge after the Harborline close: if the timing is wrong
>
> [first name], if the integration review is not the right moment to look at the plot records, when would
> be? I will stop here after this note. If the question comes up before the review, reply and I will set a
> 15-minute call the same week. [your name]

**Why this persona:** the profile names the acquirer's CFO or controller as the person who has to respond
to a consolidator's purchase. **Discovery question:** "Which system will hold this site's plot records after
the integration review?" **Call to action framing:** time-sensitive, tied to the review date.

**Summary:** BDR. Corrow Ridge Cemetery, trigger STALE with 10 days remaining. Six emails in two sequences:
three to the acquirer's CFO, and three to the site GM, which are omitted from this page.

Hand-off (read by 06):
account: Corrow Ridge Cemetery (TARGET)
run_date: 2026-10-19
trigger_type: Acquisition / M&A (profile trigger: consolidator buys the site)
urgency_window: 2026-08-30 to 2026-10-29
days_remaining: 10
event_tag: [Public: state licensing database]
sequence: six emails, three to the acquirer's CFO or controller (name [Unknown]) and three to the site GM. The GM's three are omitted from this example
report_path: none (inline)
next_action: Nadia Brandt finds the acquirer's CFO or controller by 2026-10-20, then sends Email 1 after reading the draft

---

### Example 2: Undated Finding, UNVERIFIED (Quill Hollow Memorial Park)

**Context:** Quill Hollow Memorial Park is one site with 8,800 plots (illustrative) and paper plat maps. Its
last state review produced a records finding (illustrative). The CRM records the finding but not the date of
the review. The general manager, Ines Carmody, moved here from Lowmoor six months ago and is the champion.

**Input:** "Quill Hollow had a records finding in its last state review. Build trigger outbound."

**Step 0: Role Detection.** The user is a BDR, Nadia Brandt. The CRM shows status TARGET with no open deal.
Full sequences would apply if the trigger were usable.

**Step 1. Classify.** Trigger type: Compliance Failure / Costly Error. The matching profile trigger is "Audit
finding on records or trust fund", with the cemetery GM as the persona who acts. Event tag: `[CRM]`, the note
that records the finding. The event date is `[Unknown]`, because the CRM note does not carry the review date.

**Step 1d. Stop.** The window cannot be computed.

> **Refused.** The profile's window for this trigger is 60 to 120 days after the event date, and the event
> date is `[Unknown]`. This skill will not estimate a date, will not use the day the CRM note was written, and
> will not pick either end of a window from an invented date. Days remaining: none. Share remaining: none.
> Trigger status: UNVERIFIED.

**Output.** The classification and the open question only. Sequence: none. The sequences for Account Snapshot,
Meeting Prep and Daily Prospecting cite the same finding the same way, as `[CRM]` with the date unknown.

**The question that clears it.** The review date comes from the state review letter or from Ines Carmody. Once
either one supplies the date, the CRM note is updated with the date and its source, and the skill runs again.

**Decision rule once the date is known.** If the window is still open, run the trigger as Example 1 does. If it
has closed, route to Account Snapshot (`gtm-account-snapshot`) or Research Outbound (`gtm-research-outbound`).
The finding's own date sets the clock, never the date the CRM note was entered.

**Summary:** BDR. Quill Hollow Memorial Park, trigger UNVERIFIED. Nothing is sent until the review date is found.

Hand-off (read by 06):
account: Quill Hollow Memorial Park (TARGET)
run_date: 2026-10-19
trigger_type: Compliance Failure / Costly Error (profile trigger: audit finding on records or trust fund)
urgency_window: none, the event date is [Unknown]
days_remaining: none
event_tag: [CRM], date [Unknown] (illustrative)
sequence: none, trigger status UNVERIFIED
report_path: none (inline)
next_action: Nadia Brandt asks Ines Carmody for the review date by 2026-10-23

---

### Example 3: Rival Renewal on an Active AE Deal (Brackhaven Memorial Gardens)

**Context:** Brackhaven Memorial Gardens is ACTIVE at Stage 5 Negotiate, and AE Owen Pruitt owns the deal. Its
legacy on-premise system is from Oldgate, a direct-software incumbent, with a renewal in March 2027. The
renewal day of 1 March is illustrative. The family board meets on 2026-11-12.

**Input:** "Brackhaven's Oldgate renewal is March 2027. Build trigger outbound."

**Step 0: Role Detection.** The user is a BDR, Nadia Brandt. The CRM shows ACTIVE at Stage 5 with AE Owen Pruitt
as owner. The BDR with an active AE deal path applies.

**Step 1. Classify.** Trigger type: Competitor Contract Event. The matching profile trigger is "Rival contract
renewal", which the profile routes to Competitive Displacement (12). Event tag: `[CRM]`, the renewal as logged
in the CRM.

**Step 1c. Active Deal Guard.** No sequence goes to the buyer. Two people writing to one buyer costs the deal, so
this run writes a coordination note for the AE instead.

**Step 1d. Timeliness.** No window is computed here. The profile routes this trigger to Competitive Displacement
(12), which owns the timing. This skill does not compute that window, so `urgency_window` is none.

**Output.** Zero emails. One coordination note to the AE:

> Owen, Brackhaven's Oldgate renewal is March 2027 `[CRM]`. Your deal is at Stage 5 Negotiate, and the family
> board meets on 2026-11-12 `[CRM]`. The renewal may speed the board's decision. Suggest you raise it with Ruth
> Ellery in your next conversation. I can run Competitive Displacement (12) on Oldgate before then if it helps.

**Summary:** BDR. Brackhaven Memorial Gardens, coordination only. The rival renewal goes to Competitive
Displacement, and the AE decides when to raise it with the champion.

Hand-off (read by 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate, AE Owen Pruitt)
run_date: 2026-10-19
trigger_type: Competitor Contract Event (profile trigger: rival contract renewal)
urgency_window: none, routed to Competitive Displacement (12)
days_remaining: none
event_tag: [CRM]
sequence: none, coordination note to the AE
report_path: none (inline)
next_action: Nadia Brandt sends the note to Owen Pruitt by 2026-10-21, after reading it

---

## Common Patterns

### Pattern: Stacked Triggers
**When:** Two separate dated events happen at one account, such as a private-equity acquisition and a new CFO.
**Approach:** Classify each event on its own, with its own window. Email 1 uses the event with the shorter remaining window. Each email uses a different event angle. No example here stacks triggers, because no account in the example cast has two dated events. Add one when a real stack appears.

### Pattern: Trigger and Displacement Combo
**When:** The trigger reveals a rival contract.
**Approach:** When the profile routes the trigger to Competitive Displacement (12), this skill writes no sequence and hands the timing to 12. Run 12 for the deeper competitive analysis, as Example 3 does.

### Pattern: LinkedIn Thought Leadership Trigger
**When:** An executive posts about the pain on LinkedIn.
**Approach:** The window is the profile's row for this trigger, not a number in this skill. Write a single-persona sequence for the person who posted, and quote the post in Email 1.

### Pattern: Trigger on Closed-Lost Account
**When:** A trigger event occurs at an account that was closed-lost.
**Approach:** Use this skill for the time-sensitive sequence, and open it with the history from `gtm-closed-loss-reactivation`. That skill decides first whether the account should be contacted at all.

---

## Troubleshooting

### The Event Is Past Half of Its Window
**Likely cause:** A normal window running down. Nothing is wrong.
**Response:** Read the trigger status. STALE still runs and says the deadline in Email 1. EXPIRED does not run. Acquisitions can stay in integration for months, so an acquisition can carry residual relevance. Change the Email 1 opener from "I saw your announcement" to "Since the event in [month], your team is likely dealing with [implication]."

### The Event Cannot Be Verified
**Likely cause:** The source is a rumor, a single unconfirmed post, or a record without a date.
**Response:** Mark the trigger UNVERIFIED and write no sequence. Name the source that would confirm the event and who can obtain it.

### The Event Date Is Unknown
**Likely cause:** The CRM note was written without the date.
**Response:** Use the Step 1d refusal. Ask the note's author for the date, attach the source to the note, and run the skill again once the date is known.

### Multiple Trigger Types Apply
**Likely cause:** One event matches two types, such as an acquisition that brings in a new executive.
**Response:** Follow the decision tree, which sends personnel changes to New Executive Hire first. Use Stacked Triggers only when a second, separate dated event exists.

### The Implications Feel Speculative
**Likely cause:** This is expected. The event is a record, and the implications are always `[Inferred]`.
**Response:** Frame each implication as a question, such as "I imagine..." or "Curious how this is affecting...". Let the buyer confirm or deny it.

### The Trigger Reveals a Rival Contract
**Likely cause:** The event shows a competitor's contract is near renewal.
**Response:** Route the trigger as the profile says, to Competitive Displacement (12). Coordinate with the AE if one owns the deal.

### A BDR Finds a Trigger on an Active AE Deal
**Likely cause:** The Active Deal Guard applies.
**Response:** Write the coordination note only, in the format Example 3 uses. Do not send a sequence.

---

## Best Practices

### Do's
- **Act inside the window.** The window closes on a fixed date, so a sequence that lands on time beats a polished one that lands late
- **Reference the specific event.** "Congratulations on the acquisition" is not enough. Cite the date and the detail
- **Frame urgency from real business timing.** Tie the call to the review, the renewal or the board date the record shows
- **Match proof points to the trigger.** Use only the proof points the profile marks Verified or Benchmark
- **Tag every fact.** Events are tagged to their record. Implications are tagged `[Inferred]`
- **Print the window every time.** Both dates, the days remaining and the share remaining

### Don'ts
- **Don't wait for perfect intelligence.** A dated public record is enough to start the window check
- **Don't use generic subject lines.** "Following up" removes the reason to open the email
- **Don't reference an UNVERIFIED event.** Confirm the event happened before the buyer hears about it
- **Don't send trigger sequences on an AE's active deal.** Coordinate through the AE
- **Don't use the same angle twice in a sequence.** Each email must add a different implication or question
- **Don't force a trigger that isn't there.** Not all news is a trigger. If the event does not connect to a value proposition, skip it

---

## Integration With Other Skills

- **`gtm-account-snapshot`** (02) hands this skill `account_status`, `verdict`, `contact_priority`, `pain_hypotheses` and `sequence`. Use the snapshot for context when a trigger arrives on an account that has not been profiled.
- **`gtm-closed-loss-reactivation`** (05) hands this skill `loss_classification`, `change_assessment`, `reactivation_strategy` and `history_opener`. A trigger on a closed-lost account uses `history_opener` for the first line, and `reactivation_strategy` decides whether to send at all.
- **`gtm-meeting-prep`** (06) receives from this skill `trigger_type`, `urgency_window`, `days_remaining`, `event_tag` and `sequence`. The prep sheet cites the event with its tag and its window.
- **`gtm-competitive-displacement`** (12) receives the timing when the profile routes a trigger there. This skill writes no sequence in that case.
- **`gtm-research-outbound`** (03) and **`gtm-account-snapshot`** (02) receive an EXPIRED or undated event that needs a different approach.
- **`gtm-deal-pulse`** (08) monitors the pipeline once a trigger creates an opportunity.
- **`gtm-daily-prospecting`** (07) can surface a trigger during the daily routine.
- **Wrap-Up** reads `report_path` when a file was written, the trigger status, and `next_action` with its owner and date.

### Chains

- **Win Back:** Closed-Loss Reactivation (05), then Trigger Event Outbound (04, this skill) on a dated event at a lost account, then Meeting Prep (06). This skill adds the window check, so a trigger that has closed is not sent.
- **Qualify To Book:** Account Qualification (01), Account Snapshot (02), Research Outbound (03) or Trigger Event Outbound (04, this skill), then Meeting Prep (06). This skill sends the time-sensitive sequence when a dated event opens a window.

---

## Changelog


### 2.1.3 (2026-10-26)
- Try-it evidence completed so a strict first run reproduces Example 1.
- Decision tree gains one sentence: an acquisition that changes who owns the account is Acquisition / M&A from the taxonomy unless steps 1 to 6 match first.
- Trigger Status, STALE, gains one sentence: the deadline an email names is the profile's citable date, not the window's last day.
- Example 1 implication 3 is tagged [Inferred] with its basis, not with the deal notice tag. Its subject lines now name the event, and Email 1 cites the deal notice for the review date.
- Example 1 states the disqualifier with both conditions. Email 1 asks nothing that depends on the ownership and system check, and Email 2, which waits for that check due 2026-10-22, asks the system question.
- No window, status, sequence date, verdict or next action changes.

### 2.1.2 (2026-10-25)
- Try-it evidence completed so a strict first run reproduces Example 1.

### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1. No other change.

### 2.1.0 (2026-10-25)
- Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### Version 2.0.0 (2026-10-20)
- Trigger windows and personas now come from the profile's Buying Triggers table. The rule or deadline comes from the Trigger Catalog with a citation. The unsourced 7-to-14-day and 30-to-60-day windows are removed from the taxonomy
- One window rule, stated once, with the arithmetic printed in the Corrow Ridge example
- Evidence grades replaced by the six shared tags. UNVERIFIED is kept as a trigger status for events with no date
- One name for each trigger type across the taxonomy, the decision tree and the mapping ("Earnings Miss / Margin Pressure")
- Corrow Ridge example is now a three-email sequence inside its window. Quill Hollow example refuses to time an undated finding. Brackhaven example routes the rival renewal to Competitive Displacement under the profile
- Context adds Industry Context, the Buying Triggers table and the Trigger Catalog. The shared contract is added under Context
- Output Contract is a table with the hand-off fields by name. Each stage has a Produces line. Why This Skill Exists, Hard Rules with reasons and a Quality Bar are added
- The file is written only when the user asks for one. The artifact section section is folded into the Output Contract
- The response-rate reference is removed

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, example errors fixed and a non-success example added
- Unsourced statistics removed. Persona placeholders filled from the profile. Financial trigger routing corrected to existing trigger types

Earlier versions (1.0.0 to 1.2.0) are in the git history of this repository.
