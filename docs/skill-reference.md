# Skill Reference

Quick-reference guide for choosing the right skill, understanding inputs and outputs, and chaining skills together.

---

## Decision Tree: Which Skill Do I Need?

```
START: What are you trying to do?
│
├─ "I have a new account/lead"
│   ├─ Need to know if it's worth pursuing? → 01 Account Pre-Qualification
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
| **01 Pre-Qualification** | Company name | Website, employee count, revenue, industry | ICP scorecard (8 criteria), verdict (GREENLIGHT/REVIEW/DISQUALIFY), fit narrative |
| **02 Account Snapshot** | Company name | CRM data, website, LinkedIn | Company brief, ICP score, 3 email sequences (6 emails each), cold call sheet |
| **03 Research Outbound** | Company name + research source (10-K, earnings, news) | Specific personas to target | POV brief, 24 persona-tailored emails, strategic narrative |
| **04 Trigger Event** | Company name + trigger event description | Timeline, affected stakeholders | Urgency analysis, 3 time-sensitive sequences, 7-14 day campaign |
| **05 Closed-Loss** | Company name + loss reason from CRM | Previous interactions, time since loss | Change analysis, reactivation strategy, history-aware sequences |

### Discover Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **06 Meeting Prep** | Company name, meeting type (discovery/demo), attendee(s) | CRM data, previous call notes | Single-page call sheet: SPIN questions or demo structure, persona proof, agenda scripts |
| **07 Daily Prospecting** | Your pipeline/account list | Priority overrides, activity history | 4-tier dial sheet with openers, pain questions, call framework |

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
Account Pre-Qualification (01)
  → GREENLIGHT?
    → Account Snapshot (02)
      → Meeting booked?
        → Meeting Prep (06)
```
**Time:** ~15 minutes for the full sequence (vs. 2-3 hours manually)

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
Closed-Loss Reactivation (05) [batch: all losses from 6-12 months ago]
  → Filter for "circumstances changed" candidates
    → Account Snapshot (02) [refresh intel]
      → Trigger Event Outbound (04) [if new trigger found]
```

---

## Scoring Systems Reference

### Deal Pulse (Skill 08)
- **Scale:** 0-100 health score
- **Pillars:** Why Anything (macro need), Why Us (differentiation), Why Now (urgency), Execution (process mechanics)
- **Signals per pillar:** 4 (16 total)
- **Each signal:** GREEN (strong evidence) / YELLOW (partial) / RED (missing/negative)
- **Interpretation:** 80+ = strong deal, 60-79 = needs attention, 40-59 = at risk, <40 = likely loss

### MEDDPICC (Skill 09)
- **Scale:** 1-5 per element (8 elements)
- **Evidence grades:** VERIFIED (direct evidence) / INFERRED (indirect signals) / UNVERIFIED (assumption)
- **Max score:** 40
- **Interpretation:** 32+ = well-qualified, 24-31 = gaps to address, <24 = qualification risk

### Call Coaching (Skill 13)
- **Discovery (SPIN):** 6 categories, /30 total
- **Demo (Challenger):** 8 categories, /40 total
- **Per-category:** Specific behavioral criteria with evidence
- **Interpretation:** 80%+ = strong execution, 60-79% = coaching opportunity, <60% = structural gaps

### Account Pre-Qualification (Skill 01)
- **Scale:** 8 weighted criteria, each scored
- **Verdict:** GREENLIGHT / MANUAL REVIEW / DISQUALIFY
- **Includes:** Trigger detection, risk flags, fit narrative

---

## Tips for Better Output

1. **Give Claude more context, not less.** Paste CRM notes, call transcripts, email threads. The skills are designed to filter and prioritize. Let them do the work.

2. **Be specific about what you want.** "Score this deal" works. "Score this deal, focusing on the champion gap and whether we have a paper process mapped" works better.

3. **Chain skills deliberately.** Run Pre-Qualification before Account Snapshot. Run Deal Pulse before MEDDPICC. Each skill's output enriches the next.

4. **Trust the methodology, question the data.** If a Deal Pulse score feels wrong, check whether Claude had enough context. A low score with good data is a real warning. A low score with sparse data just means you need to feed it more.

5. **Update your Client Profile.** After 30 days, review. Did new competitors emerge? Did you close a deal worth adding as a proof point? Did a pain point climb in priority? Keep the profile current.
