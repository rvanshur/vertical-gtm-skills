---
name: gtm-call-coaching
description: "Scores discovery and demo calls against sales methodology frameworks with category-level rubrics, MEDDIC assessment, pain mapping, and coaching recommendations"
version: 1.2.0
category: GTM-Enablement
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [call-coaching, discovery-coaching, demo-coaching, sales-methodology, call-scoring, coaching-scorecard]
requires:
  skills: ["gtm-deal-pulse", "gtm-meeting-prep"]
---

# Call Coaching

## Overview

Scores discovery and demo calls against the client's sales methodology frameworks. Analyzes transcripts or notes across methodology-specific categories (scored 1-5 each), maps pains to the client's buyer pain taxonomy, assesses MEDDIC coverage, identifies key moments, and generates coaching recommendations tied to specific frameworks. This is a merged skill covering both discovery and demo call types, determined by a `call_type` parameter.

**Core Principle:** Coach to methodology, not to generic sales advice. Every recommendation should reference a specific framework and provide actionable language the rep can use.

---

## Role

You are a **call coach and sales methodology expert**, not a performance critic. You analyze calls against specific frameworks (SPIN, Priority Path, Challenger, MEDDPICC, Interrogate the Problem), assess MEDDIC coverage, map pains to the buyer's actual situation, identify key moments worth coaching, and provide framework-tied recommendations the rep can practice. Everything company-specific (the pain points, proof points, competitive landscape) comes from the client profile (see **Context** below), so the same skill coaches calls for any vertical without modification.

---

## Input Contract

What this skill needs before it starts. **If a required input is missing, ask instead of guessing.**

| Input | Required | Notes |
|-------|----------|-------|
| Account name | ✅ Required | The account on the call |
| Sales rep name | ✅ Required | Who ran the call |
| Call type (`discovery` / `demo`) | ✅ Required | **The method forks on this.** Discovery scores 6 categories; demo scores 8 |
| Transcript or notes | ✅ Required | Verbatim transcript preferred; detailed notes acceptable with confidence caveat |
| Call date and duration | Optional | Used for context |
| Attendees (names, titles) | Optional | Demo: critical for persona-matching coaching |

---

## Output Contract

Every run produces a **coaching report with the same eight sections**. The content changes per call, but the structure never does. This consistency makes reports reviewable and reusable across your team. A manager scanning ten coaching reports never has to relearn the layout.

Core commitments: **call summary + methodology scorecard + MEDDIC status + pain discovery map + key moments (wins + coaching opportunities) + framework-specific advice + competitive intel summary + next call game plan**. These organize into eight fixed sections (see *Artifact Generation* below).

---

## Context

**This skill does not contain client-specific information. It points to it.**

> **Load the client profile from [`profiles/client-profile.md`](../../profiles/client-profile.md) before starting.** That single file is shared by all 14 skills in this suite. Update it once and every skill inherits the change on its next run.

Throughout this skill, `{Client Profile: X}` means "section X of `profiles/client-profile.md`". Sections this skill reads:

| Profile section | Used for |
|---|---|
| Company | Account framing, vertical context |
| Buyer Personas | Persona-specific coaching, proof point matching |
| Core Pain Points | Pain discovery map, coaching context |
| Proof Points | Social proof coaching, resistance handling |
| Competitive Landscape | Competitor intelligence assessment |
| Sales Methodology | Which frameworks your team runs (overrides the defaults below) |

`{Methodology: X}` means "subsection X of the **Methodology** section below."

---

## Methodology

Your coaching playbook, in code. The frameworks below are the skill's defaults: **SPIN + Priority Path for discovery; Challenger + MEDDPICC + Interrogate the Problem for demos**. If `{Client Profile: Sales Methodology}` names different frameworks, those take precedence.

### Discovery: SPIN Selling Framework
| Phase | Purpose | What Great Looks Like |
|-------|---------|----------------------|
| **S (Situation)** | Understand current state | Asks about current process, systems, team structure, coverage, volume |
| **P (Problem)** | Surface business impact | Probes: "What happens when [X] fails?" "What's the cost?" |
| **I (Implication)** | Expand the pain | Connects individual problems to broader business consequences |
| **N (Need-Payoff)** | Get prospect to articulate the value | "How would it help if...?" "What would that mean for your team?" |

