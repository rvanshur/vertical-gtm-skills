---
name: gtm-competitive-displacement
description: "Generates targeted outbound sequences to displace a known incumbent (classifies the incumbent, loads competitor-specific failure patterns and displacement proof points, identifies gaps, and produces persona-tailored 4-step email sequences with competitive hooks, discovery questions, and objection handling)"
version: 1.3.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-10-13
tags: [competitive-displacement, incumbent-displacement, competitive-outbound, competitor-takeout, displacement-sequences]
requires:
  skills: []
---

# Competitive Displacement Outbound

## Overview

Outbound sequences designed to displace a known incumbent. Classifies the incumbent type, loads competitor-specific failure patterns and labeled displacement proof points, identifies gaps between the incumbent and your product, and produces persona-tailored 4-step email sequences with competitive hooks, discovery questions, and objection handling. Best when you know what the account currently uses.

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
| Known incumbent | ✅ Required | Their current solution (or "unknown"). If unknown, run discovery first |
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

Your displacement playbook. The frameworks below provide a structured approach to outbound sequences focused on competitive positioning and evidence grading. These are the defaults. They adapt to your sales methodology if different.

The evidence grades, sourcing rules and confidence calibration are defined once, in the Epistemic Rules section below.

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
| **UNVERIFIED** | `[Unverified: Rumor/Single source]` | Heard once, not confirmed | Do NOT use in outbound. Note as discovery target |

### Competitive Intelligence Sourcing Rules
1. **Failure patterns must cite account evidence**. "Verified across 8+ accounts" is acceptable. "Competitors often struggle" is not.
2. **Proof points must be labeled**. Customer name, metric, verification status.
3. **Discovery questions must be genuine curiosity**. If the question is really a statement in disguise, rewrite it.
4. **Never fabricate competitor weaknesses**. If intelligence is thin for a specific incumbent, acknowledge the gap and rely on category-level positioning.
5. **Displacement difficulty ratings are directional**. Medium-Low does not mean the deal is easy. It means the competitive positioning is favorable.

### Confidence Calibration
- **HIGH confidence**: Incumbent confirmed by CRM notes, discovery call, or prospect statement. Proceed with full displacement sequences.
- **MEDIUM confidence**: Incumbent suspected from job postings, industry knowledge, or partial CRM data. Proceed but note the assumption. Discovery questions should validate it.
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

Produce a **4-step displacement sequence** for each recommended persona. The profile's Buyer Personas set the options, and the count is not fixed. Pick the personas that fit the incumbent and the account, usually two or three.

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

### Example 1: Pre-Need and Records Displacement, Stonemark at Greyfield Memorial Park

**Context:** Greyfield Memorial Park is a one-site cemetery with 9,000 plots (profile). It runs a digital map from Stonemark, and its three-person pre-need team takes requests through an intake form on the site. The Stonemark contract renews in January 2027. The account is TARGET, not yet contacted, and its verdict is GREENLIGHT (Zones 2 and 3 HIGH). No contact names are on file, so the sequence uses titles.

**Input:** "Greyfield Memorial Park uses Stonemark. Build displacement sequences."

**Step 0. Role Detection:** User is a BDR (illustrative). CRM check: no active AE deal. Clear to generate sequences.

**Step 1. Identify Incumbent:** Incumbent: Stonemark, Direct (enterprise cemetery mapping). How we know: the account's own notes name its map vendor (illustrative). Confidence: HIGH.

**Step 1d. Displacement Readiness:**
- Known pain: Yes. The pre-need team wants pre-need and records together (account notes, illustrative)
- Contract status: Expiring within 6 months. Renews January 2027
- Champion: Partial. The pre-need team lead, name not on file
- Budget cycle: Unknown
- Previous evaluation: No

**Step 2. Load Intelligence:** Stonemark is classified as Direct. Research estimates put its pricing at about $1,500 to $2,500 a month, with 90 to 120 days to live (profile, dated 2026-03-27). Gap matrix:

| Capability | Stonemark | PlotIQ | Why It Matters for Greyfield |
|---|---|---|---|
| Sold and unsold plots on the map | [Unverified: ask] | Plot inventory shows sold and unsold plots | The pre-need team needs to know which plots are free before it sells one |
| Pre-need leads | [Unverified: ask] | Pre-Need CRM and Lead Scoring | Leads from the intake form need a named follow-up owner |
| Records and trust compliance | [Unverified: ask] | Records and Trust Compliance module | The account wants pre-need and records together |
| Time to live | 90 to 120 days (research estimate) | 6 weeks (profile) | The January 2027 renewal sets the window |

Proof points: Fennick Gardens (212 unsold plots found in 90 days) and Holloway Hills (zero records findings in its first state review). Both are ILLUSTRATIVE beta results, not customer results, so neither can appear in an email yet.

**Step 3. Sequences:** Persona selection: Pre-Need Sales Manager (primary, the team that feels the intake pain) and Cemetery General Manager (secondary, the buyer). Each gets a 4-step sequence, 8 emails in total. Emails use titles, not names.

**Pre-Need Sales Manager. Email 1 (Industry Trend):**
Subject: Pre-need requests from the intake form

[Name], your team takes pre-need requests through the intake form on the site. Independent cemeteries capture pre-need on about 20% to 35% of at-need volume. The largest public operator reaches about 60% (deathcare research, March to April 2026).

How do the intake form requests get a first call back today?

[Your name]

**Email 3 status: HOLD.** Its proof point is illustrative. The profile says the Fennick Gardens case study waits until its numbers cover a full year (January 2027). Until then, Email 3 names no customer result.

