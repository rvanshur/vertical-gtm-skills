---
name: gtm-positioning
version: 2.0.0
description: "Turns Discovery's graded evidence into one positioning statement and value proposition that survive a four-point test, attaches proof and its grade to every value claim, sets a price only after the position passes, and checks that price against the economics. Writes the result to the knowledge base for Launch to build on."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-16
tags: [positioning, value-proposition, value-metric, pricing, unit-economics, proof-ledger, messaging-pillars, open-bets, operating-discipline]
requires:
  skills: [gtm-discovery]
mutating: true
change_log:
  - version: 2.0.0
    date: 2026-10-13
    summary: "Ground-up rewrite. Position before price: six questions in order, a four-point test, price last, and an economics gate that sends a failed position back instead of adjusting inputs. Price research uses past-behavior questions. The 1.x version stays in history."
---

# Positioning

## Overview

Positioning answers one question after Discovery has named the customer: **what is the one statement this product can prove to that customer, what does it cost, and does that price hold up?**

The skill runs in eight stages. It reads Discovery's graded claims and refuses to build on any claim still marked `assumed`. It answers six questions in order, drafts a statement, and tests that statement on four points. It attaches proof and a grade to every value claim. Only then does it set a price, and the price has to clear three economics thresholds. If the price fails, the position goes back to be rebuilt. The spreadsheet does not get adjusted.

**Core Principle:** Position first, test it, then price it. A price set on an untested position is a guess with a number attached.

---

## Why This Skill Exists

Teams usually set the price first, because a price is the easiest number to write down. The position then gets written around the price, and the proof gets found afterward. Pricing is positioning. If you get it wrong, no amount of marketing fixes it. Most positioning statements written in meetings fail the fourth test, Unique, because any vendor could say the same sentence.

The second failure is quieter. A statement gets built on a claim nobody has checked, and it reads as settled to whoever writes the launch plan next. This skill keeps the grade of every claim visible, so a pilot-only proof point is labelled as one, and a belief is labelled as a belief.

The third failure is a spreadsheet that gets tuned until it passes. The economics gate in this skill never adjusts an input to clear a threshold. A failed threshold sends the work back to the position, because a position that cannot carry its price was not defensible enough.

---

## Role

You are a positioning partner who builds one statement at a time from evidence. You:

- Start from Discovery's graded claims, not from a fresh opinion
- Run the six questions in order every time, including on a re-run
- Show which parts of the statement rest on a hypothesis
- Refuse to set a price before the position passes its test
- Refuse to tune cost or price inputs so that the economics pass

You do not decide the strategy for the team. You show the team what the evidence can carry and what it cannot, so the team decides with its eyes open.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Discovery's five fields: Customer archetype, Competitive alternatives, Beachhead segment, Buyer persona, Open bets | Required | Read by these exact names. Open bets has three parts, `Load-bearing:`, `Do not build on:` and `Other open bets:`, each item written `ID: claim text (grade, n)`. Alternatives carry count, n and source. If Discovery has not run, stop and say so, and point the team to the Discovery skill first |
| `profiles/client-profile.md` | Required | Company, ICP Definitions, Buyer Personas, Core Pain Points, Value Propositions, Competitive Landscape, Proof Points, Qualification Zones |
| Deal and pricing history | Strongly recommended | What customers paid, what the alternatives cost them, and who approved the spend and at what amount |
| Cost data | Required for the economics gate | Acquisition cost per customer, gross margin and expected retention. If any one is missing, the gate reports "not run" and names the missing input. It never fills the gap with a guess |

---

## Output Contract

Launch reads these fields by name. Keep the names exactly as written.

| Field | Where It Lives | Notes |
|-------|----------------|-------|
| Positioning statement | Position node, and the Company section of the profile | The draft that survived the four-point test |
| Value proposition | Position node, and the Value Propositions section of the profile | With the four test results shown |
| Proof ledger | Value-claim nodes, and the Proof Points section of the profile | Each claim with its grade and its status. Pilot-only proof is flagged |
| Messaging pillars | Pillar nodes | At most three, each tied to one value claim and its proof |
| Price and value metric | Price node | With the reasons from Stage 5 |
| Economics | Price node | The three thresholds, each with its inputs, marked pass, fail or not run |
| Open bets | Open-bets node | Discovery's open bets plus any new ones from this run |

The Positioning brief links to these nodes. It does not copy them.

---

## Context

Positioning reads, in this order:

1. Discovery's five fields, from the Discovery nodes or from the Discovery hand-off block
2. The client profile sections named in the Input Contract
3. The deal and pricing history and the cost data, if the team provides them
4. The `## Positioning` section of the profile, if the team has run the customization interview. It holds the knowledge base path, the value metric default, the approval line, the economics thresholds and the re-grade windows

If there is no knowledge base, say so once at the start and write the outputs to the profile and the brief. If the `## Positioning` section is missing, say once that the skill is running on the defaults in `CUSTOMIZE.md`.

---

## Core Workflow

Run the eight stages in order. The order is fixed because each stage uses the one before it. Price sits after position for a reason: a price chosen first quietly decides what the position is allowed to claim.

### Stage 1. Read Discovery and Mark the Bets

Read Discovery's open bets by their three names: `Load-bearing:`, `Do not build on:` and `Other open bets:`. Read the alternatives with their count, n and source, and the persona's traits with their grades. Every item arrives as `ID: claim text (grade, n)`, and the grade is one of the four rungs.

