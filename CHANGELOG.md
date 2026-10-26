# Changelog

What changed in this repo, newest first. Each skill also keeps its own Changelog section at the
bottom of its `SKILL.md`, with the detail.

---

## 2026-10-25: Sales 2.1 (All 14 Sales Skills)

**The sales skills read the knowledge base.** A new part of the Shared Contract, The Knowledge Base and Connectors, has every sales skill read the base that Context OS Setup builds, through the `Location` field of the profile's `## Knowledge Base` section, the same way the operating skills do. Each skill's Context table names the base items it opens (the account's folder under `accounts/`, and where it needs them, competitors under `gtm/` and personas under `people/`). A fact taken from the base keeps its grade, so an `assumed` item is never used as the claim.

**Connectors, read only.** When the assistant is connected to the CRM or a call recorder, a skill offers to read the records the user points at, asks first, tags each fact `[CRM]` or `[Call]` with its date, and never writes back. Pasting still works the same way.

**Chains and kits.** Each skill now names the chains it belongs to (Qualify To Book, Daily Pipeline, Win Back, Work The Deal, Beat The Incumbent, Close And Hand Off), and `docs/how-it-fits.md` lists the chains with the fields that pass between steps. The six skills whose hand-offs the Business Case & ROI Kit (a paid Guild Pro kit) reads name those fields in a Guild Pro Kits subsection. Every skill stays free and works without any kit.

---

## 2026-10-20: Sales 2.0, Wave Two (Skills 08 to 14)

**All 14 sales skills are now one system.** Deal Pulse, MEDDPICC Analysis, Stakeholder Mapping, Competitive Strategy, Competitive Displacement, Call Coaching and Sales Handoff are at 2.0.0, each brought to the skill standard in place and each carrying the same Shared Contract as wave one. The champion tests, the seven incumbent types and the talk-time bands appear once per skill, inside the contract, and nowhere else.

**Hand-offs by field name, with a run date.** Each skill's Output Contract names the fields the next skill asks for (`health_score`, `risk_level`, `pillar_scores`, `signal_scores`, `meddpicc_scores`, `stage_recommendation`, `threading_score`, `ghost_nodes`, `champion_status`, `incumbent_type`, `gap_matrix`, `displacement_difficulty`, `call_score`, `coaching_points`, `key_moments`, `readiness_score`, `three_dates` and the rest). Every worked example ends with a hand-off block that names its account, its status and its run date, so two instruments on one deal are compared by date. The seven wave-one skills take 2.0.1 for the same line. Fresh-agent hand-off tests ran on 08 to 09, 09 to 10, 09 to 14, 13 to 08 and the session close.

**Every scoring table is recomputed.** The family checker now parses each example's table (sixteen Deal Pulse signals, the eight MEDDPICC weights, the seven threading dimensions, the Call Coaching categories, the six readiness dimensions) and matches the printed total and the hand-off score to the rows.

**What each skill gained.** Deal Pulse names its four methods in plain words and states the pillar-weakness rule precisely. MEDDPICC uses one set of stage words (ADVANCE, HOLD, DOWNGRADE, DISQUALIFY) and one rule after a slip, shared with Deal Pulse: HOLD with a dated action, then DOWNGRADE one stage, never back to Discovery once the pain is confirmed. Stakeholder Mapping adds the non-buyers who still shape a deal, writes every ghost node as a role, and shows the threading formula. Competitive Strategy carries the failure-pattern and trend tables and lets only Verified proof into a talk track. Competitive Displacement has a template per incumbent type, a directional difficulty scale, and the rule that every number in an email has a named, dated source. Call Coaching adds an Alternatives category (discovery is now 7 categories out of 35, bands restated with the arithmetic), demo pacing defaults, evidence grades on every coaching point, seven key-moment types, the unraised-objections checklist and the demo return-on-investment formulas with blank inputs. Sales Handoff reads an Implementation Profile from the profile, states the two-month default with every adjustment's arithmetic, and never issues a handoff without the three dates.

**Template and example.** The seven wave-two profile sections (Deal Health, MEDDPICC, Buying Committee, Competitive Patterns and Trends, Displacement, Call Coaching, Implementation Profile) now have a fixed shape in the template, and the PlotIQ example fills each one (with `[RECORD]` where a beta company has no history). Proof Points gains a Displaced vendor column.

**Docs.** README rows 8 to 14, the skill reference (the Execute and Close tables with field names, patterns 2 to 5 rewritten with the hand-offs, the scoring reference), and the read-count tables in `docs/how-it-fits.md` and `docs/customization.md`, recounted from the 14 Context tables.

---

## 2026-10-20: Sales 2.0, Wave One (Skills 01 to 07)

**The seven prospecting and discovery skills are one system.** Account Qualification, Account Snapshot, Research Outbound, Trigger Event Outbound, Closed-Loss Reactivation, Meeting Prep and Daily Prospecting are at 2.0.0, each brought to the skill standard in place and each carrying the same Shared Contract under its Context section: five account status words, three verdict words spelled one way, stage names read from the profile, one set of six evidence tags, the rule that every rate carries its n, report first and a file only when asked, nothing sends and nothing writes to the CRM, the BDR guard, and one list each for champion tests, incumbent types and talk-time bands.

**Hand-offs by field name.** Each skill's Output Contract names the fields the next skill asks for (`verdict`, `zone_scores`, `contact_priority`, `pain_hypotheses`, `trigger_type`, `urgency_window`, `days_remaining`, `reactivation_strategy`, `history_opener`, `prep_sheet`, `top_pain`, `question_bank`, `dial_sheet`, `pre_call_briefs`, `exclusions` and the rest), every worked example ends with a hand-off block in those names, and every skill carries `next_action` and `report_path` for the session close. Fresh-agent hand-off tests ran on 01 to 02, 02 to 06, 02 to 04, 05 to 04 and 06, 04 and 07 to 06, and the close.

**What each skill gained.** Verdicts come from the profile's Verdict Rule alone, with every zone shown (UNKNOWN allowed when there is no evidence). Trigger windows come from the profile, with one window rule and a refusal when the event is undated or the window has closed. Closed-loss outcomes are REACTIVATE, MONITOR or RETIRE. Meeting Prep carries a question bank per discovery phase, objection scripts, a minute-by-minute call flow and a follow-up email draft. Daily Prospecting scores against a Fit Grid in the profile and applies the BDR guard with the pending-assignment case stated. No Illustrative proof point is ever placed in an email, talk track or battlecard a prospect reads.

**Template and example.** `profiles/client-profile-template.md` gains a "Persona who acts" column on Buying Triggers, a "Discovery question" column on Core Pain Points, two post-purchase pain columns and the seven incumbent types on Competitive Landscape, a Status (Verified, Benchmark or Illustrative) on Proof Points, numbered stage names, an optional talk-time override, and a Sales-Layer Sections block naming the section each sales skill's `CUSTOMIZE.md` writes. The PlotIQ example fills them all, with one calendar every example counts from.

**Docs.** README rows 1 to 7, the skill reference (inputs, outputs and the chaining patterns rewritten with field names), the profile maps in `docs/how-it-fits.md` and `docs/customization.md`.

Skills 08 to 14 followed the same day, in the entry above.

---

## 2026-10-18: Verification 2.0, Five Skills Rebuilt as One System

**The five verification skills (Verify, Debug, Debate, Context Gap, Second Opinion) are 2.0.0.** Each was written clean-room from one spec, and they share one contract, pasted word for word into all five: the claim slip (claim, tier, check, evidence), four tiers with Functional as tier 4 everywhere, the honest sentence when tier 4 was not reached, one spelling of the six gap states, the six-column matrix, the severity, verdict and triage words, three attempts as the circuit breaker, and the list of what the session close reads by name.

**What each one gained**
- **Verify**: grades every claim by the tier it reached and writes a claim slip with the evidence pasted, never described. Reading never reaches tier 4. Never round up: the count and the list of failures, not "mostly passing". The Common Failures table and the triggers list.
- **Debug**: five bug classes as modes, a failing test first for code, one change per hypothesis, the circuit breaker at three, a four-line handoff file, and an outcome block that carries the red run and the green run so Verify can grade it.
- **Debate**: rewritten from scratch (the earlier version adapted two MIT-licensed skills, and the credits section goes with it). The opposition is assigned, one seat always attacks the premise with three tests, the matrix has Option, Wins, Breaks, Risk, Effort and Best when, with a converge or diverge posture and an archetype bank at the end.
- **Context Gap**: thirty seconds to write the need, four places searched, one of six states with its evidence, extend over create, and a result that Debate reads before it seats a panel.
- **Second Opinion**: paste as the default route, a dry-run manifest of what leaves the machine with the hold-back list, the five-lens brief, exact severity, verdict and triage words, and the line that an APPROVED verdict alone is tier 1 evidence until Verify runs the work.

**Fixed across the set**: Verify, Debug and Second Opinion agree on what a verdict proves, Context Gap hands Debate a state in the same words Debate expects, and Wrap-Up 2.0.1 (shipped alongside) names a place for each skill's output.

The worked examples use the PlotIQ cast and one story (the trust-report export) that runs through all five. The 1.x versions stay in history.

---

## 2026-10-18: Memory 2.0, Five Skills Rebuilt as One System

**The five memory skills (Wrap-Up, Ingest, Dream, Graph Health, Weekly Review) are 2.0.0.** Each was written clean-room from one spec, and they now share one contract, pasted word for word into all five: one record format (compiled truth on top, dated timeline below), one set of item field names, one definition of stale, one expiry model (`valid_until`, expiring within three days, extension before archive, no expiry on standing records), and two scores on the same four bands (Graph Health's structure score, Dream's content count).

**What each one gained**
- **Wrap-Up**: the owner confirms the one next action before anything is written, a new note marks the older note for the same project `superseded`, same-day reruns update instead of duplicating, a debrief before closing, the checks each changed file earns, `status: draft | approved | superseded`.
- **Ingest**: two zones in every item, asks before creating a person record, three or more links on every item, suggests an expiry only for time-bound facts, a routing table, keeps durable facts after research, accepts a file, a folder, pasted text or a summary of the conversation.
- **Dream**: three modes (gentle, standard as the default, deep), confirm before flag, dry-run before write, de-link never de-line as a hard rule, a content count with capped deductions and an expiry bonus, a dated log, a two-week cadence plus a run whenever the structure score falls into Fair.
- **Graph Health**: a structure-only score with caps (content age and expiry moved to Dream), orphans as a share, a link defined as a distinct target counted once, every crossed threshold returned as a decision, `uncertain` counted as its own group.
- **Weekly Review**: null is not zero as a hard rule, the local date, a same-day rerun replaces the file, records never edited, both scores and Dream's archived count recorded, at most one priority per area.

**Fixed across the set**: Ingest no longer produces orphans by Graph Health's rule (two links versus three), `archived` is a status every skill knows, `emergent_past_30` and `emergent_past_60` are non-overlapping bands everywhere, the tag-sprawl labels match (Healthy, Warning, Unhealthy), and Dream no longer borrows Graph Health's score.

The worked examples use the PlotIQ cast and one story that runs through all five. The 1.1.0 versions stay in history.

---

## 2026-10-13: The Example Company Is PlotIQ

**One example company, now PlotIQ.** Every worked example in the docs and the 15 operating skills uses PlotIQ, a made-up software company for cemeteries and funeral homes. The 14 sales skills under `skills/` moved to the same cast the same day, at version 1.3.0, so every example in the repository runs on one company. Its completed profile, with the full cast of accounts, people, competitors, proof points and verdicts, is [`profiles/examples/plotiq-example.md`](profiles/examples/plotiq-example.md). The Lexora profile is retired and moved to [`profiles/examples/archive/lexora-legal-ops-example.md`](profiles/examples/archive/lexora-legal-ops-example.md).

**Template**
- The profile template gains a **Qualification Zones** section. Five groups of account traits are each scored HIGH, MEDIUM or LOW. Zones 1 and 3 are must-haves, and the section states the verdict rule. Skills 01, 03, 06 and 07 read it.

**Renames and credits**
- Two framework names were renamed: Question the Problem and Priority Ladder.
- The Debate and Context OS Setup credits were updated.

---

## 2026-09-29: Final Pass Before Wider Release

**One case study, everywhere.** Every worked example in all 29 skills and the docs now uses the
same fictional company, Lexora (a legal-ops platform), and the same cast of accounts, people and
competitors. The cast is defined once, at the bottom of
[`profiles/examples/legal-ops-example.md`](profiles/examples/legal-ops-example.md), so you can
follow one deal (Corvane Industrial) from qualification to handoff.

**New docs**
- [`docs/how-it-fits.md`](docs/how-it-fits.md): how the profile, the 14 sales skills and the 15
  operating skills connect, what to set up first, which operating skill to use when, and what
  each skill reads from the profile.
- This changelog.

**Operating skills (O1 to O15)**
- Every operating skill now reads the profile section its `CUSTOMIZE.md` interview writes.
  Before this, the interviews told you to add a section the skill never loaded.
- **O5 Second Opinion 1.1.0** now works when the assistant running it is the builder's own
  vendor: it builds a review packet for a different vendor (paste into another vendor's chat, a
  second vendor's CLI, or an API call) and triages the findings that come back.
- **O11 to O13:** customization interviews expanded to match the others ("what to expect",
  profile sections, "if you are stuck"). O12's had a broken code block.
- **O12 to O15:** the Context sections name the profile sections they read, and say that
  validated findings go back into the profile, which is how strategy reaches the sales skills.
- **O15:** The Mom Test credited to Rob Fitzpatrick. Examples moved to the Lexora case study.

**Sales skills (01 to 14)**
- Worked examples rewritten around the Lexora case study (version 1.2.0 each).
- **14 Sales-to-CS Handoff:** profile section names now match the template (Core Pain Points,
  Product Modules), and the third date of the handoff plan is renamed "Full Adoption Date"
  (it was "Full Service Date", an internal term that meant nothing outside one company).

**Profile**
- The template gains a **Product Modules** section (Sales-to-CS Handoff reads it) and a note on
  the optional operating-layer sections.
- The Lexora example gains Product Modules, an adjacent competitor (LedgerLine Audit, an
  outsourced bill review service) and the Example Cast.

**Docs corrected**
- README and `CLAUDE.md` / `AGENTS.md` describe all 29 skills. The agent instructions route to
  every operating skill, not just O1.
- The customization guide opens with which profile sections feed which skills, and points to
  headings that exist. The skill reference's scoring section now matches the skills: Deal Pulse
  risk bands are 85 / 46 / 0, MEDDPICC is a weighted 0-100 score (not an unweighted /40), and the
  Call Coaching bands are the skill's own.
- Codex and ChatGPT setups are labelled as documented but not yet walked through end to end.
- The starter kit's folder layouts put the profile where the skills look for it.
- Example metrics that came from a real company were replaced with the Lexora profile's own.

---

## 2026-09-29: Operator's Toolkit Operating Skills

O2 to O15 published alongside the Operator's Toolkit series.

## 2026-09-02: Front Door

Root `CLAUDE.md` / `AGENTS.md`, the ChatGPT GPT guide, and a `CUSTOMIZE.md` for all 14 sales
skills.

## 2026-08-25: The Operating Layer Begins

`operating/` added, starting with O1 Verify.

## 2026-07-06: Version 1.1.0 of the Sales Skills

Moved every sales skill from a per-skill profile block to one shared `profiles/client-profile.md`,
and gave every skill the five-part anatomy (Role, Input Contract, Output Contract, Methodology,
Context).
