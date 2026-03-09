---
name: gtm-sales-handoff
description: "Post-sale implementation readiness assessment — scores 6 dimensions (stakeholder, workflow, technical, data, resource, change management), builds a 3-date handoff plan, evaluates integration readiness, identifies risks with mitigations, maps quick wins for early value delivery, and generates a readiness card for CS team handoff"
version: 1.0.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-03-04
tags: [sales-handoff, customer-readiness, implementation-readiness, onboarding, cs-handoff, post-sale, kickoff-prep]
requires:
  skills: []
---

# Sales-to-CS Handoff

## Overview

Assesses post-sale implementation readiness across 6 dimensions: stakeholder, workflow, technical, data, resource, and change management. Builds a 3-date handoff plan (signing → implementation start → full service), evaluates integration readiness, scores current-state workflows with volume baselines, identifies risks with mitigations, and maps quick wins for early value delivery. Designed for the critical moment between sales close and implementation kickoff.

**Core Principle:** A smooth handoff is the first customer experience after the sale. Every gap left by sales becomes a surprise for CS. This assessment ensures nothing falls through the cracks.

---

## Client Profile

> **Configure this block for your company.** Replace the placeholder values below with your actual company data, product modules, pain points, and implementation profile.

### Company
- **Name:** [Your Company]
- **Industry:** [Your vertical] (B2B SaaS)
- **Product:** [One-line product description]

### Product Modules
| Module | What It Does |
|--------|-------------|
| [Module 1] | [Description] |
| [Module 2] | [Description] |
| [Module 3] | [Description] |
| [Module 4] | [Description] |

### Implementation Profile
- **Average implementation timeline:** ~[X] days from start to go-live
- **Implementation model:** [Description of data flow / setup process]
- **Key variables:** [What determines complexity, e.g., system type, data volume, number of entities]
- **Data format:** [What you ingest and how]

### Pain Points (for "Why They Bought" Context)
| # | Pain Point |
|---|-----------|
| 1 | [Pain 1 — e.g., Manual processes, spreadsheets, double entry] |
| 2 | [Pain 2 — e.g., Fragmented systems, no single source of truth] |
| 3 | [Pain 3 — e.g., Vendor deficiencies, errors, delays] |
| 4 | [Pain 4 — e.g., Lack of support, unresponsive vendor] |
| 5 | [Pain 5 — e.g., Inconsistent processes across locations] |
| 6 | [Pain 6 — e.g., Admin burden on teams] |
| 7 | [Pain 7 — e.g., Financial risk from missed deadlines or errors] |

### Implementation Stakeholder Roles
| Role | Who Fills It | Why They Matter |
|------|-------------|-----------------|
| **Executive Sponsor** | [Typical titles] | Escalation path, removes blockers, ensures commitment |
| **Implementation Champion** | Day-to-day rollout owner | Drives adoption, coordinates resources, attends all sessions |
| **IT Lead** | IT director, systems admin, or outsourced IT | Sets up integrations, manages system connections, handles authentication |
| **Power Users** | [Typical roles] | First to learn the system, train peers, provide feedback |
| **Data Owner** | Person who understands the source data model | Validates data mapping, confirms field accuracy, identifies gaps |

### Technical Assessment Dimensions
| Dimension | Green | Yellow | Red |
|-----------|-------|--------|-----|
| Source system identified | Yes, familiar format | Yes, unfamiliar format | Unknown or multiple systems |
| Data export capability | Already sending data elsewhere | IT can build it | No IT capability |
| Integration readiness | Standard practice | Need guidance but capable | Never done it |
| Data quality | Good hygiene, few gaps | Some known issues | Major gaps, duplicates |
| IT availability | Available now, dedicated | Shared resource, 2-4 week lead | Frozen, outsourced, 6+ weeks |
| Security/compliance | Standard, SOC 2 sufficient | Additional documentation needed | Full security audit required |
| Multi-system complexity | Single source system | 2 systems, known pattern | 3+ systems or custom middleware |

