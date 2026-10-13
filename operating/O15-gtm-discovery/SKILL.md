---
name: gtm-discovery
version: 2.0.1
description: "Diagnoses which Guild archetype a business is, grades every belief about its customer by evidence (assumed, heard, seen, confirmed), plans the cheapest evidence for the bets that matter most, names the real alternatives and a starting segment, and writes the result to the knowledge base for Positioning, Launch and Engine to read."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
tags: [discovery, customer-archetype, evidence-ladder, load-bearing-assumption, starting-segment, competitive-alternatives, open-bets, operating-discipline]
requires:
  skills: [context-os-setup]
mutating: true
change_log:
  - version: 2.0.1
    date: 2026-10-13
    summary: "Example 1 re-cast on PlotIQ, the library's one example company, matching article 51."
  - version: 2.0.0
    date: 2026-10-12
    summary: "Ground-up rewrite around the archetype diagnosis and the evidence ladder. Adds the open-bets node and the seven-stage workflow with a re-grade loop."
---

# Discovery

## Overview

Discovery answers one question before any positioning, pricing or launch work starts: **what kind of business is this, really, and how sure are we?**

The skill does five things in order. It writes down what the team believes. It diagnoses the archetype, because the market decides the motion. It grades every belief by the evidence behind it. It goes and gets only the evidence that is missing. It writes the result into the knowledge base so the next skills can run on it without anyone re-explaining the customer.

**Core Principle:** A belief is not a finding until it is graded. Anything still `assumed` is a bet, and the bets get named out loud.

---

## Why This Skill Exists

Most teams carry a customer picture in their heads. It is a mix of what a founder saw in one memorable deal, what a rep repeats, and what a marketing deck said last year. Each piece feels equally true. Positioning then builds a statement on top, Launch quotes the same picture, and Engine re-derives it next quarter with a different answer.

The archetype is the largest single fact in that picture. A business selling to hospital systems on 18-month cycles and a business selling to owner-operators with a two-week decision run different sales motions, need different proof, and fail in different ways. Teams often pick the archetype they want, not the one their market allows. Discovery makes the market's answer the starting point.

Discovery also refuses to let a guess look like evidence. Each claim has a state, and the state is visible wherever the claim appears. The next skill will not build on a claim that is still a guess.

---

## Role

You are a diagnostic partner who grades beliefs, not a researcher who collects opinions. Your job is to:

- Make the team write its beliefs down before it reads any data
- Show the evidence behind each claim, or mark the claim as a guess
- Say plainly when the answers contradict each other
- Refuse to invent interview results

You do not decide the strategy. You make the evidence state of the strategy visible, so the team decides with its eyes open.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| What the team believes about its customer, in its own words | Required | Collected in Stage 1. Never skipped, even when deal data exists |
| `profiles/client-profile.md` | If it exists | Treated as claims to grade, not as facts. Its ICP, persona and competitor entries are the first claims |
| Deal history: the last 10 to 20 won and lost deals | Strongly recommended | Cycle length, contract value, stakeholders, source, loss reason. Without it, most claims stay `assumed` |
| Call notes, transcripts, support tickets | Optional | Each one is a possible source for a claim. Record which claim each one supports |
| Knowledge base location | If one exists | From Context OS Setup. Without it, outputs are written to the profile and the brief only |

---

## Output Contract

Positioning reads these fields. Keep the names exactly as written, because the Positioning Input Contract asks for them by name.

| Field | Where It Lives | Notes |
|-------|----------------|-------|
| Customer archetype | Archetype node, and the Company section of the profile | One of the five Guild archetypes, with confidence and the name of the archetype that leads if it is a hybrid |
| Competitive alternatives | Alternatives node, and the Competitive Landscape section of the profile | Includes "do nothing" and in-house options, each with its count (n) and source |
| Beachhead segment | Starting-segment node, and the ICP Definitions section of the profile | Same meaning Positioning uses. Scored with n and the scoring threshold stated |
| Buyer persona | Persona node, and the Buyer Personas section of the profile | Every trait carries the claim it came from. A trait with no source is removed |
| Open bets | Open-bets node | New in 2.0. Lists every load-bearing claim still `assumed`. Positioning reads it to know what not to build on |

