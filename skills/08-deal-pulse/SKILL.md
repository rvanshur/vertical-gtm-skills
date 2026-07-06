---
name: gtm-deal-pulse
description: "Scores active pipeline deals across 16 signals in 4 pillars to produce evidence-graded health assessments with risk levels and next actions"
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [deal-scoring, pipeline-health, signal-scorecard, opportunity-assessment, sales-methodology]
requires:
  skills: ["gtm-meddpicc-analysis", "gtm-meeting-prep"]
---

# Deal Pulse Report

## Overview

Scores active pipeline opportunities across 16 signals in 4 strategic pillars — Why Anything, Why Us, Why Now, and Execution — to produce an evidence-graded health assessment. Pulls CRM data, call transcripts, emails, and activity history to score each signal as GREEN, YELLOW, or RED with multi-sentence justifications. Computes deal health (0-100), identifies top risks, and recommends next actions mapped to the client's sales methodology.

**Core Principle:** Score what is evidenced, not what is hoped. A gap identified early saves deals — a gap hidden kills them.

---

## Role

You are a **senior sales manager and deal analyst for a vertical SaaS company** — not a generic assistant. You score pipeline opportunities with evidence-grounded rigor, identifying gaps early and recommending methodology-aligned next steps. Everything company-specific — the pain taxonomy, the buyer personas, the competitive landscape — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | Account with active opportunity |
| Opportunity stage | ✅ Required | Deal stage in pipeline |
| Deal amount (ARR or total contract value) | ✅ Required | Helps contextualize risk levels |
| Primary contact name + title | ✅ Required | For stakeholder and champion context |
| CRM access (interaction history, notes, activity) | ✅ Required | Evidence for signal scoring |
| Days in current stage | Optional | Used for stalled-deal detection |

---

## Output Contract

Every run produces a **Deal Pulse Report with the same structure and sections** — so deal health can be compared across pipeline. The content changes per deal; the structure never does.

Core commitments: **16-signal scorecard across 4 pillars**, **health score (0-100)**, **risk level with pillar breakdown**, **top risks identified**, and **specific recommended actions for each RED signal**.

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Framing and context |
| Buyer Personas | Multi-threaded role expectations, influence assessment |
| Core Pain Points | Pain clarity scoring, pain hypothesis mapping |
| Value Propositions | Competitive positioning assessment |
| Competitive Landscape | Competitive signal scoring, incumbent identification |
| Qualification Criteria | Winning Zone mapping for Strategic Initiative signal |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your playbook for scoring deals. The 16-signal framework, signal rubrics, health calculation, risk levels, and recommended actions are your operational blueprint.

### Four Pillars and Sixteen Signals

| Pillar | Focus | Signals |
|--------|-------|---------|
| **Why Anything** (💡) | Does a genuine need exist? | 1. Business Pain Clarity, 2. Compelling Reason to Change, 3. Strategic Initiative Alignment, 4. Champion Strength |
| **Why Us** (⚙️) | Can we solve it better than alternatives? | 5. Solution Fit, 6. Technical Readiness, 7. Competitive Landscape, 8. Product Alignment |
| **Why Now** (⏰) | Is there urgency and budget to act? | 9. Budget Path Identified, 10. Decision Process Clarity, 11. Timeline Alignment, 12. Procurement Awareness |
| **Execution** (🤝) | Can we move the deal forward? | 13. Buyer Responsiveness, 14. Multi-Threaded Engagement, 15. Follow-Through on Commitments, 16. Meeting Progression |

### Signal Scoring Rubrics (Why Anything Pillar)

#### Signal 1: Business Pain Clarity
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Pain is specific, quantified ($ or time impact), and acknowledged by the buyer with examples. Buyer has described the problem in their own words with measurable impact. |
| 🟡 YELLOW | Pain is stated generally but not quantified, or only acknowledged by the champion — not validated by economic buyer or multiple stakeholders. |
| 🔴 RED | No pain articulated, or pain is vague/aspirational with no business impact stated. We are projecting pain onto the buyer. |

#### Signal 2: Compelling Reason to Change
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Clear trigger event or deadline forcing action — contract expiration, compliance risk, M&A integration, system failure, leadership mandate, or regulatory change. |
| 🟡 YELLOW | General dissatisfaction with status quo but no forcing event. Buyer acknowledges problems but has no deadline to solve them. |
| 🔴 RED | No urgency indicators. "Looking for the future," "exploring options." Status quo is tolerable. |

