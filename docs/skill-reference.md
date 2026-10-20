# Skill Reference

Quick-reference guide for choosing the right skill, understanding inputs and outputs, and chaining skills together.

---

## Decision Tree: Which Skill Do I Need?

```
START: What are you trying to do?
│
├─ "I have a new account/lead"
│   ├─ Need to know if it's worth pursuing? → 01 Account Qualification
│   ├─ Need outbound sequences fast? → 02 Account Snapshot
│   ├─ Enterprise target, need deep research? → 03 Research-Driven Outbound
│   └─ Spotted a trigger event (M&A, new exec)? → 04 Trigger Event Outbound
│
├─ "I have a dead deal to revisit"
│   └─ → 05 Closed-Loss Reactivation
│
├─ "I have an upcoming meeting"
│   ├─ Discovery call? → 06 Meeting Prep (discovery mode)
│   └─ Demo? → 06 Meeting Prep (demo mode)
│
├─ "I need my morning dial sheet"
│   └─ → 07 Daily Prospecting
│
├─ "I need to assess a deal in my pipeline"
│   ├─ Quick health check? → 08 Deal Pulse
│   ├─ Deep qualification? → 09 MEDDPICC Analysis
│   └─ Who's in the buying committee? → 10 Stakeholder Mapping
│
├─ "I'm in a competitive deal"
│   ├─ Active deal against a known competitor? → 11 Competitive Strategy
│   └─ Prospecting into a competitor's install base? → 12 Competitive Displacement
│
├─ "I need to review a call"
│   └─ → 13 Call Coaching
│
└─ "Deal is closing, need to hand off to CS"
    └─ → 14 Sales-to-CS Handoff
```

---

## Input/Output Reference

### Prospect Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **01 Account Qualification** | Account name, your role | CRM access, website, headcount, revenue | `verdict` (GREENLIGHT, MANUAL REVIEW or DISQUALIFY), `zone_scores`, `icp_match`, `fit_narrative`, the 8-criteria scorecard |
| **02 Account Snapshot** | Account name, your role | CRM access, prior interactions, a persona to focus on | `account_status`, `verdict`, `zone_scores`, `contact_priority`, `pain_hypotheses`, `sequence` (three emails per persona), the eight-section cheatsheet |
| **03 Research Outbound** | Account name, the research source and where it is | Personas to target | `verdict` with zones, `signal_map`, `wedge` (arithmetic shown), `pov_brief`, `persona_emails` (personas times steps) |
| **04 Trigger Event Outbound** | Account name, the event, its date and its source | Affected stakeholders | `trigger_type`, `urgency_window`, `days_remaining`, `event_tag`, `sequence` (three emails per persona), or a refusal when the window has closed or the date is unknown |
| **05 Closed-Loss Reactivation** | Account name, the CRM loss reason, the close date | AE notes, prior sequence history | `loss_classification`, `change_assessment` (tagged), `reactivation_strategy` (REACTIVATE, MONITOR or RETIRE), `history_opener`, sequences and call prep |

### Discover Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **06 Meeting Prep** | Account name, meeting type (discovery or demo), attendees with titles | CRM notes, prior call notes, the upstream hand-off fields | `prep_sheet`, `top_pain`, `question_bank`, `attendees` (with buying role), `proof_point` (with its Status), call flow, follow-up draft |
| **07 Daily Prospecting** | Today's task or account list, your role | Activity history, priority overrides | `dial_sheet` (Hot, Warm, New, Recycle), `pre_call_briefs` (top eight), `exclusions` (each with its reason) |

### Execute Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **08 Deal Pulse** | Company name + known deal context | CRM data, call notes, emails | 16-signal scorecard, health score (0-100), risk flags, next actions |
| **09 MEDDPICC** | Company name + deal context | Discovery notes, stakeholder info | 8-element analysis (1-5 scoring), evidence grades, gap identification |
| **10 Stakeholder Map** | Company name + known contacts | Org chart, call mentions | 7-role buying committee map, influence assessment, ghost node alerts |
| **11 Competitive Strategy** | Company name + competitor name | Competitor intel, prospect feedback | Battlecard, positioning matrix, gap questions, win plan |
| **12 Competitive Displacement** | Target company + incumbent product | Incumbent failure signals | Displacement narrative, 4-step outbound sequences, failure-pattern messaging |

### Close & Handoff Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **13 Call Coaching** | Call transcript or detailed notes, call type (discovery/demo) | Methodology preferences | Methodology grade (SPIN /30 or Challenger /40), category scores, coaching notes |
| **14 Sales-to-CS Handoff** | Deal summary, key stakeholders, implementation scope | Technical requirements, timeline | 6-dimension readiness score, implementation plan, risk flags |

---

## Skill Chaining Patterns

Skills are most powerful when combined. Here are proven sequences:

### Pattern 1: New Account (BDR Workflow)
```
Account Qualification (01)
  hands verdict, zone_scores, icp_match, fit_narrative
  → verdict GREENLIGHT?
    → Account Snapshot (02)
      hands account_status, verdict, contact_priority, pain_hypotheses, sequence
      → Meeting booked?
        → Meeting Prep (06)
          hands prep_sheet, top_pain, question_bank, attendees, proof_point
```
Each skill asks for the upstream fields by those names in its Integration section, so a fresh session can pick the chain up from any step.

