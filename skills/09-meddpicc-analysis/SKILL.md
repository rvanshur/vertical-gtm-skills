---
name: gtm-meddpicc-analysis
description: "Scores active deals across all 8 MEDDPICC elements using evidence-graded rubrics, computes weighted health, flags risk patterns, and generates coaching"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [meddpicc, deal-analysis, deal-scoring, pipeline-review, sales-methodology, deal-qualification]
requires:
  skills: ["gtm-deal-pulse"]
---

# MEDDPICC Deal Analysis

## Overview

Scores an active deal across all 8 MEDDPICC elements using evidence-graded rubrics from CRM data — not rep self-assessment. Maps pain to the client's buyer pain taxonomy, competition to verified competitive intel, and champion strength to the client's methodology. Computes a weighted health score (0-100), flags risk patterns (happy ears, single-threaded, zombie deals), and generates coaching tied to sales frameworks.

**Core Principle:** Evidence over optimism — score what CRM data proves, not what reps believe. Under-scoring protects deals; over-scoring kills them.

---

## Role

You are a **senior sales manager and deal analyst for a vertical SaaS company** — not a generic assistant. You score individual deals with evidence-grounded discipline, identifying gaps early and recommending methodology-aligned coaching. Everything company-specific — the pain taxonomy, the buyer personas, the competitive landscape — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | Account with active opportunity |
| Opportunity amount (ARR or total contract value) | ✅ Required | For health benchmarking |
| Deal stage | ✅ Required | Used to set stage-appropriate thresholds |
| CRM access (interaction history, contact data, notes) | ✅ Required | Evidence for element scoring |
| Contact names and titles | Optional | For Economic Buyer and Champion identification |

---

## Output Contract

Every run produces a **MEDDPICC health assessment with the same structure** — so deal quality can be compared across pipeline. The content changes per deal; the structure never does.

Core commitments: **8-element scorecard with weighted scores**, **overall health score (0-100)**, **stage-appropriate verdict**, **stakeholder map**, **top 3 risks**, and **5 prioritized next actions**.

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Core Pain Points | Identified Pain element scoring |
| Value Propositions | Metrics and product alignment assessment |
| Competitive Landscape | Competition element scoring, incumbent identification |
| Buyer Personas | Economic Buyer and Champion role identification |
| Qualification Criteria | Decision criteria and winning zone assessment |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your playbook for MEDDPICC scoring. The 8 elements, weighting system, 1-5 scoring rubrics, health calculation, stage minimums, risk patterns, and coaching framework are your operational blueprint.

### The Eight MEDDPICC Elements and Weights

| Element | Weight | What It Measures |
|---------|--------|-----------------|
| **M — Metrics** | 15% | Are success metrics defined and aligned? |
| **E — Economic Buyer** | 20% | Is the budget owner identified and engaged? |
| **D — Decision Criteria** | 10% | Do we know the evaluation criteria? |
| **D — Decision Process** | 10% | Do we understand the buying process and committee? |
| **P — Paper Process** | 10% | Are legal, security, and procurement mapped? |
| **I — Identified Pain** | 15% | Is business pain confirmed and quantified? |
| **C — Champion** | 15% | Is there an active internal advocate? |
| **C — Competition** | 5% | Do we understand the competitive landscape? |

### MEDDPICC Scoring Rubrics (1-5 Scale)

#### M — Metrics (Weight: 15%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Success metrics defined, baseline measured, target improvements quantified, ROI agreed with economic buyer. |
| 4 | Metrics discussed, prospect shared current-state numbers. ROI framework shared but not formally agreed. |
| 3 | General pain quantified but no specific baselines or targets established. |
| 2 | Pain acknowledged but not quantified. No numbers shared. |
| 1 | No metrics discussion has occurred. |

#### E — Economic Buyer (Weight: 20%)
| Score | Evidence Required |
|-------|------------------|
| 5 | EB identified by name/title, attended meeting, confirmed budget, expressed personal investment. |
| 4 | EB identified, direct access established, budget discussed but not confirmed. |
| 3 | EB identified by name but no direct access. Communicating through champion only. |
| 2 | We think we know the EB based on title/org chart but haven't confirmed. |
| 1 | Economic buyer not identified. |

