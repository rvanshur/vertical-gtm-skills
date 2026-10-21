# Skill Reference

Quick-reference guide for choosing the right skill, understanding inputs and outputs, and chaining skills together.

The repository holds 29 skills. The 14 sales skills live in `skills/` and are numbered 01 to 14. The 15 operating skills live in `operating/` and are numbered O1 to O15. Each entry below names the folder it lives in, so you can open the `SKILL.md` directly.

---

## Decision Tree: Which Skill Do I Need?

```
START: What are you trying to do?
│
├─ "I have a new account/lead"
│   ├─ Need to know if it's worth pursuing? → 01 Account Qualification (skills/01-account-qualification)
│   ├─ Need outbound sequences fast? → 02 Account Snapshot (skills/02-account-snapshot)
│   ├─ Enterprise target, need deep research? → 03 Research Outbound (skills/03-research-outbound)
│   └─ Spotted a trigger event (M&A, new exec)? → 04 Trigger Event Outbound (skills/04-trigger-event-outbound)
│
├─ "I have a dead deal to revisit"
│   └─ → 05 Closed-Loss Reactivation (skills/05-closed-loss-reactivation)
│
├─ "I have an upcoming meeting"
│   ├─ Discovery call? → 06 Meeting Prep, discovery mode (skills/06-meeting-prep)
│   └─ Demo? → 06 Meeting Prep, demo mode (skills/06-meeting-prep)
│
├─ "I need my morning dial sheet"
│   └─ → 07 Daily Prospecting (skills/07-daily-prospecting)
│
├─ "I need to assess a deal in my pipeline"
│   ├─ Quick health check? → 08 Deal Pulse (skills/08-deal-pulse)
│   ├─ Deep qualification? → 09 MEDDPICC Analysis (skills/09-meddpicc-analysis)
│   └─ Who's in the buying committee? → 10 Stakeholder Mapping (skills/10-stakeholder-mapping)
│
├─ "I'm in a competitive deal"
│   ├─ Active deal against a known competitor? → 11 Competitive Strategy (skills/11-competitive-strategy)
│   └─ Prospecting into a competitor's install base? → 12 Competitive Displacement (skills/12-competitive-displacement)
│
├─ "I need to review a call"
│   └─ → 13 Call Coaching (skills/13-call-coaching)
│
├─ "Deal is closing, need to hand off to CS"
│   └─ → 14 Sales Handoff (skills/14-sales-handoff)
│
├─ "I'm about to build something new"
│   └─ → O4 Context Gap (operating/O4-context-gap)
│
├─ "I'm about to commit to a plan or a big decision"
│   └─ → O3 Debate (operating/O3-debate)
│
├─ "Something is broken or behaving oddly"
│   └─ → O2 Debug (operating/O2-debug)
│
├─ "Other people will rely on this work"
│   └─ → O5 Second Opinion (operating/O5-second-opinion)
│
├─ "I'm about to say it's done"
│   └─ → O1 Verify (operating/O1-verify)
│
├─ "I'm ending a working session"
│   └─ → O10 Wrap-Up (operating/O10-wrap-up)
│
├─ "I want the team's knowledge to compound"
│   ├─ No knowledge base exists yet? → O11 Context OS Setup (operating/O11-context-os-setup), run first
│   ├─ Capturing a call, document or transcript? → O9 Ingest (operating/O9-ingest)
│   ├─ Cleaning up stale, contradicted or duplicate items? → O8 Dream (operating/O8-dream)
│   ├─ Checking the base's structure? → O7 Graph Health (operating/O7-graph-health)
│   └─ Running the weekly cadence? → O6 Weekly Review (operating/O6-weekly-review)
│
└─ "The profile is thin, or the market has moved"
    ├─ Who the customer really is? → O15 GTM Discovery (operating/O15-gtm-discovery)
    ├─ How to position and price? → O14 GTM Positioning (operating/O14-gtm-positioning)
    ├─ Planning a launch? → O13 GTM Launch (operating/O13-gtm-launch)
    └─ Making growth repeatable after launch? → O12 GTM Engine (operating/O12-gtm-engine)
```

---

## Input/Output Reference

Every hand-off block carries a `run_date` line directly after its account line. Two instruments on one deal are compared by the date they ran, never assumed to be the same day. Every sales skill also returns a `report_path` (`none (inline)` unless the user asked for a file) and a `next_action` (one step, with its owner and a date). The field names in the Output column are the exact names the skill's Output Contract uses.