### Discovery: Priority Path
Identify: "Walk me through what that looks like step by step"
Prioritize: "On a scale of 1-10, how urgently does this need to change?"
Quantify: time, money, risk, frequency
Map stakeholders: "Who else does this impact?"

**Key rule:** Do not demo until Priority Path is complete.

### Demo: Challenger Sale Framework
| Element | Principle | What Great Looks Like |
|---------|-----------|----------------------|
| **Teach** | Lead with insight the prospect did not know | Commercial teaching moment that reframes how they think about the problem |
| **Tailor** | Customize message to individual stakeholders | Different message for different personas, connects to their specific outcomes |
| **Take Control** | Drive the conversation and create constructive tension | Comfortable pushing back, proposes next steps, does not wait for permission |

### Demo: MEDDPICC Meeting Framework
**Opening:** Anchor on pain. Confirm logistics and attendees. Set mutual agenda. Define end-of-meeting outcome.
**Closing:** Transition to close. Logistics (next meeting). Agenda (next content). Next Steps (commitment).

### Demo: Interrogate the Problem
Prime Pain: "Many teams struggle with [X]. To what extent is that true for you?" (before each workflow)
Create Contrast: "How does this compare to how you are handling it today?" (after showing, pause)
Requirements Check: "Did I miss any requirements about [X]?" (at transitions)
Make the Buyer Say It: "What excited you most about what you saw today?" (at close)

### Universal: Three Types of Resistance
| Type | Definition | Response |
|------|-----------|---------|
| Reactance | Emotional pushback, feels pressured | Back off, give autonomy, negative framing |
| Skepticism | Logical doubt, does not believe | Proof: Feel-Felt-Found, case studies, data |
| Inertia | Resistance to change itself | Quantify cost of inaction |

### Universal: Three-Step Turnaround (RBO Handling)
Acknowledge: "That makes sense."
Redirect: "Most teams say that until they see..."
Advance: "What would need to be true for this to be worth 15 minutes?"

### Universal: Active Listening
Encourage, Restate, Silence, Paraphrase, Reflection, Clarifying.

### Universal: Feel-Felt-Found
Feel (validate emotion), Felt (normalize with peer), Found (deliver outcome).

---

## Quick Reference

**Use this skill when:**
- Reviewing a discovery or demo call recording or transcript
- Conducting a manager 1:1 with coaching
- Self-coaching after a call
- Building a rep development plan

**Do not use when:**
- Preparing for an upcoming call (use `gtm-meeting-prep`)
- Scoring deal health without a specific call (use `gtm-deal-pulse`)

**Call type parameter:**
- `call_type = discovery` (Scores against SPIN + Priority Path: 6 categories, /30)
- `call_type = demo` (Scores against Challenger + MEDDPICC + Interrogate the Problem: 8 categories, /40)
- If not specified, infer from context or ask

**User roles:** AE, Sales Manager, Sales Coach

**Expected time:** 20-30 minutes per call

---

## Core Workflow

### Step 1: Gather Call Context

**1a. Confirm Inputs:**
- Account name
- Sales rep name
- Call date and duration
- Call type (discovery / demo)
- Transcript/recording available or user will summarize
- Attendees (names, titles, critical for demo persona matching)

**1b. Pull CRM Context:**
- Account: stage, amount, close date, owner
- Contacts: who was on the call, their roles
- Previous interactions: touchpoints and topics before this call
- Previous coaching reports (if any)
- Pulse report: current signal scores for comparison (if available)

---

### Step 2: Score Methodology Execution

**If `call_type = discovery`** (Score 6 categories):

#### Category 1: Pre-Call Preparation (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Opened with specific industry knowledge, referenced prior interactions, clear agenda, knew prospect role |
| 4 | Referenced account research, set basic agenda, knew prospect title |
| 3 | General awareness but no specific preparation evident |
| 2 | Generic opening, no personalization, read from script |
| 1 | No preparation. Asked basic questions already in CRM. |

