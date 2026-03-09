---
name: gtm-trigger-event-outbound
description: "Capitalizes on time-sensitive business events — acquisitions, leadership changes, expansions, funding rounds, compliance failures — to generate urgency-driven outbound with event classification, relevance window calculation, rapid-response sequences, and single-page cheatsheet"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-03-04
tags: [trigger-event, news-outbound, acquisition, leadership-change, expansion, event-driven-prospecting, urgency-sequences]
requires:
  skills: []
---

# Trigger Event Outbound

## Overview

Capitalizes on time-sensitive business events — acquisitions, leadership changes, geographic expansions, funding rounds, competitor contract events, compliance failures, or earnings signals — to generate urgency-driven outbound. Classifies the trigger type, calculates the relevance window, connects the event to product value, and generates rapid-response email sequences. Prioritizes timeliness over depth.

**Core Principle:** Trigger events create a 7-14 day window where relevance peaks and response rates are 3-5x higher than cold outreach. Speed + specificity — reference the exact event, connect to a business implication, present your product as the solution.

---

## Client Profile

> **Configure this block for your company.** Replace the placeholder values below with your actual company data, ICP definitions, personas, and competitive landscape.

### Company
- **Name:** [Your Company]
- **Industry:** [Your vertical] (B2B SaaS)
- **Product:** [One-line product description]

### Buyer Personas
| # | Persona | Hook Focus |
|---|---------|------------|
| 1 | **[Title]** | [Top priorities and pain themes] |
| 2 | **[Title]** | [Top priorities and pain themes] |
| 3 | **[Title]** | [Top priorities and pain themes] |
| 4 | **[Title]** | [Top priorities and pain themes] |
| 5 | **[Title]** | [Top priorities and pain themes] |
| 6 | **[Title]** | [Top priorities and pain themes] |

### Trigger Type Taxonomy

| Trigger Type | What It Means | Urgency Window | Primary Persona |
|-------------|---------------|----------------|----------------|
| **Acquisition / M&A** | Instant operational complexity increase | 7-14 days | [Relevant personas] |
| **New Executive Hire** | Fresh eyes evaluate tools; 90-day mandate | 30-60 days | The new hire directly |
| **Geographic Expansion** | New regions = new requirements | 14-30 days | [Relevant personas] |
| **Competitor Contract Event** | Renewal window or dissatisfaction signal | 30-60 days pre-renewal | [Relevant personas] |
| **Compliance Failure / Costly Error** | Missed deadline or process failure — pain is fresh | 7-14 days | [Relevant personas] |
| **Earnings Miss / Margin Pressure** | Optimization becomes urgent | 7-14 days | [Relevant personas] |
| **PE Investment / Recapitalization** | New sponsor demands operational efficiency | 14-30 days | [Relevant personas] |
| **Large Contract Win** | High-value deal = high-value exposure if process fails | 14-21 days | [Relevant personas] |
| **Leadership Thought Leadership** | Executive posts about relevant pain on LinkedIn | 3-7 days | The person who posted |

### Trigger Classification Decision Tree

When classifying ambiguous events, apply this decision tree:

1. **Is this a personnel change?** → New Leadership Hire (even if triggered by M&A)
2. **Does it involve a financial event (funding, earnings, bad debt)?** → Match to Financial trigger type
3. **Does it change the company's geographic footprint?** → Geographic Expansion (even if via acquisition)
4. **Does it involve a competitor?** → Competitor Contract Event
5. **Is it a project win or award?** → Large Contract Win
6. **Is it a LinkedIn/social post?** → Leadership Thought Leadership
7. **None of the above?** → Evaluate whether it is genuinely a trigger or just news. Not all news is a trigger.

### Event-to-Value Mapping

**Acquisition / M&A:**
- Every acquisition brings new operational requirements
- Different processes, systems, and vendor relationships across entities
- Integration burden: different ERPs, workflows, and standards
- Product automates and unifies operations across all entities from a single platform

**New Leadership Hire:**
- New leaders evaluate tools in first 90 days
- May have prior experience with your product or competitors
- Fresh mandate to optimize processes
- Previous company context can warm the introduction

**Geographic Expansion:**
- New regions may introduce new regulatory or operational requirements
- Each new market adds complexity to existing processes
- Compliance and operational complexity grows non-linearly with geographic footprint

**Compliance Failure / Costly Error:**
- Financial loss is immediate and quantifiable
- Recovery opportunity diminishes over time
- Single failure often triggers a full process review
- Emotional urgency is highest of any trigger type

