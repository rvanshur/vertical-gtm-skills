---
name: gtm-research-outbound
version: 2.1.1
description: "Builds a sourced point of view and outbound package from a public filing, an owner letter or an earnings call, with an ICP verdict, a signal map, a sourced wedge and persona sequences, for the rep and the meeting-prep skill to read"
category: Sales-Methodology
author: Ryan Vanshur
license: MIT
updated: 2026-10-25
tags: [research-outbound, 10k-analysis, earnings-call, private-company, pov-brief, enterprise-prospecting, persona-sequences]
requires:
  skills: [gtm-account-snapshot]
mutating: read-write
change_log:
  - version: 2.1.1
    date: 2026-10-25
    summary: "Adds examples/try-it.md so a first run reproduces Example 1. No other change."
  - version: 2.1.0
    date: 2026-10-25
    summary: "Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section, and adds a Chains subsection that places the skill in Qualify To Book. No other change."
  - version: 2.0.1
    date: 2026-10-20
    summary: "Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change."
  - version: 2.0.0
    date: 2026-10-20
    summary: "Industry Context is read from the profile as a sourced list. Proof points are named only from the profile and only when Verified or Benchmark. The persona count comes from Buyer Personas, so the email count is personas times steps, with no fixed count. Step 7 reads the Persona who acts column. Zones and the verdict come from the profile. The six evidence tags replace the old labels. A filing-mode example ends in DISQUALIFY with zero emails. Hand-off fields are named in the Output Contract and in Integration. The report is inline, and a Markdown file is written only when asked."
  - version: 1.3.0
    date: 2026-10-13
    summary: "Examples re-cast on the PlotIQ cast, a non-success example added, and the persona count corrected to 5."
---

# Research-Driven Outbound

## Overview

Research Outbound takes one account and reads what it published, whether that is a public filing, an owner letter or an earnings call. It turns the reading into a point of view a rep can defend. The output is an ICP verdict with every zone's score beside it, a signal map, a wedge with its arithmetic shown, a point of view brief, and a persona sequence for each buyer the profile names. It is built for enterprise accounts where the depth is worth the time.

Everything the skill produces is a draft. The rep reads it and decides what to send. The point of view brief and the persona emails also go to the meeting-prep skill, so the first call starts from the same facts the outreach used.

**Core Principle:** A point of view built from what the account published, with every quote real and every number sourced.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

Outbound built on a company's own words usually fails in one of two ways. A line gets quoted that the company never wrote, or a figure gets used that nobody can trace. The prospect's finance team can open the filing or the letter in a minute, and one wrong line costs the rep the buyer and the rest of the sequence with it. The second failure is sending every persona the same story. This skill stops both. Quotes come only from the source, every fact carries its evidence tag, and each persona gets a message tied to the part of the account that person owns. No outside figure appears in this file, because the rule here is that a figure needs a named, dated source.

---

## Role

You are a senior enterprise researcher and point of view writer for a vertical SaaS company. You read what an account published, pull out the facts that connect to the product, quantify a wedge only when the sources support the numbers, and write persona sequences built on specifics. You do not write templates. Everything company-specific comes from the profile named in Context, so the same skill serves any vertical without changes.

You refuse four things. You do not quote a passage the source does not contain. You do not send anything or write to the CRM. You do not work an ACTIVE account that has an AE owner unless that AE has said yes. You do not name an Illustrative proof point in an email a prospect will read. Each refusal has its reason in Hard Rules.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

To try the skill without your own data, use `examples/try-it.md`, which holds the inputs for Example 1.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | Required | The account to research. Matched to its CRM record when there is one |
| Research source | Required | The filing, owner letter, earnings call transcript or news item, and where it is: a pasted passage, a link or a file. The source sets the mode (see Modes) |
| User role | Required, from the CRM | BDR or AE. If the CRM does not say, ask: "Are you a BDR or AE?" |
| Personas to target | Optional | Defaults to every persona in the profile's Buyer Personas that applies to this account type |
| CRM access | Optional | Status, owner and open-deal stage. Without it, ask the user for the account status |

---

## Output Contract

Every run returns its report in the chat, in the sections below, in this order. The layout does not change between accounts. The content does. A file is written only when the user asks for one.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| `verdict` | Chat, Verdict section | GREENLIGHT, MANUAL REVIEW or DISQUALIFY, from the profile's Verdict Rule as written |
| `zone_scores` | Chat, Verdict section, beside the verdict | One line per zone: HIGH, MEDIUM or LOW, or `[Unknown]` where the sources do not speak to the zone. Not handed on. Shown so the reader can see why the verdict landed where it did |
| `signal_map` | Chat, Signal Map section | Six to ten rows, each tagged and placed in one zone. Handed to 06 |
| `wedge` | Chat, Wedge section | The figure, its arithmetic and its tags. Or "Insufficient data", with the missing figure named. Handed to 06 |
| `pov_brief` | Chat, POV Brief section | Under 500 words, in the five parts of Step 6. Handed to 06 |
| `persona_emails` | Chat, Persona Sequences section | The count shown as personas times steps, then each sequence. Handed to 06 |
| Cheatsheet | Chat, Cheatsheet section | The eight sections for the research type, in the order set in Methodology |
| Intelligence appendix | Chat, Appendix section | The top eight items, each tagged, and two to four research gaps |
| `report_path` | Set only when a file was written | Empty when the report is inline |
| `next_action` | Chat, last line | One step, with its owner and a date. Read by Wrap-Up |
| Markdown file, on request | The account notes folder | Named `<account>_research-outbound_<date>.md`. Written only when the user asks for it |

---

## Context

**This skill does not contain company-specific information. It points to it.**

Read the profile, `profiles/client-profile.md`, which is written from `profiles/client-profile-template.md`. The sections below are the only ones this skill reads. The skill carries no company fact of its own.

