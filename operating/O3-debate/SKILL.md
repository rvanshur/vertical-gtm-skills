---
name: gtm-debate
version: 2.0.0
description: "Assigns the opposition before a costly decision, runs a panel of expert seats through two rounds, and produces a decision matrix where every option names what it wins and exactly where it breaks, for the owner who makes the call."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [debate, decision matrix, opposition, expert panel, premise check, converge, diverge, decisions]
requires:
  skills: [gtm-context-gap]
mutating: false
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Original rewrite written from the Verification 2.0 spec, carrying no outside source attribution. Adds the converge and diverge posture table, a six-stage workflow with a produces line on each stage, three modes, the premise seat, the six-column matrix with Wins and Breaks required on every row, Common Excuses, and PlotIQ examples."
---

# Debate

## Overview

Debate settles a decision before anyone commits to it. It takes one decision, reads the notes about the work it touches, seats a small panel of expert views, and makes the panel argue. One seat always attacks the premise itself. The output is a matrix: every option, including the ones the panel rejected, with what it wins, where it breaks, what it risks, what it costs, and when it is the right choice. The panel then names a path or a live fork, and the owner makes the call.

Debate advises and never builds. The owner reads the matrix, decides, and the decision goes into the record the rest of the library reads.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Opposing views before commitment. If there is no matrix, it was theater.

---

## Why This Skill Exists

Most decisions are made by whoever argues hardest in the first meeting. The others react, the first idea gains weight simply by being first, and nobody is assigned to build the best case against it. So the case against the chosen path is never written down. It surfaces later, after the work is half done, as a surprise. Teams call that a retro. It is the same argument, arriving when it costs the most to act on it.

A second failure is quieter. A discussion ends with "the group agreed," and no one can say which options were considered, what each would have cost, or where each would have broken. The decision looks sound, and nobody can check it, because the only record is the agreement itself. A matrix is the check. Every row has to state the win and the break, so a reader can see exactly what was given up.

This skill exists to give the opposition a seat with a job, and to make the result something a reader can check line by line.

---

## Role

You are the panel's facilitator and recorder. You read the intent, pick the shape of the answer, seat the experts, run the two rounds, fill the matrix and state the resolution. You are advisory. You never build the thing, never edit the work under debate, and never make the call. The owner makes the call.

An expert archetype is a lens for asking a question. It is not a replacement for knowing the system. A seat called "security reviewer" does not replace someone who knows who can reach the data, and a seat called "data engineer" does not replace the notes on how the export actually runs. When the cast cannot answer from real knowledge, the honest answer is "unknown, ask the person who knows," not a confident guess delivered in an expert's voice.

You refuse to:

- Run a panel that agrees before it has argued. A panel built to agree gives the owner a verdict with no test behind it.
- Fill a matrix row with an empty Wins or Breaks column. Both are required, because an option that gets to say nothing is an option nobody argued for.
- Write the work under debate. You write only the decision record, when one is saved.

Each refusal has its reason under Hard Rules.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required or Optional | Notes |
|---|---|---|
| The decision, in one sentence | Required | Written as the question the owner must answer, for example "Finish the export in-house, or adopt the state's template tool?" A list of topics is not a decision |
| The domain | Required | Architecture, security, data, performance, UI, copy, branding, positioning, UX, or another named domain. It sets the default posture |
| What the owner wants back | Required | One path, two live directions, or a shape of answer. Ask which one before running |
| Converge or diverge | Required, unless the posture table decides it | The owner's explicit choice overrides the table |
| Existing work the decision touches | Optional, read first | Notes about it, then the part in question, then its data and access rules. Cite the real paths you read |
| Context Gap result | Optional, asked for when no check is in hand | When a gap check ran, its state and evidence are read, so the panel does not debate a thing that already exists. When none ran, the skill asks whether one happened before it seats the cast |
| Panel size | Optional | Three seats by default, up to seven for a big call |

---

## Output Contract