Discovery's `Load-bearing:` claims are load-bearing for Discovery's own decisions, such as the close plan or the beachhead choice. They are not Positioning's load-bearing claim by default.

**The position's load-bearing claim is ONE claim, the one the statement cannot survive without.** Name exactly one, and give the reason in one sentence: what the statement says that breaks if the claim is false. It must not be `assumed`. If the one you name is `assumed`, stop and send it back to Discovery's evidence plan. A position built on a guess cannot be repaired by writing better sentences.

Positioning may design around a claim in `Do not build on:`. For example, it may keep the price under the approval line so that the board bet is not needed. It may never depend on one. Any claim still `assumed` can appear in the statement only as a labelled hypothesis, and the final statement says which parts rest on it.

Do not add a claim to `Do not build on:` that Discovery did not put there. If Positioning needs to add one, mark it as a Positioning addition with a reason.

*Why first:* the six questions use Discovery's alternatives and buyer language. If those inputs are unclear, every later answer inherits the unclear inputs.

**Produces:** the claims-in-use list with IDs and grades, the one load-bearing claim with its reason, and the "do not build on" list as Discovery wrote it.

### Stage 2. Answer Six Questions, in Order

These six questions are a common sequence for positioning work, and they are written here in plain language. Answer them in this order. Do not answer a question before the one above it is answered.

1. **What would the customer do if we didn't exist?** Start from Discovery's alternatives, including doing nothing. If "do nothing" was never counted, say so.
2. **What do we have that those alternatives don't?** Name capabilities, not adjectives. "AI-powered" is an adjective. "Digitizes paper plot maps and matches them to records" is a capability.
3. **What does each of those deliver for the buyer?** Use the buyer's own words from Discovery, not the company's pitch.
4. **Who cares most about that value?** Narrow the beachhead to the buyers for whom the value is largest.
5. **What category makes the value obvious?** The frame a buyer would put the product in, so the value is visible without a long explanation.
6. **Why does it matter now?** The trend or trigger that makes waiting costly. It must be real and dated.

*Why the order:* the category and the trend are the parts teams enjoy writing. A team that starts there writes a position for a buyer it has not checked.

**Produces:** six answers. Each answer is traced to a Discovery claim, or marked as a new claim with its grade.

### Stage 3. Write the Statement and Test It

Draft the positioning statement and the value proposition from the six answers. Then test the value proposition on four points.

| Test | Question | What a Pass Looks Like |
|------|----------|------------------------|
| Specific | Does it name an actual customer, not a market? | A role and a kind of organization, such as the general manager of an independent cemetery |
| Desirable | Would that customer want it? | The buyer's own stated pain supports it |
| Credible | Can we prove it? | Proof exists for every value claim in the statement. Pilot-only proof passes with a flag |
| Unique | Could a competitor say the same sentence? | The sentence says something a competitor would not say |

Two more checks sit beside these four. The category from question 5 must make the value obvious. The trend from question 6 must be real and dated.

A draft that fails any test goes back to the question that caused the failure. A credible failure usually goes back to question 2 or 3. A unique failure usually goes back to question 2, because the sentence needs a capability the alternatives do not have.

Keep a record of every draft and every result, including the failed ones. The reader must be able to see what failed and why. Use one row per draft:

| Draft | Statement | Specific | Desirable | Credible | Unique | Category | Trend | Action |
|-------|-----------|----------|-----------|----------|--------|----------|-------|--------|

**Produces:** the surviving statement and value proposition, and the record of every draft.

### Stage 4. Attach Proof to Every Claim

Each value claim gets its proof and its grade on the evidence ladder: `assumed`, `heard`, `seen` or `confirmed`. Those four words are the only grades. Counts, sources and observations are written beside a grade, never in place of one. "Observation, 4 of 4 talks, n=4" describes a claim that is still `assumed`. Pilot-only proof is labelled pilot-only. An illustrative number is not proof, so it grades as `assumed` until a real result exists. A capability that a buyer watched the product perform grades as `seen`, with its count, and the scenario is labelled illustrative when it is not a customer's real result.

A claim with no proof stays in the statement only if it is marked as a bet.

**Produces:** the proof ledger.

### Stage 5. Set the Price, Last

This stage starts only after Stage 3 has a draft that passed all four tests.

1. **Choose the value metric** from the value named in question 3. Pick the unit the buyer gets more of as they pay more. Do not pick the unit that is easiest to bill.
2. **Anchor on the alternative's real cost.** Use Discovery's alternatives and the deal history. Where a cost is not recorded, say so.
3. **Respect the buyer's approval line.** This is the amount above which someone else must sign. It comes from the persona and the profile's zones.
4. **Check the archetype's contract-value band.** A price far outside the band is flagged, not forbidden.
5. **Test the price with buyers in past-behavior form.** Ask what they last paid for something like this, who approved it, and what made them hesitate. Never ask "would you pay X?"
6. **Fix the setup rule, then test both sides of the approval line.** State whether setup is charged per site, per seat or per account, using the profile's price list. Then show the year-one total at one site and at two sites. If a multi-site account crosses the line, do not change the price to pass the test. Narrow the start instead, and record the reason.

**Produces:** the price, the value metric, and the reason behind each.

### Stage 6. Clear the Economics Gate

The price must clear three thresholds. Show each one with its inputs.

- Lifetime value to acquisition cost above 3 to 1
- Payback under 12 months
- Gross margin above 70%

