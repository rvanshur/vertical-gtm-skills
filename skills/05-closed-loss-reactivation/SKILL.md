---
name: gtm-closed-loss-reactivation
description: "Re-engages closed-lost accounts using CRM intelligence. Classifies loss reason (7 categories), assesses what's changed since deal died, re-qualifies ICP fit, selects loss-reason-specific reactivation strategy, and generates 4-step sequences with history-aware openers and call prep"
version: 1.0.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-03-04
tags: [closed-loss, reactivation, win-back, lost-deal, re-engagement, deal-recovery]
requires:
  skills: []
---

# Closed-Loss Reactivation Outbound

## Overview

Re-engages closed-lost accounts using existing CRM intelligence. Classifies the loss reason into 7 categories, assesses what's changed since the deal died (account changes, product updates, market shifts), re-qualifies ICP fit, selects a loss-reason-specific reactivation strategy, and generates 4-step sequences with history-aware openers and reactivation call prep. Distinct from cold outbound — leverages existing relationships and deal context.

**Core Principle:** This is NOT cold outreach. BDRs approaching a closed-loss account have an advantage — existing intelligence and often existing relationships. This skill weaponizes that history rather than ignoring it. Never pretend the prior deal didn't exist.

---

## Client Profile

> **Configure this block for your company.** Replace the placeholder values below with your actual company data, ICP definitions, personas, and competitive landscape.

### Company
- **Name:** [Your Company]
- **Industry:** [Your vertical] (B2B SaaS)
- **Product:** [One-line product description]

### ICP Definitions

**ICP1: [Primary Segment Name] (Core)**
- [Description of ideal customer segment]
- Enterprise ($500M+) and Mid-Market ($100-500M) preferred; minimum viable at $50M+

**ICP2: [Expansion Segment Name]**
- [Description of secondary segment]
- Revenue threshold: [Minimum viable size]
- [Priority qualifier, e.g., PE-backed is highest priority]

### Loss Reason Taxonomy

| # | Loss Reason | CRM Signals | Typical Pattern |
|---|-----------|------------|----------------|
| 1 | **Lost to competitor** | Mentions competitor name | Deal progressed through demo, prospect chose alternative |
| 2 | **No decision / went dark** | No response after a certain stage | Deal stalled mid-funnel, prospect stopped engaging |
| 3 | **Budget / timing** | Mentions budget, fiscal year, "not now" | Prospect liked product but couldn't fund it |
| 4 | **Not a fit** | Mentions fit, requirements, scope | Product didn't meet a specific requirement |
| 5 | **Champion left** | Primary contact no longer at company | Deal died because internal advocate departed |
| 6 | **Internal solution chosen** | "Building internally" or "keeping current" | Prospect invested in own process instead |
| 7 | **Price / negotiation failure** | Mentions price, cost, ROI, terms | Couldn't agree on pricing or contract structure |

### Reactivation Strategies by Loss Reason

**1. Lost to Competitor → Buyer's Remorse Play**
- **Timing:** 6-12 months (let them experience limitations)
- **Angle:** Don't bash competitor. Ask how it's going. Surface pain naturally.
- **Opener:** "When we last spoke, you went with [competitor]. Curious how that's been working out — specifically around [area of strength]."

**2. No Decision / Went Dark → Re-Engage with New Value**
- **Timing:** 3-6 months (respect silence, then bring something new)
- **Angle:** Don't reference the ghosting. Lead with new information.
- **Opener:** "I know we connected a while back. Not reaching out to rehash that — wanted to share something relevant about [new development]."

**3. Budget / Timing → Circle Back at the Right Moment**
- **Timing:** Align with fiscal year or specific timeline they mentioned
- **Angle:** Reference their own words about timing.
- **Opener:** "When we spoke in [month], you mentioned [timing signal]. Wanted to check whether that window has opened up."

**4. Not a Fit → Re-Qualify with New Evidence**
- **Timing:** Only if something materially changed (new capabilities, expanded scope)
- **Angle:** Acknowledge the original gap. Show what's different.
- **Opener:** "When we last evaluated together, [specific gap] was the sticking point. Wanted to let you know that's changed."

**5. Champion Left → Follow the Champion or Find the Replacement**
- **Timing:** Immediately on discovery
- **Track A — Follow champion:** Warm lead at their new company
- **Track B — Find replacement:** New person inherits same pain
- **Opener A:** "Congrats on the new role. Imagine you're dealing with similar challenges there."
- **Opener B:** "[Champion name] and I were working on [pain area]. Not sure where that landed."