#### D — Decision Criteria (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Written evaluation criteria received. We map favorably to all critical criteria. We've influenced criteria toward our winning zones. |
| 4 | Criteria discussed verbally. Know must-haves vs. nice-to-haves. Strong on most. |
| 3 | Some criteria known from discovery. Haven't mapped to capabilities formally. |
| 2 | Vague sense of what matters. No specific requirements documented. |
| 1 | No discussion of evaluation criteria. |

#### D — Decision Process (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Full process mapped: steps, committee members by name, timeline with dates, approval sequence confirmed. |
| 4 | Process mostly understood. Key steps and stakeholders known, some dates fuzzy. |
| 3 | General process known. Specific stakeholders and dates not confirmed. |
| 2 | Champion said "I'll handle it internally" without specifics. |
| 1 | No discussion of decision process. |

#### P — Paper Process (Weight: 10%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Legal requirements known, procurement mapped, contract terms discussed, signature authority confirmed. |
| 4 | Most paper process understood. MSA structure known. Legal review expected, timeline estimated. |
| 3 | Aware legal/procurement review exists but details unclear. |
| 2 | Paper process assumed based on company size, not confirmed. |
| 1 | No discussion of paper process. |

#### I — Identified Pain (Weight: 15%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Multiple pains across stakeholders, quantified impact in prospect's words, urgent timeline, maps to winning zones. |
| 4 | Primary pain clearly articulated with some quantification. Urgency present but not deadline-driven. |
| 3 | Pain acknowledged but generic. Not quantified. No expressed urgency. |
| 2 | We think there's pain based on profile, but prospect hasn't confirmed. |
| 1 | No pain identified. Deal is feature-led or relationship-led. |

#### C — Champion (Weight: 15%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Champion identified, has influence, actively selling internally, sharing insider info, giving political guidance. |
| 4 | Identified and engaged, shows investment, has introduced stakeholders. Not yet demonstrated active internal selling. |
| 3 | Strong contact who likes us but may lack influence or willingness to advocate. |
| 2 | Contact engages in meetings but shows no championing signs. Evaluating, not advocating. |
| 1 | No champion identified. Engaging with someone who can't influence the decision. |

#### C — Competition (Weight: 5%)
| Score | Evidence Required |
|-------|------------------|
| 5 | Competitive landscape fully understood. Incumbent known, differentiated strategy confirmed, criteria favor our winning zones. |
| 4 | Competition identified, strategy exists, prospect perception not yet confirmed. |
| 3 | Competitor or alternative known but no specific strategy. |
| 2 | Competition suspected but not confirmed. |
| 1 | No competitive intelligence. |

### Health Score Calculation & Interpretation

**Formula:** For each element, multiply its score (1-5) by its weight (%). Sum all weighted scores, then divide by 5 and multiply by 100.

| Health Score | Health | Meaning |
|-------|--------|---------|
| 80-100 | 🟢 Green | Strong. Well-qualified, progressing. Focus on execution. |
| 60-79 | 🟡 Yellow | Moderate risk. Key gaps addressable. Fill gaps before advancing. |
| 40-59 | 🟠 Orange | High risk. Multiple weak elements. Consider re-qualifying. |
| 0-39 | 🔴 Red | Critical. Lacks fundamentals. Downgrade or disqualify. |

### Stage-Appropriate Minimums

| Stage | Min Health | Critical Elements ≥3 |
|-------|-----------|----------------------|
| Discovery | 30+ | Identified Pain |
| Trial & Evaluation | 50+ | Identified Pain, Champion, Decision Criteria |
| Negotiation | 65+ | All except Competition ≥3, EB ≥4 |
| Closing | 75+ | All ≥3, EB ≥4, Paper ≥4 |

### Risk Patterns to Flag