The Discovery brief (Stage 7) links to these nodes. It does not copy them.

---

## Context

Discovery reads, in this order:

1. The team's own statement of beliefs (Stage 1)
2. The client profile, if it exists: Company, ICP Definitions, Buyer Personas, Core Pain Points and Competitive Landscape
3. The deal history and any call or ticket records the team provides
4. The `## Discovery` section of the profile, if the team has run the customization interview. It holds the knowledge base path, the team's starting archetype guess, and the re-grade windows

If there is no knowledge base, say so once at the start and write the outputs to the profile and the brief. If there is no profile, run the workflow anyway and write the outputs to the brief. Say once which of these applies.

---

## Core Workflow

Run the seven stages in order. Stages 3 and 4 branch on the archetype, so Stage 2 comes before them.

### Stage 1. Write Down What We Believe

Before any data is read, the team lists every belief about the customer: who buys, why they buy, how fast, what they would do otherwise, and what would make them leave. Each belief becomes a **claim** in the claims ledger. Every claim starts as `assumed`, with one line stating what evidence would change the team's mind.

*Why first:* a belief written down before the evidence can be proven wrong. A belief formed while reading the evidence simply agrees with it.

**Produces:** the claims ledger, with every claim `assumed`.

### Stage 2. Diagnose the Archetype

Answer the five diagnostic questions. Each answer cites its evidence, or is marked `assumed`.

1. **Sales cycle.** Use the median of the last 20 closed deals, not the best or worst one. Bands from the archetype series: 2 to 8 weeks points to SMB Community or PLG. 8 to 16 weeks to SMB Community with complexity. 4 to 12 months to Hybrid or Enterprise lite. 12 months or more to Enterprise. Read the median, not the band edge.
2. **Contract value.** Use what customers actually pay today. Bands: $500 to $5K points to PLG. $5K to $50K to SMB Community. $50K to $500K to Hybrid or Enterprise lite. $500K and up to Enterprise.
3. **Buyer comfort with software.** Tech-savvy buyers can self-serve (PLG). Everyone else needs people (Enterprise or SMB Community). Be honest. "Our buyers are very tech-savvy" is a claim to grade, not a fact.
4. **Money through the product.** Do customers move payments or transactions through the product? If yes, check monthly volume. Around $50K or more per month makes Embedded Fintech a layer worth considering. If no, Embedded Fintech is off the table.
5. **Two distinct sides.** Do two distinct user types have to transact with each other on the platform? If yes, Marketplace is a layer to consider. Users and admins, or departments in one company, do not count.

From the answers, produce a **candidate archetype**. The five archetypes are Enterprise (mission-critical), SMB Community (community-driven), PLG (self-serve), Embedded Fintech and Marketplace. Embedded Fintech and Marketplace usually layer on top of another archetype, so the answer is often a base archetype plus a layer. When the business is a hybrid, name which archetype leads. The leading archetype sets the motion. The layer sets the next motion to add. The answer is always written as a named archetype ("Enterprise leads, SMB Community in mid-market"), never as "Hybrid" on its own, because "Hybrid" is a band the diagnosis passes through, not an archetype the next skill can act on.

Then state the **ten-deal validation test** for the candidate. Run it on the next ten deals:

| Archetype | The Ten-Deal Test |
|-----------|-------------------|
| Enterprise | 8 or more of 10 take 12 months or longer. 8 or more involve 5 or more stakeholders. 8 or more need a custom proof of concept |
| SMB Community | 6 or more of 10 come from referrals or the community. 8 or more close in under 12 weeks. 8 or more customers know other customers |
| PLG | 8 or more of 10 sign up without talking to sales. 6 or more activate within 24 hours. 8 or more understand the product in under 10 minutes |
| Embedded Fintech | 6 or more of 10 process $50K or more a month. 6 or more adopt the payment product. Payment revenue is at least twice software revenue |
| Marketplace | Both sides engage with each other on the platform. Adding users makes the platform more valuable. Losing 30% of supply would clearly hurt demand |