| Profile section | Used for |
|---|---|
| Industry Context | The sourced industry facts, the number the account moves, the vertical financial signals and the private-company sources. Also read by Trigger Event Outbound (04) and Closed-Loss Reactivation (05) |
| ICP Definitions | The ICP the account is scored against, and the market segments |
| Qualification Zones | The five zones, each scored HIGH, MEDIUM or LOW, and the Verdict Rule |
| Qualification Criteria | The disqualifiers, and the Buying Triggers table, including its Persona who acts column |
| Buyer Personas | The personas to write to, which set the number of sequences |
| Value Propositions | Connecting each signal to a product capability |
| Proof Points | Which proof point may be named, by its Status: Verified, Benchmark or Illustrative |
| Competitive Landscape | Incumbent and objection context |
| Knowledge Base | The Location field of the base, and the base items this skill opens: the account's folder under `accounts/` (notes, calls, decisions for that account), read in Step 1 as tagged facts |

`{Profile: X}` means section X of the profile. `{Methodology: X}` means subsection X of the Methodology section below.

If the Industry Context section is missing, the skill says so once at the start, runs uncustomized, and marks every output that depended on that section. Run the interview in `CUSTOMIZE.md` to write it.

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

Your research frameworks and evidence standards. The structures below are the skill's defaults. Use them as they are unless the profile names a different frame.

### Research Type Selection

The source decides the mode. Each mode sets how much is written.

| Research Type | Best For | Sequence Depth | Word Limit | Relevance Window |
|--------------|---------|----------------|------------|-----------------|
| **10-K Filing** | Public companies. Annual deep-dive | Every applicable persona x 4 emails | 120 words or fewer | Months |
| **Private Company** | Private companies, owner letters, news, multi-source research | Every applicable persona x 4 emails | 120 words or fewer | Months |
| **Earnings Call** | Public companies. Quarterly signals | 2 to 3 personas x 2 emails (4 to 6 in total) | 100 words or fewer | 7 to 14 days |

### Revenue Estimation Methods

Use these when a private company gives no revenue figure. Each estimate is tagged with the method that produced it, so the reader can recompute it.

| Method | Formula | Tag |
|--------|---------|-----|
| Employee benchmark | Employees x a per-employee rate | `[Inferred: employee benchmark]` |
| Branch count proxy | Branches x a per-branch rate | `[Inferred: branch proxy]` |
| Industry ranking | Cross-reference a published industry list | `[Public: name of the list, year]` |
| PE acquisition press | Revenue language in the announcement | `[Public: name of the announcement, date]` |

A per-employee or per-branch rate needs a named, dated source. Without one, the estimate is `[Unknown]`. When methods disagree, report the range from each method and name the spread.

### Cheatsheet Layout

The cheatsheet is the one-page summary a rep reads before a call. It always has eight sections, in this order.

**For a 10-K filing or a private company:**

1. Company Snapshot: key facts from the intelligence profile
2. Geographic or Market Exposure: regions mapped to the profile's market tiers
3. Key Personas: the contacts on file, and which persona each one is
4. Pain Points and Signals: six hooks from the signal map, written as talk tracks
5. Discovery Questions: grouped by persona, grounded in the sources
6. Value Props: the wedge and the proof points that match the profile
7. Objection Handling: CRM notes and the common objections for this segment
8. Call Flow: a five-step talk track built on the research above

**For an earnings call:**

1. Earnings Snapshot: quarter, revenue, key metrics and the relevance window
2. Top Signals: ranked by urgency, with the speaker named
3. Key Personas: the contacts on file who match the signal
4. Earnings Hooks: six talk-track-ready signal hooks
5. Discovery Questions: grounded in the earnings call, not generic
6. Value Props: the wedge matched to the signal
7. Objection Handling: rebuttals that account for the earnings context
8. Call Flow: an earnings-led five-step talk track

An earnings package puts a timeliness banner at the top, showing the days since the call.

---

## Quick Reference

**Use this skill when:**
- Prospecting a high-value enterprise account that has a public filing, an owner letter or a recent earnings call
- Researching a private company for strategic outbound, where the sources are published
- Acting on a quarterly earnings call while its signals are still fresh
- A persona-tailored sequence needs to rest on the account's own published words

**Don't use when:**
- You need a quick snapshot for volume prospecting (use `gtm-account-snapshot`)
- The account has a known incumbent and the question is displacement (use `gtm-competitive-displacement`)
- A trigger event just happened (use `gtm-trigger-event-outbound`)
- The account is LOST (use `gtm-closed-loss-reactivation`)
- The account is ACTIVE with an AE owner and the AE has not said yes (the guard fires, and the skill writes only a coordination note)

**User roles:** BDR, AE
**Expected time:** 20 to 45 minutes per account

---

## Core Workflow

Each step ends with what it produces. The order matters at three points. The role check comes first because the guard in Step 1 depends on it. The verdict comes before the wedge and the sequences, so a disqualified account never gets either. The signal map comes after the zone scores, so the map cannot disagree with the verdict.

### Step 0: Detect the User Role

Determine whether the user is a BDR or an AE, from the CRM's user role or profile. If the CRM does not say, ask: "Are you a BDR or AE?"

Role-aware framing:
- **BDR:** calls to action are framed as booking a meeting. If an AE deal is active, the output goes to the AE, not to the buyer.
- **AE:** calls to action are framed as advancing the deal. The intelligence deepens the AE's engagement.

**Produces:** `user_role` (BDR or AE), and the one question asked if the CRM was silent.

### Step 1: Gather the Inputs and Check the CRM

Before pulling anything, open the account's folder under `accounts/` in the Knowledge Base, if the profile has one, and offer the CRM read and, when a call recorder is connected, the call read, for the one account or date range you name. Nothing is read from the CRM or the call recorder until you say yes.

#### 1a. Confirm the Inputs by Source

- **10-K filing:** company name and ticker, fiscal year, filing date, and the filing text or its key sections
- **Private company (owner letter, company site, news):** company name, the letter or page with its date, and anything known about headquarters, size and ownership
- **Earnings call:** company name and ticker, quarter, call date, and the transcript or its key sections

#### 1b. Check the Account Status and the Guard