### Pattern 2: Enterprise Target (AE + BDR)
```
Research-Driven Outbound (03)
  → Response / meeting booked?
    → Meeting Prep (06) [discovery]
      → After call: Call Coaching (13)
        → Deal Pulse (08)
          → Meeting Prep (06) [demo]
```

### Pattern 3: Pipeline Review (Manager)
```
Deal Pulse (08) on all commit deals
  → Flag deals < 60 health score
    → MEDDPICC Analysis (09) on flagged deals
      → Stakeholder Mapping (10) on deals with < 3 known contacts
```

### Pattern 4: Competitive Deal
```
Competitive Strategy (11)
  → Meeting Prep (06) [with battlecard context]
    → After call: Call Coaching (13)
      → Deal Pulse (08) [updated with competitive signals]
```

### Pattern 5: Deal Close + Handoff
```
MEDDPICC Analysis (09) [final qualification check]
  → All elements GREEN?
    → Sales-to-CS Handoff (14)
```

### Pattern 6: Win-Back Campaign
```
Closed-Loss Reactivation (05) [batch: all losses from 6 to 12 months ago]
  hands loss_classification, change_assessment, reactivation_strategy, history_opener
  → reactivation_strategy REACTIVATE?
    → Trigger Event Outbound (04) [when the change is a dated event]
      hands trigger_type, urgency_window, days_remaining, event_tag, sequence
    → Meeting Prep (06) [when a call is booked]
  → MONITOR: the reopening event that moves it is named in the output
  → A champion who moved to a new account is a new play there: Account Snapshot (02)
```

---

## Scoring Systems Reference

These figures are taken from the skill files. If you change a skill's scoring, change this section with it.

### Deal Pulse (Skill 08)
- **Scale:** 0-100 health score, the average of 16 signal values
- **Pillars:** Why Anything (macro need), Why Us (differentiation), Why Now (urgency), Execution (process mechanics), 4 signals each
- **Each signal:** GREEN (100, strong evidence) / YELLOW (50, partial) / RED (0, missing or negative)
- **Risk bands:** 85-100 Low Risk, 46-84 Medium Risk, 0-45 High Risk. Any pillar averaging below 30 bumps the risk up one level

### MEDDPICC (Skill 09)
- **Scale:** each of the 8 elements scored 1-5, weighted into a 0-100 health score
- **Weights:** Economic Buyer 20%, Metrics 15%, Identified Pain 15%, Champion 15%, Decision Criteria 10%, Decision Process 10%, Paper Process 10%, Competition 5%
- **Bands:** 80-100 Green, 60-79 Yellow, 40-59 Orange, 0-39 Red
- **Stage minimums:** Discovery 30+, Trial & Evaluation 50+, Negotiation 65+, Closing 75+, each with critical elements that must score 3 or better

### Call Coaching (Skill 13)
- **Discovery (SPIN + Priority Ladder):** 6 categories, /30. 26-30 Excellent, 20-25 Good, 14-19 Needs Improvement, 8-13 Poor, 6-7 Critical
- **Demo (Challenger + MEDDPICC + Question the Problem):** 8 categories, /40. 34-40 Excellent, 26-33 Good, 18-25 Needs Improvement, 10-17 Poor, 8-9 Critical
- **Per category:** specific behavioral criteria, with evidence from the transcript

### Account Pre-Qualification (Skill 01)
- **Scale:** 8 criteria, each scored STRONG / PARTIAL / WEAK / UNKNOWN, plus Qualification Zones
- **Verdict:** GREENLIGHT (6+ of 8 STRONG or PARTIAL, 2+ zones HIGH, no critical risk) / MANUAL REVIEW (4-5 of 8, data gaps) / DISQUALIFY
- **Includes:** trigger detection, risk flags, fit narrative

---

## The Operating Layer

The 15 skills in `operating/` are not stage-specific. They run around the sales work. Which one
to use, what each reads from the profile, and the order to set them up in are in
[How It Fits Together](how-it-fits.md). In short:

| Group | Skills | Reach for them when |
|---|---|---|
| Verification | O1 Verify, O2 Debug, O3 Debate, O4 Context Gap, O5 Second Opinion | Before building, before deciding, while fixing, and before calling anything done |
| Memory | O6 Weekly Review, O7 Graph Health, O8 Dream, O9 Ingest, O10 Wrap-up, O11 Context OS Setup | You want the team's knowledge to compound instead of scattering. Run O11 first |
| Strategy | O12 Engine, O13 Launch, O14 Positioning, O15 Discovery | The profile is thin, or the market has moved. They fill the profile with evidence |

---

## Tips for Better Output

1. **Give Claude more context, not less.** Paste CRM notes, call transcripts, email threads. The skills are designed to filter and prioritize. Let them do the work.

2. **Be specific about what you want.** "Score this deal" works. "Score this deal, focusing on the champion gap and whether we have a paper process mapped" works better.

3. **Chain skills deliberately.** Run Pre-Qualification before Account Snapshot. Run Deal Pulse before MEDDPICC. Each skill's output enriches the next.

4. **Trust the methodology, question the data.** If a Deal Pulse score feels wrong, check whether Claude had enough context. A low score with good data is a real warning. A low score with sparse data just means you need to feed it more.

5. **Update your Client Profile.** After 30 days, review. Did new competitors emerge? Did you close a deal worth adding as a proof point? Did a pain point climb in priority? Keep the profile current.
