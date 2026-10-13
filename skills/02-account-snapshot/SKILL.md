---
name: gtm-account-snapshot
description: "BDR daily driver (rapid account research, ICP quick-score, persona-mapped contact prioritization, pain hypothesis generation, 3-step email sequences, cold call prep sheet, and single-page outbound cheatsheet)"
version: 1.3.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
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
| User role (BDR / AE) | Optional | Detected from context. Used to shape recommendations |

---

## Output Contract

Every run produces an **8-section outbound cheatsheet with the same structure, in the same order.** The content changes per account, but the layout never does. This consistency makes it usable during a prospecting block (a rep running through 10 accounts never has to relearn the layout).

Core commitments: ICP verdict, contact mapping, pain hypotheses, email sequences, cold call prep, and objection handling (organized into 8 fixed sections. See *Artifact Generation* below).

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
| **ESTIMATED** | `[Estimated: Method]` | Revenue or volume estimate from employee count, branch proxy, or industry ranking | Label clearly. Never present as fact |
| **UNKNOWN** | `[Unknown]` | Data not available | Mark as a gap. Include a discovery question to fill it |

### Speed vs. Depth Trade-offs
1. **CRM data first.** Always check CRM before web research. It is faster and more personalized.
2. **5-minute research ceiling.** If research is taking longer than 5 minutes, stop and work with what you have.
3. **Unknown is acceptable.** An `[Unknown]` label with a discovery question is better than a fabricated fact.
4. **Pain hypotheses are always INFERRED.** They are educated guesses based on company profile, not confirmed pain.
5. **ICP verdicts must be grounded.** Every GREENLIGHT / MANUAL REVIEW / DISQUALIFY verdict must cite at least 3 data points.

### Confidence in Pain Hypotheses
- **HIGH confidence**: Pain hypothesis matches company profile on 3+ signals (size, vertical, geographic exposure, CRM history)
- **MEDIUM confidence**: Pain hypothesis matches on 1-2 signals. It is plausible but needs validation
- **LOW confidence**: Pain hypothesis is generic. It could apply to any company in the industry. Rewrite to be more specific or flag as weak.

### ICP Quick-Score Dimensions

Score each company against the scoring framework from `{Methodology: ICP Quick-Score Dimensions}` and `{Client Profile: ICP Definitions}`:

| Signal | Scoring |
|--------|---------|
| [Primary fit signal] | Yes / Partial / No |
| [Geographic/scale signal] | Yes (X regions) / Single region |
| [Regulatory or complexity signal] | High / Medium / Minimal |
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
| [Region 1] | [Tier from profile] | [volume] | [source] |
| [Region 2] | [Tier from profile] | [volume] | [source] |
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
- Only VERIFIED and INFERRED data may appear in emails. ESTIMATED data must be framed as questions

#### Sequence Structure (Per Persona)
| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | Company-specific pain hypothesis + product connection | Prove homework. Earn the open |
| **Email 2** | Different pain angle + proof point from similar company | Build credibility. Show results |
| **Email 3** | Breakup + single question | Low-pressure close. One question |

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

Account facts in these examples come from the PlotIQ example cast, and they are tagged `[CRM]` as if the CRM held them. Any number the profile does not supply is tagged `(illustrative)`. Three examples follow: a BDR research pass that leads to outbound, an AE quick prep that ends in a REVIEW verdict, and a batch that includes a disqualified account and a closed-lost one.

### Example 1: BDR Account Snapshot (Quill Hollow Memorial Park)

**Context:** A BDR prepares a first outbound touch to Quill Hollow Memorial Park during a morning block. The general manager, Ines Carmody, moved here six months ago from Lowmoor Memorial Gardens, where she was a champion.

**Input:** "Give me an account snapshot on Quill Hollow Memorial Park with outbound sequences and a cheatsheet."

**Step 0: Role Detection** User is BDR. CRM check: account exists, status TARGET, no active deal. Clear to proceed.

**Step 1: Intelligence Gathering**
CRM search: Account exists. No active deal. One contact found: Ines Carmody, General Manager (champion, `[CRM]`). The owner's name is not in the CRM. Site budget: the owner signs under $25K `[CRM]`. The last state review included a records finding `[CRM]`.

Company research: One site, 8,800 plots, paper plat maps `[CRM]`. The owner brought a growth mandate when Ines Carmody joined `[CRM]`. Region: `[Unknown]`, so the market tier is left blank until the profile's tiers are checked.

**Step 2: Account Snapshot**
Company brief: Quill Hollow Memorial Park | State not in CRM | Independent cemetery | Ownership not recorded | 8,800 plots | Paper plat maps | Mid-size (one site).