### Quick Win Types
| Type | Example | Impact |
|------|---------|--------|
| [Quick Win 1] | [Specific action for top use case] | Immediate time savings |
| [Quick Win 2] | [Specific action for key stakeholders] | Visible daily workflow improvement |
| [Quick Win 3] | [Specific action to build trust] | Builds trust, demonstrates value |
| [Quick Win 4] | [Specific action to eliminate pain] | Tangible proof of purchase decision |

### Risk Categories
| Category | Common Risks | Mitigation Strategy |
|----------|-------------|-------------------|
| **Technical** | Integration delays, unfamiliar format, IT bandwidth | Fallback: manual upload during setup. Request IT timeline at kickoff. Engage engineering early for unfamiliar systems. |
| **Adoption** | Team resistance, "we've always done it this way" | Champion-led change management. Identify 2-3 power users for pilot. Show quick wins in week 1. |
| **Resource** | Key person on leave, competing projects, seasonal constraints | Build timeline buffer. Identify backup contacts. Set availability commitments at kickoff. |
| **Data** | Poor quality, missing fields, duplicates | Data quality audit in week 1. Cleanup sprint before go-live. Accept manual workarounds initially. |
| **Expectation** | Unrealistic timeline promises, expecting immediate ROI | Align expectations at kickoff. Reference typical timeline. Set 30/60/90 day milestones. |
| **Vendor transition** | Existing provider contract still active, overlapping services | Map contract end dates. Plan parallel-run period. Ensure no service gaps. |

---

## Quick Reference

**Use this skill when:**
- A deal is closed-won (or about to close) and needs CS handoff
- Preparing for an implementation kickoff meeting
- Assessing whether a near-close deal is ready for a smooth implementation
- Sales manager reviewing handoff quality

**Don't use when:**
- Deal is still in active sales process (use `gtm-deal-pulse` or `gtm-meddpicc-analysis`)
- Need to understand account strategy pre-sale (use `gtm-competitive-strategy`)
- Customer is already in implementation (this is for the transition point only)

**User roles:** AE (primary), Sales Manager
**Expected time:** 20-30 minutes per account

---

## Core Workflow

### Step 1: Pull Deal and Engagement Data

Query CRM for the specified account:

**Deal basics:**
- Account name, industry, sub-industry
- Contract value (ARR) and deal type
- Contracted modules (from `{Client Profile: Product Modules}`)
- Contract signing date (or expected close)
- AE / opportunity owner
- CS owner (if already assigned)
- How the deal was won (competitive displacement, greenfield, expansion)

**Discovery context (from deal notes and call transcripts):**
- What pain drove the purchase? (Map to `{Client Profile: Pain Points}`)
- What does the customer expect success to look like?
- Implementation concerns raised during sales
- Competitors displaced (if any) — contract termination timeline
- Timeline commitments made during sales

**Customer profile:**
- Number of employees on the implementation team
- Number of locations or entities to onboard
- Geographic footprint (regions, multi-region complexity)
- Estimated monthly volume (units processed)
- Source system mentioned during sales

---

### Step 2: Build Stakeholder Map

Identify all contacts and assign implementation roles from `{Client Profile: Implementation Stakeholder Roles}`:

For each contact:
- Name, title, department, email, phone
- Engagement level during sales (active, moderate, passive)
- Implementation role assignment

**Flag risks:**
- No Executive Sponsor identified → high risk of stalled implementation
- IT Lead not engaged during sales → expect integration delays
- Champion is different person than sales champion → relationship transition needed
- Outsourced IT → longer lead times

---

### Step 3: Assess Current-State Workflows

Analyze how the customer handles their processes today. Pull from discovery notes and call transcripts.

**For each workflow step, assess:**
- How it's done today (manual, system-generated, third-party service)
- Volume per month
- Processing time per unit
- Team hours spent per week
- Known error rates or quality gaps

