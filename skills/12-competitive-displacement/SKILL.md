---
name: gtm-competitive-displacement
description: "Generates targeted outbound sequences to displace a known incumbent (classifies the incumbent, loads competitor-specific failure patterns and displacement proof points, identifies gaps, and produces persona-tailored 4-step email sequences with competitive hooks, discovery questions, and objection handling)"
version: 1.2.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [competitive-displacement, incumbent-displacement, competitive-outbound, competitor-takeout, displacement-sequences]
requires:
  skills: []
---

# Competitive Displacement Outbound

## Overview

Outbound sequences designed to displace a known incumbent. Classifies the incumbent type, loads competitor-specific failure patterns and verified displacement proof points, identifies gaps between the incumbent and your product, and produces persona-tailored 4-step email sequences with competitive hooks, discovery questions, and objection handling. Best when you know what the account currently uses.

**Core Principle:** Never attack a competitor directly. Lead with what your product enables, not what the competitor lacks. The prospect chose their current tool for a reason. Respect that decision while surfacing the gaps they may not realize they have.

---

## Role

You are a **competitive outbound specialist generating displacement sequences**, not a generic email writer. You classify the incumbent, load competitor-specific failure patterns and displacement proof points, identify gaps between the incumbent and your product, and produce 4-step email sequences with competitive hooks that feel like genuine curiosity, not attacks. Everything company-specific (the competitors, the proof points) comes from the client profile (see **Context** below), so the same skill generates sequences for any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | Company you're targeting for displacement |
| Known incumbent | ✅ Required | Their current solution (or "unknown"; if unknown, run discovery first) |
| How incumbent identified | Optional | CRM notes, job posting, industry knowledge, etc. |
| User role | Optional | BDR or AE (if BDR + active AE deal exists, generates analysis only, not sequences) |
| Contacts at account | Optional | Known persona targets for sequencing |

---

## Output Contract

Every run produces either a **full displacement cheatsheet (standalone BDR sequences)** or a **displacement analysis (for active AE deals)**. The structure is fixed: incumbent profile + competitive gaps + persona-specific 4-email sequences + objection handling + summary. This consistency makes sequences reviewable and reusable across your team.

Core commitments: **incumbent classification + gap matrix + persona sequences (4 emails each) + discovery questions + objection handling + proof points**. These are organized into eight fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Account framing, vertical context |
| Buyer Personas | Persona selection for sequencing |
| Competitive Landscape | Competitor classifications, failure patterns, discovery questions, proof points |
| Value Propositions | Differentiation and displacement wedges |
| Proof Points | Displacement stories matched to incumbent type |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your displacement playbook. The frameworks below provide a structured approach to outbound sequences focused on competitive positioning and evidence grading. These are the defaults; they adapt to your sales methodology if different.

### Epistemic Rules

