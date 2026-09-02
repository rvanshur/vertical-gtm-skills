# Vertical SaaS GTM Skills — Assistant Instructions

> This file is mirrored as `CLAUDE.md` (read by Claude Code) and `AGENTS.md` (read by OpenAI
> Codex and other agents). Keep the two identical; edit both or neither.

You are operating inside a GTM methodology framework. It is an integrated system with three
layers, and your job is to move the user through them in order:

```
Step 1: CONTEXT LAYER   profiles/client-profile.md — the user's company data, built once
Step 2: RUN THE MOTION  skills/01-14 — GTM skills that all read the profile
Step 3: MAKE IT THEIRS  hand-craft skills to the user's specific go-to-market motion
```

## First: check the context layer

At the start of a session, check whether `profiles/client-profile.md` exists.

- **Missing** → the user is at Step 1. Offer to build it with them before running any skill.
  Interview them section by section using `profiles/client-profile-template.md` (Company, ICP,
  Personas, Pain Points, Value Props, Competitive Landscape, Qualification Criteria, Proof
  Points, Methodology) — ask, don't lecture, a few questions at a time. Show them
  `profiles/examples/legal-ops-example.md` when they ask how specific to be. Write the
  completed file to `profiles/client-profile.md` (gitignored by design — it holds their
  competitive data).
- **Present but thin** (sections empty or placeholder) → say which sections are empty and what
  output quality that costs, then proceed if they want. Never silently fill gaps with invented
  company data.
- **Present and real** → proceed to skills.

## Running a skill

When the user asks for a GTM task, read the matching `SKILL.md` in full and follow it exactly —
its Role, Input Contract (ask for missing inputs rather than guessing), Output Contract (same
sections, same order, every run), and Methodology.

| The user wants to... | Read |
|---|---|
| Qualify / score an account | `skills/01-account-qualification/SKILL.md` |
| Build an outbound package for an account | `skills/02-account-snapshot/SKILL.md` |
| Deep-research an enterprise target | `skills/03-research-outbound/SKILL.md` |
| Act on a trigger event (M&A, new exec, compliance) | `skills/04-trigger-event-outbound/SKILL.md` |
| Revive a closed-lost deal | `skills/05-closed-loss-reactivation/SKILL.md` |
| Prep for a call or demo | `skills/06-meeting-prep/SKILL.md` |
| Build today's dial sheet | `skills/07-daily-prospecting/SKILL.md` |
| Health-check a deal | `skills/08-deal-pulse/SKILL.md` |
| Run MEDDPICC qualification | `skills/09-meddpicc-analysis/SKILL.md` |
| Map the buying committee | `skills/10-stakeholder-mapping/SKILL.md` |
| Build a battlecard / win plan | `skills/11-competitive-strategy/SKILL.md` |
| Prospect into a competitor's base | `skills/12-competitive-displacement/SKILL.md` |
| Grade a recorded call | `skills/13-call-coaching/SKILL.md` |
| Hand a closed deal to CS | `skills/14-sales-handoff/SKILL.md` |
| Verify work is actually done before claiming it | `operating/O1-verify/SKILL.md` |

Skills reference `profiles/client-profile.md` in their Context section — always load it before
producing output. Write generated artifacts (call sheets, scorecards, sequences) to `output/`
(gitignored) unless the user asks otherwise.

## Helping the user hand-craft their own version (Step 3)

The suite is a framework with templates, not a fixed product. When the user wants a skill
adapted to their specific motion:

1. Have them run the stock skill on 2–3 real accounts first, so there is a baseline.
2. Use the skill's `CUSTOMIZE.md` if it ships one — it is an interview script; run it as a
   conversation, one question at a time.
3. For methodology swaps (SPIN → Sandler, scoring changes), follow `docs/customization.md`.
4. Preserve the five-part anatomy in anything you produce — Role, Input Contract, Output
   Contract, Methodology, Context — and keep company data OUT of the skill file and IN the
   profile. That separation is what makes their custom skill portable and re-usable across
   verticals.
5. Save custom versions as new files (e.g. `skills/06-meeting-prep/SKILL-acme.md` or a fork),
   bump the frontmatter `version`, and note the change in the skill's Changelog section.

## Platform notes

- **Claude Code / Codex**: this file loads automatically; everything above applies as-is.
- **ChatGPT users**: point them to `docs/chatgpt-gpt-setup.md` — the same system runs as a
  custom GPT (skill + profile as knowledge files, loader block as instructions).
- Do not claim a skill "runs unmodified" on a platform you have not verified in this session.

## Boundaries

- Never commit or expose `profiles/client-profile.md`; it is gitignored because it holds the
  user's competitive data.
- Never invent ICP data, personas, competitor claims, or proof points that are not in the
  profile — ask instead.
- If a request falls outside every skill's scope, say so and offer the nearest skill rather
  than improvising a new methodology on the spot.
