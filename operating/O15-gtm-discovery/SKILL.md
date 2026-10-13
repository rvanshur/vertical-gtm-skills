---
name: gtm-discovery
version: 2.0.0
description: "Diagnoses which Guild archetype a business is, grades every belief about its customer by evidence (assumed, heard, seen, confirmed), plans the cheapest evidence for the bets that matter most, names the real alternatives and a starting segment, and writes the result to the knowledge base for Positioning, Launch and Engine to read."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-12
tags: [discovery, customer-archetype, evidence-ladder, load-bearing-assumption, starting-segment, competitive-alternatives, open-bets, operating-discipline]
requires:
  skills: [context-os-setup]
mutating: true
change_log:
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

1. **Sales cycle.** Use the median of the last 20 closed deals, not the best or worst one. Bands from the archetype series: 2 to 8 weeks points to SMB Community or PLG; 8 to 16 weeks to SMB Community with complexity; 4 to 12 months to Hybrid or Enterprise lite; 12 months or more to Enterprise. Read the median, not the band edge.
2. **Contract value.** Use what customers actually pay today. Bands: $500 to $5K points to PLG; $5K to $50K to SMB Community; $50K to $500K to Hybrid or Enterprise lite; $500K and up to Enterprise.
3. **Buyer comfort with software.** Tech-savvy buyers can self-serve (PLG). Everyone else needs people (Enterprise or SMB Community). Be honest. "Our buyers are very tech-savvy" is a claim to grade, not a fact.
4. **Money through the product.** Do customers move payments or transactions through the product? If yes, check monthly volume. Around $50K or more per month makes Embedded Fintech a layer worth considering. If no, Embedded Fintech is off the table.
5. **Two distinct sides.** Do two distinct user types have to transact with each other on the platform? If yes, Marketplace is a layer to consider. Users and admins, or departments in one company, do not count.

From the answers, produce a **candidate archetype**. The five archetypes are Enterprise (mission-critical), SMB Community (community-driven), PLG (self-serve), Embedded Fintech and Marketplace. Embedded Fintech and Marketplace usually layer on top of another archetype, so the answer is often a base archetype plus a layer. When the business is a hybrid, name which archetype leads. The leading archetype sets the motion. The layer sets the next motion to add. The answer is always written as a named archetype ("Enterprise leads, SMB Community in mid-market"), never as "Hybrid" on its own, because "Hybrid" is a band the diagnosis passes through, not an archetype the next skill can act on.

Then state the **ten-deal validation test** for the candidate. Run it on the next ten deals:

| Archetype | The Ten-Deal Test |
|-----------|-------------------|
| Enterprise | 8 or more of 10 take 12 months or longer; 8 or more involve 5 or more stakeholders; 8 or more need a custom proof of concept |
| SMB Community | 6 or more of 10 come from referrals or the community; 8 or more close in under 12 weeks; 8 or more customers know other customers |
| PLG | 8 or more of 10 sign up without talking to sales; 6 or more activate within 24 hours; 8 or more understand the product in under 10 minutes |
| Embedded Fintech | 6 or more of 10 process $50K or more a month; 6 or more adopt the payment product; payment revenue is at least twice software revenue |
| Marketplace | Both sides engage with each other on the platform; adding users makes the platform more valuable; losing 30% of supply would clearly hurt demand |

A candidate is confirmed only when 80% or more of the test's checks pass. Below that, the diagnosis is wrong or incomplete.

**If the answers contradict each other, say so plainly.** For example, a cycle in the Hybrid band with an Enterprise validation test that asks for 12-month cycles will fail on the very deals the team is trying to win. That contradiction is the most valuable finding this stage can produce. Report it. Do not average it away.

**Produces:** the archetype node (candidate, leading archetype if hybrid, confidence, the evidence behind each answer, the ten-deal test, and what would overturn the diagnosis).

### Stage 3. Grade What We Already Know

Go through the evidence the company already holds: deal history, the profile, calls and tickets. Move each claim along the evidence ladder in the Epistemic Rules. Most teams can grade a good share of their claims without one new conversation, and the skill reports that share as a number.

Branch on the archetype for where to look first:

| Archetype | Look First At |
|-----------|---------------|
| Enterprise | Lost deals and who blocked them; stakeholder count per deal |
| SMB Community | Referral sources; which customers know each other |
| PLG | Signup-to-activation data; where self-serve users stall |
| Embedded Fintech | Payment volume per customer; adoption of the payment product |
| Marketplace | Activity on both sides; what happens when one side thins |

Record every grade with its count, for example "signer was the General Counsel on 9 of 11 won deals (82%, n=11)." Report the number of claims graded this way as a share of all claims.

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

Both examples follow the seven stages. The Lexora numbers are illustrative and labelled as such. The upmarket example uses only the facts the published archetype article states.

### Example 1. Lexora, Full Run (Illustrative Numbers)

