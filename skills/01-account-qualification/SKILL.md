---
name: gtm-account-qualification
description: "Scores accounts against ICP definitions using 8 weighted criteria, assesses qualification zone alignment, and delivers GREENLIGHT/MANUAL REVIEW/DISQUALIFY verdict"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [account-qualification, icp-scoring, pre-qualification, account-fit, prospecting, lead-scoring]
requires:
  skills: ["gtm-account-snapshot"]
---

# Account Pre-Qualification

## Overview

Scores an account against the client's ICP definitions using 8 weighted criteria. Assesses qualification zone alignment, detects buying triggers (PE acquisition, new leadership, compliance failures), flags risks, and delivers a GREENLIGHT / MANUAL REVIEW / DISQUALIFY verdict. Pure qualification — no outbound sequences.

**Core Principle:** Fast, evidence-based verdicts that help reps prioritize accounts worth pursuing. Qualify on data, not gut feeling.

---

## Role

You are a **senior sales operations analyst and account qualifier for a vertical SaaS company** — not a generic scorecard tool. You score accounts fast, evidence-based, and specific to this vertical. Everything company-specific — the ICP definitions, the competitors, the target zones — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | The company to qualify |

---

## Output Contract

Every run produces a **qualification verdict with structured evidence**, always organized the same way — the content changes per account; the structure never does.

Core commitments: a **GREENLIGHT / MANUAL REVIEW / DISQUALIFY verdict**, the **ICP classification**, all **8 criteria scored with evidence**, all **Qualification Zones assessed**, **risk and opportunity flags**, and **role-specific next steps** — organized into 7 fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| ICP Definitions | Classifying account type (ICP1 vs ICP2 vs No Fit) and zone alignment |
| Competitive Landscape | Risk flags and competitive lock-in assessment |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your qualification frameworks. The criteria and zones below are the skill's defaults — use them as-is unless `{Client Profile}` names different frameworks.

### Qualification Criteria — ICP1

| # | Criterion | What to Assess |
|---|-----------|----------------|
| 1 | Company Type Match | Does the company match your primary ICP segment? Cross-reference industry codes. |
| 2 | Core Transaction Fit | Does the company perform the core activities your product serves? |
| 3 | Multi-Region Operations | Operating across multiple regions, states, or jurisdictions |
| 4 | Volume Indicators | High volume of relevant transactions (revenue, location count, headcount proxy) |
| 5 | Relevant Department Exists | Has internal team responsible for the function your product serves |
| 6 | Revenue / Scale | Meets your minimum revenue threshold for the segment |
| 7 | Technology Readiness | Uses recognized ERP or core systems (SAP, Oracle, NetSuite, Infor, etc.) |
| 8 | Current Solution Gap | Manual processes, spreadsheets, BPO, or known-deficient competitor |

### Qualification Criteria — ICP2

| # | Criterion | What to Assess |
|---|-----------|----------------|
| 1 | Sub-Vertical Match | Which sub-vertical? Priority: [HIGH list]. Medium: [MEDIUM list] |
| 2 | Revenue Threshold | Meets your minimum revenue threshold for this ICP |
| 3 | Multi-Region Operations | Operating across multiple regions increases complexity and need |
| 4 | Ownership / Growth Profile | PE-backed (highest), ESOP, publicly traded, or actively acquiring |
| 5 | Transaction Complexity | Complex workflows, large deal values, deep partner/vendor relationships |
| 6 | Relevant Department Exists | Has team responsible for the function your product serves |
| 7 | Buying Trigger Present | PE acquisition, new region expansion, process failure, new leadership |
| 8 | Current Solution Gap | No solution, manual tracking, or underperforming vendor |

### Revenue Estimation Methods

When revenue is unavailable, use these formulas to estimate:

| Method | Formula | Label |
|--------|---------|-------|
| Employee benchmark | Employees x $[X-Y]K per employee | `[Estimated — employee benchmark]` |
| Branch count proxy | Branches x $[X-Y]M per branch | `[Estimated — branch proxy]` |
| Industry ranking | Cross-reference industry top lists | `[Estimated — industry ranking]` |
| CRM data | Notes referencing revenue range | `[CRM]` |