### Prospect Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **01 Account Qualification** | Account name, your role | CRM access, website, headcount, revenue | `verdict` (GREENLIGHT, MANUAL REVIEW or DISQUALIFY), `zone_scores`, `icp_match`, `fit_narrative`, `next_action`, `report_path`. The eight-criteria scorecard feeds `icp_match` and `fit_narrative`. It does not set the verdict |
| **02 Account Snapshot** | Account name, your role | CRM access, prior interactions, a persona to focus on | `account_status`, `verdict`, `zone_scores`, `contact_priority`, `pain_hypotheses`, `sequence` (three emails per persona), the eight-section cheatsheet |
| **03 Research Outbound** | Account name, the research source and where it is | Personas to target | `verdict` with zones, `signal_map`, `wedge` (arithmetic shown), `pov_brief`, `persona_emails` (personas times steps) |
| **04 Trigger Event Outbound** | Account name, the event, its date and its source | Affected stakeholders | `trigger_type`, `urgency_window`, `days_remaining`, `event_tag`, `sequence` (three emails per persona), or a refusal when the window has closed or the date is unknown |
| **05 Closed-Loss Reactivation** | Account name, the CRM loss reason, the close date | AE notes, prior sequence history | `loss_classification`, `change_assessment` (tagged), `reactivation_strategy` (REACTIVATE, MONITOR or RETIRE), `history_opener`, sequences and call prep |

### Discover Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **06 Meeting Prep** | Account name, meeting type (discovery or demo), attendees with titles | CRM notes, prior call notes, the upstream hand-off fields | `prep_sheet` (seven sections, with the call flow and the follow-up draft among them), `top_pain`, `question_bank`, `attendees` (with buying role), `proof_point` (with its Status), `next_action` |
| **07 Daily Prospecting** | Today's task or account list, your role | Activity history, priority overrides | `dial_sheet` (Hot, Warm, New, Recycle), `pre_call_briefs` (top eight), `exclusions` (each with its reason) |

### Execute Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **08 Deal Pulse** | Account name with an open opportunity, CRM access | Call notes, emails | `health_score` (0 to 100), `risk_level`, `pillar_scores` (4), `signal_scores` (16), `next_actions`. Read by 09, 13 and 06 |
| **09 MEDDPICC Analysis** | Account name, opportunity amount, deal stage, CRM access | Contact names and titles | `meddpicc_scores` (8, with the weighted table), `health_score`, `stage_minimum_met`, `stage_recommendation` (ADVANCE, HOLD, DOWNGRADE or DISQUALIFY), `risk_patterns`, five next actions. Read by 10, 11 and 14 |
| **10 Stakeholder Mapping** | Account name, known contacts with titles | Org chart, call mentions | `threading_score` (0 to 10, seven dimensions shown), `buying_roles`, `ghost_nodes` ("UNKNOWN, role", never a name), `champion_status` (Strong, Developing or None, with the tests met). Read by 09 and 06 |
| **11 Competitive Strategy** | Account name with an open opportunity, the competitor or incumbent | Prospect feedback, competitor intelligence with its source | `incumbent_type` (one of the seven), `threat_level`, `gap_matrix`, `battlecard`, `win_plan`. Only Verified proof points enter a talk track. Read by 06 and 12 |
| **12 Competitive Displacement** | Target account, the incumbent product | Incumbent failure signals with their source | `incumbent_type`, `displacement_difficulty` (Low, Medium or High), `target_personas`, `sequence`. Read by 02 and 06 |

### Close & Handoff Stage

| Skill | Required Input | Optional Input | Output |
|-------|---------------|---------------|--------|
| **13 Call Coaching** | Transcript or detailed notes, call type (discovery or demo) | Methodology preferences from the profile | `call_score` (discovery N of 35, demo N of 40), `category_scores` (one from 1 to 5 each), `focus_area`, `coaching_points` (each with a quote or an evidence grade), `key_moments` (seven types), `champion_status`. Read by 08, 09 and 06 |
| **14 Sales Handoff** | Deal summary, stakeholders, contracted modules, kickoff date | Technical requirements, data sources | `readiness_score` (0 to 100), `dimension_scores` (6), `three_dates` (kickoff, go-live, full adoption), `risks`, `quick_wins`. Read by the implementation lead and Wrap-Up |

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
Research Outbound (03)
  hands signal_map, wedge, pov_brief, persona_emails
  → Response / meeting booked?
    → Meeting Prep (06) [discovery]
      hands prep_sheet, top_pain, question_bank, attendees, proof_point
      → After call: Call Coaching (13)
        hands call_score, category_scores, focus_area, coaching_points, key_moments, champion_status
        → Deal Pulse (08)
          hands health_score, risk_level, pillar_scores, signal_scores, next_actions
          → Meeting Prep (06) [demo]