**6. Internal Solution → Wait for the Cracks**
- **Timing:** 12-18 months (internal solutions take time to fail)
- **Angle:** Ask questions that surface limitations, don't declare failure.
- **Opener:** "Your team was building an internal process. Curious how that's scaled — most teams find it works until [complexity trigger]."

**7. Price / Negotiation → Return with New Proof**
- **Timing:** 3-6 months (enough time for ROI evidence to emerge)
- **Angle:** Lead with new ROI data, not "we lowered our price."
- **Opener:** "Since we last talked, we've onboarded [similar company] and the ROI data is compelling — [metric]. Wanted to share."

### Competitive Landscape (for Buyer's Remorse scenarios)
| If They Chose | Likely Pain After 6-12 Months | Best Proof Point |
|--------------|------------------------------|-----------------|
| [Competitor 1] | [Common pain with that competitor] | [Customer]: [Displacement metric] |
| [Competitor 2] | [Common pain with that competitor] | [Customer]: [Displacement metric] |
| [Competitor 3] | [Common pain with that competitor] | [Customer]: [Displacement metric] |
| Status Quo / Manual | Scaling breaks, key-person risk, missed deadlines | [Customer]: [Improvement metric] |

### Product Changes to Reference
| Change | Reactivation Angle |
|--------|-------------------|
| New customer wins in their vertical | Social proof they didn't have before |
| New displacement proof points | Evidence of competitors failing |
| Product updates (new features) | Features they asked for that now exist |
| New integrations | Technical fit may have improved |
| Industry awards/recognition | Credibility builder |

### Industry Macro Trends
- [Macro trend 1]
- [Macro trend 2]
- [Macro trend 3]
- [Macro trend 4]

---

## Quick Reference

**Use this skill when:**
- Re-engaging an account that closed-lost in the last 3-18 months
- Deciding whether a closed-lost account is worth re-approaching
- A trigger event occurs at a former prospect (new leadership, acquisition, competitor pain)
- Building a reactivation campaign across multiple closed-lost accounts

**Don't use when:**
- The account is net-new (use `gtm-account-snapshot` or `gtm-research-outbound`)
- The account is an active deal (use `gtm-deal-pulse`)
- A trigger event is the primary angle (use `gtm-trigger-event-outbound` first, reference loss history as context)

**User roles:** BDR, AE
**Expected time:** 15-25 minutes per account

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

**BDR Coordination Rule:** Always surface the original AE who owned the closed-lost deal. BDRs must coordinate with the original AE before re-engaging — the AE may have context about why re-engagement is or isn't appropriate.

---

### Step 1: Pull Closed-Lost Deal History

Query CRM for the specified account's closed-lost opportunity. Extract:

**Deal basics:**
- Account name, industry, sub-industry
- Original opportunity value (ARR)
- Stage the deal died at
- Close date and days since close
- AE who owned the deal, BDR who sourced it
- Deal origin (inbound, outbound, referral, event)

**Loss context:**
- Closed-lost reason (if logged)
- Loss notes from AE
- Last activity before deal died
- Whether demo was delivered, pricing shared, proposal sent

**Contact history:**
- All contacts engaged during the deal
- Champion and economic buyer (if identified)
- Meeting history with dates, types, participants, key learnings
- Last conversation topics and outcome

**Prior intelligence:**
- Pain points identified during discovery
- Current-state process described by prospect
- Competitors or incumbent tools mentioned
- Objections raised (resolved or not)
- Budget or timeline signals, decision criteria

---

### Step 2: Classify Loss Reason

Categorize using `{Client Profile: Loss Reason Taxonomy}`. Use CRM loss reason if logged; otherwise infer from deal history and engagement patterns.

**Inference signals:**
- Last stage + last activity type + time between activities
- If died at Discovery → likely No Decision or Not a Fit
- If died at Negotiation → likely Price, Budget, or Lost to Competitor
- If last 3+ touchpoints unanswered → likely No Decision / Went Dark

**Output:** `loss_classification` — Category, confidence level (High/Medium/Low), supporting evidence

---

### Step 3: Assess What's Changed

Search for changes since the deal closed that create a new opening.

#### Changes at the Account
- New funding, M&A, or PE acquisition
- Geographic expansion into new regions
- Revenue growth or contraction
- New leadership (relevant executive roles)
- New job postings suggesting hiring or tech changes
- Champion movement (left company? promoted? where did they go?)
- New contacts in relevant roles