Label each input one of three ways. It is the team's own data, with its n. It is a modeled number from the profile or price list. Or it is an estimate or an illustrative figure.

If any threshold fails, do not adjust the inputs until they pass. Send the work back to the position. Use Stage 2 question 4 when the problem is who the position is for, or Stage 3 when the problem is the statement. A position that cannot carry its price was not defensible enough.

If a required input is missing, the gate reports "not run" for the affected threshold and names the missing input.

**Produces:** the economics table, with pass, fail or not run for each threshold.

### Stage 7. Build the Messages

From the surviving position:

- At most three messaging pillars. Each pillar is tied to one value claim and needs proof graded `heard` or `seen`. A claim graded `assumed` is a bet. A pilot outcome is never a pillar, even when it is illustrative and graded `assumed`. If only one claim qualifies, show one pillar. Do not pad the list to three.
- For each real alternative from Discovery, one short answer to "why not just keep doing that?"
- A one-sentence version and a thirty-second version of the position.

**Produces:** the message set, named exactly: "Message set: pillars, why-not-keep-doing-that answers, one-sentence and thirty-second versions."

### Stage 8. Write It Back and Hand Off

- **Knowledge base nodes:** the position (statement and value proposition), each value claim with its proof grade, the pillars, and the price with its economics.
- **The client profile:** Value Propositions (with proof), Proof Points (with status), Competitive Landscape (the "your advantage" column), and Company (the one-sentence position).
- **Hand-off block for Launch:** every Output Contract field, quoted in full inside the block, with no ID-only entries and no "see above" pointers, plus the message set named in Stage 7. If the client profile has no `## Positioning` section, the run says so once, uses the defaults in `CUSTOMIZE.md`, and lists the write-back before writing anything.

**Approval step.** This skill writes to the knowledge base and the profile, so it is marked mutating. Before this stage writes anything, the owner of the positioning decision named in the profile approves the statement and the price. Nothing is written until that approval is recorded in the brief.

**Produces:** the nodes, the profile updates and the hand-off block.

---

## Epistemic Rules

### The Evidence Ladder

Every claim sits on exactly one rung. The rung is shown wherever the claim appears.

| State | Means | Example |
|-------|-------|---------|
| `assumed` | Somebody believes it | "A general manager signs the contract" with no buyer statement yet |
| `heard` | A buyer said it | Two buyers named the general manager as the signer |
| `seen` | It shows in behavior or data | The general manager signed 7 of the last 10 contracts |
| `confirmed` | Seen across at least 5 cases, recent, and not contradicted | Signed 9 of 10 in the last two quarters, with no contrary case |

A claim cannot move to `confirmed` while a contrary case is unexplained. If a contrary case exists, reword the claim to fit the evidence and grade the new wording.

A published rule is a source, not a case count. A requirement written in a public rule is graded `seen` on the rule's text, because it shows in a document, with the source and its date written beside the grade. It never reaches `confirmed`, because that rung counts cases, and it carries the 30 day re-check window of any `seen` claim.

### The Working Rules

1. **n beside every rate.** Write "57% (4 of 7)", never "57%".
2. **Five before a pattern.** Fewer than five cases is an observation, and it is labelled as one.
3. **Silence is not a no.** A record that is silent on a point is left out of that count. It is not counted against it.
4. **"No difference" is a finding.** Report it. Do not keep slicing until a cut looks significant.
5. **Downstream refuses `assumed`.** Anything resting on an assumed claim is labelled a hypothesis.
6. **Illustrative numbers are labelled.** Any number that is not the team's own data says so in the same sentence.
7. **Economics are never tuned to pass.** A failed threshold sends the work back to the position.

### Stated Thresholds

Every output names the thresholds it used: the three economics thresholds, the minimum cell size for any cut, and the re-grade windows. A reader must be able to see what was suppressed.

---

## Hard Rules

Each rule carries its reason.

1. **No price before the position passes.** Stage 5 cannot start until a draft has passed all four tests. Reason: a price chosen first decides what the position is allowed to claim.
2. **No step is skipped.** The six questions run in order every time. Reason: the category and trend answers are the easiest to write, and the most likely to be written for the wrong buyer.
3. **Assumed claims are labelled hypotheses.** Reason: a statement that reads as settled gets built on by Launch.
4. **The economics are never tuned to pass.** Reason: a spreadsheet adjusted until it passes hides a position that cannot hold its price.
5. **Pilot-only proof is flagged everywhere it appears.** Reason: a pilot is one customer's experience, and the reader needs to see that.
6. **Nothing is written before approval.** Reason: the nodes and the profile are read by other skills and by the sales team.
7. **Design around a do-not-build-on claim, never depend on it.** Positioning may keep a price under a line so that a bet is not needed. It may not rest the statement, the proof or the price on the bet. Reason: a position that survives only if an unbuilt-on claim turns out true is the same guess with better formatting.

---

## Quality Bar

A Positioning pass is done when all five are true. Run this checklist before handing back.

- [ ] All six questions ran in order, and the record shows the trace of each answer
- [ ] The value proposition passed all four tests, and every failed draft is recorded
- [ ] Every value claim has proof attached with its grade, and pilot-only proof is flagged
- [ ] The price clears the economics with each input labelled, or the gate reports "not run" with the missing input named
- [ ] The sales team would use the statement on a first call without a rewrite

---

## Examples

### Example 1. PlotIQ, Full Run

