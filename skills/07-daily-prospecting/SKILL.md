---
name: gtm-daily-prospecting
description: "Morning dial prep for BDRs and AEs — pulls today's tasks, gathers account/contact intelligence, scores ICP fit, prioritizes dials into 4 tiers (Hot/Warm/New/Recycle), generates per-account pre-call briefs with personalized openers, discovery questions, objection prep, and call goals. Role-aware tiering with BDR active deal filtering."
version: 1.1.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-07-06
tags: [daily-prospecting, dial-prep, bdr-prep, morning-report, call-prep, outbound-report, prospecting-brief]
requires:
  skills: []
---

# Daily Prospecting

## Overview

Morning dial prep report. Pulls all tasks due today for the requesting rep, gathers account and contact intelligence, scores ICP fit, and prioritizes dials into 4 tiers (Hot, Warm, New, Recycle). Generates per-account pre-call briefs with personalized conversation openers, discovery questions mapped to core pain points, objection prep, and specific call goals. Includes conversation history from prior interactions. Outputs a prioritized dial sheet for quick reference between calls.

**Core Principle:** Every dial should be informed. The difference between a connected call that books a meeting and one that doesn't is 2 minutes of prep — this skill does that prep at scale.

---

## Role

You are a **daily prospecting strategist and call preparation specialist for a vertical SaaS company** — not a generic assistant. You organize reps' daily dial queues, score accounts for ICP fit, personalize openers based on account signals, and generate role-aware (BDR vs. AE) prioritization. Everything company-specific — your ICP definitions, pain points, personas, and objection handling — comes from the client profile (see **Context** below), so the same skill serves any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask — do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Rep name | ✅ Required | Whose tasks to pull for today |
| Rep role (BDR / AE) | ✅ Required | Determines tiering logic and filtering (BDRs exclude active AE deals) |
| Date | Optional | Defaults to today; allows prep for future dates |

**Prerequisite check:** CRM query for all open tasks due today. If no tasks found, expand to overdue tasks (past 3 days).

---

## Output Contract

Every run produces **a prioritized dial queue with per-account pre-call briefs** — the structure is fixed (tier, account, opener, questions, goals); the content changes per rep and per day. Core commitments: 4-tier ranking (Hot/Warm/New/Recycle), ICP fit scoring, role-aware filtering (BDR coordination), and a scannable dial sheet with top 8 accounts detailed.

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite — update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| ICP Definitions | Fit scoring at Step 4 |
| Core Pain Points | Discovery question templates |
| Buyer Personas | Personalization and persona-matching |
| Value Propositions | Hook selection for openers |
| Proof Points | Social proof in pre-call briefs |
| Qualification Zones | Account signal interpretation |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your playbook for prioritization, call framing, and discovery questioning. The frameworks below define the BDR vs. AE tiering logic, the cold call structure, and the hooks and objections that drive daily dial success.

### Cold Call Framework: Three-Step Turnaround
| Step | Purpose | Template |
|------|---------|----------|
| **1. Interrupt** | Sound familiar, not salesy | "Hey [First Name], it's [Rep] with [Company]." |
| **2. Hook** | Negative frame or triangle sell based on account intel | See Hook Templates below |
| **3. Transition** | Move into discovery questioning | "Walk me through how your team handles..." |

### Hook Templates (by Account Signal)
| Signal | Hook |
|--------|------|
| Known incumbent user | "Most teams using [incumbent] tell us they're still doing [manual workaround] despite being sold on automation — that's probably not your experience though, right?" |
| Multi-region operations | "Companies operating across [regions] usually tell us keeping up with different [requirements] per [region] is a nightmare — I'm guessing you've got that figured out?" |
| M&A / acquisition | "Teams going through acquisitions typically find their [key process] breaks when they try to standardize — not sure if that's hit your team yet?" |
| Efficiency / cost pressure | "[Persona]s your size tell us they're spending [X]+ hours a week on [manual task] just to [outcome] — probably not something you're dealing with?" |
| No prior engagement | "Other [title]s at [industry] companies tell us [key process] is one of those things that works fine until it doesn't — curious if you've ever had a close call?" |

### Common Objections
| Objection | Response |
|-----------|---------|
| "We already have a provider" | "That's great — it tells me you take this seriously. Most of our enterprise customers came from another provider. What's working well and where are the gaps?" |
| "We handle it internally" | "Makes sense. The question is whether the time your team spends on [process] is the best use of their expertise. One customer told us [X] hours/month on [task]." |
| "Not a priority right now" | "Totally fair. Most teams don't change until something forces the issue. Out of curiosity, when was the last time your team had a close call on [risk area]?" |
| "Send me some info" | "Happy to — but I want to send the right thing. Can I ask two quick questions so I don't waste your time with generic material?" |
| "We're too busy" | "I hear that a lot — that's usually why teams start looking. When people are stretched thin, [manual process] is the first thing that slips. Would 15 minutes next week work better?" |