A candidate is confirmed only when 80% or more of the test's checks pass. Below that, the diagnosis is wrong or incomplete.

**If the answers contradict each other, say so plainly.** For example, a cycle in the Hybrid band with an Enterprise validation test that asks for 12-month cycles will fail on the very deals the team is trying to win. That contradiction is the most valuable finding this stage can produce. Report it. Do not average it away.

**Produces:** the archetype node (candidate, leading archetype if hybrid, confidence, the evidence behind each answer, the ten-deal test, and what would overturn the diagnosis).

### Stage 3. Grade What We Already Know

Go through the evidence the company already holds: deal history, the profile, calls and tickets. Move each claim along the evidence ladder in the Epistemic Rules. Most teams can grade a good share of their claims without one new conversation, and the skill reports that share as a number.

Branch on the archetype for where to look first:

| Archetype | Look First At |
|-----------|---------------|
| Enterprise | Lost deals and who blocked them. Stakeholder count per deal |
| SMB Community | Referral sources. Which customers know each other |
| PLG | Signup-to-activation data. Where self-serve users stall |
| Embedded Fintech | Payment volume per customer. Adoption of the payment product |
| Marketplace | Activity on both sides. What happens when one side thins |

Record every grade with its count, for example "the signer was the general manager on 9 of 11 won deals (82%, n=11)." Report the number of claims graded this way as a share of all claims.

**Produces:** an updated ledger, and an evidence-gap list: the claims still `assumed` that matter most.

### Stage 4. Go Get What Is Missing

For each important claim still `assumed`, plan the cheapest evidence that would move it. The method depends on the archetype:

- **Conversations** about what buyers actually did last time. Never what they would do.
- **Deal-data pulls** from the CRM or contract records, for counts that cannot be read from memory.
- **Usage data** for PLG: activation and stall points.
- **Both sides** for Marketplace: supply and demand activity.

The skill writes the plan, the questions, and how each answer will be recorded in the ledger. It never invents interview results. A plan is not a finding.

**Interview rule:** ask about past behavior and real decisions, never opinions or hypotheticals. Do not pitch the product during the conversation. Good question: "Walk me through the last time you replaced or added a system like this. Who was in the room?" Weak question: "Would you use a tool that did this?"

**Produces:** the evidence plan. After the team runs it and records the answers, an updated ledger.

### Stage 5. Name the Real Alternatives

From the evidence, list what buyers actually do instead of buying: named competitors, spreadsheets and email, an internal tool, an outside service, a consultant, or nothing at all. Each alternative carries how often it came up (with n) and the source it came from. A count taken from rep-entered CRM fields is a different source from a count taken from buyer statements, and the node says which.

Include "do nothing" in every list. In most B2B markets it is the largest alternative, and it is the one teams forget to count.

**Produces:** the alternatives node. This is Positioning's required input for competitive alternatives.

### Stage 6. Choose Where to Start

Score each candidate segment on **evidence strength, not attractiveness**. Every rate shows its n. Segments with fewer than five examples are reported as observations, not findings, and the report says so in the same sentence.

State the scoring threshold in the output. A difference under the threshold is reported as "no difference found at this threshold." Do not hunt for a cut that shows one.

Recommend one starting segment, and say what would make the team switch. Name a specific, measurable switch trigger, for example "switch if the win rate in this segment falls below 50% over the next 10 closed deals."

**Produces:** the starting-segment node. This is Positioning's beachhead input, with its scores and n.

### Stage 7. Write It Back

- **Atomic nodes** to the knowledge base: the archetype, each persona (every trait traced to a claim), the alternatives, the starting segment, and the open bets.
- **The client profile.** Update the Company, ICP Definitions, Buyer Personas and Competitive Landscape sections, and mark the confidence of each entry.
- **One strategic document,** the Discovery brief, two pages at most. It links to the nodes rather than copying them.
- **Re-grade dates** on every claim, following the windows in the Loop section.
- **A hand-off block** for Positioning, listing the five Output Contract fields in one place.

**Produces:** the nodes, the updated profile sections, the Discovery brief, and the hand-off block.

---

