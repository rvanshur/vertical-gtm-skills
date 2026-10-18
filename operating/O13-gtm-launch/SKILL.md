---
name: gtm-launch
version: 2.0.1
description: "Turns a position that survived its test into a dated launch plan: one scored motion decision, every channel capped with a kill date, a ranked proof stack, a staffed war room and the funnel targets that Engine measures against. Reads Positioning's hand-off and Discovery's archetype, and writes the plan to the knowledge base."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [launch, launch-plan, motion-decision, channel-caps, kill-rules, proof-stack, war-room, funnel-targets, content-plan, experiments, operating-discipline]
requires:
  skills: [gtm-positioning, gtm-discovery]
mutating: true
change_log:
  - version: 2.0.1
    date: 2026-10-18
    summary: "Results mode reads Engine's hand-off by name: Retrospective, Re-grade requests and Open bets returned. Launch applies only the re-grade requests addressed to gtm-launch, records returned bets in its Open-bet test results, and forwards the rest to their owners unchanged. No other stage changes."
  - version: 2.0.0
    date: 2026-10-16
    summary: "Ground-up rewrite. Starts from Positioning's hand-off and stops on a failed position or a failed threshold. Motion chosen from a five-motion score, one or two lead. Every unproven channel capped at 30% with a 30-day kill rule and a reserve. Four-tier proof ladder, with permission recorded before any customer is named. Economics status carried into the plan, and a 'not run on real data' status sets a capped-experiment limit. Grades are carried from the upstream hand-off unchanged. The hand-off is split into Part A, the launch plan written before launch, and Part B, the launch results written at the day-30 review. The 1.x version stays in history."
---

# Launch

## Overview

Launch answers one question after Positioning has handed over a position: **what dated, budgeted plan puts this position in front of buyers, and how will the team know within thirty days which parts are working?**

The skill runs in eight stages. It reads Positioning's hand-off and Discovery's archetype, and it refuses to launch a position that failed its test. It scores five motions and picks one or two of them to lead. It works the funnel backward from the revenue goal and checks the goal against the sales cycle. It stacks proof by strength and shows whether each piece has permission to be used. It caps every unproven channel, gives each one a kill date, and staffs a five-role war room. The plan is written in two parts. Part A is the plan, written before launch. Part B is the results, written at the day-30 review. Engine measures the real results in Part B against the plan in Part A.

**Core Principle:** A launch is a system, and it runs on a position that survived its test. A launch planned on an untested position is a guess with a calendar date attached.

---

## Why This Skill Exists

Most launches are a date on a calendar. A team picks a day, spreads the budget across five channels, and finds out on launch day which parts were never built. Article 51 puts the ratio plainly: a launch is 80% preparation and 20% execution. When a team flips that ratio, launch day becomes the day it discovers what it skipped. A budget spread across five channels also executes none of them well, which is why the skill makes the team choose one or two motions.

The second failure is a launch that runs on a claim nobody tested. The plan reads the claim as settled, the money follows the plan, and the claim turns out to be false after the budget is spent. This skill keeps the grade of every claim visible, and it refuses to use an `assumed` claim as proof.

The third failure is a channel that survives because it feels right. Without a count set before launch, nobody can say when a channel has failed. This skill writes the signal and the kill date into the plan before the first dollar is spent.

---

## Role

The agent is a launch planner who works only from the position and the evidence it is given. It plans and it reports. It refuses to:

- Launch a position that failed its test, or an economics threshold that failed.
- Lower the revenue goal, or raise a conversion rate, to make a funnel fit.
- Count a customer as named when no permission is recorded.
- Put more than 30% of the budget into a channel with no recorded result.
- Write launch copy that says the price pays back before the economics status is pass.
- Report a war room rehearsal that exists only in a plan.
- Change a grade that the upstream hand-off gave. It quotes the grade and keeps the note beside it.
- Write a dollar amount or a date that has not been committed. It marks the field [RECORD before launch] instead.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Positioning hand-off: Message set, Positioning statement, Value proposition, Proof ledger, Price and value metric, Economics, Open bets | Required | Read by these exact names. If any field is missing, stop and say so, and point the team to `gtm-positioning` |
| Customer archetype (from Discovery) | Required | Read by name from Discovery's archetype node. Positioning does not carry the archetype, so Launch reads Discovery directly. A candidate archetype is allowed, and every output labels it as a candidate |
| Revenue goal and window | Required | A number and the two dates it is measured between. Launch checks the goal against the funnel and never lowers it quietly |
| Committed resources (launch budget in dollars, people, dates) | Required | Plan only on what is committed. Hoped-for resources are listed as risks, not as inputs. A launch budget or date that is not committed is marked [RECORD before launch] |
| Names for the five war room roles | Required for the quality bar | A blank role is reported as unnamed, and the plan does not pass |
| Permission records for named customers | Required for proof tier 1 | Without a recorded permission, a customer is not counted as named |
| Cost inputs: gross margin, acquisition cost per won customer, retention | Needed to move economics off "not run on real data" | Missing inputs are named in the plan, never filled with a guess |
| Engine hand-off: Retrospective, Re-grade requests, Open bets returned | Required for a Results run that follows an Engine run, absent otherwise | Read by these exact names from Engine's hand-off block. Launch applies only the re-grade requests whose source skill is `gtm-launch`, to the field each one names. A request addressed to another skill is forwarded to that skill unchanged. A returned bet is recorded in Open-bet test results with the rule and the result Engine quoted |

---

## Output Contract

Engine reads these fields by name. Keep the names exactly as written. The output has two parts, and Engine reads both. Part A is written before launch, and Engine reads it for plan inputs: the launch budget, the team and roles, the motion decision and the other plan fields. Part B is written at the day-30 review, and Engine reads it for performance.

**Part A, Launch plan (written before launch)**

| Field | Where It Lives | Notes |
|-------|----------------|-------|
| Motion decision | Motion node, and the `## Launch Plan` section of the profile | The archetype used and its confidence, the five scores with their criteria, the lead, experiment and deferred motions, and the reason for each |
| Kill rules per channel | Channel node | Motion, budget share, signal, start date, kill date and redeploy rule for each channel. The reserve is its own row |
| Proof stack | Proof node | Ranked rows, each with tier, source, Positioning grade, launch treatment and permission status |
| Content plan | Content node | Each item dated and assigned to a named person |
| Roster | Roster node | The five roles, each with its name, escalation path and numeric response target. Part of the Engine input "Team resources", with the launch budget |
| Funnel targets | Funnel node | Three scenarios, each rate with its n and its source label. Launch measures these against the growth goal, which Engine takes from the profile (see below) |
| Economics status | Economics node | Pass, fail or not run on real data for each threshold, carried from Positioning, plus the cost ceiling |
| Experiments | Experiments node | Each open bet, its test, its n threshold and its kill rule. Includes the kill condition for T1 |
| Launch budget | Launch plan node | The dollars committed to the launch, split by channel and the reserve. Part of the Engine input "Team resources". [RECORD before launch] until committed |
| Launch date | Launch plan node | The calendar date of launch day. It sets the day-30 review date. It is Launch's own date and is not the Engine growth goal timeline, which comes from the profile. [RECORD before launch] until committed |

**Part B, Launch results (written at the day-30 review)**