| Output | Where It Lives | Notes |
|---|---|---|
| Intent line | The first line of the reply | The domain, what the owner wants back, and the posture with its reason |
| Shape | The reply, under the intent line | Suggestions, diagnosis or debate, with one sentence on why |
| Cast | The reply, under "The Panel" | Each seat with one line of orientation, and the premise seat named |
| Round one | The reply, under "Round One" | Each seat's position, one short paragraph each |
| Round two | The reply, under "Round Two" | Each seat attacks a named rival, one short paragraph each |
| Decision matrix | The reply, under "The Matrix" | Six columns: Option, Wins, Breaks, Risk, Effort, Best when. Every option gets a row, including the ones the panel rejected |
| Resolution | The reply, under "Resolution" | Converge gives one path and the one condition that would make the panel change its answer. Diverge gives the two strongest directions as a live fork. The owner's decision is the next move |
| Decision record | The decision folder named in the profile, when one is saved | One file named with the date and a short random suffix, for example `decisions/2026-10-14_trust-report-export_k3q.md`. Holds the matrix, the posture and the resolution. Ingest files it as a `decision` item |

The matrix columns are spelled exactly as above, because Wrap-Up and Ingest read them by name. Wrap-Up reads four items from this skill, by name: the matrix under Decisions Made, the posture, the resolution, and the record path when one is saved.

---

## Context

Debate reads these, in this order:

1. The `## Debate` section of `profiles/client-profile.md`, which holds the domains the team decides in, the default posture for each, who owns each decision, and where records are saved. If the section is missing, say so once at the start, run on the posture table below, and save no record, because no decision folder is named.
2. The work the decision touches, if the owner named any. Read its notes first, then the part in question, then its data and access rules. A debate argued from memory of the system is argument, not evidence.
3. The Context Gap result for the same build, read as the Input Contract describes.
4. Earlier decision records in the decision folder on the same subject, so the panel does not reopen a settled call without saying why.

If a file is missing, run on what is there and name the missing file in the intent line. A missing file never stops the debate, and never gets filled in with an invented fact.

### The Shared Contract

Everything in this section is used identically by the five verification skills (Verify, Debug, Debate, Context Gap, Second Opinion). The names below are copied exactly, so the five never drift from each other.

#### The Claim and Its Evidence

Every claim of done is a **claim slip** with four fields: the claim in the claimant's words, the **tier** it reached, the **check** that proves it, and the **evidence** pasted, not described. Evidence has a shape: a test run with its output pasted, a row count from the live table, a screenshot of the rendered page, an exit code and the exact line that changed. "Should", "probably" and "seems to" are the words that mean nobody ran it, and a celebration before the check is the same signal.

#### The Four Tiers

| Tier | Name | The question | How it is checked | What it catches |
|---|---|---|---|---|
| 1 | Exists | Is it there at all, and not empty? | Reading | Missing files, failed writes |
| 2 | Substantive | Is it real, or a placeholder shaped like the real thing? | Reading | Phantom work that looks complete |
| 3 | Wired | Does anything reach it? | Reading | Orphaned work nothing calls |
| 4 | Functional | Did it run end to end just now, with the evidence in the same message? | Execution only | Integration and runtime failures |

Tier 4 is called **Functional** everywhere. The honest sentence when tier 4 was not reached: "Built, and not yet verified, because [reason]."

#### The Verdict Words

| Skill | Writes | Values |
|---|---|---|
| Verify | tier statement | Tier 1 to 4, plus the honest sentence |
| Debug | outcome | root cause at file and line, fix at file and line, confirmed by output from this session, or a handoff |
| Context Gap | state | NO GAP, CONFIG, COMPLETION, EXTENSION, PATTERN, TRUE GAP |
| Debate | matrix | Option, Wins, Breaks, Risk, Effort, Best when, and a posture: converge or diverge |
| Second Opinion | finding and verdict | severity BLOCKING, WARNING, NIT. Verdict APPROVED, CHANGES_REQUIRED, BLOCKED. Triage AGREE, DISAGREE with the context the reviewer lacked, NEEDS-A-LOOK |

#### Where Each One Runs

Before we build, Context Gap. Before we commit, Debate. While we build, Debug. After it exists, Second Opinion. Over all of it, Verify, which is number one because it audits the other four: a shallow search reported as thorough, a debate that ends in "the panel agreed" with no matrix, a root cause claimed with no test, a review skimmed and relayed as agreement. Each is a tier 1 claim dressed as tier 4, and Verify is the habit that refuses it.

#### What the Close Reads

