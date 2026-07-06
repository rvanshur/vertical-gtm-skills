---
name: gtm-competitive-strategy
description: "Deal-specific competitive strategy for active opportunities — profiles the incumbent, builds a competitive gap matrix, creates a displacement playbook with discovery questions and objection handling, and assembles a win plan with battlecard. For AEs preparing to win against a known competitor, not for prospecting outbound."
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [competitive-strategy, battlecard, competitive-analysis, displacement-strategy, win-plan, competitive-positioning, compete]
requires:
  skills: []
---

# Competitive Strategy

## Overview

Deal-specific competitive strategy for active opportunities against an incumbent. Profiles the incumbent solution, maps positioning across a competitive gap matrix, creates a displacement playbook with gap-exposing discovery questions, generates competitor-specific objection handling, and assembles a step-by-step win plan. Unlike `gtm-competitive-displacement` (prospecting outbound), this is for AEs preparing to win an active deal.

**Core Principle:** Never trash the competition — it implies parity. Respond positively when a competitor is mentioned (budget is already allocated). Lead with what your product enables, not what the competitor lacks. The #1 competitor is always inertia.

---

## Role

You are a **competitive strategist and deal architect for an active competitive opportunity** — not a generic assistant. You profile the incumbent, map the competitive gap specific to this deal, and build a win plan that anticipates every objection and positioning landmine. Everything company-specific — the vertical, the competitors, the proof points, the qualification zones — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

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

Every run produces a **battlecard with the same eight sections** — the content changes per account; the structure never does. This consistency makes battlecards reviewable across your team: a manager scanning ten battlecards never has to relearn the layout.

Core commitments: **account profile + incumbent classification + competitive gap matrix + discovery questions + objection handling + proof points + positioning landmines + win plan checklist** — organized into eight fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

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

Your competitive playbook, in code. The frameworks below provide a structured approach to competitive strategy — focused on positioning, objection handling, and evidence grading. These are the defaults; they adapt to your sales methodology if different.

### Epistemic Rules

#### Evidence Grading for Competitive Intelligence
Every competitive claim must be graded:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified — Source]` | Confirmed across 2+ accounts, documented in CRM, review sites, or customer conversations | Use in discovery questions, talk tracks, objection handling |
| **INFERRED** | `[Inferred — Basis]` | Logical conclusion from verified data or single account report | Use in positioning hypotheses; validate during discovery |
| **UNVERIFIED** | `[Unverified — Source]` | Heard once, rumor, or unconfirmed | Do NOT use in competitive positioning; note as a discovery target |

#### Competitive Claim Standards
1. **Failure patterns must cite evidence** — "Verified across 8+ accounts" is acceptable; "competitors sometimes have issues" is not
2. **Proof points must include customer name and metric** — anonymous proof points have 50% less credibility
3. **Gap matrix items must be verifiable** — "Incumbent lacks X" must be confirmable, not speculative
4. **Discovery questions must be genuine** — if the AE already knows the answer, it is a setup, not a question; rewrite as a positioning statement
5. **Objection handling scripts must be field-tested** — mark scripts as `[Field-tested]` or `[New — test and refine]`
6. **Risk assessments must be honest** — if the competitor has a legitimate advantage, say so

### Competitive Threat Assessment Calibration
- **HIGH**: Prospect is satisfied with incumbent, incumbent is entrenched (2+ years), contract is active, no switching cost concern from prospect, or incumbent has a genuine product advantage in one area
- **MEDIUM**: Prospect has expressed some dissatisfaction, contract timing is favorable, but incumbent has strong relationships or switching costs are non-trivial
- **LOW**: Prospect is actively frustrated, incumbent is manual/no program, switching barriers are minimal, or prospect is already evaluating alternatives

---

## Quick Reference

**Use this skill when:**
- You have an active deal and know (or suspect) the incumbent
- Preparing for a competitive deal review or coaching session
- Need a battlecard for a specific deal, not generic competitive intelligence
- An incumbent is entrenched and you need a displacement strategy

**Don't use when:**
- Need prospecting outbound sequences against an incumbent (use `gtm-competitive-displacement`)
- Don't know what they're using — discovery hasn't happened (use `gtm-meeting-prep` for discovery)
- Need generic competitive intelligence across the market (maintain a competitive knowledge base instead)

**User roles:** AE (primary)
**Expected time:** 20-30 minutes per account

---

## Epistemic Rules

### Evidence Grading for Competitive Intelligence
Every competitive claim must be graded:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified — Source]` | Confirmed across 2+ accounts, documented in CRM, review sites, or customer conversations | Use in discovery questions, talk tracks, objection handling |
| **INFERRED** | `[Inferred — Basis]` | Logical conclusion from verified data or single account report | Use in positioning hypotheses; validate during discovery |
| **UNVERIFIED** | `[Unverified — Source]` | Heard once, rumor, or unconfirmed | Do NOT use in competitive positioning; note as a discovery target |