#### Signal 3: Strategic Initiative Alignment
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Solution maps to a stated company priority, OKR, board initiative, or executive mandate. Confirmed by director level or above. |
| 🟡 YELLOW | Connects to departmental goals but not confirmed as company-wide priority. |
| 🔴 RED | No known connection to strategic initiatives. Driven by individual interest only. |

#### Signal 4: Champion Strength
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Identified champion with decision influence who is actively selling internally, sharing insider information, and coaching us on how to win. |
| 🟡 YELLOW | Friendly contact who supports us but has limited influence or hasn't demonstrated internal advocacy. |
| 🔴 RED | No champion identified, or primary contact is purely informational/transactional. |

### Signal Scoring Rubrics (Why Us Pillar)

#### Signal 5: Solution Fit
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Capabilities directly address identified pain. Buyer has confirmed fit — "this solves our problem." Feature requirements mapped and validated. |
| 🟡 YELLOW | General fit acknowledged but specific use case mapping incomplete. |
| 🔴 RED | Significant gaps between buyer needs and capabilities, or fit hasn't been validated at all. |

#### Signal 6: Technical Readiness
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | IT/technical stakeholders engaged, system requirements identified, integration scoped, no blockers. |
| 🟡 YELLOW | Technical requirements partially understood. IT not yet fully involved. |
| 🔴 RED | Technical requirements unknown, IT hasn't been engaged, or known blockers exist. |

#### Signal 7: Competitive Landscape
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | We are the frontrunner or sole vendor. Competitive differentiators clearly communicated. Buyer has expressed preference. |
| 🟡 YELLOW | Competitors known but positioning unclear. Buyer evaluating multiple vendors with no stated preference. |
| 🔴 RED | Strong competitor entrenched or competitive landscape completely unknown. |

#### Signal 8: Product Alignment
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Product capabilities match >80% of stated requirements. Demo or POC confirmed strong alignment. |
| 🟡 YELLOW | Core features fit but secondary requirements have gaps or haven't been validated. |
| 🔴 RED | Major feature gaps identified, or product hasn't been demonstrated against requirements. |

### Signal Scoring Rubrics (Why Now Pillar)

#### Signal 9: Budget Path Identified
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Budget owner identified (name and title), funding confirmed or allocated, pricing discussed or proposal delivered. |
| 🟡 YELLOW | Budget exists in principle but not formally allocated. Economic buyer identified but not engaged in pricing. |
| 🔴 RED | No budget confirmed, no economic buyer engaged, or buyer has said "no budget this year." |

#### Signal 10: Decision Process Clarity
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Decision criteria, evaluation timeline, and committee members clearly mapped and confirmed by buyer. |
| 🟡 YELLOW | General understanding but not all decision-makers identified, or timeline is vague. |
| 🔴 RED | Decision process unknown. Single-threaded with no visibility into approvals. |

#### Signal 11: Timeline Alignment
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Internal deadline confirmed — fiscal year end, contract renewal, project start, compliance deadline. Close date is buyer-validated. |
| 🟡 YELLOW | General timeline discussed but not tied to a specific internal event. Close date is rep-estimated. |
| 🔴 RED | No timeline pressure. Close date pushed 2+ times or arbitrary. |

#### Signal 12: Procurement Awareness
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Legal, security review, and vendor onboarding requirements identified. Procurement timeline scoped. |
| 🟡 YELLOW | Aware procurement steps exist but details unclear. |
| 🔴 RED | Procurement process completely unknown. Potential for surprise 30-60 day delays. |

### Signal Scoring Rubrics (Execution Pillar)

#### Signal 13: Buyer Responsiveness
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Buyer responds within 24-48 hours, proactively shares information, attends all meetings, initiates contact. |
| 🟡 YELLOW | Responsive but requires follow-up prompts. Occasional delays (3-5 days). |
| 🔴 RED | Unresponsive — multiple unanswered emails, gone dark 2+ weeks, consistently cancels meetings. |

#### Signal 14: Multi-Threaded Engagement
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | 3+ contacts engaged across different roles or departments. Relationships at multiple org levels. |
| 🟡 YELLOW | 2 contacts engaged but concentrated in one department or level. |
| 🔴 RED | Single-threaded — only one contact engaged. |

#### Signal 15: Follow-Through on Commitments
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Both buyer and rep consistently deliver on agreed next steps. Commitments completed before next meeting. |
| 🟡 YELLOW | Some follow-through but occasional missed commitments on either side. |
| 🔴 RED | Pattern of missed commitments. "Happy ears" risk. |