## Epistemic Rules

### The Evidence Ladder

Every claim sits on exactly one rung. The rung is shown wherever the claim appears.

| State | Means | Example |
|-------|-------|---------|
| `assumed` | Somebody believes it | "Our buyer is the COO" |
| `heard` | A buyer said it | Three buyers named the COO as the signer in calls |
| `seen` | It shows in behavior or data | The COO signed 7 of the last 10 contracts |
| `confirmed` | Seen across at least 5 cases, recent, and not contradicted | Signed 9 of 10 in the last two quarters, with no contrary case |

A claim cannot move to `confirmed` while a contrary case is unexplained. If a contrary case exists, reword the claim to fit the evidence ("the COO signs most contracts, 9 of 11") and grade the new wording.

### The Working Rules

1. **n beside every rate.** Write "57% (4 of 7)", never "57%".
2. **Five before a pattern.** Fewer than five cases is an observation, and it is labelled as one.
3. **Silence is not a no.** A record that does not mention something is excluded from that count. It is not counted against it.
4. **"No difference" is a finding.** Report it. Do not keep slicing until a cut looks significant.
5. **Downstream refuses `assumed`.** Positioning may not build its statement on a claim still `assumed`. The skill lists every such claim in the open bets.
6. **Load-bearing bets first.** Rank open claims by how much breaks if each one is wrong, and test the top ones first. Use the term "load-bearing assumption" for this idea.

### The Quality Bar

Score every section of the Discovery brief from 1 to 5 on four dimensions: evidence, specificity, usefulness and honesty. Any section that scores under 4 on any dimension goes back for another pass before it is written.

### Stated Thresholds

Every output names the thresholds it used: the minimum cell size, the win-rate gap that counts as a difference, and the re-grade windows. A reader must be able to see what was suppressed.

---

## Examples

Both examples follow the seven stages. The PlotIQ numbers are illustrative and labelled as such. The upmarket example uses only the facts the published archetype article states.

### Example 1. PlotIQ, Full Run (Illustrative Numbers)

**Scope note.** PlotIQ is the made-up software company for cemeteries and funeral homes that the library uses as its one example company. Its price, cycle bands, personas and competitors come from its profile. Every count, median and rate below is illustrative, made up for this walk-through, and labelled that way. PlotIQ is in beta with two beta cemeteries and no paid revenue, so none of these numbers is a real PlotIQ result. The beliefs, the archetype call and the open bet match Guild article 51.

**Stage 1. Beliefs (all `assumed`).**

| Claim | What Would Change Our Mind |
|-------|----------------------------|
| A1. Cemetery general managers sign the contract | Signer named in the deal notes, and what buyers say about who signs |
| A2. Paper plot maps are the pain | Buyers describing, in their own words, how a family's plot question gets answered |
| A3. Start with independent cemeteries | Independent talks and deal notes compared with combinations and groups |
| A4. Load-bearing: the pre-need sales manager is the buyer | Who made the decision on each deal where pre-need came up |
| A5. Load-bearing: a GM can carry a deal over $25K past the board | A board date and approval record on each deal over the line, plus buyer statements about the board |
| A6. Staff resistance, not price, is what stalls deals | Stall and loss reasons in the deal notes, in the buyer's words |

**Stage 2. Archetype Diagnosis.**

| Question | Answer | Evidence | Band It Points To |
|----------|--------|----------|-----------|
| 1. Cycle | 90 to 150 days for a single site. No closed PlotIQ deals yet | The research range, not PlotIQ data (illustrative until ten deals close) | 8 to 16 weeks: SMB Community with complexity, at the slow edge |
| 2. Contract value | $10,788 a year plus $5,000 setup, at list | The modeled price in the profile, not a closed median | $5K to $50K: SMB Community |
| 3. Buyer comfort | Low to medium. "Pen and paper is free" | `assumed`. Forum posts only, no buyer records yet | SMB Community, not self-serve |
| 4. Money through product | No. PlotIQ monitors trust records and holds no funds | Product scope | Embedded Fintech off |
| 5. Two sides | No. One buyer, the operator | Product scope | Marketplace off |

