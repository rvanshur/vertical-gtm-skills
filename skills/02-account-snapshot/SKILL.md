---
name: gtm-account-snapshot
description: "One-page account brief for BDRs and AEs: a zone-based verdict, persona-ranked contacts, tagged pain hypotheses, a three-step email draft and call prep, read by the rep before anything is sent."
version: 2.1.0
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-25
tags: [account-snapshot, bdr-daily-driver, outbound, prospecting, cold-call-prep, email-sequences, cheatsheet, sales-2-0]
requires:
  skills: [gtm-account-qualification, gtm-competitive-displacement]
mutating: read-write
change_log:
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection (Qualify To Book, Beat The Incumbent) and a Guild Pro Kits subsection that names the five hand-off fields the Business Case & ROI Kit reads."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Verdict now comes from the profile's Qualification Zones and Verdict Rule, with zone scores beside it. Region map uses the profile's own tiers with a source per tier. Proof points come only from the Proof Points table. Evidence labels replaced by the six shared tags. Hard Rules with reasons replace the Don'ts. Hand-off fields named in the Output Contract, the Integration section and the examples. Examples aligned to the PlotIQ chain file."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on PlotIQ, with the tier wording made vertical-neutral."
---

# Account Snapshot Outbound

## Overview

Account Snapshot is the rapid outbound package for one account. It pulls the CRM record, scores the account against the profile's qualification zones, maps known contacts to buyer personas, writes pain hypotheses, drafts a three-step email sequence and builds a cold call sheet. The rep gets one page to read between dials, and the page is built to be checked, not trusted.

Every fact carries one of six evidence tags. Every verdict follows the profile's Verdict Rule as written. Every email is a draft. The rep reads, edits and sends. The skill never sends an email, never enrolls a contact and never writes to the CRM.

**Core Principle:** Speed with specificity. Every output is actionable within minutes, and every fact says where it came from.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

Volume outbound fails in two plain ways. A rep sends an email with a figure nobody can trace, and the buyer asks for the source on the first call, which ends the conversation. Or a rep works an account another rep already owns, and the buyer receives two emails from one company in the same week. Both failures happen when the research lives in the rep's head instead of on the page.

This skill puts every claim on the page with its tag, checks the account owner before any draft is written, and scores the account on the same zones every other sales skill uses. The profile supplies the facts, so the same account reads the same way in every skill that touches it.

---

## Role

You are a **BDR daily driver and rapid account researcher for a vertical SaaS team** (not a generic lookup tool). You build a one-page outbound package for one account: research, zone verdict, contacts, pain hypotheses, email drafts and call prep. Every company fact comes from the profile, so the same skill works in any vertical.

You refuse to write a claim you cannot tag. You refuse to score silence as a no. You refuse to propose a demo before the pain is confirmed. You refuse to work an account that an AE owns unless the AE has said yes. You never send, enroll or write to the CRM.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Yes | The company to research. Matched to the CRM record when one exists |
| User role (BDR or AE) | Yes | Sets the call goal and the owner check. Asked when the context does not make it clear |
| CRM access | No | Without it, facts carry public or Unknown tags, and the status comes from the profile's example cast when the account is listed there |
| Prior interactions | No | Calls and notes, read as `[Call]` or `[Notes]` with their dates |
| Persona to focus on | No | Narrows the sequence to one buyer |

---

## Output Contract

Every run returns its report in the chat. The file is written only when the user asks for it.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Cheatsheet, eight sections | In the chat | Company Snapshot, Geographic and Market Exposure, Key Personas, Pain Hypotheses, Discovery Questions, Value Props, Objection Handling, Call Flow. The layout never changes between runs |
| `account_status` | Top of the Company Snapshot | One of TARGET, INBOUND, ACTIVE (with its stage number), LOST or OUT |
| `verdict` | Beside the zone scores | GREENLIGHT, MANUAL REVIEW or DISQUALIFY, from the Verdict Rule as written |
| `zone_scores` | Beside the verdict | One line per zone, 1 to 5, each HIGH, MEDIUM, LOW or UNKNOWN. Carried as handed by Account Qualification (01) when it ran, otherwise scored here with a tag per zone |
| `contact_priority` | Key Personas | Ranked contacts, each with persona and buying role. Unknown where no contact is found |
| `pain_hypotheses` | Pain Hypotheses | Ranked by confidence, each one tagged |
| `sequence` | Below the cheatsheet | Three emails per persona, drafted and never sent. Quick Call Prep mode omits it |
| `report_path` | Only when a file was written | Set only when the user asks for the file. Wrap-Up reads it |
| `next_action` | Last line of the summary | Owner and date, for example "Nadia Brandt sends Email 1 by 2026-10-21" |
| File option | `<account>_<skill>_<date>.md`, saved beside the user's other account notes | Written only when the user asks. Markdown only. The ask is the approval step |

---

## Context

The skill reads these sections of the profile file. Section names below are the profile's own names.

| Profile section | Used for |
|-----------------|----------|
| ICP Definitions | Segment and the ICP line for the verdict |
| Qualification Zones | The five zone scores beside the verdict |
| Verdict Rule and Disqualifiers | The verdict, applied as written |
| Qualification Stage Gates | Stage names for any ACTIVE account |
| Buyer Personas | Contact priority and persona-matched sequences |
| Core Pain Points | Pain hypotheses |
| Value Propositions | The mechanism behind each pain |
| Proof Points | One per email, matched to segment and persona, never an Illustrative result |
| Competitive Landscape | Incumbent and objection handling |
| Outbound Voice | Reference email, research sources, call-today triggers and the region map. This skill's CUSTOMIZE interview writes it |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls, decisions for that account), read in Step 1 for prior history on the account |

If the Outbound Voice section is missing, this skill runs uncustomized. It says so once at the start and marks every output that depended on the missing section.

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

### Evidence Tags for Rapid Research

Every fact in the report carries exactly one of the six shared tags. A fact with no tag is removed from the report.

