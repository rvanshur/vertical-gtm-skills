---
name: gtm-engine
version: 2.0.0
description: "Reads a launch plan and its results, finds the step that loses the most people, ranks the next two-week sprints with one Guild score, designs one growth loop, writes the narrative and four sequences, and grades every output on whether it survives without its main operator. Its outputs go to the knowledge base and the client profile, and they are read by the launch owner and the next sprint."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-16
tags: [growth-system, bottleneck, backlog, sprint-cadence, growth-loops, narrative, sequences, metrics-board, vacation-test, operating-discipline]
requires:
  skills: [gtm-launch, gtm-positioning, gtm-discovery]
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-16
    summary: "Ground-up rewrite. Reads Launch's Part A and Part B by name, and reads NOT RUN in a plan-only run. Scores every backlog item with one Guild score, Impact × Unknown ÷ Effort, where Unknown comes from the evidence grade. Adds the vacation test as its own graded stage, with PASS, NOT YET and FAIL. Finds the bottleneck by the number of people lost, with its rate and n. Writes re-grade requests for upstream skills instead of changing grades. Takes every cap and kill date from Launch. Drops the content pillar list, the publishing calendar and the channel expansion plan, which Launch owns. Carries no outside credit. The 1.x version stays in history."
---

# Engine

## Overview

Engine answers one question after a launch: **what keeps this running, and which step should the team test next?** It reads the launch plan that Launch wrote, and the results that Launch recorded at the day-30 review. It finds the step that loses the most people, ranks what to test in two-week sprints, designs one growth loop from start to finish, writes the narrative and four sequences, and then grades every output on one question: would this survive if the main operator went on vacation for two weeks?

The skill runs in eight stages, in a fixed order. It starts from the hand-off, so no result is read before the plan it belongs to is known. It ends with a hand-off, so the next skill can find every field by name. Its findings go back upstream as requests, not as new grades. The skill that owns each claim stays the only one that changes its grade.

**Core Principle:** A growth system is finished only when it keeps running without its main operator. A plan that needs its author to run it is a hero plan, whatever its score says.

---

## Why This Skill Exists

Most growth work fails after the launch, not during it. The team that launched runs every experiment by hand. The first time the main operator takes time off, the experiments stop, and nobody notices until the next quarter, because nothing was written down about who runs what.

The second failure is a blank result read as a zero. When the results are missing, a plan can look as if it found nothing. Engine says NOT RUN in that case, and it refuses to estimate results from plan numbers.

The third failure is a score tuned to rescue an idea. When a favored idea scores low, the easy move is to change a cap, a kill date or a score until it passes. Engine keeps every number that Launch set. If the evidence says the plan is wrong, the work goes back to the owner of the plan.

---

## Role

The agent is a growth system planner. It works only from the launch plan, the launch results, and the evidence grades that Positioning and Discovery wrote. It plans, scores and reports. It refuses to:

- Change a grade that another skill wrote. It writes a re-grade request instead.
- Raise a cap, move a kill date or change a threshold that Launch set.
- Count a blank result as a zero, or write an illustrative number as a result.
- Mark any output PASS while one of its actions has no named owner or no named backup.
- Raise paid spend while any economics status reads "not run on real data".
- Name a bottleneck from plan numbers.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Launch 2.0 Part A: Motion decision, Kill rules per channel, Proof stack, Content plan, Roster, Funnel targets, Economics status, Experiments, Launch budget and Launch date | Required | Read by these exact names. If any field is missing, stop and say so, and point the team to `gtm-launch`. A field that reads [RECORD before launch] is carried as written and is not filled |
| Launch 2.0 Part B: Launch data, Conversion rate, with n, Lead quality, with method, judge and n, Current customers and retention, Open-bet test results and Economics status (day 30) | Required for a full run | If Part B is blank, the run is a plan-only run (see Stage 1) |
| Positioning hand-off: Economics (status words), Open bets (the parts `Load-bearing:`, `Do not build on:` and `Other open bets:`) and Message set | Required | Read by these exact names. Engine does not regrade any of them |
| Discovery's Customer archetype, with its confidence | Required | Read by name. A candidate archetype is labelled as a candidate in every output that uses it |
| Growth goal and timeline | Required | Read from the Growth System section of the client profile. If the profile has none, Engine uses the goal in Launch's Funnel targets, labels it "Launch goal, not profile goal", and records the gap |
| Team time, in hours per week | Required for the vacation test | Read from the Growth System section of the client profile, where it is a fact about the team. If it is missing, the cadence output cannot pass the vacation test and it is marked [RECORD] |
| Growth System section of the client profile | Optional | Read first when it exists. Written by this skill's `CUSTOMIZE.md` |

---

## Output Contract

Downstream skills read these fields by name. Keep the names exactly as written.

| Field | Where It Lives | Notes |
|-------|----------------|-------|
| Retrospective | Retrospective node | One row per channel: channel, motion (from Part A), funnel target (from Part A), actual conversion with n (from Part B), kill date passed (yes or no), decision and rule applied. Reserve as its own row. Reads NOT RUN in a plan-only run |
| Bottleneck | Bottleneck node | The stage that loses the most people, counted in people, its rate with n and its source label |
| Backlog | Backlog node | One row per item: ID, item, claim ID or "new claim", Impact, Unknown, Effort, Score, Rank, Status (Run, Queued, Held, Re-score on a date, or Cut) and kill rule |
| Sprint record | Sprint record node | One record per sprint: sprint number, dates, items run, results with n, decision |
| Loop design | Loop node | Primary loop, its steps, its compounding step, its status (designed, unmeasured or measured) and the candidate loops with their reasons |
| Narrative | Narrative node | The three layers, each with its claim ID and its grade word quoted from the hand-off, and the trace count |
| Sequences | Sequences node | The four sequences, each with its day or cadence, content piece, owner and stop rule |
| Metrics board | Metrics node | One row per measure: measure, source field name, owner, cadence and n rule |
| Vacation test | Vacation test node | One row per output: output, action, named owner, named backup, result word. The overall result |
| Re-grade requests | Re-grade node | One row per request: claim ID, source skill, source field, result, n, proposed grade word, rule applied and note |
| Open bets returned | Open bets node | Each bet whose kill rule was met: bet ID, rule, result and the owner it went back to |
| Growth System | Client profile, `## Growth System` section | Four fields: Growth measure, Current bottleneck, Sprint cadence and Narrative. Written only after approval |