#### Evidence Grading
Every competitive claim must be graded and labeled:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified: Source]` | Confirmed across 2+ accounts or documented in CRM/reviews | Use in emails, talk tracks, proof points |
| **INFERRED** | `[Inferred: Basis]` | Logical conclusion from verified data, single account report | Use in discovery questions, hypotheses |
| **UNVERIFIED** | `[Unverified: Rumor/Single source]` | Heard once, not confirmed | Do NOT use in outbound; note as discovery target |

#### Competitive Intelligence Sourcing Rules
1. **Failure patterns must cite account evidence**. "Verified across 8+ accounts" is acceptable; "competitors often struggle" is not.
2. **Proof points must be labeled**. Customer name, metric, verification status.
3. **Discovery questions must be genuine curiosity**. If the question is really a statement in disguise, rewrite it.
4. **Never fabricate competitor weaknesses**. If intelligence is thin for a specific incumbent, acknowledge the gap and rely on category-level positioning.
5. **Displacement difficulty ratings are directional**. Medium-Low does not mean the deal is easy; it means the competitive positioning is favorable.

### Confidence Calibration
- **HIGH confidence**: Incumbent confirmed by CRM notes, discovery call, or prospect statement. Proceed with full displacement sequences.
- **MEDIUM confidence**: Incumbent suspected from job postings, industry knowledge, or partial CRM data. Proceed but note assumption; discovery questions should validate.
- **LOW confidence**: Incumbent is a guess. Do NOT run displacement. Use `gtm-account-snapshot` to discover first.

---

## Quick Reference

**Use this skill when:**
- You know the account uses a specific incumbent
- CRM notes or conversations mention a current vendor
- Account is evaluating alternatives to their current solution
- A competitor contract is up for renewal

**Don't use when:**
- You don't know what they're using (use `gtm-account-snapshot` to discover)
- The account is net-new with no incumbent intelligence (use `gtm-account-snapshot` or `gtm-research-outbound`)
- The account is closed-lost (use `gtm-closed-loss-reactivation`)

**User roles:** BDR, AE
**Expected time:** 15-25 minutes per account

---

## Epistemic Rules

### Evidence Grading
Every competitive claim must be graded and labeled:

| Grade | Label | Definition | Usage |
|-------|-------|------------|-------|
| **VERIFIED** | `[Verified: Source]` | Confirmed across 2+ accounts or documented in CRM/reviews | Use in emails, talk tracks, proof points |
| **INFERRED** | `[Inferred: Basis]` | Logical conclusion from verified data, single account report | Use in discovery questions, hypotheses |
| **UNVERIFIED** | `[Unverified: Rumor/Single source]` | Heard once, not confirmed | Do NOT use in outbound; note as discovery target |

### Competitive Intelligence Sourcing Rules
1. **Failure patterns must cite account evidence**. "Verified across 8+ accounts" is acceptable; "competitors often struggle" is not.
2. **Proof points must be labeled**. Customer name, metric, verification status.
3. **Discovery questions must be genuine curiosity**. If the question is really a statement in disguise, rewrite it.
4. **Never fabricate competitor weaknesses**. If intelligence is thin for a specific incumbent, acknowledge the gap and rely on category-level positioning.
5. **Displacement difficulty ratings are directional**. Medium-Low does not mean the deal is easy; it means the competitive positioning is favorable.

### Confidence Calibration
- **HIGH confidence**: Incumbent confirmed by CRM notes, discovery call, or prospect statement. Proceed with full displacement sequences.
- **MEDIUM confidence**: Incumbent suspected from job postings, industry knowledge, or partial CRM data. Proceed but note assumption; discovery questions should validate.
- **LOW confidence**: Incumbent is a guess. Do NOT run displacement. Use `gtm-account-snapshot` to discover first.

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` (BDR / AE)

**CRITICAL GUARD: BDR + Active Deal**
If `user_role = BDR` AND this account has an active deal owned by an AE:
- **STOP.** Do NOT generate displacement sequences for the BDR.
- Produce the displacement analysis (Steps 1-2) and deliver with guidance: "Active deal owned by [AE name] at [Stage]. Share displacement intelligence with [AE name]. They should decide how to use it in their deal strategy."
- Skip sequence generation. Proceed directly to summary.

---

### Step 1: Identify the Incumbent + Gather Context

#### 1a. Confirm Inputs
- Company name
- Known incumbent tool/vendor (or "suspected manual process")
- How we know (CRM note, prospect mentioned it, job posting, conference conversation)
- Any known pain with the incumbent (if available)
- Confidence level in the incumbent identification (HIGH / MEDIUM / LOW)

#### 1b. Search CRM
Pull everything available: account record, deal stage, owner, contacts, BDR Owner, engagement history, previous deal outcomes, notes mentioning vendor/competitor.

**Key extraction targets:**
- Any direct competitor mentions in notes, emails, or call transcripts.
- Prior deal outcomes. Was the account previously won, lost, or stalled?
- Contact engagement level. Who is active, who has gone dark?
- Contract timing signals. Renewal dates, contract length mentions.
- Pain signals. Any documented frustration with current tools.

#### 1c. Classify the Incumbent
Use `{Client Profile: Competitive Landscape}` to classify the incumbent by category, displacement difficulty, and primary advantage.

#### 1d. Assess Displacement Readiness
Rate the account's readiness for displacement:

| Signal | Assessment |
|--------|-----------|
| Known pain with incumbent | Yes (specific) / Suspected / Unknown |
| Contract status | Month-to-month / Expiring within 6mo / Locked (12mo+) / Unknown |
| Champion identified | Yes (name) / Partial / No |
| Budget cycle alignment | In cycle / Off cycle / Unknown |
| Previous evaluation of your product | Yes / No |

---

### Step 2: Load Competitor-Specific Intelligence

Based on the incumbent classification, load the detailed intelligence from `{Client Profile: Competitive Landscape}`:
- Failure patterns / weaknesses
- Discovery questions that expose gaps
- Objection handling specific to this competitor
- Displacement proof points from similar switches

Build a **competitive gap matrix**:

| Capability | [Incumbent] | Your Product | Why It Matters |
|-----------|-------------|--------------|----------------|
| [Key capability 1] | [gap] | [strength] | [Account-specific relevance] |
| [Key capability 2] | [gap] | [strength] | [Account-specific relevance] |
| ... | ... | ... | ... |

The "Why It Matters" column must connect each gap to the specific account's situation, not generic competitive positioning.

---

### Step 3: Generate Displacement Sequences

Produce a **4-step displacement sequence** for each recommended persona (typically 2-3, not all).

#### Persona Selection by Incumbent

| Incumbent | Primary Persona | Secondary Personas |
|-----------|----------------|-------------------|
| Direct Software | [Functional Lead] | [Manager], [Operations Lead] |
| Adjacent Platform Only | [VP Finance/Ops] | [Functional Lead], [CFO] |
| BPO / Service Bureau | [Functional Lead] | [Manager] |
| Manual / Spreadsheets | [Manager] | [Functional Lead], [CFO] |
| No Program | [CFO] | [Functional Lead] |

#### Rules for Every Email
- Include a **subject line**
- Body **<= 120 words**
- **NEVER name the competitor in the subject line**
- **First line must reference something specific about the prospect**, not generic.
- Each step uses a different displacement angle
- Proof points must match prospect's vertical and size
- If a known contact exists, address by name
- All competitive claims must be VERIFIED grade (see Epistemic Rules)

#### Sequence Structure (Per Persona)

| Step | Angle | Purpose |
|------|-------|---------|
| **Email 1** | Industry trend + implicit gap | Reference a macro trend that makes incumbent limitations more costly. Don't attack, create context. |
| **Email 2** | Capability gap question | Ask a question their incumbent can't answer well. Let them discover the gap. |
| **Email 3** | Proof point from comparable company | Reference a customer who made the same switch, with specific metrics. |
| **Email 4** | Breakup + contract timing | Acknowledge existing vendor. Ask when contract renews. Frame as "worth 15 minutes before your next renewal." |

#### After Each Persona Sequence, Include:
- Displacement angle for this persona (1 line)
- Best discovery question (1 bullet) from the incumbent-specific list
- Why this persona was selected for this specific displacement scenario (1 line)

---

### Step 4: Summary Report

1. **Company**: Name + incumbent identified
2. **Incumbent Category**: From classification
3. **Displacement Difficulty**: Assessment
4. **Displacement Readiness**: From Step 1d assessment
5. **CRM Status**: Existing contacts, deal history, current owner
6. **Personas Targeted**: Which 2-3 and why
7. **Sequences Generated**: [Count] personas x 4 emails
8. **Strongest Opening**: Highest-impact first line
9. **Key Displacement Lever**: Single most important gap the incumbent can't fill
10. **Contract Timing**: Known or unknown. If unknown, Email 4 asks.
11. **User Role**: BDR / AE
12. **Coordination Note**: BDR + active deal guidance if applicable
13. **Evidence Grade**: Confidence in competitive intelligence used (VERIFIED / INFERRED / UNVERIFIED)

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default): `[COMPANY]_Displacement.md`
- **Option B: HTML**: Styled cheatsheet with incumbent badge and gap matrix
- **Option C: PDF**: Python + reportlab, single page, letter size