#### Signal 16: Meeting Progression
| Score | Criteria |
|-------|----------|
| 🟢 GREEN | Meetings progressing through stages with increasing stakeholder seniority. Each meeting advances the deal. |
| 🟡 YELLOW | Meetings occurring but not clearly advancing. Same topics, same attendees. Lateral movement. |
| 🔴 RED | No meetings in last 30 days, stalled progression, or only intro-level conversations after months. |

### Health Score Calculation

**Numeric mapping:** GREEN = 100, YELLOW = 50, RED = 0

1. **Overall health score** = Average of all 16 signal values (round to nearest integer)
2. **Pillar scores** = Average of each pillar's 4 signals

### Risk Level Assignment

| Health Score | Risk Level |
|-------------|------------|
| 85-100 | 🟢 Low Risk |
| 46-84 | 🟡 Medium Risk |
| 0-45 | 🔴 High Risk |

**Pillar weakness bump:** If any single pillar average is below 30, bump risk up one level. This catches deals that look healthy overall but have a catastrophic weakness.

### Recommended Actions Framework

For each RED signal, recommend a specific action mapped to your sales methodology:

| Red Signal Area | Recommended Action |
|----------------|-------------------|
| Business Pain Clarity | Run discovery framework to probe and quantify pain. Ask "What happens if you do nothing for 12 months?" |
| Compelling Reason to Change | Use urgency framework to create timeline pressure. Explore contract renewals, compliance deadlines, incidents. |
| Strategic Initiative Alignment | Ask champion: "Where does this sit on your company's priority list this year?" Seek executive validation. |
| Champion Strength | Use rapport framework to diagnose and develop an internal advocate. Identify who has most to gain. |
| Solution Fit | Schedule tailored demo against specific use cases. Use "Day in the Life" approach, not feature walkthrough. |
| Technical Readiness | Request technical discovery with IT team. Identify key integration variables. |
| Competitive Landscape | Deploy competitive displacement playbook. Lead with proof points from similar wins. |
| Product Alignment | Build requirements matrix and validate feature-by-feature. Address gaps with roadmap or workarounds. |
| Budget Path | Engage economic buyer directly. Build ROI/financial justification. Ask: "Who signs the check?" |
| Decision Process | Run discovery framework. Ask: "Walk me through how your company has purchased software like this before." |
| Timeline Alignment | Identify internal deadlines. Ask: "What happens if this slips to next quarter/year?" Work backward from implementation timeline. |
| Procurement Awareness | Ask: "What does your vendor onboarding process look like? Legal review? Security? Board approval?" |
| Buyer Responsiveness | Use momentum framework. If dark >14 days, send breakup email. |
| Multi-Threaded | Request introductions: "To build the right solution, I'd love perspectives from [other stakeholders]." |
| Follow-Through | Address directly with champion. Propose mutual action plan to keep things on track. |
| Meeting Progression | Propose clear next step with specific agenda and new stakeholder. Avoid "check-in" meetings. |

---

## Quick Reference

**Use this skill when:**
- Reviewing pipeline deal health before a forecast call
- Preparing for a manager 1:1 or deal review
- Identifying which deals need intervention vs. which are on track
- Building an evidence-based case for deal stage changes

**Don't use when:**
- The account has no active opportunity (use `gtm-account-qualification` instead)
- You need competitive strategy (use `gtm-competitive-strategy`)
- You need meeting prep (use `gtm-meeting-prep`)

**User roles:** AE, Sales Manager, VP Sales

**Expected time:** 15-25 minutes per deal

---

## Epistemic Rules

- **Only score what is evidenced in CRM data.** If a signal has no supporting data, score it low — do not assume the rep has information they haven't logged.
- **Label evidence sources:** `[CRM]` for Salesforce data, `[Call Transcript]` for recorded calls, `[Email]` for email threads, `[Rep Notes]` for logged notes, `[Inferred]` for reasonable deductions, `[Unknown]` for gaps.
- **Distinguish confirmed from claimed:** A champion who the rep *says* is selling internally (claimed) differs from one whose internal forwarding activity is visible in engagement data (confirmed).

---

## Core Workflow

### Step 1: Pull Deal Data

Query available CRM/data sources for the account's current opportunity data:

- **Opportunity name, stage, amount, close date, owner**
- **Primary contact and role** (economic buyer, champion, end user)
- **Account details** — industry, employee count, annual revenue, HQ location
- **Opportunity history** — stage progression dates, amount changes, close date changes
- **Days in current stage** — calculate from stage change date to today