**Candidate:** SMB Community leads. Confidence: medium on the archetype, low on the cycle until PlotIQ has closed deals of its own.

**The contradiction, stated plainly.** The cycle answer sits at the slow edge of the SMB Community band, but the SMB Community ten-deal test asks for 8 or more of 10 deals to close in under 12 weeks. Twelve weeks is 84 days, and the research's shortest cycle is 90, so every deal in the research range fails that line. This is not a flaw in PlotIQ. It is the finding: the cycle band and the test disagree, so the archetype is not settled until the first ten closes say which one is right. The plan is to run the test on those ten closes and report the cycle median from them, not from the research.

**Stage 3. Grading What Already Exists.** Illustrative data: notes from seven cemetery conversations (n=7), four with independent cemeteries and three with combinations. Two of the seven are the beta cemeteries. No paid deals exist yet, so the notes carry the grading.

- **A1 moves to `heard`.** Two buyers said the general manager signs the contract, so the claim is graded HEARD (2 buyers). It does not reach `seen`, because no signed PlotIQ contract exists yet to show it in behavior.
- **A4 is contradicted, and it is the load-bearing belief that proves wrong.** Two of the seven notes name a pre-need sales manager in the room, and in both the general manager made the call. A claim cannot stand as written while a contrary case is unexplained, and two cases are not enough to call a pattern either way, so A4 is reworded rather than kept. A4 is archived, not left next to its replacement. The replacement, "The general manager decides, and the pre-need sales manager champions the tool," is a new claim and stays `assumed` until a buyer confirms it.

**Claims graded without a new conversation:** 2 of 6 (33%, n=6). A1 is graded HEARD and A4 is graded contradicted. A2, A3, A5 and A6 remain `assumed`. A2 and A5 go into the evidence plan, because the deal notes do not settle either one.

**Stage 4. Evidence Plan for A2 and A5 (the open claims that matter most).**

- **Deal-data pull:** the board date and approval record from every proposal over $25K, from the proposal log. Record each one and leave blanks as blanks, not zeros. With so few proposals, any result stays an observation until ten exist.
- **Five past-behavior conversations** with cemetery general managers who have signed a contract over $25K, asking: "Tell me about the last purchase that went past your board. Who approved it, and what did the board ask?" Record each answer in the buyer's own words. No answers are recorded here. This is the plan, not a result.
- **Five past-behavior conversations** with independent cemetery staff, asking: "Walk me through the last time a family asked where a plot was." Record who answered, what they looked up, and how long it took. This is the plan for A2, not a result. The four independent talks already held feed Stage 6.

**Stage 5. Competitive Alternatives Node.** Source for every count: buyer statements from the four independent cemetery talks, recorded in the interview notes. These are what buyers said they used, not CRM fields. Every rate is an observation, because n is under five.

| Alternative | Count | Rate (n) |
|-------------|-------|----------|
| Paper maps | 4 | 100% (n=4) |
| A spreadsheet | 2 | 67% (n=3) |
| The groundskeeper's memory | 2 | 50% (n=4) |
| Stonemark Enterprise, the enterprise cemetery mapping product | 1 | 25% (n=4) |
| Oldgate Ledger Pro, the legacy on-premise system | 0 | 0% (n=4) |
| Doing nothing | Not recorded | The talks did not ask about it consistently, so this count cannot be read. Logged as an evidence gap, to be asked in the A5 conversations |

One talk says nothing about spreadsheets. It is left out of that row's count and shown as n=3, not treated as "no", because silence is not a no.

**Stage 6. Starting Segment.** Thresholds used in this run: a gap under 20 points is reported as "no difference found at this threshold," and any cell under five is reported as an observation.

| Segment | Talks (n) | Named Plot Lookup | Named Pre-Need Follow-Up |
|---------|-----------|-------------------|--------------------------|
| Independent cemetery | 4 | 100% (4 of 4) | 75% (3 of 4) |
| Combination | 3 | 67% (2 of 3) | 67% (2 of 3) |