**Earnings / Margin Pressure:**
- Optimization becomes board-level priority
- Efficiency improvements = freed working capital
- Cost optimization language in earnings calls signals openness to new tools

**PE Investment / Recapitalization:**
- New sponsor audits all operational processes in first 100 days
- Efficiency mandates come from the board, not just management
- Operational risk becomes a due diligence finding if unaddressed
- Integration of portfolio companies multiplies complexity

**Large Contract Win:**
- High-value deal = high-value exposure if operations fail
- Requirements may differ from the company's typical work
- Resource strain from large projects can cause gaps on other work

### Value Propositions
1. [Value prop 1]
2. [Value prop 2]
3. [Value prop 3]
4. [Value prop 4]
5. [Value prop 5]

### Proof Points (matched to trigger type)
| Trigger Type | Best Proof Point |
|-------------|-----------------|
| Acquisition / M&A | [Customer]: [Integration metric] |
| New Leader | [Customer]: [Adoption metric] |
| Geographic Expansion | [Customer]: [Multi-region metric] |
| Compliance Failure | [Customer]: [Recovery metric] |
| Competitor Event | [Customer]: [Displacement metric] |
| Earnings / Margin | [Customer]: [Efficiency metric] |
| PE Investment | [Customer]: [Integration metric] |
| Large Contract Win | [Customer]: [Coverage metric] |

### Industry Context
- [Macro trend 1]
- [Macro trend 2]
- [Macro trend 3]
- [Macro trend 4]
- [Macro trend 5]

---

## Quick Reference

**Use this skill when:**
- A prospect company just had a news event (acquisition, expansion, new hire)
- Earnings call revealed relevant signals
- A competitor contract is expiring
- A compliance failure or financial event just occurred
- LinkedIn post by a prospect executive touches on relevant pain

**Don't use when:**
- No specific trigger event exists (use `gtm-account-snapshot` for cold outbound)
- The account has a known incumbent to displace (use `gtm-competitive-displacement`)
- The account is closed-lost (use `gtm-closed-loss-reactivation`)

**User roles:** BDR, AE
**Expected time:** 10-15 minutes per account (speed is critical)

---

## Epistemic Rules