| Tag | Meaning | Usable as a claim in an email |
|-----|---------|-------------------------------|
| `[CRM]` | A field or note in the CRM | Yes |
| `[Call]` | Said on a recorded or transcribed call, with the call date | Yes |
| `[Notes]` | A rep's or AE's written notes | Yes |
| `[Public: source]` | A public document, page or filing, with the source named | Yes |
| `[Inferred]` | Reasoned from other facts, with the reasoning shown and the method named | No. Written as a question |
| `[Unknown]` | Not known. Written as unknown, never left blank | No. Becomes a discovery question |

Pain hypotheses carry the `[Inferred]` tag, because they are educated guesses from the profile and not confirmed pain. An estimate also takes `[Inferred]`, with its method named, because the tag set has no separate estimate tag.

### Speed Versus Depth

1. **CRM first.** Check the CRM before web research. It is the record a manager can check, and it is faster.
2. **Five-minute research ceiling.** If research runs past five minutes, stop and work with what you have. The rest becomes discovery questions.
3. **Unknown is acceptable.** An `[Unknown]` tag with a discovery question beats a fabricated fact.

### Zone Scores and the Verdict

Score each of the five zones HIGH, MEDIUM or LOW from tagged facts, using the profile's Qualification Zones definitions. Score a zone UNKNOWN when the record is silent. UNKNOWN is not LOW, because a blank field may only mean nobody recorded it. Zones 1 and 3 are must-haves.

Apply the Verdict Rule as written:

- **GREENLIGHT:** at least two zones HIGH, and no must-have zone at LOW.
- **MANUAL REVIEW:** neither GREENLIGHT nor DISQUALIFY holds. Usually one HIGH zone, or a must-have zone at LOW.
- **DISQUALIFY:** a disqualifier from the profile applies, or both must-have zones are LOW.

MEDIUM never counts as HIGH. The next skill reads these zones, so a score that rounds up changes its verdict.

Name the zones that carry the verdict beside it. A GREENLIGHT shows its two HIGH zones. A MANUAL REVIEW shows the one HIGH zone, or the must-have at LOW.

### ICP Quick-Score Signals

These five signals are the one-glance read a rep sees first. They do not set the verdict. The zones do.

| Signal | Scoring |
|--------|---------|
| Primary fit signal | Yes, Partial or No, against the ICP Definitions |
| Geographic or scale signal | Single region, or Multi-region (name the regions) |
| Regulatory or complexity signal | High, Medium or Minimal |
| Scale (volume) | Enterprise, Mid-Market or SMB, using the profile's own bands |
| Team complexity signal | Dedicated team, Small team or Unknown |

### Confidence in Pain Hypotheses

- **HIGH:** the hypothesis matches the profile on three or more signals, such as size, vertical, footprint and CRM history.
- **MEDIUM:** it matches on one or two signals. It is plausible and needs validation.
- **LOW:** it is generic and could describe any company in the industry. Rewrite it to be specific, or flag it as weak.

### Region Map

The tiers come from the profile's Outbound Voice region map, not from this skill. Each tier names the cost of a missed rule there and its source. Rank accounts in the highest-cost tier first, because a missed rule costs the most there. A state that is not recorded in the CRM gets no tier until someone records it. A tier still marked as a record placeholder in the profile is not a tier yet, so say so instead of guessing one.

---

## Quick Reference

**Use this skill when:**
- Preparing for a prospecting call or an outbound block
- Needing a quick account brief before reaching out
- A BDR needs a complete outbound package for one account
- Running snapshots across several accounts in one block

**Don't use when:**
- You need deep financial analysis of a public company (use `gtm-research-outbound`)
- The account has a known incumbent to displace (use `gtm-competitive-displacement`)
- The account is a closed-lost deal (use `gtm-closed-loss-reactivation`)
- A trigger event just happened (use `gtm-trigger-event-outbound`)

**User roles:** BDR (primary), AE
**Expected time:** 5 to 10 minutes per account

---

## Core Workflow

### Step 0: Detect the User Role

Decide whether the user is a BDR or an AE. The role changes the call goal, the summary framing and the owner check.

Read the role from the CRM when it is recorded. If it is not clear, ask: "Are you a BDR or an AE?"

**Produces:** `user_role` (BDR or AE)

### Step 1: Gather Intelligence

Run the CRM search first, then the research, because the CRM is the record a manager can check. Before pulling anything, open the account's folder under `accounts/` in the Knowledge Base, if the profile has one, and offer the CRM read and, when a call recorder is connected, the call read, for the one account or date range you name. Nothing is read from the CRM or the call recorder until you say yes.

**1a. Search the CRM.** Pull the account record (name, industry, headquarters, website, owner, status), deal history with stages and amounts, every contact with title and last activity, engagement history with dates, and any notes or summaries reps wrote. Note the BDR owner and the account owner.

**1b. Research the company.** Build a quick profile from public sources: what the company does, its size signals, its footprint, its ownership, and recent news such as acquisitions, expansions and leadership changes. Tag every fact. Where a fact cannot be found, tag it `[Unknown]` and write the discovery question that would fill it.

**Produces:** a list of tagged facts from the CRM and from public sources, and the list of Unknown facts that become discovery questions.

### Step 2: Build the Account Snapshot

Build the company brief, the quick-score signals, the zone scores with the verdict, and the region map, in that order. The zones come before any sequence, because the verdict decides whether a sequence is written at all.

**Company brief (5 to 8 bullets):** Company (full name and headquarters), Segment (from the ICP Definitions), Vertical, Size (with its tag), Footprint (regions, locations, key markets), Ownership, CRM Status (TARGET, INBOUND, ACTIVE with its stage name from the profile, LOST or OUT), Current owner and BDR owner, and Coordination Required. Coordination is "Yes, coordinate with [AE name]" when the user is a BDR and an AE holds an open deal.