```
Every hand-off block names its account and its run date, so two instruments on one deal are compared by date, never assumed to be the same day.

### Pattern 3: Pipeline Review (Manager)
```
Deal Pulse (08) on all commit deals
  hands health_score, risk_level, pillar_scores, signal_scores, next_actions
  → Flag deals under 60 health score
    → MEDDPICC Analysis (09) on flagged deals
      hands meddpicc_scores, health_score, stage_minimum_met, stage_recommendation, risk_patterns
      → Stakeholder Mapping (10) on deals with fewer than 3 known contacts
        hands threading_score, buying_roles, ghost_nodes, champion_status back to 09 and on to 06
```
Stage words after a slip follow one rule in 08 and 09. HOLD comes with a dated action. DOWNGRADE moves the deal back one stage if the date passes unconfirmed, and never back to Discovery once the pain is confirmed.

### Pattern 4: Competitive Deal
```
Competitive Strategy (11)
  hands incumbent_type, threat_level, gap_matrix, battlecard, win_plan
  → Meeting Prep (06) [with battlecard context]
    → After call: Call Coaching (13)
      → Deal Pulse (08) [updated with competitive signals]
  → Competitive Displacement (12) [when the same incumbent sits in TARGET accounts]
    hands incumbent_type, displacement_difficulty, target_personas, sequence to 02 and 06
```

### Pattern 5: Deal Close + Handoff
```
MEDDPICC Analysis (09) [final qualification check]
  hands meddpicc_scores, health_score, stage_minimum_met, stage_recommendation, risk_patterns
  → stage_recommendation ADVANCE and the Stage 6 minimum met?
    → Sales Handoff (14) [readiness check two weeks before signature, handoff at signature]
      hands readiness_score, dimension_scores, three_dates, risks, quick_wins
      → the implementation lead, and Wrap-Up for the session close