### Evidence Grading for Trigger Events
Every trigger event claim must be graded:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified — Source]` | Confirmed via press release, SEC filing, news article, LinkedIn announcement | Reference directly in outbound emails |
| **INFERRED** | `[Inferred — Basis]` | Logical conclusion from verified event (e.g., "acquisition means new operational requirements") | Use in business implications and discovery questions |
| **UNVERIFIED** | `[Unverified — Rumor/Single source]` | Heard from a single source, social media rumor, unconfirmed report | Do NOT reference in outbound; monitor until confirmed |

### Timeliness Rules
1. **Never reference an unverified event** — if the source is uncertain, wait for confirmation
2. **Date-stamp every trigger** — urgency windows are calculated from the event date, not the discovery date
3. **Stale events lose power** — if the urgency window has closed, do not send trigger sequences; use a different skill
4. **Multiple sources increase confidence** — an acquisition announced in a press release AND covered by industry media is VERIFIED; a LinkedIn rumor is UNVERIFIED
5. **Business implications are always INFERRED** — the event is verified, but the implication for the prospect is your hypothesis

### Urgency Window Calculation
- **Start date:** When the event was publicly announced (not when you discovered it)
- **End date:** Start date + urgency window from Trigger Type Taxonomy
- **Days remaining:** End date - today
- **If days remaining <= 0:** Event is stale. Consider whether residual relevance exists (acquisitions: yes, LinkedIn posts: no) or use a different skill

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

**Role-aware handling:**
- **BDR + no active deal:** Full sequences — book meeting for AE.
- **BDR + active AE deal:** Generate analysis but add coordination: "Active deal owned by [AE name]. Share trigger intel — the event may accelerate their deal."
- **AE:** Full sequences — use trigger to advance deal.

---

### Step 1: Identify and Classify the Trigger Event

#### 1a. Confirm Inputs
- Company name
- The trigger event (what happened)
- Source (news article, press release, CRM note, LinkedIn post, earnings call)
- Date of the event (timeliness matters)
- URL or reference to the source material (if available)

#### 1b. Classify the Trigger Type
Map the event to `{Client Profile: Trigger Type Taxonomy}`. If the event is ambiguous, use the `{Client Profile: Trigger Classification Decision Tree}`. Determine:
- **Trigger Type**: Classification
- **Urgency Window**: Days remaining before event becomes stale
- **Primary Persona**: Who cares most about this event
- **Evidence Grade**: VERIFIED / INFERRED / UNVERIFIED per Epistemic Rules

#### 1c. Search CRM
Check for existing pipeline, contacts, and engagement history.
**Active Deal Guard:** Surface existing deals and coordination guidance.

#### 1d. Validate Timeliness
Calculate urgency window per Epistemic Rules:
- Event date: [date]
- Urgency window: [days from taxonomy]
- Days remaining: [calculated]
- Assessment: URGENT (>50% window remaining) / CLOSING (25-50%) / STALE (<25%) / EXPIRED (0 or negative)

If EXPIRED: recommend a different approach (snapshot, research outbound) unless the event has lasting implications (e.g., acquisition integration takes 12-18 months).

---

### Step 2: Build the Event Intelligence Brief

#### Event Summary
- **Event:** What happened (specific)
- **Date:** When it occurred or was announced
- **Source:** Where the information came from + evidence grade
- **Company:** Full company name
- **Trigger Type:** Classification
- **Urgency Window:** Days remaining for peak relevance
- **Timeliness Assessment:** URGENT / CLOSING / STALE / EXPIRED

#### Business Implications
Connect the event to specific product value using `{Client Profile: Event-to-Value Mapping}`. Identify 4-6 business implications, each connecting the event to a specific value proposition.

Format each implication:
```
- **Implication:** [What the event means for the prospect]
- **Value Connection:** [How your product addresses this]
- **Evidence Grade:** [VERIFIED event → INFERRED implication]
```

---

### Step 3: Generate Time-Sensitive Sequences

Produce a **3-step rapid-response sequence** for each recommended persona. Trigger events use 3 steps (not 4) because the urgency window is shorter.

#### Persona Selection
Based on the trigger type, recommend top 2-3 personas from `{Client Profile: Trigger Type Taxonomy}`.

#### Rules for Every Email
- Include a **subject line** referencing the event (not generic)
- Body **<= 100 words** (urgency demands brevity)
- **First line must reference the specific trigger event** with enough detail to prove awareness
- **CTA**: Frame as time-sensitive ("before integration planning kicks off" / "while evaluating the landscape")
- If known contact exists, address by name
- Only VERIFIED events may be referenced directly; INFERRED implications should be framed as questions

#### Sequence Structure (Per Persona)

| Step | Timing | Angle |
|------|--------|-------|
| **Email 1** | Day 1 | Event + immediate business implication + product as the answer |
| **Email 2** | Day 4-5 | Different implication + proof point from comparable company |
| **Email 3** | Day 8-10 | Soft close / breakup — "If timing isn't right, when would be?" |

#### After Each Persona Sequence, Include:
- Why this persona for this trigger (1 line)
- Best discovery question grounded in the event (1 bullet)
- Persona-specific CTA framing (1 line)

Match proof points from `{Client Profile: Proof Points}` to the trigger type. Max 1 per email, labeled with source.

---

### Step 4: Summary Report

1. **Company**: Name + trigger event summary
2. **Trigger Type**: Classification
3. **Evidence Grade**: VERIFIED / INFERRED / UNVERIFIED
4. **Urgency Window**: Days remaining + timeliness assessment
5. **CRM Status**: Pipeline activity + known contacts + current owner
6. **Personas Targeted**: Which 2-3 and why
7. **Sequences Generated**: [Count] personas x 3 emails
8. **Strongest Opening**: Highest-impact first line
9. **User Role**: BDR / AE
10. **Coordination Note**: Active deal guidance if applicable

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_Trigger_Outbound.md`
- **Option B: HTML** — Styled cheatsheet with urgency banner
- **Option C: PDF** — Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)
1. **Event Summary** — Trigger type, date, urgency window, source
2. **Company Snapshot** — Name, HQ, segment, size, regions, CRM status
3. **Key Personas** — CRM contacts filtered by trigger relevance
4. **Event Implications** — 4-6 business implications as talk tracks
5. **Discovery Questions** — Event-specific, not generic
6. **Value Props** — Event-specific value prop, wedge, 1-2 proof points
7. **Objection Handling** — Event-aware rebuttals ("too early to evaluate," "focused on integration")
8. **Call Flow** — Event-led 5-step talk track

**Include URGENCY BANNER at top** with days remaining and timeliness assessment color.

