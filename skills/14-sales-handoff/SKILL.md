---
name: gtm-sales-handoff
description: "Post-sale implementation readiness assessment: scores 6 dimensions (stakeholder, workflow, technical, data, resource, change management), builds a 3-date handoff plan, evaluates integration readiness, identifies risks with mitigations, maps quick wins for early value delivery, and generates a readiness card for CS team handoff"
version: 1.2.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [sales-handoff, customer-readiness, implementation-readiness, onboarding, cs-handoff, post-sale, kickoff-prep]
requires:
  skills: []
---

# Sales-to-CS Handoff

## Overview

Assesses post-sale implementation readiness across 6 dimensions: stakeholder, workflow, technical, data, resource, and change management. Builds a 3-date handoff plan (signing → implementation start → full adoption), evaluates integration readiness, scores current-state workflows with volume baselines, identifies risks with mitigations, and maps quick wins for early value delivery. Designed for the critical moment between sales close and implementation kickoff.

**Core Principle:** A smooth handoff is the first customer experience after the sale. Every gap left by sales becomes a surprise for CS. This assessment ensures nothing falls through the cracks.

---

## Role

You are a **customer readiness strategist and CS handoff architect**, not a deal reviewer. You assess implementation readiness across six dimensions, build a defensible 3-date handoff plan, identify risks with specific mitigations, map quick wins for early value delivery, and produce a readiness card that signals to CS whether they're walking into a smooth onboarding or a minefield. Everything company-specific (the product modules, pain points, quick win examples) comes from the client profile (see **Context** below), so the same skill assesses readiness for any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask instead of guessing.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name + deal value | ✅ Required | Basic deal data |
| Modules/products purchased | ✅ Required | What's contracted; determines implementation scope |
| Discovery notes (summarized) | ✅ Required | Why they bought, success criteria, technical context |
| Current stakeholder contacts | ✅ Required | Who's involved; maps to implementation roles |
| Source system (if known) | Optional | Known or discovered during sales? |
| Timeline commitments made | Optional | What was promised to the customer |

---

## Output Contract

Every run produces a **readiness card with the same seven sections**. The content changes per account, but the structure never does. This consistency makes readiness assessments comparable across your team: a sales manager reviewing ten cards never has to relearn the layout.

Core commitments: **composite readiness score (0-100) + six dimension scores + 3-date handoff plan + stakeholder map + risk flags + quick wins + handoff checklist**. These are organized into seven fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Account framing, vertical context |
| Core Pain Points | Mapping why they bought (motivation for quick wins) |
| Product Modules | Determining implementation scope and complexity |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your readiness assessment framework. The dimensions and scoring rules below provide a structured approach to evaluating customer readiness and identifying implementation risks.

### 6 Readiness Dimensions (1-5 scale each)

#### Dimension 1: Stakeholder Readiness (Weight: 20%)
- **5** = All roles filled, all contacts responsive
- **4** = Key roles filled, minor gaps
- **3** = Champion identified but sponsor unclear or disengaged
- **2** = Only sales champion engaged, no other stakeholders introduced
- **1** = No clear implementation owner on customer side

#### Dimension 2: Workflow Readiness (Weight: 20%)
- **5** = Workflows fully documented, volume baselines established, success criteria defined
- **4** = Mostly understood, some baselines available
- **3** = General understanding, specific steps and volumes not well documented
- **2** = Limited discovery notes, pain exists but process not mapped
- **1** = No workflow documentation, shallow discovery

#### Dimension 3: Technical Readiness (Weight: 20%)
- **5** = Source system identified and familiar, IT available and engaged, export confirmed, clean data
- **4** = Source system identified, IT available but not briefed, minor data concerns
- **3** = Source system known but unfamiliar format, IT shared or 2-4 week lead, some gaps
- **2** = Source system unclear or multi-system, IT outsourced or constrained, significant data concerns
- **1** = Source system unknown, no IT engagement, never done integration, major data issues

#### Dimension 4: Data Readiness (Weight: 15%)
- **5** = All critical data elements available, clean, customer already exports elsewhere
- **4** = Most data available, minor gaps solvable
- **3** = Core data exists but quality uneven, some manual entry during transition
- **2** = Significant gaps, multiple systems, fragmented data
- **1** = No clear data source, data may not exist in structured format

#### Dimension 5: Resource Readiness (Weight: 15%)
- **5** = Dedicated project resources, realistic timeline, no competing initiatives
- **4** = Resources identified, some competing priorities but manageable
- **3** = Shared resources, may need to work around other initiatives
- **2** = Significant constraints (freeze, migration, key people on leave)
- **1** = No resources allocated, haven't thought about implementation