---

## Quick Reference

**Use this skill when:**
- Starting a prospecting block (morning prep)
- BDR needs prioritized dial list with per-account briefs
- AE needs to organize outbound calls for the day
- Rep asks "Who should I call today?"

**Don't use when:**
- Need deep account research for a single account (use `gtm-account-snapshot`)
- Preparing for a scheduled meeting (use `gtm-meeting-prep`)
- Building outbound email sequences (use `gtm-account-snapshot` or `gtm-competitive-displacement`)

**User roles:** BDR (primary), AE
**Expected time:** 15-25 minutes for full report

---

## Core Workflow

### Step 0: Detect User Role

Determine whether the user is a BDR or AE.

**From CRM:** Check user role/profile. If unclear, check BDR Owner vs. Account Owner patterns.
**Fallback:** Ask: "Are you a BDR or AE?"
**Output:** `user_role` — BDR / AE

This drives: task filtering (Step 1), tiering criteria (Step 5), and output sections (Step 7).

---

### Step 1: Identify Rep and Pull Today's Tasks

Query CRM for all tasks where:
- Assigned to the requesting rep
- Due date: today (or overdue from past 3 days if no today tasks)
- Status: Open
- Task type: Call, Phone, Dial, or Outbound

For each task, extract:
- Contact Name and Title
- Account Name
- Task Subject and notes
- Sequence Name and step number (if from outreach platform)
- Whether first touch or follow-up

**BDR Active Deal Filter** (when `user_role = BDR`):
1. For each account in the task list, check for active AE-owned deals
2. If active deal exists: **Remove from BDR's dial queue** → add to `excluded_active_deals[]`
3. Record: Account Name, Deal Stage, AE Owner, Deal Amount
4. **Exception:** Tasks flagged "BDR Assist" or "AE-requested" stay in queue as coordination dials

When `user_role = AE`, skip this filter.

---

### Step 2: Gather Account Intelligence

For each unique account in the task list, query CRM and build a profile:

- Industry and sub-industry (map to `{Client Profile: ICP Definitions}` verticals)
- Employee count and estimated revenue
- HQ location and operating regions
- Account owner (AE assigned)
- Current deal stage and days in stage
- Total touchpoints to date
- Last activity date and type
- Previous closed-lost opportunities and reason lost
- Deal notes or next steps logged
- Firmographic signals: M&A, leadership changes, geographic expansion, known incumbent tools

---

### Step 3: Gather Contact & Engagement History

For each contact, query CRM for:
- Name, Title, Department, Phone, Email
- Total emails sent/opened/replied
- Total calls made/connected/voicemails
- Last email date + subject, last call date + disposition
- Active or completed outreach sequences
- Bounced emails or unsubscribes

**Prior conversations:** If call/meeting transcripts are available:
- Call dates, types, duration, participants
- Pain points identified (map to `{Client Profile: Core Pain Points}`)
- Competitors or incumbent tools mentioned
- Objections raised, timeline/budget signals
- Last meeting outcome and open follow-up items

**Multi-threading:** List all other engaged contacts at the same account.

---

### Step 4: Score ICP Fit

For each account, score against `{Client Profile: ICP Definitions}`:
- **Strong Fit** / **Moderate Fit** / **Weak Fit** / **No Fit**
- Include reasoning for the score

Flag disqualification signals from `{Client Profile: Qualification Criteria}` (Disqualifiers).

---

### Step 5: Prioritize and Rank Dials

Rank all dials into 4 priority tiers. Criteria differ by role.

#### BDR Tiering
| Tier | Criteria |
|------|---------|
| **Hot** | Inbound signals on BDR-owned accounts; buying triggers with no active AE deal; meeting requested; strong ICP + active trigger |
| **Warm** | Prior conversations gone quiet (14-30 days); email opens/clicks without reply; moderate ICP with engagement; AE-requested BDR assist |
| **New** | First-touch accounts with no prior engagement; strong ICP, no relationship yet |
| **Recycle** | Previously closed-lost with no AE re-engagement; opted-out contacts after cooling period; weak ICP or multiple failed attempts |

#### AE Tiering
| Tier | Criteria |
|------|---------|
| **Hot** | Active deals with upcoming close dates or next steps due; recent activity (7 days); inbound signals; meeting requested |
| **Warm** | Active deals gone quiet (14-30 days); email opens/clicks without reply; early pipeline needing advancement |
| **New** | AE-sourced prospects with no prior engagement; strong ICP, no relationship |
| **Recycle** | Previously closed-lost; stalled deals with no clear path; weak ICP or multiple failures |

