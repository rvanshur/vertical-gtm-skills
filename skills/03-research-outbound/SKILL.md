---
name: gtm-research-outbound
description: "Deep-research POV brief and outbound package from public filings (10-K), private company intelligence, or quarterly earnings calls. Generates ICP qualification, signal mapping, quantified financial wedge, persona-tailored email sequences, and single-page outbound cheatsheet"
version: 1.0.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-03-04
tags: [research-outbound, 10k-analysis, earnings-call, private-company, pov-brief, enterprise-prospecting, persona-sequences]
requires:
  skills: []
---

# Research-Driven Outbound

## Overview

Deep-research outbound package that analyzes a company through one of three intelligence lenses: public company 10-K filings, private company web/industry research, or quarterly earnings call transcripts. Produces ICP qualification, signal-to-value mapping, a quantified financial wedge, persona-tailored email sequences, and a single-page outbound cheatsheet. Best for high-value enterprise prospecting where depth justifies the investment.

**Core Principle:** Every claim must be sourced and labeled. Research depth drives outbound quality — the deeper the intelligence, the more specific and compelling the sequences.

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
- Key indicator: [What makes them a fit]

**ICP2: [Expansion Segment Name]**
- [Description of secondary segment]
- Revenue threshold: [Minimum viable size]
- Key indicator: [What makes them a fit]
- [Priority qualifier, e.g., PE-backed is highest priority]

**No Fit**
- [Describe who is NOT a fit]

### Buyer Personas
| # | Persona | Hook Focus |
|---|---------|------------|
| 1 | **[Title]** | [Top priorities and pain themes] |
| 2 | **[Title]** | [Top priorities and pain themes] |
| 3 | **[Title]** | [Top priorities and pain themes] |
| 4 | **[Title]** | [Top priorities and pain themes] |
| 5 | **[Title]** | [Top priorities and pain themes] |
| 6 | **[Title]** | [Top priorities and pain themes] |

### Qualification Zones
1. [Zone 1: Primary segment description]
2. [Zone 2: Operational signal]
3. [Zone 3: Geographic or regulatory signal]
4. [Zone 4: Scale threshold]
5. [Zone 5: Process maturity signal]

### Value Propositions
1. [Value prop 1]
2. [Value prop 2]
3. [Value prop 3]
4. [Value prop 4]
5. [Value prop 5]

### Proof Points
| Context | Best Proof Point |
|---------|-----------------|
| [Profile 1] | [Customer]: [Metric] |
| [Profile 2] | [Customer]: [Metric] |
| [Profile 3] | [Customer]: [Metric] |
| [Profile 4] | [Customer]: [Metric] |
| [Profile 5] | [Customer]: [Metric] |

### Industry Context (weave in where relevant)
- [Macro trend 1]
- [Macro trend 2]
- [Macro trend 3]
- [Macro trend 4]
- [Macro trend 5]

### Competitive Landscape
| Competitor | Type | Your Advantage |
|-----------|------|---------------|
| [Competitor 1] | [Category] | [Why you win] |
| [Competitor 2] | [Category] | [Why you win] |
| [Competitor 3] | [Category] | [Why you win] |
| Status Quo / Manual | Do nothing | [Cost of inaction] |

### Revenue Estimation Methods (for private companies)
| Method | Formula | Label |
|--------|---------|-------|
| Employee benchmark | Employees × $[range] per employee | `[Estimated — employee benchmark]` |
| Branch count proxy | Branches × $[range] per branch | `[Estimated — branch proxy]` |
| Industry ranking | Cross-reference industry top lists | `[Estimated — industry ranking]` |
| PE acquisition press | Revenue language in announcement | `[Estimated — PE press]` |

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

## Research Type Selection

This skill operates in three modes based on the intelligence source:

| Research Type | Best For | Sequence Depth | Word Limit | Relevance Window |
|--------------|---------|----------------|------------|-----------------|
| **10-K Filing** | Public companies; annual deep-dive | 6 personas × 4 emails (24) | ≤120 words | Months |
| **Private Company** | Private companies; multi-source research | 6 personas × 4 emails (24) | ≤120 words | Months |
| **Earnings Call** | Public companies; quarterly signals | 2-3 personas × 2 emails (4-6) | ≤100 words | 7-14 days |