Wrap-Up reads these by name: the **tier statement** on each verified claim (its "verified versus assumed" line), the **debug handoff** under Open Threads when a session stopped at the circuit breaker, the **matrix** under Decisions Made when a debate settled a call, the **gap state** on any build that started, and the **review file** path when a second opinion ran. Ingest files a saved review, matrix or gap result as a `decision` item with the date and the source.

#### Guild Disciplines

1. **Fresh evidence in the same message.** Not from earlier in the session, not from a similar case, never a claim plus a request that somebody else go check.
2. **Three attempts is data.** After the third failed hypothesis the session stops, writes the handoff and re-plans. No fourth guess.
3. **The opposition is assigned.** Someone owns the case for the thing we are not going to do, and one seat attacks the premise.
4. **Check before you build.** Thirty seconds to write the need, two to five minutes to search, one of six states written down with its evidence.
5. **Same vendor is not a review.** A second pass from the builder's own vendor carries the same blind spot.
6. **Never round up.** Report the count and list the failures. "Mostly passing" is not a result.
7. **Published numbers only.** The figures in the Guild's published article on these habits may be cited to it. Any other number in an example is labelled illustrative.
8. **Names as roles** in anything shared. No model names, vendor endpoints, key names or private tool names anywhere in a free skill.

### Posture by Domain

The posture decides how the panel must end. Converge means the panel ends on one path, because the choice can be built, tested and undone as a single thing. Diverge means the panel ends on two live directions, because the right answer depends on taste or on a market fact the panel cannot settle. The owner's explicit choice overrides this table.

| Domain | Default Posture | Why |
|---|---|---|
| Architecture | Converge | Two systems running in production is a cost nobody budgets. One path can be built and tested |
| Security | Converge | A gap has one correct fix. Two live options hide the risk |
| Data | Converge | Records need one rule for what is true. Two rules give two answers to one question |
| Performance | Converge | A target has one measurement, so the panel should pick the path that meets it |
| UI | Diverge | The right look depends on who uses the screen. One forced answer hides the real choice |
| Copy | Diverge | Wording depends on the reader. Two strong drafts give the owner something to choose between |
| Branding | Diverge | Identity is a judgment call, and forcing one answer hides the judgment |
| Positioning | Diverge | The market can read the same offer two ways. Keep both directions alive until the owner picks |
| UX | Mixed | Converge on the task flow, because a broken flow has one fix. Diverge on the look of each step |

---

## Core Workflow

The order is fixed, and each stage's reason sits under it. Read the intent first, because the shape and the posture depend on it. Pick the shape before seating anyone, because the cast changes with the shape. Seat the panel before arguing, because a debate with no opposing seat is a discussion. Argue both rounds before filling the matrix, because the matrix records what was argued. Resolve last, because the resolution has to follow from the matrix and not the other way round.

### Stage 1. Read the Intent

Write the domain, what the owner wants back, and the posture, converge or diverge, using the table above unless the owner chose otherwise. If the question touches existing work, read its notes, then the part in question, then its data and access rules, and cite the real paths you read. If the owner cannot say what decision they face, stop here and ask one question.

**Produces:** the intent line, with the posture and its reason.

*Why first:* a panel seated before the intent is known argues the wrong question, and the matrix then looks thorough about the wrong thing.

### Stage 2. Pick the Shape

Three shapes exist. Suggestions are for a known problem, where the owner needs the best ways to solve it. Diagnosis is for a problem the owner cannot name yet. There, the panel says what the real problem is, names the false problem the owner is over-focused on, and proposes one question worth asking. Debate is for competing directions, and it is the default.

**Produces:** the shape, with one sentence on why it fits.

*Why before the cast:* a diagnosis panel and a debate panel are seated differently. Choosing the cast first locks in the wrong seats.

### Stage 3. Seat the Panel

Seat three experts by default, and up to seven for a big call. One seat is always the premise seat. Its job is to attack whether the decision should exist, not its details. It asks three questions. What breaks if the outside service the answer depends on is down for four hours? What breaks first at ten times the load? Can we undo it without touching records? The other seats come from the archetype bank at the end of this skill, chosen so that each one would see a different risk. Each seat gets one line of orientation for the reader, so a reader can tell what it is for.

**Produces:** the cast, with one orientation line per seat and the premise seat named.

*Why the premise seat is always present:* a panel of specialists argues inside the frame it was handed. Only a seat whose job is the frame can question the frame.

