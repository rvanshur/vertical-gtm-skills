---
name: gtm-account-snapshot
description: "BDR daily driver — rapid account research, ICP quick-score, persona-mapped contact prioritization, pain hypothesis generation, 3-step email sequences, cold call prep sheet, and single-page outbound cheatsheet"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-03-04
tags: [account-snapshot, bdr-daily-driver, outbound, prospecting, cold-call-prep, email-sequences, cheatsheet]
requires:
  skills: []
---

# Account Snapshot Outbound

## Overview

Rapid account research and outbound package for a single account. Pulls CRM data, scores ICP fit, maps contacts to buying personas, generates pain hypotheses matched to core buyer pains, produces 3-step email sequences, and builds a cold call prep sheet with opener, talk track, voicemail, and objection rebuttals. Designed to be fast enough to run between calls — the BDR daily driver.

**Core Principle:** Speed + specificity. Every output is actionable within minutes, not hours. Research depth is calibrated for volume prospecting, not deep-dive analysis.

---

## Client Profile

> **Configure this block for your company.** Replace the placeholder values below with your actual company data, ICP definitions, personas, and competitive landscape.

### Company
- **Name:** [Your Company]
- **Industry:** [Your vertical] (B2B SaaS)
- **Product:** [One-line product description]

### ICP Quick-Score Dimensions
| Signal | Scoring |
|--------|---------|
| [Primary fit signal]? | Yes / Partial / No |
| [Geographic/scale signal]? | Yes (X regions) / Single region |
| [Regulatory or complexity signal]? | Tier 1 / Tier 2 / Minimal |
| Scale (revenue/volume)? | Enterprise / Mid-Market / SMB |
| [Team complexity signal]? | Dedicated team / Small team / Unknown |

### Core Pain Points
| # | Pain Point | What to Listen For | Business Impact |
|---|-----------|-------------------|----------------|
| 1 | **[Pain]** | [Signals] | [Impact] |
| 2 | **[Pain]** | [Signals] | [Impact] |
| 3 | **[Pain]** | [Signals] | [Impact] |
| 4 | **[Pain]** | [Signals] | [Impact] |
| 5 | **[Pain]** | [Signals] | [Impact] |

### Buyer Personas
| # | Persona | Hook Focus |
|---|---------|------------|
| 1 | **[Title]** | [Top priorities and pain themes] |
| 2 | **[Title]** | [Top priorities and pain themes] |
| 3 | **[Title]** | [Top priorities and pain themes] |
| 4 | **[Title]** | [Top priorities and pain themes] |

### Value Propositions
1. [Value prop 1]
2. [Value prop 2]
3. [Value prop 3]
4. [Value prop 4]
5. [Value prop 5]

### Proof Points
| Prospect Profile | Best Proof Point |
|-----------------|-----------------|
| [Profile 1] | [Customer]: [Metric] |
| [Profile 2] | [Customer]: [Metric] |
| [Profile 3] | [Customer]: [Metric] |

### Competitive Landscape
| Competitor | Type | Your Advantage |
|-----------|------|---------------|
| [Competitor 1] | [Category] | [Why you win] |
| [Competitor 2] | [Category] | [Why you win] |
| [Competitor 3] | [Category] | [Why you win] |
| Status Quo / Manual | Do nothing | [Cost of inaction] |

### Qualification Zones
1. [Zone 1: Primary segment description]
2. [Zone 2: Operational signal]
3. [Zone 3: Geographic or regulatory signal]
4. [Zone 4: Scale threshold]
5. [Zone 5: Process maturity signal]

---

## Quick Reference

**Use this skill when:**
- Preparing for a prospecting call or outbound block
- Need a quick account brief before reaching out
- BDR needs a complete outbound package for a single account
- Running rapid-fire prospecting across multiple accounts

**Don't use when:**
- You need deep financial analysis (use `gtm-research-outbound` for public company filings)
- The account has a known incumbent to displace (use `gtm-competitive-displacement`)
- The account is a closed-lost deal (use `gtm-closed-loss-reactivation`)
- A trigger event just happened (use `gtm-trigger-event-outbound`)

**User roles:** BDR (primary), AE
**Expected time:** 5-10 minutes per account (designed for speed)