#### Changes at Your Company
Use `{Client Profile: Product Changes to Reference}` — new customer wins in their vertical, new features, new integrations, displacement proof points.

#### Changes in the Market
Use `{Client Profile: Industry Macro Trends}` — flag trends that have intensified since the deal closed.

**Output:** `change_assessment` — Categorized changes with reactivation relevance

---

### Step 4: Re-Qualify ICP Fit

Re-score against `{Client Profile: ICP Definitions}`. The company may have changed since original evaluation.

**Re-qualification verdict:**
- **REACTIVATE** — ICP fit is strong AND meaningful changes have occurred
- **MONITOR** — ICP fit is decent but no compelling change event yet. Set reminder for 60-90 days.
- **RETIRE** — ICP fit was weak then and hasn't improved. Don't waste cycles.

---

### Step 5: Select Reactivation Strategy

Based on loss classification and change assessment, select the approach from `{Client Profile: Reactivation Strategies by Loss Reason}`. Each strategy specifies timing assessment, angle, opener, and key intelligence needs.

**Output:** `reactivation_strategy` — Approach, timing assessment (too soon / right time / overdue), entry angle

---

### Step 6: Generate Reactivation Sequences

Produce a **4-step email sequence** for top 2-3 personas. Reactivation differs from cold outbound:
1. **Acknowledge the history** — never pretend prior deal didn't happen
2. **Lead with what's changed** — new information justifies re-approach
3. **Lower the ask** — aim for conversation, not demo

#### Rules for Reactivation Emails
- Include a **subject line** (never "Following up" or "Checking in")
- Body **<= 120 words**
- **Email 1 must reference the prior relationship** with specific context
- Use the contact's name (known from CRM)
- Each step uses a different angle from the reactivation strategy
- **Never bash their current solution or decision**
- Tone: peer-to-peer, not salesperson-to-prospect

#### Sequence Structure (Per Persona)
| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1: Re-Opener** | Prior relationship + what's changed | Re-establish relevance without being pushy |
| **Email 2: New Evidence** | Proof point, customer win, or trend | Build credibility with new information |
| **Email 3: Peer Comparison** | Similar company that made the same decision | Social proof matching their loss scenario |
| **Email 4: Direct Ask** | Transparent, low-pressure ask | "I think there's a conversation worth having. If not, no hard feelings." |

#### Proof Point Matching
Use `{Client Profile: Competitive Landscape}` to match proof points to the specific loss scenario:

| Loss Scenario | Best Proof Point | Why It Works |
|--------------|-----------------|-------------|
| Lost to competitor | Customer who displaced that competitor | Prospect sees own decision reflected |
| No decision (inertia) | Customer showing cost of waiting | Quantifies delay cost |
| Internal solution | Customer who outgrew internal process | Shows where internal breaks |
| Budget/pricing | Customer with compelling ROI | Reframes value equation |

---

### Step 7: Build Reactivation Call Prep

#### Reactivation Opener (30 seconds)
**Structure: Acknowledge → Reference → Bridge** (NOT the standard cold call opener)

1. **Acknowledge:** "Hey [Name], it's [Rep] from [Company]. We connected back in [month/year]."
2. **Reference:** One specific thing from prior deal — pain shared, meeting attended, topic discussed.
3. **Bridge:** What's changed. "Reaching out because [specific development] — thought it might be worth a quick conversation."

#### Talk Track
| Step | Script Element |
|------|---------------|
| Validate current state | "Last I knew, you were [using competitor / handling internally / holding off]. How's that been going?" |
| Surface new pain | "Companies in your position find that [loss-reason-specific pain] tends to show up after [timeframe]." |
| Introduce new evidence | "Since we last talked, we've brought on [similar company] and results have been [metric]." |
| Low-pressure ask | "Worth 15 minutes to compare notes? Not a full evaluation — just a conversation about what's changed." |

#### Loss-Reason-Specific Pain Questions
Map to `{Client Profile: Loss Reason Taxonomy}` — each loss type has specific pain surfacing questions.