**Scope note.** Lexora is the fictional legal-operations company used across the Guild's example profile. Its ACV bands, cycle bands, personas and competitors come from its profile. Every count, median and rate below is illustrative, made up for this walk-through, and labelled that way. None is a real Lexora result.

**Stage 1. Beliefs (all `assumed`).**

| Claim | What Would Change Our Mind |
|-------|----------------------------|
| A1. The General Counsel signs the contract | Signer field on won contracts |
| A2. Mid-market buyers decide without the CFO | CFO appearing in won mid-market deals |
| A3. The mid-market sales cycle is 3 to 4 months | Create-to-close dates on won mid-market deals |
| A4. Spreadsheets and email are the alternative we lose to most | Alternative field on closed deals, with source |
| A5. Load-bearing: a firm count of 20 or more is the trigger that gets the meeting | Outside-firm count on won deals, and buyer statements about the trigger |
| A6. They buy because they can't see outside-counsel spend until invoices land ("We find out at quarter close") | Buyers describing, in their own words, what set off the purchase |

**Stage 2. Archetype Diagnosis.**

| Question | Answer | Evidence | Band It Points To |
|----------|--------|----------|-----------|
| 1. Cycle | Median 4 months | Last 20 closed deals (illustrative, n=20) | Hybrid or Enterprise lite |
| 2. Contract value | Median $82K | Won deals (illustrative, n=13) | Hybrid or Enterprise lite |
| 3. Buyer comfort | Legal leaders, not tech-savvy | `assumed`. No buyer records yet | Enterprise or SMB Community |
| 4. Money through product | No | Product scope: counsel spend is invoice data, not a payment flow | Embedded Fintech off |
| 5. Two sides | No | Profile disqualifies law firms: "we sell to in-house teams, not firms" | Marketplace off |

**Candidate:** Enterprise leads, with mid-market deals running on a shorter, SMB-Community-like cycle. Confidence: medium on Enterprise as the leading archetype, low on the mid-market split.

**The contradiction, stated plainly.** The cycle and value answers sit in the Hybrid band. The Enterprise ten-deal test, however, asks for 12-month cycles in 8 of 10 deals. Lexora's mid-market deals will fail that line by design. This is not a flaw in Lexora. It is the finding: the archetype test has to run per segment, not once for the whole company. The plan is to run the test on the next 10 mid-market closes and the next 10 enterprise closes, separately. Each segment is a group of 10, so each passes or fails on its own count.

**Stage 3. Grading What Already Exists.** Illustrative data: 20 closed deals in 12 months, 13 won and 7 lost. Mid-market: 10 closed, 7 won. Enterprise: 10 closed, 6 won.

- **A3 moves to `confirmed`.** Mid-market won deals (n=7) show a median create-to-close of 3.4 months, range 2.8 to 4.5. The seven cases are recent and none contradicts the 3 to 4 month band. Enterprise won deals (n=6) show a median of 6.1 months, inside the profile's 5 to 7 month band.
- **A2 is contradicted, and it is the load-bearing bet that proves wrong.** The CFO is recorded as a stakeholder on 4 of 7 mid-market wins (57%, n=7). The team had been drafting mid-market messaging that left the CFO out. Positioning would have built on it. A2 moves to contradicted. The replacement claim is "the CFO is present on about half of mid-market wins (4 of 7, 57%, n=7)," graded `seen`. A2 is archived under the `/dream` rule, not left next to its replacement.
- **A1 stays at `seen`, not `confirmed`.** The signer was recorded on 11 of 13 won deals. The General Counsel signed 9 of 11 (82%, n=11). The two other signatures were the CFO. Because two cases contradict the wording "the General Counsel signs," the claim is reworded to "the General Counsel signs most contracts," and graded `seen`.
- **A4 moves to `seen`.** Of 20 closed deals, the rep-entered alternative field reads: spreadsheets and email 11 (55%, n=20), Competitor X 5 (25%, n=20), LedgerLine Audit 1 (5%, n=20), none recorded 3 (15%, n=20). The source is rep entry, so the node records it as CRM data and not as buyer statements.

**Claims graded without a new conversation:** 4 of 6 (67%, n=6). A1 through A4 are graded. A5 and A6 remain `assumed` and become open bets, because no deal record holds either one. Both need buyer conversations.

**Stage 4. Evidence Plan for A5 (the open load-bearing claim).**

- **Deal-data pull:** the outside-firm count from the intake form on all 13 won deals (n=13). Record the count and leave blanks as blanks, not zeros.
- **Five past-behavior conversations** with recent mid-market buyers, asking: "Tell me about the last time you looked at outside-counsel spend. What set it off?" Record each answer with the buyer's own words and the firm count they gave. No answers are recorded here. This is the plan, not a result.