---

## Epistemic Rules

### Evidence Grading for Rapid Research
Even in a speed-optimized workflow, every data point must be labeled:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[CRM]` or `[Verified — Source]` | Confirmed from CRM data, company website, SEC filings, or authoritative source | Use directly in emails and call prep |
| **INFERRED** | `[Inferred — Basis]` | Logical conclusion from verified data (e.g., "multi-state operations" inferred from branch locations) | Use in pain hypotheses and discovery questions |
| **ESTIMATED** | `[Estimated — Method]` | Revenue or volume estimate from employee count, branch proxy, or industry ranking | Label clearly; never present as fact |
| **UNKNOWN** | `[Unknown]` | Data not available | Mark as a gap; include a discovery question to fill it |

### Speed vs. Depth Trade-offs
1. **CRM data first** — always check CRM before web research; it is faster and more personalized
2. **5-minute research ceiling** — if research is taking longer than 5 minutes, stop and work with what you have
3. **Unknown is acceptable** — an `[Unknown]` label with a discovery question is better than a fabricated fact
4. **Pain hypotheses are always INFERRED** — they are educated guesses based on company profile, not confirmed pain
5. **ICP verdicts must be grounded** — every GREENLIGHT / MANUAL REVIEW / DISQUALIFY verdict must cite at least 3 data points

### Confidence in Pain Hypotheses
- **HIGH confidence**: Pain hypothesis matches company profile on 3+ signals (size, vertical, geographic exposure, CRM history)
- **MEDIUM confidence**: Pain hypothesis matches on 1-2 signals; plausible but needs validation
- **LOW confidence**: Pain hypothesis is generic; could apply to any company in the industry. Rewrite to be more specific or flag as weak.

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE — this affects call goals, summary framing, and coordination guidance.

**From CRM:** Check user role/profile. If unclear, check whether user appears as BDR Owner (contacts) or Account Owner (pipeline deals).
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

---

### Step 1: Gather Intelligence (Parallel)

#### 1a. Search CRM
Pull everything available:
- Account record: name, industry, HQ, website, owner, status
- Deal history: current opportunities, past closed-won/lost, amounts, stages
- Contacts: all known contacts with titles, email, phone, engagement level, last activity
- Engagement history: meetings, calls, emails — with dates and key notes
- AI summaries: any existing deal intelligence or AI-generated summaries
- Tags/notes: anything reps have documented
- BDR Owner / Account Owner: who owns this account today

#### 1b. Research the Company
Build a quick profile using available information:
- What they do (vertical, products/services)
- Size signals (employee count, revenue if known, branch/location count)
- Geographic footprint (regions of operation)
- Ownership (public, private, PE-backed, ESOP, family)
- Recent news (acquisitions, expansions, leadership changes)

**Label every data point** with its source per Epistemic Rules. If a data point cannot be found, mark as `[Unknown]` and generate a discovery question to fill the gap.

---

### Step 2: Build Account Snapshot

#### Company Brief (5-8 bullets)
- **Company:** Full name and HQ city/state
- **Segment:** From `{Client Profile: ICP Quick-Score Dimensions}`
- **Vertical:** Specific vertical
- **Size:** Revenue estimate or employee count — with source label
- **Footprint:** Number of regions, number of locations, key markets
- **Ownership:** Public, Private, PE-backed, ESOP, or Family
- **CRM Status:** New, Existing pipeline, Former customer, or Closed-lost
- **Current Owner / BDR Owner:** From CRM
- **Active Deal?:** Yes/No — if Yes, include stage, AE owner, amount
- **Coordination Required?:** If `user_role = BDR` AND active AE deal → "Yes — coordinate with [AE name]"

#### ICP Quick-Score
Rate against `{Client Profile: ICP Quick-Score Dimensions}` and deliver verdict: GREENLIGHT / MANUAL REVIEW / DISQUALIFY (1 line).

**Scoring matrix:**

| Verdict | Criteria |
|---------|----------|
| **GREENLIGHT** | Meets primary fit signal + scale/complexity signals from ICP Quick-Score Dimensions |
| **MANUAL REVIEW** | Meets 2-3 criteria but has gaps (e.g., single-region but large, or partial vertical fit) |
| **DISQUALIFY** | Primary fit signal = No, or Scale = below threshold, or No Fit per ICP definitions |

Each verdict must cite 3+ data points with source labels.

#### Geographic/Market Exposure Map
Map regions to relevant tiers from `{Client Profile: Qualification Zones}`. Estimate monthly volume using available data.

| Region | Tier | Estimated Monthly Volume | Source |
|--------|------|-------------------------|--------|
| [Region 1] | Tier 1 | [volume] | [source] |
| [Region 2] | Tier 2 | [volume] | [source] |
| ... | ... | ... | ... |

---

### Step 3: Contact Mapping + Persona Prioritization

Map known CRM contacts to `{Client Profile: Buyer Personas}`:

| Persona | Name | Title | Engagement Level | Last Activity | Priority |
|---------|------|-------|-----------------|---------------|----------|
| [Persona 1] | [name or Unknown] | [title] | [level] | [date] | [1-5] |
| [Persona 2] | [name or Unknown] | [title] | [level] | [date] | [1-5] |
| ... | ... | ... | ... | ... | ... |

Mark gaps as "Unknown — no contact found."

Prioritize by:
1. Known contacts with engagement history (warm > cold)
2. Persona relevance to likely pain
3. Recency of activity
4. Previous deal context

Recommend **top 2-3 personas to target first** with reasoning.

---

### Step 4: Pain Hypothesis Generation

Generate 3-5 likely pain points from `{Client Profile: Core Pain Points}` ranked by probability based on the company's profile.

For each hypothesis, include:
- **Pain Point:** Name from the taxonomy
- **Why likely for this company:** Specific reasoning tied to company profile [with source label]
- **Confidence:** HIGH / MEDIUM / LOW per Epistemic Rules
- **Discovery question:** To validate the hypothesis on a call
- **Value prop:** From `{Client Profile: Value Propositions}` that addresses this pain

**Ranking rule:** Pain hypotheses must be ordered by confidence level (HIGH first). If all hypotheses are MEDIUM or LOW, note that the account needs more research or a discovery call before deeper investment.

---

### Step 5: Generate Outbound Sequences

Produce a **3-step email sequence** for the top 2-3 prioritized personas. Account Snapshots use 3 steps (not 4) because this is volume outreach.

#### Rules for Every Email
- Include a **subject line**
- Body **<= 100 words** (volume outreach demands brevity)
- **First line must reference something specific about the company** — not generic
- Personalize with contact name when known
- Each step uses a different pain hypothesis or angle
- Only VERIFIED and INFERRED data may appear in emails; ESTIMATED data must be framed as questions

#### Sequence Structure (Per Persona)
| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | Company-specific pain hypothesis + product connection | Prove homework; earn the open |
| **Email 2** | Different pain angle + proof point from similar company | Build credibility; show results |
| **Email 3** | Breakup + single question | Low-pressure close; one question |

Match proof points from `{Client Profile: Proof Points}` to the prospect's vertical and size. Max 1 per email, labeled with source.

---

### Step 6: Cold Call Prep Sheet

#### Role-Aware Call Goal
| Role | Call Goal |
|------|----------|
| **BDR** | "Book a 15-minute discovery call for [AE name]" |
| **BDR + Active Deal** | "STOP — Share research with [AE name] instead" |
| **AE** | "Advance the deal — [specific next step]" |
| **AE (no deal)** | "Qualify interest for new opportunity" |

#### 30-Second Opener
Reference the company by name, state one specific reason for calling (tied to pain hypothesis #1), ask a permission-based question.

**Structure:** "Hi [Name], this is [Rep] from [Company]. I'm calling because [specific reason tied to their company]. Do you have 30 seconds?"

#### Talk Track (if they engage)
- Pain validation question
- Impact question ("What does that cost you in terms of...?")
- Product bridge (1 sentence)
- Ask ("Worth 15 minutes to see how [similar company] solved this?")

#### Voicemail Script (<30 seconds)
- Name + company
- One specific, relevant statement
- CTA: "I'll send a quick email with details"

#### Expected Objections + Rebuttals
Use `{Client Profile: Competitive Landscape}` for competitive objections. Include 4-5 common objections with rebuttals tailored to the prospect's profile:

| Objection | Rebuttal |
|-----------|----------|
| "We already have a solution" | "Great — that means you understand the value. Curious what's working well and what you'd improve?" |
| "Not interested" | "Totally fair. Quick question — how is your team handling [pain hypothesis] today?" |
| "Send me an email" | "Happy to. What would be most useful — ROI benchmarks or the [relevant capability] overview?" |
| "No budget" | "Makes sense. If I could show you how [similar company] achieved [metric], would that be worth a 15-minute conversation?" |
| "We're too small / not ready" | "That's what [proof point company] said before they had a [specific consequence]. Worth understanding the risk?" |

---

### Step 7: Summary

1. **User Role**: BDR / AE
2. **Account**: Name, segment, vertical, size, regions
3. **ICP Verdict**: Quick-score result + 3 supporting data points
4. **CRM Status**: New / existing / closed-lost + owner
5. **Active Deal?**: If yes — stage, AE owner, amount
6. **Coordination Guidance**: (BDR only) Active deal coordination or "Clear to proceed"
7. **Contacts Found**: Count + persona coverage gaps
8. **Top Pain Hypotheses**: Ranked 1-3 with confidence levels
9. **Personas Targeted**: Which 2-3 + reasoning
10. **Sequences Generated**: [Count] personas x 3 emails
11. **Call Prep Included**: Yes/No
12. **Recommended First Action**: Email or call, which persona, which pain hypothesis
13. **Data Quality**: Count of VERIFIED vs. INFERRED vs. UNKNOWN data points

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[COMPANY]_Account_Snapshot.md`
- **Option B: HTML** — Styled 8-section cheatsheet with color-coded sections
- **Option C: PDF** — Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)
1. **Company Snapshot** — Firmographics, ICP verdict, CRM status
2. **Geographic/Market Exposure** — Regions mapped to tiers, volume estimate
3. **Key Personas** — Top 3-4 contacts with priorities and pain mapping
4. **Pain Hypotheses** — 4-5 talk-track-ready hooks with validation questions
5. **Discovery Questions** — Organized open -> probe -> confirm
6. **Value Props** — Vertical-matched value prop, proof point, estimated impact
7. **Objection Handling** — 5 common objections with rebuttals
8. **Call Flow** — 5-step talk track + voicemail script