```
A HOLD from 09 runs 14 as a preview only. No handoff is issued without the three dates.

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
- **Scale:** 0-100 health score, the sum of the 16 signal values divided by 16, rounded half up
- **Pillars:** Why Anything (macro need), Why Us (differentiation), Why Now (urgency), Execution (process mechanics), 4 signals each
- **Each signal:** GREEN (100, strong evidence) / YELLOW (50, partial) / RED (0, missing or negative)
- **Risk bands:** 85 to 100 Low Risk, 46 to 84 Medium Risk, 0 to 45 High Risk
- **Pillar weakness step:** if any pillar average is below 30, the risk level rises one step. The step is taken once, however many pillars fall below 30. A pillar average of exactly 30 does not trigger it
- **Pillar bands:** 75 or more GREEN, 26 to 74 YELLOW, 25 or less RED

### MEDDPICC (Skill 09)
- **Scale:** each of the 8 elements scored 1-5, weighted into a 0-100 health score (the weighted Total divided by 5, multiplied by 100, rounded)
- **Weights:** Economic Buyer 20%, Metrics 15%, Identified Pain 15%, Champion 15%, Decision Criteria 10%, Decision Process 10%, Paper Process 10%, Competition 5%
- **Bands:** 80-100 GREEN, 60-79 YELLOW, 40-59 ORANGE, 0-39 RED
- **Stage minimums (the skill's defaults):**
  - Stage 2 Discovery needs 30 or higher, with Identified Pain at 3 or higher
  - Stage 3 Demo and Stage 4 Proposal need 50 or higher, with Identified Pain, Champion and Decision Criteria at 3 or higher
  - Stage 5 Negotiate needs 65 or higher, with every element except Competition at 3 or higher and Economic Buyer at 4 or higher
  - Stage 6 Closed-Won and Handoff needs 75 or higher, with every element at 3 or higher and Economic Buyer and Paper Process at 4 or higher
- **Profile override:** where the profile's Qualification Stage Gates state a different figure, the profile's figure is the minimum and the report says so (the PlotIQ examples use 70 for Stage 5 Negotiate)
- **Stage words:** ADVANCE, HOLD, DOWNGRADE, DISQUALIFY

### Call Coaching (Skill 13)
- **Discovery (SPIN, Priority Ladder and Alternatives):** 7 categories, out of 35. 31 to 35 Excellent, 24 to 30 Good, 17 to 23 Needs Improvement, 10 to 16 Poor, 7 to 9 Critical
- **Demo (Challenger, MEDDPICC and Question the Problem):** 8 categories, out of 40. 34 to 40 Excellent, 26 to 33 Good, 18 to 25 Needs Improvement, 10 to 17 Poor, 8 to 9 Critical
- **Per category:** a score from 1 to 5 with specific behavioral criteria, and a quote from the transcript or an evidence grade (Strong, Moderate, Weak) on every coaching point
- **Talk time and champion tests:** the shared bands and the shared champion tests in the Shared Contract, used by 06, 09, 10 and 13 alike

### Account Qualification (Skill 01)
- **Scale:** 8 criteria, each scored STRONG / PARTIAL / WEAK / UNKNOWN, plus the five qualification zones, each scored HIGH, MEDIUM, LOW or UNKNOWN
- **Verdict:** comes from the profile's Verdict Rule, applied as written. The skill's defaults are:
  - GREENLIGHT applies when at least two zones are HIGH, no must-have zone (1 or 3) at LOW, and no disqualifier applies
  - DISQUALIFY applies when a disqualifier applies, or when both must-have zones (1 and 3) are LOW
  - MANUAL REVIEW covers every other case
- **MEDIUM never counts as HIGH.** The eight-criteria scorecard does not gate the verdict. It feeds `icp_match` and `fit_narrative`
- **Includes:** trigger detection, risk flags, fit narrative

---

## The Operating Layer

The 15 skills in `operating/` are not stage-specific. They run around the sales work. Each one adds an optional section of its own to the client profile, which its `CUSTOMIZE.md` interview writes. Which one to use, what each reads from the profile, and the order to set them up in are in [How It Fits Together](how-it-fits.md).

The three families below use the same layout. Each table gives one line per skill. It names what the skill does, what it reads, and the field names it hands on. The shared words for each family come after its table, quoted from the skill files.

### Verification Family

| Skill | What It Does | Reads | Hands Off |
|---|---|---|---|
| O1 Verify (`operating/O1-verify`, 2.0.0) | Holds each claim of done to a tier and states the tier it reached | The `## Verification` section, the claim and its work, the check output from this session | The claim slip, the tier statement, the Common Failures table, the honest sentence |
| O2 Debug (`operating/O2-debug`, 2.0.0) | Finds a root cause one hypothesis at a time, and stops at the circuit breaker | Its profile section, any earlier handoff file for the same symptom, the error and the file it names | The hypothesis card, the outcome block (Root cause, Fix, Test name, Red run, Green run, Reproduction, Reproduction output, Confirmed by, Gate), the handoff file (Problem, Hypotheses, Now believed, Next action) |
| O3 Debate (`operating/O3-debate`, 2.0.0) | Runs a panel of opposing experts on a decision and ends with a matrix | Its profile section, the work the decision touches, the Context Gap result, earlier decision records | Intent line, Cast, Round One, Round Two, the decision matrix, Resolution (posture converge or diverge), the decision record |
| O4 Context Gap (`operating/O4-context-gap`, 2.0.0) | Searches before anything is built and writes one of six gap states | Its profile section, the codebase, the knowledge base if the profile names one, the project's notes | The gap result, with the fields Date, Need, Assumptions, Searched, Findings, State, Evidence and Next step |
| O5 Second Opinion (`operating/O5-second-opinion`, 2.0.0) | Sends a diff to a reviewer from a different vendor and triages what comes back | Its profile section, the target diff only, earlier review files for the same target | The target line, the manifest, the packet, the routing line, the triaged list, and the header fields `verdict`, `finding_count`, `triaged_list`, `review_file` |

**Shared words in the verification family.** The five skills use these words exactly as written.

- **Claim slip.** Every claim of done is a claim slip with four fields, in this order (`Claim`, `Tier`, `Check`, `Evidence`). The evidence is pasted, not described.
- **Four tiers.** Tier 1 Exists, Tier 2 Substantive, Tier 3 Wired, Tier 4 Functional. "Tier 4 is called **Functional** everywhere." When tier 4 was not reached, the sentence is "Built, and not yet verified, because [reason]."
- **Six gap states.** NO GAP, CONFIG, COMPLETION, EXTENSION, PATTERN, TRUE GAP. Every search ends in exactly one of them. Each state is set out for code and for documents in O4's Gap Classifier.
- **Six-column matrix.** Option, Wins, Breaks, Risk, Effort, Best when. Every option gets a row, including the ones the panel rejected. The posture is converge or diverge.
- **Circuit breaker.** "Three attempts is data." After the third failed hypothesis the session stops, writes the handoff and re-plans. There is no fourth guess.
- **Review verdicts.** APPROVED, CHANGES_REQUIRED or BLOCKED. Severity is BLOCKING, WARNING or NIT. Triage is AGREE or DISAGREE, or NEEDS-A-LOOK.