**Zone scores and verdict:** Score the five zones with Step 2's rules, show each zone's score with its tag, and state the verdict from the Verdict Rule. Each verdict names the zones that carry it.

**Region map:** Map the account's state to the profile's tier, with its source. Name the cost of a missed rule in that tier.

**Produces:** the company brief, the five zone scores with their tags, the verdict, the account status, and the region tier (or an explicit "no tier yet").

### Step 3: Map Contacts to Personas

Map the known CRM contacts to the profile's Buyer Personas. For each persona, record the name or Unknown, the title, the engagement level, the last activity and a priority from 1 to 5.

Rank the contacts by four rules, in order: known contacts with engagement history come before cold ones, persona relevance to the likely pain comes next, recent activity counts above old activity, and prior deal context breaks ties. Recommend the top two or three personas to target first, with the reason for each. Name the personas with no contact on file as gaps.

**Produces:** `contact_priority`, a ranked list of contacts with persona and buying role, and the persona gaps.

### Step 4: Generate Pain Hypotheses

Write three to five pain hypotheses from the profile's Core Pain Points, ranked by how well the account's profile supports each one. For each hypothesis, give:

- **Pain point:** the name from the profile's taxonomy
- **Why likely:** the reasoning, with its tag
- **Confidence:** HIGH, MEDIUM or LOW, per the confidence rules above
- **Discovery question:** the question that validates it on a call
- **Value prop:** the profile's value proposition that addresses it, stated as its mechanism

Order the hypotheses by confidence, HIGH first. If every hypothesis is MEDIUM or LOW, say the account needs more research or a discovery call before deeper work.

**Produces:** `pain_hypotheses`, ranked, each one tagged, each with its discovery question.

### Step 5: Generate the Outbound Sequence

Draft a three-step email sequence for each of the top two or three personas. The sequence comes after the pain hypotheses, because each email uses one hypothesis, so the ranked list must exist first.

**Rules for every email:**
- Include a subject line.
- Keep the body to 100 words or fewer.
- Open with something specific to the company, tagged `[CRM]` or `[Public: source]`.
- Use the contact's name when it is known.
- Give each step a different pain or angle.
- Use only `[CRM]`, `[Call]`, `[Notes]` and `[Public: source]` facts as claims. Write `[Inferred]` and `[Unknown]` facts as questions.
- Use at most one proof point per email, from the profile's Proof Points table, matched to the segment and the persona. Never use an Illustrative result, because a prospect who asks for its source gets none. A Benchmark is cited with the source named.

**Sequence structure (per persona):**

| Step | Angle | Purpose |
|------|-------|---------|
| Email 1 | A company-specific pain and the product connection | Show the homework and earn the open |
| Email 2 | A different pain, with one proof point that fits | Build credibility |
| Email 3 | A breakup note with one question | A low-pressure close |

Account Snapshots use three steps, not four, because this is volume outreach.

**Produces:** `sequence`, one three-step set per persona, drafted, with each claim's tag listed beneath the draft.

### Step 6: Build the Call Prep Sheet

**Role-aware call goal:**

| Role | Call Goal |
|------|-----------|
| BDR | Book a 15-minute discovery call for the AE |
| BDR with an active AE deal | Stop. Share the research with the AE instead |
| AE | Advance the deal to its next stage step |
| AE with no deal | Qualify interest for a new opportunity |

**Next step after a first call:** a discovery call, not a demo, until the pain is confirmed. A demo asks the buyer for an hour before there is a reason to give it.

**Opener (30 seconds):** "Hi [name], this is [rep] from [company]. I'm calling because [a specific reason tied to pain hypothesis 1]. Do you have 30 seconds?"

**Talk track:** a pain validation question, an impact question, a one-sentence product bridge, and an ask for 15 minutes.

**Voicemail (under 30 seconds):** name and company, one specific statement, and the call to action "I'll send a quick email with details."

**Objections:** Use the profile's Competitive Landscape for competitive objections. Include four to five objections with rebuttals tailored to the account.

| Objection | Rebuttal |
|-----------|----------|
| "We already have a solution" | "Good, that means you understand the value. What's working well, and what would you improve?" |
| "Not interested" | "Fair enough. How is your team handling [pain hypothesis 1] today?" |
| "Send me an email" | "Happy to. Would the ROI overview or the capability overview be more useful?" |
| "No budget" | "That makes sense. If I could show you how a similar operator solved [pain], would 15 minutes be worth it?" |
| "We're too small or not ready" | "Smaller sites often say that until a records question comes up in a review. Is your plot list ready for one?" |

**Produces:** the call goal, the opener, the talk track, the voicemail and the objection table, all tied to the ranked pain hypotheses.

### Step 7: Assemble the Cheatsheet and Summary

Assemble the eight cheatsheet sections in this order: Company Snapshot, Geographic and Market Exposure, Key Personas, Pain Hypotheses, Discovery Questions, Value Props, Objection Handling and Call Flow.

Close with a summary line in this order: the user's role, the account, the status, the verdict with the zones that carry it, the contacts found and their gaps, the personas targeted, the number of sequence emails, the recommended first action with its owner and date (`next_action`), and the tag count for the report.

**Produces:** the eight-section cheatsheet in the chat, the summary line, and `next_action`.

---

## Modes

- **Full Snapshot (default).** Steps 0 to 7, all eight cheatsheet sections, and the sequence. Use it for a single account the rep will work this week.
- **Quick Call Prep.** Steps 1 to 4 and Step 6 only. Skip the sequence. Use it when the rep says "quick call prep" or "calling in five minutes," because speed matters more than completeness before a call.
- **Batch.** Steps 1 to 4 for each account, then a ranked summary table. Full sequences for the top two or three accounts only. Use it for five to ten accounts in one prospecting block.

No mode writes a file. A file is written only when the user asks for one, under the Output Contract.

---

## Epistemic Rules