**Capture volume baselines** (for post-implementation success measurement):
- Units processed per month
- Average processing time per unit
- Team hours spent on admin per week
- Current quality/compliance rate (if known)
- Financial losses attributable to process failures (if disclosed)

---

### Step 4: Assess Technical Readiness

Evaluate the customer's technical environment using `{Client Profile: Technical Assessment Dimensions}`.

Score each dimension as Green / Yellow / Red based on the evidence gathered.

Note integration advantages: system agnostic (if it generates standard output, product can ingest it), most customers already export data to other systems (redirect to integration), existing parsers for familiar file formats.

---

### Step 5: Score 6 Readiness Dimensions

Score each dimension from 1 to 5:

#### Dimension 1: Stakeholder Readiness (Weight: 20%)
| 5 | All roles filled, all contacts responsive |
|---|---|
| 4 | Key roles filled, minor gaps |
| 3 | Champion identified but sponsor unclear or disengaged |
| 2 | Only sales champion engaged, no other stakeholders introduced |
| 1 | No clear implementation owner on customer side |

#### Dimension 2: Workflow Readiness (Weight: 20%)
| 5 | Workflows fully documented, volume baselines established, success criteria defined |
|---|---|
| 4 | Mostly understood, some baselines available |
| 3 | General understanding, specific steps and volumes not well documented |
| 2 | Limited discovery notes, pain exists but process not mapped |
| 1 | No workflow documentation, shallow discovery |

#### Dimension 3: Technical Readiness (Weight: 20%)
| 5 | Source system identified and familiar, IT available and engaged, export confirmed, clean data |
|---|---|
| 4 | Source system identified, IT available but not briefed, minor data concerns |
| 3 | Source system known but unfamiliar format, IT shared or 2-4 week lead, some gaps |
| 2 | Source system unclear or multi-system, IT outsourced or constrained, significant data concerns |
| 1 | Source system unknown, no IT engagement, never done integration, major data issues |

#### Dimension 4: Data Readiness (Weight: 15%)
| 5 | All critical data elements available, clean, customer already exports elsewhere |
|---|---|
| 4 | Most data available, minor gaps solvable |
| 3 | Core data exists but quality uneven, some manual entry during transition |
| 2 | Significant gaps, multiple systems, fragmented data |
| 1 | No clear data source, data may not exist in structured format |

#### Dimension 5: Resource Readiness (Weight: 15%)
| 5 | Dedicated project resources, realistic timeline, no competing initiatives |
|---|---|
| 4 | Resources identified, some competing priorities but manageable |
| 3 | Shared resources, may need to work around other initiatives |
| 2 | Significant constraints (freeze, migration, key people on leave) |
| 1 | No resources allocated, haven't thought about implementation |

#### Dimension 6: Change Management Readiness (Weight: 10%)
| 5 | Strong executive mandate, team enthusiastic, champion has communication plan |
|---|---|
| 4 | Leadership supports, team open but needs training |
| 3 | Some team members resistant, champion will need to manage expectations |
| 2 | Significant inertia, multiple skeptics during discovery |
| 1 | High resistance, current team sees product as threat, no change champion |

**Compute composite score:**
Weighted sum / 5 × 100 = score out of 100.

| Score | Level | Recommendation |
|-------|-------|----------------|
| 80-100 | Green — Ready | Proceed to kickoff. Standard timeline. |
| 60-79 | Yellow — Ready with conditions | Address gaps before kickoff. May add 2-4 weeks. |
| 40-59 | Orange — At risk | Significant gaps. Delay kickoff until critical dimensions reach 3+. |
| 0-39 | Red — Not ready | Major failures. Sales may need to re-engage. |

---

### Step 6: Build 3-Date Handoff Plan + Risk Mitigations

#### The 3-Date Plan

**Date 1 — Signing Date:** Contract signing date. Revenue books; starting gun for operations.