### Competitive Claim Standards
1. **Failure patterns must cite evidence** — "Verified across 8+ accounts" is acceptable; "competitors sometimes have issues" is not
2. **Proof points must include customer name and metric** — anonymous proof points have 50% less credibility
3. **Gap matrix items must be verifiable** — "Incumbent lacks X" must be confirmable, not speculative
4. **Discovery questions must be genuine** — if the AE already knows the answer, it is a setup, not a question; rewrite as a positioning statement
5. **Objection handling scripts must be field-tested** — mark scripts as `[Field-tested]` or `[New — test and refine]`
6. **Risk assessments must be honest** — if the competitor has a legitimate advantage, say so

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

Include only capabilities relevant to this deal — not a generic feature matrix. The "Why It Matters" column connects each capability to stated pains or business context.

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
| "We already use [Competitor]" | Positive frame → Discovery | "That's great — it means you already understand the value. What's working well? What would you change?" | [Field-tested] |
| "Switching cost is too high" | Quantify ROI vs. switch cost | "What's the annual cost of staying? When we look at [metric] x 12 months, the math usually surprises people." | [Field-tested] |
| "We're building in-house" | Core vs. context | "That makes sense for core differentiators. Is [your domain] where you want to invest IT resources? We have [X]+ engineers focused just on this." | [Field-tested] |
| "Send me info" | Bridge to meeting | "Happy to — what would be most useful? ROI benchmarks or the [relevant overview] for [their situation]?" | [Field-tested] |
| "Timing isn't right" | Cost of delay | "What's the cost between now and when timing is right? At your volume, each month of [pain] is roughly $[amount]." | [Field-tested] |

**Competitor-Specific Objections:** Load from `{Client Profile: Competitive Landscape}` for the identified incumbent.

**Incumbent-Specific Objections to Prepare For:**

| If Incumbent Is | Likely Objection | Response |
|----------------|-----------------|----------|
| [Direct Competitor] | "We're integrated with [ecosystem]" | "Many of our customers use [ecosystem] for [function] and [your product] for [your domain]. They're complementary, not competitive." |
| [Direct Competitor] | "We've invested too much to switch" | "[Reference customer] had been on [competitor] for years. The switch took [X weeks] and they're now saving $[amount] annually. The question is: what's the cost of NOT switching?" |
| BPO / Service Provider | "We trust our service bureau" | "Trust is important. How do you verify what they process is accurate? What's your backup plan if they have a staffing issue?" |
| BPO / Service Provider | "They handle everything for us" | "Convenience is valuable. The question is whether you're comfortable without real-time visibility into what's being done on your behalf." |
| Manual / Spreadsheets | "It works fine for us" | "It often does — until it doesn't. What happens if your [key person] is out for two weeks? Or you expand into a new [region/segment]?" |
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
- **Option A: Markdown** (default) — `[COMPANY]_Competitive_Strategy.md`
- **Option B: HTML** — Styled battlecard with incumbent badge and gap matrix
- **Option C: PDF** — Python + reportlab, single page, letter size