---

## Context

The skill reads these, in this order:

1. **The client profile.** The `## Growth System` section first, when it exists. Then `## Launch Plan`, for the name of the person who approves writes. Then `## Company`, `## ICP Definitions`, `## Buyer Personas` and `## Proof Points`, as context.
2. **Launch's hand-off**, read by the Part A and Part B field names above.
3. **Positioning's hand-off**, read by the names Economics, Open bets and Message set.
4. **Discovery's archetype node**, read by the name Customer archetype.

If the profile has no `## Growth System` section, say so once at the start of the run, use the defaults in `CUSTOMIZE.md`, and list the gap. If the profile has no `## Launch Plan` section, the write-back step cannot name an approver, so write-back stops until one is named.

---

## Core Workflow

The order is fixed. Each stage ends with what it produces. The mode comes first, because a retrospective run on the wrong mode reads blank results as zero. The retrospective comes before the backlog, because the backlog is only worth ranking once the team knows what the launch showed. The vacation test comes after every other output, because it grades those outputs.

### Stage 1. Read the Hand-Off and Set the Mode

- Check that every Part A field is present by its name. Check that Part B is present by its name, even when its values are blank.
- Set one mode, and say it at the top of the output:
  - **Full run.** Part A is complete and Part B has at least one channel line with values.
  - **Plan-only run.** Part A is present, and Part B is blank or holds only the template. Launch's [RECORD before launch] markers may still be there, and they are carried as written.
  - **Blocked.** A Part A field is missing by name. Engine stops, names the field and points to `gtm-launch`.
- Read each economics status word exactly as Positioning and Launch wrote it: pass, fail or not run on real data. Read the word, never the illustrative number beside it.
- **Any "not run on real data" status sets a limit.** No backlog item may raise paid spend above the cap Launch set, and every cost input that is missing becomes a backlog item.
- A claim that appears in no hand-off enters the run as `assumed`. Engine does not grade it higher.

*Why first:* a retrospective run on the wrong mode reads blank results as zero results, and that is the most common way a growth system starts measuring noise.

**Produces:** the input record, one line per field, each with its status word, and the mode.

### Stage 2. Run the Retrospective and Find the Bottleneck

- **Retrospective (full run only).** For each channel in Part B, show four things in a row: the funnel target from Part A, the actual conversion from Part B with its n, whether the kill date has passed, and the decision Launch recorded with the rule it applied. Show the reserve as its own row. Report the variance in counts before it is shown as a rate.
- **Plan-only run.** The retrospective says NOT RUN and names Part B as the missing input. It does not estimate results.
- **Bottleneck.** Find the funnel stage where the largest number of people is lost, counted in people and not in rates. Then show that stage's rate with its n and its source label. A rate with n below five is an observation, and the sentence says so.
- **Bottleneck in a plan-only run.** Engine names the stage that must have pipeline on launch day, as Launch's funnel check requires, and reports the count as [RECORD before launch]. It does not name a bottleneck from plan numbers.

*Why counts and not rates first:* a stage that loses two people out of three looks worse than a stage that loses forty out of a hundred, and only the second one moves the goal.

**Produces:** the Retrospective table, or the NOT RUN line, and the Bottleneck record.

### Stage 3. Score the Backlog and Set the Cadence

**The score.** Each backlog item gets three inputs, each from a fixed scale, and one score.

| Input | Scale | What the number means |
|-------|-------|-----------------------|
| Impact | 1 to 5 | How far the item could move the growth measure if it works. 1 is no measurable effect on the funnel. 2 is one stage of one channel. 3 is one channel. 4 is two or more channels, or a whole funnel stage. 5 is the whole funnel goal, or a gate on spend |
| Unknown | 1 to 4 | How unproven the claim is that the item tests. Read the grade word from the hand-off and map it: `confirmed` is 1, `seen` is 2, `heard` is 3, `assumed` is 4. A claim not in any hand-off counts as `assumed`, so it is 4. A "not run on real data" input counts as 4 |
| Effort | 1 to 5 | 1 is under one day with no spend. 2 is one to three days, with no spend above the channel's cap. 3 is four to ten working days, or spend inside the cap. 4 is more than two weeks, or a second person must join. 5 is spend above the channel's cap, or a new hire |

**Score = Impact × Unknown ÷ Effort**, shown to one decimal. The score runs from 0.2 to 20.0.

- Rank the items from the highest score to the lowest.
- **Tie rule.** A tie goes to the item with the lower Effort. If it is still tied, Engine lists both items and says the owner decides.
- Every item shows all three inputs beside the score, so a reader can see what drove it.
- Every item names the claim ID it tests, or says "new claim" and carries the grade `assumed`. A data task, such as recording a cost input, is an item too.
- A backlog holds five to fifteen items. Fewer than five cannot be ranked honestly, so Engine says so.
- Launch's experiments (its Part A Experiments field) are listed as inherited. Engine does not re-score them, because Launch owns their kill rules.

**Sprint cadence.** Each sprint lasts two weeks. It opens with a planning session and closes with a review of results.

- A sprint runs one item of Effort 3 or higher on its own.
- Otherwise a sprint runs up to three items of Effort 1 or 2.
- The sprint review writes its results into the Sprint record, with the n for every rate.

*Why this score:* it rewards an idea that could move the goal, that rests on a claim nobody has checked, and that is cheap to check. A big idea that rests on a confirmed claim has little left to learn, so it scores low.