The pre-need gap is 8 points, under the 20-point threshold, so the report says **no difference found on pre-need follow-up**. The plot lookup gap is 33 points, the widest in the table, but both cells are under five, so it is reported as an observation and not as a finding. The choice rests on the ICP ranking, which puts independents first, and on A3, which stays `assumed` and is supported only by observation. **Recommendation:** start with independent cemeteries. **Switch trigger:** if fewer than three of the next ten independent-cemetery talks name plot lookup as their top problem, reopen this stage and consider combinations.

**Stage 7. Write-Back.**

- **Archetype node:** SMB Community leads, medium confidence, with the cycle contradiction and the ten-deal test attached.
- **Persona node, with every trait traced:**

| Persona | Trait | Source Claim | Grade |
|---------|-------|--------------|-------|
| Cemetery General Manager | Signs the contract | A1 | `heard`, 2 buyers |
| Cemetery General Manager | Keeps the trust fund records and the state filing | Profile pain #2, not yet graded | `assumed` |
| Cemetery General Manager | Decides, with the pre-need sales manager championing the tool | Replaces A4 | `assumed` |

The CFO or Controller persona (groups only) has no trait with a source in this run, so it is not written to the node. That is the rule working: a persona with no traced trait does not get a persona entry.

- **Open bets node:**
  1. A5, a GM can carry a deal over $25K past the board. Load-bearing for the close plan. `assumed`. Do not build the close plan on it.
  2. A6, staff resistance is what stalls deals. `assumed`. Positioning may not rest its objection handling on it until buyers say it.
  3. The do-nothing count, which the deal notes do not hold.
  4. The SMB Community ten-deal test, incomplete until ten closes are recorded.
  5. Buyer comfort with software (Stage 2, question 3). `assumed`.
  6. A3, start with independents. Observation only, n=4.
- **Profile write-back:** ICP Definitions ranks independent cemeteries first, with the observation counts and n. The profile's Zone 3 line, "GM or owner signs under $25K," is marked `assumed` beside A5, so the profile stops stating the general manager's authority as fact. Buyer Personas carries the traced traits above. Competitive Landscape carries the alternatives table with its source.
- **Re-grade dates:** A1 (`heard`) in 30 days. A4 is archived. Open bets carry no date and are listed for review once they have been open for a month.

**Hand-off to Positioning (the five fields in one place, every number illustrative):**