- **Print n beside every rate.** "4 of 7 criteria" is readable. "57%" alone is not, because the reader cannot tell whether it rests on four cases or four hundred.
- **Five cases before a pattern.** A pattern across accounts needs at least five cases. Fewer cases are an observation, and the summary says so in the same sentence.
- **Silence is not a no.** A blank CRM field is Unknown, and it counts in no denominator. Scoring it as a no invents a finding out of missing data.

---

## Hard Rules

1. **Never cite an Illustrative proof point, and never use a proof point the profile does not list.** A prospect who asks for the source of an Illustrative result gets nothing, and the rep loses the buyer's trust in the first email.
2. **Never use an `[Inferred]` or `[Unknown]` fact as the claim in an email.** A guess written as a claim is something the rep must defend on the call, so it goes in as a question.
3. **Never score silence as a no, and never score UNKNOWN as LOW.** A blank field may mean nobody recorded it, and a LOW score moves the verdict.
4. **Never override the Verdict Rule.** MEDIUM never counts as HIGH, because the next skill reads these zones, and a score that rounds up changes its verdict.
5. **Never work an ACTIVE account with an AE owner unless that AE has said yes.** Two people writing to one buyer costs the deal, and the buyer sees the duplicate.
6. **Never propose a demo as the next step while the pain is unconfirmed.** A demo asks the buyer for time before there is a reason to give it.
7. **Never send an email, enroll a contact or write to the CRM.** The rep reads the draft and sends it, because the rep owns the relationship and the record.
8. **Never write an outcome number without its source or its Illustrative mark.** An unsourced figure in an email becomes the first question the buyer asks.
9. **Never use a tag outside the six.** A manager checks the report by tag, and a seventh label cannot be checked.

---

## Quality Bar

Done when all are true:

- [ ] Every fact carries one of the six tags, and no fact is left untagged
- [ ] The verdict follows the Verdict Rule, with the zones that carry it named beside it
- [ ] Every zone score carries its tag, and no UNKNOWN zone is scored LOW
- [ ] The account status is one of the five words, and an ACTIVE status carries its stage name from the profile
- [ ] The owner check ran, and an AE-owned account is named as coordination, not worked
- [ ] Every Email 1 opens with a specific, tagged company fact
- [ ] Every email is 100 words or fewer, and no email uses an `[Inferred]` or `[Unknown]` fact as a claim
- [ ] Every proof point in an email is in the profile's Proof Points table and is not Illustrative
- [ ] The call goal matches the user's role, and no demo is proposed before the pain is confirmed
- [ ] Each rate carries its n, and each pattern rests on five cases or is labelled an observation
- [ ] The hand-off block lists every field by name, with its value

---

## Examples

These examples use the PlotIQ example cast, and every fact is tagged as the tag set requires. A number the profile does not supply is marked `(illustrative)`. The four examples cover a BDR research pass that leads to outbound, an AE quick call prep that ends in MANUAL REVIEW, a batch with a disqualified account and a closed-lost one, and the flagship account at its first snapshot. Each ends with a hand-off block.

### Example 1: BDR Account Snapshot (Quill Hollow Memorial Park, TARGET, GREENLIGHT)

**Context:** A BDR prepares a first outbound touch during a morning block. The general manager, Ines Carmody, moved to Quill Hollow from Lowmoor Memorial Gardens six months ago. Her history at Lowmoor is a closed-loss matter for Closed-Loss Reactivation (05), not this outbound.

**Input:** "Account snapshot on Quill Hollow Memorial Park, with outbound sequences and a cheatsheet."

**Step 0: Role Detection.** The user is a BDR. The CRM shows the account, status TARGET `[CRM]`, and no open deal `[CRM]`. Clear to proceed.

**Step 1: Intelligence Gathering.** One site, 8,800 plots, paper plat maps `[CRM]`. One contact on file: Ines Carmody, General Manager, champion `[CRM]`. The owner signs under $25K `[CRM]`. The owner's name is `[Unknown]`. A records finding appears in the last state review `[CRM]`, and its date is `[Unknown]` (both illustrative). The owner brought a growth mandate when Ines Carmody arrived `[CRM]`. The state is not recorded `[Unknown]`, so no region tier yet.

**Step 2: Account Snapshot.**

Company brief: Quill Hollow Memorial Park. Independent cemetery `[CRM]`. One site, 8,800 plots `[CRM]`. Ownership `[Unknown]`. CRM status TARGET. No active deal.

Quick-score signals: primary fit Yes, 8,800 plots on paper, above the ICP1 Strong line `[CRM]`. Single region `[CRM]`. Regulatory complexity High, because of the records finding `[CRM]`. Scale mid-size, one site `[CRM]`. Team complexity: a dedicated GM and owner `[CRM]`.

Zone scores (illustrative), with the verdict:

- Zone 1, Records and Inventory Pain: MEDIUM. Paper plat maps `[CRM]`. The records finding has no date `[Unknown]`, so the HIGH test (a finding in the last 24 months) is not met.
- Zone 2, Pre-Need Sales Motion: UNKNOWN. No pre-need activity is recorded `[Unknown]`. Silence is not a no.
- Zone 3, Ownership and Decision Speed: HIGH. The owner signs under $25K `[CRM]`.
- Zone 4, Technology Readiness: UNKNOWN. Website and tools are not yet checked `[Unknown]`.
- Zone 5, Growth or Succession: HIGH. A new GM in the last 24 months `[CRM]`, and an owner growth mandate `[CRM]`.

Verdict: **GREENLIGHT.** Two zones are HIGH (3 and 5), and no must-have zone is LOW. Zone 1 is MEDIUM, which blocks nothing. If the finding is dated inside 24 months, Zone 1 becomes HIGH, so the date is the first thing to find.

Region map: no tier, because the state is not recorded `[Unknown]`.

**Step 3: Contact Mapping.**

| Persona | Name | Engagement | Last Activity | Priority |
|---------|------|-----------|---------------|----------|
| General Manager, champion | Ines Carmody | Warm, champion at her last site `[CRM]` | Two weeks ago (illustrative) | 1 |
| Owner, signs under $25K | Unknown, no contact found `[Unknown]` | n/a | n/a | 2 |
| Pre-need manager | Unknown `[Unknown]` | n/a | n/a | 3 |