ICP Quick-Score: **GREENLIGHT**
- Primary fit signal: Yes (8,800 plots, paper plat maps, above the 2,000-plot threshold) `[CRM]`
- Multi-region: Single site, so no multi-region signal `[CRM]`
- Regulatory or complexity signal: High (a records finding in the last state review) `[CRM]`
- Scale: Mid-size (one site, 8,800 plots) `[CRM]`
- Team complexity: Dedicated owner and GM. Owner signs under $25K `[CRM]`

**Step 3: Contact Mapping**
| Persona | Name | Engagement | Last Activity | Priority |
|---------|------|-----------|---------------|----------|
| General Manager (champion) | Ines Carmody | Warm (champion from a prior site) | 2 weeks ago (illustrative) | 1 |
| Owner (signs under $25K) | Unknown (no contact found) | n/a | n/a | 2 |
| Pre-Need Sales Manager | Unknown (no contact found) | n/a | n/a | 3 |

Top personas: Ines Carmody first, because she has engagement history and runs the site now. The owner is second, because the owner signs. Her history at Lowmoor is closed-lost and belongs to Closed-Loss Reactivation (05), not this outbound.

**Step 4: Pain Hypotheses**
1. **Plot visibility** (The plot map is on paper, so nobody can list the unsold plots without walking the grounds. HIGH confidence. `[CRM: paper plat maps]` and `[Inferred: 8,800 plots on paper]`)
2. **Records after a state finding** (The last state review found a records problem, so the next review is a pressure point. MEDIUM-HIGH confidence. `[CRM: records finding]`)
3. **Pre-need follow-up** (No pre-need team is recorded, so this is a question, not a finding. LOW confidence. `[Unknown: pre-need activity not in CRM]`. Use it only as a discovery question.)

**Step 5: Sequences** (Ines Carmody, General Manager) Email 1
Subject: Plot records after the state review at Quill Hollow

Ines,

Quill Hollow's last state review turned up a records finding, and the plot maps are still on paper. How do you check, today, which plots are sold and which are open?

Fennick Gardens, a beta cemetery, found 212 unsold plots in 90 days with PlotIQ's plot inventory (beta result, illustrative). Worth 15 minutes to see whether your maps show the same gap?

Emails 2 and 3 for this persona are omitted for length. They follow the same structure, with a different pain hypothesis in each.

**Step 7: Summary** BDR. Quill Hollow Memorial Park, GREENLIGHT. One contact found (champion). Targeting Ines Carmody (General Manager). Owner and pre-need contacts are unknown, so they are next. 1 persona x 3 emails = 3 sequence emails (2 more omitted). Call prep omitted for length. Recommended first action: Send Email 1 to Ines Carmody. Data quality: 5 CRM, 2 INFERRED, 1 UNKNOWN (illustrative counts for this example).

---

### Example 2: AE Quick Prep (Sable Fork Cemetery, Inbound, REVIEW)

**Context:** An AE has 20 minutes before an inbound discovery call. Sable Fork Cemetery asked for a demo through the website form after a search. The general manager, Arlen Biggs, signs contracts under $25K.

**Input:** "Quick call prep for Sable Fork Cemetery (they requested a demo from the website)."

**Step 0: Role Detection** User is AE. Quick Call Prep pattern detected. Skip sequence generation, deliver Steps 1-4 + Step 6 only.

**Step 1: Intelligence Gathering**
CRM search: New account (inbound form), status INBOUND, no active deal, no prior history. Requester's name and title: `[Unknown]`, so confirm on the call.

Company research: Sable Fork Cemetery, one site, 2,900 plots `[CRM]`. Plot list kept in a spreadsheet `[CRM]`. General Manager Arlen Biggs signs under $25K `[CRM]`. The search that led to the form is not recorded `[Unknown]`.

**Step 2: Account Snapshot**
ICP Quick-Score: **MANUAL REVIEW**
- Primary fit signal: Yes (2,900 plots, above the 2,000-plot threshold) `[CRM]`
- Multi-region: Single site, so no multi-region signal `[CRM]`
- Regulatory or complexity signal: Minimal (no state finding recorded) `[Unknown: not asked]`
- Scale: Single site, mid-size `[CRM]`
- Team complexity: Unknown. No records team is named `[Unknown]`

Why not GREENLIGHT: two of five signals are unknown. Zone ratings (illustrative) from `{Client Profile: Qualification Zones}`: Zone 3 HIGH (GM signs under $25K). Zone 1 MEDIUM (spreadsheet plot list). Zones 2, 4 and 5 UNKNOWN. One HIGH zone is the profile's REVIEW verdict.