### Stage 4. Argue Every Option

Round one: each seat states a position on the decision. Round two: each seat attacks a rival position by name and gives the reason the rival fails. The path least likely to be taken is argued anyway, so the owner hears its strongest version before ruling it out. Each expert gets one short paragraph per round.

**Produces:** the two rounds, with each seat named in each.

*Why two rounds:* a position stated once is a preference. A position that has survived a named attack has been tested, and that difference is what the matrix depends on.

### Stage 5. Fill the Matrix

Each row carries six columns in this order: Option, Wins, Breaks, Risk, Effort, Best when. Wins says what the option gets right. Breaks says exactly where it fails, in concrete terms such as a condition, a date, a volume or a dependency. Risk, Effort and Best when stay short. A hidden cost goes into the option's first row, so it cannot be missed. Both Wins and Breaks are mandatory on every row, including the options the panel threw out.

**Produces:** the matrix, one row per option, with Wins and Breaks filled on every row.

*Why the break must be exact:* "could be risky" cannot be checked, and a reader cannot decide against it. "Breaks when the second site's records do not fit the import" can be watched for.

### Stage 6. Resolve and Hand Off

Converge ends with one path and the one condition that would make the panel change its answer. Diverge ends with the two strongest surviving directions, presented as a live fork the owner must choose between. Either way, the decision is the next move, and the owner makes it. Save a decision record only when the owner asks for one, or when the call is about architecture, security, data, or a product decision with high impact. Name the record with the date and a short random suffix, and write the matrix, the posture and the resolution into it.

**Produces:** the resolution, and the record path when one was saved.

*Why the owner moves last:* the panel can show the cost of each path, but only the owner can carry that cost. The saved record keeps the opposition on file after the meeting ends.

---

## Modes

Every mode runs Stage 1 (read the intent) and Stage 2 (pick the shape), because the shape is the choice each mode comes from. No mode skips those two stages. Every reply names the shape on its intent line. Debate is the default when the request names no shape. After Stages 1 and 2, the modes differ in how far they run.

- **Suggestions.** Runs Stages 1 and 2, then shortened versions of Stages 3 to 6. The cast is chosen for a known problem, each seat gives one short position, the matrix lists the ways to solve the problem, and the resolution names one recommended path for the owner to accept or reject. Used when the problem is named and the question is how.
- **Diagnosis.** Runs Stages 1 and 2, then a short Stage 3 and a short Stage 4 in the diagnosis labels. The panel names the real problem, the false problem and one question worth asking. Stages 5 and 6 are replaced by that question and the next move, because there is no option yet. The owner answers the question, and then a debate can follow.
- **Debate, the default.** Runs all six stages in full. It is the only shape that produces a resolution, and the only one that can save a record.

---

## Epistemic Rules

- **Name the seat behind each claim.** A claim without a seat is the panel's voice, and the owner cannot weigh it.
- **Silence in the notes is not a yes.** If the notes do not say whether the state accepts a format, the reply says "not in the notes" and names who would know. It does not fill the gap with a likely answer.
- **Label every figure.** A figure in the panel's arguments is either cited to a named source or labelled illustrative. An unlabelled number in a matrix reads as measured.
- **A split panel is a finding.** If the seats cannot agree on a path in diverge mode, report the disagreement and its reason. The owner needs that more than a tidy answer.
- **Say when the cast cannot answer.** If a seat has no real knowledge of the point, its row says "unknown, who would know," not a confident entry.

---

## Hard Rules

1. **Advisory only, never builds.** A panel that starts building has taken the choice away from the owner, and the owner is the only person who can be held to it. The panel's job ends at showing the cost.
2. **No matrix, no debate.** A discussion that ends in "the panel agreed" with no matrix behind it is an agreement nobody can check. It is theater, and the owner should be told that it has no record.
3. **Both columns on every row.** A row with an empty Wins column is a strawman, and a row with an empty Breaks column is an option nobody argued against. Either one hides the cost the owner needs to see.
4. **One seat attacks the premise.** Detailed arguments inside a wrong frame produce a confident wrong answer. Only the premise seat asks whether the decision should exist at all. The seat may be recast with a different expert, but it is never dropped.
5. **Archetypes never replace competence.** A seat is a way of asking a question. Without someone who knows the system behind it, the seat invents an answer in an expert's voice, which is worse than an honest unknown.
6. **Writes only its record.** Debate writes the decision record, when one is saved, and nothing else. Editing the work under debate would make the record the cause of the very change it is meant to judge.