---

## Examples

### Example 1: Acquisition Trigger — PE Rollup

**Context:** Large company in your vertical acquires a regional player. Press release published 3 days ago.

**Input:** "[Target Company] just acquired a regional competitor. Build trigger event outbound sequences."

**Step 1 — Classify:** Trigger type: Acquisition / M&A. Source: Press release on investor relations page [Verified — press release]. Event date: 3 days ago. Urgency window: 7-14 days. Days remaining: 11. Timeliness: URGENT.

**Step 1c — CRM Search:** Existing account with 2 contacts: VP [Function] (active, last meeting 60 days ago) and Controller (inactive, 180 days). No active deal. BDR Owner assigned. Previous closed-lost deal 14 months ago (budget/timing).

**Step 2 — Event Intelligence Brief:**
- **Implication 1:** Acquisition adds new regional requirements — different processes and standards to absorb. [INFERRED from verified acquisition]
- **Implication 2:** Integration of acquired entity means different ERP, different processes, different vendor relationships to unify. [INFERRED]
- **Implication 3:** Staff from acquired company may not know the parent company's process — training gap risk. [INFERRED]
- **Implication 4:** Increased operational exposure — acquired entity's work now needs coverage. [INFERRED]

**Step 3 — Sequences:** 3 persona sequences (CFO, VP Finance, Head of [Function]) x 3 emails = 9 emails.

**CFO — Email 1:**
Subject: [Target Company]'s acquisition and multi-region operations

Congratulations on the acquisition. Integrating a new entity's operational requirements across multiple regions is one of the fastest ways for an acquisition to create hidden risk.

[Target Company] already operates in [X] regions — each with different requirements. The acquired entity adds new projects, new deadlines, and new processes to absorb.

When [Reference Customer] faced a similar integration, they [key metric]. Worth a conversation about how [Target Company] is planning the operational integration?

**Step 4 — Summary:** 3 personas targeted, 9 emails generated. Urgency: 11 days remaining (URGENT). Strongest entry: CFO with "operational complexity multiplied overnight" angle. Evidence grade: VERIFIED (press release). Note: Account has prior closed-lost deal from 14 months ago — this trigger event may reopen the conversation.

---

### Example 2: New Leadership Hire — Executive from Customer Company

**Context:** Company just hired a new executive from one of your current customers. LinkedIn announcement posted 5 days ago.

**Input:** "[Target Company] just hired a new VP of [Function] from [Customer Company]. Build trigger outbound."

**Step 1 — Classify:** Trigger type: New Leadership Hire. Source: LinkedIn announcement [Verified — LinkedIn post by the new hire]. Event date: 5 days ago. Urgency window: 30-60 days (90-day evaluation window). Days remaining: 55 at peak. Timeliness: URGENT.

**Step 1c — CRM Search:** [Target Company] exists in CRM. No active deal. No contacts. ICP2 fit. The new hire came from [Customer Company] — a reference customer. Their prior email is in CRM from a user group event.

**Step 2 — Event Intelligence Brief:**
- **Implication 1:** The new hire evaluated tools at [Customer Company] — they know your product's value firsthand. Warm lead by definition. [INFERRED from verified hire + CRM data]
- **Implication 2:** New leaders evaluate and change tools in first 90 days — they have mandate to optimize. [INFERRED]
- **Implication 3:** [Target Company]'s operations may be less mature than [Customer Company]'s — they may see gaps immediately. [INFERRED]
- **Implication 4:** They may bring best practices (and vendor preferences) from [Customer Company]. [INFERRED]

**Step 3 — Sequences:** Single-persona sequence targeting the new hire directly. 3 emails.

**[New Hire] — Email 1:**
Subject: Welcome to [Target Company], [Name]

[Name] — congrats on the VP [Function] role at [Target Company]. Having seen what you built at [Customer Company], I imagine you're already assessing how [Target Company] handles [core process] across their [X] regions.

At [Customer Company], your team [key metric]. Curious whether [Target Company]'s current process is giving you that same level of automation.

Would love to reconnect now that you're settling in — even just to compare notes on what's working.

**Step 4 — Summary:** 1 persona targeted, 3 emails generated. Urgency: 55 days remaining (URGENT — but longer window). Strongest entry: Direct reference to their [Customer Company] experience. Evidence grade: VERIFIED (LinkedIn announcement + CRM data). This is the warmest possible trigger — personal relationship + product familiarity.

---