**Date 2 — Implementation Start Date:** When customer is ready to begin. Assess based on:
- IT availability
- Competing priorities (system migration, year-end freeze, seasonal)
- Contract terms (deferred billing?)
- Customer's stated preference
- Readiness scores: Green (80+) = immediate, Yellow (60-79) = 2-4 week buffer, Orange/Red = resolve blockers first

**Date 3 — Full Service Date:** Implementation Start + 2 months (default). Adjust based on:
- Familiar format → faster (shave 2-3 weeks)
- Multi-system or phased rollout → slower (add 2-4 weeks)
- Subsidiary on different system → phased timeline with separate dates per entity

**Volume projection:** "Expect to take on [X] units per month for this customer."

#### Risk Mitigations
For each identified risk, document using `{Client Profile: Risk Categories}`:
- What the risk is
- Severity (HIGH / MEDIUM / LOW)
- Likelihood
- Specific mitigation plan

#### Quick Wins
Identify 2-3 items from `{Client Profile: Quick Win Types}` matched to the customer's actual situation:
- Week 1 quick win
- Month 1 value milestone
- 90-day success criteria (measurable outcomes)

---

### Step 7: Readiness Report

**1. Deal Handoff Summary**
Account, ARR, modules, AE, CS owner, why they bought, competitor displaced

**2. 3-Date Handoff Plan**
| Date | Value | Basis |
|------|-------|-------|
| Signing | [date] | Contract signed / expected close |
| Implementation Start | [date] | Based on readiness factors |
| Full Service | [date] | Impl start + [X] months |

Volume projection.

**3. Readiness Scorecard**
| Dimension | Score | Key Evidence | Primary Risk |
|-----------|-------|-------------|-------------|
| Stakeholder | X/5 | | |
| Workflow | X/5 | | |
| Technical | X/5 | | |
| Data | X/5 | | |
| Resource | X/5 | | |
| Change Mgmt | X/5 | | |
| **Composite** | **X/100** | | |

**4. Stakeholder Map**
| Name | Title | Impl Role | Engagement | Contact |
|------|-------|-----------|-----------|---------|

**5. Current-State Workflow Summary**
How they handle each process today, monthly volume, processing time, key pain.

**6. Technical Environment**
Source system, server type, integration path, IT availability, data quality.

**7. Risk Mitigations — Top 3**
Risk, severity, mitigation plan.

**8. Quick Wins**
Week 1, Month 1, 90-day success criteria.

**9. Handoff Checklist**

**Sales Team Completes:**
- [ ] Discovery notes and call recordings shared
- [ ] All stakeholder contacts verified
- [ ] Timeline commitments documented
- [ ] Technical requirements noted
- [ ] Success criteria agreed with customer
- [ ] 3-date plan communicated