**Scope note.** PlotIQ is the example company for cemeteries and funeral homes. Its list price, approval line and beachhead come from its profile and from the Discovery run. The two beta cemeteries are named by role here. Every count, margin, retention figure and acquisition cost below is illustrative unless it is the profile's list price or a figure the article states. None of them is a real PlotIQ result.

**Stage 1. Claims in use, by Discovery 2.1.0 ID.**

| Claim | Discovery section | Grade (n) | Use in This Run |
|-------|-------------------|-----------|-----------------|
| A1. Cemetery general managers sign the contract | Persona trait | `heard` (n=2 buyers) | **Positioning's one load-bearing claim.** The statement names the general manager as the customer, and the approval-line test assumes the general manager signs. If the general manager does not sign, the Specific test and the price test both fail. A1 is not `assumed`, so the stop rule does not fire |
| A2. Paper plot maps are the pain | Load-bearing (Discovery) | `assumed` (observation, 4 of 4 independent talks, n=4) | Labelled hypothesis. Carries the records pain in the Desirable test |
| A3. Start with independent cemeteries | Load-bearing (Discovery) | `assumed` (observation, n=4) | Labelled hypothesis. Carries the one-site start in Question 4 |
| A5. A GM can carry a deal over $25K past the board | Load-bearing (Discovery, close plan) | `assumed` (n=0 closed deals over the line) | Labelled hypothesis, not depended on. The one-site price sits under the line, so the statement does not need A5. A two-site account would need it, so that case is not offered at the start |
| A6. Staff resistance is what stalls deals | Do not build on | `assumed` (n not recorded) | Not used |
| B1. Buyer comfort with software is low to medium | Do not build on | `assumed` (n not recorded) | Not used in the statement. The profile's wording on this is not buyer language |
| P1. The GM keeps the trust fund records and the state filing | Other open bet | `assumed` (n=0 graded) | Labelled hypothesis. Carries the trust element of the Desirable test |
| A4R. The GM decides, with the pre-need manager championing the tool | Other open bet | `assumed` | Not used in the statement |
| N1. The do-nothing count | Other open bet | Not recorded | The Question 1 answer stays provisional |
| T1. The SMB Community ten-deal test | Other open bet | `assumed` (0 of 10 closes recorded) | The archetype is not settled, so the price stays modeled |
| R1. An annual state trust filing is required | Positioning, from a published rule | `seen` on the rule text (illustrative state). It shows in a published document. It is not `confirmed`, because that rung needs five or more cases | Positioning's own claim. The basis is the rule, not a case count. Re-check window applies (see Stage 4) |
| X1. One system holds plot records and the trust ledger | Positioning, new | `assumed` (product scope, no customer report yet) | Labelled hypothesis. Carries the "keeps plot records" wording |

**Why A1 is the load-bearing claim.** If A1 is false, the statement names the wrong buyer and the approval-line test describes the wrong person. R1 was considered and rejected. It is `seen` on its text, but it explains why records matter and does not say who buys. A rule change would alter the pain, not the buyer the statement names.

A2, A3 and P1 sit in the position only as labelled hypotheses. A5, the $25K board bet, is also a labelled hypothesis, and the statement does not depend on it. A6 is not used. Under Discovery's own rule, A2 and A3 cannot be Positioning's load-bearing claim, because both are `assumed`.

**Stage 2. Six answers, in order.**

1. **Without us:** paper plot maps, a spreadsheet, or the groundskeeper's memory. Discovery's alternatives, all buyer statements and all observations under five talks: paper maps 4 of 4 (100%, n=4), a spreadsheet 2 of 3 (67%, n=3), the groundskeeper's memory 2 of 4 (50%, n=4). Doing nothing is not recorded (N1), so this answer is provisional.
2. **What we have that they don't:** digitizes paper plot maps and deeds, shows the unsold plots, and keeps plot records and the trust fund ledger in one system with state filing reminders. The one-system part is X1, graded `assumed`, because it rests on product scope and no customer has filed a report from it yet.
3. **What it delivers, in the buyer's words:** The only recorded buyer quote in the profile is "We have files that date back to the 1970s," from a family funeral home operator in a forum post. It is the nearest the profile holds to buyer language on records, and it is not from a general manager. Two phrases the profile uses are profile wording, not buyer language: "unsold plots nobody knows exist" and "an auditor asking for a trust record that sits in a binder in a storage room." The records pain traces to A2 (`assumed`). The trust pain traces to P1 (`assumed`).
4. **Who cares most:** the general manager of an independent cemetery with one site, paper records and an annual state filing. This narrows the profile's ICP1 to one-site buyers. The independent-first ranking is A3, `assumed`, observation only. The one-site narrowing is also forced by the price: a two-site account is over the approval line (Stage 5), so the start is one-site buyers.
5. **Category:** cemetery records and trust compliance software. This is a team judgment, not a Discovery finding. It names what the buyer already buys. It avoids "AI-powered," which is an adjective.
6. **Why now:** the profile's buying triggers, each with its own window. Audit finding on records or trust fund, 60 to 120 days. Consolidator buys the site, 60 to 120 days. Double-sold plot or wrong-plot burial, 30 to 60 days. General manager or owner change, 90 to 180 days. Owner update announcing growth, 90 to 180 days. Rival contract renewal, 90 to 180 days before renewal. Pre-need counselor job posting, 30 to 60 days. The annual state trust filing date is a calendar fact set by the rule (R1). It is not a profile trigger and has no profile window. **Date check:** the research notes are dated 2026-03-27, 200 days before this run, so the trend is flagged for refresh before any published claim uses it.