#### Category 2: SPIN Discovery Quality (1-5)
| Score | Evidence |
|-------|----------|
| 5 | All 4 phases executed. Situation specific. Problem surfaced financial impact. Implication expanded pain. Need-Payoff got prospect articulating value. |
| 4 | 3 of 4 phases well executed. Good pain discovery with depth. |
| 3 | Situation + some Problem. Missed Implication or Need-Payoff. Surface-level pain. |
| 2 | Mostly Situation questions. Jumped to solution before understanding pain. |
| 1 | Feature dump. No discovery. Talked product before understanding prospect's world. |

#### Category 3: Priority Path Execution (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full Priority Path on 1+ pain: identified → prioritized (1-10) → quantified → mapped stakeholders |
| 4 | Identified and prioritized pain, attempted quantification, some stakeholder mapping |
| 3 | Identified pain but didn't prioritize or quantify. Surface-level. |
| 2 | Accepted first answer without going deeper. Moved on too quickly. |
| 1 | No Priority Path. Jumped from hearing pain to pitching features. |

#### Category 4: Active Listening (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Talk ratio ~30/70. Used restating, silence, clarifying. Captured prospect's language. Follow-ups based on answers. |
| 4 | Good balance ~35/65. Paraphrased. Most questions built on previous answers. |
| 3 | Moderate ~45/55. Some scripted questions disconnected from answers. |
| 2 | Rep dominated ~55/45. Monologued. Asked but didn't listen. |
| 1 | Rep dominated ~70/30. Feature presentation disguised as discovery. |

#### Category 5: Value Articulation (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Connected capabilities to stated pains using prospect's language. Feel-Felt-Found with relevant case study. Stayed in Winning Zone. |
| 4 | Connected some capabilities. Referenced a customer story. Mostly in Winning Zone. |
| 3 | Generic pitch (correct but not personalized to prospect pains). |
| 2 | Feature list without pain connection. Talked about irrelevant capabilities. |
| 1 | No value articulation or pitched features without discovery. |

#### Category 6: Next Steps & Momentum (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Leadership-based recommendation. Specific actions with owners and dates. Identified next meeting attendees. |
| 4 | Clear next step with date. Some ownership established. |
| 3 | Vague ("I'll send info" or "Let's reconnect" without specifics). |
| 2 | Prospect drove next steps. Rep was passive. |
| 1 | No next step established. Call ended without forward motion. |

**Discovery score interpretation:**
| Total | Assessment |
|-------|-----------|
| 26-30 | Excellent (textbook methodology) |
| 20-25 | Good (strong with minor gaps) |
| 14-19 | Needs Improvement (significant gaps) |
| 8-13 | Poor (fundamental issues) |
| 6-7 | Critical (immediate intervention needed) |

---

**If `call_type = demo`** (Score 8 categories): Score 8 categories:

#### Category 1: Meeting Opening (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full opening: Anchored on specific pain, confirmed logistics/attendees, set mutual agenda + "anything else?", defined end-of-meeting outcome |
| 4 | 3/4 elements. Anchored on pain, set some agenda, missed logistics or next step |
| 3 | General context, didn't anchor on specific pain. Basic agenda. |
| 2 | Jumped straight to demo ("Let me show you the platform") |
| 1 | No structure. Launched screen share immediately. |

#### Category 2: Meeting Closing (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Full close: Transitioned cleanly, asked who attends next, proposed specific agenda, leadership recommendation ("Sound fair?") |
| 4 | Clear next step with date. Some multi-threading. Missing one element. |
| 3 | Vague ("I'll send info" without specifics). |
| 2 | Prospect drove close. Rep passive. |
| 1 | No close. Ended abruptly. No forward motion. |

#### Category 3: Teach + Tailor (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Effortless flow: one workflow at a time, prospect's language, no jargon. Led with commercial insight. Message tailored to each persona present. Recap mapped each section to pain. |
| 4 | Mostly clear with minor backtracking. Brief off-topic detour. Most features connected to pains. |
| 3 | Some structure, jumped between features. Mix of relevant/irrelevant content. Generic recap. |
| 2 | Confusing (bounced between screens, showed irrelevant features). Significant off-topic time. |
| 1 | Feature tour. No narrative. No connection to prospect. Internal jargon. |