**CS Team Confirms:**
- [ ] CS owner assigned
- [ ] Implementation resources allocated
- [ ] Kickoff meeting scheduled
- [ ] Integration requirements reviewed
- [ ] Risk mitigation plan acknowledged

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_Readiness_Card.md`
- **Option B: HTML** — Styled readiness card with color-coded scores
- **Option C: PDF** — Python + reportlab, single page, letter size, portrait

### Readiness Card Sections (7 Sections)
1. **Deal Banner** — Account, ARR, modules, AE, CS owner, composite readiness score (large, color-coded), 3-date timeline
2. **Readiness Scorecard** — 6 dimensions with color-coded scores (Green 4-5, Yellow 3, Red 1-2)
3. **3-Date Handoff Plan** — Timeline with milestones and volume projection
4. **Stakeholder Map** — Compact table: Name, Title, Impl Role, Status, Contact
5. **Risk Flags** — Top 3 risks with severity badges and one-line mitigations
6. **Quick Wins** — 2-3 early value items for week 1 and month 1
7. **Handoff Checklist** — Two columns: Sales Complete (left), CS Confirms (right)

---

## Examples

### Example 1: Green Readiness — Enterprise Displacement

**Context:** $1.2M ARR deal just closed. Competitor displacement. Strong discovery, champion engaged, IT briefed during eval.

**Input:** "Run customer readiness for [Enterprise Account] — they just signed."

**Process:** CRM shows closed-won, $1.2M ARR, [Module A] + [Module B] + [Module C]. Discovery notes: 2,800 units/month current volume, 10-15 min each manual processing, [competitor] displaced. IT lead participated in technical review. Champion (VP [Function]) drove internal advocacy. CFO signed as Executive Sponsor. Source system: [familiar system] (familiar format).

**Output:** Composite score: 88/100 (Green — Ready). All dimensions 4-5 except Resource (3 — Q4 competing priorities). 3-date plan: Signing Jan 15 → Impl Start Feb 1 → Full Service Mar 28 (familiar format, shaved 2 weeks). Risks: Q4 resource competition (MEDIUM). Quick win: automate top-volume use case in week 1. Readiness card generated.

### Example 2: Yellow Readiness — Technical Gaps

**Context:** $95K ARR deal near close. Manual process displacement. IT not engaged during sales.

**Input:** "Prep the handoff for [Mid-Market Account]."

**Process:** CRM shows expected close next week, $95K ARR, [Module A] + [Module B]. Discovery: spreadsheet-based processes across 45+ locations, 30+ regions. Champion identified ([Director]). BUT: IT was never in any sales meeting, source system is "some custom system" (details unclear), no integration experience. 3 team members expressed skepticism about changing process.

**Output:** Composite score: 62/100 (Yellow — Ready with conditions). Technical (2/5 — Red) and Change Management (2/5 — Red) are critical gaps. Stakeholder (3/5) — IT Lead not identified. 3-date plan: Signing Feb 10 → Impl Start Mar 10 (4-week buffer for IT setup) → Full Service May 28 (unfamiliar system, add 3 weeks). Risks: IT availability (HIGH), change resistance (MEDIUM), unknown system format (HIGH). Recommendations: (1) AE should facilitate IT introduction before kickoff, (2) Champion needs change management support. Readiness card generated.

### Example 3: Red Readiness — Not Ready

**Context:** $45K deal closed but discovery was shallow. Champion left the company.

**Input:** "Run readiness assessment for [Account]."

**Process:** CRM shows closed-won, $45K ARR. But: sales champion ([Manager]) left the company 2 weeks after signing. No other contacts engaged. Discovery notes are minimal — pain confirmed but not quantified. Source system unknown. No IT contact. No volume baselines.

**Output:** Composite score: 28/100 (Red — Not ready). Stakeholder (1/5), Workflow (2/5), Technical (1/5), Data (1/5), Resource (1/5), Change Mgmt (2/5). Recommendation: **Do not proceed to kickoff.** AE must re-engage: (1) identify new champion, (2) introduce to executive sponsor, (3) identify IT lead, (4) run abbreviated discovery to fill gaps. 3-date plan: Signing Jan 30 → Impl Start TBD (blocked until critical gaps resolved) → Full Service TBD. Readiness card generated with RED banner.

---

## Common Patterns

### Pattern: Phased Rollout (Multi-Entity)
**When:** Customer has subsidiaries on different systems or multiple business units.
**Approach:** Build separate 3-date plans per entity. Start with the highest-volume entity or the one with the strongest champion. Use early entity success as proof for rolling out to others. Each entity gets its own technical assessment.

### Pattern: Competitive Displacement with Overlap
**When:** Customer is displacing an incumbent and there's a contract overlap period.
**Approach:** Map the incumbent's contract end date. Plan a parallel-run period where both solutions are active. Ensure the handoff plan accounts for data migration from the incumbent. Quick win: demonstrate superiority during the overlap.

### Pattern: Champion-Led Handoff
**When:** The sales champion IS the implementation champion (most common).
**Approach:** Assess champion fatigue risk — they've been driving the evaluation and now need to drive implementation. Identify a backup champion. Ensure the executive sponsor is providing air cover so the champion doesn't burn out.

---

## Troubleshooting

### "Discovery was too shallow for proper assessment"
**Solution:** Score Workflow and Data dimensions as 2 or lower. Flag the gap explicitly: "Sales discovery did not capture sufficient process detail for CS handoff." Recommend the AE conduct a brief follow-up call focused on workflow mapping and volume baselines before kickoff.

### "Champion left the company after signing"
**Solution:** This is a RED flag. Score Stakeholder as 1. Recommendation: AE must identify a new internal champion before implementation begins. Check if the departing champion provided any introductions. Consider whether the deal is still viable without the champion.

### "Customer wants to start immediately but isn't ready"
**Solution:** Use the readiness score to have an evidence-based conversation. "Your eagerness is great — but our experience shows that [specific gap] will cause delays mid-implementation. Let's spend [X weeks] addressing [specific items] so we can go live faster with fewer surprises."

### "AE made timeline promises that don't match readiness"
**Solution:** Document the promise in the Expectation risk category. Recommend the CS team address this at kickoff: align expectations based on actual readiness, not sales-cycle promises. Reference typical implementation timelines and similar customer experiences.

---

## Best Practices

### Do's
- **Run this before the deal closes** (when possible) — identifying gaps early gives sales time to address them
- **Capture volume baselines** — these become the success metrics post-implementation
- **Introduce CS during the sales process** — the best handoffs start before the contract is signed
- **Be honest about readiness** — a Red score that surfaces risks early is more valuable than a Green score that hides them

### Don'ts
- **Don't skip the technical assessment** — integration is the #1 cause of implementation delays
- **Don't assume the sales champion will be the implementation champion** — verify this explicitly
- **Don't hand off without a 3-date plan** — CS needs dates to plan resources
- **Don't ignore change management** — team resistance derails more implementations than technical issues

### Quality Checklist
- [ ] Deal data complete (account, ARR, modules, AE, contract date)
- [ ] 3-date plan built with reasoning for each date
- [ ] At least Executive Sponsor, Champion, and IT Lead identified or flagged as missing
- [ ] Workflow baselines captured (volume, processing time)
- [ ] Technical assessment complete (source system, integration path)
- [ ] All 6 dimensions scored with evidence
- [ ] Every risk has a specific mitigation plan (not generic)
- [ ] Quick wins reference the customer's actual situation
- [ ] No placeholder brackets in final output
- [ ] Implementation timeline uses product benchmarks with adjustments documented
- [ ] Handoff checklist populated for both sales and CS teams

---

## Integration with Other Skills

- **`gtm-deal-pulse`** — Deal health signals from pulse inform readiness assessment (especially champion status and stakeholder engagement).
- **`gtm-meddpicc-analysis`** — MEDDPICC elements (champion, economic buyer, decision criteria) map directly to stakeholder and workflow dimensions.
- **`gtm-stakeholder-mapping`** — Org map from stakeholder mapping feeds the implementation stakeholder map with pre-existing role classifications.
- **`gtm-meeting-prep`** — Use meeting prep for the kickoff meeting, incorporating readiness gaps as discussion topics.
- **`gtm-call-coaching`** — Post-kickoff calls can be coached for implementation-specific methodology adherence.

---

## Changelog

### Version 1.0.0 (2026-03-04)
- Initial release — migrated from customer readiness index
- Generalized via Client Profile block with configurable defaults
- Preserved 6-dimension readiness scoring with weighted composite (1-5 scale, 0-100 composite)
- Preserved 3-date handoff plan (signing → impl start → full service, +2 months rule)
- Preserved technical assessment dimensions (source system, integration, data quality)
- Preserved implementation stakeholder role taxonomy
- Preserved quick win types and risk categories with mitigation strategies
- Added Implementation Profile and Product Modules to Client Profile
- Multi-format artifact generation replacing reportlab-only