Read the account's status and owner from the CRM. Without a CRM, read it from the profile's example cast. Then apply the guard for the case that matches:

- **ACTIVE with an AE owner, and the user is a BDR:** the guard fires. Write one coordination note for the AE, with the intelligence the AE can use, and stop. Write no POV brief and no sequences. Run the rest of the workflow only after the AE has said yes.
- **Pending AE assignment:** the account is not ACTIVE. Work it, and say in the output that it is pending.
- **OUT:** a disqualifier applies in the profile. Carry the account to Step 3, where the verdict ends the run.
- **LOST:** stop, and name `gtm-closed-loss-reactivation` as the right skill.

**Produces:** the source, the status word, and the guard result (fired, not fired, or pending). This runs before any research, because the guard decides whether research happens at all.

### Step 2: Build the Sourced Intelligence Profile

Only tagged facts enter the profile. Industry claims come only from the profile's Industry Context section, and each one keeps its own source and year. An industry claim with no source there is dropped.

#### For 10-K Filings: Fact Bank

Scan the required sections: Items 1, 1A, 3, 7 and 9A. Record each fact with its location:

```
- Fact in plain words, tag [Public: 10-K, Item X, PDF p. ##]
```

#### For Private Companies: Sourced Intelligence Profile

Research every available source:

| Source | What to Look For |
|--------|-----------------|
| Company website | About, leadership, locations, services, history, careers |
| News and press releases | Acquisitions, expansions, hires, awards, milestones |
| Job postings | Roles that point to the pain the product solves |
| Industry databases | Rankings, trade association memberships |
| Ownership and M&A signals | Ownership structure, recent acquisitions |
| Regulatory and licensing records | Active licenses by region, which show the footprint |
| Owner letters and annual letters | Dated plans, such as a systems move or a growth project |

Tag every fact with one of the six evidence tags. `[Public: source, date]` marks a published page, filing, letter or article, with its source named. `[CRM]` marks a CRM field or note. `[Call]` marks something said on a dated call, with the call date. `[Notes]` marks a rep's written notes. `[Inferred: method]` marks a conclusion reasoned from other facts, with the method named. `[Unknown]` marks a fact that is not known. A fact with no tag is removed.

#### For Earnings Calls: Signal Extraction

The transcript is public, so its quotes are tagged `[Public: earnings call transcript, date]`. Scan the full transcript for the priority signals:

| Signal Category | What to Look For | Product Connection |
|----------------|-----------------|-------------------|
| Working Capital | DSO, receivables trends, cash conversion | The profile's relevant value proposition |
| Bad Debt or Credit Loss | Allowance changes, write-offs, collections | The profile's relevant value proposition |
| Operational Efficiency | Headcount, SG&A optimization | The profile's relevant value proposition |
| Growth or Expansion | New markets, acquisitions, organic growth | The profile's relevant value proposition |
| M&A Activity | Acquisitions, integration commentary | The profile's relevant value proposition |
| Systems | Technology investments, consolidation | The profile's relevant value proposition |
| Margin Pressure | Gross margin, cost inflation | The profile's relevant value proposition |
| Guidance Changes | Lowered outlook, revised targets | The profile's relevant value proposition |

Extract six to ten signals, ranked by urgency, in this format:

```
- Signal: [category]
- Quote or paraphrase: "[what was said]"
- Speaker: [name, title]
- Section: [prepared remarks or Q&A]
- Product connection: [how this connects to the value proposition]
- Urgency: [High, Medium or Low]
- Tag: [Public: earnings call transcript, date]
```

**Produces:** the intelligence profile, with every fact tagged and every industry claim sourced from Industry Context.

### Step 3: Score the Zones and Apply the Verdict

Score each of the profile's five zones HIGH, MEDIUM or LOW, from observable facts. Apply the profile's Verdict Rule as written, so the verdict is GREENLIGHT, MANUAL REVIEW or DISQUALIFY. Show every zone's score beside the verdict, and name any must-have zone that scored LOW in the reason.

Three rules apply here. MEDIUM never counts as HIGH. A zone the sources do not speak to is `[Unknown]`, not LOW, because silence is not a no. A zone scored on a checked absence (a search that was run and found nothing, for example) is scored, and the check is named so a reader can repeat it.

The reasons for the verdict go in three to six bullets, each with its tag.

**Produces:** every zone's score, the verdict, and its reasons. A DISQUALIFY ends the run here. No wedge and no sequence follow it.

### Step 4: Map the Signals to the Zones

Place each signal or fact from Step 2 against the zone it bears on. Build the table with six to ten rows:

| Intelligence Signal | Why It Matters | Qualification Zone | Value Prop | Discovery Question | Source |
|---------------------|---------------|-------------------|-----------|-------------------|--------|

Each row has one tag in the Source column. Each Discovery Question is something the rep can ask on a call, grounded in the source and not generic.

**Produces:** the signal map, six to ten rows, each tagged and placed in a zone. It comes after Step 3 so the zone column matches the scores already given.

### Step 5: Build the Quantified Wedge

Build a wedge only when the sources support the numbers. Show every calculation, one line per step, so the reader can recompute it.

| Data Available | Calculation | Tag |
|---------------|-------------|-----|
| A figure from a filing or public page | Cite it, and show any arithmetic on it | `[Public: source, date]` |
| A profile price or rate | Units x the profile figure, with the arithmetic shown | `[Inferred: units x profile list price]` |
| A profile Benchmark | Cite the benchmark with its source and date. It is a hook, not a result | `[Public: source, date]` |
| A figure the sources lack | Write it as unknown, and name it as a discovery question | `[Unknown]` |

Never claim savings as a guarantee. Frame the result as what companies of a similar size typically see, and name the source for that claim.

**Produces:** the wedge as a sentence with its arithmetic, or "Insufficient data" with the missing figure named.

### Step 6: Write the POV Brief

Keep the brief under 500 words, skimmable, with every claim tagged.

