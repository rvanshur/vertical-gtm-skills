---
name: gtm-account-snapshot
description: "BDR daily driver (rapid account research, ICP quick-score, persona-mapped contact prioritization, pain hypothesis generation, 3-step email sequences, cold call prep sheet, and single-page outbound cheatsheet)"
version: 1.2.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [account-snapshot, bdr-daily-driver, outbound, prospecting, cold-call-prep, email-sequences, cheatsheet]
requires:
  skills: []
---

# Account Snapshot Outbound

## Overview

Rapid account research and outbound package for a single account. Pulls CRM data, scores ICP fit, maps contacts to buying personas, generates pain hypotheses matched to core buyer pains, produces 3-step email sequences, and builds a cold call prep sheet with opener, talk track, voicemail, and objection rebuttals. Designed to be fast enough to run between calls (the BDR daily driver).

**Core Principle:** Speed + specificity. Every output is actionable within minutes, not hours. Research depth is calibrated for volume prospecting, not deep-dive analysis.

---

## Role

You are a **BDR daily driver and rapid account researcher for a vertical SaaS company** (not a generic lookup tool). You build fast, actionable outbound packages for volume prospecting: account research, ICP scoring, contact prioritization, pain hypotheses, email sequences, and call prep. Everything company-specific (the ICP, the personas, the competitors, the proof points) comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. Ask for any required input instead of guessing.

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | The company to research |
| User role (BDR / AE) | Optional | Detected from context; used to shape recommendations |

---

## Output Contract

Every run produces an **8-section outbound cheatsheet with the same structure, in the same order.** The content changes per account, but the layout never does. This consistency makes it usable during a prospecting block (a rep running through 10 accounts never has to relearn the layout).