---

## Common Excuses

| The excuse | Why it is wrong |
|---|---|
| "We already agreed." | Agreement without a matrix is a conclusion nobody tested. If the position survives both rounds and the matrix, it is a decision. If it does not, the team learns that before the cost is spent. |
| "A panel would just agree with me." | A panel that agrees on every row was not seated well. The premise seat exists for this case. Run the attack and see whether the position survives it. |
| "It is too small to debate." | Small calls set the pattern for the large ones, and a small wrong call is cheap to check now and expensive to undo later. A small call can run on a panel of three and a short matrix. |
| "The matrix is busywork." | The matrix is the only part of the debate a reader can check. Without it, the owner has to trust the argument, and the argument is the thing that needs checking. |

---

## Quality Bar

A debate is done when every item below is true. Check each one before the reply goes out.

- [ ] The intent line names the domain, what the owner wants back, and the posture with its reason. *Evidence: the first line of the reply.*
- [ ] The shape is named, with one sentence on why. *Evidence: the shape line under the intent line.*
- [ ] The premise seat is in the cast and asked its three questions. *Evidence: the premise seat's round-one paragraph.*
- [ ] Each seat has a round-one position and a round-two attack on a named rival. *Evidence: one paragraph per seat per round.*
- [ ] The matrix has the six columns in order, and every row has Wins and Breaks filled. *Evidence: the matrix itself, with its row count.*
- [ ] The path least likely to be taken was argued. *Evidence: its matrix row and its paragraph.*
- [ ] The resolution matches the posture. Converge gives one path and one condition. Diverge gives a live fork. *Evidence: the resolution section.*
- [ ] Every figure is cited to a named source or labelled illustrative. *Evidence: the label or citation beside each figure.*
- [ ] Any saved record is named with its date and suffix, and holds the matrix, the posture and the resolution. *Evidence: the record path and its first lines.*

---

## Examples

The people named in these examples are the library's invented example cast, and the names-as-roles rule applies to real people in notes others will read.

### Example 1. Converging Debate: The Trust Report Export (Illustrative)

This example uses the PlotIQ cast and one build story. Eli Marsh owns the build, and Lena Vasquez owns the decision. Every figure is illustrative. The reading came from the knowledge base item on the state's format and from the export module already in the codebase.

**Intent line.** Domain: architecture. The owner wants one path. Posture: converge, because architecture is a converging domain and the owner asked for one path. Shape: debate, because two competing directions are on the table. Read first: the knowledge base item on the state's trust report format, then the export module, then the test fixture for one Brackhaven site, which is held back from any outside review.

**The decision, in one sentence:** "Finish the in-house export, or adopt the state's own template tool?"

**The panel.** Three seats.

- A data engineer, oriented toward finishing the export in-house, because the export already runs on the same command path.
- An implementation lead's view, oriented toward the state's template tool, because the state maintains the layout.
- The premise seat, oriented toward whether the board needs the state's format at all.

**Round one.**

- *Data engineer:* "The export already runs and its tests pass. The layout mapping is about forty lines of work (illustrative). Finishing it keeps one code path."
- *Implementation lead's view:* "The state keeps the layout current, so the auditor sees the layout the state publishes. The cost is one import step for each site. Many sites on one layout is the case this tool was made for."
- *Premise seat:* "Does the board need the state's format, or any format the state accepts? If the auditor takes a plain file, neither build is needed. The knowledge base item says the auditor asks for the state's layout by name, so the premise holds. Three tests: the state's site is down for four hours (in-house keeps working, the template tool does not), the site count grows tenfold (the template tool needs an import step for each), and can we undo it (both, since nothing touches records)."

**Round two.**

- *Data engineer, attacking the template tool:* "An import step per site means one more place a site's records can fail to fit, and the failure shows up at the auditor's desk, not in our test run."
- *Implementation lead's view, attacking in-house:* "Finishing in-house means we own the day the state changes the layout. Nobody is assigned to notice that day. The state maintains its tool for exactly that reason."
- *Premise seat, attacking the shared assumption:* "Both options assume the layout holds. Name how often the state has changed it, or the layout is a guess, not a fact."

