---
name: gtm-stakeholder-mapping
description: "Builds complete stakeholder intelligence maps — contact inventory with buying role classification, organizational hierarchy with ghost nodes, 7-dimension weighted multi-threading score, political landscape mapping, and prioritized engagement strategy"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [stakeholder-mapping, org-map, org-chart, multi-threading, buying-committee, influence-map, contact-mapping, deal-strategy]
requires:
  skills: []
---

# Stakeholder Mapping

## Overview

Builds a complete stakeholder intelligence map for a target account. Queries CRM for contacts, classifies each by buying role (Economic Buyer, Champion, Technical Evaluator, Influencer, End User, Blocker, Coach), maps organizational hierarchy with ghost nodes for expected-but-missing positions, scores multi-threading coverage across 7 weighted dimensions, maps political dynamics, and generates a prioritized engagement strategy. Requires only an account name — assembles intelligence entirely from CRM and public sources.

**Core Principle:** Deals are won through multi-threaded consensus, not single-threaded relationships. This map shows who you know, who you're missing, and where to focus next.

---

## Role

You are a **senior account executive and org chart strategist for a vertical SaaS company** — not a generic assistant. You build complete stakeholder maps from CRM data, identifying buying roles, multi-threading gaps, and political dynamics. Everything company-specific — the buyer personas, the ghost node expectations, the value propositions — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | Account in CRM with contact records |
| User role (BDR / AE) | ✅ Required | Framing of engagement strategy (entry point vs. multi-threading) |
| CRM access (all contacts, titles, departments, engagement) | ✅ Required | Complete contact inventory is essential |
| Company size / revenue (if available) | Optional | Used for ghost node identification |
| Active deal status | Optional | If AE with active deal, coordination guidance applies |

---

## Output Contract

Every run produces a **complete stakeholder map with the same 8 sections** — so buying committee strategy can be compared across accounts. The content changes per account; the structure never does.

Core commitments: **contact inventory with buying roles classified**, **organizational hierarchy with ghost nodes**, **7-dimension multi-threading score**, **political landscape**, **coverage gaps and risks**, and **prioritized engagement strategy**.

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Buyer Personas | Buying role classification, department inference |
| Qualification Criteria | Winning zone assessment, org structure expectations |
| Value Propositions | Engagement messaging, persona relevance |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your playbook for stakeholder mapping. The 7 buying roles, multi-threading dimensions and weighting, influence assessment framework, engagement status classification, political landscape quadrant, and ghost node identification logic are your operational blueprint.

### Seven Buying Roles

| Role | Definition | Typical Influence | Key Signals |
|------|-----------|------------------|-----------|
| **Economic Buyer** | Can approve budget and sign contracts | HIGH | Budget authority, P&L responsibility, signature authority |
| **Champion** | Actively advocates internally, sells when you're not in room | HIGH | Shares insider info, coaches on politics, enables other introductions |
| **Technical Evaluator** | Assesses integration, security, technical fit; can veto | HIGH | Tests architecture, asks integration questions, flags blockers |
| **Influencer** | Shapes decision through opinion/expertise; cannot approve alone | MEDIUM | Submits analysis, participates in meetings, frames requirements |
| **End User** | Will use product daily; cares about workflow and ease | MEDIUM | Daily pain points, process feedback, adoption risk signals |
| **Blocker** | Opposes or delays deal; may prefer incumbent | MEDIUM | Raises objections, advocates for status quo, flags concerns |
| **Coach** | Internal ally who provides intel about buying process and politics | LOW-MEDIUM | Shares confidential process details, warns of threats, accelerates timelines |

### Influence Levels

| Level | Criteria |
|-------|----------|
| HIGH | C-level title, confirmed budget authority, demonstrated seniority in meetings |
| MEDIUM | Director/VP, participates actively, asks detailed questions |
| LOW | Manager/IC, end user, referred to by others, minimal participation |
| UNKNOWN | No notes, no meetings, contact added from list |

### Engagement Status

| Status | Criteria |
|--------|----------|
| Actively Engaged | 2+ interactions in last 30 days |
| Partially Engaged | 1 interaction in last 30 days, or 2+ in last 90 days |
| Disengaged/Cold | No interaction in 90+ days |
| Never Contacted | On file but no recorded outreach |
| Active Blocker | Has expressed opposition in notes/calls |