#### Dimension 6: Change Management Readiness (Weight: 10%)
- **5** = Strong executive mandate, team enthusiastic, champion has communication plan
- **4** = Leadership supports, team open but needs training
- **3** = Some team members resistant, champion will need to manage expectations
- **2** = Significant inertia, multiple skeptics during discovery
- **1** = High resistance, current team sees product as threat, no change champion

**Composite score:** Weighted sum / 5 × 100 = 0-100 score.

| Score | Level | Recommendation |
|-------|-------|----------------|
| 80-100 | Green: Ready | Proceed to kickoff. Standard timeline. |
| 60-79 | Yellow: Ready with conditions | Address gaps before kickoff. May add 2-4 weeks. |
| 40-59 | Orange: At risk | Significant gaps. Delay kickoff until critical dimensions reach 3+. |
| 0-39 | Red: Not ready | Major failures. Sales may need to re-engage. |

### Implementation Stakeholder Roles
| Role | Why They Matter | How to Identify |
|------|-----------------|----------------|
| **Executive Sponsor** | Escalation path, removes blockers, ensures commitment | Senior-most person engaged during sales |
| **Implementation Champion** | Day-to-day rollout owner | Drives adoption, coordinates resources, attends all sessions |
| **IT Lead** | Sets up integrations, manages system connections | Technical person from prospect's IT team |
| **Power Users** | First to learn, train peers | Front-line staff who understand the workflow |
| **Data Owner** | Validates data mapping, confirms accuracy | Person who understands source data model |

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

### Risk Categories
| Category | Common Risks | Mitigation Strategy |
|----------|-------------|-------------------|
| **Technical** | Integration delays, unfamiliar format, IT bandwidth | Fallback: manual upload during setup. Request IT timeline at kickoff. Engage engineering early for unfamiliar systems. |
| **Adoption** | Team resistance, "we've always done it this way" | Champion-led change management. Identify 2-3 power users for pilot. Show quick wins in week 1. |
| **Resource** | Key person on leave, competing projects, seasonal constraints | Build timeline buffer. Identify backup contacts. Set availability commitments at kickoff. |
| **Data** | Poor quality, missing fields, duplicates | Data quality audit in week 1. Cleanup sprint before go-live. Accept manual workarounds initially. |
| **Expectation** | Unrealistic timeline promises, expecting immediate ROI | Align expectations at kickoff. Reference typical timeline. Set 30/60/90 day milestones. |
| **Vendor transition** | Existing provider contract still active, overlapping services | Map contract end dates. Plan parallel-run period. Ensure no service gaps. |

### The 3-Date Handoff Plan
**Date 1: Signing Date:** Contract signing date. Revenue books; starting gun for operations.

**Date 2: Implementation Start Date:** When customer is ready to begin. Based on:
- IT availability
- Competing priorities (system migration, year-end freeze, seasonal)
- Contract terms (deferred billing?)
- Readiness scores: Green (80+) = immediate, Yellow (60-79) = 2-4 week buffer, Orange/Red = resolve blockers first

**Date 3: Full Adoption Date:** Implementation Start + 2 months (default). Adjusted based on:
- Familiar format → faster (shave 2-3 weeks)
- Multi-system or phased rollout → slower (add 2-4 weeks)
- Subsidiary on different system → phased timeline with separate dates per entity

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
- Contracted modules (from the closed-won opportunity record; product/module names per `{Client Profile: Company}`)
- Contract signing date (or expected close)
- AE / opportunity owner
- CS owner (if already assigned)
- How the deal was won (competitive displacement, greenfield, expansion)

**Discovery context (from deal notes and call transcripts):**
- What pain drove the purchase? (Map to `{Client Profile: Core Pain Points}`)
- What does the customer expect success to look like?
- Implementation concerns raised during sales
- Competitors displaced (if any): contract termination timeline
- Timeline commitments made during sales

**Customer profile:**
- Number of employees on the implementation team
- Number of locations or entities to onboard
- Geographic footprint (regions, multi-region complexity)
- Estimated monthly volume (units processed)
- Source system mentioned during sales

---

### Step 2: Build Stakeholder Map

Identify all contacts and assign implementation roles from `{Methodology: Implementation Stakeholder Roles}`:

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

Evaluate the customer's technical environment using `{Methodology: Technical Assessment Dimensions}`.

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
| 80-100 | Green: Ready | Proceed to kickoff. Standard timeline. |
| 60-79 | Yellow: Ready with conditions | Address gaps before kickoff. May add 2-4 weeks. |
| 40-59 | Orange: At risk | Significant gaps. Delay kickoff until critical dimensions reach 3+. |
| 0-39 | Red: Not ready | Major failures. Sales may need to re-engage. |

---

### Step 6: Build 3-Date Handoff Plan + Risk Mitigations

#### The 3-Date Plan

**Date 1: Signing Date:** Contract signing date. Revenue books; starting gun for operations.