1. **Company Context** (2 to 3 bullets): what the company does, its segment, ownership and footprint
2. **Why They Should Care** (3 to 5 bullets): how the profile connects to the product's value
3. **Risks and Complexity Signals** (3 to 5 bullets): multi-site exposure, manual processes, growth strain
4. **Fit Verdict:** the verdict word, with its reasons from Step 3
5. **POV Statement** (6 to 8 sentences): lead with the most notable fact, connect it to the complexity, state the wedge and the value proposition, and close with one ask

**Produces:** the POV brief, under 500 words, with the verdict stated.

### Step 7: Generate the Persona Sequences

**Count first.** The persona count comes from the profile's Buyer Personas. Count the personas that apply to this account type, because the profile marks some personas for groups only. Multiply by the steps for the mode. In a filing or private package, that is personas x 4. For a profile with five personas, a multi-location group gets 20 emails. A single site drops the group-only persona and gets 16. The count is never fixed.

**Route the trigger.** Match the source's signal to a row in the profile's Buying Triggers table. The row's Persona who acts column names the person who has to respond. That persona's sequence is listed first, and its Email 1 is the one the rep sends first. A trigger sequence goes to the person who must act on the event, not to every persona.

| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | Point of view and wedge | The most specific fact from the source |
| **Email 2** | Complexity or risk | A different anchor: geographic, integration or operational |
| **Email 3** | Process or efficiency | An industry trend or operational pain hypothesis |
| **Email 4** | Breakup and validation | A soft close with one specific question |

Rules for every email: 120 words or fewer (100 for an earnings call). A different intelligence anchor in each email, so no signal repeats within a persona's sequence. A citation in the first line. At most one proof point, and only one whose Status in the profile is Verified or Benchmark. An Illustrative proof point is never named in an email, because the prospect reads it and it is not a real result.

Earnings sequences draw two to three personas from the trigger row, with two emails each, and the subject line names the earnings event.

After each persona's sequence, include the persona's hook focus (one line) and that persona's two best discovery questions, grounded in the source.

**Produces:** the persona sequences, with the count shown as "N personas x M emails = total", and the trigger routing named.

### Step 8: Build the Intelligence Appendix

List the top eight intelligence items, each as a finding with its tag. Then list two to four research gaps: unknowns that would strengthen the outreach if they were found.

**Produces:** eight tagged findings and two to four gaps, each gap written as a question the rep could answer on a call.

### Step 9: Write the Summary and Hand Off

Write the summary as one numbered list, in this order:

1. Company: name, headquarters, ownership, revenue, segment
2. Research type: 10-K filing, private company or earnings call
3. Verdict and zones: the verdict word, the zone scores and the top three reasons
4. Quantified wedge: the strongest figure, or "Insufficient data"
5. CRM status: pipeline activity and known contacts
6. Geographic exposure: regions mapped to the profile's tiers (filing and private only)
7. Relevance window: days remaining (earnings only)
8. Sequences: the persona count, times the steps, equals the total
9. Personalized contacts: which emails address a known person
10. Strongest entry point: the persona and the email with the highest-impact opening
11. User role: BDR or AE
12. Coordination note: the guard result, if it fired
13. Research gaps: the top three unknowns

Then write the cheatsheet, then the hand-off block, which lists the fields from Output Contract by name, and the `next_action` line with its owner and date.

**Produces:** the summary, the cheatsheet, the hand-off block, and the next action with owner and date.

---

## Modes

The source decides the mode. The default when the source is ambiguous is Private Company, because the owner letters, company pages and news that make up most enterprise research in this profile are private-company sources.

- **10-K Filing mode:** the source is a public company's annual filing. Build the Fact Bank from Items 1, 1A, 3, 7 and 9A. The filing also states the systems the company runs, so this is where a consolidator that runs its own system is found. That finding ends the run as DISQUALIFY.
- **Private Company mode (default):** the source is an owner letter, company page, news item or licensing record. The sequences run every applicable persona for four steps.
- **Earnings Call mode:** the source is a quarterly transcript. The relevance window is 7 to 14 days, so the timeliness banner shows the days since the call.

No mode writes a file on its own. A file is written only when the user asks for one, and then it is named as the Output Contract says.

---

## Epistemic Rules

- **n beside every rate.** Write "3 of 5 zones HIGH", never a bare ratio or a bare figure with no count behind it. A count with no n is not a finding.
- **Five cases before a pattern.** A claim that a pattern holds across signals or personas needs five matching cases. Fewer is an observation, and it is labelled as one with its n, such as "observation, n=3".
- **Silence is not a no.** A zone or a signal the sources do not speak to is `[Unknown]`, and it is counted in no denominator. Blank is unknown, never negative.
- **"No difference found" is a finding.** When a comparison shows nothing, report that. It stops a weak angle from becoming a playbook.
- **Unsourced facts are dropped.** An industry claim with no source in the Industry Context section is removed, not kept with a caveat.

---

## Hard Rules

1. **Never quote a passage the source does not contain.** The prospect can open the filing or the letter, and one invented line costs the rep the buyer. Copy each quote from the source and give its location.
2. **Never send, enroll a contact or write to the CRM.** The rep owns the send and the record. The skill drafts, and the rep reads before anything leaves.
3. **Never work an ACTIVE account with an AE owner unless that AE has said yes.** Two people writing to one buyer costs the deal, and the AE's conversation is the one at risk.
4. **Never name an Illustrative proof point in an email or a talk track.** The prospect reads it, and an illustrative result is not a real result. Only Verified or Benchmark proof points are named.
5. **Never score a zone LOW from silence.** A blank is unknown. Scoring it LOW turns a gap into a no, and the verdict then rests on something nobody checked.
6. **Never write a wedge or a sequence for a DISQUALIFY.** The verdict is the gate. A sequence to a disqualified account spends the rep's first touch on an account that cannot buy.
7. **Never use a fixed persona count.** The count comes from the profile's Buyer Personas, so a profile with three personas does not produce twenty emails. A fixed count invents work the profile does not support.
8. **Never claim savings as a guarantee.** Use typical outcomes with a named source. A guaranteed figure is a promise the company cannot keep, and the buyer's finance team will ask for the proof.
9. **Use only the six evidence tags.** The next skill grades every fact by its tag, and a label outside the set cannot be read.
10. **Write no file unless the user asks.** The report is for the rep to read in the chat. A file that nobody asked for is one more thing to find and delete later.