### Relationship Strength (1-5)

| Score | Evidence |
|-------|----------|
| 5 | Champion-level. Actively advocates. Internal conversations on your behalf. |
| 4 | Strong advocate. Responds quickly. Provides intel. |
| 3 | Positive/neutral. Engages when prompted. |
| 2 | Building rapport. Limited interaction history. |
| 1 | Cold/unknown. No meaningful engagement. |

### Multi-Threading Score (7 Dimensions, Weighted)

| Dimension | Weight | 0 (Weak) | 1 (Developing) | 2 (Strong) |
|-----------|--------|----------|---------------|-----------|
| **C-Level Access** | 2x | No C-level contacts | 1 contact, no engagement | 1+ engaged |
| **Champion Identified** | 2x | No champion | Potential champion | Confirmed, active champion |
| **Department Breadth** | 1x | 1 dept only | 2-3 depts | 4+ depts represented |
| **Technical Evaluator** | 1x | No IT contact | IT contact, not engaged | IT engaged/supportive |
| **Economic Buyer Engaged** | 2x | No EB identified | EB identified, not engaged | EB actively engaged |
| **End User Validation** | 1x | No end users known | End users identified | End users engaged |
| **Blocker Mitigation** | 1x | Known blocker, no strategy | Blocker identified, strategy exists | No blockers, or all neutralized |

**Calculation:** Sum all weighted dimension scores (max 20). Normalize to 10-point scale. Interpretation:
- 9-10 = Excellent coverage
- 7-8 = Good coverage with 1-2 gaps
- 5-6 = Developing, material gaps
- 3-4 = Weak, narrow coverage
- 1-2 = Critical, almost no contacts

### Political Landscape Positioning

Classify influential contacts on two axes: **Influence (Y-axis: high to low)** × **Support (X-axis: opponent to strong supporter)**

**Quadrants:**
- **Top-Right (High Influence + Support):** Leverage — your champion, enabler
- **Top-Left (High Influence + Opposition):** Neutralize — the blocker with power
- **Bottom-Right (Low Influence + Support):** Keep Informed — friendly contact
- **Bottom-Left (Low Influence + Opposition):** Monitor — low threat, watch

### Ghost Node Identification

Expected positions that SHOULD exist based on company size but have no contact on file. By revenue threshold:

| Revenue Threshold | Typical Expected Roles |
|-------------------|-----|
| $50M+ | CEO, CFO, CIO/IT Director, VP Operations, VP Sales, General Counsel |
| $100M+ | Add: VP Finance, Chief Procurement Officer, Board members (if relevant) |
| $200M+ | Add: COO, Multiple VPs by function, Regional managers (if multi-region) |
| $500M+ | Add: Senior Director layer, Treasury, Investor Relations |

---

## Quick Reference

**Use this skill when:**
- Preparing for a deal strategy session or coaching call
- Need to assess multi-threading coverage on an active deal
- Building an engagement plan for a new account
- Identifying gaps in buying committee coverage
- Coaching a rep on who to engage next

**Don't use when:**
- Need outbound sequences (use `gtm-account-snapshot` or `gtm-competitive-displacement`)
- Analyzing a specific call (use `gtm-call-coaching`)
- Building competitive strategy (use `gtm-competitive-strategy`)

**User roles:** AE (primary), BDR (entry point identification)
**Expected time:** 15-20 minutes per account

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs. Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

**Role-aware framing:**
- **BDR:** Org map focuses on identifying the best entry point and understanding who to target. Engagement strategy emphasizes prospecting tactics and meeting-booking. If an active AE deal exists, share the org map with the AE — do not prospect independently.
- **AE:** Org map focuses on multi-threading strategy, navigating the buying committee, and advancing the deal. Engagement strategy emphasizes deal progression and consensus-building.

---

### Step 1: Gather Account Context

Query CRM for the account record:

| Field | Source |
|-------|--------|
| Company name | Account record |
| Industry / vertical | Account record |
| Revenue | Account record (if unavailable, estimate from employee count) |
| Employee count | Account record |
| HQ location | Account record |
| Active deal? | Opportunity records (stage, amount, close date, owner) |
| Deal stage | Opportunity record |
| Account owner | Account record |
| BDR owner | Contact/Account record |
| Total contacts on file | Count of Contact records |
| Last interaction | Most recent Activity |