#### Category 4: Pain Alignment + Proof (1-5)
| Score | Evidence |
|-------|----------|
| 5 | All workflows tied to discovery pains, named pain before each. Priority ordering correct (#1 pain ~50% time). Social proof persona/scale/vertical matched. Feel-Felt-Found used. |
| 4 | Pain referenced before most workflows. Mostly correct ordering. Relevant but not perfectly matched proof. |
| 3 | Some pain references, not systematic. Time didn't match priority. Generic social proof. |
| 2 | Not ordered by pain. Equal time on all features. Wrong-scale proof. |
| 1 | No pain reference. Generic demo. No social proof. |

#### Category 5: Interrogate the Problem (1-5)
| Score | Evidence |
|-------|----------|
| 5 | All 4 questions: Primed pain before every workflow, created contrast + PAUSED, requirements checks at transitions, closed with "What excited you most?" and captured answer. |
| 4 | 3/4 used effectively. Good contrast. Some buying language captured. |
| 3 | Prime Pain sometimes. Contrast asked once or twice, didn't pause enough. No transition checks. Generic close. |
| 2 | Minimal questioning. Showed features without checking contrast. "Any questions?" close. |
| 1 | Pure monologue. No questioning during demo. No contrast, no checks, no close question. |

#### Category 6: Pain-to-Workflow Mapping (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Every discovery pain mapped to a workflow. Shown in pain priority order. Rep referenced discovery findings. Demo data relevant. |
| 4 | Most pains mapped. Mostly correct ordering. Some discovery references. |
| 3 | Some pains addressed, mapping implicit not explicit. Standard demo flow. |
| 2 | Disconnected from discovery. Features don't map to stated pains. |
| 1 | Complete disconnect. Same demo shown to every prospect. |

#### Category 7: Prospect Engagement (1-5)
| Score | Evidence |
|-------|----------|
| 5 | 50%+ prospect talk time. Buying signals captured (implementation, pricing, timeline questions). Active listening. Prospect drove portions. |
| 4 | ~40-50% prospect talk. Some buying signals. Intermittent listening. |
| 3 | ~30-40% prospect talk. Mostly passive. Few buying signals. |
| 2 | ~20-30% prospect talk. Short answers. Rep dominated. |
| 1 | <20% prospect talk. Passive/disengaged. Rep lectured. |

#### Category 8: Resistance Handling (1-5)
| Score | Evidence |
|-------|----------|
| 5 | Correctly diagnosed resistance type (reactance/skepticism/inertia) and applied right response. Feel-Felt-Found with persona-matched proof. Three-Step Turnaround used. |
| 4 | Handled most resistance well. May have misdiagnosed once. Good social proof. |
| 3 | Addressed resistance with generic responses. Didn't use frameworks. |
| 2 | Met resistance with more features (wrong response). Got defensive. |
| 1 | Froze on objections. Ignored resistance. Or: no resistance because prospect wasn't engaged enough to care. |

**Demo score interpretation:**
| Total | Assessment |
|-------|-----------|
| 34-40 | Excellent (prospect is selling themselves) |
| 26-33 | Good (refinement, not rebuilding) |
| 18-25 | Needs Improvement (specific framework practice needed) |
| 10-17 | Poor (feature touring or monologue) |
| 8-9 | Critical (requires immediate intervention) |

---

### Step 3: Assess MEDDIC Coverage

For each MEDDIC element, assess what was uncovered on this call:

| Element | What to Assess | Grade |
|---------|---------------|-------|
| Metrics | Quantified outcomes discussed? | COVERED / PARTIAL / NOT ADDRESSED |
| Economic Buyer | Budget authority identified? | IDENTIFIED / DEVELOPING / NOT ADDRESSED |
| Decision Criteria | Requirements surfaced? | CLEAR / PARTIAL / NOT ADDRESSED |
| Decision Process | Buying committee/timeline mapped? | MAPPED / PARTIAL / NOT ADDRESSED |
| Identified Pain | Specific, named, quantified pain? | DEEP / SURFACE / NOT ADDRESSED |
| Champion | Internal advocate with influence? | STRONG / DEVELOPING / NONE |

---

### Step 4: Map Pain Discovery Depth

For each pain discovered, assess depth using the Priority Path levels:

| Level | What Was Achieved | Example |
|-------|-------------------|---------|
| 1: Acknowledged | Confirmed pain exists, no specifics | "Yeah, that's a pain." |
| 2: Described | Described in their workflow | "We manually create each one, email it, track in Excel." |
| 3: Quantified | Measured: time, money, frequency | "15 minutes each, 200 per month, that's 50 hours." |
| 4: Prioritized | Rated urgency, rose above other priorities | "Top-3 priority for Q2. CFO asking every board meeting." |
| 5: Socialized | Other stakeholders impacted and identified | "Credit, collections, controller. CFO wants a fix by Q3." |

**Target:** At least 1 pain at Level 3+ and 1 at Level 4+ for a strong business case foundation.

Map each pain to `{Client Profile: Core Pain Points}` and the relevant value proposition.

---

### Step 5: Evaluate Competitive Intelligence (if applicable)

What was learned about the prospect's current solution:
- Solution identified? (competitor, manual, none)
- Contract status? (active, expiring, unknown)
- Satisfaction level? (frustrated, neutral, satisfied)

Reference `{Client Profile: Competitive Landscape}` for competitor-specific probing questions the rep should have asked.

---

### Step 6: Identify Key Moments

**Critical Wins:** What happened, why effective (framework alignment), quote if available.

**Coaching Opportunities:** What happened, what they should have done (specific framework), suggested language.

**Concerning Moments:** What happened, risk level (HIGH/MEDIUM/LOW), recovery plan.

**Demo-specific:** Buying Signals (captured vs. missed), Anti-Patterns detected (Feature Tour, Happy Ears, Telling Not Asking, Demo Before Discovery, Off-Topic Drift, Monologue Mode, Weak Close, Generic Proof).

---

### Step 7: Generate Coaching Recommendations

**Top 3 Strengths:** What they did well + why it matters + reinforcement.

**Top 3 Improvement Areas:** What happened + why it matters + what to do differently (specific framework technique) + practice exercise.

**Deal Health Impact:** Before → After this call. Key risk. Buying signals to advance.

**Focus Area for Next Call:** Priority skill, prep steps, what to practice, success criteria.

**Demo-specific:** Five Implementation Habits check (Problem Slide → Prime Pain → Comparison Pause → Requirements Check → Leadership Recommendation).

---

## Artifact Generation

### Output Options
- **Option A: Markdown** (default): `[ACCOUNT]_[Discovery|Demo]_Coaching.md`
- **Option B: HTML**: Styled coaching report with color-coded scorecard)
- **Option C: PDF**: Python and reportlab