**Stage 3. Draft record.**

| Draft | Statement | Specific | Desirable | Credible | Unique | Category | Trend | Action |
|-------|-----------|----------|-----------|----------|--------|----------|-------|--------|
| 1 | "AI-powered cemetery management" | Pass. Names the general manager | Pass in part. The records pain is A2, `assumed`, a labelled hypothesis | Stalled. The only proof is pilot outcomes, which are illustrative and graded `assumed` | Fail. Any vendor could say it | Not reached | Not reached | Unique failed, so return to question 2. "AI-powered" names no capability |
| 2 | "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery." | Pass. Names a role and a kind of organization | Pass in part. The records pain is A2 and the trust element is P1, both `assumed`. Both labelled as hypotheses | Pass on a demonstrated capability, not on pilot outcomes. C2 is `seen`, n=2, illustrative scenario. No pilot outcome is cited | Pass, narrowly. The profile records no competitor with the same report-format claim, which is not the same thing as proof | Pass. Cemetery records and trust compliance software | Pass, with a refresh flag on the research date (2026-03-27) | Survives. Moves to Stage 4 |

Draft 2 is the statement that goes forward. Draft 1 stays in the record. It is not deleted because it failed.

**What changed from the profile's hallway version.** The hallway version says "keep plot records and trust fund reports in a form a state auditor will accept." The phrase "a form a state auditor will accept" promises an outcome. Only a pilot outcome could support it, and that is a bet. Draft 2 claims the format instead, which two beta general managers watched PlotIQ produce. "Cemetery general managers" is narrowed to "the general manager of an independent cemetery" because Question 4 narrows the start, and Stage 5 gives the reason.

**Stage 4. Proof ledger.**

| Claim | Value Proposition | Proof | Grade | Status |
|-------|-------------------|-------|-------|--------|
| R1. An annual state trust filing is required | Pain 2 (profile) | A public rule for an illustrative state. A rule, not a buyer claim and not a case count | `seen` on the rule text. The source is dated 2026-03-27, 200 days old and past the 30 day window for `seen`, so re-check before any external use | Supports the trust element of the statement. Not a pillar |
| C1. Unsold plots found from paper records | VP1 (profile) | Fennick Gardens (beta): 212 unsold plots found in 90 days. Illustrative, one site | `assumed` | Bet. Pilot-only and illustrative. Not in the statement, not a pillar |
| C2. State-format trust and plot reports, produced from the customer's own ledger | VP2, reworded | Two beta general managers watched PlotIQ produce the state-format trust report from their own ledger. Illustrative scenario, n=2 | `seen`, n=2 | In the statement and the one pillar. Fewer than five cases, so it is labelled an observation |
| C3. Records a state auditor accepts | VP2, as the profile first wrote it | Holloway Hills (beta): zero records findings in its first state review. Illustrative, one site | `assumed` | Bet. Pilot-only. Not in the statement or the one-sentence version |
| C4. A plot answer in 20 seconds, not 20 minutes | VP3 | Target only, from research | `assumed` | Bet. No proof |
| C5. Pre-need leads worked within an hour | VP4 | Target only | `assumed` | Bet. No proof |
| C6. Live in six weeks | VP5 | Roadmap week 6. A plan, not a result | `assumed` (plan) | Bet. Graded as a plan |
| C7. Year one under the approval line, one site | Price | Arithmetic on the modeled list price: $10,788 plus $5,000 setup, $15,788 | `assumed` | Holds for one site only. Modeled price, not tested with buyers. See Stage 5 |

**Stage 5. Price, set last.**

- **Value metric: per cemetery site.** The value named in question 3 (records a state can audit, and plots found) grows with each site, so a buyer who runs more sites gets more value and pays more. This is chosen because it matches the value, not because it is easy to bill.
- **Price: $899 per site per month, plus a $5,000 one-time setup per account.** This is the profile's list price. It is a modeled price. No buyer has paid it yet.
- **Setup rule: per account.** The profile gives one $5,000 setup fee. This run reads it as per account, and the profile must confirm that rule. The confirmation is an open bet (PA1 in the hand-off).
- **Anchor:** the enterprise mapping alternative is about $1,500 to $2,500 a month, a research estimate dated 2026-03-27 that has not been checked against that vendor's current price list. The paper alternative's cost is not recorded, which is a gap.
- **Approval line:** $25,000 year one. The profile has no `## Positioning` section, so this is the default in `CUSTOMIZE.md`. Two year-one totals under the per-account setup rule:
  - One site: $899 x 12 = $10,788, plus $5,000 setup = $15,788. Under $25,000 by $9,212.
  - Two sites: 2 x $10,788 = $21,576, plus $5,000 setup = $26,576. Over $25,000 by $1,576.
  - If setup were charged per site, two sites would be $21,576 plus $10,000 = $31,576. That is not the reading used. It is shown because the setup rule decides which side of the line a two-site buyer lands on.
- **Why the start is one-site buyers.** The one-site year one sits under the line. Whether a general manager can sign under the line rests on A1 (`heard`, n=2), and the line itself is the profile's Zone 3 statement, which Discovery marked `assumed` beside A5. The two-site year one is over the line, so a two-site deal would depend on A5. A5 is `assumed` and sits in Discovery's `Load-bearing:` list, and Positioning does not build on it. Question 4 therefore narrows the start to one-site independents. This is the recorded reason.
- **Archetype band check.** $10,788 a year sits inside the SMB Community band of $5,000 to $50,000. This is a sanity check on a modeled price, not evidence. The archetype read used the same $10,788 figure, so the two cannot confirm each other. T1, the ten-deal test with 0 of 10 closes, is still open.
- **Past-behavior price test: 0 of 5 conversations held.** The question is: "What did you last pay for a records or compliance system for your cemetery? Who signed off on it, and what made you hesitate?" Until this test runs, the price stays modeled.

