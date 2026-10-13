---
name: gtm-research-outbound
description: "Deep-research POV brief and outbound package from public filings (10-K), private company intelligence, or quarterly earnings calls. Generates ICP qualification, signal mapping, quantified financial wedge, persona-tailored email sequences, and single-page outbound cheatsheet"
version: 1.3.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
tags: [research-outbound, 10k-analysis, earnings-call, private-company, pov-brief, enterprise-prospecting, persona-sequences]
requires:
  skills: []
---

# Research-Driven Outbound

## Overview

Deep-research outbound package that analyzes a company through one of three intelligence lenses: public company 10-K filings, private company web/industry research, or quarterly earnings call transcripts. Produces ICP qualification, signal-to-value mapping, a quantified financial wedge, persona-tailored email sequences, and a single-page outbound cheatsheet. Best for high-value enterprise prospecting where depth justifies the investment.

**Core Principle:** Every claim must be sourced and labeled. Research depth drives outbound quality. The deeper the intelligence, the more specific and compelling the sequences.

---

## Role

You are a **senior enterprise researcher and POV writer for a vertical SaaS company**, not a template maker. You analyze deep company intelligence (10-K filings, private company research, or earnings calls), extract verified facts tied to product value, quantify financial wedges with evidence, and write persona-tailored outbound sequences backed by specifics. Everything company-specific (the ICP, the competitors, the proof points) comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Company name | ✅ Required | The account to research |
| Research type | ✅ Required | 10k_filing / private_company / earnings_call. Determines intelligence source and sequence depth |
| Intelligence source | ✅ Required | The 10-K filing content, private company research, or earnings transcript |

**Role detection:** From CRM. Used to shape recommendations. Fallback: Ask "Are you a BDR or AE?"

---

## Output Contract

Every run produces a **research-backed outbound package with the same structure, in the same order**. The content changes per company and research type. The layout never does.

Core commitments: **ICP verdict**, **signal mapping**, **quantified financial wedge** (when data supports it), **POV brief**, **persona-tailored email sequences**, and **intelligence appendix**. These are organized into 8 fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| ICP Definitions | Qualification gate (GREENLIGHT / MANUAL REVIEW / DISQUALIFY) and market/geographic tiers |
| Qualification Zones | The zone column of the signal map (Step 4) and the zone verdict rule (Step 3) |
| Buyer Personas | Persona-tailored sequences (5 personas x up to 4 emails per research type) |
| Value Propositions | Connecting extracted signals to product capability |
| Proof Points | Selecting reference customers matched to prospect vertical and persona |
| Competitive Landscape | Objection handling and competitive positioning |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your research frameworks and evidence standards. The structures below are the skill's defaults. Use them as-is unless `{Client Profile}` names different frameworks.

### Research Type Selection

This skill operates in three modes based on the intelligence source. Select the research type based on available intelligence and desired sequence depth:

| Research Type | Best For | Sequence Depth | Word Limit | Relevance Window |
|--------------|---------|----------------|------------|-----------------|
| **10-K Filing** | Public companies. Annual deep-dive | 5 personas × 4 emails (20) | ≤120 words | Months |
| **Private Company** | Private companies. Multi-source research | 5 personas × 4 emails (20) | ≤120 words | Months |
| **Earnings Call** | Public companies. Quarterly signals | 2-3 personas × 2 emails (4-6) | ≤100 words | 7-14 days |

### Revenue Estimation Methods

When revenue is unavailable for private companies, use these formulas to estimate:

| Method | Formula | Label |
|--------|---------|-------|
| Employee benchmark | Employees × $[range] per employee | `[Estimated: employee benchmark]` |
| Branch count proxy | Branches × $[range] per branch | `[Estimated: branch proxy]` |
| Industry ranking | Cross-reference industry top lists | `[Estimated: industry ranking]` |
| PE acquisition press | Revenue language in announcement | `[Estimated: PE press]` |

---

## Quick Reference

**Use this skill when:**
- Prospecting a high-value enterprise account with public filings available
- Researching a private company for strategic outbound
- Capitalizing on a quarterly earnings call with time-sensitive signals
- Need persona-tailored sequences backed by verified company intelligence

**Don't use when:**
- You need a quick snapshot for volume prospecting (use `gtm-account-snapshot`)
- The account has a known incumbent (use `gtm-competitive-displacement`)
- A trigger event just happened (use `gtm-trigger-event-outbound`)
- The account is a closed-lost deal (use `gtm-closed-loss-reactivation`)