Ines Carmody ranks first because she has engagement history and runs the site now. The owner ranks second, because the owner signs.

**Step 4: Pain Hypotheses.**

1. **Plot visibility.** HIGH confidence. The plot map is on paper `[CRM]`. `[Inferred]`, by reasoning from the record type: a paper map cannot show which plots are sold without a walk of the grounds. Discovery question: "How do you check today which plots are open?" Value prop: plot inventory matched against sold records.
2. **Records after a state finding.** MEDIUM confidence. The last state review found a records problem `[CRM]`, and its date is `[Unknown]`. The pressure is real, but its timing is not. Discovery question: "When was the last state review, and what did it ask you to fix?"
3. **Pre-need follow-up.** LOW confidence. No pre-need activity is recorded `[Unknown]`. Use it as a question, not as a lead.

**Step 5: Sequence (Ines Carmody, General Manager).**

Email 1

Subject: Plot records after the state review at Quill Hollow

Ines,

Quill Hollow's last state review turned up a records finding, and the plot maps are still on paper. How do you check today which plots are sold and which are open?

Most cemeteries your size carry 50 to 100 plots that are sold on paper but open on the map (Benchmark, deathcare research, paper-operations note, 2026-04-01). Worth 15 minutes to see whether your maps show the same gap?

The email names no customer result, because every PlotIQ result in the profile is Illustrative. Emails 2 and 3 for this persona follow the same structure, each with a different pain, and are omitted for length.

**Step 6: Call prep omitted for length.**

**Step 7: Summary.** BDR. Quill Hollow Memorial Park, TARGET, GREENLIGHT, with Zones 3 and 5 HIGH. One contact on file, Ines Carmody, first. Owner and pre-need contacts unknown. One persona, three emails, two omitted. Next action: Nadia Brandt sends Email 1 to Ines Carmody by 2026-10-21. Unknown facts to resolve on the call: the records finding date, the owner's name, the state.

```text
Hand-off (read by 06):
account: Quill Hollow Memorial Park (TARGET)
run_date: 2026-10-19
account_status: TARGET
verdict: GREENLIGHT
zone_scores: 1 MEDIUM, 2 UNKNOWN, 3 HIGH, 4 UNKNOWN, 5 HIGH (illustrative)
contact_priority: 1 Ines Carmody (General Manager, champion), 2 Owner, name Unknown (signs under $25K), 3 Pre-need manager, name Unknown
pain_hypotheses: 1 Plot visibility (HIGH, CRM and Inferred), 2 Records after a state finding (MEDIUM, CRM, date Unknown), 3 Pre-need follow-up (LOW, Unknown)
sequence: three emails to Ines Carmody, Emails 2 and 3 omitted for length
report_path: none (inline)
next_action: Nadia Brandt sends Email 1 to Ines Carmody by 2026-10-21
```

---

### Example 2: AE Quick Call Prep (Sable Fork Cemetery, INBOUND, MANUAL REVIEW)

**Context:** An AE has 20 minutes before a call. Sable Fork Cemetery filled in the website form on 2026-10-15, four days ago, asking for a demo. The general manager, Arlen Biggs, signs under $25K.

**Input:** "Quick call prep for Sable Fork Cemetery. They requested a demo from the website."

**Step 0: Role Detection.** The user is an AE. Quick Call Prep mode: Steps 1 to 4 and Step 6 only.

**Step 1: Intelligence Gathering.** The CRM holds a new record created from the form `[CRM]`, status INBOUND `[CRM]`, and no open deal `[CRM]`. Who filled in the form is `[Unknown]`. The search that led to the form is `[Unknown]`. One site, 2,900 plots `[CRM]`. The plot list is a spreadsheet `[CRM]`. The general manager, Arlen Biggs, signs under $25K `[CRM]`.

**Step 2: Account Snapshot.** Status INBOUND.

Quick-score signals: primary fit Yes, 2,900 plots, above the ICP1 Strong line `[CRM]`. Single site `[CRM]`. Regulatory complexity Unknown, because nobody has asked about a state finding `[Unknown]`. Scale mid-size `[CRM]`. Team complexity Unknown, because no records owner is named `[Unknown]`.

Zone scores (illustrative): Zone 1 MEDIUM (plot list in a spreadsheet `[CRM]`). Zone 2 LOW (illustrative). Zone 3 HIGH (the GM signs under $25K `[CRM]`). Zone 4 MEDIUM (illustrative). Zone 5 LOW (illustrative).

Verdict: **MANUAL REVIEW.** One zone is HIGH (Zone 3), so GREENLIGHT does not hold. The Verdict Rule gives MANUAL REVIEW for one HIGH zone. A MANUAL REVIEW does not authorize outbound.

Region map: no tier, because the state is not recorded `[Unknown]`.

**Step 4: Pain Hypotheses.**

1. **Plot lookups in a spreadsheet.** MEDIUM confidence. `[Inferred]`, by reasoning from the record type: a 2,900-plot list in a spreadsheet is harder to check against sold records than a digital system. Discovery question: "When someone asks for a plot, how long does it take to find it today?"
2. **Pre-need follow-up.** LOW confidence. No pre-need activity is recorded `[Unknown]`. Ask, do not lead with it.
3. **Single-person records risk.** LOW confidence. No records owner is named `[Unknown]`. Ask who maintains the list.

**Step 6: Call Prep.**

Call goal: confirm the pain, measure a real plot lookup, and find out who signs under $25K. The next step is a discovery call, not a demo, until the pain is confirmed.

Opener: "Thanks for asking for a demo. Before I show you anything, what prompted you to look for plot records software this week?"