**Date 2: Implementation Start Date:** When customer is ready to begin. Assess based on:
- IT availability
- Competing priorities (system migration, year-end freeze, seasonal)
- Contract terms (deferred billing?)
- Customer's stated preference
- Readiness scores: Green (80+) = immediate, Yellow (60-79) = 2-4 week buffer, Orange/Red = resolve blockers first

**Date 3: Full Adoption Date:** Implementation Start + 2 months (default). Adjust based on:
- Familiar format → faster (shave 2-3 weeks)
- Multi-system or phased rollout → slower (add 2-4 weeks)
- Subsidiary on different system → phased timeline with separate dates per entity

**Volume projection:** "Expect to take on [X] units per month for this customer."

#### Risk Mitigations
For each identified risk, document using `{Methodology: Risk Categories}`:
- What the risk is
- Severity (HIGH / MEDIUM / LOW)
- Likelihood
- Specific mitigation plan

#### Quick Wins
Identify 2-3 items from `{Methodology: Quick Win Types}` matched to the customer's actual situation:
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
| Full Adoption | [date] | Impl start + [X] months |

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

**7. Risk Mitigations: Top 3**
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
- **Option A: Markdown** (default): `[COMPANY]_Readiness_Card.md`
- **Option B: HTML**: Styled readiness card with color-coded scores
- **Option C: PDF**: Python + reportlab, single page, letter size, portrait

### Readiness Card Sections (7 Sections)
1. **Deal Banner**: Account, ARR, modules, AE, CS owner, composite readiness score (large, color-coded), 3-date timeline
2. **Readiness Scorecard**: 6 dimensions with color-coded scores (Green 4-5, Yellow 3, Red 1-2)
3. **3-Date Handoff Plan**: Timeline with milestones and volume projection
4. **Stakeholder Map**: Compact table: Name, Title, Impl Role, Status, Contact
5. **Risk Flags**: Top 3 risks with severity badges and one-line mitigations
6. **Quick Wins**: 2-3 early value items for week 1 and month 1
7. **Handoff Checklist**: Two columns: Sales Complete (left), CS Confirms (right)

---

## Examples

### Example 1: Green Readiness: Enterprise Displacement

**Context:** Corvane Industrial ($3.2B manufacturer), $180K ARR deal just closed. Displaced Competitor X. Strong discovery with Sam Okafor (Legal Ops), Dana Whitfield (new GC) signed as Executive Sponsor, IT lead briefed.

**Input:** "Run customer readiness for Corvane Industrial, they just signed."

**Process:** CRM shows closed-won, $180K ARR, Spend Intelligence + Invoice Review + Matter Tracking. Discovery notes: 60+ outside firms, ~$14M counsel spend, currently using spreadsheets. Baseline: ~150 invoices per quarter, 20-30 minutes manual review each, 3-week audit lag. Sam owns ops day-to-day. Dana is executive sponsor. IT lead (network team) confirmed export capability. Source system: existing e-billing export (familiar format).

**Output:** Composite score: 88/100 (Green, ready). All dimensions 4-5 except Resource (3; Q4 budget freeze). 3-date plan: Signing Dec 20 → Impl Start Jan 15 → Full Adoption Mar 15 (familiar format, shaved 2 weeks). Risks: Q4 competing priorities (MEDIUM). Quick win: automate invoice review on top 5 firms in week 1, show 20% time savings. Readiness card generated.

### Example 2: Yellow Readiness: Technical Gaps

**Context:** Ardent Insurance Group ($1.1B carrier), $95K ARR deal near close. Spreadsheet-based process displacement. IT not engaged during sales.

**Input:** "Prep the handoff for Ardent Insurance Group."

**Process:** CRM shows expected close next week, $95K ARR, Spend Intelligence + Invoice Review. Discovery: 17 attorneys managing ~$6M counsel spend across spreadsheets. Acquired by PE firm last quarter. Champion identified (Legal Ops Manager). BUT: IT was never in any sales meeting, source system is "some custom system" (details unclear), no prior integrations. Two team members expressed skepticism about changing spreadsheet process.

**Output:** Composite score: 62/100 (Yellow, ready with conditions). Technical (2/5, red) and Change Management (2/5, red) are critical gaps. Stakeholder (3/5): IT Lead not identified. 3-date plan: Signing Feb 10 → Impl Start Mar 10 (4-week buffer for IT setup) → Full Adoption May 28 (unfamiliar system, add 3 weeks). Risks: IT availability (HIGH), change resistance (MEDIUM), unknown system format (HIGH). Recommendations: (1) AE should facilitate IT introduction before kickoff, (2) Champion needs change management support to address skepticism. Readiness card generated.

### Example 3: Red Readiness: Not Ready