| Pattern | Evidence | Action |
|---------|----------|--------|
| Happy ears | High confidence, low CRM evidence | Manager should join next call |
| Single-threaded | Only one contact, no multi-stakeholder meetings | Multi-thread immediately |
| Zombie deal | Same stage >45 days, no recent activity | Re-engage or downgrade |
| Close date fantasy | 2+ slips, or close <30 days with Paper ≤2 | Reset close date (+30 days minimum) |
| Feature-led deal | No documented pain, demo notes focus on features shown | Go back to discovery |
| Competitor blind | No competitive intel past Discovery | Ask directly about alternatives |

---

## Quick Reference

**Use this skill when:**
- Deep-diving a specific deal's qualification gaps
- Preparing coaching recommendations for a rep's deal
- Deciding whether to advance, hold, or downgrade a deal stage
- Running pipeline reviews with weighted health scoring

**Don't use when:**
- You need a quick health check (use `gtm-deal-pulse`)
- The account has no active opportunity (use `gtm-account-qualification`)
- You need meeting-specific coaching (use `gtm-call-coaching`)

**User roles:** AE, Sales Manager, VP Sales

**Expected time:** 20-30 minutes per deal

---

## Epistemic Rules

- **Only score what is evidenced in CRM data.** No evidence = low score. Do not inflate.
- **Label evidence:** `[CRM]`, `[Call Transcript]`, `[Rep Notes]`, `[Inferred]`, `[Unknown]`
- **Distinguish confirmed from claimed:** A champion the rep *claims* is selling internally differs from one with visible internal activity.

---

## Core Workflow

### Step 1: Pull Deal Data from CRM

Query available CRM/data sources for the account. Extract:

**Deal basics:** Account name, industry, opportunity value (ARR), deal type, current stage, days in stage, expected close date (and slip history), deal owner, supporting team, deal origin (inbound/outbound/referral/event).

**Engagement history:** Total touchpoints, last activity date/type, sequence history, meeting history with dates/types/participants/duration.

**Contact records:** All contacts on the opportunity — name, title, department, seniority, engagement level per contact, meeting attendance vs. email-only.

**Deal notes:** AE/BDR notes, next steps from most recent meeting, objections raised, competitors mentioned, budget/timeline signals.

**Prior opportunities:** Previous closed-lost at this account, reason lost, time elapsed.

**Output artifact:** `deal_profile`

---

### Step 2: Score All 8 MEDDPICC Elements

Score each element 1-5 based on evidence criteria. Be honest.

#### M — Metrics (Weight: 15%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Success metrics defined, baseline measured, target improvements quantified, ROI agreed with economic buyer. |
| 4 | Metrics discussed, prospect shared current-state numbers. ROI framework shared but not formally agreed. |
| 3 | General pain quantified but no specific baselines or targets established. |
| 2 | Pain acknowledged but not quantified. No numbers shared. |
| 1 | No metrics discussion has occurred. |

**Client context:** Look for metrics matching `{Client Profile: Value Propositions}` — time savings, cost reduction, efficiency gains, compliance rates, volume metrics.

**Coaching:** If below 3, the AE likely skipped quantification. Run discovery methodology to quantify business impact.

#### E — Economic Buyer (Weight: 20%)

| Score | Evidence Required |
|-------|------------------|
| 5 | EB identified by name/title, attended meeting, confirmed budget, expressed personal investment. |
| 4 | EB identified, direct access established, budget discussed but not confirmed. |
| 3 | EB identified by name but no direct access. Communicating through champion only. |
| 2 | We think we know the EB based on title/org chart but haven't confirmed. |
| 1 | Economic buyer not identified. |

**Client context:** economic-buyer patterns from `{Client Profile: Buyer Personas}` (the persona that owns budget).

**Coaching:** If below 3, ask champion: "If you decided this was the right move, could you make it happen — or does someone else need to approve?"

#### D — Decision Criteria (Weight: 10%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Written evaluation criteria received. We map favorably to all critical criteria. We've influenced criteria toward our winning zones. |
| 4 | Criteria discussed verbally. Know must-haves vs. nice-to-haves. Strong on most. |
| 3 | Some criteria known from discovery. Haven't mapped to capabilities formally. |
| 2 | Vague sense of what matters. No specific requirements documented. |
| 1 | No discussion of evaluation criteria. |

**Client context:** Push toward `{Client Profile: Qualification Criteria}`. Redirect away from areas where competitors are stronger.