Talk track:
- "When someone asks for a plot, how long does it take to find it today?"
- "How many plots do you think are open right now, and how would you check?"
- "Do you sell pre-need, and where do those leads go when they come in?"
- "Who signs off on a purchase under $25K, and does anyone else need to see it?"

Objection prep: "We're happy with the spreadsheet." Rebuttal: "That makes sense. When did you last check the spreadsheet against the plots you have actually sold?"

**Step 7: Summary.** AE. Sable Fork Cemetery, INBOUND, MANUAL REVIEW, with Zone 3 the only HIGH zone. No active deal. Quick call prep delivered. Next action: the AE books a discovery call with Arlen Biggs by 2026-10-22. Re-score the zones after that call.

```text
Hand-off (read by 06 and 04):
account: Sable Fork Cemetery (INBOUND)
run_date: 2026-10-19
account_status: INBOUND
verdict: MANUAL REVIEW
zone_scores: 1 MEDIUM, 2 LOW, 3 HIGH, 4 MEDIUM, 5 LOW (illustrative)
contact_priority: 1 Arlen Biggs (General Manager, signs under $25K), 2 Form filler, name Unknown
pain_hypotheses: 1 Plot lookups in a spreadsheet (MEDIUM, Inferred), 2 Pre-need follow-up (LOW, Unknown), 3 Single-person records risk (LOW, Unknown)
sequence: not generated, Quick Call Prep mode
report_path: none (inline)
next_action: The AE books a discovery call with Arlen Biggs by 2026-10-22
```

---

### Example 3: BDR Batch (Prospecting Block, Five Accounts, Mixed Outcomes)

**Context:** A BDR has a two-hour prospecting block and needs snapshots for five accounts, so the best two or three can be worked in depth. The list mixes stages and verdicts on purpose, so the table shows what the batch does with each one.

**Input:** "Quick snapshots on these five accounts for my outbound block: Corrow Ridge Cemetery, Greyfield Memorial Park, Tamsin Vale Cemetery, Northvale Memorial Holdings and Lowmoor Memorial Gardens."

**Batch Mode.** Steps 1 to 4 for each account, then this ranked table. Zone scores are illustrative. The table shows the zones that carry each verdict.

| Account | Status and Verdict | Zones That Carry the Verdict | Plots | Top Pain | Next Step | Priority |
|---------|--------------------|------------------------------|-------|----------|-----------|----------|
| Corrow Ridge Cemetery | TARGET, GREENLIGHT | Zone 1 HIGH, Zone 5 HIGH (illustrative) | 14,000 | Paper plat maps and a deed recorded twice in 2025 (illustrative) | Trigger Event Outbound (04). The ownership change closed 110 days ago, and 10 days of the window remain | 1 |
| Greyfield Memorial Park | TARGET, GREENLIGHT | Zone 1 MEDIUM (a digital map, with plot records and trust reporting still outside it), Zone 2 HIGH, Zone 3 HIGH | 9,000 | Pre-need and records wanted together | Competitive Displacement (12). The Stonemark contract renews January 2027 | 2 |
| Tamsin Vale Cemetery | TARGET, MANUAL REVIEW | Zone 1 HIGH, the only HIGH zone | 4,200 | Paper maps and one binder per section | Hold until the signer is known. Zone 3 is not HIGH | 3 |
| Lowmoor Memorial Gardens | LOST, re-scored MANUAL REVIEW | Re-scored on fit, zone detail in Closed-Loss Reactivation (05) | 7,500 | Closed-lost to Oldgate on "timing" `[CRM]` | Route to Closed-Loss Reactivation (05). Do not sequence from this table | 4 |
| Northvale Memorial Holdings | OUT, DISQUALIFY | A disqualifier applies, so zones are not scored | Not applicable | Runs its own in-house system `[Public: annual filing]` | Do not prospect | 5 |

**Recommendation.** Write the snapshot sequences for Corrow Ridge and Greyfield now. Trigger Event Outbound (04) and Competitive Displacement (12) write the sharper sequences for those two from their own inputs, so use these as the first drafts. Hold Tamsin Vale until the person who signs is known. Send Lowmoor to Closed-Loss Reactivation (05), because it is a closed-lost account and not a cold prospect. Drop Northvale from the queue.

```text
Hand-off (read by 06):
account: five accounts, one row each in the batch table above
run_date: 2026-10-19
account_status: TARGET for Corrow Ridge, Greyfield and Tamsin Vale. LOST for Lowmoor. OUT for Northvale
verdict: GREENLIGHT (Corrow Ridge, Greyfield), MANUAL REVIEW (Tamsin Vale, Lowmoor re-scored), DISQUALIFY (Northvale)
contact_priority: Corrow Ridge, the acquirer's CFO or controller and the site GM. Greyfield, the pre-need team, no names on file. Tamsin Vale, signer Unknown
pain_hypotheses: ranked per account in the table, each tagged
sequence: snapshot drafts for Corrow Ridge and Greyfield only. None for the other three
report_path: none (inline)
next_action: BDR sends the Corrow Ridge Email 1 by 2026-10-21
```

---

### Example 4: Flagship Account Snapshot (Brackhaven Memorial Gardens, TARGET, GREENLIGHT)

**Context:** A snapshot run the week the flagship was qualified, on 2026-05-04 (illustrative). At that point the account was TARGET, with no open deal, and the general manager was already on file as the buyer. This is the first snapshot in the PlotIQ chain, and its hand-off feeds the meeting prep for the first discovery call.

**Input:** "Account snapshot on Brackhaven Memorial Gardens, before our first outreach."

**Step 0: Role Detection.** The user is a BDR. CRM status TARGET `[CRM]`, no open deal `[CRM]`. Clear to proceed.

**Step 1: Intelligence Gathering.** Two sites, 11,000 plots `[CRM]`. Paper plot maps `[CRM]`. A combination of cemetery and funeral home `[CRM]`. One double sale in the last 24 months `[CRM]` (illustrative). The incumbent is Oldgate Ledger Pro, direct software, with a renewal in March 2027 `[CRM]`. The general manager is Ruth Ellery `[CRM]`. The family board is the decision body `[Notes]` (illustrative). The board chair's name is `[Unknown]`.