### Battlecard Sections (8 Sections)
1. **Account & Incumbent Summary** — Firmographics, deal stage, incumbent, category, contract status, satisfaction, competitive threat level. Include INCUMBENT BADGE at top.
2. **Competitive Gap Matrix** — Side-by-side capability comparison with "Why It Matters" column. Visual scoring (checkmarks/warnings/X marks).
3. **Winning Zone Strategy** — Primary positioning for this deal, supporting points, where to steer vs. avoid conversations. Include positioning landmines.
4. **Discovery Questions** — 5-6 competitor-specific, talk-track-ready questions with pivot guidance.
5. **Displacement Talk Tracks** — 3-4 verbatim positioning statements.
6. **Objection Handling Playbook** — 4-5 likely objections with scripted responses (universal + competitor-specific). Field-tested labels.
7. **Proof Points & Reference Stories** — 2-3 matched displacement stories with customer, scenario match, key metric, source label.
8. **Win Plan Checklist** — Pre-meeting → During Discovery → Demo → Post-Meeting actions specific to this competitive scenario.

**Color-code by competitive threat level:**
- HIGH threat = red accent
- MEDIUM threat = yellow accent
- LOW threat = green accent

---

## Examples

### Example 1: Direct Competitor Displacement — Enterprise Account

**Context:** AE has active deal at Demo stage against [Primary Competitor]. Deal value $180K. Discovery notes confirm frustration with manual processing.

**Input:** "Build a competitive strategy for [Enterprise Account] — they're currently using [Primary Competitor]."

**Step 1 — CRM Intelligence:**
- Account: [Enterprise Account], HQ [City, State], [industry-specific description]
- Deal: Demo stage, $180K, owned by [AE Name], close date in 45 days
- Contacts: VP [Function] (primary champion, 3 meetings), [Manager] (attended demo), CFO (briefed but not engaged)
- Discovery notes: "Manual processing taking 12+ min each. Service quality has declined. Architecture doesn't fit our model. Want to automate across all locations."
- Incumbent confirmed: [Primary Competitor] [Verified — prospect stated in discovery call]

**Step 2 — Incumbent Profile:**
- Classification: Direct Software, Medium-Low displacement difficulty
- Satisfaction: Frustrated [Verified — discovery call notes]
- Contract status: Annual, renewal in 4 months [Verified — prospect mentioned]
- Switching barriers: Moderate — data migration, 2 years of historical data
- Internal champion for incumbent: None identified [Inferred — no one defended incumbent in discovery]
- Failure patterns matched: broken automation, manual bottleneck (12+ min confirmed), service decline, architecture mismatch

**Step 2c — Threat Assessment:**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Frustrated | LOW |
| Contract | Expiring in 4 months | LOW |
| Switching barriers | Moderate (data migration) | MEDIUM |
| Incumbent champion | None identified | LOW |
| Incumbent advantage | Ecosystem integration | MEDIUM |

**Overall: LOW-MEDIUM threat.** Favorable competitive position. Primary risk: ecosystem lock-in.

**Step 3b — Gap Matrix:**

| Capability | [Primary Competitor] | [Your Product] | Why It Matters for [Account] |
|-----------|---------|--------|----------------------|
| Process automation | Manual (12+ min/unit) | Automated (48 sec) | Account processes 1,500+ units/month — this is 375+ hours saved |
| Multi-entity support | Single-model focused | Built for complex orgs | Account has 600+ locations; need multi-entity architecture |
| Support responsiveness | Declining post-acquisition | Dedicated customer success | VP cited support as key frustration |
| Accuracy | 1-2% error rate | Built-in verification | At account volume, 1% errors = 15+ wrong actions per month |
| System integration | Basic | Deep ERP integration | Account needs data flowing without manual touchpoints |

**Step 3c — Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| Ecosystem integration | Account may use [ecosystem] for other functions | "[Your product] and [ecosystem] are complementary — many customers use both. We're not asking you to leave [ecosystem], just to upgrade your [domain] tool." |
| Data migration | 2 years of historical data | "[Reference customer] migrated [large dataset] successfully. Our implementation team has done this dozens of times. We can walk through the migration plan." |