---

## Examples

### Example 1: BDR Account Snapshot — PE-Backed Enterprise Account

**Context:** BDR prepping for a prospecting call to a large PE-backed company during a morning outbound block.

**Input:** "Give me an account snapshot on [Target Company] with outbound sequences and a cheatsheet."

**Step 0 — Role Detection:** User is BDR. CRM check: account exists in CRM, no active deal, no BDR owner assigned. Clear to proceed.

**Step 1 — Intelligence Gathering:**
CRM search: Account exists. No active deal. No closed-lost history. 3 contacts found: CFO (no activity), VP of [relevant function] (last email opened 120 days ago), [Operations Manager] (no activity).

Company research: [Target Company], HQ [City, State]. Private, PE-backed [Verified — company website]. 400+ locations across 40+ states [Verified — website locations page]. Revenue: $8B+ [Estimated — industry ranking]. Dedicated operations team with 15+ members [Inferred — job postings show multiple relevant roles].

**Step 2 — Account Snapshot:**
Company brief: [Target Company] | [City, State] | [Industry] | PE-backed | $8B+ revenue [Estimated] | 400+ locations | 40+ states.

ICP Quick-Score: **GREENLIGHT**
- Primary fit signal: Yes [Verified — company profile]
- Multi-region: Yes, 40+ states [Verified — website]
- Tier 1 market exposure [Verified — locations page]
- Scale: Enterprise ($8B+) [Estimated — industry ranking]
- Team complexity: Dedicated team (15+) [Inferred — job postings]