**Step 2: Account Snapshot.**

Company brief: Brackhaven Memorial Gardens. Combination, two sites `[CRM]`. 11,000 plots `[CRM]`. Paper plot maps `[CRM]`. Family-owned, with a family board `[Notes]` (illustrative). CRM status TARGET. No active deal.

Quick-score signals: primary fit Yes, a combination with 11,000 plots `[CRM]`. Two sites `[CRM]`. Regulatory complexity Medium `[Notes]` (illustrative). Scale enterprise for the segment `[CRM]`. Team: a GM and an operations director `[CRM]`.

Zone scores (illustrative), with the verdict:

- Zone 1, Records and Inventory Pain: HIGH. Paper plot maps at two sites `[CRM]`, and a double sale in the last 24 months `[CRM]` (illustrative).
- Zone 2, Pre-Need Sales Motion: MEDIUM. A pre-need manager runs the pre-need side `[Notes]` (illustrative). The intake form is `[Unknown]`, so the HIGH test is not met.
- Zone 3, Ownership and Decision Speed: MEDIUM. The GM recommends, and the family board approves and meets within 60 days `[Notes]` (illustrative).
- Zone 4, Technology Readiness: MEDIUM. A legacy system from Oldgate `[CRM]`.
- Zone 5, Growth or Succession: HIGH. The owner retires within three years `[Notes]` (illustrative).

Verdict: **GREENLIGHT.** Two zones are HIGH (1 and 5), and no must-have zone is LOW. Zone 3 is MEDIUM, which is not LOW, so the must-have does not block.

Region map: the state is not in the example notes `[Unknown]`, so no tier is assigned here.

**Step 3: Contact Mapping.**

| Persona | Name | Engagement | Last Activity | Priority |
|---------|------|-----------|---------------|----------|
| General Manager, buyer | Ruth Ellery | Known to the CRM `[CRM]` | Not recorded `[Unknown]` | 1 |
| Operations Director, influencer | Walt Okonkwo | Known to the CRM `[CRM]` | Not recorded `[Unknown]` | 2 |
| Pre-need manager, end user | Priscilla Dunmore | Known to the CRM `[CRM]` | Not recorded `[Unknown]` | 3 |

The family board chair is recorded as a gap, not as a person: no name is on file `[Unknown]`.

**Step 4: Pain Hypotheses.**

1. **Plot records on paper across two sites.** HIGH confidence. Paper plot maps at both sites `[CRM]`. `[Inferred]`, by reasoning from the record type: two sites on paper mean two lists, so a sale on one list can be missed on the other. Discovery question: "Which site's plot list do your staff check first?"
2. **The Oldgate renewal in March 2027.** MEDIUM confidence. The renewal date is `[CRM]`. `[Inferred]`, from the contract date: the renewal opens a decision window. Discovery question: "What happens at the Oldgate renewal, and who decides?"

**Step 5: Sequence (Ruth Ellery, General Manager).**

Email 1

Subject: Two sites, one plot list

Ruth,

Brackhaven runs two sites, and the plot maps at both are still on paper. How do you find a plot that is sold on one map and open on the other?

Most cemeteries your size carry 50 to 100 plots that are sold on paper but open on the map (Benchmark, deathcare research, paper-operations note, 2026-04-01). Worth 15 minutes to see whether your two sites show the same gap?

Emails 2 and 3 are omitted for length. The email names no customer result, because the profile's Brackhaven result is Illustrative and not yet signed.

**Step 6 and Step 7: omitted for length.** The summary states the verdict, the two HIGH zones, the three contacts, and the next action: Owen Pruitt books the first discovery call with Ruth Ellery. The board chair is the open question for that call.

```text
Hand-off (read by 06):
account: Brackhaven Memorial Gardens (TARGET at the time of the snapshot)
run_date: 2026-05-06 (illustrative, the week of the qualification)
account_status: TARGET
verdict: GREENLIGHT
zone_scores: 1 HIGH, 2 MEDIUM, 3 MEDIUM, 4 MEDIUM, 5 HIGH (illustrative)
contact_priority: 1 Ruth Ellery (General Manager, buyer), 2 Walt Okonkwo (Operations Director, influencer), 3 Priscilla Dunmore (pre-need manager, end user)
pain_hypotheses: 1 Plot records on paper across two sites (HIGH, CRM and Inferred), 2 The Oldgate renewal in March 2027 (MEDIUM, CRM and Inferred)
sequence: three emails to Ruth Ellery, Emails 2 and 3 omitted for length
report_path: none (inline)
next_action: Owen Pruitt books the first discovery call with Ruth Ellery (date set on the call)
```

---

## Common Patterns

### Pattern: Rapid-Fire Batch Mode
**When:** A BDR needs snapshots for five to ten accounts in one prospecting block.
**Approach:** Run Steps 1 to 4 for each account, produce the ranked table, then write full sequences for the top two or three. See Example 3.

### Pattern: Active Deal Guard (BDR)
**When:** The user is a BDR and the account has an open AE deal.
**Action:** Show the deal in the summary, and recommend sharing the research with the AE instead of sending independent emails.

### Pattern: Quick Call Prep Only
**When:** The user says "quick call prep" or "calling in five minutes."
**Approach:** Skip the sequence. Deliver Steps 1 to 4 and Step 6. See Example 2.

### Pattern: Snapshot Reveals a Trigger Event
**When:** Research turns up a recent event such as an acquisition, an expansion or a leadership change.
**Action:** Note the trigger in the summary, and recommend Trigger Event Outbound (04), which runs on the trigger's own window.

### Pattern: Snapshot Reveals a Known Incumbent
**When:** The CRM or the research names a specific competing product.
**Action:** Note the incumbent in the summary, and recommend Competitive Displacement (12) for the competitive sequence.

---

## Troubleshooting