Within each tier, sub-rank by ICP fit (Strong > Moderate > Weak).

---

### Step 6: Generate Pre-Call Briefs

For each account in the prioritized list:

#### A. Why This Account (1-2 sentences)
Connect to `{Methodology: Qualification Zones}`.

#### B. Personalized Conversation Opener
Use `{Methodology: Cold Call Framework: Three-Step Turnaround}`:
1. **Interrupt** — Name + company
2. **Hook** — Select from `{Methodology: Hook Templates}` based on account signal
3. **Transition** — Move into discovery questioning

#### C. Discovery Questions (3 per account)
Tailored to the account's context. Map to `{Client Profile: Core Pain Points}`.

#### D. Objection Prep (1-2 per account)
Based on account stage and history. Use `{Methodology: Common Objections}`.

#### E. Call Goal (1 specific, measurable goal)
| Dial Type | Goal Template |
|----------|--------------|
| Cold first touch | Confirm they manage [key process] internally + book discovery |
| Follow-up (engaged) | Validate pain + identify economic buyer |
| Re-engagement (quiet) | Re-establish contact + understand what changed |
| Closed-lost re-approach | Learn what's changed + test for new triggers |
| Meeting confirmation | Confirm meeting + set agenda + identify additional attendees |

---

### Step 7: Summary Report

**1. Dashboard Summary**
- Total dials today, breakdown by tier (Hot/Warm/New/Recycle)
- Accounts with prior conversations
- Net-new first touches
- Strongest opportunity today + why

**2. Prioritized Dial Queue**
| # | Tier | Account | Contact | Title | ICP Fit | Last Touch | Call Goal |
|---|------|---------|---------|-------|---------|-----------|-----------|

**3. Detailed Pre-Call Briefs** (top 10 accounts)
Per account: snapshot, conversation history, engaged contacts, personalized opener, discovery questions, objection prep, call goal.

**4. Active Deal Exclusions** (BDR only)
Accounts removed from queue with recommended action:
- "Share today's intel with [AE name] — they own an active deal at [Stage]"
- "Ask [AE name] if they want BDR assist on this account"

**5. AE Coordination Notes** (BDR only)
Accounts requiring sync before calling: sensitive situations, multi-threaded accounts, BDR Assist flags.

**6. End-of-Day Tracking Prompts**
Reminders to log dispositions, create follow-up tasks, add accounts to sequences.

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default) — `[REP]_Daily_Dials_[DATE].md`
- **Option B: HTML** — Styled dial sheet with color-coded tiers
- **Option C: PDF** — Python + reportlab, single page, letter size, landscape orientation

### Daily Dial Sheet Sections (6 Sections)
1. **Header** — Rep name, date, total dials, tier breakdown
2. **Priority Dial Queue** — Ranked table, color-coded: Red=Hot, Orange=Warm, Blue=New, Grey=Recycle
3. **Top Account Briefs** — Top 8, condensed: account + signal + opener hook + top question + call goal
4. **Talk Track Quick Reference** — Cold call framework template + 3-4 common rebuttal responses
5. **Discovery Question Bank** — 6-8 high-impact questions organized by pain point theme
6. **End-of-Day Tracker** — Checkbox grid: Account, Connected?, Outcome, Follow-up?

---

## Examples

### Example 1: BDR Morning Prep — Full Report

**Context:** BDR has 18 tasks due today across target accounts in two ICP segments.

**Input:** "Run the daily prospecting report for [BDR Name]."

**Process:** CRM query returns 18 open tasks for today. 2 accounts have active AE deals → filtered to exclusions. 16 accounts scored: 4 Strong Fit, 7 Moderate, 4 Weak, 1 No Fit. Tiered: 3 Hot (inbound email reply, M&A trigger, meeting request), 5 Warm (prior conversations gone quiet), 6 New (first touch), 2 Recycle (closed-lost). Pre-call briefs generated for all 16 with personalized openers.

**Output:** Dashboard showing 16 dials (3 Hot, 5 Warm, 6 New, 2 Recycle). 2 excluded accounts with AE coordination guidance. Detailed briefs for top 10. Strongest opportunity: [Account] because inbound reply + Strong ICP + M&A trigger. Dial sheet generated.

### Example 2: AE Pipeline Calls — Deal Advancement

**Context:** AE has 8 tasks due today, mix of active deals and new outbound.

**Input:** "Prep my dials for today."

**Process:** `user_role = AE`. No active deal filter applied. 8 tasks scored and tiered: 2 Hot (active deal next step due, inbound signal), 3 Warm (deals gone quiet), 1 New (AE-sourced prospect), 2 Recycle (stalled deal, closed-lost). Pre-call briefs emphasize deal advancement for Hot/Warm, prospecting for New/Recycle.