---

## Quality Bar

**Done when all are true:**

- [ ] Every fact carries one of the six evidence tags, and no fact is untagged
- [ ] Every quote appears in the source, with its location
- [ ] Every zone is scored or marked `[Unknown]`, and the verdict follows the profile's Verdict Rule as written
- [ ] The email count equals the applicable personas times the steps for the mode, and the count is shown
- [ ] No Illustrative proof point appears in any email or talk track
- [ ] The guard result is in the output, and an ACTIVE account with an AE owner has either the AE's yes or no sequences
- [ ] Every rate carries its n
- [ ] Every wedge figure shows its arithmetic, or the output says "Insufficient data"
- [ ] Every email is within its word limit (120 for filing and private, 100 for earnings)
- [ ] The hand-off block lists `pov_brief`, `signal_map`, `wedge`, `persona_emails`, `report_path` and `next_action` by name
- [ ] No file was written unless the user asked for one

---

## Examples

All examples use PlotIQ and its cast from the profile's Example Cast. Every figure is in the profile or marked `(illustrative)`. Each example ends with the hand-off block to the meeting-prep skill.

### Example 1: Private Company Research (Saltmarsh Heritage Group, MANUAL REVIEW)

**Context:** Research outbound to Saltmarsh Heritage Group, a family-owned group with 5 sites (2 cemeteries, 3 funeral homes) and no public filing. Its annual owner letter, posted on the company site, says all five sites move to one system in 2027. The CFO, Hector Ruiz, approves budget. This is the one account in the cast whose research starts from an owner letter. The status is TARGET, so the guard does not fire. The user is Nadia Brandt, BDR.

**Input:** "Build a research outbound package for Saltmarsh Heritage Group from its owner letter, with sequences and the summary."

**Process:**

- **Steps 0 and 1:** BDR. Status TARGET, no open deal, no AE owner. Mode: Private Company, because the source is a company-site letter.
- **Step 2, the sourced profile:**
  - All five sites move to one system in 2027. `[Public: company site, owner letter 2026]`
  - Five sites: 2 cemeteries and 3 funeral homes. `[CRM]`
  - Three funeral homes run pre-need counselors. `[CRM]`
  - The group is family owned. `[CRM]`
  - The CFO, Hector Ruiz, approves budget. `[CRM]`
  - Which system, and when the plot records move: `[Unknown]`
- **Step 3, the zones and the verdict.** ICP3 Multi-Location Group, four to ten sites. The five zones from the profile:

| Zone | Score | Basis |
|---|---|---|
| 1 Records and Inventory Pain | MEDIUM | The plot records method is `[Unknown]`, so the middle score stands until a call says otherwise |
| 2 Pre-Need Sales Motion | HIGH | Pre-need counselors at three funeral homes `[CRM]` |
| 3 Ownership and Decision Speed | LOW | The CFO approves budget `[CRM]`, and the profile's ICP3 cycle runs 6 to 9 months. A must-have zone |
| 4 Technology Readiness | MEDIUM | The current system is `[Unknown]`, so the middle score stands |
| 5 Growth or Succession | HIGH | The owner letter names a systems move for 2027 `[Public: company site, owner letter 2026]` |

**MANUAL REVIEW.** Two zones are HIGH (2 and 5), but a must-have zone (3) is LOW, so GREENLIGHT is out. No disqualifier applies and only one must-have is LOW, so DISQUALIFY is out too. The open items are the CFO gate and the 6 to 9 month cycle.

- **Step 4, the signal map:**

| Intelligence Signal | Why It Matters | Zone | Value Prop | Discovery Question | Source |
|---|---|---|---|---|---|
| One system across five sites in 2027 | A dated systems project is open | 5 HIGH | One records system for every site | Which plot records and pre-need leads move first? | `[Public: company site, owner letter 2026]` |
| Pre-need counselors at three funeral homes | Pre-need leads need somewhere to land | 2 HIGH | Pre-need leads that get a call back | Where do pre-need leads land today? | `[CRM]` |
| Two cemetery sites | Plot records are the first pain | 1 MEDIUM | Find the unsold plots | Where does a plot lookup start on each cemetery site? | `[CRM]` |
| CFO approves budget | The decision sits at a CFO gate | 3 LOW | Trust compliance across every site | What does the CFO need to see before a system move is approved? | `[CRM]` |
| Current system not known | Sets how hard the move will be | 4 MEDIUM | A migration plan the sites can staff | Which system do the sites use day to day? | `[Unknown]` |
| Family owned and owner-led | The owner letter is the family's own plan | 5 HIGH | A growth story the owner can carry | Who in the family signs off on the 2027 move? | `[Public: company site, owner letter 2026]` |

- **Step 5, the wedge.** Two cemetery sites x 50 to 100 plots each = 100 to 200 plots to check. The 50 to 100 is the profile's first-call hook, a Benchmark `[Public: deathcare research, 2026-03-27 to 2026-04-01]`. It is a hook, not a result. Five sites x $10,788 a year at list = $53,940 a year, plus $5,000 setup once `[Inferred: units x profile list price]`. The price of an unsold plot is `[Unknown]`, so no payback figure is written. The first discovery question asks for it.
- **Step 6, the POV statement** (six sentences): Five sites under one family owner are moving to one system, and the first question is records, not software. Two cemeteries carry plot records, and the first-call hook is 50 to 100 plots per cemetery site `[Public: deathcare research, 2026-03-27 to 2026-04-01]`. Three funeral homes already generate pre-need leads, so the same system has to reach the sales side. The CFO is the gate, and the cycle runs 6 to 9 months. The point of view: one system across five sites in 2027 is a records project before it is a software project, and the group can start with the cemetery plots. The ask: 20 minutes to map which records and leads move first.
- **Step 7, the sequences.** Five personas apply, because Saltmarsh is a group and the profile marks the CFO persona for groups. Five personas x 4 steps = 20 emails. The owner-letter trigger's Persona who acts column reads "CFO or Controller in a group", so the CFO's sequence is listed first. Email 1 to the CFO:

> **Subject:** One system across five sites in 2027
>
> Hector,
>
> Your owner letter says all five Saltmarsh sites move to one system in 2027. Two cemeteries and three funeral homes on one system is a records question before it is a software question. Which plot records and pre-need leads move first?
>
> Your pre-need counselors at three funeral homes already generate leads. Where do those leads land today?
>
> Worth 20 minutes to map it before the move?

- **Steps 8 and 9.** Research gap: which system the group picks, and when the records move.

**Output:** Intelligence profile with tags. Point of view brief built on the single-system plan. Twenty persona emails, with Email 1 to the CFO shown above. Verdict MANUAL REVIEW.

```text
Hand-off (read by 06):
account: Saltmarsh Heritage Group (TARGET)
run_date: 2026-10-19
pov_brief: POV statement, one system across five sites in 2027 as a records project first, verdict MANUAL REVIEW stated
signal_map: six rows, each tagged and placed in a zone (table above)
wedge: 2 cemetery sites x 50 to 100 plots = 100 to 200 plots to check (Benchmark, not a result). 5 sites x $10,788 = $53,940 a year at list, plus $5,000 setup once. Plot price unknown, so no payback figure
persona_emails: 20 (5 personas x 4 steps). Email 1 to the CFO shown above
verdict: MANUAL REVIEW
zone_scores: 1 MEDIUM, 2 HIGH, 3 LOW, 4 MEDIUM, 5 HIGH
account_status: TARGET
report_path: none (inline)
next_action: Nadia Brandt reads the 20 drafts and sends Email 1 to Hector Ruiz by 2026-10-23
```

### Example 2: Active Deal Guard (Brackhaven Memorial Gardens)

**Context:** Nadia Brandt, BDR, asks for a research outbound package on Brackhaven Memorial Gardens, a combination with 2 sites and 11,000 plots. The account is ACTIVE at Stage 5 Negotiate, and Owen Pruitt, the AE, owns the deal. Owen has not said yes to any outbound on the account.

**Input:** "Build a research outbound package for Brackhaven Memorial Gardens."

**Step 0: Role detection.** The user is a BDR.

**Step 1b: The guard fires.** "Active deal owned by Owen Pruitt (AE) at Stage 5 Negotiate. Share this analysis with Owen. Do not send sequences independently. This skill writes no POV brief and no sequences for a BDR on this account."

**Intelligence for Owen, not for outbound:**

- Two sites, 11,000 plots, paper plot maps `[CRM]`
- One double sale in the last 24 months `[CRM]` (illustrative)
- Legacy on-premise system from Oldgate, renewal March 2027 `[CRM]`
- Stonemark mapping also evaluated, no preference stated `[Call]`
- The owner retires within 3 years `[CRM]` (illustrative)
- Ruth Ellery, GM, is the champion `[Call]`. Walt Okonkwo, Operations Director, is skeptical of tablets `[CRM]`

**Zones shown beside the verdict:** 1 HIGH, 2 MEDIUM, 3 MEDIUM, 4 MEDIUM, 5 HIGH. **GREENLIGHT**, because two zones are HIGH and no must-have zone is LOW. Zone 3 stays MEDIUM even though the family board meets within 60 days (2026-11-12), because year one with setup, $26,576, is above the $25K board line.

**Output:** A coordination note for Owen. The March 2027 Oldgate renewal is the timing hook. Owen should lead it, because BDR outreach to a deal in Negotiate would cross Owen's conversation with Ruth Ellery. No sequences are written.

```text
Hand-off (read by 06):
account: Brackhaven Memorial Gardens (ACTIVE, Stage 5 Negotiate, AE Owen Pruitt)
run_date: 2026-10-19
pov_brief: none (guard fired, Owen Pruitt owns the deal)
signal_map: none (guard fired)
wedge: none (guard fired)
persona_emails: none (guard fired, 0 emails)
verdict: GREENLIGHT (shown to Owen, not for outbound)
zone_scores: 1 HIGH, 2 MEDIUM, 3 MEDIUM, 4 MEDIUM, 5 HIGH
account_status: ACTIVE, Stage 5 Negotiate
report_path: none (inline)
next_action: Nadia Brandt sends the coordination note to Owen Pruitt by 2026-10-21, and Owen decides what outreach happens
```

### Example 3: Insufficient Intelligence Fallback (Tamsin Vale Cemetery)

**Context:** Research outbound on Tamsin Vale Cemetery, a one-site cemetery with 4,200 plots, paper plat maps and one binder per section. It has two double sales in 2 years `[CRM]` (illustrative). The status is TARGET. The search found no owner letter, no filing and no news. Who signs is `[Unknown]`.

**Input:** "Build a research-driven outbound package for Tamsin Vale Cemetery."

**Process:**

- **Step 2, the sourced profile:** 4,200 plots, paper plat maps and one binder per section `[CRM]`. Two double sales in 2 years `[CRM]` (illustrative). No owner letter, filing or news found `[Unknown]`. The signer is `[Unknown]`.
- **Step 3, the zones:**

| Zone | Score | Basis |
|---|---|---|
| 1 Records and Inventory Pain | HIGH | Paper plat maps, one binder per section, two double sales in 2 years `[CRM]` (illustrative) |
| 2 Pre-Need Sales Motion | LOW | The account's website was checked on 2026-10-19 and has no pre-need intake form `[Public: account website, checked 2026-10-19]` (illustrative). A checked absence, not a blank |
| 3 Ownership and Decision Speed | MEDIUM | Provisional. The signer is `[Unknown]`, so the score rests on the one fact the sources give: one site under one management team (illustrative). The first research action confirms or changes it |
| 4 Technology Readiness | LOW | The search found no website. The search was run and found nothing `[Unknown]` as a complete check, so a site visit or a call can overturn this score |
| 5 Growth or Succession | MEDIUM | Provisional. The search found no new owner, owner update or growth project `[Unknown]`, so the middle score stands until a call says otherwise |