**Step 4a — Discovery Questions (for remaining gaps):**
1. "Walk me through your process start to finish — how much is truly automated vs. manual?" → Exposes: manual bottleneck. If confirmed: pivot to automation speed proof point. If denied: "How does that look at the location level vs. centralized?"
2. "How does [competitor] handle your multi-entity structure across 600+ locations?" → Exposes: architecture gap. If confirmed: pivot to multi-entity design. If denied: probe on location-level configuration.
3. "When something goes wrong, how quickly does [competitor] support resolve it?" → Exposes: service decline. If confirmed: pivot to dedicated customer success model.

**Step 5 — Win Plan highlights:**
- Renewal in 4 months → position evaluation timeline to align with renewal decision
- Demo should lead with automation speed — this is the biggest visual differentiator
- Risk: ecosystem argument. Mitigation prepared.
- CFO not engaged — recommend champion propose a business case to CFO using ROI data

**Output:** Full 8-section battlecard. Threat level: LOW-MEDIUM (green-yellow accent). Strongest competitive lever: Processing speed at account's volume.

---

### Example 2: Manual Process — PE-Backed Mid-Market Account

**Context:** AE at Discovery stage, prospect uses spreadsheets. $95K deal.

**Input:** "Build a competitive strategy for [Mid-Market Account] — they manage processes with spreadsheets."

**Step 1 — CRM Intelligence:**
- Deal: Discovery stage, $95K, 60-day close timeline
- Contacts: Controller (primary, 2 calls), [Manager] (1 call), CFO (not yet engaged)
- Discovery notes: "One person manages everything for the entire company using Excel. Process works but they know it's risky. Controller wants to modernize before the next PE operating review."
- Incumbent: Manual/Spreadsheets [Verified — prospect described process in discovery]

**Step 2c — Threat Assessment:**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Neutral — "works but risky" | MEDIUM |
| Contract | N/A (no vendor) | LOW |
| Switching barriers | Minimal — no data to migrate | LOW |
| Incumbent champion | The key person (defensive?) | MEDIUM |
| Incumbent advantage | "It works" / familiarity / free | MEDIUM |

**Overall: MEDIUM threat.** Inertia is the primary competitor. The key person may resist change (threatens their role). PE operating review creates urgency.

**Step 3b — Gap Matrix:**

| Capability | Spreadsheets | [Your Product] | Why It Matters for [Account] |
|-----------|-------------|--------|-----------------------------------|
| Key-person dependency | Single person | Team platform | PE sponsors flag single-point-of-failure in operating reviews |
| Scalability | Breaks at volume | Enterprise-grade | 45+ locations in 30+ states |
| Audit trail | None | Complete documentation | PE compliance requirements demand audit trails |
| Multi-region automation | Manual per region | Automated across all regions | 30+ regions with different requirements |
| Error prevention | Human error risk | Built-in verification | One mistake at this scale = material risk |

**Step 3c — Positioning Landmines:**

| Landmine | Risk | Mitigation |
|----------|------|-----------|
| "We can't afford it" | No existing budget line | "The question isn't whether you can afford it — it's whether you can afford not to. One major error on a $500K engagement costs more than a year of the platform." |
| Key person feels threatened | May resist adoption | "The platform doesn't replace your expert — it makes them 10x more effective. Their knowledge of your business becomes amplified by automation, not replaced." |
| Internal build proposal | IT may want to build custom | "Core vs. context: is [your domain] where [Account] wants to invest engineering resources? We have [X]+ engineers focused on this alone." |

**Step 4 — Playbook:** Educational selling approach. Discovery questions help the prospect quantify their own risk rather than telling them they have a problem. PE operating review creates natural urgency — "before your next operating review" framing. Talk tracks emphasize single-point-of-failure at enterprise scale.