**Step 4. Summary:** 2 personas, 8 emails. Key displacement lever: pre-need leads and records on one system. Contract timing: January 2027, known from the account notes, and Email 4 confirms it. Evidence grade: INFERRED. No competitor claim has reached VERIFIED, so the emails name no competitor claim.

---

### Example 2: Manual-Process Displacement, Tamsin Vale Cemetery (Non-Success)

**Context:** Tamsin Vale Cemetery is a one-site cemetery with 4,200 plots, paper plat maps and one binder per section. It has had two double sales in two years (illustrative). The account is TARGET, not yet contacted, and its verdict is MANUAL REVIEW (Zone 1 HIGH only). This is the non-success case: the displacement is easy to describe and hard to justify yet.

**Input:** "Tamsin Vale Cemetery runs paper plat maps. Build displacement sequences."

**Step 0. Role Detection:** User is a BDR (illustrative). CRM check: no active AE deal.

**Step 1. Identify Incumbent:** Incumbent: paper maps and binders, Manual / Spreadsheets. How we know: the GM's description on one call (illustrative). Confidence: MEDIUM. The process is known, but the double sales come from one conversation and are not yet in writing.

**Step 1d. Displacement Readiness:**
- Known pain: Suspected. The two double sales (illustrative) have not been counted in plots or dollars
- Contract status: Unknown. Manual process, so there is no vendor contract to time against
- Champion: No
- Budget cycle: Unknown
- Previous evaluation: No

**Step 2. Load Intelligence:** Manual process, classified as Low displacement difficulty. Gap matrix: no single view of sold and unsold plots (one binder per section), no audit trail, and key-person risk. The only proof point is Fennick Gardens, which is ILLUSTRATIVE and cannot be cited yet.

**Step 3. Sequences:** Persona selection: Cemetery General Manager, the primary persona for a manual process. The Operations Director is not on file. A CFO is not a fit for a single-site account (profile: the CFO role applies to groups). So the sequence has one persona, with 4 emails, not 8.

**Cemetery General Manager. Email 1 (Pain Question):**
Subject: Plot lookups across one binder per section

[Name], Tamsin Vale keeps its plot records in one binder per section. When a family asks about a plot in another section, how long does the lookup take?

[Your name]

**Step 4. Summary and recommendation (the non-success):** 1 persona, 4 emails drafted, 0 sent. Recommendation: hold the sequence. The verdict is MANUAL REVIEW, not GREENLIGHT, so Email 1 would put a double-sales claim in front of a buyer before anyone has confirmed it. Next step: a discovery call that asks for the two double sales in writing (plot numbers and dates) and names the person who decides. Release Email 1 only after both are in hand, because Zone 3 (decision speed) is still unknown. Evidence grade: INFERRED. If the double sales do not hold up, the displacement case is a guess, and it does not go out.

---

### Example 3: Active Deal Guard, Brackhaven Memorial Gardens

**Context:** A BDR (illustrative) finds that Brackhaven Memorial Gardens runs Oldgate Ledger Pro, with a renewal in March 2027. The account has an ACTIVE AE deal at Stage 5 Negotiate, owned by Owen Pruitt (illustrative assignment).

**Input:** "Brackhaven runs Oldgate. Build displacement sequences."

**Step 0. Role Detection:** User is BDR. CRM check: active deal owned by Owen Pruitt at Stage 5 Negotiate.

**ACTIVE DEAL GUARD TRIGGERED.** The BDR cannot send independent displacement sequences on an active AE deal. Generating displacement analysis only (Steps 1 and 2).

**Steps 1 to 2. Analysis Delivered:**
- Incumbent: Oldgate Ledger Pro (Direct, legacy on-premise). Confidence: MEDIUM. The March 2027 renewal is the only timing signal, and the GM stated it on one call (illustrative).
- Gap matrix: mobile use by the grounds crew (research estimate: poor mobile), unsold-plot visibility (not yet known, ask), and trust fund records (a deep accounting pitch, so show the state filing format).
- Discovery questions for the AE (both from the profile): "When does your software contract renew, and what did the last quote include for support?" and "Where does the plot map live today, and when was it last updated?"
- Proof point: Fennick Gardens is ILLUSTRATIVE and cannot be used yet.

**Coordination Guidance:** "Active deal owned by Owen Pruitt at Stage 5 Negotiate. Share this displacement intelligence with Owen and let him decide how to use the March 2027 renewal in his conversations with Ruth Ellery. Do not send sequences independently. The competitive strategy for this deal is in skill 11."

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
- **Don't bash the prospect's decision**. They chose their current tool for reasons. Respect that.
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
- [ ] Role detected. BDR + active deal guarded
- [ ] Evidence graded per Epistemic Rules (VERIFIED / INFERRED / UNVERIFIED)
- [ ] Gap matrix includes "Why It Matters" column specific to account

---

## Integration with Other Skills

- **`gtm-account-snapshot`**. Run first when incumbent is unknown. The snapshot may discover it.
- **`gtm-competitive-strategy`**. For full battlecard generation across an entire competitive landscape, not just account-level displacement.
- **`gtm-research-outbound`**. When displacement target is a public company, combine financial intelligence with competitive angles.
- **`gtm-trigger-event-outbound`**. When a competitor contract event or vendor dissatisfaction signal triggers the displacement opportunity.
- **`gtm-deal-pulse`**. Once displacement creates a pipeline opportunity, monitor deal health.

---

## Changelog

### Version 1.3.0 (2026-10-13)
- Examples re-cast on PlotIQ, the library's one example company. Example arithmetic and listed errors fixed, and a non-success example added.

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