**Active Deal Guard:** If `user_role = BDR` and an active AE deal exists, add coordination guidance: "Active deal owned by [AE name] at [Stage]. Share this org map with the AE — do not prospect independently."

---

### Step 2: Build Contact Inventory

Pull ALL contacts associated with the account from CRM. For each contact, extract:

| Field | Required? |
|-------|-----------|
| Name | Yes |
| Title | Yes |
| Department | Yes (infer from title if not set) |
| Email | If available |
| Phone | If available |
| Location | If available |
| Last interaction date | Yes |
| Last interaction type | If available |
| BDR Owner | Yes |
| Engagement score | Infer from interaction frequency |

**Department Inference Rules:**

| Title Contains | Department |
|---------------|-----------|
| CFO, Controller, Finance, Treasurer, FP&A | Finance |
| Credit, Collections, AR, Accounts Receivable | Finance / Collections |
| CIO, CTO, IT, Technology, Systems, Developer, ERP | Technology |
| COO, Operations, Ops, Supply Chain, Logistics | Operations |
| VP Sales, Sales Director, Sales Manager, Sales Ops | Sales |
| General Counsel, Legal, Compliance Officer | Legal & Compliance |
| CEO, President, GM, General Manager, Owner | Executive |
| HR, People, Talent | Human Resources |
| Procurement, Purchasing | Procurement |

Sort contacts by department, then by seniority (C-level → VP → Director → Manager → IC).

---

### Step 3: Classify Buying Roles & Influence

For each contact, assign:

#### Buying Role (exactly one per contact)

| Role | Definition | Typical Titles |
|------|-----------|---------------|
| **Economic Buyer** | Can approve budget and sign contracts | CFO, CEO, VP Finance, SVP |
| **Champion** | Actively advocates internally, sells when you're not in the room | Director or VP who "gets it" and feels the pain daily |
| **Technical Evaluator** | Assesses integration, security, and technical fit; can veto | CIO, IT Director, ERP Admin, Security Manager |
| **Influencer** | Shapes the decision through opinion/expertise; cannot approve alone | Controller, Department Managers, Regional Managers |
| **End User** | Will use the product daily; cares about workflow and ease of use | Analysts, Specialists, Staff |
| **Blocker** | Opposes or delays the deal; may prefer incumbent | Anyone with stated objections |
| **Coach** | Internal ally who provides intel about buying process and politics | Any contact who shares "insider" information |

#### Influence Level

| Level | Evidence |
|-------|----------|
| HIGH | C-level title, budget authority, demonstrated in notes |
| MEDIUM | Director/VP, participates in demos, asks detailed questions |
| LOW | Manager/IC, end user, referred to by others |
| UNKNOWN | No notes, no meetings, contact added from list |

#### Engagement Status

| Status | Evidence |
|--------|----------|
| Actively Engaged | 2+ interactions in last 30 days |
| Partially Engaged | 1 interaction in last 30 days, or 2+ in last 90 days |
| Disengaged/Cold | No interaction in 90+ days |
| Never Contacted | On file but no recorded outreach |
| Active Blocker | Has expressed opposition in notes/calls |

#### Relationship Strength (1-5)

| Score | Evidence |
|-------|----------|
| 5 | Champion-level. Actively advocates. Internal conversations on your behalf. |
| 4 | Strong advocate. Responds quickly. Provides intel. |
| 3 | Positive/neutral. Engages when prompted. |
| 2 | Building rapport. Limited interaction history. |
| 1 | Cold/unknown. No meaningful engagement. |

---

### Step 4: Map Organizational Hierarchy

Build a hierarchical tree from classified contacts:

1. **Identify top node:** CEO, President, or highest-ranking contact
2. **Group by department:** Finance, Operations, Technology, Sales, Legal, Executive, etc.
3. **Infer reporting lines from titles:** C-level → VP → Director → Manager → IC within each department
4. **Flag confirmed vs. inferred relationships:**
   - **Confirmed:** CRM explicitly shows relationship, or notes reference it
   - **Inferred:** Based on title hierarchy and department
