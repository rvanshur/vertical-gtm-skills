# How It Fits Together

This repo is 29 skills and one data file. This page shows how they connect, so you know
what to set up first, which skill to reach for, and what each one reads and writes.

---

## The Three Layers

```
                    ┌─────────────────────────────────────────────┐
  STRATEGY          │ O15 Discovery → O14 Positioning → O13 Launch │
  (operating/)      │              → O12 Engine                    │
                    └──────────────────────┬──────────────────────┘
                                           │ validated findings are written into
                                           ▼
  CONTEXT           ┌─────────────────────────────────────────────┐
  (profiles/)       │         profiles/client-profile.md           │
                    │  ICP, personas, pains, competitors, proof    │
                    └──────────────────────┬──────────────────────┘
                                           │ read by every skill, written by none of 01-14
                                           ▼
  MOTION            ┌─────────────────────────────────────────────┐
  (skills/)         │ 01-05 Prospect · 06-07 Discover · 08-12      │
                    │ Execute · 13 Coach · 14 Handoff              │
                    └─────────────────────────────────────────────┘

  DISCIPLINE (operating/, runs around all of it)
    Verification  O1 Verify · O2 Debug · O3 Debate · O4 Context Gap · O5 Second Opinion
    Memory        O11 Context OS Setup → O9 Ingest · O8 Dream · O7 Graph Health · O6 Weekly Review
    Sessions      O10 Wrap-up
```

**The profile is the center.** The 14 motion skills in `skills/` read it and never write it.
The four strategy skills (O12 to O15) are how it gets filled with evidence instead of guesses:
they read what is there, test it, and what they validate goes back into the same sections.
The discipline skills run on any work at all, including work on the other skills.

If you only ever use `skills/`, the repo still works. The operating layer is what keeps the
profile honest and the output checked.

---

## Set Up in This Order

1. **Fill the profile.** Copy `profiles/client-profile-template.md` to
   `profiles/client-profile.md` and complete it. The
   [PlotIQ example](../profiles/examples/plotiq-example.md) shows the density to aim for.
   If you cannot fill the ICP, Personas or Competitive Landscape sections from evidence, run
   **O15 Discovery** and **O14 Positioning** first. That is what they are for.
2. **Run three motion skills** on real accounts. Pick them by role from the README.
3. **Add the verification skills** once you are producing work other people rely on. Start with
   **O1 Verify** and **O5 Second Opinion**.
4. **Build the knowledge base only when you need memory across weeks.** Run **O11 Context OS
   Setup** first. Ingest, Dream, Graph Health and Weekly Review all assume the knowledge base it
   creates, so running them before O11 gives them nothing to work on.
5. **Customize** a skill after you have a baseline from running it stock. See
   [customization.md](customization.md).

---

## Which Operating Skill, When

| You are about to... | Use | What it gives you |
|---|---|---|
| Build something new | **O4 Context Gap** | A written check of what already exists, sorted into six buckets, before any work starts |
| Commit to a plan or a big decision | **O3 Debate** | Three to seven opposing experts and a decision matrix where every option names what it wins and where it breaks |
| Fix something that is not working | **O2 Debug** | A hypothesis before every fix, and a stop after three failed attempts with a written handoff |
| Ship something another person will rely on | **O5 Second Opinion** | A review packet for a model from a different vendor, and a triage of what comes back |
| Say something is done | **O1 Verify** | A four-tier check (exists, substantive, wired, functional) and an honest statement of which tier you reached |
| End a working session | **O10 Wrap-up** | A continuation note with the exact state and one next action that someone can resume cold |
| Set up memory for the team | **O11 Context OS Setup** | A two-layer knowledge base, a starter taxonomy, and where it lives |
| Capture a call, document or transcript | **O9 Ingest** | Structured knowledge items with a timeline and links |
| Clean up what the base has collected | **O8 Dream** | Stale, contradicted and duplicate items found and pruned without deleting surrounding text |
| Check the base's structure | **O7 Graph Health** | A structure score (tag sprawl, link density, provisional item age) |
| Run the weekly cadence | **O6 Weekly Review** | A dated record of what changed, so health becomes a trend |
| Find out who the customer really is | **O15 GTM Discovery** | Archetype diagnosis, graded claims, real alternatives, a starting segment, open bets |
| Decide how to position and price | **O14 GTM Positioning** | A tested positioning statement, graded proof, a price set after the position, a message set |
| Plan a launch | **O13 GTM Launch** | A scored motion choice, capped channels with kill dates, a ranked proof stack, a war room, day-30 results |
| Make growth repeatable after launch | **O12 GTM Engine** | The bottleneck, a scored backlog with kill rules, two-week sprints, one growth loop, a narrative and sequences, a vacation test |

For the 14 motion skills, the decision tree in [skill-reference.md](skill-reference.md) does
the same job.

---

## What Each Skill Reads From the Profile

**Motion skills (01 to 14)** read the standard sections. This is also the order to fill them in,
because the first two feed nearly everything:

| Profile section | Read by (counted from the 14 Context tables, 2026-10-20) |
|---|---|
| Buyer Personas | 12 of the 14 motion skills (all but 01 and 14) |
| Competitive Landscape | 10 |
| Value Propositions | 10 |
| Proof Points | 9 |
| Qualification Criteria | 9 (its Buying Triggers and Disqualifiers tables included) |
| Core Pain Points | 7 (with the Discovery question column) |
| Company | 7 name it, and every skill uses it for framing |
| ICP Definitions | 5 (01, 02, 03, 05 and 07) |
| Qualification Zones | 5 (01, 02, 03, 07 and 11) |
| Sales Methodology | 5 (06, 08, 09, 11 and 13 calibrate to it) |
| Qualification Stage Gates | 3 (02, 06 and 07) |
| Market Segments | 01 |
| Product Modules | 14 Sales Handoff (implementation scope) |

**Sales skills** each also read one section of their own, which the skill's `CUSTOMIZE.md`
interview writes. The template's "Sales-Layer Sections" block lists them, and the PlotIQ example
shows each one filled.

| Section | Written by the CUSTOMIZE.md of | Read by |
|---|---|---|
| `## Fit Grid` | 01 Account Qualification | 01, 07 |
| `## Outbound Voice` | 02 Account Snapshot | 02 |
| `## Industry Context` | 03 Research Outbound | 03, 04, 05 |
| `## Trigger Catalog` | 04 Trigger Event Outbound | 04 |
| `## Closed-Loss Intelligence` | 05 Closed-Loss Reactivation | 05 |
| `## Meeting Prep` | 06 Meeting Prep | 06 |
| `## Daily Prospecting` | 07 Daily Prospecting | 07 |
| `## Deal Health` | 08 Deal Pulse | 08 |
| `## MEDDPICC` | 09 MEDDPICC Analysis | 09 |
| `## Buying Committee` | 10 Stakeholder Mapping | 10 |
| `## Competitive Patterns and Trends` | 11 Competitive Strategy | 11 |
| `## Displacement` | 12 Competitive Displacement | 12 |
| `## Call Coaching` | 13 Call Coaching | 13 |
| `## Implementation Profile` | 14 Sales Handoff | 14 |

**Operating skills** each add one optional section of their own. The skill's `CUSTOMIZE.md`
interview writes it, and the skill's Context section reads it. If the section is missing, the
skill runs with its defaults and says so.

| Section | Written by the CUSTOMIZE.md of | Holds |
|---|---|---|
| `## Verification` | O1 Verify | Your test, lint and build commands, and what counts as done |
| `## Debugging` | O2 Debug | Where bugs show up and how you reproduce them |
| `## Decision Discipline` | O3 Debate | Which decisions get a panel, and the expert archetypes that fit your work |
| `## Knowledge Locations` | O4 Context Gap | Where to search before building |
| `## Review Process` | O5 Second Opinion | Your builder vendor, your second vendor and how you reach it |
| `## Operational Health Metrics` | O6 Weekly Review | What the weekly record measures |
| `## Knowledge Base Structure` | O7 Graph Health | Your thresholds for tags, links and provisional items |
| `## Knowledge Base Consolidation` | O8 Dream | How stale items are handled |
| `## Knowledge Ingestion` | O9 Ingest | Your source types and where items land |
| `## Session Handoff` | O10 Wrap-up | Where continuation notes go |
| `## Knowledge Base` | O11 Context OS Setup | Where the base lives, so O6 to O9 can find it |
| `## Growth System` | O12 GTM Engine | Growth goal and window, team time for growth work, growth measure, current bottleneck, sprint cadence, narrative |
| `## Launch Plan` | O13 GTM Launch | Knowledge base path, decision owner, what is launching, motion, revenue goal and window, launch day owner and date, budget in dollars, day-30 review date, channel cap, kill and volume rules, reserve, war room, permission and cost records |
| `## Positioning` | O14 GTM Positioning | Knowledge base path, decision owner, value metric default, price list and setup rule, approval line, economics thresholds, re-grade windows, price test channel |
| `## Discovery` | O15 GTM Discovery | Knowledge base path, starting archetype guess, deal history source, stakeholder field, re-grade windows, interview channel |

O14 GTM Positioning writes its results straight into the standard Value Propositions and
Competitive Landscape sections, which is where the motion skills pick them up.

---

## Where Output Goes

Generated artifacts (call sheets, scorecards, sequences, review packets) go to `output/`,
which is gitignored. `profiles/client-profile.md` is gitignored too, because it holds your
competitive data. Neither ever leaves your machine unless you move it.

---

## The Example Everyone Uses

Every worked example in every skill uses the same fictional company, **PlotIQ**, a made-up
software company for cemeteries and funeral homes, and the same cast of prospect accounts
(Brackhaven Memorial Gardens is the flagship deal). Both are defined once, in
[`profiles/examples/plotiq-example.md`](../profiles/examples/plotiq-example.md). That
means you can follow one account from qualification to handoff across the skills, and compare
any skill's example output with what your own profile produces.