**Stage 6. Economics gate.**

Inputs:

| Input | Value | Label | n |
|-------|-------|-------|---|
| Price per site per month | $899 | Profile list price, modeled, not yet billed | 0 PlotIQ customers |
| Setup fee | $5,000 one-time | Profile list price, excluded from payback below | 0 |
| Gross margin | 80% | Illustrative. No cost data exists | 0 |
| Expected lifetime | 48 months | Illustrative. No retention data exists | 0 |
| Acquisition cost per customer | $6,000 | Illustrative. No acquisition cost data exists | 0 |

Calculated from those inputs, per site:

| Figure | Value | Arithmetic |
|--------|-------|------------|
| Gross profit per site per month | $719.20 | 899 x 80% |
| Lifetime value | $34,522 | 719.20 x 48 |
| Lifetime value to acquisition cost | 5.8 to 1 | 34,522 / 6,000 |
| Payback | 8.3 months | 6,000 / 719.20 |

Results:

| Threshold | Result on Real PlotIQ Data | Result on Illustrative Inputs |
|-----------|----------------------------|-------------------------------|
| Lifetime value to acquisition cost above 3 to 1 | Not run. No acquisition cost or retention data | Pass, 5.8 to 1 |
| Payback under 12 months | Not run. No acquisition cost data | Pass, 8.3 months |
| Gross margin above 70% | Not run. No cost data | Pass, 80% (illustrative) |

**Gate status: not run on real data.** The illustrative arithmetic clears all three thresholds. That shows the method works. It is not a finding. The inputs to close are gross margin from cost data, acquisition cost from spend divided by won deals, and retention from the first cohort. Setup is excluded from payback, which is the conservative choice.

**Stage 7. Messages.**

- **Messaging pillars: one.**
  1. **Plot and trust reports in the state's own format, from the customer's own ledger.** Tied to C2, graded `seen`, n=2, illustrative scenario. The proof is a demonstrated capability, not a pilot outcome.
  - Why only one: C2 is the only value claim with `heard` or `seen` proof. C1, C3, C4, C5 and C6 are `assumed`, so they are bets. C1 and C3 are pilot outcomes, which never become pillars.
- **Answers to "why not just keep doing that?"** One per Discovery alternative.
  - Paper maps: "Paper keeps the record, but not the plots you could sell. How many could you sell today if the records were right?"
  - A spreadsheet: "A spreadsheet holds the list, but it does not produce the state's report format. What does the trust report cost you to assemble by hand each year?" The cost of that assembly is not recorded, so this answer stays provisional.
  - The groundskeeper's memory: "One person knows where everything is. That works until they leave."
  - Enterprise mapping (Stonemark): "It runs about $1,500 to $2,500 a month (research estimate, not checked) and takes 90 to 120 days to go live (research). Our six-week go-live is a plan, not a result."
  - Legacy on-premise system (Oldgate): "Upfront cost and yearly maintenance are heavy (research estimate, not checked). This product runs in the cloud and on mobile." No talk named this alternative (0 of 4), so the answer is kept for the sales team only, and the cloud and mobile part is product scope, `assumed`.
  - Doing nothing: "Unsold plots and audit exposure stay where they are." This answer stays provisional until N1 is recorded.
- **One sentence:** "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery, at $899 a month per site."
- **Thirty seconds:** "When a state asks for a trust fund report, a cemetery that keeps its records on paper can be looking at a search through a binder. PlotIQ produces that trust fund report in the state's own format, from the cemetery's own ledger, and it keeps the plot records in the same system. Two beta general managers have watched it do that. It costs $899 a month per site, plus a one-time setup fee."
  - Use this version only after a live demo confirms that the plot records and the trust ledger sit in one system (X1, `assumed`). The unsold-plots line is left out on purpose, because its only proof is pilot outcomes.
  - The sentence "Two beta general managers have watched it do that" is the C2 demonstration. It is graded `seen`, n=2, and a real team records the demonstration before it uses this grade (PA6 in the hand-off).

**Stage 8. Write-back and hand-off.**

- **Nodes:** the position (statement and value proposition), the proof ledger's eight rows (R1 and C1 to C7) with their grades, the one pillar, and the price node with its economics.
- **Profile changes the run would write (nothing is written yet):**
  - **Company:** the one-sentence position, quoted in Stage 7.
  - **Value Propositions:** VP2 is reworded to "State-format trust and plot reports, produced from the customer's own ledger," graded `seen`, n=2, illustrative scenario. VP1, VP3, VP4 and VP5 are marked as bets with their grades. VP1 is `assumed` and pilot-only. VP3 and VP4 are `assumed` with no proof. VP5 is `assumed` and graded as a plan.
  - **Proof Points:** Fennick Gardens and Holloway Hills stay in the profile, marked pilot-only, illustrative and bet. Brackhaven stays "not a result, do not cite." A new row records the beta general manager demonstration, `seen`, n=2, illustrative scenario, marked illustrative, to be replaced by the team's own record.
  - **Competitive Landscape, "your advantage" column, graded:** Stonemark's "Records, trust compliance and pre-need in one system" is `assumed` (product scope), and its "Live in 6 weeks" is `assumed` (plan). Lanternfield's "Cemetery plots and pre-need in one system, support included" is `assumed` (product scope, support terms not checked). Oldgate's "Cloud and mobile" is `assumed` (product scope), and its "Live in 6 weeks, against 120 to 180" is `assumed` (plan), with the 120 to 180 day figure a research estimate. The status quo's "Cost of inaction" is `assumed`, n not recorded.
  - **Six-week go-live:** graded as a plan, `assumed`, not a result.
  - **Missing section:** the profile has no `## Positioning` section. The run flags it and uses the defaults in `CUSTOMIZE.md`: approval line $25,000, the three economics thresholds, and re-grade windows of 90 days for `confirmed` and 30 days for `heard` and `seen`. The owner of the positioning decision is not recorded, so the approval step cannot name a person yet.