**Step 3 — Contact Mapping:**
| Persona | Name | Engagement | Last Activity | Priority |
|---------|------|-----------|---------------|----------|
| CFO | [Name] | None | N/A | 3 |
| VP [Function] | [Name] | Low (email opened) | 120 days ago | 1 |
| [Operations Manager] | [Name] | None | N/A | 2 |
| [Persona 4] | Unknown | — | — | 4 |

Top personas: VP [Function] (warmest — opened email), [Operations Manager] (closest to daily pain), CFO (PE reporting angle).

**Step 4 — Pain Hypotheses:**
1. **[Pain Point A]** — 400+ branches almost certainly use different methods. HIGH confidence. [Verified: 400+ locations + PE rollup model]
2. **[Pain Point B]** — At enterprise scale, manual processes are unsustainable. MEDIUM confidence. [Inferred: no known vendor in CRM]
3. **[Pain Point C]** — Operating in key markets with high volume = high exposure. HIGH confidence. [Verified: Tier 1 market presence]

**Step 5 — Sequences (VP [Function] — Email 1):**
Subject: [Company-specific pain] across 400+ [Target Company] locations

[Name] — managing [core challenge] across 400+ locations in 40+ states is a challenge that gets harder every time [PE firm] acquires another company.

When processes differ by location, the risk isn't just inefficiency — it's [specific business consequence].