**Produces:** the Backlog, ranked, with each item's inputs, claim, status and kill rule, and the sprint cadence.

### Stage 4. Design the Loops

- Assess three loop types, defined in this skill's own words:
  - **Viral.** A customer or user brings in another buyer or user.
  - **Content.** Published work keeps bringing in buyers through search or referral.
  - **Paid.** Revenue from customers pays for the acquisition that brings in more revenue.
- Choose one **primary loop** to design from start to finish, and mark the others as candidates with the reason.
- For the primary loop, write each step, the **compounding step** (the step where an output becomes the next input), the measured conversion at each step with its n, and the step that loses the most people.
- A loop with no measured step is labelled **designed, unmeasured**. It is never labelled working.
- A loop that needs a product feature the profile does not list is a candidate, and Engine says which feature is missing.

**Produces:** the Loop design, with the primary loop, its steps, its compounding step, its status and its candidates.

### Stage 5. Write the Narrative and the Sequences

**The narrative has three layers.** Each layer is one sentence. Each sentence carries its claim ID and its grade word from the hand-off, quoted exactly.

1. **The shift.** What is changing in the market that buyers cannot ignore.
2. **The stakes.** What happens to a buyer who does not act on the shift.
3. **The possible world.** The world the product makes possible for the buyer who does act.

A layer whose claim is not in any hand-off enters as `assumed`, and the sentence says so.

**The trace test.** Every piece in Launch's content plan and every sequence email must name the layer it uses. A piece that traces to no layer is cut or rewritten. The result is written as a count, such as "3 of 3 trace".

**Four sequences carry the narrative on a schedule.** Each sequence has a name, a day or cadence, one content piece, one owner and one stop rule.

| Sequence | Timing | Job |
|----------|--------|-----|
| Start | Day 0 | Delivers what the contact asked for |
| Story | Day 3 | Tells the shift and the stakes, with the grade of each claim |
| Invitation | Day 7 | Makes one invitation, to a conversation or to an event the company runs |
| Keep Going | Monthly, after day 7 | Sends one useful item from the content plan |

Every sequence follows two rules. It reaches only contacts with a prior conversation or a recorded permission to email. A contact who books a first conversation or asks to stop leaves the sequence at once.

**Produces:** the Narrative with its three layers, the trace count, and the four Sequences.

### Stage 6. Set Owners and the Metrics Board

- Write a **Metrics board** row for each measure. Each row has the measure's name, the Part A or Part B field it reads from, one named owner, a review cadence and the n rule that applies.
- **The growth measure** is the measure the profile names. If the profile names none, Engine uses Launch's funnel goal, labels it, and marks the owner as [RECORD].
- Every row needs a named owner. A row with no owner is reported as NOT ASSIGNED, and the vacation test fails for it.
- **Profile write-back.** When write-back is approved, the `## Growth System` section of the client profile holds four fields: Growth measure, Current bottleneck (or "not run" in a plan-only run), Sprint cadence and Narrative (one sentence, with the grade of each claim it uses).

**Produces:** the Metrics board and the profile section draft.

### Stage 7. Take the Vacation Test

The vacation test is its own graded question. It asks, of each output, whether the output would keep running if the main operator were away for two weeks. The question, in the owner's wording, is:

> would this survive if the main operator went on vacation for two weeks?

For each output, list every action the output needs, the named owner of each action and a named backup for that owner. Then grade the output with one word.

| Result | Meaning |
|--------|---------|
| PASS | Every action has a named owner and a named backup, and no action depends on a role that has no name |
| NOT YET | Every action has an owner, but a backup is missing, or a required record is still [RECORD] or blank |
| FAIL | A required role has no name, or an owner has been recorded as unavailable for the period |

- Grade each output in this order: Retrospective, Bottleneck, Backlog, Loop design, Narrative, Sequences and Metrics board.
- **The overall result is the worst output result.** A single FAIL makes the overall result FAIL.
- **A FAIL or a NOT YET goes back to the stage that owns the output.** Engine does not mark it PASS to close the stage.
- The result is written in the hand-off block as a word. A public page may show only the word Engine wrote. The page cannot show PASS while any output reads NOT YET or FAIL.

*Why it is its own stage:* each earlier stage can be right while the whole system still needs one person to run it. The test grades the outputs, not the intent behind them.

**Produces:** the Vacation test table, one row per output, with the owner, the backup and the result word.

### Stage 8. Write Back and Hand Off

- **Write the nodes.** The Retrospective, Bottleneck, Backlog, Sprint record, Loop design, Narrative, Sequences, Metrics board and Vacation test go to the knowledge base, after the approval step in Modes.
- **Re-grade requests.** For each result that could change a grade upstream, Engine writes one request. Engine does not change the grade itself. The owning skill applies the change on its next run. Each request holds the claim ID, the source skill, the source field, the result, its n, the proposed grade word, the rule applied and a note.
- **Open bets returned.** Any bet whose kill rule has been met is returned to its owner, with the rule and the result. Engine does not rewrite the bet.
- **Growth System.** The `## Growth System` section, with the four fields in Stage 6.
- **Hand-off block.** Every output field is quoted in full, with no ID-only entries and no "see above" pointers. The block names the vacation test result for each output.

**Produces:** the nodes, the Re-grade requests, the Open bets returned, the Growth System section and the hand-off block.

The hand-off block uses these labels, exactly as the Output Contract names them:

```text
HAND-OFF FROM ENGINE: [company], Engine 2.0.0 ([full run or plan-only run])

Mode: [full run, plan-only run or blocked, with the reason]
Input record: [one line per field, each with its status word]
Retrospective: [the table, or NOT RUN with the missing input named]. Vacation test: [result word]
Bottleneck: [the stage, its count, its rate with n and source label, or not named with the missing input]. Vacation test: [result word]
Backlog: [each item in full: ID, item, claim ID, Impact, Unknown, Effort, Score, Rank, Status, kill rule]. Vacation test: [result word]
Sprint record: [each sprint: number, dates, items run, results with n, decision]
Loop design: [primary loop, each step, compounding step, status, candidates with reasons]. Vacation test: [result word]
Narrative: [each layer in full, with its claim ID and grade word quoted from the hand-off, and the trace count]. Vacation test: [result word]
Sequences: [each sequence in full: name, timing, content piece, owner, stop rule]. Vacation test: [result word]
Metrics board: [each row in full: measure, source field, owner, cadence, n rule]. Vacation test: [result word]
Vacation test: [one line per output: output, action, named owner, named backup, result word]. Overall: [result word]
Re-grade requests: [each request in full, or "none, no results"]
Open bets returned: [each bet in full, or "none"]
Growth System: Growth measure, Current bottleneck, Sprint cadence, Narrative. [each field in full]
```

---

## Modes

- **Plan (default).** Runs Stages 1 to 7 and reports the result in the brief. It writes nothing.
- **Write-back.** Runs the Stage 8 writes. Before anything is written, the owner named in the client profile's `## Launch Plan` section approves the backlog ranking and the owner list in the brief. Nothing is written until that approval is recorded in the brief.
- **Results.** Reads Part B at Launch's day-30 review, and reads each sprint's results afterward. It writes the Retrospective, the Bottleneck, the Sprint record and any Re-grade requests. It needs the approval recorded in the brief, the same as write-back.

Re-run the plan when Launch writes a new Part A, when Part B changes, when Positioning changes an economics status, and when the team changes who owns a role.

---

## Epistemic Rules