- **Customer archetype:** SMB Community leads (medium confidence). The cycle sits at the slow edge of the band and has not yet passed the ten-deal test.
- **Competitive alternatives:** paper maps 100% (n=4), a spreadsheet 67% (n=3), the groundskeeper's memory 50% (n=4), Stonemark Enterprise 25% (n=4), Oldgate Ledger Pro 0% (n=4). Doing nothing: not recorded, open. All observations, under five talks.
- **Beachhead segment:** Independent cemeteries, 1 to 2 sites (the profile's ICP1). Plot lookup named by 4 of 4 talks (n=4, observation). No difference found on pre-need follow-up against combinations (8-point gap, threshold 20). Switch if fewer than three of the next ten talks name plot lookup.
- **Buyer persona:** Cemetery General Manager (three traced traits: one `heard`, two `assumed`).
- **Open bets:** A5, A6, the do-nothing count, the SMB Community ten-deal test, buyer comfort with software.

**Do not build on:** A5 (the $25K board trigger), A6 (what stalls deals), buyer comfort with software. Each is `assumed`. A positioning statement that needs one of them is a hypothesis and must say so.

### Example 2. The Upmarket Move (Published Facts Only)

**Scope note.** The company history below is taken only from the published archetype article on the CourseKey story. The article gives no contract values, no deal counts and no dates for the shift. So this walk-through shows the method on those published facts and adds no numbers. Where a diagnosis question needs a number the article does not give, the answer is marked `assumed` and a data pull is planned.

**The published shape.** The company began by selling to individual vocational schools. Each sale was a single call with one decision-maker. It then moved upmarket to multi-campus education providers. The sales motion moved from demo-and-close to committee decisions that ran about six months, with a deal desk, legal redlines and enterprise onboarding programs the company had to build from scratch. The article calls it the same product category with a completely different go-to-market.

**Stage 1. Beliefs.** The team, still running its school-level motion, believes: "Our next multi-campus deal will close the way our school deals close." Assumed.

**Stage 2. Diagnosis, run on the first multi-campus opportunity.**

| Question | Answer | Evidence | Band It Points To |
|----------|--------|----------|-----------|
| 1. Cycle | Committee decision, about six months | Published account | 4 to 12 months: Hybrid or Enterprise lite |
| 2. Contract value | Not stated in the article | `assumed` until the deal data is pulled | Cannot place yet |
| 3. Buyer comfort | Not stated for the new buyer | `assumed` | Cannot place yet |
| 4. Money through product | Not stated in the article | `assumed` | Cannot place yet |
| 5. Two sides | Not stated in the article | `assumed` | Cannot place yet |

**The diagnosis catches the shift.** The school-level answers point to SMB Community. The first multi-campus opportunity, with a six-month committee cycle, points into the Hybrid or Enterprise lite band. The contradiction is visible before the deal starts: the team is about to run a single-call, one-decision-maker motion against a buyer whose cycle and approval path do not fit it. The stall would show up as the deal going quiet between the first call and the committee, and the diagnosis names that risk in advance.

**Stage 3. Grading.** The team pulls its own records and grades the claim "one decision-maker signs" on the school deals and on any multi-campus deals it has. Counts are the team's own, with n shown. The skill does not supply them.

**Stage 4. Evidence plan.** Plan conversations with past multi-campus buyers about the approval path: who reviewed the contract, which step took longest, and where the deal stopped moving. Ask about what happened, not what the buyer would do. Record the answer in the buyer's words.

**Stage 5. Alternatives.** For this buyer type, the named alternative is whatever the buyer already runs, plus "do nothing." The team records each with its source before it names any competitor.

**Stage 6 and 7.** Starting segment and open bets are written back the same way as in Example 1. The open bets for this run are: contract value for multi-campus deals (`assumed`), whether the existing school motion can carry the first committee deal (`assumed`), and the approval-path stages (`assumed`). Positioning does not build on any of them until they are graded.

---

## Best Practices

- **Write beliefs before opening the data.** A belief written afterward is a summary of the data, not a test of it.
- **Name the contradiction when it appears.** Two answers that point different ways are a finding. Do not average them into a comfortable middle.
- **Grade in the open.** Show the rung and the count beside every claim. A reader should never have to ask how sure the team is.
- **Re-grade on a schedule.** A `confirmed` claim from two years ago is a historical note until it is re-checked.
- **Keep the brief short.** Two pages, linking to the nodes. A longer brief gets read once and then ignored.
- **Let the team choose who is interviewed.** The skill plans the conversations and the questions. It does not decide which of the team's contacts to call.

---

## Integration With Other Skills

- **Context OS Setup (`context-os-setup`)** creates the knowledge base this skill writes to. Run it first if no knowledge base exists. Without it, this skill writes to the profile and the brief only.
- **Positioning (`gtm-positioning`)** reads the five Output Contract fields. It refuses any claim still `assumed`, and it reads the open bets to know what not to build on.
- **Launch (`gtm-launch`)** and **Engine (`gtm-engine`)** read the archetype and the starting segment, and write their results back as new claims for Discovery to grade.

### The Loop: How Claims Stay Current

- **Re-grade dates.** `confirmed` claims are re-checked after 90 days. `heard` and `seen` claims are re-checked after 30 days. `assumed` claims carry no date, because they are open bets.
- **Weekly Review** lists claims past their re-grade date, and any open bet that has been open for a month.
- **Dream** archives claims that newer evidence contradicts, so both versions never sit side by side in the knowledge base.
- **Graph Health** counts claims by state, so "how much of our customer picture is still a guess" becomes a number someone can watch.

---

## Changelog

- **2.0.1 (2026-10-13):** Example 1 re-cast on PlotIQ, the library's one example company, matching article 51.
- **2.0.0 (2026-10-12):** Ground-up rewrite around the archetype diagnosis and the evidence ladder. Adds the open-bets output, the seven-stage workflow with a re-grade loop, and the per-segment ten-deal test.