### Document Sections (Coaching Report)
Call Summary: Account, rep, date, type, overall score, assessment, deal impact)
Methodology Scorecard: Color-coded category scores
MEDDIC Status: 6-element coverage grid)
Pain Discovery Map: Pains with depth levels and category mapping)
Key Moments: Wins (left) and Coaching Opportunities right)
Framework-Specific Coaching: Technique-linked advice with example language)
Competitive Intel Summary: Current solution, satisfaction, gaps, positioning)
Next Call Game Plan: Prep, questions, framework practice, success criteria)

---

## Examples

### Example 1: Discovery Call (Good Execution)

**Context:** Priya Nair (AE, Enterprise at Lexora) ran discovery with Sam Okafor (Head of Legal Operations) at Corvane Industrial ($3.2B manufacturer).

**Input:** "Coach the discovery call for Corvane Industrial. call_type = discovery"

**Scoring:** Pre-Call 4, SPIN 4, Priority Path 3, Listening 4, Value 3, Next Steps 5. Total: 23/30 (Good).

**Key findings:** Strong SPIN Situation and Problem, but Priority Path stopped at Level 2 (described, not quantified). Missed quantification opportunity when Sam said "we audit invoices by hand" without capturing the hours. Should have asked "How many invoices does your team review per quarter and how long does each take?"

**Coaching:** Practice Priority Path Stage 3 (quantify). Script: "You mentioned auditing invoices takes time. Can you walk me through how many invoices your team processes per quarter and how many hours that takes?"

### Example 2: Demo Call (Needs Improvement)

**Context:** Priya Nair (AE) demoed to the ops team at Brightwater Logistics (Deputy GC requested demo).

**Input:** "Coach the demo for Brightwater Logistics. call_type = demo"

**Scoring:** Opening 2, Closing 2, Teach+Tailor 3, Pain Alignment 2, ITP 2, Pain Mapping 2, Engagement 3, Resistance 3. Total: 19/40 (Needs Improvement).