### Memory Family

| Skill | What It Does | Reads | Hands Off |
|---|---|---|---|
| O6 Weekly Review (`operating/O6-weekly-review`, 2.0.0) | Writes one dated record a week, so health becomes a trend | Last week's record, the latest Graph Health report and Dream log, open continuation notes, its profile section, the base for claims with re-grade dates | Frontmatter fields `skill`, `type`, `week_ending`, `structure_score`, `content_count`, `items_archived`, `tag_sprawl`, `orphans`, `hubs`, `emergent_past_30`, `emergent_past_60`, `broken_links`, `items_written`, `expiring_soon`, `carried_over`, `uncommitted_repos`; body sections Carried Over, System Health, What Needs Attention, Next Week |
| O7 Graph Health (`operating/O7-graph-health`, 2.0.0) | Scores the base's structure, meaning tags, links, provisional age and broken links | Its profile section, the item fields, the last report | `structure_score`, `tag_sprawl`, `orphans`, `hubs`, `emergent_past_30`, `emergent_past_60`, `broken_links`, the band, Decisions Returned |
| O8 Dream (`operating/O8-dream`, 2.0.0) | Finds stale, contradicted and duplicate items and proposes changes. It never deletes | Its profile section, item frontmatter and compiled truth, the latest Graph Health report, the last dream log | Mode line, Findings, Applied list, Approval list, the content count and its band, the dream log entry (`items_archived`, `content_count_before`, `content_count_after`, `next_run`) |
| O9 Ingest (`operating/O9-ingest`, 2.0.0) | Turns a call, document or transcript into knowledge items with a timeline | Its profile section, the `## Knowledge Base` section, the tag list if one exists, the base itself | Item frontmatter (`name`, `description`, `domain`, `node_type`, `status`, `created`, `updated`, `valid_until`, `tags`, `related`, `source`), appended timeline entries, the save report |
| O10 Wrap-Up (`operating/O10-wrap-up`, 2.0.2) | Writes the continuation note that lets someone resume a session cold | Its profile section, the continuation notes already in the project folder, the session and the files it changed | Continuation note frontmatter (`skill`, `type`, `date`, `project`, `context`, `status`, `next_action`, `blockers`, `supersedes`); sections What Happened, Where We Stopped, Decisions Made, Open Threads |
| O11 Context OS Setup (`operating/O11-context-os-setup`, 1.1.2) | Builds the two-layer knowledge base that the memory skills read | The folder structure, existing notes, the team's workflow, the client profile if it exists | Directory structure (Layer 1 and Layer 2), taxonomy of blessed tags, ontology, documentation guide, first ingest, and a `## Knowledge Base` section in the profile |

**Shared words in the memory family.** Wrap-Up, Ingest, Dream, Graph Health and Weekly Review carry the same contract. O11 is on version 1.1.2 and does not carry this contract or the evidence ladder of the 2.x skills. Its changelog says it names the item field list the memory skills share.

- **The record.** Every knowledge item has two zones. "**Compiled truth** at the top, one to three sentences, rewritten whenever understanding changes." Underneath, the "**Timeline**" holds dated entries in reverse order, append-only, with exact quotes never paraphrased. "The top can be wrong and fixed. The bottom is the audit trail."
- **One definition of stale.** "An item is **stale** when it is past its `valid_until`, or, when it has none, when its `updated` date is more than 90 days old and its status is still `emergent`." Age comes from the frontmatter dates, never from file modification time. An item past its `valid_until` counts as expired, never also as stale.
- **The expiry model.** `valid_until` is optional. "**Expiring soon** means within three days." An expired item is offered an extension before it is archived. Use protects an item from age. An item used often is never archived for age alone.
- **Two scores, one band table.** The **Structure score** belongs to Graph Health and never counts content age or truth. The **Content count** belongs to Dream. Both start at 100, and both report the same bands, **90 to 100 Excellent, 70 to 89 Good, 50 to 69 Fair, under 50 Poor.** Weekly Review records both numbers. Every rate in these reports carries its n, and a measure nobody checked is `null`, never zero.