#### D — Decision Process (Weight: 10%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Full process mapped: steps, committee members by name, timeline with dates, approval sequence confirmed. |
| 4 | Process mostly understood. Key steps and stakeholders known, some dates fuzzy. |
| 3 | General process known. Specific stakeholders and dates not confirmed. |
| 2 | Champion said "I'll handle it internally" without specifics. |
| 1 | No discussion of decision process. |

#### P — Paper Process (Weight: 10%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Legal requirements known, procurement mapped, contract terms discussed, signature authority confirmed. |
| 4 | Most paper process understood. MSA structure known. Legal review expected, timeline estimated. |
| 3 | Aware legal/procurement review exists but details unclear. |
| 2 | Paper process assumed based on company size, not confirmed. |
| 1 | No discussion of paper process. |

**Risk flag:** If close date is <60 days away and Paper Process scores below 3, the close date is almost certainly wrong.

#### I — Identified Pain (Weight: 15%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Multiple pains across stakeholders, quantified impact in prospect's words, urgent timeline, maps to winning zones. |
| 4 | Primary pain clearly articulated with some quantification. Urgency present but not deadline-driven. |
| 3 | Pain acknowledged but generic. Not quantified. No expressed urgency. |
| 2 | We think there's pain based on profile, but prospect hasn't confirmed. |
| 1 | No pain identified. Deal is feature-led or relationship-led. |

**Client context:** Map to `{Client Profile: Core Pain Points}`. A deal without confirmed pain is a deal without a reason to buy.

#### C — Champion (Weight: 15%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Champion identified, has influence, actively selling internally, sharing insider info, giving political guidance. |
| 4 | Identified and engaged, shows investment, has introduced stakeholders. Not yet demonstrated active internal selling. |
| 3 | Strong contact who likes us but may lack influence or willingness to advocate. |
| 2 | Contact engages in meetings but shows no championing signs. Evaluating, not advocating. |
| 1 | No champion identified. Engaging with someone who can't influence the decision. |

**Validation questions:** Has champion given EB access? Shared internal context? Forwarded content? Told us about objections? Helped navigate procurement?

#### C — Competition (Weight: 5%)

| Score | Evidence Required |
|-------|------------------|
| 5 | Competitive landscape fully understood. Incumbent known, differentiated strategy confirmed, criteria favor our winning zones. |
| 4 | Competition identified, strategy exists, prospect perception not yet confirmed. |
| 3 | Competitor or alternative known but no specific strategy. |
| 2 | Competition suspected but not confirmed. |
| 1 | No competitive intelligence. |

**Client context:** Reference `{Client Profile: Competitive Landscape}` for known competitors, weaknesses, and displacement proof points.

**Key insight:** The #1 competitor is always inertia (status quo). Assess urgency to overcome doing nothing.

---

### Step 3: Compute Weighted Deal Health Score

| Element | Weight | Score (1-5) | Weighted |
|---------|--------|-------------|----------|
| Metrics | 15% | [scored] | score × 0.15 |
| Economic Buyer | 20% | [scored] | score × 0.20 |
| Decision Criteria | 10% | [scored] | score × 0.10 |
| Decision Process | 10% | [scored] | score × 0.10 |
| Paper Process | 10% | [scored] | score × 0.10 |
| Identified Pain | 15% | [scored] | score × 0.15 |
| Champion | 15% | [scored] | score × 0.15 |
| Competition | 5% | [scored] | score × 0.05 |
| **TOTAL** | **100%** | | **Sum / 5 × 100** |

**Health interpretation:**
| Score | Health | Meaning |
|-------|--------|---------|
| 80-100 | 🟢 Green | Strong. Well-qualified, progressing. Focus on execution. |
| 60-79 | 🟡 Yellow | Moderate risk. Key gaps addressable. Fill gaps before advancing. |
| 40-59 | 🟠 Orange | High risk. Multiple weak elements. Consider re-qualifying. |
| 0-39 | 🔴 Red | Critical. Lacks fundamentals. Downgrade or disqualify. |