**Verdict: MANUAL REVIEW.** One zone is HIGH, and no must-have zone is LOW enough to disqualify, but one HIGH zone does not reach GREENLIGHT. Do not write a point of view brief from one strong fact.

**Gate:** Insufficient Intelligence Fallback. The output has no point of view brief, no signal map and no sequences, so it has 0 emails.

**Output:** What the sources show, and three research actions: find the signer (Zone 3), confirm the pre-need sales (Zone 2), and check what staff use day to day (Zone 4). Recommend `gtm-account-snapshot` as the faster route to a usable profile.

```text
Hand-off (read by 06):
account: Tamsin Vale Cemetery (TARGET)
run_date: 2026-10-19
pov_brief: none (one HIGH zone is not enough for a point of view)
signal_map: none (three research actions listed instead)
wedge: none (4,200 plots are on file, but the plot price is unknown)
persona_emails: none (0 emails)
verdict: MANUAL REVIEW
zone_scores: 1 HIGH, 2 LOW, 3 MEDIUM, 4 LOW, 5 MEDIUM
account_status: TARGET
report_path: none (inline)
next_action: Nadia Brandt runs gtm-account-snapshot on Tamsin Vale by 2026-10-23 to find the signer
```

### Example 4: Filing Check Ends in DISQUALIFY (Northvale Memorial Holdings)

**Context:** A rep asks for a research outbound package on Northvale Memorial Holdings, a public consolidator with about 240 funeral homes and 90 cemeteries. Its annual filing says it runs its own in-house system `[Public: annual filing]`. The status is OUT, not LOST. OUT means the profile has disqualified the account. A LOST status would mean a closed loss, and there is no loss record here.

**Input:** "Build a research outbound package for Northvale Memorial Holdings from its annual filing."

**Process:**

- **Step 0 and 1:** The user is the rep, who has asked for the package. Status OUT, so the guard does not apply. No AE owns the account.
- **Step 2, the filing (10-K Filing mode):**
  - Public consolidator, about 240 funeral homes and 90 cemeteries `[Public: annual filing]`
  - Runs its own in-house system `[Public: annual filing]`
  - Quoted passage (illustrative, not a quote from a real filing): "All of our funeral homes and cemeteries run on one in-house records platform that we build and maintain." `[Public: annual filing]` (illustrative)

  The passage is an illustrative stand-in. A real run quotes the filing's own words and gives the item and page.
- **Step 3, the zones and the verdict:**

| Zone | Score | Basis |
|---|---|---|
| 1 Records and Inventory Pain | `[Unknown]` | The filing does not describe the plot records. Not weighed |
| 2 Pre-Need Sales Motion | `[Unknown]` | The filing does not speak to pre-need. Not weighed |
| 3 Ownership and Decision Speed | `[Unknown]` | The filing does not name the buying decision. Not weighed |
| 4 Technology Readiness | LOW | The filing says the company runs its own in-house system. The zone's LOW case covers an enterprise system already in place `[Inferred: in-house system]` |
| 5 Growth or Succession | `[Unknown]` | The filing does not speak to succession. Not weighed |

The zones the filing does not speak to are not scored. A blank is unknown, not a no, and the verdict does not need them.

**DISQUALIFY.** The profile's disqualifiers include public or PE-backed consolidators that run their own system. This account is one.

- **Steps 4 to 7:** No signal map, no wedge and no sequences. A disqualified account gets no wedge and 0 emails. The point of the disqualifier is that the company already runs the system PlotIQ would sell into.
- **Step 8:** Research gaps: none that would change the verdict.

**Output:** A plain verdict for the rep: DISQUALIFY, with its disqualifier named and its filing source tagged. The rep is told the reason in one sentence, and no outreach is drafted.

```text
Hand-off (read by 06):
account: Northvale Memorial Holdings (OUT)
run_date: 2026-10-19
pov_brief: none (DISQUALIFY)
signal_map: none (DISQUALIFY, the disqualifier is the only signal)
wedge: not computed (DISQUALIFY)
persona_emails: none (DISQUALIFY, 0 emails)
verdict: DISQUALIFY
zone_scores: 1 [Unknown], 2 [Unknown], 3 [Unknown], 4 LOW, 5 [Unknown]
account_status: OUT
report_path: none (inline)
next_action: the rep is told the verdict and its disqualifier by 2026-10-21, and no sequence is drafted
```

---

## Common Patterns

### Pattern: 10-K vs. Earnings Selection

**When:** A public company has both an annual filing and a recent earnings call.
**Approach:** Use the earnings call for time-sensitive outbound, where the window is 7 to 14 days. Use the filing for deeper strategic outbound, where the relevance lasts months. Both can run on the same company at different times.

### Pattern: The Filing Check Before Any Package

**When:** The source is a public company's filing.
**Approach:** Read the systems section first. A consolidator that runs its own system is disqualified before any zone is scored. That is the cheapest check in the workflow, and it saves the rest of the run.

### Pattern: Active Deal Guard (BDR)

**When:** The user is a BDR and the account has an AE owner who has not said yes.
**Approach:** Write the coordination note for the AE, with the intelligence the AE can use. Write no POV brief and no sequences. The BDR shares the note with the AE rather than sending anything.

### Pattern: Insufficient Intelligence Fallback

**When:** The sources are too thin to score enough zones for a verdict.
**Approach:** Deliver what is available. Mark unscored zones `[Unknown]`, classify the account as MANUAL REVIEW only when at least one zone is scored HIGH, list the research actions by zone, and recommend `gtm-account-snapshot` as the faster route.

---

## Troubleshooting

### "The 10-K content is too long to process"

**Symptom:** The filing is too large to read in one pass.
**Likely cause:** The whole document was pasted.
**Response:** Work the required sections only: Items 1, 1A, 7 and 9A. These carry most of the relevant intelligence. Skip the financial statement tables, and say in the summary that they were skipped.