- **n beside every rate,** with its source label.
- **Five before a pattern.** Below five cases, a number is an observation, and the sentence says so.
- **Silence is not a no.** A contact with no recorded answer leaves the rate's denominator. It is not counted as a no.
- **"No difference" is a finding.** Report it, so that no one writes a playbook the results do not support.
- **Grades come from the hand-off, and they are quoted exactly.** The grade ladder is `assumed` (someone believes it), `heard` (a buyer said it), `seen` (it shows up in the company's own deals or data) and `confirmed` (it held across at least five cases with nothing contradicting it).
- **Illustrative is not a result.** An illustrative number or a pilot number is never written into the Retrospective as a result.
- **Scores are judgements** until a recorded result exists, and the output says so.
- **Targets are numbers.** "A quick response" is not a target.

---

## Hard Rules

1. **Engine never regrades.** It writes a re-grade request, and the skill that owns the claim applies the change. *Why:* a grade changed in the wrong place becomes a fact that nobody checks again.
2. **"Not run on real data" is not a pass.** It sets a limit on paid spend, and it creates a backlog item for the missing input. *Why:* a benchmark copied in for a missing input turns a guess into a finding.
3. **Economics gate the spend, not the learning.** While any status reads "not run on real data", no item raises paid spend above Launch's cap. Data tasks that fill the missing input may run. *Why:* spend that scales before the margin is known can lose money as fast as it grows.
4. **Engine never tunes a number to rescue an idea.** Caps, kill dates, thresholds, scores from Launch and grades stay as the owning skill wrote them. If an idea needs a different number, the work goes back to the owner. *Why:* a rescued idea makes the next result unreadable.
5. **The vacation test grades every output.** No output reads PASS while any action in it has no named owner or no named backup. *Why:* a plan that needs its author to run it is a hero plan, whatever the score says.
6. **Plan-only runs say so.** A retrospective with blank Part B reads NOT RUN. *Why:* blank results read as zero results unless the output names them.
7. **Illustrative is not a result.** The Retrospective shows illustrative numbers only inside a worked example, and the label stays beside them. *Why:* a planned number that looks measured is the easiest way to report a success that never happened.
8. **The hand-off quotes in full.** Every item is written out, so the next skill can check it without opening this one. *Why:* an ID alone cannot be checked.
9. **Every rate shows its n.** Below five, the sentence says it is an observation.
10. **Nothing invented.** A launch budget, a date, a team hour figure or a growth goal that the inputs do not hold is marked [RECORD], and the output does not pass on it.

---

## Quality Bar

An Engine run is done when every item below is true. Run the list in order, and report every item that fails, with what would close it.

- [ ] The mode is named at the top, and it is one of full run, plan-only run or blocked.
- [ ] Every Part A field and every Part B field is named in the input record, with its status word.
- [ ] The Retrospective compares plan with actual for each channel with n, or it says NOT RUN.
- [ ] Every backlog item shows its Impact, Unknown, Effort and Score, its rank, its claim ID or "new claim", its status and its kill rule.
- [ ] Launch's experiments are listed as inherited, and none is re-scored.
- [ ] One primary loop is designed from start to finish, with its compounding step, or it is marked designed, unmeasured.
- [ ] The three narrative layers each carry a grade word quoted from the hand-off, or `assumed` for a claim with no hand-off.
- [ ] The trace count is written, and four sequences each have an owner and a stop rule.
- [ ] Every Metrics board row has a named owner.
- [ ] The vacation test has one result word for each output, the dependency named for each action, and an overall result.
- [ ] The Re-grade requests section is present, and it reads "none, no results" when Part B is blank.
- [ ] The hand-off block quotes every output field in full.

---

## Examples

Both examples continue the PlotIQ run from Launch 2.0. Every number that is not in the PlotIQ profile, in article 51 or in Launch's PlotIQ hand-off is labelled illustrative. Example 1 runs in plan-only mode, because Launch's PlotIQ run ended with Part B blank. Example 2 is an illustrative day-90 run, so that the failure path can be shown without inventing a real result.

### Example 1. PlotIQ, Plan-Only Run on Launch 2.0's Output

**Stage 1. The mode and the input record.** Launch 2.0's PlotIQ run gives a Part A with every field present, with two [RECORD before launch] markers (Launch budget and Launch date), and a Part B that is an empty template. The run is **plan-only**. The input record:

| Field | Status (as Launch wrote it) | Engine's treatment |
|-------|-----------------------------|--------------------|
| Motion decision | Present. Archetype SMB Community, candidate, 2 of 6 beliefs graded | Carried. Every output says "candidate" |
| Kill rules per channel | Present. Three channels at 30% each, reserve at 10%, kill date Day 30 | Carried. Engine changes none of them |
| Proof stack | Present. C2 at tier 4, `seen`, n=2, illustrative scenario. C1, "Unsold plots found from paper records", and C3, "Records a state auditor accepts", are labelled bets | Carried. Named customers stay out of copy |
| Content plan | Present. The L-21 guide has NOT ASSIGNED as owner | Flagged in Stage 7 |
| Roster | Present. Content and Comms is NOT NAMED | Flagged in Stage 7 |
| Funnel targets | Present. Illustrative, pipeline count [RECORD before launch] | Carried. The pipeline count is a requirement |
| Economics status | Present. Three thresholds "not run on real data", price "Modeled, not yet tested with buyers (past-behavior test, 0 of 5 held)" | Sets the spend limit in Stage 3 |
| Experiments | Present. A5, A2 and A3, T1, PA1 and PA6 | Inherited, not re-scored |
| Launch budget | [RECORD before launch] | Carried. No spend is computed from it |
| Launch date | [RECORD before launch] | Carried. No sprint date is set from it |
| Part B, six fields | Blank template | Mode is plan-only |
| Message set (Positioning) | Present. One pillar, six why-not answers, one-sentence and thirty-second versions | Carried. Not regraded |
| Economics status (Positioning) | not run on real data for all three thresholds | Same limit as Launch |
| Open bets (Positioning) | Load-bearing: A2, A3, A5. Do not build on: A6, B1. Other open bets: P1, A4R, N1, T1, and PA1 to PA8 | Carried by name |
| Growth System (profile) | Growth goal and window: four one-site contracts signed within 150 days of launch day (illustrative). Team time: [RECORD]. Growth measure, Current bottleneck and Sprint cadence: [RECORD] | The goal is read from the profile and labelled illustrative. Team time is [RECORD], so the cadence cannot pass the vacation test yet. The growth measure is Launch's funnel goal, labelled, with its owner marked [RECORD] |

**Stage 2. Retrospective and bottleneck: NOT RUN.** Part B is blank, so the Retrospective reads NOT RUN and names Part B as the missing input. No bottleneck is named from plan numbers. Engine records the one requirement it can state now: the pipeline count for the four target contracts must exist on launch day, and it is [RECORD before launch].

**Stage 3. The backlog.** The scores below are illustrative judgements. They are not measured, and the output says so.

| ID | Item | Claim tested | Impact | Unknown | Effort | Score | Rank | Status |
|----|------|--------------|--------|---------|--------|-------|------|--------|
| E-001 | Record gross margin, acquisition cost and retention from cost data | Economics status, PA2 (the cost inputs are "not run on real data," so Unknown is 4) | 5 | 4 | 1 | 20.0 | 1 | Run (Sprint 1) |
| E-002 | Comparison guide: PlotIQ against paper plot maps | A2, `assumed`, observation, 4 of 4, n=4 (Unknown is 4) | 4 | 4 | 2 | 8.0 | 2 | Run (Sprint 1) |
| E-003 | Roundtable for cemetery general managers | New claim, `assumed` (Unknown is 4) | 3 | 4 | 3 | 4.0 | 3 | Queued (Sprint 2, runs alone) |
| E-004 | Certification program for pre-need sales teams | New claim, `assumed` (Unknown is 4) | 5 | 4 | 5 | 4.0 | 4 | Re-score on a date (the next quarter review) |

Engine's notes on the table:

- E-001 ranks first. It is a data task, and it unlocks the economics status that gates every spend item.
- E-002 and E-001 both run in Sprint 1, because each has Effort 2 or lower.
- E-003 ties E-004 at 4.0. The tie rule gives E-003 the higher rank, because its Effort is lower. A sprint runs an Effort 3 item alone, so E-003 waits for Sprint 2.
- E-004 needs a trained team and spend above the channel cap, which is Effort 5. Its score cannot move until a buyer-side test exists, so it is re-scored quarterly.
- The five inherited Launch experiments are listed in the output and not scored here.

**Stage 4. The loops.** The primary loop is **referral**, and it is **designed, unmeasured**:

1. A general manager with a clean trust fund filing becomes a champion.
2. The champion refers a peer general manager, directly or through a state association event.
3. The peer books a first conversation. This is the signal Launch named for the channel.
4. The peer becomes a customer. **This is the compounding step.**
5. The new customer refers the next peer after its first state filing cycle.

Every measured step has n=0, so the loop is not labelled working. The step that loses the most people is step 3, but no count exists yet. Candidate loops: **content** (candidate, waits for E-002's result) and **viral** (candidate, not designed). The profile's product modules list no invite feature, so viral needs a product feature the profile does not list. Engine names that feature as the gap.

**Stage 5. The narrative and the sequences.** Each sentence below is Engine's own wording. The claim beside it is quoted from the hand-off, so a reader can check it.

- **The shift.** "State trust fund and records filings call for records a state auditor will accept." Claim R1, hand-off wording: "An annual state trust filing is required." Grade: `seen` on the rule text, illustrative state. The Positioning hand-off adds: "Source dated 2026-03-27, past the 30 day window for `seen`, so re-check before any external use." The re-check is PA7.
- **The stakes.** "A missed trust fund audit can put the license at risk." The profile records this as a pain point with no grade. Positioning's hand-off grades no claim with this wording, so it enters as `assumed`, and the narrative says so.
- **The possible world.** "State-format trust and plot reports, produced from the customer's own ledger." Claim C2, `seen`, n=2, illustrative scenario. It stands only once PA6 records two real demonstrations.

The trace test: Launch's launch email (L-7), the guide (L-21) and the Start sequence each name the shift and the stakes. The possible world appears only in the email, with its illustrative-scenario note. **Result: 3 of 3 trace.**

The four sequences:

1. **Start** (day 0). Delivers the guide to contacts who asked for it. Owner: Nadia Brandt. Stop rule: the contact books a first conversation, or asks to stop.
2. **Story** (day 3). Tells the shift and the stakes, with the grade of each claim. Owner: Nadia Brandt. Stop rule: the same.
3. **Invitation** (day 7). One invitation, a 20-minute call on one date. Owner: Owen Pruitt. The roundtable invitation is added only after E-003 runs.
4. **Keep Going** (monthly, after day 7). One useful item from the content plan. Owner: Lena Vasquez. Stop rule: the same.

**Stage 6. The metrics board and the Growth System draft.**

| Measure | Source field | Owner | Cadence | n rule |
|---------|--------------|-------|---------|--------|
| Contracts signed within 150 days of launch day (Launch goal, illustrative) | Funnel targets | Lena Vasquez | Weekly | Shown with n |
| Conversion to first conversation, per channel | Conversion rate, with n | Nadia Brandt | Weekly | n below five is an observation |
| Cost inputs recorded (E-001) | Economics status | Lena Vasquez | Until recorded | Not applicable |
| Named customers with a recorded permission | Proof stack | Owen Pruitt | Weekly | Not applicable |
| Sequence sends and stops | Sequences | Nadia Brandt | Weekly | Shown with n |

Growth System, draft, not written in plan mode: **Growth measure:** contracts signed within 150 days of launch day, Launch's illustrative goal, owner Lena Vasquez. **Current bottleneck:** not run. Part B is blank. **Sprint cadence:** two weeks, reviewed by Lena Vasquez. **Narrative:** "State trust fund and records filings call for records a state auditor will accept, and PlotIQ produces the report in that format from the cemetery's own ledger (the possible world is `seen`, n=2, illustrative scenario)."

**Stage 7. The vacation test.**

| Output | Action | Named owner | Named backup | Result |
|--------|--------|-------------|--------------|--------|
| Retrospective | Read Part B at the day-30 review and write the table | Lena Vasquez | None named | NOT YET |
| Bottleneck | Count the funnel from Part B | Nadia Brandt | None named | NOT YET |
| Backlog | Run E-001 and E-002 in Sprint 1 | Lena Vasquez | None named | NOT YET |
| Loop design | Run the referral pilot through state association events | Nadia Brandt | None named | NOT YET |
| Narrative | Trace each send before it goes out | Nadia Brandt | None named | NOT YET |
| Sequences | Send the Start sequence with the guide (L-21) | Not assigned. Content and Comms is NOT NAMED | None | FAIL |
| Metrics board | Weekly review of each row | Lena Vasquez | None named | NOT YET |

**Overall result: FAIL.** The one FAIL is the guide's owner. It sits with the role Launch left unnamed, which is Launch's own first fix. Every other output reads NOT YET, because no backup is named, and a backup is the mechanism the test checks. Engine says so in these words and does not mark any output PASS.

**Stage 8. Write-back and hand-off.** Plan mode, so nothing is written. The hand-off block for this run:

```text
HAND-OFF FROM ENGINE: PlotIQ, Engine 2.0.0 (plan-only run, illustrative)

Mode: Plan-only. Launch 2.0 Part A present. Launch 2.0 Part B blank.
Input record: Launch Part A, all ten fields present. Launch budget: [RECORD before launch]. Launch date: [RECORD before launch]. Launch Part B, six fields: blank template. Growth goal and window: four one-site contracts signed within 150 days of launch day (illustrative, from the profile). Team time: [RECORD].

Retrospective: NOT RUN. Part B is blank. Vacation test: NOT YET.

Bottleneck: Not named. The pipeline count for four target contracts must exist on launch day: [RECORD before launch]. Vacation test: NOT YET.

Backlog (scores illustrative):
E-001 | Record gross margin, acquisition cost and retention from cost data | Claim: Economics status, PA2, not run on real data (Unknown 4) | Impact 5 | Unknown 4 | Effort 1 | Score 20.0 | Rank 1 | Status: Run (Sprint 1) | Test: the owner records each cost input from the company's own cost data. n threshold: 3 of 3 inputs recorded. Kill rule: no spend. The data task ends when the three cost inputs are recorded.
E-002 | Comparison guide: PlotIQ against paper plot maps | Claim: A2, paper maps are the pain (assumed, observation, 4 of 4, n=4) (Unknown 4) | Impact 4 | Unknown 4 | Effort 2 | Score 8.0 | Rank 2 | Status: Run (Sprint 1) | Kill rule: the guide's signal is the A2 test, fewer than four of five describe a paper lookup.
E-003 | Roundtable for cemetery general managers | Claim: new claim, assumed (Unknown 4) | Impact 3 | Unknown 4 | Effort 3 | Score 4.0 | Rank 3 | Status: Queued (Sprint 2, runs alone) | Kill rule: invitations go to 10 general managers. If fewer than 3 of 10 accept by day 10 of Sprint 2, the roundtable is dropped and the slot goes to the next item in the backlog.
E-004 | Certification program for pre-need sales teams | Claim: new claim, assumed (Unknown 4) | Impact 5 | Unknown 4 | Effort 5 | Score 4.0 | Rank 4 | Status: Re-score on a date (the next quarter review) | Test: past-behavior conversations with pre-need sales leads on how they train new staff today. n threshold: 5. Kill rule: fewer than three of five name training as a cost they pay today, and the item is cut. No re-score before this test has run.
Inherited from Launch, not re-scored:
- A5: a GM can carry a deal over $25K past the board (assumed, carries the close plan). Test: past-behavior conversations on the last deal over $25K and who approved it. n threshold: 5. Kill rule: three or more of five show a board approved a deal over $25K. Fewer than three means A5 comes out of the close plan.
- A2 and A3: paper maps are the pain (assumed, observation, 4 of 4, n=4) and start with independent cemeteries (assumed, observation, n=4). Test: ask each outbound conversation how a plot is found today. n threshold: 5. Kill rule: fewer than four of five describe a paper lookup. The pain pillar goes back to Positioning.
- T1: the SMB Community ten-deal test (0 of 10 closes recorded). Test: count closes as they happen. n threshold: 10. Kill rule: reported as "0 of 10" until ten closes exist. If fewer than ten closes are recorded by Day 90, SMB Community is withdrawn as the archetype, the motion decision is re-run from recorded results, and the community-led lead is held with no new budget.
- PA1: the setup rule is per account and not yet confirmed. Test: owner writes the rule in the profile's Positioning section, with the two-site year-one total. n threshold: 1 written rule. Kill rule: no written rule by Day 30. Then no two-site quote is issued and the two-site figure stays out of all copy.
- PA6: the C2 demonstration (seen, n=2, illustrative scenario). Test: a real team records its own dated demonstration from a customer's own ledger. n threshold: 2 recorded demonstrations. Kill rule: fewer than two recorded by Day 30. Then C2 drops to assumed, comes out of the pillar and the lead, and the launch leads with no real proof.
Vacation test: NOT YET.

Sprint record: Two weeks per sprint. Sprint 1 runs E-001 and E-002. Sprint 2 runs E-003 alone. Results: none, no results. Vacation test: NOT YET.

Loop design: Primary loop, referral. Status: designed, unmeasured. Steps: (1) a general manager with a clean trust fund filing becomes a champion. (2) The champion refers a peer general manager, directly or through a state association event. (3) The peer books a first conversation. (4) The peer becomes a customer, the compounding step. (5) The new customer refers the next peer after its first state filing cycle. Every measured step has n=0. Candidates: content (waits for E-002's result) and viral (not designed, because the profile lists no invite feature). Vacation test: NOT YET.

Narrative:
Shift: "State trust fund and records filings call for records a state auditor will accept." Claim R1, hand-off wording: "An annual state trust filing is required." Grade: `seen` on the rule text, illustrative state. Re-check due (PA7).
Stakes: "A missed trust fund audit can put the license at risk." Not graded in the hand-off. Enters as `assumed`.
Possible world: "State-format trust and plot reports, produced from the customer's own ledger." Claim C2, grade `seen`, n=2, illustrative scenario.
Trace count: 3 of 3 trace. Vacation test: NOT YET.

Sequences:
Start (day 0). Content: the guide (L-21). Owner: Nadia Brandt. Stop rule: the contact books a first conversation, or asks to stop.
Story (day 3). Content: the shift and the stakes, with the grade of each claim. Owner: Nadia Brandt. Stop rule: the same.
Invitation (day 7). Content: one 20-minute call on one date. Owner: Owen Pruitt. Stop rule: the same. The roundtable invitation is added only after E-003 runs.
Keep Going (monthly, after day 7). Content: one useful item from the content plan. Owner: Lena Vasquez. Stop rule: the same.
Vacation test: FAIL, because the guide's owner is not assigned and Content and Comms is NOT NAMED.

Metrics board:
Contracts signed within 150 days of launch day (Launch goal, illustrative) | Source: Funnel targets | Owner: Lena Vasquez | Cadence: weekly | n rule: shown with n. Vacation test: NOT YET.
Conversion to first conversation, per channel | Source: Conversion rate, with n | Owner: Nadia Brandt | Cadence: weekly | n rule: n below five is an observation. Vacation test: NOT YET.
Cost inputs recorded | Source: Economics status | Owner: Lena Vasquez | Cadence: until recorded | n rule: not applicable. Vacation test: NOT YET.
Named customers with a recorded permission | Source: Proof stack | Owner: Owen Pruitt | Cadence: weekly | n rule: not applicable. Vacation test: NOT YET.
Sequence sends and stops | Source: Sequences | Owner: Nadia Brandt | Cadence: weekly | n rule: shown with n. Vacation test: NOT YET.

Vacation test:
Retrospective: NOT YET (no backup named)
Bottleneck: NOT YET (no backup named)
Backlog: NOT YET (no backup named)
Loop design: NOT YET (no backup named)
Narrative: NOT YET (no backup named)
Sequences: FAIL (guide owner not assigned, and Content and Comms NOT NAMED)
Metrics board: NOT YET (no backup named)
Overall: FAIL

Re-grade requests: none, no results.
Open bets returned: none.
Growth System (draft, not written in plan mode): Growth measure: contracts signed within 150 days of launch day, Launch's illustrative goal, owner Lena Vasquez. Current bottleneck: not run. Sprint cadence: two weeks, reviewed by Lena Vasquez. Narrative: "State trust fund and records filings call for records a state auditor will accept, and PlotIQ produces the report in that format from the cemetery's own ledger (the possible world is `seen`, n=2, illustrative scenario)."
```

**What Example 1 shows.** An honest plan-only run produces a backlog, a loop and a narrative. It does not produce a retrospective or a bottleneck. It grades the team's own roster as the reason the system would not run without its author, and it leaves every number marked where the inputs are missing.

### Example 2. A Failure That Goes Back Upstream

This example is illustrative. It is a day-90 run, and its numbers are assumed for the purpose of the example.

**The setup (illustrative).** Launch's day-30 review found the referral channel under its volume check, with 4 contacts reached, and extended it once, because it stayed under its cap. At day 90 the channel shows 6 contacts reached and 1 first conversation booked (1 of 6, n=6, illustrative). Launch's T1 test, the SMB Community ten-deal test, shows 2 closes by day 90 (illustrative), against the 10 that its kill rule needs.

**The request.** The sales lead asks Engine to place the referral idea at the top of the next sprint, and to raise the referral channel from 30% to 50%, "because community is the lead motion."

**What Engine refuses to do.**

- It does not raise the cap. The 30% cap belongs to Launch's channel rule, and Launch is the only skill that changes it.
- It does not re-score the referral idea to lift it. Its claim is still `assumed`, so its Unknown stays at 4, and a higher Impact would be a judgement with no result behind it.
- It does not count the 1 of 6 conversion as a pattern. The n is 6, and one case is a single observation of one channel.
- It does not treat the T1 count as "nearly there." Launch's rule is a count of ten.

**What Engine does.**

1. **The rule is met.** Launch's kill rule for T1 says that if fewer than ten closes are recorded by Day 90, SMB Community is withdrawn as the archetype, the motion decision is re-run from recorded results, and the community-led lead is held with no new budget. Two closes are recorded. Engine reports the condition as met.
2. **To Launch.** The motion decision needs a re-run from recorded results. The community-led lead is held with no new budget, as Launch's own rule says. Engine does not write the new motion decision.
3. **To Discovery.** The SMB Community archetype is withdrawn, and the archetype must be re-diagnosed from the closes that exist.
4. **In Engine's own outputs.** The Retrospective records that the T1 rule was met and that the referral channel has 1 of 6 (n=6). The Backlog keeps the referral item at its recorded score, with the status "Held, no new budget." No new item is added to rescue it.
5. **Re-grade request.** One request, to Discovery, with a copy to Positioning, which carries T1 as an open bet: claim T1, "the SMB Community ten-deal test (0 of 10 closes recorded)", source field Open-bet test results, result "2 closes recorded against 10 needed by Day 90 (illustrative)," n=10 threshold not reached. The proposed grade word is not written, because T1 is a count, and the kill rule itself is the outcome that Discovery applies.

**What the example shows.** The failure sends the work upstream and changes no number that Launch set. The referral item stays where its evidence puts it, and the team sees the rule that was met.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| The Retrospective shows numbers, but Part B is blank | A template value or an illustrative number was copied into the results | Stop. Reset the Retrospective to NOT RUN, and name Part B as the missing input |
| Every economics threshold reads "not run on real data" | The cost inputs (gross margin, acquisition cost, retention) are not recorded | Name the missing inputs. Put a data task at the top of the backlog. Keep spend at Launch's cap. Do not enter a benchmark |
| The score of a favored idea is too low | The idea has a confirmed claim, or a low impact | Show the three inputs. Do not change them to lift the score. If the evidence is wrong, send the request to the owner of the claim |
| A backlog item has no claim ID | The item tests a new idea | Write "new claim" and grade it `assumed`, so its Unknown is 4 |
| The vacation test reads FAIL on the Sequences | The owner of the guide or a sequence is not assigned, or a role has no name | Name the role. The output stays FAIL until it is named, and the overall result stays FAIL |
| Two items tie on score | Same Score, so the tie rule applies | Give the item with the lower Effort the higher rank. If still tied, list both and say the owner decides |
| The Growth System section is missing from the profile | The profile was never customized for Engine | Say so once at the start. Use the defaults in `CUSTOMIZE.md`, and record the gap |
| The approver for write-back cannot be named | The profile has no `## Launch Plan` section | Stop write-back. Run plan mode only until the owner is named in the profile |

---

## Best Practices

- Run plan mode first, every time. A plan that has been checked before results arrive is the easiest one to trust after they do.
- Write each sprint's kill rule before the sprint starts. A kill rule set after the results is a negotiation.
- Keep the backup for every owner current. A backup who has never done the task does not count as a backup for the vacation test.
- Count the people lost at each stage before looking at any rate. The largest loss in people is the one that moves the goal.
- Quote every grade from the hand-off, character for character. A grade that drifts between documents becomes a fact nobody checks again.
- Write the Narrative in the buyer's problem first. The shift and the stakes carry the sequences, and the possible world comes last.
- When a number is illustrative, say so next to the number, every time it appears.

---

## Integration With Other Skills

- **Reads from `gtm-launch`:** Part A and Part B, by the field names in the Input Contract. Engine reads both parts. Part A carries the plan inputs, and Part B carries the performance results.
- **Reads from `gtm-positioning`:** the Economics status words, the Open bets, and the Message set, by those names, with each grade word quoted as written. Engine reads the archetype from Discovery, and the economics and open bets from Positioning.
- **Reads from `gtm-discovery`:** the Customer archetype field, with its confidence.
- **Hands to the next Engine sprint:** the Backlog rows with a status of Queued, Held or Re-score, the Sprint record and the Retrospective, by those names.
- **Hands to the next Launch run:** the Retrospective and the Re-grade requests. Launch 2.0 does not read these fields today, so a later Launch patch must add that read before it is used.
- **Hands to Discovery and Positioning:** the Re-grade requests and the Open bets returned. Each skill decides each grade itself.
- **`/weekly-review`** lists the Backlog items past their dates, the Sequences with no owner and the Metrics board rows with no owner.
- **`/dream`** archives a Growth System section that a newer one replaces.
- **Re-run** when Launch writes a new Part A or Part B, when Positioning changes an economics status or the open bets, and when a Re-grade request is applied upstream, because the Unknown inputs in the backlog change with the grade.

---

## Changelog

### 2.0.0 (2026-10-16)

- Ground-up rewrite on the vacation-test rule: the hardest move in go-to-market is from heroic effort to a system that runs, and the test is whether it survives the main operator going on vacation for two weeks.
- Reads Launch's Part A and Part B by name. A plan-only run reads NOT RUN for the retrospective.
- Scores every backlog item with one Guild score, Impact × Unknown ÷ Effort, where Unknown follows the evidence grade. Both the backlog and the conversion items use this score.
- Adds the vacation test as its own stage, graded PASS, NOT YET or FAIL for each output.
- Finds the bottleneck by the count of people lost, with its rate and n.
- Writes re-grade requests for the owning skill instead of changing grades. Takes every cap and kill date from Launch and does not change them.
- Drops the content pillar list, the publishing calendar and the channel expansion plan, because Launch's content plan and motion decision own them.
- Carries no outside credit.
- The 1.x version stays in history.