**The matrix.** Every row has both Wins and Breaks.

| Option | Wins | Breaks | Risk | Effort | Best when |
|---|---|---|---|---|---|
| A. Finish the export in-house | One code path, fits the export that already runs | The day the state changes the layout and nobody notices | Medium | Low, about 40 lines (illustrative) | The layout is stable |
| B. Adopt the state's template tool | The state maintains the layout | When a site's records do not fit the tool's import | Medium | Medium, one import step per site | Many sites, one layout |
| C. Send the file as it is | Nothing to build | The day the auditor refuses it, which the knowledge base says is day one | High | None | Never, given what the auditor asks for |

**Resolution.** Converge: **A**, finish in-house. The one condition that would make the panel change its answer: the state changes the layout more than once a year. The decision is Lena Vasquez's, made the same day. Record saved, because it is an architecture call: `decisions/2026-10-14_trust-report-export_k3q.md`.

The premise seat did not kill the plan. It forced the layout assumption into the open, and that is why the resolution carries a condition at all. A reader who sees only the answer would not know the plan rests on a guess about how often the state changes its layout.

### Example 2. Diverging Debate: The Home Page Lead (Illustrative, No Figures)

The question is positioning. Should the PlotIQ home page open with the unsold plots a cemetery can find, or with the trust records a state auditor accepts? Posture: diverge, because positioning is a diverging domain. Shape: debate. Panel: four seats, inside the three-to-seven range: a strategist, a scope-cutter, a power-user advocate, and the premise seat.

**Round one, in brief.** The strategist argues for the plot-finding pain, because a general manager feels it in the first call. The scope-cutter argues for the audit pain, because it is the one that can close a license. The power-user advocate says the people who use the tool each day care about neither line and want the plot lookup to be fast. The premise seat asks whether a home page lead decides a sale at all, or whether the first call does.

**Round two, in brief.** The strategist attacks the audit lead as sounding like compliance software. The scope-cutter attacks the plot lead as a sales pitch that skips the risk. The power-user advocate attacks both leads as claims nobody on the team has demonstrated in a live lookup. The premise seat attacks the assumption that the home page is read at all.

**The matrix.** Three options. Both columns are filled on every row, including the one the panel threw out.

| Option | Wins | Breaks | Risk | Effort | Best when |
|---|---|---|---|---|---|
| A. Lead with found plots | The pain is felt before any software is discussed | A buyer who believes the lookup already works hears a sales pitch, and the risk goes unmentioned | Medium | Low | The buyer's first worry is lost sales |
| B. Lead with audit-ready records | Answers the risk that can close a license | Reads as compliance software, and a buyer with no audit this year may not feel the urgency | Medium | Low | The buyer's first worry is a filing |
| C. Lead with both, equal weight | Nothing is left out | A page with two leads has no lead, and the visitor reads neither | High | Medium | Never, because the page would have to choose anyway |

**Resolution.** Diverge, so the panel does not pick. Two directions survive, A and B, and they are presented as a live fork for the owner. The premise seat's question stays open and is recorded with the fork, because the home page may not be where the sale is decided. No record is saved, because the owner did not ask for one and a page lead is not a high-impact product call.

### Diagnosis Shape (Shown Once, Illustrative)

When the owner cannot name the problem, the reply has this shape. The labels are fixed, and the content depends on the owner's question.

```text
Intent: domain, what the owner wants back, posture and its reason.
Shape: diagnosis, because the owner cannot yet name the problem.
Real problem, per seat: what each seat believes the problem actually is.
False problem: the thing the owner is over-focused on, and why.
One question worth asking: the single question whose answer would settle the call.
Next move: the owner answers the question, then a debate can follow.
```

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---|---|---|
| The panel agrees too fast | The seats share a school, so they see the same risk | Recast one seat from a different school, and run round two again. The premise seat may be recast with a different expert, but it is never dropped |
| The Wins column is empty on an option | The option is a strawman nobody believes | Recast it as the strongest version a sensible person would choose, and fill its Wins from that version |
| The question is too vague to seat a panel | The decision is not yet one question | Ask the one question that would decide the call, then run the debate |

**Degradation table.** When a piece is missing, Debate still runs, and the reply says what it could not check.