[Reference customer] standardized [process] across all locations on a single platform. Their team now [key metric].

Worth 15 minutes to compare approaches?

**Step 7 — Summary:** BDR. [Target Company], GREENLIGHT. 3 contacts found, targeting VP [Function] first. 3 personas x 3 emails = 9 sequences. Call prep included. Recommended first action: Email VP [Function] with PE rollup operations angle. Data quality: 4 VERIFIED, 3 INFERRED, 1 ESTIMATED.

---

### Example 2: AE Quick Prep — Inbound Account

**Context:** AE needs quick prep before an inbound discovery call scheduled in 20 minutes.

**Input:** "Quick call prep for [Target Company] — they called in."

**Step 0 — Role Detection:** User is AE. Quick Call Prep pattern detected — skip sequence generation, deliver Steps 1-4 + Step 6 only.

**Step 1 — Intelligence Gathering:**
CRM search: New account, no prior history. No contacts in CRM yet.

Company research: [Target Company], HQ [City, State]. Public ([Ticker]) [Verified — SEC]. $5.3B revenue [Verified — 10-K]. [Industry vertical] [Verified]. 45+ locations across 30+ states [Verified — company website]. Dedicated operations team [Inferred — company size].

**Step 2 — Account Snapshot:**
ICP Quick-Score: **GREENLIGHT**
- Primary fit signal: Yes [Verified — company profile]
- Multi-region: Yes, 30+ states [Verified]
- Tier 1 + Tier 2 market exposure [Verified — locations]
- Scale: Enterprise ($5.3B) [Verified — SEC filing]
- Team complexity: Dedicated team [Inferred — enterprise size]

**Step 4 — Pain Hypotheses:**
1. **[Pain Point A]** — 45+ locations, likely different approaches per region. HIGH confidence.
2. **[Pain Point B]** — Operating in 30+ regions at enterprise scale. HIGH confidence.
3. **[Pain Point C]** — At this volume, manual processes consume significant team capacity. MEDIUM confidence.

**Step 6 — Call Prep:**
Call goal: "Qualify interest for new opportunity."

30-Second Opener: "Hi [Name], this is [Rep] from [Company]. Thanks for reaching out. Before I dive in — you're managing [core challenge] across 45+ locations in 30+ states. Curious what prompted the call today?"

Talk Track:
- "How does your team currently handle [core process] across all 30+ regions?"
- "When a [critical deadline or event] is approaching, how does the local team know?"
- "What would it mean for your team if [core process] was automated across every location from a single platform?"
- "We work with companies like [Reference Customer] who [key metric]. Worth exploring what that looks like for [Target Company]?"

Objection prep: "We're just looking" → "Totally understand. What specifically triggered the research? Knowing that helps me make the next 15 minutes more valuable."

**Step 7 — Summary:** AE. [Target Company], GREENLIGHT. No contacts in CRM (inbound — will be created). Quick call prep delivered. Recommended approach: Let the prospect lead with their pain, then validate with discovery questions. Data quality: 5 VERIFIED, 2 INFERRED, 0 ESTIMATED.

---

### Example 3: BDR Batch Mode — Rapid-Fire Prospecting Block