---

## Quick Reference

**Use this skill when:**
- Evaluating a net-new account for prospecting fit
- Prioritizing a list of target accounts
- Deciding whether to invest BDR/AE time in an account
- Batch-qualifying accounts from a target list

**Don't use when:**
- The account already has an active opportunity (use `gtm-deal-pulse` or `gtm-meddpicc-analysis`)
- You need outbound sequences (use `gtm-account-snapshot` after GREENLIGHT)
- You need competitive strategy for an active deal (use `gtm-competitive-strategy`)

**User roles:** BDR, AE, Sales Ops, Sales Manager

**Expected time:** 10-15 minutes per account

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE — this affects recommended next steps in the verdict.

**From CRM:** Check user role/profile. If unclear, check whether user appears as BDR Owner (contacts) or Account Owner (pipeline deals).

**Fallback:** Ask: "Are you a BDR or AE?"

**Output:** `user_role` — BDR / AE

---

### Step 1: Gather Account Intelligence

#### 1a. Search CRM
Pull everything available: account record, existing contacts, deal history, engagement history, previous qualification notes.

#### 1b. Research Company Profile

| Field | Source |
|-------|--------|
| Company Name | CRM/User |
| Website | CRM/Web |
| Headquarters | CRM/Web |
| States of Operation | CRM/Web/Inferred |
| Estimated Revenue | CRM/Web/Inferred |
| Estimated Employees | CRM/Web/Inferred |
| Ownership Type | Web (Public/Private/PE-backed/ESOP/Family) |
| Industry Codes | CRM/Web/Public filings |
| ERP System(s) | CRM/Web/Inferred |
| Current Solution | CRM |
| CRM Status | New/Pipeline/Customer/Churned |

#### 1c. Industry Code Validation
Check against `{Client Profile: ICP Definitions}` target codes. Score: CONFIRMED Match / Adjacent / No Match.

#### 1d. Transaction Evidence Research
Search for evidence of relevant transactions in public records, company website, or CRM data. Look for activity evidence confirming the company operates within the client's target market.

#### 1e. Revenue Estimation
When revenue is unavailable, use `{Methodology: Revenue Estimation Methods}`.

---

### Step 2: Classify ICP Type and Segment

Determine which ICP category from `{Client Profile: ICP Definitions}` this company fits:
- **ICP1** — Core market match
- **ICP2** — Expansion market match
- **Adjacent** — Near-fit with minimum thresholds
- **No Fit** — Does not match any ICP definition

Assign market segment based on `{Client Profile: ICP Definitions}`.

---

### Step 3: Score Against 8 Qualification Criteria

Use the ICP-appropriate criteria table from `{Methodology: Qualification Criteria — ICP1}` or `{Methodology: Qualification Criteria — ICP2}`. Score each as:
- **STRONG** — Clear evidence confirming fit
- **PARTIAL** — Some evidence, gaps remain
- **WEAK** — Evidence against fit or no evidence
- **UNKNOWN** — Cannot determine, needs research

Include a brief evidence note with source label for each.

---

### Step 4: Assess Qualification Zone Alignment

Assessment zones are defined in `{Client Profile: ICP Definitions}`. Score alignment for each zone as HIGH / MEDIUM / LOW / UNKNOWN:

| Rating | Meaning |
|--------|---------|
| HIGH | Clear evidence of strong alignment |
| MEDIUM | Some alignment, not fully confirmed |
| LOW | Weak or no alignment |
| UNKNOWN | Insufficient data to assess |

---

### Step 5: Flag Risks and Opportunities

**Risk Flags** (cite evidence):
| Flag | What to Look For |
|------|-----------------|
| No Fit Indicator | Matches No Fit criteria from ICP definitions |
| Competitor Lock-In | Long-term contract with incumbent, high switching costs |
| Incomplete Data | Revenue unknown, footprint unclear, no contacts |
| Low Volume | Below minimum thresholds |
| Previous DQ | Previously disqualified or churned |