### Cheatsheet Sections (8 Sections)
1. **Company + Incumbent Snapshot**: Firmographics, incumbent, category, displacement difficulty, contract status
2. **Competitive Gap Matrix**: Side-by-side capability comparison
3. **Key Personas**: CRM contacts filtered to target personas, flagging anyone who mentioned incumbent
4. **Displacement Hooks**: 6 talk-track-ready angles (complete sentences BDR can read verbatim)
5. **Discovery Questions**: Gap-exposing questions that feel like genuine curiosity
6. **Product vs. Incumbent**: Primary advantage, quantified wedge, 2-3 matched proof points
7. **Objection Handling**: Competitor-specific: "happy with incumbent," "switching is risky," "locked into contract," "cheaper"
8. **Call Flow**: Displacement-focused 5-step talk track

**Include INCUMBENT BADGE at top** (e.g., "Current: [Competitor Name]").

---

## Examples

### Example 1: Direct Competitor Displacement (Enterprise Account)

**Context:** Corvane Industrial (enterprise account using Competitor X), team frustrated with manual invoice review. CRM shows 3 contacts, no active deal.

**Input:** "Corvane Industrial uses Competitor X. Build displacement sequences."

**Step 1. Identify Incumbent:** CRM search finds existing account with 3 contacts: Sam Okafor, Head of Legal Operations (last active 45 days ago), a Manager (last active 90 days ago), an Operations Lead (no activity). Incumbent: Competitor X. How we know: AE notes from January mention frustration with manual processing. Confidence: HIGH.

**Step 1d. Displacement Readiness:**
- Known pain: Yes. "Frustration with manual processing" [CRM note]
- Contract status: Unknown
- Champion: Partial. Sam Okafor most engaged
- Budget cycle: Unknown
- Previous evaluation: No

**Step 2. Load Intelligence:** Incumbent classified as Direct Software (legacy e-billing), Medium-Low difficulty. Failure patterns loaded: broken automation promises, manual invoice processing bottleneck, service decline post-acquisition, single-model architecture. Competitive gap matrix built with 5 rows. Most relevant proof points: Apex Legal (enterprise displacement with 20% invoice review automation year one), Northgate Foods (real-time processing, $340K overbilling caught in 90 days).

**Step 3. Sequences:** Persona selection: Head of Legal Operations (primary), Manager, Operations Lead. Each gets a 4-step sequence (12 emails total).

**Head of Legal Operations. Email 1 (Industry Trend):**
Subject: Legal ops automation after recent rate environment shift

Sam, Corvane's footprint across 60+ outside counsel firms means your counsel spend complexity is only growing. With legal departments facing rate increases and increased scrutiny, companies that centralize invoice review on an automated platform are pulling ahead of those still reviewing manually.

Curious how your team is handling invoice review across all your firms today?

Jordan

**Step 4. Summary:** 3 personas targeted, 12 emails generated. Key displacement lever: Invoice processing automation (2+ weeks to real-time). Strongest entry: Head of Legal Operations with "invoice automation" angle. Contract timing: Unknown. Email 4 probes renewal window. Evidence grade: HIGH (verified across 8+ accounts).

---

### Example 2: Manual Process Displacement (PE-Backed Mid-Market Account)

**Context:** Ardent Insurance Group (PE-backed mid-market account, $1.1B carrier, managing outside counsel spend via spreadsheets). No CRM history. BDR researching for prospecting block.

**Input:** "Ardent Insurance Group uses spreadsheets for counsel spend management. Build displacement outbound."

**Step 0. Role Detection:** User is BDR. CRM check: no active AE deal. Clear to proceed with full sequences.

**Step 1. Identify Incumbent:** Incumbent: Manual/Spreadsheets (Low difficulty). How we know: Job posting for "Analyst" mentions "Excel-based tracking" and "deadline management." Confidence: MEDIUM (inferred from job posting, not confirmed by prospect). Company research reveals: $1.1B revenue, multi-state insurance carrier, 17 in-house attorneys. No contacts in CRM.

**Step 1d. Displacement Readiness:**
- Known pain: Suspected. Job posting language suggests capacity strain [Inferred]
- Contract status: N/A (no vendor contract)
- Champion: No. No contacts in CRM
- Budget cycle: Unknown (public company, likely calendar year fiscal)
- Previous evaluation: No