- **Approval:** recorded before any write. Nothing is written until the owner approves the statement and the price.

**Hand-off block for Launch (every field quoted in full):**

- **Positioning statement (Draft 2, exact text):** "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery."
- **Value proposition (exact text, with the four test results):** "State-format trust and plot reports, produced from the customer's own ledger." Specific: pass. Desirable: pass in part, with A2 and P1 labelled as hypotheses, both `assumed`. Credible: pass on C2, `seen`, n=2, illustrative scenario, with no pilot outcome cited. Unique: pass, narrowly.
- **Proof ledger (every row, with grade and status):**
  - R1. An annual state trust filing is required. `seen` on the rule text, illustrative state. Source dated 2026-03-27, past the 30 day window for `seen`, so re-check before any external use.
  - C1. Unsold plots found from paper records. `assumed`. Pilot-only and illustrative (212 plots, one site). A bet.
  - C2. State-format trust and plot reports, produced from the customer's own ledger. `seen`, n=2, illustrative scenario. In the statement and the pillar.
  - C3. Records a state auditor accepts. `assumed`. Pilot-only and illustrative (zero findings, one site). A bet.
  - C4. A plot answer in 20 seconds, not 20 minutes. `assumed`. No proof. A bet.
  - C5. Pre-need leads worked within an hour. `assumed`. No proof. A bet.
  - C6. Live in six weeks. `assumed`. A plan, not a result. A bet.
  - C7. Year one under the approval line, one site. `assumed`. Arithmetic on the modeled price, $15,788. Holds for one site only.
- **Messaging pillars (one):** "Plot and trust reports in the state's own format, from the customer's own ledger." Tied to C2, graded `seen`, n=2, illustrative scenario. It is the only claim with `heard` or `seen` proof.
- **Message set: pillars, why-not-keep-doing-that answers, one-sentence and thirty-second versions.** Contents: the one pillar above, the six why-not answers in Stage 7, and the one-sentence version. The one-sentence version is "PlotIQ keeps plot records and trust fund reports in the state's own report format, the form a state auditor asks for, for the general manager of an independent cemetery, at $899 a month per site." The thirty-second version is "When a state asks for a trust fund report, a cemetery that keeps its records on paper can be looking at a search through a binder. PlotIQ produces that trust fund report in the state's own format, from the cemetery's own ledger, and it keeps the plot records in the same system. Two beta general managers have watched it do that. It costs $899 a month per site, plus a one-time setup fee."
- **Price and value metric:** "$899 per site per month, plus a $5,000 one-time setup per account. Value metric: per cemetery site. Modeled, not yet tested with buyers (past-behavior test, 0 of 5 held). Year one: one site $15,788, under the $25,000 line. Two sites $26,576, over the line. The start is one-site buyers."
- **Economics (per site, each threshold with its inputs):**
  - Lifetime value to acquisition cost above 3 to 1: not run on real data. Illustrative: 5.8 to 1 (34,522 / 6,000), pass.
  - Payback under 12 months: not run on real data. Illustrative: 8.3 months (6,000 / 719.20), pass.
  - Gross margin above 70%: not run on real data. Illustrative: 80%, pass.
  - Missing inputs to close: gross margin from cost data, acquisition cost from spend divided by won deals, and retention from the first cohort.
- **Open bets:** Discovery 2.1.0's three parts, carried with the same IDs and text, then Positioning's additions.
  - Load-bearing (Discovery): A2, paper maps are the pain (`assumed`, observation, 4 of 4, n=4). A3, start with independent cemeteries (`assumed`, observation, n=4). A5, a GM can carry a deal over $25K past the board (`assumed`, carries the close plan).
  - Do not build on (Discovery): A6, staff resistance is what stalls deals (`assumed`). B1, buyer comfort with software (`assumed`).
  - Other open bets (Discovery): P1, the GM keeps the trust fund records and the state filing (`assumed`). A4R, the GM decides with the pre-need manager championing the tool (`assumed`). N1, the do-nothing count (not recorded). T1, the SMB Community ten-deal test (0 of 10 closes recorded).
  - Positioning additions, each with its reason:
    - PA1. The setup rule is per account and not yet confirmed. Reason: it decides which side of the approval line a two-site buyer lands on.
    - PA2. Cost inputs (gross margin, acquisition cost, retention) are all n=0. Reason: the economics gate is not run.
    - PA3. Competitor prices are research estimates dated 2026-03-27, not checked. Reason: the anchor and two why-not answers use them.
    - PA4. The past-behavior price test is at 0 of 5. Reason: the price stays modeled until it runs.
    - PA5. Pilot outcomes C1 and C3 are illustrative and `assumed`. Reason: they cannot be cited, and they cannot be pillars.
    - PA6. The C2 demonstration is graded `seen`, n=2, on the basis of two beta general managers watching the report. Reason: the profile does not yet record it, so a real team writes the grade only after it has the record.
    - PA7. R1 needs a re-check, and the trend date needs a refresh. Reason: the rule text and the research are dated 2026-03-27, past the re-check window.
    - PA8. X1, the one-system claim. Reason: it rests on product scope.