#### Voicemail Script (<30 seconds)
- Name + company + "we spoke back in [month]"
- One specific reason for calling (what's changed)
- CTA: "I'll send a quick email with details"

#### Objection Handling (Reactivation-Specific)
| Objection | Rebuttal |
|-----------|----------|
| "We already went through this" | "Not looking to restart a full evaluation. A few things have changed on our side worth sharing — can I send a 2-minute read?" |
| "We're happy with [competitor]" | "Great. Out of curiosity, how's [area of strength] working? That's where most companies like [proof point] found the biggest gap." |
| "Nothing has changed" | "On our end, we've brought on [similar company] and results have been [metric]. If ever relevant, I'd love to reconnect." |
| "We built our own solution" | "Smart move. Teams who've done that usually hit a ceiling around [complexity point]. If you get there, I'd love to compare notes." |
| "Don't have budget" | "Makes sense. Mind if I send a quick case study from [similar company]? Might be useful even if timing isn't right today." |
| "I'm not the right person anymore" | "No problem. Who should I be talking to about [relevant area] now?" |

---

### Step 8: Deliver Analysis

Present complete reactivation analysis:

1. **Deal History Summary** — Account, original value, stage lost, days since close, AE, champion status
2. **Loss Classification** — Category, confidence, evidence
3. **What's Changed** — Account, product, and market changes
4. **Re-Qualification Verdict** — REACTIVATE / MONITOR / RETIRE with reasoning
5. **Reactivation Strategy** — Approach, timing assessment, entry angle
6. **Reactivation Sequences** — Full email sequences per persona
7. **Call Prep** — Opener, talk track, voicemail, objection handling
8. **User Role**: BDR / AE
9. **Coordination Guidance** (BDR): "Coordinate with [original AE] before sending reactivation outreach"
10. **Recommended First Action** — Specific next step with persona and angle

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_Reactivation.md`
- **Option B: HTML** — Styled cheatsheet with loss reason badge and deal history banner
- **Option C: PDF** — Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)
1. **Deal History Banner** — Account, original ARR, stage lost, days since close, loss reason badge, verdict
2. **What's Changed** — Two-column: account changes (left), product changes (right)
3. **Reactivation Strategy** — Approach, entry angle, timing assessment
4. **Key Personas** — Original contacts + new contacts, with engagement history and priority
5. **Reactivation Hooks** — 3-4 loss-reason-specific talk-track-ready hooks
6. **Discovery Questions** — 4-5 history-aware questions (open → probe → confirm)
7. **Objection Handling** — Top 4 objections matched to loss scenario
8. **Call Flow** — Reactivation-specific: Acknowledge → Reference → Bridge → Validate → Ask

Color-code by reactivation urgency. Include **LOSS REASON BADGE** in header.

---

## Examples

### Example 1: Buyer's Remorse — Lost to Competitor

**Context:** Account chose [Competitor] 8 months ago. Competitor quality has continued declining.

**Input:** "Should we try to win back [Target Company]? They chose [Competitor]."

**Process:** CRM pull: closed-lost $45K, chose [Competitor] at Negotiation stage, AE was [Name]. Champion: VP [Function], still at company. Loss classification: Lost to Competitor (High confidence). What's changed: [Competitor] support continues declining, you've displaced 3 more [Competitor] accounts since this deal closed. Verdict: REACTIVATE.

**Output:** Buyer's Remorse strategy, 2 persona sequences (VP [Function] + [Operations Manager], 8 emails), reactivation call prep, cheatsheet. Entry angle: "How has [Competitor] been handling [key capability] at scale?"

### Example 2: Budget Hold — Timing Play

**Context:** Account liked the product but couldn't fund it. Mentioned revisiting in Q3.

**Input:** "Build reactivation for [Target Company] — closed-lost due to budget in January."

**Process:** Loss classification: Budget/Timing (High confidence — AE notes say "revisit Q3"). What's changed: New PE investment announced in February (potential budget unlock). Days since close: 60. Timing assessment: slightly early but PE investment creates opening. Verdict: REACTIVATE.

**Output:** Circle Back strategy leveraging PE investment as budget unlock signal. Entry: "When we spoke in January, budget was the blocker. Noticed the [PE Firm] announcement — does that change the picture?"

### Example 3: Champion Left — Follow the Champion

**Context:** Champion left the company and joined another company in ICP.

**Input:** "Our champion at [Company A] left. They went to [Company B]. What do we do?"

**Process:** Two-track approach. Track A: Champion at [Company B] (ICP2 GREENLIGHT). Track B: Replacement at [Company A] (unknown — need to identify). Verdict: REACTIVATE both tracks.

**Output:** Track A sequence targeting champion at [Company B] (warm lead), Track B sequence for [Company A] replacement. Two cheatsheets. Champion follow has highest priority.

---

## Common Patterns

### Pattern: Batch Reactivation Campaign
**When:** User provides a list of 5-20 closed-lost accounts.
**Approach:** Run abbreviated reactivation (Steps 1-4 only) for each. Produce a ranked table: REACTIVATE / MONITOR / RETIRE with reasoning. Full sequences for top REACTIVATE accounts only.

### Pattern: BDR Coordination
**When:** `user_role = BDR` on any closed-loss account.
**Action:** Always surface the original AE. Include coordination guidance: "Coordinate with [AE name] before sending reactivation outreach." The AE may have context about why re-engagement is or isn't appropriate.

### Pattern: Champion Follow
**When:** The loss reason was "Champion Left" and the champion moved to another company in ICP.
**Action:** Run two parallel tracks: Track A (follow champion to new company), Track B (find replacement at original account). Prioritize Track A — the champion already knows your product's value.

---

## Troubleshooting

### "No loss reason recorded in CRM"
**Solution:** Infer from behavioral signals. Last stage reached + last activity type + time between activities. If died at Discovery with multiple unanswered follow-ups = "Went Dark." If died at Negotiation = likely Price or Budget. State confidence level and cite evidence.

### "Deal closed more than 18 months ago"
**Solution:** The account may have changed significantly. Run a fresh ICP re-qualification (Step 4) before proceeding. If no meaningful changes, classify as MONITOR or RETIRE rather than forcing a stale reactivation.

### "Multiple loss reasons apply"
**Solution:** Classify by the primary reason (the one that ultimately killed the deal). Note secondary factors as context. Build sequences around the primary but reference secondary in discovery questions.

### "Champion moved to a non-ICP company"
**Solution:** Track A is not viable. Focus entirely on Track B (find replacement at original account). Note the champion's new company in case ICP classification changes in the future.

---

## Best Practices

### Do's
- **Acknowledge the history** — Email 1 must reference the prior relationship with specific context
- **Lead with what's changed** — new information justifies the re-approach; without it, you're just pestering
- **Lower the ask** — "conversation about what's changed" not "let's restart the evaluation"
- **Match proof points to loss scenario** — competitor loss → competitor displacement proof point
- **Coordinate BDRs with original AEs** — the AE has context the BDR doesn't

### Don'ts
- **Don't pretend the deal never happened** — "We haven't spoken in a while" is not a reason to call
- **Don't bash their decision** — they chose what they chose; respect it
- **Don't reactivate accounts that were genuinely a poor fit** — unless something has materially changed
- **Don't use "Following up" as a subject line** — ever
- **Don't use the cold call opener** — use the reactivation Acknowledge → Reference → Bridge opener

### Quality Checklist
- [ ] Deal history fully pulled from CRM
- [ ] Loss reason classified with confidence level and evidence
- [ ] Change assessment covers at least 2 of 3 dimensions (account, product, market)
- [ ] ICP re-scored with comparison to original
- [ ] Strategy matches loss reason (not generic)
- [ ] Email 1 references prior relationship with specific context
- [ ] No competitor bashing
- [ ] Proof points match loss scenario
- [ ] Call prep uses reactivation framework (Acknowledge → Reference → Bridge)
- [ ] BDR coordination guidance included
- [ ] No placeholder brackets in final output

---

## Integration with Other Skills

- **`gtm-competitive-displacement`** — When loss reason is "Lost to Competitor" and reactivation verdict is REACTIVATE, combine with displacement intelligence.
- **`gtm-trigger-event-outbound`** — When a trigger event occurs at a closed-lost account, use trigger event skill for timeliness, reference loss history as context.
- **`gtm-account-qualification`** — For Step 4 re-qualification, can use the full qualification framework for deeper ICP scoring.
- **`gtm-deal-pulse`** — Once reactivation creates a new pipeline opportunity, switch to deal health monitoring.
- **`gtm-meddpicc-analysis`** — Use the prior deal's MEDDPICC gaps to inform the reactivation strategy.

---

## Changelog

### Version 1.0.0 (2026-03-04)
- Initial release
- Generalized via Client Profile block with placeholder defaults
- Preserved 7-category loss taxonomy, what's-changed assessment, re-qualification framework (REACTIVATE/MONITOR/RETIRE)
- Preserved all 7 loss-reason-specific strategies with openers, timing, and angles
- Maintained BDR coordination pattern and reactivation-specific call prep framework
- Multi-format artifact generation
