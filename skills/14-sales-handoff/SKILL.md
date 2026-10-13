---
name: gtm-sales-handoff
description: "Post-sale implementation readiness assessment: scores 6 dimensions (stakeholder, workflow, technical, data, resource, change management), builds a 3-date handoff plan, evaluates integration readiness, identifies risks with mitigations, maps quick wins for early value delivery, and generates a readiness card for CS team handoff"
version: 1.3.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
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
| Modules/products purchased | ✅ Required | What's contracted. Determines implementation scope |
| Discovery notes (summarized) | ✅ Required | Why they bought, success criteria, technical context |
| Current stakeholder contacts | ✅ Required | Who's involved. Maps to implementation roles |
| Source system (if known) | Optional | Known or discovered during sales? |
| Timeline commitments made | Optional | What was promised to the customer |

---

## Output Contract

Every run produces a **readiness report with the same nine sections** (Step 7). The content changes per account, but the structure never does. The readiness card in *Artifact Generation* shows seven of those nine sections. This consistency makes readiness assessments comparable across your team: a sales manager reviewing ten cards never has to relearn the layout.

Core commitments: **composite readiness score (0-100) + six dimension scores + 3-date handoff plan + stakeholder map + risk flags + quick wins + handoff checklist**. These are organized into nine fixed sections (see Step 7 below).

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
**Date 1: Signing Date:** Contract signing date. Revenue books. This is the starting gun for operations.

**Date 2: Implementation Start Date:** When customer is ready to begin. Based on:
- IT availability
- Competing priorities (system migration, year-end freeze, seasonal)
- Contract terms (deferred billing?)
- Readiness scores: Green (80+) = immediate, Yellow (60-79) = 2-4 week buffer, Orange/Red = resolve blockers first

**Date 3: Full Adoption Date:** Implementation Start + 2 months (default). Adjusted based on:
- Familiar format → faster (shave 2-3 weeks)
- Multi-system or phased rollout → slower (add 2-4 weeks)
- Subsidiary on different system → phased timeline with separate dates per entity

### Quick Win Types
Pick 2 or 3 quick wins from these four types. Each one must be something the customer can see working in week one or month one.

| Type | What it is | Generic example |
|------|-----------|-----------------|
| **Automate the highest-volume segment** | Move the most frequent repeat task for one segment into the product | Route the most common request type through the system for the top five accounts in week one |
| **Enable self-service for top customers** | Give the most active customers direct access to the status they check most often | Let the most active customers see their own item status without a call to the team |
| **Run a risk audit of open items** | Review open items for the errors or deadlines that carry the most risk | Check all open items against the deadline list and flag any item due in the next 30 days |
| **Remove one manual step** | Find the single manual step that costs the most team hours and remove or automate it | Replace a manual copy from a spreadsheet with a direct import from the source system |

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
- Contracted modules (from the closed-won opportunity record). Product and module names come from `{Client Profile: Product Modules}`
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

**Date 1: Signing Date:** Contract signing date. Revenue books. This is the starting gun for operations.

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

### Example 1: Green Readiness, Brackhaven Memorial Gardens After Signing

**Context:** Brackhaven Memorial Gardens, two sites and 11,000 plots (profile), has signed (illustrative date). Contract: $21,576 a year at list (two sites at $10,788). Contracted modules: Plot Inventory Digitization and Records and Trust Compliance (illustrative). Pre-need and proposal modules are not in this contract (illustrative). Eli Marsh, Implementation Lead (profile), takes the handoff. Since the last check, the Oldgate systems administrator has joined and confirmed the trust fund ledger export.

**Input:** "Run customer readiness for Brackhaven Memorial Gardens. They just signed."