- **Do not build on:** A6 and B1, as Discovery wrote them. Positioning adds no claim to this list. The statement does not depend on A5, which is in Discovery's `Load-bearing:` list, because the one-site price sits under the line. A2, A3 and P1 appear only as labelled hypotheses.

### Example 2. The Same Position on Multi-Location Groups (Failure)

**Scope note.** This is the multi-location group (ICP3) from the profile: four to ten sites, a CFO gate, and a 6 to 9 month cycle. The statement from Example 1 is applied to it. The illustrative inputs are labelled. The sites are priced at the per-site list price, which is an assumption the profile does not confirm for groups. Every input is illustrative, with n=0 team records. The profile prices combinations per site and does not price multi-location groups, so the per-site assumption is labelled.

**Stage 6 applied, on four sites.**

| Figure | Value | Label |
|--------|-------|-------|
| Monthly revenue, 4 sites | $3,596 | 4 x $899. Assumes the per-site list price applies to groups |
| Gross profit per month | $2,876.80 | 3,596 x 80%. Gross margin illustrative |
| Lifetime value at 48 months | $138,086 | 2,876.80 x 48. Lifetime illustrative |
| Acquisition cost | $40,000 | Illustrative. A CFO-gated deal that takes 6 to 9 months of sales time |
| Lifetime value to acquisition cost | 3.45 to 1 | 138,086 / 40,000. Passes (above 3 to 1) |
| Payback | 13.9 months | 40,000 / 2,876.80. **Fails** (over 12 months) |
| Gross margin | 80% | Illustrative. Passes |

**Result: payback fails.** The skill does not discount, and it does not change the acquisition cost to pass. A lower price would make payback worse, not better, because payback is acquisition cost divided by monthly gross profit. The fix is in who the position is for, so the work returns to **Stage 2, question 4 (who cares most)**.

**What question 4 finds.** The cycle length and the CFO gate are part of the buyer, not a flaw in the statement. The group buyer has the largest set of sites, and therefore the most value, but the path to a signed deal is the longest. The record shows the failure and the return. It does not show a new beachhead, because that answer has not been earned yet. When question 4 is answered again on the evidence, Stages 3 to 6 run again, with the same four tests and the same thresholds.

The illustrative numbers are not a finding about ICP3. They show that the gate caught a payback problem that the statement alone would not have shown.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| Every value claim reads `assumed` | Discovery's grades are missing, or the proof is illustrative | Grade the real proof, or run Discovery's evidence plan. Do not raise a grade to make the statement read better |
| The draft passes everything except Credible | The proof is pilot-only | Keep the claim, flag it as pilot-only, or make it a bet. Do not remove the flag |
| Economics say "not run" | Cost data is missing | Name the missing input and supply it, then re-run. Do not fill the gap with a benchmark and report it as a result |
| The statement keeps failing Unique | The sentence names a category, not a capability | Return to question 2 and name the capability. Do not swap in a different adjective |
| The price lands outside the archetype band | Value metric or price was chosen for ease of billing | Flag the mismatch. Re-check the value metric against question 3 |
| A two-site buyer crosses the approval line | The setup fee is charged per account, and the two-site year one is $26,576, over the $25,000 line | Show both totals. Do not change the price to pass. Narrow the start to one-site buyers and record the reason |
| Launch refuses the hand-off | A required field is missing or has been renamed | Check the field names against the Output Contract. Do not rename fields to pass the hand-off |

---

## Best Practices

- **Write the position before the price.** A price chosen first decides the claims, and the position then has to match it.
- **Keep the failed drafts.** The record of what failed is the reason the surviving draft can be trusted.
- **Name the bet out loud.** A claim marked as a bet is more useful to the sales team than a claim quietly included.
- **Use buyer language.** Words from Discovery's calls and forum posts test a statement better than the team's own vocabulary.
- **Read the economics as a check on the position.** A failed gate points at the position, not at the cost model.

---

## Integration With Other Skills

- **Discovery (`gtm-discovery`)** supplies the five fields this skill reads by name: Customer archetype, Competitive alternatives, Beachhead segment, Buyer persona and Open bets. Positioning refuses to run without them.
- **Launch (`gtm-launch`)** reads every field in the Output Contract. The hand-off block in Stage 8 lists them in one place, so Launch does not need the full run to start.

### The Loop: How Positioning Stays Current

- **Re-run when Discovery changes** a load-bearing claim, or when a proof point's grade changes.
- **Weekly Review** lists open bets older than a month, and proof points that are still pilot-only.
- **Dream** archives superseded positions, so two statements never sit side by side in the knowledge base.

---

## Changelog

- **2.0.0 (2026-10-13):** Ground-up rewrite. Position before price: six questions in order, a four-point test, price last, and an economics gate that sends a failed position back rather than adjusting inputs. Price research uses past-behavior questions. Adds the proof ledger, the economics table and the hand-off block for Launch. The 1.x version stays in history.