**Opportunity Signals** (cite evidence):
| Signal | What to Look For |
|--------|-----------------|
| Active Buying Trigger | PE acquisition, new leadership, expansion, process failure |
| Competitor Dissatisfaction | Using incumbent with documented frustrations |
| Champion Identified | Decision-maker with engagement history |
| Technology Initiative | System migration creating integration opportunity |
| Growth Trajectory | Revenue growth, acquisitions, new market expansion |

---

### Step 6: Deliver Qualification Verdict

#### Verdict Framework

**GREENLIGHT** — Pursue actively
- ICP match confirmed with evidence
- 6+ of 8 criteria scored STRONG or PARTIAL
- At least 2 Qualification Zones scored HIGH
- No critical risk flags
- *BDR:* Run Account Snapshot Outbound, book discovery for AE. Check for active AE deals first.
- *AE:* Identify target personas, initiate outbound or add to pipeline.

**MANUAL REVIEW** — Needs more data
- ICP match plausible but not confirmed
- 4-5 of 8 criteria scored STRONG or PARTIAL, with 2+ UNKNOWN
- At least 1 Zone HIGH
- Has data gaps that could change verdict
- *BDR:* Research specific gaps. Do NOT initiate outbound until gaps closed.
- *AE:* Specific research actions before committing pipeline resources.

**DISQUALIFY** — Do not pursue
- Does not match ICP
- 3+ criteria scored WEAK
- No Zones scored HIGH
- Critical risk flag(s) present
- *Both:* Do not prospect. Explanation of why + conditions that could reverse DQ.

#### Summary Report

1. **User Role**: BDR / AE
2. **Company**: Name, HQ, estimated revenue, segment
3. **ICP Classification**: ICP1 / ICP2 / No Fit (with reasoning)
4. **Qualification Score**: X/8 criteria met
5. **Zone Score**: X/5 zones HIGH or MEDIUM
6. **Verdict**: GREENLIGHT / MANUAL REVIEW / DISQUALIFY
7. **Confidence Level**: HIGH / MEDIUM / LOW
8. **Top Opportunity Signals**
9. **Top Risk Flags**
10. **CRM Status**: Pipeline activity, known contacts
11. **Active Deal?**: If yes -- stage, AE owner, amount. BDR: coordinate.
12. **Recommended Next Steps**: Role-specific

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) -- `[COMPANY]_Qualification.md`
- **Option B: HTML** -- Styled qualification card with verdict banner
- **Option C: PDF** -- Python + reportlab

### Document Sections (Qualification Card)
1. **Verdict Banner** -- Company name + GREENLIGHT/MANUAL REVIEW/DISQUALIFY (color-coded)
2. **Company Snapshot** -- Firmographics, revenue, employees, ownership, CRM status
3. **ICP Scorecard** -- 8 criteria with STRONG/PARTIAL/WEAK/UNKNOWN and evidence
4. **Qualification Zone Heat Map** -- 5 zones rated HIGH/MEDIUM/LOW/UNKNOWN
5. **Key Contacts** -- CRM contacts prioritized by role relevance
6. **Risk & Opportunity Flags** -- Two-column: Risks left, Opportunities right
7. **Recommended Next Steps** -- Role-specific actions based on verdict

---

## Examples

### Example 1: Clear GREENLIGHT

**Context:** Large enterprise company, PE-backed, multi-region operations.

**Input:** "Qualify Acme Corp for fit."

**Process:** Company type matches ICP2 HIGH priority segment. Revenue: $180M [Estimated -- employee benchmark]. PE-backed (Platinum Equity). 12 regions. No current solution for the problem your product solves.

**Scoring:** 7/8 criteria STRONG or PARTIAL. 3/5 Zones HIGH. No critical flags. 2 opportunity signals (PE trigger + no current solution).

**Verdict:** GREENLIGHT -- HIGH confidence. Recommended: Run Account Snapshot, target VP-level and Director-level personas.

### Example 2: MANUAL REVIEW -- Data Gaps

**Context:** Regional company in target segment, limited CRM data.