### Example 3: Stacked Triggers — PE Acquisition + Geographic Expansion + New CFO

**Context:** Company received PE investment, announced expansion into 3 new regions, and hired a new CFO — all within the past 30 days.

**Input:** "[Target Company] just got PE backing, they're expanding into [3 new regions], and they hired a new CFO. Build trigger outbound."

**Step 1 — Classify:** Three triggers detected. Applying Stacked Triggers pattern.

| Trigger | Type | Urgency | Days Remaining |
|---------|------|---------|---------------|
| PE Investment | PE Investment / Recapitalization | 14-30 days | 22 |
| Geographic Expansion | Geographic Expansion | 14-30 days | 18 |
| New CFO | New Leadership Hire | 30-60 days | 48 |

Primary trigger (highest urgency): Geographic Expansion (18 days). Secondary: PE Investment. Tertiary: New CFO (longest window, use for follow-up).

**Step 3 — Sequences:** 2 personas (New CFO, Head of [Function]) x 3 emails = 6 emails. Each email uses a different trigger.

**New CFO — Email 1 (Geographic Expansion angle):**
Subject: Operations in [new regions] for [Target Company]

[Name] — congratulations on the CFO role at [Target Company]. With the expansion into [new regions], [Target Company] is adding regions with different operational requirements.

[Specific requirement detail]. Miss it once on a large project and you've [specific consequence].

Worth a quick conversation about how other PE-backed companies handle multi-region operations during expansion?

**New CFO — Email 2 (PE Investment angle — different trigger):**
Subject: Operational automation post-PE investment

With [PE Firm]'s investment, [Target Company] likely has efficiency mandates in the first 100 days. One area that typically surfaces in PE due diligence is operational risk — particularly across multiple regions.

[Reference Customer] standardized operations on a single platform and [key metric]. Their CFO called it "one of the fastest ROI decisions we made."

Happy to share how other PE-backed companies are approaching this.

**Step 4 — Summary:** 2 personas targeted, 6 emails generated. Stacked triggers allow each email to use a different event angle. Strongest entry: New CFO with geographic expansion angle (most time-sensitive). Evidence grade: VERIFIED (all three events confirmed via press releases and LinkedIn).

---

## Common Patterns

### Pattern: Stacked Triggers
**When:** Multiple trigger events occur simultaneously (e.g., PE acquisition + geographic expansion + new CFO).
**Approach:** Classify all triggers. Use the highest-urgency trigger for Email 1, second trigger for Email 2. Each email gets a different event angle. See Example 3 for a detailed walkthrough.

### Pattern: Trigger + Displacement Combo
**When:** Trigger event reveals a competitor contract event (e.g., "switching from [competitor]").
**Approach:** Run trigger event outbound for the time-sensitive sequences, then run `gtm-competitive-displacement` for deeper competitive analysis.

### Pattern: LinkedIn Thought Leadership Trigger
**When:** Executive posts about relevant pain on LinkedIn.
**Approach:** Shortest urgency window (3-7 days). Single-persona sequence targeting the person who posted. Reference their specific post content in Email 1.

### Pattern: Trigger on Closed-Lost Account
**When:** A trigger event occurs at a previously closed-lost account.
**Approach:** Use trigger event outbound for the time-sensitive sequences, but reference the prior relationship. Combine with `gtm-closed-loss-reactivation` intelligence for context on why the deal was lost and what has changed.

---

## Troubleshooting

### "The trigger event is more than 30 days old"
**Solution:** Assess whether the event is still relevant. Acquisitions may still be in integration (relevant for months). Leadership changes have a 90-day window. Flag reduced urgency but proceed if business implications are still active. Adjust email language from "I saw your recent announcement" to "Since your [event] in [month], I imagine your team is now dealing with [implication]."

### "Can't verify the trigger event"
**Solution:** Do not reference unverified events in outbound. If the source is uncertain (rumor, unconfirmed report), note "Unverified" and recommend monitoring until confirmed. Never build sequences around events that might not have happened. Per Epistemic Rules, only VERIFIED events may be referenced in emails.

### "Multiple trigger types apply"
**Solution:** Use the Stacked Triggers pattern above. Classify each independently and use the highest-urgency trigger as the primary angle. Each email in the sequence gets a different trigger angle.

### "Event is verified but implications are speculative"
**Solution:** This is expected. Events are VERIFIED; implications are always INFERRED. Frame implications as questions in the emails: "I imagine this means..." or "Curious how this is affecting..." rather than stating them as fact. Let the prospect confirm or deny your hypothesis.