**Step 4: Pain Hypotheses**
1. **Plot lookups in a spreadsheet** (A 2,900-plot list in a spreadsheet makes unsold plots hard to see. MEDIUM confidence. `[Inferred: spreadsheet plot list]`)
2. **Pre-need follow-up** (No pre-need activity is recorded, so this is a question to ask, not a hypothesis to lead with. LOW confidence. `[Unknown]`)
3. **Single-person records risk** (The plot list may depend on one person. LOW confidence. `[Unknown: no records owner named]`. Ask who maintains the list.)

**Step 6: Call Prep**
Call goal: "Confirm whether pre-need sales happen, measure a real plot lookup, and find out who signs under $25K."

30-Second Opener: "Thanks for asking for a demo. Before I show you anything, tell me what prompted you to look for plot records software this week."

Talk Track:
- "When someone asks for a plot, how long does it take to find it today?"
- "How many plots do you think are unsold right now, and how would you check?"
- "Do you sell pre-need, and where do those leads go when they come in?"
- "Who signs off on a purchase under $25K, and does anyone else need to see it?"

Objection prep: "We're happy with the spreadsheet" → "That makes sense. When did you last check the spreadsheet against the plots you have actually sold?"

**Step 7: Summary.** AE. Sable Fork Cemetery, MANUAL REVIEW (the profile's REVIEW verdict). Inbound request, no active deal. Quick call prep delivered. Recommended approach: Confirm pre-need (Zone 2) and plot lookup time (Zone 1) on the call, then re-score. A MANUAL REVIEW does not authorize outbound. Data quality: 3 CRM, 2 INFERRED, 3 UNKNOWN (illustrative counts for this example).

---

### Example 3: BDR Batch Mode (Rapid-Fire Prospecting Block)

**Context:** A BDR has a 2-hour prospecting block and needs snapshots for 5 accounts to identify the best 2-3 to pursue deeply. The list mixes accounts at different stages on purpose, so the table shows what the batch does with each one.

**Input:** "Quick snapshots on these 5 accounts for my outbound block: Corrow Ridge Cemetery, Greyfield Memorial Park, Tamsin Vale Cemetery, Northvale Memorial Holdings, Lowmoor Memorial Gardens."

**Rapid-Fire Batch Mode activated.** Running abbreviated snapshots (Steps 1-4 only) for each, producing a ranked summary table. Plot counts are from the cast. Zone ratings are illustrative.

| Account | ICP Verdict | Plots | Top Pain | Next Step | Priority |
|---------|------------|-------|----------|-----------|----------|
| Corrow Ridge Cemetery | GREENLIGHT | 14,000 | Paper plat maps and a double-recorded deed (illustrative) | Trigger Event Outbound: new owner four months ago | 1 |
| Greyfield Memorial Park | GREENLIGHT | 9,000 | Pre-need and records wanted together | Competitive Displacement: Stonemark contract renews January 2027 | 2 |
| Tamsin Vale Cemetery | MANUAL REVIEW (REVIEW in the profile) | 4,200 | Paper maps and one binder per section | Hold. Confirm who signs (Zone 3 is not HIGH) | 3 |
| Lowmoor Memorial Gardens | LOST, re-scored REVIEW | 7,500 | Closed-lost to Oldgate on "timing" | Route to Closed-Loss Reactivation (05). Do not sequence from this table | 4 |
| Northvale Memorial Holdings | DISQUALIFY (OUT) | Not applicable (240 funeral homes, 90 cemeteries) | None. Own in-house system | Do not prospect | 5 |

**Recommendation:** Generate full sequences for Corrow Ridge (#1) and Greyfield (#2) first. Greyfield's Stonemark renewal is the time pressure. Hold Tamsin Vale (#3) until its decision maker is known. Send Lowmoor to the reactivation skill, because it is a closed-lost account and not a cold prospect. Drop Northvale from the queue.

Full sequences generated for the top 2 accounts. Tamsin Vale held pending a decision-maker check. Lowmoor routed to 05. Northvale removed.

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

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example errors fixed and a non-success example added.
- Lien-state tier wording replaced with vertical-neutral labels

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying an embedded Client Profile block (one profile powers every skill)
- Framework machinery (evidence grading, speed vs. depth trade-offs, confidence calibration, ICP Quick-Score dimensions) moved to an explicit Methodology section with `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats
- Prior release notes (2026-03-04): Added Epistemic Rules section with evidence grading framework. Added ICP Quick-Score scoring matrix
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