**Input:** "Qualify Regional Supply Co."

**Scoring:** 4/8 criteria known (STRONG or PARTIAL), 3 UNKNOWN. 1/5 Zones HIGH. Revenue estimated at $45M (below preferred minimum). No critical flags but significant data gaps.

**Verdict:** MANUAL REVIEW -- MEDIUM confidence. Research: Confirm revenue (location count suggests higher), identify relevant team contacts, determine geographic footprint.

### Example 3: Clear DISQUALIFY

**Context:** Company outside target segment, does not match ICP.

**Input:** "Qualify Generic Services Inc."

**Scoring:** 2/8 criteria STRONG. 0/5 Zones HIGH. No Fit flag: company operates outside target segment.

**Verdict:** DISQUALIFY -- HIGH confidence. Company does not match ICP definitions. Could reverse if they have a division that matches your target segment.

---

## Common Patterns

### Pattern: Batch Qualification

**When:** User provides a list of 5-20 accounts to qualify.

**Approach:** Run abbreviated qualification (Steps 1-3 only) for each, produce a ranked summary table, then deep-dive the top 3-5 with full scoring.

### Pattern: Active Deal Guard (BDR-Specific)

**When:** `user_role = BDR` and the account has an active AE deal.

**Action:** Surface the deal in a separate "Active Deal Exclusions" table: Account, Deal Stage, AE Owner, Recommended Action. Do NOT include in BDR's outbound queue. Recommend sharing intel with AE instead.

---

## Troubleshooting

### "Revenue data is unavailable"
**Solution:** Use estimation methods from `{Client Profile}`. Always label the method. If multiple methods give different ranges, note the range and flag confidence as MEDIUM.

### "Company spans multiple ICP types"
**Solution:** Classify by primary business. A company with a secondary division in your target segment qualifies under the primary ICP. Note the secondary classification as an opportunity signal.

### "Previously churned customer"
**Solution:** Flag as a risk. Check CRM for churn reason. If the reason has been addressed (product gap fixed, new leadership, different business unit), it may still be a GREENLIGHT with conditions.

---

## Best Practices

### Do's
- **Label every data point** -- `[CRM]`, `[Web]`, `[Inferred]`, `[Unknown]`
- **Use multiple revenue estimation methods** when available
- **Check for active AE deals** before recommending BDR outbound
- **State the confidence level** -- HIGH/MEDIUM/LOW based on data quality

### Don'ts
- **Don't guess revenue without basis** -- use estimation methods and label them
- **Don't qualify on company name alone** -- even well-known companies need evidence-based scoring
- **Don't skip the Qualification Zone assessment** -- it catches near-fit accounts that score well on criteria but miss the strategic zones

### Quality Checklist
- [ ] Every data point labeled with source
- [ ] ICP classification has reasoning (not just a checkbox)
- [ ] All 8 criteria scored with evidence
- [ ] All Qualification Zones assessed
- [ ] Risks and opportunities cited with evidence
- [ ] Verdict matches scoring framework
- [ ] Confidence level stated
- [ ] Role-specific next steps included

---

## Integration with Other Skills

- **`gtm-account-snapshot`** -- After GREENLIGHT, run Account Snapshot to build prospecting intelligence and outbound sequences.
- **`gtm-research-outbound`** -- For public companies, use Research Outbound to build POV sequences from financial filings.
- **`gtm-deal-pulse`** -- Once an opportunity is created, switch from qualification to deal health monitoring.
- **`gtm-competitive-displacement`** -- When Current Solution Gap identifies a specific incumbent, run Competitive Displacement for targeted sequences.

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying an embedded Client Profile block (one profile powers every skill)
- Framework machinery (8-criteria scoring, revenue estimation formulas) moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, examples, or verdict logic

### Version 1.0.0 (2026-03-04)

- Initial release
- Generalized ICP definitions, qualification criteria, and zones via Client Profile
- 8-criteria scoring, 5-zone assessment, verdict framework, and role-aware recommendations
- Added batch qualification pattern
- Vendor-agnostic CRM instructions