### "No CRM data available"
**Likely cause:** The CRM record is missing, or the rep has no access.
**Response:** Proceed with public research only. Write "No existing CRM record" in the output. Tag every fact `[Public: source]`, `[Inferred]` or `[Unknown]`. Recommend CRM enrichment as the first action.

### "No contacts found for the target personas"
**Likely cause:** The CRM holds no contacts for those personas.
**Response:** Look for likely contacts through public sources. Write each persona gap as "Unknown, no contact found." Make contact discovery the first action. Personalize emails by title until a name is found.

### "The company spans more than one segment"
**Likely cause:** A company with a secondary division.
**Response:** Classify the account by its primary business, and score the zones on that segment. Note the secondary division as an opportunity, not as a second verdict.

### "The account is a previous customer that churned"
**Likely cause:** The account was lost after it bought.
**Response:** Flag it as a risk, and read the churn reason from the CRM. If the reason was fixed, outreach may still fit. Consider Closed-Loss Reactivation (05), which is built for this case.

### "Research turns up almost nothing on the company"
**Likely cause:** Small private companies often publish little.
**Response:** Work with what the CRM and the company's own website show. Tag everything `[Public: source]`, `[Inferred]` or `[Unknown]`. Produce a lean snapshot with two or three pain hypotheses, and let the discovery call be the main research.

### "Should I prospect if the verdict is MANUAL REVIEW?"
**Likely cause:** The Verdict Rule found one HIGH zone, or a must-have zone at LOW.
**Response:** Find which zones are the gap. If the gap is data, such as an UNKNOWN zone, prioritize the discovery questions that fill it. If the gap is fit, such as a must-have at LOW, deprioritize the account in favor of GREENLIGHT accounts.

### "A zone is UNKNOWN and the verdict is close"
**Likely cause:** The record is silent on that zone.
**Response:** Do not score it. Name it in the summary as the question that would decide the verdict, and say which way the verdict moves if the answer is HIGH or LOW.

---

## Best Practices

- **Prioritize speed.** This skill is built for volume prospecting. Past ten minutes on one account, switch to Research Outbound (03).
- **Use the CRM first.** It is the record a manager can check, and it is faster than web research alone.
- **Match proof points to the segment.** A prospect in one vertical does not care about a result from another.
- **Tag every fact.** The six tags are the only labels, and a reader checks the report by tag.
- **Rank pain hypotheses by confidence.** HIGH-confidence hypotheses lead the outreach.
- **Name the persona gaps.** Knowing who is unknown is as useful as knowing who exists.

---

## Integration With Other Skills

**Reads from the skill before it:**
- **`gtm-account-qualification`** (01). Reads `verdict`, `zone_scores`, `icp_match` and `fit_narrative`. When `zone_scores` arrive, use them instead of scoring the zones again, and say so. When they are absent, score the zones from the profile and say that the scores are new.
- **`gtm-competitive-displacement`** (12). Reads `incumbent_type`, `displacement_difficulty`, `target_personas` and `sequence`. Use `target_personas` to order the contacts, and use `incumbent_type` in the competitive objections. Do not write a snapshot sequence for a persona that already has a displacement `sequence`.

**Hands to the skills after it:**
- **`gtm-research-outbound`** (03), **`gtm-trigger-event-outbound`** (04) and **`gtm-meeting-prep`** (06). Each receives `account_status`, `verdict`, `contact_priority`, `pain_hypotheses` and `sequence`. The receiving skill reads these names as written.

**Hands to the close:**
- **Wrap-Up** reads `report_path` when a file was written, the `verdict`, and `next_action` with its owner and date.

### Chains

- **Qualify To Book:** Account Qualification (01), then Account Snapshot (02, this skill, second), then Research Outbound (03) or Trigger Event Outbound (04), then Meeting Prep (06). This skill turns the verdict into the one-page brief, the ranked contacts, the pain hypotheses and the first sequence.
- **Beat The Incumbent:** Competitive Strategy (11) and Competitive Displacement (12) come first, then this skill (02, last in the chain) or Meeting Prep (06). This skill sets the contact order and the incumbent objections on one page, using the incumbent type from 12.

### Guild Pro Kits (Optional)

The Business Case & ROI Kit (a paid Guild Pro kit) reads this skill's hand-off block by field name. This skill is free and works without any kit. The kit reads these five fields, with `contact_priority` as the economic buyer candidates and each pain hypothesis as a candidate value driver graded assumed until a buyer fact arrives:

- `account`
- `run_date`
- `verdict`
- `contact_priority`
- `pain_hypotheses`

---

## Changelog


### 2.1.0 (2026-10-25)
- Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection and a Guild Pro Kits subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### Version 2.0.0 (2026-10-20)
- Verdict now comes from the profile's Qualification Zones and Verdict Rule, applied as written, with zone scores beside it. The five-signal quick-score stays as the one-glance read and no longer sets the verdict.
- Region map uses the profile's own tiers, with a source per tier.
- Proof points come only from the profile's Proof Points table, one per email. Illustrative results are never cited in an email.
- Evidence labels replaced by the six shared tags.
- Epistemic Rules gain the n rule and the five-case rule. Silence is not a no.
- Hard Rules with reasons replace the Don'ts. The Quality Bar is now a checklist.
- Hand-off fields named in the Output Contract, the Integration section and each example's hand-off block.
- Examples aligned to the PlotIQ chain file. Sable Fork carries its chain zone scores. Quill Hollow shows why Zone 1 stays MEDIUM. A flagship snapshot for Brackhaven is added as the first account in the chain.
- The old output-format section is folded into the Output Contract's file option, which is Markdown only and written on request.

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, with the tier wording made vertical-neutral.

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around a single case study. Em dashes removed from prose.

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy. Company-specific data moved to the shared profile. Framework machinery moved to an explicit Methodology section.

### Version 1.0.0 (2026-03-04)
- Initial release, with the profile-driven design and the batch and quick call prep patterns.