5. **Identify ghost nodes:** Positions that SHOULD exist based on company size and industry but have no contact on file. Use `{Methodology: Ghost Node Identification}` as reference for expected roles by revenue threshold.

Present as a department-grouped table showing:
- Name (or "UNKNOWN — [Expected Title]" for ghost nodes)
- Title
- Buying role badge
- Engagement status
- Relationship strength

---

### Step 5: Score Multi-Threading Coverage

Calculate the multi-threading score (1-10 scale) based on 7 weighted dimensions:

| Dimension | Weight | 0 | 1 | 2 |
|-----------|--------|---|---|---|
| **C-Level Access** | 2x | No C-level contacts | 1 contact, no engagement | 1+ engaged |
| **Champion Identified** | 2x | No champion | Potential champion | Confirmed, active champion |
| **Department Breadth** | 1x | 1 dept only | 2-3 depts | 4+ depts represented |
| **Technical Evaluator** | 1x | No IT contact | IT contact, not engaged | IT engaged/supportive |
| **Economic Buyer Engaged** | 2x | No EB identified | EB identified, not engaged | EB engaged |
| **End User Validation** | 1x | No end users known | End users identified | End users engaged |
| **Blocker Mitigation** | 1x | Known blocker, no strategy | Blocker identified, strategy exists | No blockers, or all neutralized |

**Calculation:** Sum weighted scores. Max = 20. Normalize to 10-point scale.

| Score | Rating | Meaning |
|-------|--------|---------|
| 9-10 | Excellent | Broad coverage, strong champion, EB engaged |
| 7-8 | Good | Solid coverage with 1-2 gaps |
| 5-6 | Developing | Material gaps — missing champion or EB engagement |
| 3-4 | Weak | Narrow — single-threaded or thin contacts |
| 1-2 | Critical | Almost no contacts — deal at risk of ghosting |

**Gap identification:**
- Which buying roles are missing?
- Which departments have zero contacts?
- Are ghost nodes clustered in a critical department?
- Is there a champion? If not, who is the best candidate?

---

### Step 6: Map Political Landscape

For each contact with MEDIUM or HIGH influence, classify:

| Position | Evidence |
|----------|----------|
| **Strong Supporter** | Actively advocates |
| **Supporter** | Positive, willing to help |
| **Neutral** | No clear position |
| **Skeptic** | Has concerns, not yet opposed |
| **Opponent** | Actively resists or prefers incumbent |

**Key dynamics to identify:**
1. **Alliances** — Contacts who work closely together with shared positive sentiment
2. **Tensions** — Known conflicts or competing priorities (e.g., IT security vs. business urgency)
3. **Bridges** — Contacts who can influence multiple departments or levels
4. **Power centers** — Informal influence beyond title
5. **Incumbent loyalty** — Anyone championing the current vendor

Source from CRM notes, activity logs, call transcripts, email patterns, meeting attendance.

---

### Step 7: Build Engagement Strategy

Create a prioritized engagement plan:

| Priority | Criteria | Action Window |
|----------|---------|---------------|
| URGENT | Blocker unaddressed, EB not engaged, Champion at risk | This week |
| HIGH | Missing buying role, key department uncontacted, critical ghost node | Next 2 weeks |
| MEDIUM | Strengthen existing relationship, expand into adjacent department | Next 30 days |
| LOW | Informational contact, maintain awareness | Ongoing |

For each recommended action:
- **Who:** Contact name or ghost node title
- **What:** Specific action (introduction via [contact], direct outreach, executive briefing, technical review)
- **Why:** What gap this closes or risk this mitigates
- **How:** Suggested approach (ask Champion for intro, leverage existing relationship, use peer reference)
- **Messaging:** Which value prop or proof point from `{Client Profile}` is most relevant

**Role-aware strategy:**
- **BDR:** Focus on identifying best entry point and booking first meeting. Recommend personas to target and outreach angles.
- **AE:** Focus on multi-threading breadth, champion enablement, and consensus-building. Recommend deal-advancing actions.

---

### Step 8: Summary Report