Select the research type based on available intelligence. If multiple sources are available, the 10-K provides the deepest analysis; earnings calls provide the most time-sensitive signals.

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

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

**Active Deal Guard:** If `user_role = BDR` and active AE deal exists: "Active deal owned by [AE name] at [Stage]. Share analysis with AE — do not send sequences independently."

---

### Step 2: Build Intelligence Profile

#### For 10-K Filings — Verified Fact Bank
Scan required sections (Item 1, 1A, 3, 7, 9A). Extract facts with citations:
```
- [Fact] — (10-K: Item X, Section, PDF p. ##)
```

#### For Private Companies — Verified Intelligence Profile
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

Tag every fact: `[Verified — Source]`, `[Inferred — Basis]`, `[Estimated — Method]`.

#### For Earnings Calls — Signal Extraction
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

**GREENLIGHT** — Confirmed fit with evidence. Proceed with full sequences.
**MANUAL REVIEW** — Plausible fit, data gaps. Note specific unknowns.
**DISQUALIFY** — Does not match ICP. Explain why.

Output: Verdict + 3-6 bullet reasons, each with source tags.

---

### Step 4: Map Intelligence to Qualification Zones

Map extracted signals/facts to `{Client Profile: Qualification Zones}`.

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

1. **Company Context** (2-3 bullets) — What they do, segment, ownership, footprint
2. **Why They Should Care** (3-5 bullets) — Connect profile to product value
3. **Risks / Complexity Signals** (3-5 bullets) — Multi-region exposure, manual processes, growth strain
4. **Fit Verdict** — GREENLIGHT / MANUAL REVIEW / DISQUALIFY with reasons
5. **POV Statement** (6-8 sentences) — Lead with notable attribute, connect to complexity, wedge, value prop, close with ask

---

### Step 7: Generate Persona Email Sequences

#### 10-K and Private Company: All 6 personas × 4 steps (24 emails)

| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | POV + wedge | Most compelling company-specific intelligence |
| **Email 2** | Complexity / risk | Different anchor — geographic, integration, operational |
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
1. [Finding] — [Source, Confidence Level]
...
8. [Finding] — [Source, Confidence Level]
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
- **Option A: Markdown** (default) — `[COMPANY]_Research_Outbound.md`
- **Option B: HTML** — Styled cheatsheet with color-coded sections
- **Option C: PDF** — Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)

**For 10-K / Private Company:**
1. Company Snapshot — Key metrics from intelligence profile
2. Geographic/Market Exposure — Regions mapped to relevant tiers
3. Key Personas — CRM contacts + prioritization
4. Pain Points / Signals — 6 hooks from signal mapping as talk tracks
5. Discovery Questions — Persona-organized, intelligence-grounded
6. Value Props — Wedge + proof points matched to profile
7. Objection Handling — CRM intel + common objections
8. Call Flow — 5-step talk track using research artifacts

**For Earnings Calls:**
1. Earnings Snapshot — Quarter, revenue, key metrics, relevance window
2. Top Signals — Ranked by urgency with speaker attribution
3. Key Personas — Signal-matched from CRM
4. Earnings Hooks — 6 talk-track-ready signal hooks
5. Discovery Questions — Earnings-grounded, not generic
6. Value Props — Signal-matched wedge
7. Objection Handling — Earnings-aware rebuttals
8. Call Flow — Earnings-led 5-step talk track

**Earnings-specific:** Include TIMELINESS BANNER at top showing days since call.

---

## Examples

### Example 1: 10-K Analysis — Public Enterprise Account

**Context:** Enterprise prospecting into a public company in your vertical.

**Input:** "Run full 10-K outbound analysis for [Target Company] ([TICKER]) based on their FY2025 10-K."

