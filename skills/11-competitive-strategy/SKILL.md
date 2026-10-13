---
name: gtm-competitive-strategy
description: "Deal-specific competitive strategy for active opportunities (profiles the incumbent, builds a competitive gap matrix, creates a displacement playbook with discovery questions and objection handling, and assembles a win plan with battlecard). For AEs preparing to win against a known competitor, not for prospecting outbound."
version: 1.3.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
tags: [competitive-strategy, battlecard, competitive-analysis, displacement-strategy, win-plan, competitive-positioning, compete]
requires:
  skills: []
---

# Competitive Strategy

## Overview

Deal-specific competitive strategy for active opportunities against an incumbent. Profiles the incumbent solution, maps positioning across a competitive gap matrix, creates a displacement playbook with gap-exposing discovery questions, generates competitor-specific objection handling, and assembles a step-by-step win plan. Unlike `gtm-competitive-displacement` (prospecting outbound), this is for AEs preparing to win an active deal.

**Core Principle:** Never trash the competition. It implies parity. Respond positively when a competitor is mentioned (budget is already allocated). Lead with what your product enables, not what the competitor lacks. The #1 competitor is always inertia.

---

## Role

You are a **competitive strategist and deal architect for an active competitive opportunity**, not a generic assistant. You profile the incumbent, map the competitive gap specific to this deal, and build a win plan that anticipates every objection and positioning landmine. Everything company-specific (the vertical, the competitors, the proof points, the qualification zones) comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | The account with the active deal |
| Deal stage + amount | ✅ Required | Current stage and deal value |
| Known incumbent | ✅ Required | Current solution or "unknown" (if unknown, run discovery first) |
| How incumbent identified | Optional | CRM notes, discovery call, job posting, etc. |
| Incumbent satisfaction level | Optional | Frustrated / Neutral / Satisfied / Unknown |
| Contract status (incumbent's) | Optional | Active, expiring, month-to-month, unknown |
| Primary contact (name + title) | Optional | Persona-matching drives positioning |

---

## Output Contract

Every run produces a **battlecard with the same eight sections**. The content changes per account, but the structure never does. This consistency makes battlecards reviewable across your team: a manager scanning ten battlecards never has to relearn the layout.

Core commitments: **account profile + incumbent classification + competitive gap matrix + discovery questions + objection handling + proof points + positioning landmines + win plan checklist**, organized into eight fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Account framing, vertical context |
| Buyer Personas | Persona-specific positioning and objection handling |
| Competitive Landscape | Competitor classifications, failure patterns, discovery questions, proof points |
| Value Propositions | Differentiation matrix, positioning statements |
| Proof Points | Displacement stories matched to competitive scenario |
| Qualification Criteria | ICP alignment, zone-specific positioning |
| Sales Methodology | Overrides framework defaults (if specified) |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your competitive playbook, in code. The frameworks below provide a structured approach to competitive strategy, focused on positioning, objection handling, and evidence grading. These are the defaults. They adapt to your sales methodology if different.

The evidence grades, claim standards and threat calibration are defined once, in the Epistemic Rules section below.

---

## Quick Reference

**Use this skill when:**
- You have an active deal and know (or suspect) the incumbent
- Preparing for a competitive deal review or coaching session
- Need a battlecard for a specific deal, not generic competitive intelligence
- An incumbent is entrenched and you need a displacement strategy

**Don't use when:**
- Need prospecting outbound sequences against an incumbent (use `gtm-competitive-displacement`)
- Don't know what they're using. Discovery hasn't happened (use `gtm-meeting-prep` for discovery)
- Need generic competitive intelligence across the market (maintain a competitive knowledge base instead)

**User roles:** AE (primary)
**Expected time:** 20-30 minutes per account

---

## Epistemic Rules

### Evidence Grading for Competitive Intelligence
Every competitive claim must be graded:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified: Source]` | Confirmed across 2+ accounts, documented in CRM, review sites, or customer conversations | Use in discovery questions, talk tracks, objection handling |
| **INFERRED** | `[Inferred: Basis]` | Logical conclusion from verified data or single account report | Use in positioning hypotheses. Validate during discovery |
| **UNVERIFIED** | `[Unverified: Source]` | Heard once, rumor, or unconfirmed | Do NOT use in competitive positioning. Note as a discovery target |

### Competitive Claim Standards
1. **Failure patterns must cite evidence:** "Verified across 8+ accounts" is acceptable. "Competitors sometimes have issues" is not.
2. **Proof points must include customer name and metric.** Anonymous proof points carry much less weight with a buyer.
3. **Gap matrix items must be verifiable:** "Incumbent lacks X" must be confirmable, not speculative.
4. **Discovery questions must be genuine:** if the AE already knows the answer, it is a setup, not a question. Rewrite it as a positioning statement.
5. **Objection handling scripts must be field-tested:** mark scripts as `[Field-tested]` or `[New: test and refine]`.
6. **Risk assessments must be honest:** if the competitor has a legitimate advantage, say so.

### Competitive Threat Assessment Calibration
- **HIGH**: Prospect is satisfied with incumbent, incumbent is entrenched (2+ years), contract is active, no switching cost concern from prospect, or incumbent has a genuine product advantage in one area
- **MEDIUM**: Prospect has expressed some dissatisfaction, contract timing is favorable, but incumbent has strong relationships or switching costs are non-trivial
- **LOW**: Prospect is actively frustrated, incumbent is manual/no program, switching barriers are minimal, or prospect is already evaluating alternatives

---

## Core Workflow

### Step 1: Gather CRM + Competitive Intelligence

#### 1a. Search CRM
Pull everything available:
- Account record: name, HQ, revenue, segment, states
- Current deal: stage, amount, close date, owner
- Contact records: roles, engagement level, competitive mentions
- Interaction history: discovery calls, demos, emails
- Notes: competitive context, incumbent mentions, switching barriers
- Deal health signals: pulse scores (especially "Why Us" pillar if available)

#### 1b. Identify the Incumbent
From CRM data, interaction history, and discovery notes:
- **Current solution:** What they're using today
- **How identified:** CRM notes, discovery call, job posting, or needs discovery
- **Evidence grade:** VERIFIED / INFERRED / UNVERIFIED per Epistemic Rules
- **Contract status:** Active (how long?), expiring (when?), month-to-month, unknown
- **Satisfaction level:** Frustrated, neutral, satisfied, unknown
- **Switching barriers:** Contract terms, data lock-in, process dependency, political
- **Internal champion for incumbent:** Is someone in the org an advocate for the current tool?

If incumbent is unknown, flag as a critical discovery gap and provide questions to identify it.

---

### Step 2: Profile the Incumbent

#### 2a. Classify the Incumbent
Map to `{Client Profile: Competitive Landscape}` by category, competitors in the category, and core positioning.

#### 2b. Load Competitor-Specific Intelligence
Based on classification, load from `{Client Profile: Competitive Landscape}`:
- Failure patterns / weaknesses (verified)
- Gap-exposing discovery questions
- Key gaps vs. your product
- Applicable displacement proof points

#### 2c. Assess Competitive Threat Level
Using the Competitive Threat Assessment Calibration from Epistemic Rules, assign a threat level:

| Factor | Assessment | Score |
|--------|-----------|-------|
| Prospect satisfaction with incumbent | [Frustrated / Neutral / Satisfied / Unknown] | [LOW / MEDIUM / HIGH / MEDIUM] |
| Contract status | [Expiring / Active / Month-to-month / Unknown] | [LOW / MEDIUM-HIGH / LOW / MEDIUM] |
| Switching barriers | [Minimal / Moderate / Significant] | [LOW / MEDIUM / HIGH] |
| Internal champion for incumbent | [None / Suspected / Confirmed] | [LOW / MEDIUM / HIGH] |
| Incumbent product advantage | [None / Niche / Broad] | [LOW / MEDIUM / HIGH] |

**Overall Threat Level:** Weighted average → HIGH / MEDIUM / LOW with justification.

---

### Step 3: Build Positioning Strategy

#### 3a. Qualification Zone Alignment
Rank `{Client Profile: Qualification Criteria}` by relevance to this specific deal:

| # | Zone | Relevance to This Deal | Positioning Strategy |
|---|------|----------------------|---------------------|
| 1 | [Zone] | [Assessment] | [How to position] |
| ... | ... | ... | ... |

#### 3b. Competitive Differentiation Matrix
Build a capability comparison specific to this deal (only include the identified incumbent):

| Capability | Incumbent | Your Product | Why It Matters for This Account |
|------------|-----------|-------------|-------------------------------|
| [Relevant capability 1] | [Status] | [Status] | [Specific to account] |
| [Relevant capability 2] | [Status] | [Status] | [Specific to account] |

Include only capabilities relevant to this deal, not a generic feature matrix. The "Why It Matters" column connects each capability to stated pains or business context.

#### 3c. Identify Positioning Landmines
Areas where the conversation could go badly:

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| [Topic where incumbent is strong] | [What could happen] | [How to redirect] |
| [Feature you lack] | [Prospect may ask] | [Honest response + bridge] |

Being prepared for landmines is more valuable than having perfect positioning. AEs who get surprised by competitor strengths lose credibility.

---

### Step 4: Create Displacement Playbook

#### 4a. Discovery Questions (Competitor-Specific)
Provide 5-6 questions from the competitor-specific intelligence that expose gaps WITHOUT directly attacking. Questions should feel like genuine curiosity, not accusations.

For each question, include:
- **Question:** The actual question to ask
- **What it exposes:** The specific gap or limitation this surfaces
- **If they confirm the gap:** How to pivot to your product's strength
- **If they deny the gap:** How to probe deeper or move on gracefully

#### 4b. Objection Handling Playbook

**Universal Objections (Any Competitor):**

| Objection | Response Framework | Script | Status |
|-----------|-------------------|--------|--------|
| "We already use [Competitor]" | Positive frame → Discovery | "That's great. It means you already understand the value. What's working well? What would you change?" | [Field-tested] |
| "Switching cost is too high" | Quantify ROI vs. switch cost | "What's the annual cost of staying? When we look at [metric] x 12 months, the math usually surprises people." | [Field-tested] |
| "We're building in-house" | Core vs. context | "That makes sense for core differentiators. Is [your domain] where you want to invest IT resources? We have [X]+ engineers focused just on this." | [Field-tested] |
| "Send me info" | Bridge to meeting | "Happy to. What would be most useful? ROI benchmarks or the [relevant overview] for [their situation]?" | [Field-tested] |
| "Timing isn't right" | Cost of delay | "What's the cost between now and when timing is right? At your volume, each month of [pain] is roughly $[amount]." | [Field-tested] |

**Competitor-Specific Objections:** Load from `{Client Profile: Competitive Landscape}` for the identified incumbent.

**Incumbent-Specific Objections to Prepare For:**

| If Incumbent Is | Likely Objection | Response |
|----------------|-----------------|----------|
| [Direct Competitor] | "We're integrated with [ecosystem]" | "Many of our customers use [ecosystem] for [function] and [your product] for [your domain]. They're complementary, not competitive." |
| [Direct Competitor] | "We've invested too much to switch" | "[Reference customer] had been on [competitor] for years. The switch took [X weeks] and they're now saving $[amount] annually. The question is: what's the cost of NOT switching?" |
| BPO / Service Provider | "We trust our service bureau" | "Trust is important. How do you verify what they process is accurate? What's your backup plan if they have a staffing issue?" |
| BPO / Service Provider | "They handle everything for us" | "Convenience is valuable. The question is whether you're comfortable without real-time visibility into what's being done on your behalf." |
| Manual / Spreadsheets | "It works fine for us" | "It often does. Until it doesn't. What happens if your [key person] is out for two weeks? Or you expand into a new [region/segment]?" |
| No Program | "We don't need it" | "That's a bet worth quantifying. You have $[X]M in [exposure] across [Y] [dimensions]. What's the cost if even 5% of that goes wrong?" |

#### 4c. Displacement Talk Tracks
3-4 positioning statements formatted as verbatim talk tracks:
- "When [prospect situation], [product] [specific capability]. For example, [proof point]."

Each talk track must:
- Reference the specific prospect's situation (not generic)
- Name a specific capability relevant to the competitive gap
- Include a proof point with customer name and metric
- Be readable aloud in under 20 seconds

#### 4d. Match Proof Points
Select the most relevant displacement proof points from `{Client Profile: Proof Points}` matching the competitive scenario, prospect vertical, and company size.

| Proof Point | Why It Matches This Deal | How to Use It |
|------------|------------------------|---------------|
| [Customer: Metric] | [Similarity to this prospect] | [When to deploy in the conversation] |
| [Customer: Metric] | [Similarity] | [When to deploy] |

---

### Step 5: Build Win Plan

#### Win Plan Checklist
A step-by-step action plan specific to this competitive scenario:

**Pre-Meeting:**
- [ ] Review competitive gap matrix
- [ ] Prepare 3 gap-exposing discovery questions
- [ ] Know the top 2 proof points cold
- [ ] Identify positioning landmines and prepare mitigations
- [ ] Review incumbent-specific objection handling

**During Discovery:**
- [ ] Ask gap-exposing questions (genuine curiosity, not interrogation)
- [ ] Listen for incumbent pain signals (frustration, workarounds, complaints)
- [ ] Confirm contract status and renewal timing
- [ ] Identify internal champion vs. incumbent champion
- [ ] Note exact language the prospect uses to describe pain (mirror it back)

**During Demo:**
- [ ] Lead with capabilities that address stated gaps (not a feature tour)
- [ ] Show proof points from comparable companies
- [ ] Demonstrate the specific workflow that the incumbent does poorly
- [ ] Address known objections proactively before they're raised
- [ ] End with "How does this compare to your current experience?"

**Post-Meeting:**
- [ ] Send follow-up referencing specific pain they articulated (use their words)
- [ ] Include the most relevant proof point with permission to reference
- [ ] Propose next step with clear timeline
- [ ] If multi-threaded, send persona-specific follow-ups to each stakeholder
- [ ] Update CRM with competitive intelligence learned

---

### Step 6: Competitive Strategy Summary

1. **Account**: Name, deal stage, amount, owner
2. **Incumbent**: Current solution + category + evidence grade
3. **Competitive Threat Level**: HIGH / MEDIUM / LOW with factor-by-factor assessment
4. **Primary Positioning**: Which qualification zone is strongest for this deal
5. **Top 3 Competitive Gaps to Exploit**: Specific gaps the incumbent can't fill
6. **Positioning Landmines**: Where the conversation could go badly + mitigations
7. **Displacement Proof Point**: Most relevant case study for this scenario
8. **Critical Discovery Gap**: What we still need to learn about their current solution
9. **Win Strategy Summary**: 2-3 sentences on how to win this deal competitively
10. **Risk Assessment**: Where the competitor could beat you (honest evaluation)
11. **Recommended Next Steps**: Specific actions with timeline

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default): `[COMPANY]_Competitive_Strategy.md`
- **Option B: HTML:** Styled battlecard with incumbent badge and gap matrix
- **Option C: PDF:** Python + reportlab, single page, letter size

### Battlecard Sections (8 Sections)
1. **Account & Incumbent Summary:** Firmographics, deal stage, incumbent, category, contract status, satisfaction, competitive threat level. Include INCUMBENT BADGE at top.
2. **Competitive Gap Matrix:** Side-by-side capability comparison with "Why It Matters" column. Visual scoring (checkmarks/warnings/X marks).
3. **Winning Zone Strategy:** Primary positioning for this deal, supporting points, where to steer vs. avoid conversations. Include positioning landmines.
4. **Discovery Questions:** 5-6 competitor-specific, talk-track-ready questions with pivot guidance.
5. **Displacement Talk Tracks:** 3-4 verbatim positioning statements.
6. **Objection Handling Playbook:** 4-5 likely objections with scripted responses (universal + competitor-specific). Field-tested labels.
7. **Proof Points & Reference Stories:** 2-3 matched displacement stories with customer, scenario match, key metric, source label.
8. **Win Plan Checklist:** Pre-meeting → During Discovery → Demo → Post-Meeting actions specific to this competitive scenario.

**Color-code by competitive threat level:**
- HIGH threat = red accent
- MEDIUM threat = yellow accent
- LOW threat = green accent

---

## Examples

### Example 1: Incumbent Renewal, Oldgate Ledger Pro at Brackhaven Memorial Gardens

**Context:** Owen Pruitt, Account Executive (illustrative assignment), has an ACTIVE deal at Stage 5 Negotiate with Brackhaven Memorial Gardens, a two-site combination with 11,000 plots (profile). The deal is $21,576 a year at list (two sites at $10,788). The incumbent is Oldgate Ledger Pro, a legacy on-premise system whose renewal is in March 2027, about five months out. Stonemark was also evaluated, and it gets its own example below.

**Input:** "Build a competitive strategy for Brackhaven Memorial Gardens. They run Oldgate, and the renewal is in March 2027."

**Step 1: CRM Intelligence:**
- Account: Brackhaven Memorial Gardens, combination, 2 sites, 11,000 plots, paper plot maps (profile)
- Deal: Stage 5 Negotiate, $21,576 a year at list, owned by Owen Pruitt, 19 days in stage (illustrative)
- Contacts: Ruth Ellery, GM (champion). Walt Okonkwo, Operations Director (skeptic). Priscilla Dunmore, pre-need manager. Family board chair (economic buyer, one call). Contact counts are illustrative.
- Discovery notes (illustrative quote): Ruth: "We can't tell which plots are sold without going to the binder."
- Incumbent: Oldgate Ledger Pro. [Inferred: Ruth named it on one call (illustrative)]

**Step 2: Incumbent Profile:**
- Classification: Direct (legacy), an on-premise system. Profile category: Oldgate Ledger Pro
- Their pitch: "Mature, deep accounting." Research weaknesses: $10,000 to $50,000 upfront plus 20% a year maintenance, poor mobile, no AI. [Inferred: research estimate from the profile, dated 2026-03-27. Not yet checked with this buyer]
- Satisfaction: Neutral. Ruth tolerates it, and Walt works from paper. [Inferred: discovery calls (illustrative)]
- Contract status: Renewal in March 2027. [Inferred: Ruth stated the date on one call (illustrative)]
- Switching barriers: Moderate. Two sites of plot records and a trust fund ledger export to scope.
- Internal champion for incumbent: None identified. [Inferred: nobody defended Oldgate on any call]

**Step 2c: Threat Assessment:**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Neutral | MEDIUM |
| Contract | Renewal in March 2027, a favorable window | LOW |
| Switching barriers | Moderate (two sites of records, ledger export) | MEDIUM |
| Internal champion for incumbent | None identified | LOW |
| Incumbent product advantage | Niche (accounting depth) | MEDIUM |

**Overall: MEDIUM threat.** The skill sets no weights, so each factor counts equally here. MEDIUM is 2, LOW is 1, and the five factors sum to 8 (2 + 1 + 2 + 1 + 2). 8 ÷ 5 = 1.6 on a 1 (LOW) to 3 (HIGH) scale, which rounds to MEDIUM. The main risk is inertia: Walt's paper process has no one pushing for change.

**Step 3b: Gap Matrix:**

| Capability | Oldgate Ledger Pro | PlotIQ | Why It Matters for Brackhaven |
|-----------|---------|--------|----------------------|
| Mobile use by the grounds crew | Poor mobile (research estimate) | Mobile field app | Walt needs work orders in the field so the crew can find a plot in seconds |
| Unsold-plot visibility | Unknown. Ask in discovery (question 1 below) | Plot inventory digitization shows unsold plots | Ruth's unsold-plot count depends on this, and it is not in Oldgate's known features |
| Trust fund records | Deep accounting (their pitch) | Records and Trust Compliance module | A state auditor has to accept the record. Show the output side by side with the filing format |
| Cost | $10,000 to $50,000 upfront plus 20% a year maintenance (research estimate) | $899 a month per site, one price, $5,000 setup (profile) | Year one at list for two sites is $21,576 plus setup (profile price list) |
| Time to live | 120 to 180 days (research estimate) | 6 weeks (profile) | The March 2027 renewal leaves room to go live before the window closes |

**Step 3c: Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| "Oldgate has deep accounting" | Ruth or the board chair hears depth as safety | "Oldgate is strong on accounting. Our trust records are built for what a state auditor reads, and we can show you the output next to your current ledger." |
| Migrating two sites of records | Staff fear losing the paper binders | "We start with the plot map, which is the first module. Our implementation team digitizes the maps and deeds in weeks 2 to 3 (profile)." |
| Stonemark was also evaluated | The board compares two new tools | "Stonemark is built for enterprise mapping. We put records, trust compliance and pre-need in one system, live in six weeks." |

**Step 4a: Discovery Questions (from the profile's Competitive Discovery Questions):**
1. "Where does the plot map live today, and when was it last updated?" → Exposes: how old the plot map is, and whether sales can see it. If confirmed (a binder, years old): pivot to the plot inventory digitization, which runs in weeks 2 to 3. If denied (a current digital map exists): probe whether it shows sold and unsold plots.
2. "Which system runs the funeral side, and who maintains it?" → Exposes: a second system and key-person dependency. If confirmed: pivot to the combined records view. If denied: ask how the pre-need leads are tracked today.
3. "When does your software contract renew, and what did the last quote include for support?" → Confirms the March 2027 date and the support cost. If confirmed: align the evaluation to the renewal decision. If denied: ask who makes the renewal decision.

**Step 5: Win Plan highlights:**
- Renewal in March 2027. Plan the evaluation to finish before the renewal decision. The 60 to 90 day evaluation window is an illustrative assumption to calibrate with Ruth.
- The demo leads with an unsold-plot list drawn from Brackhaven's own records, not a feature tour. Ask Ruth to pull the count of plots with no recorded sale. Do not estimate that number.
- Risk: the "deep accounting" argument lands with the family board chair. Mitigation: show the trust report output next to the state filing format.
- Economic buyer: the family board chair. Ruth builds the case, and the number she brings must be her own count.

**Output:** Full 8-section battlecard. Threat level: MEDIUM (yellow accent). Strongest competitive lever: unsold-plot visibility and records a state auditor accepts, both shown in Brackhaven's own records. Honest risk: Oldgate's accounting depth, and the chance that the paper process stays the default.

---

### Example 2: Stonemark Pilot Request, Brackhaven Memorial Gardens (Non-Success)

**Context:** Three weeks after Example 1 (timing illustrative), the same deal is now a bake-off. Walt Okonkwo has asked for a Stonemark pilot before he signs off. The family board chair has not joined a call since the board meeting moved. Oldgate still renews in March 2027. This is the non-success case: the buyer's own criterion favors the rival, and the battlecard has to say so rather than hide it.

**Input:** "Build a competitive strategy for Brackhaven. Walt has asked for a Stonemark pilot."

**Step 1: CRM Intelligence:**
- Deal: Stage 5 Negotiate, $21,576 a year at list, 40 days in stage, close date pushed three times (all illustrative)
- Contacts: Ruth Ellery (champion, no reply in 16 days, illustrative). Walt Okonkwo (asked for the pilot). Family board chair (one call)
- Discovery notes (illustrative quote): Walt: "Show me it on one section of our map before I sign anything."
- Competitors: Stonemark (pilot requested, the rival now). Oldgate (incumbent, renews March 2027). [Inferred: Walt named Stonemark on one call (illustrative)]

**Step 2: Rival Profile:**
- Stonemark: enterprise cemetery mapping. Their pitch: "The best mapping in the category." Research estimates: about $1,500 to $2,500 a month, 90 to 120 days to live, no AI. [Inferred: research estimate from the profile, dated 2026-03-27]
- Their advantage: depth of mapping. [Inferred: their pitch, and Walt's interest in the map]
- Their gap: records and trust compliance are not part of their positioning. [Inferred: profile positioning, not yet tested with the buyer]

**Step 2c: Threat Assessment (Stonemark, the rival in the pilot):**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Walt wants a pilot before he decides. Our proof is not yet in front of him | HIGH |
| Contract | Stonemark has no contract yet, and a pilot would be its first step. Oldgate renews in March 2027 | MEDIUM |
| Switching barriers | A pilot needs a load of Brackhaven's map data | MEDIUM |
| Internal champion for the rival | Suspected: Walt sees the mapping as the first step | MEDIUM |
| Product advantage | Broad: mapping depth is the rival's core pitch | HIGH |

**Overall: HIGH threat.** The five factors average 2.4 (MEDIUM is 2, HIGH is 3, so 2 + 2 + 2 + 3 + 3 = 12, and 12 ÷ 5 = 2.4). The average alone reads MEDIUM. The calibration still gives HIGH, because the rival holds a genuine product advantage in one area, mapping depth, and that is the buyer's stated criterion.

**Step 3b: Gap Matrix:**

| Capability | Stonemark | PlotIQ | Why It Matters for Brackhaven |
|-----------|-----------|--------|-----------------------------------|
| Mapping depth | Enterprise mapping, their core pitch [Inferred] | Plot inventory digitization of paper maps and deeds | Walt's pilot criterion sits on the map. Their strength here is real, and we say so |
| Records and trust compliance in one system | Not in their positioning [Unverified: ask] | Records and Trust Compliance module | A state auditor reads the trust record. This is the part Walt has not yet seen |
| Pre-need leads in the same system | [Unverified: ask] | Pre-Need CRM and Lead Scoring | Priscilla's leads land in one place with a follow-up owner |
| Time to live | 90 to 120 days (research estimate) | 6 weeks (profile) | The timing decides whether a pilot can finish before the March 2027 renewal |
| Price | About $1,500 to $2,500 a month (research estimate) | $899 a month per site, one price (profile) | Shows the monthly gap without claiming their total cost |

**Step 3c: Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| "Stonemark's mapping is better" | Walt agrees, and the deal goes to the rival | "You're right that their mapping is built for enterprise. Ask them whether one system holds the trust record and the pre-need leads. Ask us the same question, and we'll show you." |
| The pilot scope | A pilot on a small part of the map makes both tools look equal | Propose one shared pilot section, with the trust report and one pre-need lead run through both tools, scored against Walt's own criteria |
| The price comparison | The board compares monthly cost only | Add the cost of a missed trust filing and of unsold plots, using Brackhaven's own counts. Do not state a dollar figure for the risk |

**Step 4a: Discovery Questions (for the open pilot question):**
1. "What would a pilot have to show you before the family board can say yes?" → Exposes the buyer's real criteria. If confirmed (specific criteria): build the pilot around them. If denied (no criteria yet): ask Walt to write them with you.
2. "Which records would you need on day one, and where do they live?" → Exposes the migration load. If confirmed (paper binders): start the pilot with the plot map. If denied: ask who maintains the current records.
3. "Would the board also want to see the trust fund report, or only the map?" → Exposes whether the trust record is part of the decision. If confirmed: run the trust report inside the pilot. If denied: ask what the state auditor requires.

**Step 5: Win Plan:**
- Ask Walt to write the pilot criteria in his own words, before any demo.
- Put the family board chair on the call where the criteria are set. The economic buyer is still only one call deep.
- Propose one shared pilot: one section of the plot map, plus one trust report run through both tools. Dates to be set with Ruth.
- Finish the pilot decision before the Oldgate renewal in March 2027. Ask Ruth for the renewal notice date. Do not assume it.
- Re-score the threat once the pilot criteria are written.

**Risk Assessment:** Stonemark could win the pilot on the map. If the family picks the deeper map, we lose on mapping, and Oldgate renews by default. The rival's mapping is the buyer's stated criterion, so positioning alone will not win this deal.

**Output:** Full battlecard, HIGH threat (red accent). Win strategy: test records and trust compliance together, on Walt's criteria, before the renewal date. Do not claim we beat Stonemark on mapping. If the criteria test only the map, tell Ruth so, and reassess the deal.

---

## Common Patterns

### Pattern: Unknown Incumbent
**When:** Incumbent hasn't been identified through discovery.
**Action:** Flag as critical gap. Provide the discovery questions needed to identify the incumbent. Build a generic competitive strategy that covers the most likely scenarios for this account type. Recommend running `gtm-meeting-prep` for discovery to uncover the incumbent.

### Pattern: Dual-Tool Pain
**When:** Account uses two separate tools (e.g., competitor A for one function + competitor B for another).
**Action:** Build the strategy around the unification angle. Reference proof points where your product replaced both tools simultaneously. The gap matrix shows the silo between the two tools as the primary pain.

### Pattern: Renewal Window
**When:** Contract renewal date is known (or discovered during the process).
**Action:** Align the competitive strategy timeline to arrive 60-90 days before renewal. The win plan should create urgency around evaluation timing. Email 4 in displacement sequences (if combined with `gtm-competitive-displacement`) specifically targets this window.

### Pattern: Incumbent Champion (Blocker)
**When:** Someone in the prospect org is an advocate for the current tool and may resist change.
**Action:** Identify the blocker's concerns (job security, familiarity, political capital invested in choosing the current tool). Build positioning that neutralizes without confronting: "The platform doesn't replace your team's expertise. It amplifies it." Consider multi-threading around the blocker to the economic buyer.

---

## Troubleshooting

### "We don't have competitive intelligence for this specific competitor"
**Solution:** Classify the competitor into the closest category from `{Client Profile: Competitive Landscape}`. Use category-level gaps and positioning. Build competitor-specific intelligence from the discovery call by using the general discovery questions. Document what you learn for future deals. Tag all claims as `[Inferred: category-level]`.

### "Prospect is satisfied with incumbent (no dissatisfaction signal)"
**Solution:** This is a HIGH threat assessment. Don't try to create dissatisfaction. Instead, lead with what's possible that they may not know they're missing. Use the "Many teams tell us..." approach to surface latent pain. Focus on macro trends from `{Client Profile: Competitive Landscape}` that make their current approach increasingly risky over time.

### "Incumbent is a department within the prospect company (internal build)"
**Solution:** Classify as Manual/Spreadsheets but add the "build vs. buy" objection handling: "Core vs. context. Is [your domain] where you want to invest IT resources?" Reference proof points about engineering focus ([X]+ engineers on [domain] alone). Acknowledge their internal expertise while positioning the scale and coverage challenge.

### "Multiple competitors in play (bake-off scenario)"
**Solution:** Build strategy against the strongest competitor first. Add a section addressing the secondary competitor. In the win plan, identify which competitor poses the greater threat and allocate positioning energy accordingly. The gap matrix can include multiple columns if helpful.

### "Prospect likes the incumbent but is evaluating out of obligation (procurement requirement)"
**Solution:** This is effectively a HIGH threat. The incumbent is the default winner. Strategy must create genuine preference, not just check-the-box participation. Focus on demonstrating capabilities the prospect didn't know they needed. Use discovery questions to uncover pain they haven't articulated to their current vendor. Win plan should target multi-threading to a stakeholder who isn't invested in the incumbent.

---

## Best Practices

### Do's
- **Respond positively to competitor mentions:** budget is allocated, no new capital outlay needed.
- **Lead with enablement, not criticism:** "Here's what's possible" beats "Here's what's broken".
- **Use competitor-specific discovery questions:** genuine curiosity exposes gaps better than accusations.
- **Include an honest risk assessment:** where could the competitor win? Addressing this shows credibility.
- **Match proof points to the competitive scenario:** displacement stories for displacement deals, not generic.
- **Prepare for positioning landmines:** knowing where the conversation could go badly is more valuable than perfect positioning.
- **Grade your evidence:** tag competitive claims per Epistemic Rules to calibrate confidence.

### Don'ts
- **Don't trash the competition:** it implies parity ("we are peerless in this space").
- **Don't tell the prospect what pain they have:** let them articulate it through discovery questions.
- **Don't use generic feature matrices:** every capability row must connect to this specific account's situation.
- **Don't ignore inertia:** even when competing against a named vendor, the real battle is against the comfort of the status quo.
- **Don't assume the prospect's dissatisfaction:** let discovery questions surface it naturally.
- **Don't skip the win plan:** a battlecard without action steps is a document, not a strategy.

### Quality Checklist
- [ ] Incumbent identified or flagged as unknown with discovery plan
- [ ] Competitor profiled using verified intelligence (not generic)
- [ ] Competitive threat level assessed with factor-by-factor justification
- [ ] Discovery questions expose gaps without attacking, with pivot guidance
- [ ] Objection handling uses field-tested scripts
- [ ] Proof points match the competitive scenario (vertical, size, competitor)
- [ ] Honest risk assessment included
- [ ] Positioning landmines identified with mitigations
- [ ] Win strategy is specific to this deal (not generic "displace the incumbent")
- [ ] Gap matrix connects each capability to this account's stated pains
- [ ] Talk tracks are verbatim-ready (rep can read aloud in <20 seconds)
- [ ] Competitive philosophy respected (positive frame, never trash)
- [ ] Win plan has actionable steps per deal stage

---

## Integration with Other Skills

- **`gtm-competitive-displacement`:** For prospecting outbound sequences against a known incumbent. Complementary: competitive strategy is for active deals (AE), displacement is for pipeline generation (BDR/AE).
- **`gtm-meeting-prep`:** Run competitive strategy first, then meeting prep to incorporate competitive positioning into discovery or demo structure.
- **`gtm-stakeholder-mapping`:** Org map reveals who might be an incumbent champion (Blocker role). Feed this into the competitive strategy.
- **`gtm-deal-pulse`:** Competitive strategy informs the "Why Us" pillar of deal health scoring.
- **`gtm-call-coaching`:** After competitive conversations, run call coaching to assess how well the rep executed the competitive strategy.
- **`gtm-research-outbound`:** For public companies, financial intelligence can reveal competitive pressure points (e.g., earnings miss making cost optimization urgent).

---

## Changelog

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (Epistemic Rules, Competitive Threat Assessment Calibration) moved to an explicit Methodology section; `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release; migrated from competitive strategy builder
- Generalized via Client Profile block with configurable defaults
- Preserved all competitor intelligence structure: 7 categories, failure patterns, gaps, educational positioning
- Preserved competitive philosophy ("never trash," "#1 competitor is inertia")
- Preserved Winning Zone alignment, differentiation matrix, win plan checklist
- Preserved field-tested objection handling (universal + competitor-specific)
- Multi-format artifact generation replacing reportlab-only