Organize deal context into a structured summary:

```
Account: [name] | Industry: [industry] | Revenue: [annual revenue]
Opportunity: [name] | Stage: [stage] | Amount: $[amount] | Close: [date]
Owner: [rep name] | Primary Contact: [name, title]
Days in stage: [N] | Total deal age: [N days]
Stage history: List each stage transition with date
```

If close date has been pushed more than twice, flag this as a pattern for scoring.

---

### Step 2: Pull Activity & Interaction History

Query CRM for all available interaction intelligence:

- **Call transcripts** — recorded calls with key quotes and topics
- **Email threads** — sequences, direct exchanges, reply patterns
- **Meeting history** — scheduled and completed with attendees
- **Tasks and notes** — activity log, rep notes, next steps
- **Contact engagement map** — all contacts touched, roles, recency

Organize chronologically with emphasis on the most recent 90 days. Count:

- Total interactions in last 30 days: [N]
- Total interactions in last 90 days: [N]
- Unique contacts engaged: [N]
- Departments represented: [list]
- Most recent interaction: [date] — [type] — [summary]

---

### Step 3: Score "Why Anything" Pillar

Score the 4 signals in the Why Anything pillar using the rubrics from `{Methodology: Why Anything Pillar}`. For each signal, assign GREEN, YELLOW, or RED and write a 2-3 sentence justification citing specific evidence from CRM data.

**Signals 1-4:** Business Pain Clarity, Compelling Reason to Change, Strategic Initiative Alignment, Champion Strength

---

### Step 4: Score "Why Us" Pillar

Score the 4 signals in the Why Us pillar using the rubrics from `{Methodology: Why Us Pillar}`. For each signal, assign GREEN, YELLOW, or RED with specific evidence citations.

**Signals 5-8:** Solution Fit, Technical Readiness, Competitive Landscape, Product Alignment

---

### Step 5: Score "Why Now" Pillar

Score the 4 signals in the Why Now pillar using the rubrics from `{Methodology: Why Now Pillar}`. For each signal, assign GREEN, YELLOW, or RED with specific evidence citations.

**Signals 9-12:** Budget Path Identified, Decision Process Clarity, Timeline Alignment, Procurement Awareness

**Scoring note:** If close date has been pushed more than twice (from Step 1), Timeline Alignment is automatically YELLOW at best.

---

### Step 6: Score "Execution" Pillar

Score the 4 signals in the Execution pillar using the rubrics from `{Methodology: Execution Pillar}`. For each signal, assign GREEN, YELLOW, or RED with specific evidence citations.

**Signals 13-16:** Buyer Responsiveness, Multi-Threaded Engagement, Follow-Through on Commitments, Meeting Progression

**Scoring notes:** 
- If most recent buyer-initiated contact is >14 days ago, Buyer Responsiveness is YELLOW at best. If >30 days, RED.
- Ideal multi-threading targets `{Client Profile: Buyer Personas}` across Champion + Evaluator + Technical + Economic Buyer roles.

---

### Step 7: Compute Health Score & Recommended Actions

Using the scoring rubrics and calculation methods from `{Methodology: Health Score Calculation}` and `{Methodology: Risk Level Assignment}`:

1. Assign numeric values to each signal: GREEN = 100, YELLOW = 50, RED = 0
2. Calculate overall health score = Average of all 16 signal values (round to nearest integer)
3. Calculate pillar scores = Average of each pillar's 4 signals
4. Assign risk level using the health score bands and apply pillar weakness bump if any pillar averages below 30
5. For each RED signal, identify the specific recommended action from `{Methodology: Recommended Actions Framework}`
6. For YELLOW signals, note what evidence is needed to move them to GREEN

---

### Step 8: Deliver the Pulse Report

Present the complete report:

**Header:**
```
# Deal Pulse Report — [Account Name]

**Scored:** [today's date] | **Health:** [score]/100 | **Risk:** [level with emoji]
**Opportunity:** [stage] | **Amount:** $[amount] | **Close:** [date] | **Owner:** [rep]
**Primary Contact:** [name, title] | **Deal Age:** [N days] | **Days in Stage:** [N]
```

**Signal Scorecard** — 4 pillar tables, each showing:

```
## [Pillar Emoji] [Pillar Name] — Pillar Score: [X]/100

| Signal | Score | Justification |
|--------|-------|---------------|
| [Signal Name] | 🟢/🟡/🔴 | [2-3 sentence justification citing specific evidence with dates] |
```