**Output:** Full battlecard, MEDIUM threat (yellow accent). Win strategy: Quantify risk first, then show automation. Lead with PE accountability angle for Controller/CFO. Protect the key person's role in positioning.

---

### Example 3: No Program — Mid-Market Account (Educational Selling)

**Context:** AE discovers prospect has no program at all. Discovery stage, $45K deal.

**Input:** "Build a competitive strategy for [Account] — they have no program."

**Step 1 — CRM Intelligence:**
- Deal: Discovery stage, $45K
- Contacts: CFO (1 call), Head of [Function] (2 calls — primary champion)
- Discovery notes: "Didn't realize they needed [your solution]. Head of [Function] started researching after a $200K loss on a project where they hadn't taken protective action."
- Incumbent: No Program [Verified — prospect confirmed no process]

**Step 2c — Threat Assessment:**

| Factor | Assessment | Threat |
|--------|-----------|--------|
| Satisfaction | Pain is fresh ($200K loss) | LOW |
| Contract | N/A | LOW |
| Switching barriers | None — nothing to switch from | LOW |
| Incumbent champion | None (no incumbent) | LOW |
| Incumbent advantage | "Free" / "we've never needed it" | MEDIUM |

**Overall: LOW threat.** Pain is fresh and quantifiable. Main risk: budget (no existing line item) and organizational inertia ("we've survived this long").

**Step 3 — Positioning:**
Gap matrix replaced with **Risk Exposure Assessment**:

| Dimension | Requirement | Deadline | Account Exposure | Current Protection |
|-----------|-------------|----------|-----------------|-------------------|
| [Region A] | Yes | [Timeframe] | $4.2M annual exposure [Estimated] | None |
| [Region B] | Yes | [Timeframe] | $3.1M [Estimated] | None |
| [Region C] | Yes | [Timeframe] | $2.8M [Estimated] | None |
| [Region D] | Yes | [Timeframe] | $1.5M [Estimated] | None |
| **Total estimated exposure** | — | — | **$11.6M+ unprotected** | **None** |

This becomes the primary selling tool: "You have $11.6M in unprotected exposure across 4 dimensions. The $200K loss was the first one you caught — how many others are you absorbing without knowing it?"

**Step 4a — Discovery Questions:**
1. "When was the last time you had difficulty with a situation where you hadn't taken protective action?" → They already answered this ($200K loss). Use to probe deeper: "Was that the only one, or just the biggest one you noticed?"
2. "What percentage of your exposure is in areas that require protective action?" → Quantifies exposure. Most companies underestimate.
3. "How do you decide which engagements are worth protecting?" → Surfaces the decision framework (or lack thereof). The answer is usually "we don't — we just hope things work out."

**Step 5 — Win Plan:**
1. Quantify total exposure using their own data (ask for dimension-by-dimension breakdown)
2. Share industry data on relevant trends and risks
3. Show specific requirements for their key dimensions
4. Demonstrate platform with their specific profile
5. Position budget conversation: "This is risk insurance, not a new expense. Compare to the $200K you already lost."

**Risk Assessment:** Budget. There is no existing line item for this type of software. The CFO must create a new budget category. The $200K loss is the strongest argument for justification — frame the platform cost as a fraction of one loss event.

**Output:** Full battlecard, LOW threat (green accent). Win strategy: Educational selling — help them discover the size of the risk they've been absorbing. The $200K loss is the opening; the $11.6M exposure assessment is the closer.

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
**Action:** Identify the blocker's concerns (job security, familiarity, political capital invested in choosing the current tool). Build positioning that neutralizes without confronting: "The platform doesn't replace your team's expertise — it amplifies it." Consider multi-threading around the blocker to the economic buyer.

---

## Troubleshooting

### "We don't have competitive intelligence for this specific competitor"
**Solution:** Classify the competitor into the closest category from `{Client Profile: Competitive Landscape}`. Use category-level gaps and positioning. Build competitor-specific intelligence from the discovery call by using the general discovery questions. Document what you learn for future deals. Tag all claims as `[Inferred — category-level]`.