**Stage 5. Competitive Alternatives Node.** Source for every count: the rep-entered alternative field on 20 closed deals, which is CRM data, not buyer statements.

| Alternative | Count | Rate (n) |
|-------------|-------|----------|
| Spreadsheets and email | 11 | 55% (n=20) |
| Competitor X, the legacy e-billing platform | 5 | 25% (n=20) |
| LedgerLine Audit, the outsourced review service | 1 | 5% (n=20) |
| Do nothing | Not recorded | The CRM field has no "do nothing" option, so this count cannot be read. Logged as an evidence gap, to be asked in the A6 conversations |

Three deals have no alternative recorded. They are left out of the counts, not treated as "do nothing", because silence is not a no.

**Stage 6. Starting Segment.** Threshold used in this run: a win-rate gap under 20 points is reported as "no difference found."

| Segment | Closed (n) | Won | Win Rate (n) | Median Cycle (n) | Key Claims Confirmed |
|---------|-----------|-----|--------------|------------------|----------------------|
| Mid-Market | 10 | 7 | 70% (7 of 10) | 3.4 months (n=7) | 1 of 2 (A3 confirmed; A2 contradicted) |
| Enterprise | 10 | 6 | 60% (6 of 10) | 6.1 months (n=6) | 0 of 2 |

The 10-point win-rate gap is under the 20-point threshold, so the report says **no difference found on win rate**. The choice rests on the shorter cycle and the better-graded claims. **Recommendation:** start with Mid-Market. **Switch trigger:** if the Mid-Market win rate falls below 50% over the next 10 closed mid-market deals, reopen this stage and consider Enterprise.

**Stage 7. Write-Back.**

- **Archetype node:** Enterprise leads (mid-market on a shorter cycle), medium confidence, with the contradiction and the per-segment test plan attached.
- **Persona node, with every trait traced:**

| Persona | Trait | Source Claim | Grade |
|---------|-------|--------------|-------|
| General Counsel | Signs most contracts | A1 (reworded) | `seen`, 9 of 11 (82%) |
| General Counsel | Shares mid-market approvals with the CFO (CFO recorded as a stakeholder on 4 of 7 mid-market wins) | Replaces A2 | `seen`, 4 of 7 (57%) |
| Head of Legal Operations | Owns outside-counsel management day to day | Profile, not yet graded | `assumed` |

The Deputy GC persona has no trait with a source in this run, so it is not written to the node. That is the rule working: a persona with no traced trait does not get a persona entry.

- **Open bets node:**
  1. A5, firm count of 20 or more as the trigger. Load-bearing for the outbound opener. `assumed`. Do not build the opener on it.
  2. A6, why they buy (spend visibility before invoices land). `assumed`. Positioning's value statement may not rest on it until buyers say it.
  3. The do-nothing count, which the CRM cannot hold.
  4. The Enterprise ten-deal test, per segment. Incomplete until 10 closes per segment are recorded.
  5. Buyer comfort with software (Stage 2, question 3). `assumed`.
- **Profile write-back:** ICP Definitions gets Mid-Market as the starting segment, with its win rate and n. The profile's checked box "20+ active outside firms" is rewritten as a claim, A5, with the grade `assumed`, so the profile stops stating it as fact. Buyer Personas carries the graded traits above. Competitive Landscape carries the alternatives table with its source.
- **Re-grade dates:** A1 and A4 (`seen`) in 30 days. A3 (`confirmed`) in 90 days. Open bets carry no date and are listed for review once they have been open for a month.

**Hand-off to Positioning (the five fields, in one place; every number illustrative):**

- **Customer archetype:** Enterprise leads (medium confidence). Mid-market deals run a shorter cycle and have not yet been tested against the Enterprise ten-deal test.
- **Competitive alternatives:** spreadsheets and email 55%, Competitor X 25%, LedgerLine Audit 5% (all n=20, rep-entered CRM field). Do nothing: not recorded, open. 3 of 20 deals had no alternative recorded and are excluded.
- **Beachhead segment:** Mid-Market, meaning companies with $500M to $1.5B revenue (the profile's segment definition). 10 closed, 7 won (70%, n=10); median cycle 3.4 months (n=7). No difference found on win rate against Enterprise (threshold 20 points). Switch if mid-market win rate falls below 50% over the next 10 closes.
- **Buyer persona:** General Counsel (two traced traits), Head of Legal Operations (one `assumed` trait).
- **Open bets:** A5, A6, the do-nothing count, the per-segment test, buyer comfort with software.

**Do not build on:** A5 (the 20-firm trigger), A6 (why they buy), buyer comfort with software. Each is `assumed`. A positioning statement that needs one of them is a hypothesis and must say so.

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

- **2.0.0 (2026-10-12):** Ground-up rewrite around the archetype diagnosis and the evidence ladder. Adds the open-bets output, the seven-stage workflow with a re-grade loop, and the per-segment ten-deal test.