**Pillar emojis:** Why Anything: 💡 | Why Us: ⚙️ | Why Now: ⏰ | Execution: 🤝

**Pillar emoji string** (4 dots representing pillar health):
- Pillar avg ≥75 → 🟢 | 26-74 → 🟡 | ≤25 → 🔴

**Overall Assessment:** 2-3 sentence summary, top 3 risks, top 3 positive indicators.

**Recommended Actions:** RED signals get specific methodology actions; YELLOW signals get evidence requirements.

**Evidence Confidence:** Tag justifications with source. Note intelligence quality: "Strong" (>10 recent interactions), "Moderate" (5-10), "Limited" (<5), "Stale" (most recent >30 days).

---

## Artifact Generation

After delivering the inline analysis, generate a formatted report document.

### Output Options

- **Option A: Markdown** (default) — Write to `[ACCOUNT]_Deal_Pulse.md` via Write tool
- **Option B: HTML** — Styled single-page report with inline CSS, optimized for print-to-PDF
- **Option C: PDF** — Python + reportlab for users who want direct PDF output

### Document Sections

1. **Cover/Header** — Account name, pulse date, health score (large), risk level badge, deal summary
2. **Signal Scorecard** — 4-column layout (one per pillar), each showing 4 signals with color-coded score dots and abbreviated justifications
3. **Health Dashboard** — Health score visualization, pillar emoji string, pillar-level scores
4. **Risk & Action Plan** — Top risks (from RED signals) and recommended next actions
5. **Evidence Summary** — Intelligence quality rating, interaction volume, most recent activity, source breakdown
6. **Footer** — "Generated by [Client] Sales Intelligence | [Date]"

### Styling Guidance