**Context:** Brightwater Logistics ($780M), $45K deal closed but discovery was shallow. Champion left the company post-signature.

**Input:** "Run readiness assessment for Brightwater Logistics."

**Process:** CRM shows closed-won, $45K ARR, Invoice Review only. But: Deputy GC (sales champion) left the company 2 weeks after signing. No other contacts engaged during sales. Discovery notes minimal: pain confirmed ("invoices take too long") but not quantified. Source system unknown. No IT contact. No volume baselines, no current-state process mapped.

**Output:** Composite score: 28/100 (Red, not ready). Stakeholder (1/5), Workflow (2/5), Technical (1/5), Data (1/5), Resource (1/5), Change Mgmt (2/5). Recommendation: **Do not proceed to kickoff.** AE must re-engage: (1) identify new champion, (2) introduce to executive sponsor, (3) identify IT lead, (4) run abbreviated discovery to map workflow and volume. 3-date plan: Signing Jan 30 → Impl Start TBD (blocked until critical gaps resolved) → Full Adoption TBD. Readiness card generated with red banner.

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
**Approach:** Assess champion fatigue risk: they've been driving the evaluation and now need to drive implementation. Identify a backup champion. Ensure the executive sponsor is providing air cover so the champion doesn't burn out.

---

## Troubleshooting

### "Discovery was too shallow for proper assessment"
**Solution:** Score Workflow and Data dimensions as 2 or lower. Flag the gap explicitly: "Sales discovery did not capture sufficient process detail for CS handoff." Recommend the AE conduct a brief follow-up call focused on workflow mapping and volume baselines before kickoff.

### "Champion left the company after signing"
**Solution:** This is a RED flag. Score Stakeholder as 1. Recommendation: AE must identify a new internal champion before implementation begins. Check if the departing champion provided any introductions. Consider whether the deal is still viable without the champion.

### "Customer wants to start immediately but isn't ready"
**Solution:** Use the readiness score to have an evidence-based conversation. "Your eagerness is great: but our experience shows that [specific gap] will cause delays mid-implementation. Let's spend [X weeks] addressing [specific items] so we can go live faster with fewer surprises."

### "AE made timeline promises that don't match readiness"
**Solution:** Document the promise in the Expectation risk category. Recommend the CS team address this at kickoff: align expectations based on actual readiness, not sales-cycle promises. Reference typical implementation timelines and similar customer experiences.

---

## Best Practices

### Do's
- **Run this before the deal closes** (when possible): identifying gaps early gives sales time to address them
- **Capture volume baselines**: these become the success metrics post-implementation
- **Introduce CS during the sales process**: the best handoffs start before the contract is signed
- **Be honest about readiness**: a Red score that surfaces risks early is more valuable than a Green score that hides them

### Don'ts
- **Don't skip the technical assessment**: integration is the #1 cause of implementation delays
- **Don't assume the sales champion will be the implementation champion**: verify this explicitly
- **Don't hand off without a 3-date plan**: CS needs dates to plan resources
- **Don't ignore change management**: team resistance derails more implementations than technical issues

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

- **`gtm-deal-pulse`**: Deal health signals from pulse inform readiness assessment (especially champion status and stakeholder engagement).
- **`gtm-meddpicc-analysis`**: MEDDPICC elements (champion, economic buyer, decision criteria) map directly to stakeholder and workflow dimensions.
- **`gtm-stakeholder-mapping`**: Org map from stakeholder mapping feeds the implementation stakeholder map with pre-existing role classifications.
- **`gtm-meeting-prep`**: Use meeting prep for the kickoff meeting, incorporating readiness gaps as discussion topics.
- **`gtm-call-coaching`**: Post-kickoff calls can be coached for implementation-specific methodology adherence.

---

## Changelog

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose
- Profile section names aligned with the template (Core Pain Points, Product Modules)
- Third handoff date renamed "Full Adoption Date" (was "Full Service Date")

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (6 Readiness Dimensions, Stakeholder Roles taxonomy, Technical Assessment, Risk Categories, 3-Date Plan structure) moved to an explicit Methodology section (`{Methodology: X}` references)
- No functional changes to the workflow, scoring rubrics, or readiness assessment logic

### Version 1.0.0 (2026-03-04)
- Initial release: migrated from customer readiness index
- Generalized via Client Profile block with configurable defaults
- Preserved 6-dimension readiness scoring with weighted composite (1-5 scale, 0-100 composite)
- Preserved 3-date handoff plan (signing → impl start → full adoption, +2 months rule)
- Preserved technical assessment dimensions (source system, integration, data quality)
- Preserved implementation stakeholder role taxonomy
- Preserved quick win types and risk categories with mitigation strategies
- Added Implementation Profile and Product Modules to Client Profile
- Multi-format artifact generation replacing reportlab-only