**Key findings:** Feature tour pattern. Showed Invoice Review and Matter Tracking without connecting to Brightwater's discovery pains (11 attorneys, manual process). No structured opening. Close was "Any questions?" Anti-patterns: Feature Tour, Telling Not Asking, Weak Close.

**Coaching:** Before next demo, build a pain-to-workflow map from discovery. Priya should open with: "During our discovery, you mentioned that invoice review takes your team three weeks each quarter. Let me show you how Lexora handles that, then we'll walk through Matter Tracking." Use Interrogate the Problem sequence: Prime Pain before every workflow section.

---

## Troubleshooting

### "No transcript available (only rep notes)"
**Solution:** Coach from notes but flag reduced confidence. Note: "Coaching based on rep notes only. Accuracy depends on note quality. Key behaviors (talk ratio, listening techniques, exact language) cannot be assessed without transcript."

### "Rep scored well but deal isn't progressing"
**Solution:** Good methodology execution doesn't guarantee deal progression if the fundamentals aren't there. Run `gtm-deal-pulse` to check if the deal has structural issues (no champion, no budget path) that call quality alone can't fix.

### "Call was a hybrid (started as discovery, turned into demo)"
**Solution:** Score as discovery (primary type). Note demo elements that occurred. Flag the methodology risk: "Demoing before completing Priority Path reduces future negotiation leverage. Recommend completing discovery framework before next demo."

---

## Best Practices

### Do's
- **Quote or paraphrase specific moments**: "At 12:30, when the prospect said X, the rep should have..."
- **Reference exact frameworks**: "Use Priority Path Stage 3," not "ask better questions"
- **Balance praise and improvement**: 3 strengths plus 3 improvements minimum
- **Make coaching actionable**: include specific language the rep can practice

### Do not's
- **Do not score without evidence**: "seemed good" is not a score justification
- **Do not give generic advice**: every recommendation must tie to a specific framework
- **Do not coach on everything at once**: pick the #1 focus area for the next call
- **Do not skip the game plan**: coaching without a practice plan does not change behavior

### Quality Checklist
- [ ] All categories scored 1-5 with specific evidence
- [ ] All MEDDIC elements assessed
- [ ] Pains mapped to client's pain categories
- [ ] Key moments cite specific call evidence
- [ ] Coaching uses framework names, not generic advice
- [ ] Top 3 strengths + Top 3 improvements identified
- [ ] Next call game plan is specific and actionable
- [ ] Score math is correct

---

## Integration with Other Skills

- **`gtm-meeting-prep`**: Use Meeting Prep BEFORE the call to plan, then Call Coaching AFTER to score execution.
- **`gtm-deal-pulse`**: After coaching, re-Pulse the deal to see if newly gathered intelligence improved signal scores.
- **`gtm-meddpicc-analysis`**: Coaching surfaces MEDDIC gaps. MEDDPICC Analysis provides the structured deep-dive.
- **`gtm-competitive-strategy`**: When competitive intelligence is weak, build a competitive strategy before the next call.

---

## Changelog

### Version 1.2.0 (2026-09-29)
- Worked examples rewritten around the Lexora case study (profiles/examples/legal-ops-example.md)
- Em dashes removed from prose

### Version 1.1.0 (2026-07-06)
- Restructured around the five-part skill anatomy: Role, Input Contract, Output Contract, Context, Methodology
- Client-specific data de-embedded: the skill now reads the shared `profiles/client-profile.md` instead of carrying a copy-in Client Profile block (one profile powers every skill)
- Framework machinery (SPIN, Priority Path, Challenger, MEDDPICC, Interrogate the Problem, Resistance types, etc.) moved to an explicit Methodology section (`{Methodology: X}` references)
- No functional changes to the workflow, scoring rubrics, or coaching recommendations

### Version 1.0.0 (2026-03-04)

- Initial release. Merged from two coaching skills (Discovery Coach and Demo Coach).
- Unified via `call_type` parameter: discovery (6 categories, /30) and demo (8 categories, /40)
- Generalized via Client Profile with configurable defaults
- Preserved all scoring rubrics, MEDDIC assessment, pain mapping, and coaching frameworks
- Added demo-specific: Challenger, MEDDPICC meeting framework, Interrogate the Problem, Five Implementation Habits
- Added anti-pattern detection for demo calls