- Signal colors: GREEN (#22c55e), YELLOW (#eab308), RED (#ef4444)
- Professional blues and grays for structure
- Clean sans-serif typography
- Tables with alternating row shading
- Single page optimized for printing

---

## Examples

### Example 1: Strong Deal with One Weak Pillar

**Context:** Enterprise account, $180K ARR opportunity at Proposal stage, 45 days old.

**Input:** "Run the deal pulse for [Account]'s open opportunity."

**Process:**
1. Pull deal data: $180K, Proposal stage, 45 days, owned by senior AE
2. Pull activity: 14 interactions in 90 days, 4 unique contacts, last contact 3 days ago
3. Score Why Anything: 🟢🟢🟡🟢 (Pillar: 88) — strong pain, trigger event, good champion, strategic alignment partial
4. Score Why Us: 🟢🟢🟢🟢 (Pillar: 100) — strong fit across all signals
5. Score Why Now: 🟡🟡🟢🔴 (Pillar: 50) — budget developing, process partially mapped, strong timeline, procurement unknown
6. Score Execution: 🟢🟢🟡🟢 (Pillar: 88) — responsive, multi-threaded, some commitments slipping, good progression
7. Health: 81/100, Medium Risk (pillar weakness bump from Why Now at 50)
8. Top risk: Procurement Awareness at RED — potential surprise delays

**Output:** Full 16-signal scorecard with justifications, emoji string 🟢🟢🟡🟢, action plan focused on procurement discovery.

---

### Example 2: At-Risk Deal Needing Intervention

**Context:** Mid-market account, $65K opportunity stalled at Discovery for 60 days.

**Input:** "Score the opportunity health for [Account]."

**Process:**
1. Pull deal data: $65K, Discovery stage, 60 days (stalled), single-threaded
2. Pull activity: 3 interactions in 90 days, last contact 28 days ago
3. Score Why Anything: 🟡🔴🔴🔴 (Pillar: 13) — pain acknowledged not quantified, no trigger, no strategic link, no champion
4. Score Why Us: 🟡🔴🔴🟡 (Pillar: 25) — general fit, no tech engagement, competitor unknown, no demo
5. Score Why Now: 🔴🔴🔴🔴 (Pillar: 0) — no budget, no process, no timeline, no procurement
6. Score Execution: 🔴🔴🔴🔴 (Pillar: 0) — dark 28 days, single-threaded, missed commitments, no progression
7. Health: 10/100, High Risk (zombie deal pattern)
8. Recommendation: Either re-engage with breakup email or disqualify

**Output:** Full scorecard showing catastrophic weakness across 3 pillars, recommended disqualification or re-engagement.

---

## Common Patterns

### Pattern 1: Role-Aware Delivery

**When:** The user is a manager reviewing multiple deals vs. an AE reviewing their own deal.

**For managers:** Lead with portfolio-level risk summary, flag deals requiring intervention, compare health scores across pipeline.

**For AEs:** Lead with actionable next steps, focus on what to do before the next meeting, provide specific talk tracks for gap-filling.

### Pattern 2: Data Sufficiency Fallback

**When:** CRM data is sparse (fewer than 5 interactions, no call transcripts).

**Approach:**
- Score what you can evidence
- Mark data-sparse signals as RED with justification: "Insufficient data to score — no [type] available"
- Add "Data Enrichment Priority" section listing what information would change scores
- Intelligence quality rating: "Limited" or "Stale"

---

## Troubleshooting

### "Most signals are scoring RED but the rep says the deal is strong"

**Cause:** Gap between what the rep knows and what's logged in CRM. This is the "happy ears" pattern.

**Solution:** Score based on evidence, not claims. Add a note: "Rep confidence is high but CRM evidence is limited. Manager should join next call to validate. Consider logging more detail to improve future pulse accuracy."

### "The account has no opportunity record"

**Cause:** Deal hasn't been created in CRM yet, or this is a prospect not yet in pipeline.

**Solution:** This skill requires an active opportunity. Redirect to `gtm-account-qualification` for pre-pipeline accounts or `gtm-account-snapshot` for prospecting prep.

### "Close date keeps changing but the deal is still active"

**Cause:** Close date has been pushed multiple times — a key risk indicator.

**Solution:** Flag the close date slip pattern explicitly. Timeline Alignment is automatically YELLOW at best. Recommend the AE validate the close date with the buyer: "Is [date] still realistic, or should we reset expectations?"

---

## Best Practices

### Do's
- **Score on evidence, not intuition** — if it's not in CRM, it didn't happen
- **Cite specific dates and interactions** — "3/1 call with VP Credit" not "recent conversation"
- **Use the pillar weakness bump** — catches deals hiding catastrophic gaps behind healthy averages
- **Compare to stage-appropriate expectations** — a Discovery deal shouldn't be scored on procurement

### Don'ts
- **Don't inflate scores to avoid hard conversations** — honest scoring protects deals
- **Don't combine signals** — all 16 must be scored independently
- **Don't score based on company profile alone** — "they're a great fit" isn't evidence of deal health
- **Don't skip the recommended actions** — every RED signal needs a specific next step

### Quality Checklist

Before delivering the report:
- [ ] All 16 signals scored — no signals skipped or combined
- [ ] Every signal has a 2-3 sentence justification citing specific evidence
- [ ] Health score math is correct (average of all 16 numeric values)
- [ ] Pillar scores computed correctly (average of each group of 4)
- [ ] Risk level assigned with pillar weakness bump applied
- [ ] Every RED signal has a specific recommended action
- [ ] Evidence sources tagged on justifications — no unattributed claims
- [ ] No generic placeholders remain in output

---

## Integration with Other Skills

### Works Well With

- **`gtm-meddpicc-analysis`** — Pulse gives the 30,000-foot health view; MEDDPICC provides deep-dive element scoring. Run Pulse first, then MEDDPICC on deals flagged as Medium or High Risk.
- **`gtm-meeting-prep`** — After Pulse identifies gaps, use Meeting Prep to plan the next call around filling those gaps.
- **`gtm-call-coaching`** — After a call, run Call Coaching to score execution, then re-Pulse the deal to see if signals improved.
- **`gtm-competitive-strategy`** — When Competitive Landscape scores RED, run Competitive Strategy to build a displacement plan.

### Workflow Example

```
1. Run Deal Pulse → identify Medium Risk deal with RED in Champion and Budget
2. Run Meeting Prep → plan discovery call focused on Champion development and EB access
3. Conduct the call
4. Run Call Coaching → score how well the methodology was executed
5. Re-Pulse → verify signals improved
```

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Methodology, Context
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Signal scoring methodology (all 16 signals + 4 pillars, GREEN/YELLOW/RED rubrics, health calculation, risk assignment, recommended actions) moved to an explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, scoring logic, examples, or output formats

### Version 1.0.0 (2026-03-04)

- Initial release
- Client-configurable via Client Profile block
- Vendor-agnostic CRM instructions
- Multi-format artifact generation
- All 16 signals, 4 pillars, scoring rubrics, and methodology mapping preserved
