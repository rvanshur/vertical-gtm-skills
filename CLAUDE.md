# Vertical SaaS GTM Skills: Assistant Instructions

> This file is mirrored as `CLAUDE.md` (read by Claude Code) and `AGENTS.md` (read by OpenAI
> Codex and other agents). Keep the two identical; edit both or neither.

You are operating inside a GTM operating system: 14 sales skills, 15 operating skills, and one
client profile they all read. Move the user through it in order:

```
Step 1: CONTEXT LAYER   profiles/client-profile.md, the user's company data, built once
Step 2: RUN THE MOTION  skills/01-14, GTM skills that all read the profile
Step 3: MAKE IT THEIRS  adapt skills to the user's specific go-to-market motion
Around all of it:       operating/O1-O15, the disciplines that check the work, keep the
                        knowledge base honest, and fill the profile with evidence
```

`docs/how-it-fits.md` explains how the layers connect. Read it when the user asks how the pieces
fit, or which operating skill to use.

## First: Check the Context Layer

At the start of a session, check whether `profiles/client-profile.md` exists.

- **Missing:** the user is at Step 1. Offer to build it with them before running any skill.
  Interview them section by section using `profiles/client-profile-template.md` (Company, ICP,
  Personas, Pain Points, Value Props, Product Modules, Competitive Landscape, Qualification
  Criteria, Proof Points, Methodology). Ask, don't lecture, a few questions at a time. Show them
  `profiles/examples/legal-ops-example.md` when they ask how specific to be. Write the completed
  file to `profiles/client-profile.md` (gitignored by design, because it holds their competitive
  data). If they want to see output first, they can copy the Lexora example into that path.
- **Present but thin** (sections empty or placeholder): say which sections are empty and what
  output quality that costs, then proceed if they want. If the ICP, Personas or Competitive
  Landscape can't be filled from evidence, suggest `operating/O15-gtm-discovery` and
  `operating/O14-gtm-positioning`. Never silently fill gaps with invented company data.
- **Present and real:** proceed to skills.

## Running a Skill

When the user asks for a task, read the matching `SKILL.md` in full and follow it exactly: its
Role, Input Contract (ask for missing inputs rather than guessing), Output Contract (same
sections, same order, every run), Methodology and Context.

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
| Check that work is actually done before claiming it | `operating/O1-verify/SKILL.md` |
| Fix something that isn't working | `operating/O2-debug/SKILL.md` |
| Pressure-test a decision or a plan | `operating/O3-debate/SKILL.md` |
| Check what already exists before building | `operating/O4-context-gap/SKILL.md` |
| Get a review from a different AI vendor | `operating/O5-second-opinion/SKILL.md` |
| Run the weekly operating review | `operating/O6-weekly-review/SKILL.md` |
| Check the knowledge base's structure | `operating/O7-graph-health/SKILL.md` |
| Clean up stale or duplicated knowledge | `operating/O8-dream/SKILL.md` |
| Turn a transcript, call or document into knowledge | `operating/O9-ingest/SKILL.md` |
| Close a working session with a handoff | `operating/O10-wrap-up/SKILL.md` |
| Set up a knowledge base | `operating/O11-context-os-setup/SKILL.md` |
| Build a repeatable post-launch growth system | `operating/O12-gtm-engine/SKILL.md` |
| Plan a launch | `operating/O13-gtm-launch/SKILL.md` |
| Position and price the product | `operating/O14-gtm-positioning/SKILL.md` |
| Find out who the customer really is | `operating/O15-gtm-discovery/SKILL.md` |

Skills reference `profiles/client-profile.md` in their Context section, so always load it before
producing output. Operating skills also read one optional profile section of their own (their
`CUSTOMIZE.md` writes it). If it is missing, run with the defaults and say so once.

O6 to O9 run on a knowledge base. If the user has none, suggest O11 first.

Write generated artifacts (call sheets, scorecards, sequences) to `output/` (gitignored) unless
the user asks otherwise.

## Helping the User Adapt a Skill (Step 3)

The suite is a framework with templates, not a fixed product. When the user wants a skill
adapted to their specific motion:

1. Have them run the stock skill on 2-3 real accounts first, so there is a baseline.
2. Use the skill's `CUSTOMIZE.md`. Every skill ships one. It is an interview script, so run it
   as a conversation, one question at a time.
3. For methodology swaps (SPIN to Sandler, scoring changes), follow `docs/customization.md`.
4. Preserve the five-part anatomy in anything you produce (Role, Input Contract, Output
   Contract, Methodology, Context) and keep company data OUT of the skill file and IN the
   profile. That separation is what makes their custom skill portable across verticals.
5. Save custom versions as new files (e.g. `skills/06-meeting-prep/SKILL-acme.md` or a fork),
   bump the frontmatter `version`, and note the change in the skill's Changelog section.

## Examples

Every worked example in the skills uses the same fictional company, Lexora, and the cast of
accounts at the bottom of `profiles/examples/legal-ops-example.md`. When you show the user an
example, draw on that cast rather than inventing a new company.

## Platform Notes

- **Claude Code / Codex:** this file loads automatically, and everything above applies as-is.
- **ChatGPT users:** point them to `docs/chatgpt-gpt-setup.md`. The same system runs as a custom
  GPT (skill + profile as knowledge files, loader block as instructions).
- Do not claim a skill "runs unmodified" on a platform you have not verified in this session.

## Boundaries

- Never commit or expose `profiles/client-profile.md`. It is gitignored because it holds the
  user's competitive data.
- Never invent ICP data, personas, competitor claims or proof points that are not in the
  profile. Ask instead.
- If a request falls outside every skill's scope, say so and offer the nearest skill rather
  than improvising a new methodology on the spot.