| Field | Value |
|-------|-------|
| Account | [Name] |
| Industry | [Industry] |
| Revenue / Employees | [Revenue] / [Employees] |
| Active Deal | [Yes/No — Stage, Amount, Owner] |
| Total Contacts on File | [Count] |
| Contacts Classified | [Count with buying roles assigned] |
| Ghost Nodes Identified | [Count — expected positions with no contact] |
| Multi-Threading Score | [X/10 — Rating] |
| Champion Status | [Confirmed / Potential / None — Name] |
| Economic Buyer Status | [Engaged / Identified / Unknown — Name] |
| Blocker Status | [None / Identified — Name + mitigation] |
| Top 3 Gaps | [Specific gaps] |
| Recommended Next Action | [#1 priority from engagement strategy] |
| User Role | [BDR / AE] |
| Coordination Note | [If BDR + active deal: "Share with AE"] |

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_Stakeholder_Map.md`
- **Option B: HTML** — Styled map with color-coded buying roles and hierarchy visualization
- **Option C: PDF** — Python + reportlab, single page, letter size, landscape orientation

### Stakeholder Map Sections (8 Sections)
1. **Account Snapshot** — Firmographics, deal stage, threading score
2. **Stakeholder Hierarchy** — Department-grouped table with buying role badges, engagement icons, relationship strength. Ghost nodes in italics.
3. **Buying Committee Matrix** — Name, Title, Role, Influence, Engagement, Last Touch, Risk
4. **Multi-Threading Scorecard** — Overall score bar + coverage by dimension + gap callouts
5. **Engagement Status Heat Map** — Grid by department × engagement status
6. **Political Landscape** — Quadrant layout: Influence (Y) × Support (X). Top-right = leverage, Top-left = neutralize, Bottom-right = keep informed, Bottom-left = monitor
7. **Coverage Gaps & Risks** — Missing buying roles, uncontacted departments, ghost nodes, blocker alerts, single-threading risk
8. **Priority Actions** — Top 5 actions with Who, What, Why

**Color-code buying roles:**
- Economic Buyer → red
- Champion → green
- Influencer → yellow
- End User → blue
- Technical Evaluator → purple
- Blocker → grey with warning

---

## Examples

### Example 1: AE Deal Strategy — Enterprise Account

**Context:** AE needs multi-threading assessment before a critical deal review.

**Input:** "Build an org map for [Account] — we're at Negotiation stage and need to multi-thread before the executive review."

**Process:** CRM shows active deal at Negotiation, $1.79M. 8 contacts on file across Finance, Operations, and IT departments. Buying roles classified: CFO (Economic Buyer, partially engaged), VP Operations (Champion, actively engaged), 2 Managers (End Users, engaged), IT Director (Technical Evaluator, neutral), 3 others. Ghost nodes: COO, General Counsel (expected at this company size). Multi-threading score: 7/10 (Good) — strong champion and IT engaged, but EB only partially engaged and no Legal coverage.

**Output:** Full org analysis with hierarchy, 7/10 threading score, political landscape showing VP Operations as bridge between Finance and Operations teams. Engagement strategy: URGENT — get CFO from partial to active engagement via executive briefing. HIGH — identify General Counsel for compliance angle. 8-section stakeholder map generated.

### Example 2: BDR Prospecting — Unknown Account

**Context:** BDR researching a new account to identify the best entry point.

**Input:** "Map the org structure for [Account] so I know who to target first."

**Process:** `user_role = BDR`. CRM shows new account, no active deal. 2 contacts on file (Controller, Analyst). Company research: $5B+ revenue, 45+ locations, multi-region. Ghost nodes: CFO, VP Operations, Director, IT Director, COO, General Counsel (all expected at $5B). Multi-threading score: 2/10 (Critical) — minimal contacts, no champion, no EB.

**Output:** Org analysis showing massive gaps. Engagement strategy focuses on entry point: recommend targeting Director or VP level (likely champion persona) with operational pain angle. BDR-focused recommendations: LinkedIn research for missing contacts, suggested outreach angles per persona. 8-section stakeholder map generated.

---

## Common Patterns

### Pattern: Active Deal Guard (BDR)
**When:** `user_role = BDR` and account has active AE deal.
**Action:** Generate the full org map but deliver with coordination guidance: "Active deal owned by [AE name] at [Stage]. Share this org map with the AE — do not prospect independently."

### Pattern: Pre-Meeting Org Review
**When:** Used in conjunction with `gtm-meeting-prep` before a critical meeting.
**Approach:** Run stakeholder mapping first to understand the buying committee, then run meeting prep to prepare for the specific call. The org map informs who else should be in the room and what political dynamics to navigate.

### Pattern: Coaching Session Prep
**When:** Sales manager needs to review deal health with an AE.
**Approach:** The threading score and gap analysis provide objective coaching points. Focus the conversation on: "What's your plan to engage [missing role]?" and "How are you developing [potential champion]?"

---

## Troubleshooting

### "Only 1-2 contacts on file"
**Solution:** This is common for new accounts. Generate the map with heavy ghost node identification. The value is showing what's MISSING — the engagement strategy becomes a contact discovery plan. Recommend LinkedIn research and `gtm-account-snapshot` for broader intelligence.

### "Can't determine buying roles from titles"
**Solution:** When titles are ambiguous (e.g., "Manager" without department), use department inference rules from Step 2. If department is also unclear, classify as UNKNOWN and flag for discovery. During the next interaction, ask: "Can you tell me about your team's structure?"

### "Political dynamics unclear — no notes in CRM"
**Solution:** Flag political landscape as "Insufficient data — requires direct engagement to assess." Provide a framework for the rep to assess during their next interaction: ask about decision process, who else is involved, and where concerns might come from.

### "Contact is both Champion and Economic Buyer"
**Solution:** Assign the primary role that most affects deal strategy. If someone has budget authority AND actively advocates, classify as Economic Buyer (higher-priority role) and note champion behaviors in the analysis. The engagement strategy should reflect both dimensions.

---

## Best Practices

### Do's
- **Pull ALL contacts** — don't filter to "relevant" ones. The full picture reveals patterns.
- **Identify ghost nodes aggressively** — missing positions are as important as known contacts
- **Source political dynamics from evidence** — CRM notes, interaction patterns, meeting attendance. Don't guess.
- **Tailor engagement strategy to user role** — BDR needs entry points; AE needs multi-threading tactics

### Don'ts
- **Don't assume buying roles from titles alone** — a VP who hasn't engaged isn't automatically a Champion
- **Don't skip the threading score** — it provides the objective assessment that coaching conversations need
- **Don't ignore low-influence contacts** — End Users can become internal champions or surface hidden objections
- **Don't treat ghost nodes as optional** — every missing position is a gap in your deal strategy

### Quality Checklist
- [ ] All CRM contacts pulled (not a subset)
- [ ] Every contact has exactly one buying role, influence level, engagement status
- [ ] Ghost nodes identified using company size thresholds
- [ ] Hierarchy shows confirmed vs. inferred relationships
- [ ] Threading score uses all 7 dimensions with correct weights
- [ ] Political landscape sourced from CRM evidence, not assumed
- [ ] Engagement strategy prioritized by urgency with specific who/what/why
- [ ] Role detected and applied (BDR vs. AE framing)
- [ ] Active Deal Guard checked for BDR users

---

## Integration with Other Skills

- **`gtm-meeting-prep`** — Run stakeholder mapping before meeting prep when multi-attendee dynamics are complex.
- **`gtm-account-snapshot`** — For new accounts with minimal contacts, run snapshot first for broader intelligence, then stakeholder mapping for what you find.
- **`gtm-competitive-strategy`** — Stakeholder map reveals who might be an incumbent champion (Blocker role) — feed this into competitive strategy.
- **`gtm-deal-pulse`** — Threading score and champion status are key inputs to deal health scoring.
- **`gtm-meddpicc-analysis`** — Champion and Economic Buyer identification from the org map directly fills MEDDPICC elements.
- **`gtm-call-coaching`** — After calls, update the org map with new stakeholder intelligence captured during the conversation.

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Buying role definitions (7 roles), influence levels, engagement status, relationship strength framework, multi-threading dimensions (7-weighted), and ghost node expectations moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, contact classification logic, threading algorithm, political landscape assessment, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release
- Client-configurable via Client Profile block
- 7-dimension weighted multi-threading score algorithm
- Buying role classification (7 roles), influence levels, engagement status, relationship strength
- Ghost node identification with revenue-based thresholds
- Political landscape mapping (support/opposition quadrant)
- Ghost Node Expectations in Client Profile for portability
- Multi-format artifact generation