### "Prospect is satisfied with incumbent — no dissatisfaction signal"
**Solution:** This is a HIGH threat assessment. Don't try to create dissatisfaction — instead, lead with what's possible that they may not know they're missing. Use the "Many teams tell us..." approach to surface latent pain. Focus on macro trends from `{Client Profile: Competitive Landscape}` that make their current approach increasingly risky over time.

### "Incumbent is a department within the prospect company (internal build)"
**Solution:** Classify as Manual/Spreadsheets but add the "build vs. buy" objection handling: "Core vs. context — is [your domain] where you want to invest IT resources?" Reference proof points about engineering focus ([X]+ engineers on [domain] alone). Acknowledge their internal expertise while positioning the scale and coverage challenge.

### "Multiple competitors in play (bake-off scenario)"
**Solution:** Build strategy against the strongest competitor first. Add a section addressing the secondary competitor. In the win plan, identify which competitor poses the greater threat and allocate positioning energy accordingly. The gap matrix can include multiple columns if helpful.

### "Prospect likes the incumbent but is evaluating out of obligation (procurement requirement)"
**Solution:** This is effectively a HIGH threat — the incumbent is the default winner. Strategy must create genuine preference, not just check-the-box participation. Focus on demonstrating capabilities the prospect didn't know they needed. Use discovery questions to uncover pain they haven't articulated to their current vendor. Win plan should target multi-threading to a stakeholder who isn't invested in the incumbent.

---

## Best Practices

### Do's
- **Respond positively to competitor mentions** — budget is allocated, no new capital outlay needed
- **Lead with enablement, not criticism** — "Here's what's possible" beats "Here's what's broken"
- **Use competitor-specific discovery questions** — genuine curiosity exposes gaps better than accusations
- **Include an honest risk assessment** — where could the competitor win? Addressing this shows credibility.
- **Match proof points to the competitive scenario** — displacement stories for displacement deals, not generic
- **Prepare for positioning landmines** — knowing where the conversation could go badly is more valuable than perfect positioning
- **Grade your evidence** — tag competitive claims per Epistemic Rules to calibrate confidence

### Don'ts
- **Don't trash the competition** — it implies parity ("we are peerless in this space")
- **Don't tell the prospect what pain they have** — let them articulate it through discovery questions
- **Don't use generic feature matrices** — every capability row must connect to this specific account's situation
- **Don't ignore inertia** — even when competing against a named vendor, the real battle is against the comfort of the status quo
- **Don't assume the prospect's dissatisfaction** — let discovery questions surface it naturally
- **Don't skip the win plan** — a battlecard without action steps is a document, not a strategy

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

- **`gtm-competitive-displacement`** — For prospecting outbound sequences against a known incumbent. Complementary: competitive strategy is for active deals (AE), displacement is for pipeline generation (BDR/AE).
- **`gtm-meeting-prep`** — Run competitive strategy first, then meeting prep to incorporate competitive positioning into discovery or demo structure.
- **`gtm-stakeholder-mapping`** — Org map reveals who might be an incumbent champion (Blocker role). Feed this into the competitive strategy.
- **`gtm-deal-pulse`** — Competitive strategy informs the "Why Us" pillar of deal health scoring.
- **`gtm-call-coaching`** — After competitive conversations, run call coaching to assess how well the rep executed the competitive strategy.
- **`gtm-research-outbound`** — For public companies, financial intelligence can reveal competitive pressure points (e.g., earnings miss making cost optimization urgent).

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (Epistemic Rules, Competitive Threat Assessment Calibration) moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release — migrated from competitive strategy builder
- Generalized via Client Profile block with configurable defaults
- Preserved all competitor intelligence structure: 7 categories, failure patterns, gaps, educational positioning
- Preserved competitive philosophy ("never trash," "#1 competitor is inertia")
- Preserved Winning Zone alignment, differentiation matrix, win plan checklist
- Preserved field-tested objection handling (universal + competitor-specific)
- Multi-format artifact generation replacing reportlab-only