**Process:** 10-K extraction reveals $7.6B revenue, 320+ locations, 48 states, DSO of 42 days, $1.2B A/R balance, recent acquisition. Signal mapping identifies 8 signals across all 5 Qualification Zones. Quantified wedge: 1 day of sales = $20.8M.

**Output:** Full POV brief, 24 persona email sequences, evidence appendix, 8-section cheatsheet. Verdict: GREENLIGHT — HIGH confidence. Strongest entry: VP Finance with DSO/working capital angle.

### Example 2: Private Company Research — PE-Backed Account

**Context:** Strategic outbound to a PE-backed company with no public filings.

**Input:** "Build a POV outbound campaign for [Target Company] with sequences and a cheatsheet."

**Process:** Web research reveals $5B+ revenue [Estimated — employee benchmark], PE-backed, 24 offices across 12 states. LinkedIn shows 6,000+ employees. No current vendor discoverable. ICP2 GREENLIGHT.

**Output:** Intelligence profile with source tags, POV brief, 24 persona emails, PDF cheatsheet. Strongest entry: CFO with PE integration angle.

### Example 3: Earnings Call — Quarterly Signals

**Context:** Time-sensitive outbound after a public company's quarterly earnings call.

**Input:** "Analyze [Target Company]'s Q4 2025 earnings call and build outbound sequences."

**Process:** Transcript analysis extracts 8 signals. Top 3: CFO commentary on "working capital discipline" (High urgency), DSO improvement targets mentioned by analysts (High), geographic expansion into 3 new states (Medium). Relevance window: 11 days remaining.

**Output:** Signal extraction, rapid-response sequences for CFO and VP Finance (4 emails), earnings cheatsheet with timeliness banner. Strongest entry: CFO with working capital signal.

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
- **Source-tag every claim** — `[Verified — 10-K Item 7]`, `[Inferred — branch locations]`, `[Estimated — employee benchmark]`, `[Product benchmark]`
- **Use different intelligence anchors per email** — no repeating the same signal across a persona's sequence
- **Match proof points to vertical** — use relevant customer stories, not random ones
- **For earnings calls, act fast** — the 7-14 day window is real; speed beats perfection

### Don'ts
- **Don't fabricate company-specific data** — if you can't verify it, don't state it
- **Don't recycle old earnings data** — signals must be from the current quarter
- **Don't claim savings as guaranteed** — frame as typical outcomes or benchmarks
- **Don't skip the POV brief** — it forces synthesis of raw intelligence into a narrative

### Quality Checklist
- [ ] Every claim has a source tag
- [ ] Confidence levels honest (`[Estimated]` and `[Inferred]` labeled)
- [ ] No fabricated details — Unknown = discovery question
- [ ] Product claims labeled appropriately
- [ ] POV brief is company-specific (name not swappable)
- [ ] Proof points match vertical
- [ ] Each email has unique anchor (no repeated signals per persona)
- [ ] All emails within word limit (120 for 10-K/private, 100 for earnings)
- [ ] Research gaps documented
- [ ] Role detected and coordination guidance applied

---

## Integration with Other Skills

- **`gtm-account-qualification`** — Run qualification first for net-new accounts; use research outbound for GREENLIGHT accounts.
- **`gtm-account-snapshot`** — Faster alternative for volume prospecting. Use research outbound when depth justifies the investment.
- **`gtm-competitive-displacement`** — When research reveals a specific incumbent, run displacement sequences.
- **`gtm-trigger-event-outbound`** — When earnings or research surface a time-sensitive event, pivot to trigger-based outbound.
- **`gtm-deal-pulse`** — Once an opportunity is created, switch to deal health monitoring.

---

## Changelog

### Version 1.0.0 (2026-03-04)
- Initial release — merged from three research intelligence workflows (10-K POV, Private Company POV, Earnings Call)
- Unified via `research_type` parameter: 10k_filing, private_company, earnings_call
- Generalized via Client Profile block with placeholder defaults
- Preserved all scoring frameworks, signal extraction patterns, and sequence architectures
- Added revenue estimation methods for private companies
- Multi-format artifact generation
