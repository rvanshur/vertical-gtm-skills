# Changelog

What changed in this repo, newest first. Each skill also keeps its own Changelog section at the
bottom of its `SKILL.md`, with the detail.

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

**One example company, now PlotIQ.** Every worked example in the docs and the 15 operating skills uses PlotIQ, a made-up software company for cemeteries and funeral homes. The 14 sales skills under `skills/` still use the earlier Lexora cast, and they switch to PlotIQ when they are rebuilt (the last phase of the 2.0 program), so until then the two groups do not share an example. Its completed profile, with the full cast of accounts, people, competitors, proof points and verdicts, is [`profiles/examples/plotiq-example.md`](profiles/examples/plotiq-example.md). The Lexora profile is retired and moved to [`profiles/examples/archive/lexora-legal-ops-example.md`](profiles/examples/archive/lexora-legal-ops-example.md).

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