**Step 2. Load Intelligence:** Incumbent classified as Manual Process, Low difficulty. Gap matrix built: single-point-of-failure risk (critical at multi-state scale), no audit trail, no automation across counsel firms, no scalability path. Proof points matched: Meridian-class manufacturer ($2.1B, multi-state, 17+ attorneys trained), Northgate Foods (manual process displacement, spreadsheet to platform).

**Step 3. Sequences:** Persona selection: Manager (primary, closest to daily pain), Head of Legal Ops, CFO. No known contacts. Emails use title-based personalization. Each gets a 4-step sequence (12 emails total).

**Manager. Email 1 (Pain Hypothesis):**
Subject: Tracking counsel spend across multi-state operations

Managing outside counsel spend across 17+ attorneys in multi-state operations is complex when done with spreadsheets. It gets harder every time Ardent opens a new location.

One missed billing deadline in a high-risk state could mean significant financial exposure on a six-figure engagement.

How does your team currently track what's being billed across all your outside counsel without manual audits?

[Rep name]

**Step 4. Summary:** 3 personas targeted, 12 emails generated. Key displacement lever: Single-point-of-failure risk (one person managing all outside counsel spend). Strongest entry: Manager with "what happens when your expert is out" angle. Evidence grade: MEDIUM (incumbent inferred from job posting). Recommendation: Discovery questions in sequence should validate the spreadsheet assumption before investing further.

---

### Example 3: BPO Displacement (Regional Account with Active AE Deal)

**Context:** BDR finds intelligence that Pinecrest Hospitality ($620M, 9 attorneys) uses LedgerLine Audit (outsourced legal bill review service). Account has an active AE deal at Discovery stage.

**Input:** "Pinecrest Hospitality uses LedgerLine Audit for legal bill review. I want to build displacement sequences."

**Step 0. Role Detection:** User is BDR. CRM check: Active deal owned by Priya Nair at Discovery stage, $65K, created 3 weeks ago.

**ACTIVE DEAL GUARD TRIGGERED.** BDR cannot send independent displacement sequences on an active AE deal. Generating displacement analysis only (Steps 1-2).

**Step 1-2. Analysis Delivered:**
- Incumbent: LedgerLine Audit (BPO/Service Bureau, Medium difficulty)
- Gap matrix: No visibility platform vs. real-time dashboards, human-dependent review vs. automated, findings after payment vs. real-time prevention, service bureau dependent vs. in-house control
- Discovery questions for AE: "What visibility do you have into your invoice pipeline right now? Real time?" / "How do you audit the accuracy of what LedgerLine does on your behalf?"
- Best proof point: Beacon Health (similar scale, switched from service bureau, real-time visibility on $8M counsel spend, 92% first-pass compliance in 2 quarters)

**Coordination Guidance:** "Active deal owned by Priya Nair at Discovery. Share this displacement intelligence with Priya and let her decide how to incorporate it into discovery calls. The LedgerLine Audit-specific discovery questions are particularly valuable for the next conversation."

---

## Common Patterns

### Pattern: BDR Active Deal Guard
**When:** `user_role = BDR` and account has active AE deal.
**Action:** Generate analysis only (Steps 1-2). Skip sequence generation. Deliver intel to AE. "Active deal owned by [AE name] at [Stage]. Share displacement intelligence. Do not send sequences independently."

### Pattern: Unknown Incumbent
**When:** User suspects a competitor but isn't certain.
**Action:** Run `gtm-account-snapshot` first to discover the incumbent through CRM notes, job postings, or discovery questions. Then return to displacement with confirmed intelligence.

### Pattern: Dual-Tool Pain
**When:** Account uses two separate tools (e.g., Competitor A for one function + Competitor B for another).
**Action:** Build displacement around the unification angle. Reference proof points where your product replaced both tools simultaneously.

### Pattern: Contract Renewal Window
**When:** Contract renewal date is known or estimated.
**Action:** Time the displacement sequence to arrive 60-90 days before renewal. Adjust Email 4 from "when does your contract renew?" to "with your renewal in [month], now is the right time to evaluate."

---

## Troubleshooting