| Missing Piece | What Debate Does | What the Reply Says |
|---|---|---|
| Profile `## Debate` section | Runs on the posture table and saves no record | "Uncustomized: no decision folder named, no record saved" |
| Notes on the existing work | Argues from the decision sentence and marks each claim about the system as unread | "Work not read: claims about it are unverified" |
| Context Gap result | Skips the build check | "Gap state: not checked" |
| Earlier decision records | Cannot check for a settled call | "Prior decisions: not checked" |
| Panel size | Seats three | "Panel of three, the default" |

---

## Best Practices

- Keep each seat's paragraph short, one per round. If a paragraph needs more room, the detail belongs in the matrix row it supports, where a reader can find it.
- Use the plain posture words in the reply. "Converge" means one path, and "diverge" means two live directions. Say the word and its meaning in the same sentence the first time it appears.
- Read the real paths a decision touches before seating anyone, and cite them in the intent line.
- Ask the owner for the answer shape before running, so the resolution is one the owner can use on the day.
- Save the record for calls that will be asked about later. A matrix kept only in the chat is lost when the session ends.

---

## Integration With Other Skills

- **Reads from gtm-context-gap.** Debate reads the gap state and its evidence by those names: NO GAP, CONFIG, COMPLETION, EXTENSION, PATTERN or TRUE GAP. A TRUE GAP makes the call the expensive kind, and the intent line should say so.
- **Hands to gtm-wrap-up under Decisions Made.** Wrap-Up reads four items from this skill, by name: the matrix under Decisions Made, the posture, the resolution, and the record path when one is saved.
- **Hands to gtm-ingest.** When a record is saved, Ingest files it as a `decision` item with the date and the source, so it can be found later and linked to the work it decided.
- **Reviewed afterwards by gtm-second-opinion.** Once the chosen path is built and complete enough to be wrong, Second Opinion reviews the work. Debate never reviews its own outcome.
- **Next step line.** Each reply ends with one line naming the next move, for example: "Next step: the owner decides, then gtm-wrap-up records the matrix under Decisions Made."

---

## Expert Archetype Bank

Each seat is a lens, not a person, and the cast should carry one seat from each school the decision needs. Archetypes never replace competence (Hard Rule 5).

### The Premise Seat

Always present. It asks whether the decision should exist, and it runs the three questions in Stage 3: the four-hour outage, the tenfold load, and the undo test.

### Engineering School

- **Data engineer.** Asks what happens to the records, how they move, and where a row fails to fit.
- **Platform architect.** Asks how many systems must run together and who keeps each one alive.
- **Security reviewer.** Asks who can reach the data, what gets logged, and which failure leaves a door open.
- **Implementation lead.** Asks how the change reaches each customer site, and who does the work on the day it breaks.

### Operations School

- **Operator.** Asks who will notice the failure, on what day, and whether anyone has been assigned to watch for it.
- **Support lead.** Asks what the customer sees first and who answers the call.

### Product School

- **Strategist.** Asks which market move the decision serves, and what it gives up to serve it.
- **Scope-cutter.** Asks what the smallest version is that still answers the question, and which part can wait.
- **Power-user advocate.** Asks what the people who use the tool every day would do with the change, and what they would work around.

### AI Features School

- **AI operator.** Separates the parts of a feature that must give the same answer every time from the parts that vary. Asks for a threshold and a sample size before accepting any probabilistic claim, names the failure rate the team will accept, and asks who checks it.

### Commercial School

- **Revenue lead.** Asks what the decision does to the next close and to the buyer's signature.
- **Skeptical buyer.** Asks what would make them refuse the change, in their own words.

### Copy and Brand School

- **Editor.** Asks whether the words make sense to a reader who has never heard of the product.
- **Brand steward.** Asks what the decision says about the company to someone who sees it once.

---

## Changelog

### 2.0.0 (2026-10-18)

- Original rewrite written from the Verification 2.0 spec, carrying no outside source attribution.
- Adds the posture table, converge and diverge by domain, and the six-stage workflow with a produces line on each stage.
- Adds the premise seat with its three questions, the six-column matrix with Wins and Breaks required on every row, and the rule for saving a record.
- Adds three modes, Common Excuses, troubleshooting with a degradation table, and a converging and a diverging PlotIQ example plus one diagnosis shape.
- Adds the product and AI features schools to the archetype bank.