### Strategy Family

| Skill | What It Does | Reads | Hands Off |
|---|---|---|---|
| O15 GTM Discovery (`operating/O15-gtm-discovery`, 2.1.0) | Finds out who the customer really is, with every claim graded | The team's own beliefs, the profile sections Company, ICP Definitions, Buyer Personas, Core Pain Points and Competitive Landscape, the deal history, its `## Discovery` section | Customer archetype, Competitive alternatives, Beachhead segment, Buyer persona, Open bets (`Load-bearing:`, `Do not build on:`, `Other open bets:`) |
| O14 GTM Positioning (`operating/O14-gtm-positioning`, 2.0.1) | Tests a positioning statement, its graded proof, a price and a message set | Discovery's five fields, the profile sections named in its Input Contract, deal and pricing history, its `## Positioning` section | Positioning statement, Value proposition, Proof ledger, Message set, Price and value metric, Economics, Open bets |
| O13 GTM Launch (`operating/O13-gtm-launch`, 2.0.1) | Plans a launch with capped channels and kill dates, then reviews at day 30 | Its `## Launch Plan` section, its `## Positioning` section, Company, Buyer Personas, Competitive Landscape, Proof Points, the Positioning and Discovery hand-offs, and Engine's hand-off in Results mode | Part A, written before launch, holds Motion decision, Kill rules per channel, Proof stack, Content plan, Roster, Funnel targets, Economics status, Experiments, Launch budget, Launch date. Part B, written at day 30, holds Launch data, Current customers and retention, Open-bet test results, Conversion rate with n, Lead quality, Economics status (day 30) |
| O12 GTM Engine (`operating/O12-gtm-engine`, 2.0.0) | Finds the bottleneck, then runs a scored backlog in two-week sprints | Its `## Growth System` section, the approver named in `## Launch Plan`, Company, ICP Definitions, Buyer Personas, Proof Points, the Launch and Positioning hand-offs, Discovery's archetype | Retrospective, Bottleneck, Backlog, Sprint record, Loop design, Narrative, Sequences, Metrics board, Vacation test, Re-grade requests, Open bets returned, Growth System |

**Shared words in the strategy family.** O14 and O15 define the evidence ladder in their own Evidence Ladder section. O12 and O13 quote its grade words from the hand-off, unchanged.

- **The evidence ladder.** "Every claim sits on exactly one rung. The rung is shown wherever the claim appears." The rungs, in order, are `assumed` (somebody believes it), `heard` (a buyer said it), `seen` (it shows in behavior or data) and `confirmed` ("Seen across at least 5 cases, recent, and not contradicted"). "A claim cannot move to `confirmed` while a contrary case is unexplained."
- **Published rules.** A requirement written in a public rule is graded `seen` on the rule's text, with its source and date beside the grade. It never reaches `confirmed`, because that rung counts cases (O14).
- **Hand-off fields.** Each skill quotes the field names of the skill before it. "Keep the names exactly as written." A hand-off block quotes every field in full, "with no ID-only entries and no 'see above' pointers." The brief links to the nodes and "does not copy them."
- **Grades are quoted, not changed.** "Launch does not regrade a claim up or down." Engine writes Re-grade requests and "does not change the grade itself." The owning skill applies the change on its next run.

### Context OS Setup and the Operating Hand-Offs

Context OS Setup (O11) sits in the memory group because it builds the base that Ingest, Graph Health, Dream and Weekly Review read. Run it first. It does not use the evidence ladder, and the Output Contract lists the base's structure rather than graded claims.

---

## Tips for Better Output

1. **Give Claude more context, not less.** Paste CRM notes, call transcripts, email threads. The skills are designed to filter and prioritize. Let them do the work.

2. **Be specific about what you want.** "Score this deal" works. "Score this deal, focusing on the champion gap and whether we have a paper process mapped" works better.

3. **Chain skills deliberately.** Run Account Qualification before Account Snapshot. Run Deal Pulse before MEDDPICC Analysis. Each skill's output enriches the next.

4. **Trust the methodology, question the data.** If a Deal Pulse score feels wrong, check whether Claude had enough context. A low score with good data is a real warning. A low score with sparse data just means you need to feed it more.

5. **Update your Client Profile.** After 30 days, review. Did new competitors emerge? Did you close a deal worth adding as a proof point? Did a pain point climb in priority? Keep the profile current.