### "We don't have competitive intelligence for this incumbent"
**Solution:** Classify as "Unknown Incumbent." Use general displacement principles: lead with macro trends, ask capability gap questions, reference proof points from similar switches. Build competitive intelligence from the discovery call. Tag all claims as `[Inferred: category-level]` per Epistemic Rules.

### "The prospect is in an active contract"
**Solution:** Email 4 is specifically designed to surface contract timing. If contract timing is known, align the sequence cadence to arrive 60-90 days before renewal. If unknown, the sequence discovers it. Do not frame the outreach as "break your contract". Frame it as "evaluate before your next renewal."

### "BDR wants to send displacement sequences on an AE's active deal"
**Solution:** This is blocked by the Active Deal Guard in Step 0. The BDR should share displacement intelligence with the AE, not send independent sequences. The AE decides how to use competitive intel in their deal strategy.

### "Incumbent confidence is MEDIUM. Should we still run displacement?"
**Solution:** Yes, but adapt the approach. Frame discovery questions to validate the incumbent assumption before going deep on competitive positioning. Email 1 should use a broader industry angle that works regardless of the specific tool. Email 2 should include a question that surfaces what they actually use: "How does your team handle [domain] today?"

### "Multiple contacts at the account mentioned different tools"
**Solution:** The account may use different tools across divisions or branches. Build displacement around the primary incumbent (most frequently mentioned), but include a discovery question about tool standardization: "Are all locations using the same approach, or does it vary by region?" This can uncover a consolidation opportunity.

---

## Best Practices

### Do's
- **Lead with enablement, not criticism**. "Here's what's possible" beats "Here's what's broken."
- **Use displacement proof points**. Stories from companies who made the same switch are the most powerful.
- **Ask gap-exposing questions**. Genuine curiosity surfaces pain better than accusations.
- **Address contract timing**. Every displacement sequence should discover or leverage renewal windows.
- **Grade your evidence**. Tag claims as VERIFIED, INFERRED, or UNVERIFIED per Epistemic Rules.
- **Personalize the gap matrix**. Connect each gap to this specific account's situation, not generic positioning.

### Don'ts
- **Don't name competitors in subject lines**. Unprofessional and triggers spam filters.
- **Don't bash the prospect's decision**. They chose their current tool for reasons; respect that.
- **Don't assume incumbent pain**. Let discovery questions surface it naturally.
- **Don't send displacement sequences as BDR on active AE deals**. Coordinate through the AE.
- **Don't use UNVERIFIED competitive claims in outbound**. Only VERIFIED and INFERRED claims belong in emails.
- **Don't use the same displacement angle twice**. Each email must use a different competitive hook.

### Quality Checklist
- [ ] Competitor never named in subject lines
- [ ] Tone is "we enable" not "they lack"
- [ ] Each email uses different displacement angle
- [ ] Proof points match prospect's vertical and size
- [ ] Discovery questions expose real gaps
- [ ] Contract timing addressed (Email 4 asks if unknown)
- [ ] All emails <= 120 words
- [ ] Role detected; BDR + active deal guarded
- [ ] Evidence graded per Epistemic Rules (VERIFIED / INFERRED / UNVERIFIED)
- [ ] Gap matrix includes "Why It Matters" column specific to account

---

## Integration with Other Skills

- **`gtm-account-snapshot`**. Run first when incumbent is unknown; snapshot may discover it.
- **`gtm-competitive-strategy`**. For full battlecard generation across an entire competitive landscape, not just account-level displacement.
- **`gtm-research-outbound`**. When displacement target is a public company, combine financial intelligence with competitive angles.
- **`gtm-trigger-event-outbound`**. When a competitor contract event or vendor dissatisfaction signal triggers the displacement opportunity.
- **`gtm-deal-pulse`**. Once displacement creates a pipeline opportunity, monitor deal health.

---

## Changelog

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (Epistemic Rules, Confidence Calibration) moved to an explicit Methodology section with `{Methodology: X}` references
- No functional changes to the workflow, examples, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release (migrated from competitive displacement skill)
- Generalized via Client Profile block with configurable defaults
- Preserved all competitor intelligence structure, failure patterns, discovery questions, and proof points
- Maintained BDR Active Deal Guard pattern
- Multi-format artifact generation replacing reportlab-only