**Context:** BDR has a 2-hour prospecting block and needs snapshots for 5 accounts to identify the best 2-3 to pursue deeply.

**Input:** "Quick snapshots on these 5 accounts for my outbound block: [Company A], [Company B], [Company C], [Company D], [Company E]."

**Rapid-Fire Batch Mode activated.** Running abbreviated snapshots (Steps 1-4 only) for each, producing a ranked summary table.

| Account | ICP Verdict | Vertical | Regions | Revenue | Top Pain | Priority |
|---------|------------|----------|---------|---------|----------|----------|
| [Company C] | GREENLIGHT | [Vertical] | 48 | $7.6B [Verified] | Fragmented systems at scale | 1 |
| [Company A] | GREENLIGHT | [Vertical] | 50 | $9.8B [Verified] | Inconsistent processes | 2 |
| [Company B] | GREENLIGHT | [Vertical] | 44 | $5B+ [Estimated] | Manual processes | 3 |
| [Company D] | MANUAL REVIEW | [Vertical] | 22 | $500M+ [Estimated] | [Pain] | 4 |
| [Company E] | DISQUALIFY | [Vertical] | 4 | $50M [Estimated] | — | Skip |

**Recommendation:** Generate full sequences for [Company C] (#1) and [Company A] (#2). [Company B] (#3) is also strong — queue for tomorrow. [Company E] disqualified (too small, no Tier 1 markets). [Company D] needs manual review — partial ICP fit.

Full sequences then generated for the top 2 accounts.

---

## Common Patterns

### Pattern: Rapid-Fire Batch Mode
**When:** BDR needs snapshots for 5-10 accounts in a single prospecting block.
**Approach:** Run abbreviated snapshots (Steps 1-4 only) for each, produce a ranked summary table, then generate full sequences for the top 3-5. See Example 3.

### Pattern: Active Deal Guard (BDR)
**When:** `user_role = BDR` and the account has an active AE deal.
**Action:** Surface the deal in the summary. Recommend sharing research with AE instead of sending independent sequences.

### Pattern: Quick Call Prep Only
**When:** User says "quick call prep" or "calling in 5 minutes."
**Approach:** Skip sequence generation (Step 5). Deliver Steps 1-4 + Step 6 (call prep) only. Speed over completeness. See Example 2.

### Pattern: Snapshot Reveals Trigger Event
**When:** Research uncovers a recent news event (acquisition, expansion, leadership change).
**Action:** Note the trigger in the snapshot summary. Recommend switching to `gtm-trigger-event-outbound` to capitalize on the time-sensitive angle.

### Pattern: Snapshot Reveals Known Incumbent
**When:** CRM notes or research reveal a specific competing tool or vendor.
**Action:** Note the incumbent in the snapshot summary. Recommend switching to `gtm-competitive-displacement` for deeper competitive positioning.

---

## Troubleshooting

### "No CRM data available"
**Solution:** Proceed with web research only. Note "No existing CRM record" in the output. Flag data gaps in the summary and recommend CRM enrichment. All data points will be labeled `[Verified — web]`, `[Inferred]`, or `[Estimated]` instead of `[CRM]`.

### "No contacts found for target personas"
**Solution:** Research LinkedIn for likely contacts. Include persona gaps in the summary as "Unknown — no contact found." Recommend contact discovery as first action. Emails should use title-based personalization instead of names.

### "Company spans multiple segments"
**Solution:** Classify by primary business. A company with a secondary division qualifies under the primary ICP. Note the secondary classification as an opportunity signal. ICP scoring should be based on the primary segment.

### "Previously churned customer"
**Solution:** Flag as a risk. Check CRM for churn reason. If addressed (product gap fixed, new leadership), may still warrant outreach. Consider using `gtm-closed-loss-reactivation` instead for a more tailored approach.

### "Research turns up almost nothing on the company"
**Solution:** This is common for small private companies. Work with what you have: CRM data, company website, LinkedIn employee count. Label everything as `[Estimated]` or `[Inferred]`. Generate a lean snapshot with 2-3 pain hypotheses and a call prep focused on discovery questions. The call itself becomes the primary research tool.

### "ICP verdict is MANUAL REVIEW — should I still prospect?"
**Solution:** MANUAL REVIEW means plausible but uncertain. Check what specific signals are missing. If the gap is data quality (e.g., can't confirm revenue), proceed with outbound but prioritize discovery questions that fill the gap. If the gap is fit quality (e.g., partial vertical fit), deprioritize in favor of GREENLIGHT accounts.

---

## Best Practices

### Do's
- **Prioritize speed** — this skill is designed for volume prospecting, not deep research
- **Use CRM data first** — faster and more personalized than web research alone
- **Match proof points to vertical** — a prospect in one vertical doesn't care about proof points from a different vertical
- **Label every data point** — `[CRM]`, `[Verified — web]`, `[Inferred]`, `[Estimated]`, `[Unknown]`
- **Rank pain hypotheses by confidence** — HIGH confidence hypotheses should lead the outreach
- **Include persona coverage gaps** — knowing which personas are unknown is as valuable as knowing who exists

### Don'ts
- **Don't over-research** — if you're spending more than 10 minutes, use `gtm-research-outbound` instead
- **Don't send generic emails** — every Email 1 must reference something specific about the company
- **Don't skip the call prep** — BDRs calling without prep waste the prospect's time and their own
- **Don't ignore active deals** — always check for AE deals before BDR outbound
- **Don't present ESTIMATED data as fact** — "Your team likely handles..." not "Your team handles..."
- **Don't use LOW confidence pain hypotheses as email openers** — they feel generic and damage credibility

### Quality Checklist
- [ ] Company-specific details in every Email 1
- [ ] Pain hypotheses grounded in company profile with confidence levels
- [ ] Contact names used when available
- [ ] Proof points match vertical
- [ ] All emails <= 100 words
- [ ] Call prep is conversational, not scripted
- [ ] Voicemail < 30 seconds when read aloud
- [ ] Role detected and coordination guidance applied
- [ ] Every data point labeled with source
- [ ] ICP verdict cites 3+ data points

---

## Integration with Other Skills

- **`gtm-account-qualification`** — Run qualification first for net-new accounts, then snapshot for GREENLIGHT accounts.
- **`gtm-research-outbound`** — For deeper analysis of public companies (10-K, earnings) or private companies with high strategic value.
- **`gtm-competitive-displacement`** — When the snapshot reveals a known incumbent, switch to displacement sequences.
- **`gtm-trigger-event-outbound`** — When research reveals a recent event, pivot to trigger-based outbound.
- **`gtm-closed-loss-reactivation`** — If the account is closed-lost, use reactivation instead of cold snapshot.
- **`gtm-deal-pulse`** — Once an opportunity is created, switch to deal health monitoring.

---

## Changelog

### Version 1.1.0 (2026-03-04)
- Added Epistemic Rules section with evidence grading (VERIFIED / INFERRED / ESTIMATED / UNKNOWN), speed vs. depth trade-offs, and confidence calibration for pain hypotheses
- Added ICP Quick-Score scoring matrix with explicit criteria for GREENLIGHT / MANUAL REVIEW / DISQUALIFY
- Expanded Example 1 with full step-by-step detail including CRM search results, evidence-labeled company research, contact mapping table, pain hypothesis confidence ratings, email sample, and data quality summary
- Expanded Example 2 with AE quick call prep walkthrough including talk track and objection prep
- Added Example 3 demonstrating Batch Mode pattern with 5-account ranked summary table and prioritization guidance
- Added Snapshot Reveals Trigger Event and Snapshot Reveals Known Incumbent patterns
- Added 2 new troubleshooting entries (thin research, MANUAL REVIEW guidance)
- Expanded pain hypothesis generation with confidence levels and ranking rules
- Added objection handling table to cold call prep with 5 scripted rebuttals
- Updated quality checklist with evidence labeling and ICP verdict requirements
- Added data quality count to summary report

### Version 1.0.0 (2026-03-04)
- Initial release
- Generalized via Client Profile block with placeholder defaults
- 7-step workflow, 3-step sequences, cold call prep, 8-section cheatsheet
- Batch mode and quick call prep patterns
- Vendor-agnostic CRM instructions
- Multi-format artifact generation