| Field | Where It Lives | Notes |
|-------|----------------|-------|
| Launch data | Results node | One line per channel: channel, motion, budget spent in dollars, result count with its n, the decision (keep, extend once or cut), and the rule applied (kill date, volume check or cost ceiling). Also the reserve released, in dollars |
| Current customers and retention | Results node | Won customers as a count with its n, retention in months from the first cohort, and the reasons customers stayed or left as the buyers stated them, each with its count, all with a source label. Before any customer has stayed or left, the reasons read "none recorded yet" |
| Open-bet test results | Experiments node | One line per test that resolved: bet ID, test run, n reached, result, the new grade word the result supports, and the action on the plan |
| Conversion rate, with n | Results node, per channel in Launch data | Conversions over contacts reached, stated as a rate with its n. A conversion is the signal named for that channel in Stage 6 (for example, a first conversation booked). A rate with n below five is an observation |
| Lead quality, with method, judge and n | Results node, per channel in Launch data | How each lead was judged to be a good lead (the method, for example a written checklist), who did the judging, and how many leads were judged (n) |
| Economics status (day 30) | Economics node | The three threshold words once the cost inputs are recorded, plus the cost ceiling checked against any won site |

**Engine inputs that come from the profile, not from Launch.** Launch does not supply these, and the plan does not claim to:

- **Growth goal and timeline.** The company's own growth goal and the timeline it is measured over. Launch reads the revenue goal and window from the profile and measures its funnel against them. It does not set them.
- **Client profile.** The Company, ICP, Buyer Personas, Proof Points and related sections of `profiles/client-profile.md`, which Engine reads from the profile when it exists.
- **Team time.** The hours per week the team can give to growth work after launch. It is a fact about the team, recorded in the profile, not a launch result.

The Launch brief links to these nodes. It does not copy them. The Stage 8 hand-off block quotes every Part A field in full, and it names every Part B field.

---

## Context

The skill reads these, in this order:

1. **The client profile**, `profiles/client-profile.md`. It reads these sections: `## Launch Plan` (this skill's section, written by `CUSTOMIZE.md`), `## Positioning` (the knowledge base path, the owner of the launch decision, the approval line, the economics thresholds and the price test channel), `## Company`, `## Buyer Personas`, `## Competitive Landscape` and `## Proof Points`.
2. **Positioning's hand-off**, read by its names: Message set, Positioning statement, Value proposition, Proof ledger, Price and value metric, Economics and Open bets. Read it from the knowledge base if the nodes exist. Otherwise use the hand-off text that the team pastes in.
3. **Discovery's archetype node**, read by the name Customer archetype.
4. **Engine's hand-off**, when one exists, read by the names Retrospective, Re-grade requests and Open bets returned. It is read only in Results mode, after Engine has run against this plan.

If the profile has no `## Launch Plan` section, say so once at the start of the run, use the defaults in `CUSTOMIZE.md`, and list every write-back before anything is written. If the profile is uncustomized in other ways, say that once as well.

---

## Core Workflow

The order is fixed. Each stage ends with what it produces. The position comes first because every later choice is built on it. The motion comes before the channel, because a channel picked before its motion is a guess about the wrong thing.

### Stage 1. Read the Position and Set the Limits

- Check that every hand-off field is present, by its name: Message set, Positioning statement, Value proposition, Proof ledger, Price and value metric, Economics and Open bets.
- Read the status word for each economics threshold: pass, fail or not run on real data. Read the word, never the illustrative number printed beside it.
- **A failed position test or a failed threshold stops the launch.** The plan names the upstream stage to return to. A statement or price problem goes back to Positioning. A beachhead or archetype problem goes back to Discovery.
- **A "not run on real data" threshold sets a limit.** The launch may run only as capped experiments, and no channel scales spend until the missing inputs are recorded. Missing cost inputs (gross margin, acquisition cost, retention) are named in the plan, never filled with a guess.
- Launch copy may not say the price pays back until the status is pass.
- Quote each grade word exactly as the hand-off gives it. Launch does not regrade a claim up or down.

*Why first:* a launch is only as sound as the position it runs on. A plan written before this check is written on a guess.

**Produces:** the launch input record, one line per field, each with its status.

### Stage 2. Read the Archetype and Frame the Motions

Read Discovery's Customer archetype and its confidence. The leading archetype sets the first motion. If the archetype is a candidate, every output that uses it says "candidate".

| Archetype (Discovery's name) | Motions that lead | First proof to get | Launch mistake to avoid |
|------------------------------|-------------------|--------------------|-------------------------|
| Enterprise | Account-based outbound to a named target list, with executive relationships | A named reference from a paid pilot | Adding sellers before pilots convert |
| SMB Community | Community-led and partner-led: referrals and association events | Share of new customers from referrals (the article target is 40% to 60%, which is a target, not a result) | Scaling sales before community momentum exists |
| Product-Led | Product-led, with inbound from the activation path | Activation rate (the article target is 60% or more) | Launching before activation is fixed |
| Embedded Fintech | Partner-led (the processor or bank), plus adoption inside existing customers | Payment adoption rate (the article target is 60% to 80%) | Launching payments before compliance is in place |
| Marketplace | One side first, in one city or one category | Share of searches with five or more results (the article target is 80% or more) | Launching both sides at once |
| Hybrid | The leading archetype's motion only | Nothing from the second motion until the first is at scale | Launching every motion at once |

**Produces:** the motion frame, with the archetype, its confidence and the leading archetype if the archetype is a hybrid.

### Stage 3. Score the Five Motions and Choose

Score inbound, outbound, product-led, community-led and partner-led on four criteria, each from 1 to 5:

1. Impact.
2. Resource match.
3. Time to first result.
4. Scalability.

- A motion's score is the average of its four criteria. Show every criterion beside the average, so a reader can see what drove it.
- **Lead:** the top one or two motions. Never more than two. If two motions tie for second place, the plan names the tie, and the motion with the shorter time to first result leads.
- **Experiment:** one further motion with a named test, an n threshold and a kill date.
- **Deferred:** every other motion, with a note on what would bring it back. For example: "returns when its cycle is seen, not assumed."
- Scores are judgements until a recorded result exists, and the plan labels them that way.
- Motions are chosen before channels. Channels are picked only inside the chosen motions.

*Why this order:* a score given to a motion the archetype does not support is a score for a motion the customer will not buy through.

**Produces:** the motion decision, with the five scores, the criteria, and the reason for each lead, experiment and deferred motion.

### Stage 4. Work the Funnel Backward and Check the Window

- Work backward from the revenue goal: contracts, then qualified opportunities, then conversations, then outreach or visitor volume.
- Build three scenarios: conservative, base and optimistic. Show which rate moves the goal the most.
- Every rate shows its n and a source label: team record, profile model, research estimate or illustrative. A rate with n = 0 is labelled as such.
- **Window check.** If the sales cycle in the profile or the archetype is longer than the window, the funnel must start from pipeline that already exists. If that pipeline is empty, the goal cannot be met inside the window. The stage says so, instead of adjusting a rate to make the funnel fit.

*Why this check comes here:* the window decides whether any funnel arithmetic is possible at all, so it runs before the funnel is trusted.

**Produces:** funnel targets for each lead and experiment channel. Engine compares these with actual results.

### Stage 5. Stack the Proof, Strongest Real Tier First

The proof ladder has four tiers, as the public page and article 51 publish it:

| Tier | Proof | Counts only when |
|------|-------|------------------|
| 1 | A named customer on the record | A named source and a recorded permission |
| 2 | A quote | A recorded quote with its source and its permission |
| 3 | A logo | A logo with its permission |
| 4 | A claim | Shown with its Positioning grade: assumed, heard, seen or confirmed |

- The launch leads with the highest tier that passes its check.
- **A claim graded `assumed` may appear only as a labelled bet.** It never serves as proof.
- Pilot-only proof is labelled pilot-only.
- **The grade comes from the upstream hand-off, unchanged.** Launch quotes each grade word as Positioning wrote it, and it keeps the note Positioning attached. An illustrative scenario stays labelled as one in every copy that uses it. A demonstration graded `seen` is shown with its `seen` grade and its illustrative-scenario note, and an illustrative number is never presented as a customer result.
- Each row shows its tier, its source, its Positioning grade, its launch treatment and its permission status.
- **Named customers.** A customer is named only with a recorded permission. Until then, a customer is referred to by a neutral label, such as "beta cemetery 1", and it is not counted as named.

*Why:* a launch that leads with its best-sounding proof, rather than its strongest proof at the grade it actually holds, gets caught the first time a buyer asks for the source.

**Produces:** the proof stack, ranked.

### Stage 6. Set Caps, Signals and Kill Dates for Every Channel

For each lead and experiment channel, write one row: motion, budget share, signal, start date, kill date and redeploy rule.

- **Unproven channel.** A channel with no recorded result from this company. Any unproven channel gets no more than 30% of the budget.
- **Reserve.** Budget not allocated to a channel is held in reserve and is not spent until a channel has a recorded result. Three channels at the cap give 90%, so a fourth proven channel is needed to spend the full budget. The reserve is shown as its own row, not hidden.
- **Signal.** Defined before launch as a count, such as booked first conversations. A channel with no signal at its kill date is killed, and its money moves to the reserve or to a proven channel.
- **Volume check.** A channel with fewer than five contacts at its kill date reports "not tested at volume". That is a finding, not a pass and not a kill. It may be extended once, and only if it stayed under its cap. Otherwise it is killed.
- **Cost ceiling.** Acquisition cost per won site may not exceed the payback limit at the price and gross margin that Positioning recorded. The ceiling is the payback limit in months times the monthly gross profit per site. A channel above the ceiling at its kill date is killed, even when it has a signal.
- **Experiments.** Each open bet the plan depends on becomes an experiment with a named test, an n threshold and a kill rule. A bet in "do not build on" appears only as an experiment. It never sets a channel, a message or a proof claim. A bet the plan does not depend on is not an experiment, and it is not used.
- **Day 30 review.** At day 30, each channel is kept, extended once under the volume check, or cut under the cost ceiling and kill rules. The review writes the budget spent, the result count with its n and the decision for each channel into Part B, Launch data. Each experiment that resolves is written into Part B, Open-bet test results, with its new grade word.

*Why a 30-day kill rule:* a channel with no signal after a month has no evidence it will produce one, and the money waits in reserve for a channel that has.

**Produces:** the channel table with caps, signals and kill dates, the reserve row, and the experiment table.

### Stage 7. Staff the War Room and Build the Launch Assets

**War room.** Five roles, each with a name, an escalation path and a numeric response target:

- **Commander.** Makes the launch-day calls, logs each decision with its time, and escalates to the launch day owner.
- **Customer Response.** Answers buyer and prospect questions. Routes product faults to the Technical Monitor and pricing or contract questions to the Commander.
- **Technical Monitor.** Watches the sign-up, demo and form paths for faults, acknowledges each one, and passes any fix decision to the Commander.
- **Social Monitor.** Watches public mentions and replies to each one. Passes questions that need an answer to Customer Response.
- **Content and Comms.** Owns every public wording, every correction and every change to a published page. Escalates to the Commander.

Numeric response targets: social mentions are answered inside 15 minutes. The other targets are numbers set in this stage and confirmed by the launch owner. A target with no number does not get hit, and a number with no owner does not get met.

**Launch assets.**

- **Site and demo blueprint.** Each section names the proof tier it uses. A section that uses a tier 4 claim says so on the page, with the claim's grade and its illustrative note where the grade carries one.
- **Launch email framework.** A three-part structure written from this skill's own rules, with no outside method behind it:
  1. Open on the buyer's problem, in the buyer's own words, in one or two sentences.
  2. Show the strongest proof tier the launch really holds, with its grade. Name a customer only when a permission is recorded.
  3. Make one ask, with one date.

**Content plan.** Each item is dated and assigned to a named person. An item with no named owner is written as NOT ASSIGNED, and the plan fails until it has one.

**Produces:** the roster, the asset blueprint and the dated content plan.

### Stage 8. Rehearse, Write It Back and Hand Off

- **Rehearse the war room twice.** Each rehearsal is recorded with its date and the gaps it found. A rehearsal that is only planned does not count.
- **Check the quality bar** (below), and report every item that fails, with what would close it.
- **Write back to the knowledge base**, after the approval step in Modes: the motion decision and why, the kill rules per channel, the proof stack with its sources, the content plan dated and assigned, the roster, the funnel targets, the economics status, the experiments, the launch budget and the launch date. Engine reads these.
- **Profile section.** The `## Launch Plan` section, with five fields: what is launching, the motion, the revenue goal and window, the launch day owner, and the launch budget.
- **Hand-off block for Engine, in two parts.** Part A, Launch plan, is written before launch. It quotes every Output Contract field in full, with no ID-only entries and no "see above" pointers. Part B, Launch results, is written at the day-30 review. Its fields are named in full. Engine reads both parts: Part A for plan inputs and Part B for performance.

**Produces:** the nodes, the profile section and the two-part hand-off block.

---

## Modes

- **Plan (default).** Runs Stages 1 to 7 and reports the plan in the brief. It writes nothing.
- **Write-back.** Runs the Stage 8 writes. Before anything is written, the owner named in the profile's `## Positioning` section approves the motion decision and the channel caps in the brief. Nothing is written until that approval is recorded in the brief.
- **Results.** Runs at the day-30 review and writes Part B only. It needs the approval recorded in the brief, the same as write-back. When Engine has already run against this plan, Results also reads Engine's hand-off by name. For each re-grade request whose source skill is `gtm-launch`, it changes the grade word on the named field, quotes the result and its n, and records the rule Engine applied. Requests addressed to Positioning or Discovery are forwarded to that skill unchanged. Each returned open bet is written into Open-bet test results with the kill rule and the result Engine quoted. Launch does not re-score the retrospective. It reads the decision per channel and carries it into Launch data.

Re-run the plan when Positioning changes the message set, the price or an economics status, and when a permission is recorded or withdrawn, because the proof stack depends on it.

---

## Epistemic Rules

- **n beside every rate,** with its source label.
- **Five before a pattern.** Below five cases, a number is an observation, and the sentence says so.
- **Silence is not a no.** A contact with no recorded answer leaves the rate's denominator. It is not counted as a no.
- **"No difference" is a finding.** Report it as one, so no one writes a playbook the evidence does not support.
- **The grade ladder:** assumed means someone believes it. Heard means a buyer said it. Seen means it shows up in the company's own deals or data. Confirmed means it held across at least five cases with nothing contradicting it.
- **Grades come from the upstream hand-off.** Launch quotes them and does not regrade. An illustrative result is not a customer result, and its note stays beside it. The one exception is a re-grade request from Engine that names `gtm-launch` as the source skill: Launch owns that field, so Launch applies the change and records the result and n that justified it.
- **Scores are judgements** until a recorded result exists.
- **Targets are numbers.** "A quick response" is not a target.

---

## Hard Rules

1. **No launch on a failed position.** A failed position test or a failed threshold stops the plan, because a launch on a failed test is a launch on a guess. The plan names the upstream stage to return to. Never tune a number to clear a gate.
2. **"Not run on real data" is not a pass.** It sets a capped-experiment limit, and no launch copy claims payback before the status is pass.
3. **Downstream refuses `assumed`.** A claim graded `assumed` may appear only as a labelled bet, because a bet that reads like a fact gets built on.
4. **Motion before channel, and two lead motions at most.** A budget spread across five channels executes none of them well.
5. **No more than 30% on any unproven channel, with a 30-day kill rule.** The cap limits what an untested channel can lose, and the kill rule moves the money when the signal does not come.
6. **Strongest proof first, and permission before a name.** A customer is named only with a recorded permission, because a named customer who never agreed is a relationship problem the launch created.
7. **The archetype branches the motion, and a candidate stays labelled.** A thin archetype gives a motion choice that is still a guess, and the label keeps that visible.
8. **Illustrative is not a result.** The grade comes from the upstream hand-off, and the illustrative note stays beside it. A demonstration or pilot number is never cited as a customer result.
9. **Rehearsal is recorded.** A plan is not a rehearsal, so the quality bar cannot pass on a rehearsal that exists only in a plan.
10. **The hand-off quotes in full.** Engine cannot check what it cannot read, and an ID alone cannot be checked.
11. **No committed figure is invented.** A launch budget or a launch date that has not been committed is marked [RECORD before launch], and the plan does not pass until it is recorded.

---

## Quality Bar

A Launch plan is done when every item below is true. Run the list in order, and report every item that fails, with what would close it.

- [ ] One or two motions were chosen by score. The rest are labelled as experiments or deferred.
- [ ] Budget guardrails are written down: no more than 30% on any unproven channel, a 30-day kill rule per channel, and a kill date on each row.
- [ ] The launch leads with its strongest proof at the grade the hand-off gives it, with that grade and its note in the copy, and every named customer has a recorded permission.
- [ ] All five war room roles have a name, an escalation path and a numeric response target.
- [ ] The war room was rehearsed twice, and both rehearsals are recorded with their dates.
- [ ] The economics status is stated, and any "not run on real data" limit is written into the plan.
- [ ] Every open bet the plan depends on has an experiment with a test, an n threshold and a kill rule. Each experiment that the plan depends on has a kill condition that ends it or re-runs the decision it supports.
- [ ] Part A is complete: the launch budget in dollars and the launch date are recorded, and no [RECORD before launch] marker remains.
- [ ] Part B names every launch-results field, and the day-30 review is the only writer of its values.

---

## Examples

### Example 1. PlotIQ, Full Run (Continues Positioning 2.0.1)

PlotIQ is the example company. The input is Positioning 2.0.1's PlotIQ hand-off, quoted in full in Stage 1. Every number that is not in that hand-off, the profile or article 51 is labelled illustrative. Where the hand-off gives a grade to an illustrative item, that grade is carried unchanged. PlotIQ has not launched. Part B is therefore shown as an empty template.

**Stage 1. The hand-off, read by its names and status words.**

The hand-off below quotes, in full, every field Launch reads from Positioning 2.0.1's PlotIQ Stage 8 hand-off block: the five text fields, the economics status words, and the open bets. The Message set includes its six why-not answers, quoted in full.

> **Positioning statement:** "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery."
>
> **Value proposition:** "State-format trust and plot reports, produced from the customer's own ledger." Specific: pass. Desirable: pass in part, with A2 and P1 labelled as hypotheses, both `assumed`. Credible: pass on C2, `seen`, n=2, illustrative scenario, with no pilot outcome cited. Unique: pass, narrowly.
>
> **Proof ledger (every row, with grade and status):**
> - R1. An annual state trust filing is required. `seen` on the rule text, illustrative state. Source dated 2026-03-27, past the 30 day window for `seen`, so re-check before any external use.
> - C1. Unsold plots found from paper records. `assumed`. Pilot-only and illustrative (212 plots, one site). A bet.
> - C2. State-format trust and plot reports, produced from the customer's own ledger. `seen`, n=2, illustrative scenario. In the statement and the pillar.
> - C3. Records a state auditor accepts. `assumed`. Pilot-only and illustrative (zero findings, one site). A bet.
> - C4. A plot answer in 20 seconds, not 20 minutes. `assumed`. No proof. A bet.
> - C5. Pre-need leads worked within an hour. `assumed`. No proof. A bet.
> - C6. Live in six weeks. `assumed`. A plan, not a result. A bet.
> - C7. Year one under the approval line, one site. `assumed`. Arithmetic on the modeled price, $15,788. Holds for one site only.
>
> **Message set:**
> - **Pillar (one):** "Plot and trust reports in the state's own format, from the customer's own ledger." Tied to C2, graded `seen`, n=2, illustrative scenario. It is the only claim with `heard` or `seen` proof.
> - **Why-not answers (six), quoted in full:**
>   - (1) Paper maps: "Paper keeps the record, but not the plots you could sell. How many could you sell today if the records were right?"
>   - (2) A spreadsheet: "A spreadsheet holds the list, but it does not produce the state's report format. What does the trust report cost you to assemble by hand each year?" The cost of that assembly is not recorded, so this answer stays provisional.
>   - (3) The groundskeeper's memory: "One person knows where everything is. That works until they leave."
>   - (4) Enterprise mapping (Stonemark): "It runs about $1,500 to $2,500 a month (research estimate, not checked) and takes 90 to 120 days to go live (research). Our six-week go-live is a plan, not a result."
>   - (5) Legacy on-premise system (Oldgate): "Upfront cost and yearly maintenance are heavy (research estimate, not checked). This product runs in the cloud and on mobile." No talk named this alternative (0 of 4), so the answer is kept for the sales team only, and the cloud and mobile part is product scope, `assumed`.
>   - (6) Doing nothing: "Unsold plots and audit exposure stay where they are." This answer stays provisional until N1 is recorded.
> - **One-sentence version:** "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery, at $899 a month per site."
> - **Thirty-second version:** "When a state asks for a trust fund report, a cemetery that keeps its records on paper can be looking at a search through a binder. PlotIQ produces that trust fund report in the state's own format, from the cemetery's own ledger, and it keeps the plot records in the same system. Two beta general managers have watched it do that. It costs $899 a month per site, plus a one-time setup fee."
>
> **Price and value metric:** "$899 per site per month, plus a $5,000 one-time setup per account. Value metric: per cemetery site. Modeled, not yet tested with buyers (past-behavior test, 0 of 5 held). Year one: one site $15,788, under the $25,000 line. Two sites $26,576, over the line. The start is one-site buyers."
>
> **Economics (per site, each threshold with its inputs):**
> - Lifetime value to acquisition cost above 3 to 1: not run on real data. Illustrative: 5.8 to 1 (34,522 / 6,000), pass.
> - Payback under 12 months: not run on real data. Illustrative: 8.3 months (6,000 / 719.20), pass.
> - Gross margin above 70%: not run on real data. Illustrative: 80%, pass.
> - Missing inputs to close: gross margin from cost data, acquisition cost from spend divided by won deals, and retention from the first cohort.
>
> **Open bets:** Discovery 2.1.0's three parts, carried with the same IDs and text, then Positioning's additions.
> - **Load-bearing (Discovery):** A2, paper maps are the pain (`assumed`, observation, 4 of 4, n=4). A3, start with independent cemeteries (`assumed`, observation, n=4). A5, a GM can carry a deal over $25K past the board (`assumed`, carries the close plan).
> - **Do not build on (Discovery):** A6, staff resistance is what stalls deals (`assumed`). B1, buyer comfort with software (`assumed`).
> - **Other open bets (Discovery):** P1, the GM keeps the trust fund records and the state filing (`assumed`). A4R, the GM decides with the pre-need manager championing the tool (`assumed`). N1, the do-nothing count (not recorded). T1, the SMB Community ten-deal test (0 of 10 closes recorded).
> - **Positioning additions, each with its reason:**
>   - PA1. The setup rule is per account and not yet confirmed. Reason: it decides which side of the approval line a two-site buyer lands on.
>   - PA2. Cost inputs (gross margin, acquisition cost, retention) are all n=0. Reason: the economics gate is not run.
>   - PA3. Competitor prices are research estimates dated 2026-03-27, not checked. Reason: the anchor and two why-not answers use them.
>   - PA4. The past-behavior price test is at 0 of 5. Reason: the price stays modeled until it runs.
>   - PA5. Pilot outcomes C1 and C3 are illustrative and `assumed`. Reason: they cannot be cited, and they cannot be pillars.
>   - PA6. The C2 demonstration is graded `seen`, n=2, on the basis of two beta general managers watching the report. Reason: the profile does not yet record it, so a real team writes the grade only after it has the record.
>   - PA7. R1 needs a re-check, and the trend date needs a refresh. Reason: the rule text and the research are dated 2026-03-27, past the re-check window.
>   - PA8. X1, the one-system claim. Reason: it rests on product scope.
> - **Do not build on:** A6 and B1, as Discovery wrote them. Positioning adds no claim to this list. The statement does not depend on A5, which is in Discovery's `Load-bearing:` list, because the one-site price sits under the line. A2, A3 and P1 appear only as labelled hypotheses.

What Launch takes from this:

- The economics status words are "not run on real data" for all three thresholds. The launch is a capped experiment with a limit, and no spend scales until the cost inputs are recorded.
- The illustrative "pass" labels in the hand-off are not status words. Launch reads the status, which is "not run on real data".
- The price status is "Modeled, not yet tested with buyers (past-behavior test, 0 of 5 held)." Launch copy does not say the price pays back.
- The load-bearing bets are A2, A3 and A5. A6 and B1 are do-not-build-on, so no channel, message or claim rests on them.
- The illustrative ratios in the copy (5.8 to 1, 8.3 months and 80%) rest on cost inputs that the copy records as n=0 (PA2). They are arithmetic on illustrative inputs, not measured ratios, so each one carries n=0 wherever this example shows it.

**Stage 2. The archetype.** Discovery's leading archetype is SMB Community. It is a **candidate**: 2 of 6 beliefs are graded, and the ten-deal test shows 0 of 10 closes. Every output below says "candidate".

**Stage 3. The motions.** These scores are illustrative judgements. They are not measured, and the plan labels them that way.

| Motion | Impact | Resource match | Time to first result | Scalability | Average | Decision |
|--------|--------|----------------|----------------------|-------------|---------|----------|
| Community-led (referrals from other cemeteries) | 5 | 4 | 3 | 4 | 4.00 | Lead |
| Partner-led (state association events) | 4 | 4 | 3 | 4 | 3.75 | Lead |
| Outbound (independent cemeteries) | 4 | 3 | 3 | 3 | 3.25 | Experiment, capped at 30% |
| Inbound | 3 | 2 | 2 | 3 | 2.50 | Deferred |
| Product-led | 2 | 1 | 2 | 2 | 1.75 | Deferred |

The two leads match the profile's motion section. That agreement is not evidence, because the profile's motion was also written by hand. Inbound is deferred because no inbound result exists for this company yet. Product-led is deferred because the first value needs a human conversation, so it has the weakest resource match.

**Stage 4. The funnel.** The goal is illustrative: four one-site contracts signed within 150 days of launch day.

- At list price, year one is 4 × $10,788 = $43,152. Setup is $5,000 per site for a one-site account under either reading, so four one-site accounts add $20,000 in setup. The per-account question (PA1) changes only two-site totals. The funnel is built on one-site contracts, so it does not depend on PA1. Any two-site quote waits for PA1 (see the experiment table).
- **Window check.** The profile's single-site cycle is 90 to 150 days (research estimate, n not recorded). The 150-day window reaches the top of that range. The four deals must therefore already be in pipeline on launch day. The pipeline count is a requirement of the plan, not a result. Today's count is: [RECORD before launch].

| Scenario | Proposal to signed | Qualified demo to proposal | Proposals needed for 4 contracts | Qualified demos needed | n | Source |
|----------|--------------------|----------------------------|----------------------------------|------------------------|---|--------|
| Conservative | 40% | 40% | 10 | 25 | 0 | Illustrative |
| Base | 50% | 50% | 8 | 16 | 0 | Illustrative |
| Optimistic | 60% | 60% | 7 (6.67, rounded up) | 12 (11.67, rounded up) | 0 | Illustrative |

Both rates multiply, so neither dominates at these values. Both have n = 0, so both are measured first. Outreach volume is not computed, because no outreach rate is recorded. It is a requirement, not a result.

**Stage 5. The proof stack.**

| Rank | Tier | Proof | Source (hand-off row) | Positioning grade (quoted) | Launch treatment | Permission | Check result |
|------|------|-------|-----------------------|----------------------------|------------------|------------|--------------|
| 1 | 4 | State-format trust and plot reports, produced from the customer's own ledger (C2) | Proof ledger C2: illustrative scenario, n=2 | `seen`, n=2, illustrative scenario | Leads, with the illustrative-scenario note in the copy. PA6 tests it | Not applicable, no customer named | Pass at its graded tier |
| 2 | 1 | Unsold plots found from paper records (C1), beta cemetery 1 | Proof ledger C1: pilot-only and illustrative (212 plots, one site) | `assumed` | Labelled bet only. Not counted as named | No permission recorded | Fails. Not counted as named |
| 3 | 1 | Records a state auditor accepts (C3), beta cemetery 2 | Proof ledger C3: pilot-only and illustrative (zero findings, one site) | `assumed` | Labelled bet only. Not counted as named | Permission pending | Fails. Not counted as named |
| 4 | 2 | None recorded | Not applicable | Not applicable | Not available | Not applicable | Not available |
| 5 | 3 | None recorded | Not applicable | Not applicable | Not available | Not applicable | Not available |

The launch leads with C2, the strongest proof the hand-off grades `seen`. It leads with the illustrative-scenario note in the copy, so a reader can see that the scenario is not a customer result. Tier 1 rows do not lead. They stay out of launch copy until a permission is recorded. If PA6 fails its kill rule, C2 drops to `assumed` and the launch leads with no real proof.

**Stage 6. The channels and the reserve.**

| Channel | Motion | Budget share | Signal, counted | Start | Kill date | Redeploy rule |
|---------|--------|--------------|-----------------|-------|-----------|---------------|
| Referrals from other cemeteries | Community-led | 30% (unproven) | A referred GM books a first conversation | Day 0 | Day 30 | Money moves to the reserve or to a proven channel |
| State association events | Partner-led | 30% (unproven) | An event contact books a first conversation | Day 0 | Day 30 | Money moves to the reserve or to a proven channel |
| Outbound to independent cemeteries | Outbound (experiment) | 30% (unproven) | A cemetery GM books a first conversation | Day 0 | Day 30 | Money moves to the reserve or to a proven channel |
| Reserve | None | 10% | Not spent until a channel has a recorded result | None | None | Released to a channel with a recorded result |

Three channels at the cap give 90%. Without the reserve, the plan would have to put 10% into a channel it cannot yet prove, and the rule forbids that. The dollar amount of each row is the launch budget, which is [RECORD before launch].

**Cost ceiling.** At $899 a month and an illustrative 80% gross margin (n=0, PA2), gross profit is $719.20 a month (illustrative, n=0). A payback under 12 months allows $8,630 of acquisition cost per won site (illustrative: 12 × $719.20). Setup is excluded from payback, the same rule Positioning uses. The ceiling cannot be tested until the first won site exists. The margin is not a recorded input, so this ceiling does not clear the economics gate.

**Experiments.**

| Bet | Test | n threshold | Kill rule |
|-----|------|-------------|-----------|
| A5, a GM can carry a deal over $25K past the board (assumed, carries the close plan) | Past-behavior conversations: the last deal over $25K and who approved it | 5 | Three or more of five show a board approved a deal over $25K. Fewer than three means A5 comes out of the close plan |
| A2 and A3, paper maps are the pain (`assumed`, observation, 4 of 4, n=4) and start with independent cemeteries (`assumed`, observation, n=4) | Ask each outbound conversation how a plot is found today, from the outbound channel only | 5 | Fewer than four of five describe a paper lookup. The pain pillar goes back to Positioning |
| T1, the SMB Community ten-deal test (0 of 10 closes recorded). The motion decision reads this archetype | Count closes as they happen | 10 | Reported as "0 of 10" until ten closes exist. If fewer than ten closes are recorded by Day 90, SMB Community is withdrawn as the archetype, the motion decision is re-run from recorded results, and the community-led lead is held with no new budget. No archetype verdict before ten closes |
| PA1, the setup rule is per account and not yet confirmed. It decides which side of the approval line a two-site buyer lands on | The owner writes the setup rule in the `## Positioning` section of the profile, with the year-one total for a two-site account under that rule | 1 written rule | No written rule by Day 30. Then no two-site quote is issued and the two-site figure stays out of all copy. The one-site plan continues |
| PA6, the C2 demonstration (`seen`, n=2, illustrative scenario). Positioning grades it on two beta general managers watching the report | A real team records its own dated demonstration of the state-format report produced from a customer's own ledger. The customer is named only if permitted | 2 recorded demonstrations | Fewer than two recorded by Day 30. Then C2 drops to `assumed`, comes out of the pillar and the lead, and the launch leads with no real proof. The launch copy says so |

No channel, message or claim rests on A6 (staff resistance) or B1 (buyer comfort with software). PA2 and PA4 (the missing cost inputs and the unrun price test) are covered by the economics limit in Stage 1, which holds all spend at a capped experiment until the inputs are recorded.

**Stage 7. The roster, the content plan and the assets.**

| Role | Name (illustrative) | Escalates to | Numeric response target |
|------|---------------------|--------------|-------------------------|
| Commander | Lena Vasquez | Ryan | Decision logged within 60 minutes of escalation (proposed) |
| Customer Response | Owen Pruitt | Commander | Inbound questions answered within 60 minutes (proposed) |
| Technical Monitor | Eli Marsh | Commander | Bug acknowledged within 30 minutes (proposed) |
| Social Monitor | Nadia Brandt | Customer Response | Social mentions answered inside 15 minutes (fixed) |
| Content and Comms | NOT NAMED | Commander | Correction posted within 60 minutes of a confirmed error (proposed). The roster fails the quality bar until this role has a name |

The names are illustrative assignments from the profile's team. The launch day owner is Lena Vasquez, illustrative.

Content plan. Dates are offsets from launch day (L), because the profile does not yet record a launch date. Each offset becomes a calendar date when the launch day is committed.

| Date | Item | Channel | Owner |
|------|------|---------|-------|
| L-21 | Guide comparing PlotIQ with paper plot maps (runs first, per profile) | Site | NOT ASSIGNED. Content and Comms has no name |
| L-10 | Referral note for beta cemetery GMs to forward to peers. Permission check first | Email | Lena Vasquez |
| L-7 | Launch email to independent cemetery GMs, using the three-part framework | Email | Nadia Brandt |
| L-3 | One-page leave-behind for state association events | Print and PDF | Owen Pruitt |
| L-0 | Site and demo live, each section labelled with its proof tier and grade | Site | Eli Marsh |
| L-0 | Launch day public posts and replies | Social | Nadia Brandt |
| L+30 | Day 30 review for each channel, with the volume check and the PA6 count | Internal | Lena Vasquez |

The launch email framework, applied: open on the buyer's problem (unsold plots nobody can find on paper), show the C2 claim with its `seen` grade and its illustrative-scenario note, and make one ask (a 20-minute call on one date).

**Stage 8. The quality bar, checked.**

| # | Check | Result | Why |
|---|-------|--------|-----|
| 1 | Motions chosen by score | Pass | Two lead, one experiment, two deferred, each with its reason |
| 2 | Guardrails written down | Pass | Caps, kill dates and the cost ceiling are in the plan |
| 3 | Strongest proof leads at its hand-off grade, and every named customer has a permission | Pass | C2 leads at tier 4 with its `seen` grade and illustrative-scenario note. Beta cemetery 1 and beta cemetery 2 are not counted as named and stay out of launch copy |
| 4 | Five roles named, with escalation and numeric target | **Fail** | Four of five named. Content and Comms is unnamed |
| 5 | Rehearsed twice, both recorded | **Fail** | Zero of two recorded |
| 6 | Economics status stated, "not run on real data" limit written in | Pass | Three thresholds not run on real data, and the capped-experiment limit is written in |
| 7 | Every open bet the plan depends on has an experiment with a test, an n threshold and a kill rule | Pass | A5, A2, A3, T1, PA1 and PA6 each have all three. T1's kill condition re-runs the motion decision it supports. PA2 and PA4 are covered by the economics limit |
| 8 | Part A complete: launch budget in dollars and launch date recorded | **Fail** | Both are [RECORD before launch]. No committed figure is invented |
| 9 | Part B names every launch-results field | Pass | The template in the hand-off names every field, and the day-30 review fills it. Nothing is filled yet, because PlotIQ has not launched |

**Result: not ready to launch.** Three checks fail, and they close it:

1. Name the fifth role, Content and Comms.
2. Rehearse twice, and record both rehearsals with their dates and gaps.
3. Record the launch budget in dollars and the launch date in Part A.

Two experiments then run against their kill dates. PA1 needs a written setup rule by Day 30. PA6 needs two recorded demonstrations by Day 30. T1 needs ten closes by Day 90, or the archetype is withdrawn. The cost inputs stay on the list, because the economics stay "not run on real data".

**Hand-off to Engine, in two parts.** Part A quotes every Output Contract field in full. Part B is an empty template, because PlotIQ has not launched. It is written at the day-30 review.

```text
HAND-OFF TO ENGINE: PlotIQ, Launch 2.0.0 (illustrative run)

PART A. LAUNCH PLAN (written before launch)

Motion decision
Archetype: SMB Community (candidate). Confidence: candidate, 2 of 6 beliefs graded. Ten-deal test: 0 of 10 closes.
Scores (impact, resource match, time to first result, scalability, average):
- Community-led (referrals from other cemeteries): 5, 4, 3, 4, average 4.00. Lead. Reason: buyers trust referrals from other properties over ads (profile motion section).
- Partner-led (state association events): 4, 4, 3, 4, average 3.75. Lead. Reason: association events earn trust for a cemetery buyer.
- Outbound (independent cemeteries): 4, 3, 3, 3, average 3.25. Experiment, capped at 30%. Reason: the named test is A2 and A3, with a kill date of Day 30.
- Inbound: 3, 2, 2, 3, average 2.50. Deferred. Reason: no inbound result exists for this company yet.
- Product-led: 2, 1, 2, 2, average 1.75. Deferred. Reason: the first value needs a human conversation.

Kill rules per channel
- Referrals from other cemeteries. Motion: Community-led. Budget share: 30% (unproven). Signal: a referred GM books a first conversation. Start: Day 0. Kill date: Day 30. Redeploy rule: money moves to the reserve or to a proven channel.
- State association events. Motion: Partner-led. Budget share: 30% (unproven). Signal: an event contact books a first conversation. Start: Day 0. Kill date: Day 30. Redeploy rule: money moves to the reserve or to a proven channel.
- Outbound to independent cemeteries. Motion: Outbound (experiment). Budget share: 30% (unproven). Signal: a cemetery GM books a first conversation. Start: Day 0. Kill date: Day 30. Redeploy rule: money moves to the reserve or to a proven channel.
- Reserve. Motion: None. Budget share: 10%. Signal: not spent until a channel has a recorded result. Start: none. Kill date: none. Redeploy rule: released to a channel with a recorded result.

Proof stack
- Rank 1. Tier 4 (claim). Proof: C2, "State-format trust and plot reports, produced from the customer's own ledger." Source: Positioning proof ledger, illustrative scenario. Positioning grade: seen, n=2, illustrative scenario. Launch treatment: leads, with the illustrative-scenario note in the copy. Experiment: PA6. Permission: not applicable.
- Rank 2. Tier 1. Proof: C1, "Unsold plots found from paper records" (beta cemetery 1, 212 plots, one site). Positioning grade: assumed. Pilot-only and illustrative. Launch treatment: labelled bet only. Permission: none recorded. Not counted as named.
- Rank 3. Tier 1. Proof: C3, "Records a state auditor accepts" (beta cemetery 2, zero findings, one site. GM on video, permission pending). Positioning grade: assumed. Pilot-only and illustrative. Launch treatment: labelled bet only. Permission: pending. Not counted as named.
- Tiers 2 and 3: none recorded.

Content plan
- L-21. Guide comparing PlotIQ with paper plot maps. Channel: site. Owner: NOT ASSIGNED.
- L-10. Referral note for beta cemetery GMs, after a permission check. Channel: email. Owner: Lena Vasquez.
- L-7. Launch email to independent cemetery GMs, three-part framework. Channel: email. Owner: Nadia Brandt.
- L-3. One-page leave-behind for state association events. Channel: print and PDF. Owner: Owen Pruitt.
- L-0. Site and demo live, each section labelled with its proof tier and grade. Channel: site. Owner: Eli Marsh.
- L-0. Launch day public posts and replies. Channel: social. Owner: Nadia Brandt.
- L+30. Day 30 review for each channel, with the volume check and the PA6 count. Channel: internal. Owner: Lena Vasquez.

Roster
- Commander. Name: Lena Vasquez. Escalates to: Ryan. Target: decision logged within 60 minutes of escalation (proposed).
- Customer Response. Name: Owen Pruitt. Escalates to: Commander. Target: inbound questions answered within 60 minutes (proposed).
- Technical Monitor. Name: Eli Marsh. Escalates to: Commander. Target: bug acknowledged within 30 minutes (proposed).
- Social Monitor. Name: Nadia Brandt. Escalates to: Customer Response. Target: social mentions answered inside 15 minutes (fixed).
- Content and Comms. Name: NOT NAMED. Escalates to: Commander. Target: correction posted within 60 minutes of a confirmed error (proposed).

Funnel targets (goal illustrative: four one-site contracts within 150 days of launch day)
- Conservative (illustrative, n = 0): proposal to signed 40%, qualified demo to proposal 40%. Proposals needed: 10. Qualified demos needed: 25.
- Base (illustrative, n = 0): proposal to signed 50%, qualified demo to proposal 50%. Proposals needed: 8. Qualified demos needed: 16.
- Optimistic (illustrative, n = 0): proposal to signed 60%, qualified demo to proposal 60%. Proposals needed: 7. Qualified demos needed: 12.
- Window check: sales cycle 90 to 150 days (research estimate, n not recorded). The four deals must already be in pipeline on launch day. Pipeline count: [RECORD before launch].

Economics status
- Lifetime value to acquisition cost above 3 to 1: not run on real data.
- Payback under 12 months: not run on real data.
- Gross margin above 70%: not run on real data.
- Price: Modeled, not yet tested with buyers (past-behavior test, 0 of 5 held).
- Cost ceiling (illustrative, not an input): $8,630 of acquisition cost per won site (12 × $719.20, at an illustrative 80% gross margin, n=0 for the margin input, PA2).

Experiments
- A5: a GM can carry a deal over $25K past the board (assumed, carries the close plan). Test: past-behavior conversations on the last deal over $25K and who approved it. n threshold: 5. Kill rule: three or more of five show a board approved a deal over $25K. Fewer than three means A5 comes out of the close plan.
- A2 and A3: paper maps are the pain (assumed, observation, 4 of 4, n=4) and start with independent cemeteries (assumed, observation, n=4). Test: ask each outbound conversation how a plot is found today. n threshold: 5. Kill rule: fewer than four of five describe a paper lookup. The pain pillar goes back to Positioning.
- T1: the SMB Community ten-deal test (0 of 10 closes recorded). Test: count closes as they happen. n threshold: 10. Kill rule: reported as "0 of 10" until ten closes exist. If fewer than ten closes are recorded by Day 90, SMB Community is withdrawn as the archetype, the motion decision is re-run from recorded results, and the community-led lead is held with no new budget.
- PA1: the setup rule is per account and not yet confirmed. Test: owner writes the rule in the profile's Positioning section, with the two-site year-one total. n threshold: 1 written rule. Kill rule: no written rule by Day 30. Then no two-site quote is issued and the two-site figure stays out of all copy.
- PA6: the C2 demonstration (seen, n=2, illustrative scenario). Test: a real team records its own dated demonstration from a customer's own ledger. n threshold: 2 recorded demonstrations. Kill rule: fewer than two recorded by Day 30. Then C2 drops to assumed, comes out of the pillar and the lead, and the launch leads with no real proof.

Launch budget: [RECORD before launch]. Split by channel and reserve: [RECORD before launch].
Launch date: [RECORD before launch]. The day-30 review date is set from it.
Growth goal and timeline: not supplied by Launch. It comes from the profile. Launch's funnel measures against it, with the goal illustrative as four one-site contracts within 150 days of launch day.
Team resources: the roster above, with the launch budget above.
Current customers and retention, and the client profile: not supplied by Launch. Engine reads them from Part B and from the profile.

PART B. LAUNCH RESULTS (written at the day-30 review)

Status: empty template. PlotIQ has not launched. Every value below is blank until the day-30 review writes it. Engine reads this part for performance, together with Part A, which holds the plan inputs.

Launch data (one line per channel, and the reserve)
- Channel: [blank]. Motion: [blank]. Budget spent (dollars): [blank]. Result count with n: [blank]. Decision (keep, extend once or cut): [blank]. Rule applied (kill date, volume check or cost ceiling): [blank].
- Reserve released (dollars): [blank].

Conversion rate, with n (one line per channel)
- Channel: [blank]. Conversions: [blank]. Contacts reached: [blank]. Conversion rate with n: [blank].

Lead quality, with method, judge and n (one line per channel)
- Channel: [blank]. Method: [blank]. Judged by: [blank]. Leads judged (n): [blank]. Quality result: [blank].

Current customers and retention
- Won customers (count, with n): [blank].
- Retention (months, first cohort, with n): [blank].
- Why customers stayed or left (each reason in the buyer's words, with its count, or "none recorded yet"): [blank].
- Source label (team record, profile model, research estimate or illustrative): [blank].

Open-bet test results (one line per test that resolved)
- Bet ID: [blank]. Test run: [blank]. n reached: [blank]. Result: [blank]. New grade word the result supports: [blank]. Action on the plan: [blank].
- Tests due: A5, A2 and A3, T1, PA1, PA6.

Economics status (day 30)
- Lifetime value to acquisition cost above 3 to 1: [blank].
- Payback under 12 months: [blank].
- Gross margin above 70%: [blank].
- Cost ceiling checked against any won site: [blank].
```

### Example 2. A Failure That Goes Back Upstream

**The request.** Sales asks to lead with the multi-location groups (ICP3), because a group deal is bigger. Positioning ranks ICP3 third, as an expansion segment, and the buyer is a CFO who signs through a gate.

**The window check.** The profile's ICP3 cycle is 6 to 9 months (research estimate, n not recorded). Six months is about 180 days, which is longer than the 150-day window in Example 1. The pipeline shows zero group opportunities on launch day (illustrative). The funnel cannot produce a single group contract inside the window, so the goal is out of reach for this segment as planned.

**What the skill refuses to do.** It does not lower the goal to fit the window. It does not raise a proposal rate to fit. It does not assume a shorter cycle because a larger deal is wanted. It does not move outbound budget into group prospects to fill a pipeline that does not exist.

**What the skill does.** It stops the group motion and sends the work back:

1. **To Positioning, Stage 2, question 4** (who cares most about the value). ICP3 is ranked third, and the position was written for independent cemetery general managers.
2. **To Discovery.** The ICP3 cycle is a research estimate, and it is load-bearing for this window. It must be graded before any group launch is planned. Until then, it is an open bet, and it is labelled as one.

Launch continues on ICP1 with the two lead motions from Example 1. The group segment becomes a deferred motion with the note "returns when its cycle is seen, not assumed." The plan records the failure and its upstream route in the Stage 1 input record, so the next run does not start from the same request.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| Every economics threshold reads "not run on real data" | Acquisition cost, gross margin or retention is not recorded | Name the missing input in the plan, and run as capped experiments. Do not enter a benchmark and report the result as a finding |
| The skill refuses to plan | A hand-off field is missing, or a threshold failed | Stop at Stage 1. Send the field or the failed threshold back to Positioning. Do not work around it |
| Two motions score almost the same | The judgement scores are close | Show every criterion beside the average. The tie rule in Stage 3 decides the lead, and the plan says a recorded result would settle it |
| A channel shows fewer than five contacts at its kill date | The channel was not tested at volume | Report "not tested at volume". Extend once only if it stayed under its cap. Otherwise kill it |
| The roster has a blank role | A name was not supplied | Report the role as NOT NAMED. The plan fails the quality bar until it is named |
| The funnel cannot reach the goal in the window | The sales cycle is longer than the window, and the pipeline is empty | Say so. Do not lower the goal, raise a rate, or shorten the cycle to fit |
| A named customer has no permission on file | Permission was not recorded, or was withdrawn | Remove the name from launch copy, and re-run when the permission is recorded |
| A proof row's grade is challenged in review | The grade in the plan differs from the upstream hand-off | Quote the hand-off's grade word again, character for character. Launch does not regrade. Raise the difference with Positioning |
| The archetype is a candidate, and the team wants a verdict | Too few beliefs are graded, or the ten-deal test has not reached ten | Label it a candidate in every output. No archetype verdict before the test is complete |
| The launch budget or launch date is not known | Neither has been committed | Mark the field [RECORD before launch]. Do not estimate either one |
| The brief runs past two pages | The plan was written out in full in the brief | Ask for the two-page brief only. The nodes hold the detail, and the brief links to them |

---

## Best Practices

- Run the launch after Positioning, because a launch planned on a guess is a launch that spends the budget finding out.
- Write the signal and the kill date for each channel before the first dollar is spent. A kill date set after launch is a negotiation.
- Keep the proof stack current. A permission withdrawn today should come off the launch copy today, and the plan should be re-run.
- Use the Stage 7 war room names early, and rehearse with the people who will actually be on the day.
- When a number is illustrative, say so next to the number, every time it appears.
- Leave the reserve visible. A reserve shown on the page is a discipline. A reserve that vanishes into a channel is a decision nobody approved.
- Fill Part B only at the day-30 review. A results block written before the review is a guess about the results.

---

## Integration With Other Skills

- **Reads from `gtm-positioning`:** the hand-off fields Message set, Positioning statement, Value proposition, Proof ledger, Price and value metric, Economics and Open bets, by those names, with each grade word quoted as written.
- **Reads from `gtm-discovery`:** the Customer archetype field, with its confidence.
- **Hands to `gtm-engine`:** Engine reads both parts. Part A carries the plan inputs by name: the eight Output Contract fields Motion decision, Kill rules per channel, Proof stack, Content plan, Roster, Funnel targets, Economics status and Experiments, and also the launch budget and the launch date. Part B carries the performance results by name: Launch data, Conversion rate, with n, Lead quality, with method, judge and n, Current customers and retention, Open-bet test results and Economics status (day 30). Engine's inputs ask for launch data, current customers and retention, team resources, and a growth goal and timeline. Team resources come from Part A, the roster and the launch budget. Launch data, conversion, lead quality and current customers and retention come from Part B. The growth goal and timeline, and the client profile, come from the profile and are not supplied by Launch.
- **Loop:** `/weekly-review` lists channels past their kill date, experiments past their n threshold, and named customers without a recorded permission. `/dream` archives a launch plan that a newer plan replaces.

---

## Changelog

### 2.0.1 (2026-10-18)

- Results mode reads Engine's hand-off by name: Retrospective, Re-grade requests and Open bets returned. Launch applies only the re-grade requests addressed to `gtm-launch`, records each returned bet in Open-bet test results, and forwards the rest to their owners unchanged. One Input Contract row, one Context item and one epistemic sentence added. No other stage changes.

### 2.0.0 (2026-10-16)

- Ground-up rewrite. The skill starts from Positioning's hand-off and stops on a failed position or a failed threshold.
- The motion is chosen from a five-motion score, with one or two leads, one capped experiment and the rest deferred.
- Every unproven channel is capped at 30%, with a 30-day kill rule, a redeploy rule and a reserve row.
- Four-tier proof ladder, with permission recorded before any customer is named. Customers without a recorded permission are referred to by neutral labels.
- Economics status is carried into the plan. A "not run on real data" status sets a capped-experiment limit.
- Grades are carried from the upstream hand-off unchanged, with their notes.
- The hand-off is split into Part A, the launch plan written before launch, and Part B, the launch results written at the day-30 review. Owner decision, 2026-10-16.
- Every open-bet experiment has a kill condition, including T1.
- The Stage 8 hand-off quotes every Part A field in full and names every Part B field.
- The 1.x version stays in history.