### "Trigger event reveals the account already uses a competitor"
**Solution:** The trigger creates immediate time-sensitivity, but the competitive angle creates depth. Run trigger event outbound first (speed matters), then run `gtm-competitive-displacement` for deeper competitive positioning. The trigger email gets their attention; the displacement strategy wins the deal.

### "BDR finds a trigger on an account with an active AE deal"
**Solution:** This is valuable intelligence for the AE. Generate the trigger analysis but do not send independent sequences. Deliver to the AE with context: "Trigger event at [account] — [event description]. This may accelerate your deal at [stage]. Recommend referencing the event in your next conversation."

---

## Best Practices

### Do's
- **Act fast** — trigger event response rates drop 80% after the relevance window closes
- **Reference the specific event** — generic "congratulations on the acquisition" isn't enough; cite details
- **Frame urgency genuinely** — connect to real business timing, not artificial pressure
- **Match proof points to trigger type** — acquisition triggers use integration proof points, not speed metrics
- **Grade your evidence** — events are VERIFIED, implications are INFERRED; label accordingly
- **Calculate the urgency window** — know exactly how many days of relevance remain

### Don'ts
- **Don't wait for perfect intelligence** — speed beats depth for trigger events
- **Don't use generic subject lines** — "Following up" destroys the timeliness advantage
- **Don't reference unverified events** — always confirm the trigger happened
- **Don't send trigger sequences on BDR's active AE deals** — coordinate through AE
- **Don't use the same trigger angle twice in a sequence** — each email must use a different implication
- **Don't force a trigger that isn't there** — not all news is a trigger; if the event doesn't connect to product value, skip it

### Quality Checklist
- [ ] Event referenced in every Email 1 with specifics
- [ ] Subject lines reference event (not generic)
- [ ] Event source verified and evidence grade assigned
- [ ] Urgency window calculated with days remaining
- [ ] Urgency is genuine (real business timing, not artificial)
- [ ] Each email uses different angle
- [ ] All emails <= 100 words
- [ ] Proof points match trigger type
- [ ] CRM checked for active deals
- [ ] Role detected and coordination applied
- [ ] Implications labeled as INFERRED (not stated as fact)

---

## Integration with Other Skills

- **`gtm-account-snapshot`** — Use snapshot for context when trigger event arrives on an unknown account.
- **`gtm-competitive-displacement`** — When the trigger is a competitor contract event, run displacement for deeper competitive analysis.
- **`gtm-research-outbound`** — When the trigger is an earnings call, use the earnings mode of research outbound for deeper signal extraction.
- **`gtm-closed-loss-reactivation`** — When a trigger event occurs at a closed-lost account, combine trigger urgency with reactivation intelligence.
- **`gtm-deal-pulse`** — Once a trigger event creates a pipeline opportunity, monitor deal health.
- **`gtm-daily-prospecting`** — Trigger events can be surfaced during daily prospecting routines.

---

## Changelog

### Version 1.1.0 (2026-03-04)
- Added Epistemic Rules section with evidence grading (VERIFIED / INFERRED / UNVERIFIED), timeliness rules, and urgency window calculation methodology
- Added Trigger Classification Decision Tree for disambiguating ambiguous events
- Expanded Event-to-Value Mapping with PE Investment and Large Contract Win subsections
- Added PE Investment and Large Contract Win proof points to proof point table
- Expanded Example 1 with full step-by-step detail including CRM search, business implications with evidence grades, email sample, and closed-lost account note
- Expanded Example 2 with CRM data integration, warm lead analysis from customer company, and detailed email sample
- Added Example 3 demonstrating Stacked Triggers pattern with three simultaneous triggers and multi-angle email sequence
- Added Step 1d (Timeliness Validation) to workflow with URGENT / CLOSING / STALE / EXPIRED assessment
- Added 3 new troubleshooting entries (speculative implications, competitor discovery from trigger, BDR + active AE deal)
- Added Trigger on Closed-Lost Account pattern
- Expanded Best Practices with evidence grading and urgency window calculation guidance
- Updated quality checklist with evidence grading and timeliness requirements

### Version 1.0.0 (2026-03-04)
- Initial release
- Generalized via Client Profile block with placeholder defaults
- Preserved 9 trigger types, urgency windows, event-to-value mapping, and 3-step rapid sequences
- Added stacked triggers and LinkedIn thought leadership patterns
- Multi-format artifact generation