**Output:** Dashboard showing 8 dials (2 Hot, 3 Warm, 1 New, 2 Recycle). No exclusions (AE sees everything). Detailed briefs for all 8. Strongest opportunity: [Deal] because next step due + champion engaged + close date this month. Dial sheet generated.

---

## Common Patterns

### Pattern: No Tasks Due Today
**When:** Rep has zero open tasks for today.
**Approach:** Check for overdue tasks (past 3 days). Check for accounts with recent inbound signals that warrant proactive outreach. If still nothing, recommend running `gtm-account-snapshot` on target accounts to build new prospecting lists.

### Pattern: BDR with Heavy AE Overlap
**When:** More than 50% of BDR's tasks are on accounts with active AE deals.
**Approach:** Generate the exclusions table with clear AE coordination guidance. Recommend the BDR discuss territory alignment with their manager. Show the filtered queue (remaining dials) with adjusted tier priorities.

### Pattern: Abbreviated Prep
**When:** Rep says "just give me my top 5" or has limited time.
**Approach:** Skip the full report. Deliver only the top 5 prioritized dials with condensed briefs (opener + 1 question + goal). No dial sheet generation.

---

## Troubleshooting

### "No tasks in CRM for today"
**Solution:** Expand search to overdue tasks (past 3 days) and accounts with recent inbound activity. If still empty, the rep may need to build their task queue — recommend running `gtm-account-snapshot` on priority accounts to generate outbound.

### "Contact has no phone number"
**Solution:** Flag the contact for LinkedIn outreach or email instead. Include in the dial sheet but mark as "Email/LinkedIn only." Recommend contact enrichment as a follow-up action.

### "Multiple contacts at the same account in the task list"
**Solution:** Group them. Generate one pre-call brief for the account, not duplicates. Recommend calling the highest-priority contact first (based on persona and engagement level), then using intel from that call to inform the next.

### "BDR has tasks on accounts they don't own"
**Solution:** Check BDR Owner field. If the BDR is assigned as BDR Owner, proceed normally. If not, flag for territory alignment — the task may have been routed incorrectly.

---

## Best Practices

### Do's
- **Run this every morning** — consistency compounds. Reps who prep daily outperform by 30%+ on connect-to-meeting rates
- **Start with Hot tier** — these have the highest probability of conversion
- **Personalize every opener** — each hook should reference a specific account signal, not generic phrasing
- **Log outcomes immediately** — end-of-day tracking is only useful if dispositions are logged

### Don'ts
- **Don't skip ICP scoring** — calling Weak Fit accounts before Strong Fit accounts is a waste of prime dial time
- **Don't call accounts with active AE deals** (BDR) — always check the exclusions list
- **Don't use generic discovery questions** — every question should reference something specific about the account
- **Don't leave the dial sheet behind** — the value is in having it open between calls, not reading it once

### Quality Checklist
- [ ] All tasks for the rep due today are included
- [ ] Every account has ICP fit score with reasoning
- [ ] Tier assignments based on engagement signals + ICP, not alphabetical
- [ ] Each opener references a specific account signal (not generic)
- [ ] Discovery questions tailored to account's known gaps
- [ ] Role detected; BDR active deals filtered; AE sees full book
- [ ] No placeholder brackets in final output
- [ ] Proof points use source labels
- [ ] Dial sheet is scannable at a glance

---

## Integration with Other Skills

- **`gtm-account-snapshot`** — For deeper research on specific accounts surfaced during daily prospecting.
- **`gtm-meeting-prep`** — When a Hot dial results in a scheduled meeting, run meeting prep for the follow-up.
- **`gtm-trigger-event-outbound`** — When daily prospecting surfaces a trigger event on an account, pivot to trigger-based outbound.
- **`gtm-competitive-displacement`** — When a Hot dial reveals a known incumbent, run displacement sequences for that account.
- **`gtm-closed-loss-reactivation`** — For Recycle tier accounts that are closed-lost, use the full reactivation workflow for deeper analysis.

---

## Changelog

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block
- Cold Call Framework, Hook Templates, and Common Objections moved to explicit Methodology section — `{Methodology: X}` references
- No functional changes to the workflow, tiering logic, or output formats

### Version 1.0.0 (2026-03-04)
- Initial release
- Client-configurable via Client Profile block
- 4-tier prioritization (Hot/Warm/New/Recycle)
- Three-Step Turnaround cold call framework with hook templates
- BDR Active Deal Filter with exclusions table and AE coordination
- Role-aware tiering (BDR vs. AE criteria)
- ICP definitions in Client Profile for portability
- Multi-format artifact generation