### "The earnings call transcript is not available yet"

**Symptom:** The transcript has not been published.
**Likely cause:** The call is recent, or the company does not publish transcripts.
**Response:** Use the earnings press release as the substitute. It carries the key metrics but not the analyst questions. Tag it `[Public: earnings press release, date]`, and note the reduced depth at the top of the output.

### "The private company has almost no public information"

**Symptom:** Step 2 finds only one or two tagged facts.
**Likely cause:** The company is small, new, or has no press presence.
**Response:** Classify it as MANUAL REVIEW only if at least one zone is scored HIGH. Otherwise say "Insufficient data" and list the research gaps. Recommend the routes that do exist: a licensing record search, a job posting review, and the company's own staff pages.

### "The revenue estimation methods give conflicting results"

**Symptom:** The employee benchmark and the branch proxy give different figures.
**Likely cause:** The rates come from different sources, or the company's footprint does not match its headcount.
**Response:** Report the range from each method and name the spread. Tag each figure with its method. Do not average them into a single number.

### "A zone cannot be scored"

**Symptom:** The sources do not say anything about a zone.
**Likely cause:** The source is narrow, such as a single filing that covers only financial matters.
**Response:** Mark the zone `[Unknown]`. Never score it LOW from silence. Name the source that would settle it as a research action.

### "The account is ACTIVE with an AE owner"

**Symptom:** The user is a BDR and the account has an open deal.
**Likely cause:** The account is in a late stage, and the BDR was not aware of the AE's work.
**Response:** The guard fires. Write the coordination note for the AE and stop. Write no sequences, unless the AE has said yes.

---

## Best Practices

### Do's

- **Tag every claim.** Use the six tags: `[Public: source, date]`, `[CRM]`, `[Call]`, `[Notes]`, `[Inferred: method]` and `[Unknown]`. The tag tells the next reader how much weight the fact can bear.
- **Use a different anchor in each email.** A signal used twice in one persona's sequence reads as a copy-paste, and the prospect notices.
- **Match proof points to the vertical.** Pick the proof point that matches the prospect's segment and persona, and only from Verified or Benchmark status.
- **For earnings calls, act fast.** The 7 to 14 day window is real. Speed matters more than polish.

---

## Integration With Other Skills

- **Reads from `gtm-account-snapshot` (02), by these names:**
  - `account_status`: an ACTIVE status with an AE owner triggers the guard
  - `verdict`: a DISQUALIFY from 02 is confirmed here, not assumed, before research starts
  - `contact_priority`: the ranked personas and names to write to first
  - `pain_hypotheses`: each one is tagged. Only a claim tagged `[Public: source]` or `[CRM]` may be the claim in an email. An `[Inferred]` hypothesis is not used as a claim
  - `sequence`: 02's sequence is not repeated. This skill's sequences add the source-based anchors that 02 did not have
- **Account Qualification (01)** runs before 02. Its verdict reaches this skill through 02's `verdict` field, so nothing is read from 01 directly.
- **Hands to `gtm-meeting-prep` (06), by these names:** `pov_brief`, `signal_map`, `wedge` (with its arithmetic shown) and `persona_emails`. Meeting prep reads them to start the first call from the same facts.
- **Hands to Wrap-Up:** `report_path` when a file was written, the `verdict` and `zone_scores` as the session's result, and `next_action` with its owner and date.
- **Shared profile section:** Trigger Event Outbound (04) and Closed-Loss Reactivation (05) read the same Industry Context section. This skill hands them no fields.
- **Routes to:** `gtm-competitive-displacement` (12) when a specific incumbent is named in the source, `gtm-trigger-event-outbound` (04) when the source carries a dated event, and `gtm-deal-pulse` (08) once an opportunity exists.

### Chains

- **Qualify To Book:** Account Qualification (01), Account Snapshot (02), then Research Outbound (03, this skill) or Trigger Event Outbound (04), then Meeting Prep (06). This skill adds the sourced point of view, the signal map and the wedge for enterprise accounts, where the depth is worth the time.

---

## Changelog


### 2.1.1 (2026-10-25)
- Adds examples/try-it.md so a first run reproduces Example 1. No other change.

### 2.1.0 (2026-10-25)
- Reads the Context OS account folder and offers read-only CRM and call connectors through the shared contract's new Knowledge Base and Connectors section. Adds a Chains subsection. No other change.

### 2.0.1 (2026-10-20)

- Every hand-off block carries a run_date line after its account line, so two instruments on one deal are compared by date (found by the wave two hand-off tests). No other change.
### Version 2.0.0 (2026-10-20)

- Industry Context is read from the profile as a sourced list. An unsourced industry claim is dropped.
- The persona count comes from Buyer Personas, and the email count is personas times steps. The fixed count is removed.
- Step 7 reads the Persona who acts column of the Buying Triggers table.
- The six evidence tags replace the old labels. The Verified, Estimated and product-benchmark labels are retired.
- Zones and the verdict come from the profile. A zone the sources do not speak to is `[Unknown]`, not LOW.
- Proof points are named only when Verified or Benchmark.
- New Example 4: a filing check that ends in DISQUALIFY with zero emails. Example 3 now shows all five zones. Every example ends in a hand-off block.
- Structure brought to the house format: Why This Skill Exists, Role, Modes, Epistemic Rules, Hard Rules and Quality Bar added. The old file-format options are replaced by one file option in the Output Contract.
- Hand-off fields named in the Output Contract and in Integration. The report is inline, and a Markdown file is written only when asked.

### Version 1.3.0 (2026-10-13)

- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Persona count corrected to 5, giving 20 emails per 10-K or private package.

### Version 1.2.0 (2026-09-29)

- Worked examples rewritten around one shared case.
- Em dashes removed from prose.

### Version 1.1.0 (2026-07-06)

- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology.
- Company-specific data moved out of the skill and into the shared profile.

### Version 1.0.0 (2026-03-04)

- Initial release, merged from three research workflows (10-K, private company, earnings call) and unified by research type.