**Process:** CRM shows closed-won with the two contracted modules. Discovery notes: Ruth Ellery wants unsold plots found and trust fund reports a state auditor will accept (profile). Baseline (illustrative): one double sale in 24 months (profile), trust reports built by hand each year, and plot lookups not yet timed. The family board chair is the executive sponsor. Ruth is the implementation champion. Walt Okonkwo, Operations Director, owns the work orders. Source system: Oldgate Ledger Pro, with a standard export confirmed by IT. Data: plot records on paper, with deed scans scheduled for weeks 2 to 3 (profile).

**Scoring:**

| Dimension | Weight | Score (1 to 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 4 | 0.80 | Sponsor, champion and IT lead named. Power users not yet named |
| Workflow | 20% | 4 | 0.80 | Lookup and trust report steps mapped. Lookup times not yet timed |
| Technical | 20% | 4 | 0.80 | Oldgate export confirmed. IT engaged but not yet briefed |
| Data | 15% | 4 | 0.60 | Deed scans scheduled. Ledger export clean on a sample |
| Resource | 15% | 4 | 0.60 | Eli Marsh assigned. The March 2027 Oldgate renewal competes for attention |
| Change Management | 10% | 4 | 0.40 | Ruth champions it. Walt agreed to a work-order pilot (illustrative) |
| **Total** | **100%** | | **4.00** | |

**Composite:** 4.00 ÷ 5 × 100 = **80/100 (Green, ready)**. The score sits exactly on the Green threshold of 80.

**3-date plan:**
- Signing: 2026-11-16 (illustrative).
- Implementation start: 2026-11-16. Green means immediate.
- Full adoption: implementation start + 2 months = 2027-01-16. No adjustment. The Oldgate export is a standard export, and there is one source system.
- Volume projection: expect to take on about 11,000 plot records across two sites (profile).

**Risks (top 3):** Vendor transition (MEDIUM): the Oldgate contract renews in March 2027, so the parallel run must finish before then. Adoption (MEDIUM): Walt's skepticism, so the work-order pilot goes first. Data (MEDIUM): paper records, so the deed-scan sprint runs in weeks 2 to 3.

**Quick wins:** Week 1, Remove one manual step: replace the binder lookup for the top section with a search, and time it. Month 1, Run a risk audit of open items: check the open plots at both sites for double-sale risk. 90 days: lookup times at or below the baseline Ruth provides, and the trust report built from the system without hand steps.

**Output:** Composite 80 (Green, ready). Kickoff on 2026-11-23 (illustrative) with Eli Marsh and Ruth. Readiness card generated.

### Example 2: Yellow Readiness, Brackhaven Memorial Gardens at Signing (Non-Success)

**Context:** Brackhaven Memorial Gardens is at signing (expected, illustrative date). The IT side was never in a sales meeting. The Oldgate export is known but not yet confirmed by anyone who runs IT. The family board chair is the economic buyer, has been on one call, and has not confirmed the sponsor role. Walt Okonkwo, Operations Director, is skeptical of tablets (profile). This is the non-success case: the deal can be signed, but the handoff is not clean.

**Input:** "Prep the handoff for Brackhaven Memorial Gardens. Signing is expected this month."

**Process:** CRM shows the expected close this month, $21,576 a year at list. Ruth Ellery is the champion. No IT contact is on file. The source is Oldgate Ledger Pro, with an export that has never been tested by IT. Plot records are on paper, and no lookup has been timed. Walt is the operations owner, and he has not agreed to the work-order pilot.

**Scoring:**

| Dimension | Weight | Score (1 to 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 3 | 0.60 | Champion identified. Sponsor unclear: the board chair has not confirmed the role |
| Workflow | 20% | 3 | 0.60 | Steps understood. Volumes and lookup times not documented |
| Technical | 20% | 3 | 0.60 | Oldgate is known. IT is shared, with a 2 to 4 week lead time |
| Data | 15% | 3 | 0.45 | Core data exists on paper. Quality is uneven, and the ledger export is unconfirmed |
| Resource | 15% | 3 | 0.45 | Shared implementation resource, with the March 2027 renewal to work around |
| Change Management | 10% | 3 | 0.30 | Ruth is open. Walt is a skeptic who needs managing |
| **Total** | **100%** | | **3.00** | |

**Composite:** 3.00 ÷ 5 × 100 = **60/100 (Yellow, ready with conditions)**. The score sits at the bottom of the 60 to 79 band.

**3-date plan:**
- Signing: 2026-11-16 (expected, illustrative).
- Implementation start: Yellow means a 2 to 4 week buffer. Three weeks gives 2026-12-07.
- Full adoption: implementation start + 2 months = 2027-02-07. No adjustment, because the paper records are a data-entry step and not a second system. The date leaves about four weeks before the March 2027 renewal.

**Risks (top 3):** Technical (HIGH): no IT lead identified, and the export is untested. Stakeholder (HIGH): the sponsor is not confirmed in writing. Adoption (MEDIUM): Walt's skepticism about tablets.

**Conditions before kickoff:**
1. The AE introduces the Oldgate systems administrator to Eli Marsh before kickoff.
2. The family board chair confirms the executive sponsor role in writing.
3. Ruth brings a week of plot lookup times, so the baseline exists.
4. Walt joins the work-order demo, so his pilot is agreed before kickoff.

**Output:** Composite 60 (Yellow, ready with conditions). The two HIGH risks are the reason it is not Green. Readiness card generated.

### Example 3: Red Readiness, Brackhaven Memorial Gardens Not Ready

**Context:** The family board has moved its meeting twice (illustrative), so no board approval date is set. The Stage 5 to 6 gate requires that date and an agreed handoff plan (profile), so this deal does not clear the gate. Ruth Ellery has been silent for 16 days (illustrative). Walt Okonkwo says he will not sign without a Stonemark pilot. Nobody has looked at the Oldgate export.

**Input:** "Run readiness for Brackhaven Memorial Gardens. Ruth says they're ready to sign."

**Process:** CRM shows Stage 5 Negotiate, $21,576 a year at list, and a close date pushed three times (illustrative). Ruth is the only contact who has responded, and she has gone quiet. No IT contact is on file. No volume baseline exists, and no lookup has been timed. Ruth's "ready to sign" is a claim with no board date behind it, so the skill scores the evidence, not the claim.

**Scoring:**

| Dimension | Weight | Score (1 to 5) | Weighted | Evidence |
|---|---|---|---|---|
| Stakeholder | 20% | 2 | 0.40 | Only the sales champion is engaged. No sponsor or IT lead is introduced |
| Workflow | 20% | 2 | 0.40 | Limited notes. The process is not mapped, and no lookup is timed |
| Technical | 20% | 1 | 0.20 | Source system unverified. No IT engagement, and no integration history |
| Data | 15% | 2 | 0.30 | Paper records and an unexamined ledger export |
| Resource | 15% | 2 | 0.30 | Significant constraint: the board date keeps moving, and the champion is silent |
| Change Management | 10% | 2 | 0.20 | Walt is a skeptic, and the team has not been briefed |
| **Total** | **100%** | | **1.80** | |

**Composite:** 1.80 ÷ 5 × 100 = **36/100 (Red, not ready)**. The score is in the 0 to 39 band.

**Recommendation:** Do not proceed to kickoff. Sales must re-engage first:
1. Get the board approval date, which the Stage 5 to 6 gate requires.
2. Have IT confirm the Oldgate export, using a test file.
3. Find a second champion, since Ruth is the only responsive contact.
4. Run an abbreviated discovery to time plot lookups and set the volume baseline.

**3-date plan:**
- Signing: TBD (not signed, and no board date is set).
- Implementation start: TBD. Blocked until the critical gaps are resolved.
- Full adoption: TBD.

**Output:** Composite 36 (Red, not ready). Sales may need to re-engage before the handoff can happen. Readiness card generated with a red banner.

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
- [ ] Implementation timeline uses the 3-date plan rules, with each adjustment documented
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

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

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