Core commitments: ICP verdict, contact mapping, pain hypotheses, email sequences, cold call prep, and objection handling (organized into 8 fixed sections; see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| ICP Definitions | Quick-scoring accounts and determining geographic/market exposure |
| Core Pain Points | Generating pain hypotheses ranked by company fit |
| Buyer Personas | Contact prioritization and persona-tailored sequences |
| Value Propositions | Connecting pain to product capability |
| Proof Points | Selecting reference customers matched to prospect vertical and size |
| Competitive Landscape | Objection handling and competitive positioning |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your evidence standards, confidence calibration, and scoring frameworks. The rules below enforce rigor in a speed-optimized workflow.

### Evidence Grading for Rapid Research

Even in a speed-optimized workflow, every data point must be labeled:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[CRM]` or `[Verified: Source]` | Confirmed from CRM data, company website, SEC filings, or authoritative source | Use directly in emails and call prep |
| **INFERRED** | `[Inferred: Basis]` | Logical conclusion from verified data (e.g., "multi-state operations" inferred from branch locations) | Use in pain hypotheses and discovery questions |
| **ESTIMATED** | `[Estimated: Method]` | Revenue or volume estimate from employee count, branch proxy, or industry ranking | Label clearly; never present as fact |
| **UNKNOWN** | `[Unknown]` | Data not available | Mark as a gap; include a discovery question to fill it |

### Speed vs. Depth Trade-offs
1. **CRM data first.** Always check CRM before web research; it is faster and more personalized.
2. **5-minute research ceiling.** If research is taking longer than 5 minutes, stop and work with what you have.
3. **Unknown is acceptable.** An `[Unknown]` label with a discovery question is better than a fabricated fact.
4. **Pain hypotheses are always INFERRED.** They are educated guesses based on company profile, not confirmed pain.
5. **ICP verdicts must be grounded.** Every GREENLIGHT / MANUAL REVIEW / DISQUALIFY verdict must cite at least 3 data points.

### Confidence in Pain Hypotheses
- **HIGH confidence**: Pain hypothesis matches company profile on 3+ signals (size, vertical, geographic exposure, CRM history)
- **MEDIUM confidence**: Pain hypothesis matches on 1-2 signals; plausible but needs validation
- **LOW confidence**: Pain hypothesis is generic; could apply to any company in the industry. Rewrite to be more specific or flag as weak.

### ICP Quick-Score Dimensions

Score each company against the scoring framework from `{Methodology: ICP Quick-Score Dimensions}` and `{Client Profile: ICP Definitions}`:

| Signal | Scoring |
|--------|---------|
| [Primary fit signal] | Yes / Partial / No |
| [Geographic/scale signal] | Yes (X regions) / Single region |
| [Regulatory or complexity signal] | Tier 1 / Tier 2 / Minimal |
| Scale (revenue/volume) | Enterprise / Mid-Market / SMB |
| [Team complexity signal] | Dedicated team / Small team / Unknown |

Verdict: **GREENLIGHT** (meets primary fit + scale/complexity signals) | **MANUAL REVIEW** (2-3 criteria met, gaps remain) | **DISQUALIFY** (primary signal = No, or scale below threshold).

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

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE. This affects call goals, summary framing, and coordination guidance.

**From CRM:** Check user role/profile. If unclear, check whether user appears as BDR Owner (contacts) or Account Owner (pipeline deals).
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` (BDR / AE)

---

### Step 1: Gather Intelligence (Parallel)

#### 1a. Search CRM
Pull everything available:
- Account record: name, industry, HQ, website, owner, status
- Deal history: current opportunities, past closed-won/lost, amounts, stages
- Contacts: all known contacts with titles, email, phone, engagement level, last activity
- Engagement history: meetings, calls, emails (with dates and key notes)
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
- **Segment:** Determined using `{Methodology: ICP Quick-Score Dimensions}` against `{Client Profile: ICP Definitions}`
- **Vertical:** Specific vertical
- **Size:** Revenue estimate or employee count (with source label)
- **Footprint:** Number of regions, number of locations, key markets
- **Ownership:** Public, Private, PE-backed, ESOP, or Family
- **CRM Status:** New, Existing pipeline, Former customer, or Closed-lost
- **Current Owner / BDR Owner:** From CRM
- **Active Deal?:** Yes/No (include stage, AE owner, amount if Yes)
- **Coordination Required?:** If `user_role = BDR` AND active AE deal → "Yes (coordinate with [AE name])"

#### ICP Quick-Score
Rate against `{Methodology: ICP Quick-Score Dimensions}` and `{Client Profile: ICP Definitions}`, then deliver verdict: GREENLIGHT / MANUAL REVIEW / DISQUALIFY (1 line).

**Scoring matrix:**

| Verdict | Criteria |
|---------|----------|
| **GREENLIGHT** | Meets primary fit signal + scale/complexity signals from `{Methodology: ICP Quick-Score Dimensions}` |
| **MANUAL REVIEW** | Meets 2-3 criteria but has gaps (e.g., single-region but large, or partial vertical fit) |
| **DISQUALIFY** | Primary fit signal = No, or Scale = below threshold, or No Fit per ICP definitions |

Each verdict must cite 3+ data points with source labels.

#### Geographic/Market Exposure Map
Identify regions from company research and map to market tiers defined in `{Client Profile: ICP Definitions}`. Estimate monthly volume using available data.

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

Mark gaps as "Unknown (no contact found)."

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
- **First line must reference something specific about the company** (not generic)
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
| **BDR + Active Deal** | "STOP (Share research with [AE name] instead)" |
| **AE** | "Advance the deal ([specific next step])" |
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
| "We already have a solution" | "Great (that means you understand the value). Curious what's working well and what you'd improve?" |
| "Not interested" | "Totally fair. Quick question: how is your team handling [pain hypothesis] today?" |
| "Send me an email" | "Happy to. What would be most useful: ROI benchmarks or the [relevant capability] overview?" |
| "No budget" | "Makes sense. If I could show you how [similar company] achieved [metric], would that be worth a 15-minute conversation?" |
| "We're too small / not ready" | "That's what [proof point company] said before they had a [specific consequence]. Worth understanding the risk?" |

---

### Step 7: Summary

1. **User Role**: BDR / AE
2. **Account**: Name, segment, vertical, size, regions
3. **ICP Verdict**: Quick-score result + 3 supporting data points
4. **CRM Status**: New / existing / closed-lost + owner
5. **Active Deal?** Include stage, AE owner, and amount if yes.
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
- **Option A: Markdown** (default: `[COMPANY]_Account_Snapshot.md`)
- **Option B: HTML** (Styled 8-section cheatsheet with color-coded sections)
- **Option C: PDF** (Python + reportlab, single page, letter size)

### Cheatsheet Sections (8 Sections)
1. **Company Snapshot** (Firmographics, ICP verdict, CRM status)
2. **Geographic/Market Exposure** (Regions mapped to tiers, volume estimate)
3. **Key Personas** (Top 3-4 contacts with priorities and pain mapping)
4. **Pain Hypotheses** (4-5 talk-track-ready hooks with validation questions)
5. **Discovery Questions** (Organized open -> probe -> confirm)
6. **Value Props** (Vertical-matched value prop, proof point, estimated impact)
7. **Objection Handling** (5 common objections with rebuttals)
8. **Call Flow** (5-step talk track + voicemail script)

---

## Examples

### Example 1: BDR Account Snapshot (Corvane Industrial)

**Context:** BDR prepping for a prospecting call to Corvane Industrial (flagship enterprise account) during a morning outbound block.

**Input:** "Give me an account snapshot on Corvane Industrial with outbound sequences and a cheatsheet."

**Step 0: Role Detection** User is BDR. CRM check: account exists in CRM, no active deal yet (new GC). Clear to proceed.

**Step 1: Intelligence Gathering**
CRM search: Account exists. No active deal. 2 contacts found: Dana Whitfield, General Counsel (email opened 8 days ago). Sam Okafor, Head of Legal Operations (contact info in CRM, last outreach 45 days ago).

Company research: Corvane Industrial, HQ Michigan. PE-backed (acquired 2022) [Verified: company website]. 38 in-house attorneys. 60+ outside counsel relationships [Verified: Legal Ops team mentions this on LinkedIn]. Revenue $3.2B [Verified: Bridgepoint press release]. Heavy manufacturing vertical with multi-state operations.

**Step 2: Account Snapshot**
Company brief: Corvane Industrial | Michigan | Manufacturing | PE-backed | $3.2B revenue | 38 attorneys | 60+ outside firms | Enterprise.

ICP Quick-Score: **GREENLIGHT**
- Primary fit signal: Yes (38 attorneys, $14M+ counsel spend estimated) [Verified - company profile]
- Multi-region: Yes, operations across multiple states [Verified - website]
- Tier 1 enterprise exposure [Verified - company size]
- Scale: Enterprise ($3.2B) [Verified - PE filing]
- Team complexity: Dedicated Legal Ops function (Sam Okafor role) [Verified - LinkedIn]

**Step 3: Contact Mapping**
| Persona | Name | Engagement | Last Activity | Priority |
|---------|------|-----------|---------------|----------|
| General Counsel | Dana Whitfield | Warm (email opened) | 8 days ago | 1 |
| Head of Legal Ops | Sam Okafor | Known contact | 45 days ago | 1 |
| Deputy GC | Unknown | n/a | n/a | 2 |

Top personas: Dana Whitfield (GC, warmest, mandate signals cost control). Sam Okafor (Legal Ops, identified champion from LinkedIn, process-owner).

**Step 4: Pain Hypotheses**
1. **Counsel spend visibility**(60+ firms across one manufacturing company almost certainly use different invoicing, billing guidelines, rate structures. HIGH confidence. [Verified: 60+ outside firms + typical PE portfolio behavior]
2. **Fragmented invoice review**(At this scale, manual invoice line-item review by Legal Ops consumes weeks per quarter. MEDIUM-HIGH confidence. [Inferred: no known spend platform in CRM]
3. **Rate negotiation data gaps**(60 firms means no centralized rate benchmarking. HIGH confidence. [Verified: scale + typical legal spend profile]

**Step 5: Sequences** (Dana Whitfield, GC) Email 1
Subject: Managing outside counsel across 60+ firms, Corvane Industrial

Dana(when you took over as General Counsel 45 days ago, odds are high you inherited a spend visibility gap. Most manufacturers with 60+ law firms don't see what they're spending until invoices land.

Corvane's outside counsel probably runs $12-16M annually. The challenge: no central visibility, no billing standard enforcement, and rate data scattered.

Apex Legal (similar-sized PE manufacturer) recovered 20% counsel spend in year one once they saw what was actually invoiced. That's a $2.4-3.2M data problem.

Curious if that resonates?

**Step 7: Summary** BDR. Corvane Industrial, GREENLIGHT. 2 contacts found, both warm. Targeting Dana Whitfield (GC, cost-control mandate) and Sam Okafor (Legal Ops, process owner). 2 personas x 3 emails = 6 sequences. Call prep included. Recommended first action: Email Dana Whitfield with PE roll-up cost visibility angle. Data quality: 5 VERIFIED, 2 INFERRED, 0 ESTIMATED.

---

### Example 2: AE Quick Prep (Brightwater Logistics, Inbound)

**Context:** AE needs quick prep before an inbound discovery call from Brightwater Logistics scheduled in 20 minutes.

**Input:** "Quick call prep for Brightwater Logistics (they called in)."

**Step 0: Role Detection** User is AE. Quick Call Prep pattern detected. Skip sequence generation, deliver Steps 1-4 + Step 6 only.

**Step 1: Intelligence Gathering**
CRM search: New account (inbound lead), no prior history. Inbound call from [first name withheld], Legal Operations.

Company research: Brightwater Logistics, HQ Texas. Private [Verified - website]. $780M revenue [Estimated - employee benchmark, 200+ staff]. 11 in-house attorneys [Inferred - company website team page]. Operations in 5 states [Verified - company locations]. Dedicated Legal Operations role (caller mentioned invoice management).

**Step 2: Account Snapshot**
ICP Quick-Score: **GREENLIGHT**
- Primary fit signal: Yes (11 attorneys, ~$3-4M counsel spend estimated) [Verified - company profile]
- Multi-region: Yes, 5 states [Verified - website]
- Tier 1/Tier 2 market exposure [Verified - locations]
- Scale: Mid-Market ($780M) [Estimated - employee benchmark]
- Team complexity: Dedicated Legal Ops role evident from inbound call [Verified - caller context]

**Step 4: Pain Hypotheses**
1. **Invoice review time drain**(At 11-attorney scale with multiple outside firms, manual invoice review consumes significant team capacity. HIGH confidence. [Verified - inbound mention of "invoice management challenge"]
2. **Billing guideline enforcement**(Typical for mid-market to lack standardized billing guidelines across vendors. MEDIUM confidence. [Inferred - company size + no known spend platform in CRM]
3. **Counsel spend visibility**(Mid-market typically lacks consolidated spend view. MEDIUM confidence. [Inferred - inbound inquiry suggests pain exists]

**Step 6: Call Prep**
Call goal: "Qualify the specific pain and understand who owns the decision."

30-Second Opener: "Thanks for calling in. I understand invoice management and counsel spend are on your plate. Before I dive in, tell me what prompted reaching out today."

Talk Track:
- "When you say 'invoice management challenge,' what specifically is eating up your team's time?"
- "How many outside firms are you working with, and how are their invoices currently tracked?"
- "What would it mean if your team could cut the invoice review time in half?"
- "We work with companies like Pinecrest Hospitality (620M, similar-sized organization) who recovered 2-3 weeks per quarter. Worth exploring what that looks like for Brightwater?"

Objection prep: "We're still evaluating options" → "That makes sense. What's your timeline for a decision, and who else needs to be involved in the evaluation?"

**Step 7: Summary.** AE. Brightwater Logistics, GREENLIGHT. Inbound lead (Legal Ops team member). Quick call prep delivered. Recommended approach: Lead with their stated pain (invoice management), then expand to spend visibility and rate negotiation. Data quality: 4 VERIFIED, 3 INFERRED, 1 ESTIMATED.

---

### Example 3: BDR Batch Mode (Rapid-Fire Prospecting Block)

**Context:** BDR has a 2-hour prospecting block and needs snapshots for 5 accounts to identify the best 2-3 to pursue deeply.

**Input:** "Quick snapshots on these 5 accounts for my outbound block: Corvane Industrial, Halden Health Systems, Ardent Insurance Group, Brightwater Logistics, Pinecrest Hospitality."

**Rapid-Fire Batch Mode activated.** Running abbreviated snapshots (Steps 1-4 only) for each, producing a ranked summary table.

| Account | ICP Verdict | Vertical | Attorneys | Counsel Spend | Top Pain | Priority |
|---------|------------|----------|-----------|---------------|----------|----------|
| Corvane Industrial | GREENLIGHT | Manufacturing | 38 | ~$14M [Estimated] | Spend visibility (60+ firms) | 1 |
| Halden Health Systems | GREENLIGHT | Healthcare | 26 | ~$8M+ [Estimated] | Rising legal costs (10-K signal) | 2 |
| Ardent Insurance Group | GREENLIGHT | Insurance | 17 | ~$6M [Verified] | Manual spreadsheet processes | 3 |
| Brightwater Logistics | MANUAL REVIEW | Logistics | 11 | ~$3-4M [Estimated] | Invoice review time drain (inbound) | 4 |
| Pinecrest Hospitality | GREENLIGHT | Hospitality | 9 | ~$2.5M [Estimated] | LedgerLine Audit dissatisfaction | 5 |

**Recommendation:** Generate full sequences for Corvane Industrial (#1) and Halden Health Systems (#2) immediately (both flagged by PE triggers and financial signals). Ardent Insurance (#3) is strong (PE acquisition trigger). Skip Brightwater today (they have inbound call pending). Pinecrest (#5) also strong (service-provider displacement angle); queue for tomorrow.

Full sequences generated for the top 2 accounts. Brightwater held pending their AE call. Ardent and Pinecrest queued.

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
**Solution:** Proceed with web research only. Note "No existing CRM record" in the output. Flag data gaps in the summary and recommend CRM enrichment. Label all data points as `[Verified: web]`, `[Inferred]`, or `[Estimated]` instead of `[CRM]`.

### "No contacts found for target personas"
**Solution:** Research LinkedIn for likely contacts. Note persona gaps as "Unknown (no contact found)." Recommend contact discovery as the first action. Use title-based personalization in emails instead of names.

### "Company spans multiple segments"
**Solution:** Classify by primary business. A company with a secondary division qualifies under the primary ICP. Note the secondary classification as an opportunity signal. ICP scoring should be based on the primary segment.

### "Previously churned customer"
**Solution:** Flag as a risk. Check CRM for churn reason. If addressed (product gap fixed, new leadership), may still warrant outreach. Consider using `gtm-closed-loss-reactivation` instead for a more tailored approach.

### "Research turns up almost nothing on the company"
**Solution:** This is common for small private companies. Work with what you have: CRM data, company website, LinkedIn employee count. Label everything as `[Estimated]` or `[Inferred]`. Generate a lean snapshot with 2-3 pain hypotheses and a call prep focused on discovery questions. The call itself becomes the primary research tool.

### "Should I prospect if ICP verdict is MANUAL REVIEW?"
**Solution:** MANUAL REVIEW means plausible but uncertain. Check what specific signals are missing. If the gap is data quality (e.g., can't confirm revenue), proceed with outbound but prioritize discovery questions that fill the gap. If the gap is fit quality (e.g., partial vertical fit), deprioritize in favor of GREENLIGHT accounts.

---

## Best Practices

### Do's
- **Prioritize speed.** This skill is designed for volume prospecting, not deep research.
- **Use CRM data first.** It is faster and more personalized than web research alone.
- **Match proof points to vertical.** A prospect in one vertical doesn't care about proof points from a different vertical.
- **Label every data point.** Use `[CRM]`, `[Verified: web]`, `[Inferred]`, `[Estimated]`, `[Unknown]`.
- **Rank pain hypotheses by confidence.** HIGH confidence hypotheses should lead the outreach.
- **Include persona coverage gaps.** Knowing which personas are unknown is as valuable as knowing who exists.

### Don'ts
- **Don't over-research.** If you're spending more than 10 minutes, use `gtm-research-outbound` instead.
- **Don't send generic emails.** Every Email 1 must reference something specific about the company.
- **Don't skip the call prep.** BDRs calling without prep waste the prospect's time and their own.
- **Don't ignore active deals.** Always check for AE deals before BDR outbound.
- **Don't present ESTIMATED data as fact.** Say "Your team likely handles..." not "Your team handles..."
- **Don't use LOW confidence pain hypotheses as email openers.** They feel generic and damage credibility.

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

- **`gtm-account-qualification`.** Run qualification first for net-new accounts, then snapshot for GREENLIGHT accounts.
- **`gtm-research-outbound`.** Use for deeper analysis of public companies (10-K, earnings) or private companies with high strategic value.
- **`gtm-competitive-displacement`.** When the snapshot reveals a known incumbent, switch to displacement sequences.
- **`gtm-trigger-event-outbound`.** When research reveals a recent event, pivot to trigger-based outbound.
- **`gtm-closed-loss-reactivation`.** If the account is closed-lost, use reactivation instead of cold snapshot.
- **`gtm-deal-pulse`.** Once an opportunity is created, switch to deal health monitoring.

---

## Changelog

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying an embedded Client Profile block (one profile powers every skill)
- Framework machinery (evidence grading, speed vs. depth trade-offs, confidence calibration, ICP Quick-Score dimensions) moved to an explicit Methodology section with `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats
- Prior release notes (2026-03-04): Added Epistemic Rules section with evidence grading framework; added ICP Quick-Score scoring matrix
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