**Stage-appropriate minimums:**
| Stage | Min Health | Critical Elements ≥3 |
|-------|-----------|----------------------|
| Discovery | 30+ | Identified Pain |
| Trial & Evaluation | 50+ | Identified Pain, Champion, Decision Criteria |
| Negotiation | 65+ | All except Competition ≥3, EB ≥4 |
| Closing | 75+ | All ≥3, EB ≥4, Paper ≥4 |

---

### Step 4: Identify Critical Gaps and Risks

**Gap severity ranking:**
1. Any element scoring 1 past Discovery — **critical blocker**
2. EB or Pain ≤2 at any stage — **deal killer if not addressed**
3. Champion ≤2 past Discovery — **no internal advocate, running on hope**
4. Paper Process ≤2 with close <60 days — **close date is wrong**
5. Decision Process ≤2 past Trial & Eval — **being evaluated without knowing rules**

**Risk patterns to flag:**

| Pattern | Evidence | Action |
|---------|----------|--------|
| Happy ears | High confidence, low CRM evidence | Manager should join next call |
| Single-threaded | Only one contact, no multi-stakeholder meetings | Multi-thread immediately |
| Zombie deal | Same stage >45 days, no recent activity | Re-engage or downgrade |
| Close date fantasy | 2+ slips, or close <30 days with Paper ≤2 | Reset close date (+30 days minimum) |
| Feature-led deal | No documented pain, demo notes focus on features shown | Go back to discovery |
| Competitor blind | No competitive intel past Discovery | Ask directly about alternatives |

---

### Step 5: Generate Coaching Recommendations

Generate 5 prioritized next actions, each targeting a specific MEDDPICC gap:

1. **Reference specific methodology** from `{Client Profile: Sales Methodology}` (or your company's sales frameworks if not specified in the profile)
2. **Include success criteria** — how will we know the action was effective?
3. **Assign an owner** — AE, BDR, SE, or manager
4. **Set a deadline** — 5 business days for critical, 10 for moderate

---

### Step 6: Deliver Inline Analysis

**Structure:**
1. **Deal Summary Banner** — Account, amount, stage, days in stage, AE, close date, health score
2. **MEDDPICC Scorecard** — 8 elements with score, key evidence, primary gap
3. **Stakeholder Map** — Name, title, role, influence, engagement, last contact
4. **Gap Analysis — Top 3 Risks** — What, why it matters at this stage, what to do
5. **Coaching — Next 5 Actions** — Action, element targeted, owner, deadline, success criteria
6. **Stage Recommendation** — Advance / Hold / Downgrade / Disqualify with rationale

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[ACCOUNT]_MEDDPICC_Analysis.md`
- **Option B: HTML** — Styled single-page deal health card with inline CSS
- **Option C: PDF** — Python + reportlab

### Document Sections (Deal Health Card)
1. **Deal Banner** — Account, amount, stage, health score (color-coded), close date with slip indicator
2. **MEDDPICC Scorecard** — 8 elements with visual scores (green 4-5 / yellow 3 / red 1-2)
3. **Evidence Summary** — Two columns: Strongest Elements + Critical Gaps
4. **Stakeholder Map** — Compact: Name | Title | Role | Influence | Status
5. **Gap Analysis** — Top 3 risks with severity badges and actions
6. **Next 5 Actions** — Action | Owner | Due | Element Targeted
7. **Stage Recommendation** — ADVANCE / HOLD / DOWNGRADE / DISQUALIFY badge with rationale

---

## Examples

### Example 1: Well-Qualified Deal at Negotiation Stage

**Context:** Enterprise account, $200K ARR, 90 days in pipeline, at Negotiation stage.

**Input:** "Run MEDDPICC deal analysis for [Account]."

**Scoring summary:**
- Metrics: 4/5 — ROI discussed, baseline shared, not formally agreed
- Economic Buyer: 5/5 — VP in meetings, budget confirmed
- Decision Criteria: 4/5 — RFP received, mapping favorable
- Decision Process: 4/5 — Committee known, timeline confirmed, one approver unclear
- Paper Process: 3/5 — Legal review expected, timeline not scoped
- Identified Pain: 5/5 — Multiple quantified pains across stakeholders
- Champion: 5/5 — Key contact actively selling internally
- Competition: 4/5 — Incumbent identified, displacement strategy in place

**Health:** 86/100 (Green). Stage minimum for Negotiation: 65+ ✅. All critical thresholds met.

**Stage Recommendation:** ADVANCE — ready for Closing stage once Paper Process is clarified.

### Example 2: At-Risk Deal Needing Intervention

**Context:** Mid-market account, $45K ARR, stalled at Discovery for 55 days.

**Input:** "MEDDPICC score the [Account] deal."

**Scoring summary:**
- Metrics: 1/5 — No metrics discussion
- Economic Buyer: 1/5 — Unknown
- Decision Criteria: 2/5 — Vague requirements
- Decision Process: 1/5 — Unknown
- Paper Process: 1/5 — Unknown
- Identified Pain: 2/5 — Pain assumed, not confirmed
- Champion: 2/5 — Contact engaging but not advocating
- Competition: 1/5 — No competitive intel

**Health:** 24/100 (Red). Stage minimum for Discovery: 30+ ❌.

**Risk patterns:** Zombie deal (55 days, no progression), Feature-led (no documented pain), Single-threaded.

**Stage Recommendation:** DISQUALIFY unless gaps can be filled within 2 weeks. Specific actions: Re-engage with breakup email, run discovery if they respond, identify EB and champion.

---

## Troubleshooting

### "The weighted score seems wrong"
**Cause:** Math error in weighting. **Solution:** Verify weights sum to 100% and formula is `(sum of score × weight) / 5 × 100`. Each element contributes its score (1-5) × its weight percentage.

### "Rep disagrees with low scores"
**Cause:** Gap between rep knowledge and CRM evidence. **Solution:** Score based on evidence. Suggest the rep log their intelligence to CRM so next pulse reflects it. Frame it as: "The CRM tells one story — let's make sure it tells the right one."

### "Multiple deals requested at once"
**Cause:** Manager wants portfolio view. **Solution:** Run MEDDPICC on each deal individually, then create a summary table comparing health scores and common gap patterns across the portfolio.

---

## Best Practices

### Do's
- **Use the weighting system** — Economic Buyer at 20% is weighted highest for a reason
- **Flag risk patterns** — "happy ears" and "zombie deal" are the most common pipeline killers
- **Connect coaching to specific frameworks** — not generic advice
- **Compare health to stage minimums** — a deal at Closing with health below 75 needs attention

### Don'ts
- **Don't let reps self-score** — the whole point is evidence-based objectivity
- **Don't skip elements** — all 8 must be scored
- **Don't score based on potential** — "they're a great company" isn't a MEDDPICC score
- **Don't average without weighting** — the weights exist to prioritize what matters most

### Quality Checklist
- [ ] All 8 elements scored 1-5 with cited evidence
- [ ] Evidence uses epistemic labels
- [ ] Weighted health score mathematically correct
- [ ] Gap analysis prioritizes deal-killing elements
- [ ] Coaching references specific methodology frameworks
- [ ] Stage recommendation grounded in health vs. stage minimums
- [ ] No placeholder brackets in output

---

## Integration with Other Skills

- **`gtm-deal-pulse`** — Pulse provides the quick 16-signal health check; MEDDPICC is the deep dive. Use Pulse for portfolio triage, MEDDPICC for deals needing intervention.
- **`gtm-call-coaching`** — After coaching a call, re-run MEDDPICC to see if newly gathered intel changes element scores.
- **`gtm-meeting-prep`** — Use MEDDPICC gaps to inform meeting prep: "This meeting should target EB access and Decision Process mapping."
- **`gtm-competitive-strategy`** — When Competition scores ≤2, build a full competitive strategy.

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- MEDDPICC element rubrics, weighting system, health calculation, stage minimums, risk patterns, and coaching framework moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, element definitions, scoring logic, examples, or output formats

### Version 1.0.0 (2026-03-04)

- Initial release
- Client-configurable via Client Profile block
- All 8 weighted elements, scoring rubrics, risk patterns, and coaching mappings preserved
- Vendor-agnostic CRM instructions
- Multi-format artifact generation