**User roles:** BDR, AE
**Expected time:** 20-45 minutes per account

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` (BDR / AE)

**Role-aware framing:**
- **BDR:** CTAs frame as meeting-booking. If active AE deal exists, share analysis with AE instead.
- **AE:** CTAs frame as deal-advancing. Use intelligence to deepen engagement.

---

### Step 1: Gather Inputs + Check CRM

#### 1a. Confirm Inputs (varies by research type)

**10-K Filing:**
- Company name and ticker
- Fiscal year and filing date
- 10-K content (pasted or key sections)

**Private Company:**
- Company name
- What they do (if known)
- Any known details (HQ, size, vertical, PE ownership)

**Earnings Call:**
- Company name and ticker
- Quarter and fiscal year
- Earnings call date
- Transcript content (pasted or key sections)

#### 1b. Search CRM
Pull existing intelligence: account record, contacts, deal stage, BDR Owner, engagement history.

**Active Deal Guard:** If `user_role = BDR` and active AE deal exists: "Active deal owned by [AE name] at [Stage]. Share analysis with AE. Do not send sequences independently."

---

### Step 2: Build Intelligence Profile

#### For 10-K Filings: Verified Fact Bank
Scan required sections (Item 1, 1A, 3, 7, 9A). Extract facts with citations:
```
- [Fact] (10-K: Item X, Section, PDF p. ##)
```

#### For Private Companies: Verified Intelligence Profile
Research from all available sources:

| Source | What to Look For |
|--------|-----------------|
| Company website | About, leadership, locations, services, history, careers |
| News/press releases | Acquisitions, expansions, hires, awards, milestones |
| LinkedIn | Employee count, growth, headquarters, specialties |
| Job postings | Roles relevant to your product's value (signals of pain) |
| Industry databases | Rankings, trade association memberships |
| PE/M&A signals | Ownership structure, recent acquisitions |
| Trade publications | Industry mentions, project wins |
| Regulatory/licensing | Active licenses by region (geographic footprint) |

Tag every fact: `[Verified: Source]`, `[Inferred: Basis]`, `[Estimated: Method]`.

#### For Earnings Calls: Signal Extraction
Scan the full transcript for priority signals:

| Signal Category | What to Look For | Product Connection |
|----------------|-----------------|-------------------|
| Working Capital | DSO, A/R trends, cash conversion | [Your relevant value prop] |
| Bad Debt/Credit Loss | Allowance changes, write-offs, collections | [Your relevant value prop] |
| Operational Efficiency | Headcount, SG&A optimization | [Your relevant value prop] |
| Growth/Expansion | New markets, acquisitions, organic growth | [Your relevant value prop] |
| M&A Activity | Acquisitions, integration commentary | [Your relevant value prop] |
| ERP/Systems | Tech investments, consolidation | [Your relevant value prop] |
| Margin Pressure | Gross margin, cost inflation | [Your relevant value prop] |
| Guidance Changes | Lowered outlook, revised targets | [Your relevant value prop] |

Extract 6-10 signals ranked by urgency. Format:
```
- Signal: [Category]
- Quote/Paraphrase: "[What was said]"
- Speaker: [Name, Title]
- Section: [Prepared Remarks / Q&A]
- Product Connection: [How this connects to value]
- Urgency: [High / Medium / Low]
```

---

### Step 3: ICP Qualification Gate

Score against `{Client Profile: ICP Definitions}`.

**GREENLIGHT**. Confirmed fit with evidence. Proceed with full sequences.
**MANUAL REVIEW**. Plausible fit, data gaps. Note specific unknowns.
**DISQUALIFY**. Does not match ICP. Explain why.

Output: Verdict + 3-6 bullet reasons, each with source tags.

---

### Step 4: Map Intelligence to Company Profile

Map extracted signals/facts to company characteristics from `{Client Profile: ICP Definitions}` (market and geographic tiers) and `{Client Profile: Qualification Zones}` (the zone column below).

Create a signal mapping table:

| Intelligence Signal | Why It Matters | Qualification Zone | Value Prop | Discovery Question | Source |
|---------------------|---------------|-------------------|-----------|-------------------|--------|

Populate with 6-10 rows. Each row must have a source tag.

---

### Step 5: Build Quantified Wedge

Only when intelligence supports the numbers. Label all calculations.

| Data Available | Calculation | Label |
|---------------|-------------|-------|
| Revenue known | 1 day of sales = Revenue / 365 | `[From filing/research]` |
| DSO disclosed | Cite directly + typical improvement benchmark | `[Product benchmark]` |
| A/R balance | Working capital exposure calculation | `[Illustrative]` |
| Employee count | Team size estimate from benchmarks | `[Estimated]` |
| Branch count | Volume estimate from branch count | `[Estimated]` |

**Never claim savings as guaranteed.** Frame as: "Customers typically see..." or "Companies of similar size typically..."

---

### Step 6: Write POV Brief

**Max 350-500 words. Skimmable. Every claim sourced.**

1. **Company Context** (2-3 bullets): What they do, segment, ownership, footprint
2. **Why They Should Care** (3-5 bullets): Connect profile to product value
3. **Risks / Complexity Signals** (3-5 bullets): Multi-region exposure, manual processes, growth strain
4. **Fit Verdict**: GREENLIGHT / MANUAL REVIEW / DISQUALIFY with reasons
5. **POV Statement** (6-8 sentences): Lead with notable attribute, connect to complexity, wedge, value prop, close with ask

---

### Step 7: Generate Persona Email Sequences

#### 10-K and Private Company: All 5 personas × 4 steps (20 emails)

| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | POV + wedge | Most compelling company-specific intelligence |
| **Email 2** | Complexity / risk | Different anchor: geographic, integration, operational |
| **Email 3** | Process / efficiency | Industry trend, operational pain hypothesis |
| **Email 4** | Breakup + validation | Soft close with specific question |

Rules: ≤120 words, different intelligence anchor per email, citation in first line, max 1 proof point per email.

#### Earnings Call: 2-3 personas × 2 steps (4-6 emails)

| Step | Timing | Angle |
|------|--------|-------|
| **Email 1** | Within 3-5 days | Most relevant earnings signal + product connection |
| **Email 2** | Day 7-10 | Different signal + proof point + soft close |

Rules: ≤100 words (urgency demands brevity), subject line references earnings, citation in first line.

**Persona selection for earnings:** Match to strongest signal category using the trigger-persona mapping in `{Client Profile: Buyer Personas}`.

#### After Each Persona Pack, Include:
- Persona hook focus (1 line)
- Best 2 discovery questions (2 bullets, grounded in intelligence)

---

### Step 8: Intelligence Appendix

**Top 8 Intelligence Items:**
```
1. [Finding] ([Source, Confidence Level])
...
8. [Finding] ([Source, Confidence Level])
```

**Research Gaps:** 2-4 unknowns that would strengthen outreach if discovered.

---

### Step 9: Summary Report

1. **Company**: Name, HQ, ownership, revenue, segment
2. **Research Type**: 10-K / Private Company / Earnings Call
3. **ICP Verdict**: GREENLIGHT / MANUAL REVIEW / DISQUALIFY + top 3 reasons
4. **Quantified Wedge**: Strongest financial hook, or "Insufficient data"
5. **CRM Status**: Pipeline activity + known contacts
6. **Geographic Exposure**: Regions mapped to relevant tiers (10-K/Private only)
7. **Relevance Window**: Days remaining (Earnings only)
8. **Sequences Generated**: [Count] personas × [steps] emails
9. **Personalized Contacts**: Which emails addressed to known individuals
10. **Strongest Entry Point**: Persona + email with highest-impact opening
11. **User Role**: BDR / AE
12. **Coordination Note**: Active deal guidance if applicable
13. **Research Gaps**: Top 3 unknowns for discovery

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default): `[COMPANY]_Research_Outbound.md`
- **Option B: HTML**: Styled cheatsheet with color-coded sections
- **Option C: PDF**: Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)

**For 10-K / Private Company:**
1. Company Snapshot: Key metrics from intelligence profile
2. Geographic/Market Exposure: Regions mapped to relevant tiers
3. Key Personas: CRM contacts + prioritization
4. Pain Points / Signals: 6 hooks from signal mapping as talk tracks
5. Discovery Questions: Persona-organized, intelligence-grounded
6. Value Props: Wedge + proof points matched to profile
7. Objection Handling: CRM intel + common objections
8. Call Flow: 5-step talk track using research artifacts

**For Earnings Calls:**
1. Earnings Snapshot: Quarter, revenue, key metrics, relevance window
2. Top Signals: Ranked by urgency with speaker attribution
3. Key Personas: Signal-matched from CRM
4. Earnings Hooks: 6 talk-track-ready signal hooks
5. Discovery Questions: Earnings-grounded, not generic
6. Value Props: Signal-matched wedge
7. Objection Handling: Earnings-aware rebuttals
8. Call Flow: Earnings-led 5-step talk track

**Earnings-specific:** Include TIMELINESS BANNER at top showing days since call.

---

## Examples

### Example 1: Private Company Research (Saltmarsh Heritage Group, MANUAL REVIEW)

**Context:** Research-driven outbound to Saltmarsh Heritage Group, a family-owned group with 5 sites (2 cemeteries, 3 funeral homes) and no public filings. Its annual owner letter, posted on the company site, says all five sites move to one system in 2027. The CFO, Hector Ruiz, approves budget. This is the one account in the cast whose research starts from an owner letter.

**Input:** "Build a research outbound package for Saltmarsh Heritage Group from its owner letter, with sequences and a cheatsheet."

**Process:** Intelligence profile: owner letter says all five sites move to one system in 2027 `[Verified: owner letter on company site]`. Five sites, with 2 cemeteries and 3 funeral homes `[CRM]`. Three funeral homes run pre-need counselors `[CRM]`. Ownership is family `[CRM]`. The CFO approves budget `[CRM]`.

Gate: The group sits at the top of ICP3 (four to ten sites). The decision runs through a CFO, which rates Zone 3 LOW in `{Client Profile: Qualification Zones}`. Zone 5 HIGH is plausible from the owner update (illustrative rating). The verdict rule does not reach GREENLIGHT with a must-have zone at LOW, and it does not reach DISQUALIFY, so the verdict is **MANUAL REVIEW**. The CFO gate and the 6 to 9 month cycle are the open items.

**Output:** Intelligence profile with source tags. POV brief built on the single-system plan. 20 persona emails (5 personas x 4), with Email 1 to the CFO shown below. Research gap: which system, and when the records move.

> **Subject:** One system across five sites in 2027
>
> Hector,
>
> Your owner letter says all five Saltmarsh sites move to one system in 2027. Two cemeteries and three funeral homes on one system is a records question before it is a software question. Which plot records and pre-need leads move first?
>
> Your pre-need counselors at three funeral homes already generate leads. Where do those leads land today?
>
> Worth 20 minutes to map it before the move?

### Example 2: Active Deal Guard (Brackhaven Memorial Gardens)

**Context:** A BDR asks for a research outbound package on Brackhaven Memorial Gardens. The account is ACTIVE at Stage 5 Negotiate, and an AE owns the deal. The profile lists Brackhaven as the flagship deal.

**Input:** "Build a research outbound package for Brackhaven Memorial Gardens."

**Step 0: Role Detection** User is BDR. CRM check: active AE deal at Stage 5 Negotiate.

**Step 1b: Active Deal Guard** "Active deal owned by the account AE at Stage 5 Negotiate. Share analysis with AE. Do not send sequences independently."

**Intelligence (for the AE, not for outbound):** Two sites, 11,000 plots, paper plat maps `[CRM]`. One double sale in 24 months (illustrative) `[CRM]`. Legacy on-premise system from Oldgate, renewal March 2027 `[CRM]`. Stonemark mapping was also evaluated `[CRM]`. The owner retires within 3 years (illustrative) `[CRM]`. The GM is the champion and the operations director is skeptical of tablets `[CRM]`.

**Output:** Analysis and verdict for the AE only. No sequences. Verdict: GREENLIGHT (the cast verdict). Coordination note: "The March 2027 Oldgate renewal is the timing hook. The AE should lead it, because BDR outreach to a deal in Negotiate would cross the AE's conversation."

### Example 3: Insufficient Intelligence Fallback (Tamsin Vale Cemetery)

**Context:** Research outbound on Tamsin Vale Cemetery. It is a private, one-site cemetery with little public information: no owner letter, no filing, and no news found.

**Input:** "Build a research-driven outbound package for Tamsin Vale Cemetery."

**Process:** Intelligence available: 4,200 plots, paper plat maps, and one binder per section `[CRM]`. Two double sales in 2 years (illustrative) `[CRM]`. Web and news search found nothing `[Unknown]`. The Zone 1 signal is HIGH. The other zones are not scored, because the sources do not say who signs or whether pre-need sales happen.

**Gate:** Insufficient Intelligence Fallback. Classify as **MANUAL REVIEW**. One HIGH zone is not enough for a full package. Do not write a POV brief from one strong fact.

**Output:** What is available, plus the research actions: find the decision-maker (Zone 3), confirm pre-need sales (Zone 2), and check what staff already use day to day (Zone 4). Recommend `gtm-account-snapshot` as the faster route. No sequences are generated at this stage, so the output has 0 emails.

---

## Common Patterns

### Pattern: 10-K vs. Earnings Selection
**When:** Public company with both annual filing and recent earnings call available.
**Approach:** Use earnings call for time-sensitive outbound (7-14 day window). Use 10-K for deeper strategic outbound (months of relevance). Both can be run on the same company at different times.

### Pattern: Active Deal Guard (BDR)
**When:** `user_role = BDR` and the account has an active AE deal.
**Action:** Generate the analysis but add coordination guidance. BDR should share intelligence with AE rather than sending independent sequences.

### Pattern: Insufficient Intelligence Fallback
**When:** Private company research yields too little intelligence for full qualification.
**Action:** Deliver what's available, classify as MANUAL REVIEW, list specific research actions needed, and recommend `gtm-account-snapshot` as a faster alternative.

---

## Troubleshooting

### "10-K content is too long to process"
**Solution:** Focus on Items 1 (Business), 1A (Risk Factors), 7 (MD&A), and 9A (Controls). These contain 90% of relevant intelligence. Skip financial statements tables.

### "Earnings call transcript not available yet"
**Solution:** Use the earnings press release as a substitute. It contains key metrics but lacks Q&A analyst questions. Note reduced signal depth in the output.

### "Private company has almost no public information"
**Solution:** Classify as MANUAL REVIEW. List specific research gaps. Recommend alternative approaches: LinkedIn deep-dive, trade association membership lists, job posting analysis, regulatory/licensing databases.

### "Revenue estimation methods give conflicting results"
**Solution:** Report the range from multiple methods. Note the variance and flag confidence as MEDIUM. Example: "Revenue estimated at $80-150M (employee benchmark: $100M, branch proxy: $80M, industry ranking: $150M)."

---

## Best Practices

### Do's
- **Source-tag every claim**: `[Verified: 10-K Item 7]`, `[Inferred: branch locations]`, `[Estimated: employee benchmark]`, `[Product benchmark]`
- **Use different intelligence anchors per email**: no repeating the same signal across a persona's sequence
- **Match proof points to vertical**: use relevant customer stories, not random ones
- **For earnings calls, act fast**: the 7-14 day window is real. Speed beats perfection

### Don'ts
- **Don't fabricate company-specific data**: if you can't verify it, don't state it
- **Don't recycle old earnings data**: signals must be from the current quarter
- **Don't claim savings as guaranteed**: frame as typical outcomes or benchmarks
- **Don't skip the POV brief**: it forces synthesis of raw intelligence into a narrative

### Quality Checklist
- [ ] Every claim has a source tag
- [ ] Confidence levels honest (`[Estimated]` and `[Inferred]` labeled)
- [ ] No fabricated details. Unknown = discovery question
- [ ] Product claims labeled appropriately
- [ ] POV brief is company-specific (name not swappable)
- [ ] Proof points match vertical
- [ ] Each email has unique anchor (no repeated signals per persona)
- [ ] All emails within word limit (120 for 10-K/private, 100 for earnings)
- [ ] Research gaps documented
- [ ] Role detected and coordination guidance applied

---

## Integration with Other Skills

- **`gtm-account-qualification`**: Run qualification first for net-new accounts. Use research outbound for GREENLIGHT accounts.
- **`gtm-account-snapshot`**: Faster alternative for volume prospecting. Use research outbound when depth justifies the investment.
- **`gtm-competitive-displacement`**: When research reveals a specific incumbent, run displacement sequences.
- **`gtm-trigger-event-outbound`**: When earnings or research surface a time-sensitive event, pivot to trigger-based outbound.
- **`gtm-deal-pulse`**: Once an opportunity is created, switch to deal health monitoring.

---

## Changelog

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Persona count corrected to 5 (20 emails per 10-K or private package)

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying an embedded Client Profile block (one profile powers every skill)
- Framework machinery (research type selection, revenue estimation methods) moved to an explicit Methodology section: `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release: merged from three research intelligence workflows (10-K POV, Private Company POV, Earnings Call)
- Unified via `research_type` parameter: 10k_filing, private_company, earnings_call
- Generalized via Client Profile block with placeholder defaults
- Preserved all scoring frameworks, signal extraction patterns, and sequence architectures
- Added revenue estimation methods for private companies
- Multi-format artifact generation
