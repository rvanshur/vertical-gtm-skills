# Vertical SaaS GTM Skills for Claude Code

**A GTM operating system for vertical SaaS teams: 14 sales skills, 15 operating skills, one client profile they all read, and a step-by-step guide for making every piece your own. Built for [Claude Code](https://claude.ai/code). The same files are documented for [OpenAI Codex](https://openai.com/codex/) and a [custom GPT in ChatGPT](docs/chatgpt-gpt-setup.md).**

Turn Claude into your team's sales methodology engine. These aren't prompt templates. They're codified playbooks that score deals, prep meetings, coach calls, build outbound sequences and map stakeholders, all grounded in your company's actual ICP, personas, competitors and proof points. Around them sits an operating layer: the disciplines that check the work before it ships, keep a knowledge base honest, and turn strategy into the profile the sales skills run on.

One client profile file. Twenty-nine skills. One worked example company, used everywhere, so you can see exactly what good output looks like.

---

## What This Is

A complete AI-powered GTM suite designed for vertical SaaS companies. Each sales skill encodes proven frameworks (SPIN, MEDDPICC, Challenger) into structured instructions that produce operational output, like call sheets, deal scorecards, battlecards, outbound sequences and coaching reports.

**The key insight:** Your company's data lives in **one file**, [`profiles/client-profile.md`](profiles/client-profile-template.md). Every skill reads from it. None of them contain it. Update the profile once and every skill inherits the change on its next run. When you move to a new vertical or client engagement, you swap that one file. The methodology stays the same. The profile is the fuel.

### The System, Three Steps, in Order

This is a framework with templates, not a pile of prompts. It is built to be walked in order:

| Step | What you do | Where |
|---|---|---|
| **1. Build your context layer** | Fill out the client profile once: ICP, personas, pains, competitors, proof points | [`profiles/client-profile-template.md`](profiles/client-profile-template.md) |
| **2. Run the motion** | The 14 sales skills read that one file and produce operational artifacts | [`skills/`](skills/) |
| **3. Make it yours** | Adapt skills to your specific go-to-market motion, keeping the anatomy | [`docs/customization.md`](docs/customization.md) + each skill's `CUSTOMIZE.md` |

Skip step 1 and every skill degrades to generic output. Do step 1 well and steps 2 and 3 compound.

**How the pieces connect**, including what to set up first and which operating skill to reach for, is drawn out in **[docs/how-it-fits.md](docs/how-it-fits.md)**.

### Anatomy of a Skill

Every sales skill has the same five parts. Learn to read one and you can read them all:

| Part | What it does |
|---|---|
| **Role** | Who the AI is for this task. A senior operator, not a generic assistant |
| **Input Contract** | What it needs before it starts, and it asks rather than guesses |
| **Output Contract** | The shape of the artifact, same sections, same order, every run |
| **Methodology** | Your playbook, in code. SPIN, MEDDPICC, Challenger, scoring rubrics |
| **Context** | The pointer to `profiles/client-profile.md`. The skill reads your data and doesn't own it |

The operating skills follow the same pattern and add one section, **Why This Skill Exists**, because each one exists because something broke.

### The Example Everyone Uses

Every worked example in this repo uses one fictional company: **Lexora**, a legal-ops platform that sells to in-house legal teams, and its flagship prospect, **Corvane Industrial**. The complete profile and the cast of accounts are in [`profiles/examples/legal-ops-example.md`](profiles/examples/legal-ops-example.md). Follow Corvane from qualification (01) through handoff (14), then run the same skills on your own profile and compare.

### Who This Is For

- **Revenue leaders** building AI-native sales teams
- **Sales ops / enablement** standardizing methodology across reps
- **GTM consultants** deploying repeatable systems across client engagements
- **Founders** who need enterprise-grade sales process without a 6-person ops team

### Where This Fits

This repo is the free tier of a larger GTM operating system. It is the working bottom of that stack, not a lite version of the top.

| Layer | What it decides | Where it lives |
|---|---|---|
| **Strategy** | Who the customer actually is, how you price and position against real alternatives, how a launch runs as a system, how growth keeps running without a hero | The four strategy skills in [`operating/`](operating/) (O12 to O15), and the thinking behind them in the [Operator's Toolkit series](https://substack.com/@verticalgtmguild) |
| **Context** | The facts every other skill runs on | [`profiles/client-profile.md`](profiles/client-profile-template.md) |
| **Execution** | The work a sales team runs every day: qualification, outbound, meeting prep, deal scoring, coaching, handoff | The 14 skills in [`skills/`](skills/) |
| **Discipline** | Whether the work is real before it ships, and whether the team's knowledge stays true | The verification, memory and session skills in [`operating/`](operating/) |

The 14 sales skills read your client profile and never write it. They assume the strategy work is done. If your profile comes out thin because nobody has run discovery or positioning yet, run O15 and O14 first, and every sales skill gets sharper once you do.

---

## The 14 Sales Skills

Skills are organized by deal stage, matching the natural flow of a B2B sales cycle.

### Prospect (Skills 1-5)
*Find, qualify and engage the right accounts.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 1 | **[Account Pre-Qualification](skills/01-account-qualification/SKILL.md)** | Scores accounts against 8 weighted ICP criteria → GREENLIGHT / MANUAL REVIEW / DISQUALIFY | New account lands on your desk |
| 2 | **[Account Snapshot](skills/02-account-snapshot/SKILL.md)** | Company brief + persona-matched email sequences + cold call sheet | BDR daily outbound building |
| 3 | **[Research-Driven Outbound](skills/03-research-outbound/SKILL.md)** | Deep research (10-K, earnings, private company intel) → 24 persona-tailored emails | Enterprise targets, high-value accounts |
| 4 | **[Trigger Event Outbound](skills/04-trigger-event-outbound/SKILL.md)** | Time-sensitive signal detection → urgency sequences (7-14 day window) | M&A, new exec, compliance failure, earnings miss |
| 5 | **[Closed-Loss Reactivation](skills/05-closed-loss-reactivation/SKILL.md)** | Loss-reason analysis → history-aware re-engagement sequences | Revisiting dead deals with new context |

### Discover (Skills 6-7)
*Prepare for and execute high-quality conversations.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 6 | **[Meeting Prep](skills/06-meeting-prep/SKILL.md)** | SPIN (discovery) or Challenger (demo) call sheet in about 90 seconds | Before any customer-facing call |
| 7 | **[Daily Prospecting](skills/07-daily-prospecting/SKILL.md)** | 4-tier prioritized dial sheet with personalized openers | Every morning before you pick up the phone |

### Execute (Skills 8-12)
*Score deals, qualify rigorously and outmaneuver competitors.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 8 | **[Deal Pulse](skills/08-deal-pulse/SKILL.md)** | 16-signal health score (0-100) across 4 pillars | Pipeline review, deal health check |
| 9 | **[MEDDPICC Analysis](skills/09-meddpicc-analysis/SKILL.md)** | 8-element deep qualification with evidence grading | Deal strategy session, forecast commit |
| 10 | **[Stakeholder Mapping](skills/10-stakeholder-mapping/SKILL.md)** | 7-role buying committee map + ghost node detection | Mid-deal: who are we missing? |
| 11 | **[Competitive Strategy](skills/11-competitive-strategy/SKILL.md)** | Deal-specific battlecard + positioning matrix + win plan | Active deal against a known competitor |
| 12 | **[Competitive Displacement](skills/12-competitive-displacement/SKILL.md)** | 4-step outbound targeting incumbent failure patterns | Prospecting into competitor accounts |

### Close (Skill 13)
*Coach reps and improve execution quality.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 13 | **[Call Coaching](skills/13-call-coaching/SKILL.md)** | Post-call methodology grading (SPIN /30, Challenger /40) | After any recorded call |

### Handoff (Skill 14)
*Ensure clean transitions from sales to customer success.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 14 | **[Sales-to-CS Handoff](skills/14-sales-handoff/SKILL.md)** | 6-dimension readiness score + implementation plan | Deal closing, pre-implementation |

---

## The 15 Operating Skills

The 14 sales skills are the motion. [`operating/`](operating/) is the layer that keeps the motion honest: the disciplines that decide whether work is real before it ships, the memory that keeps what the team learns, and the strategy work that fills the profile with evidence. They are numbered as a countdown, so O1 is the one that matters most.

**Verification**

| # | Skill | What It Does |
|---|-------|-------------|
| O1 | **[Verify](operating/O1-verify/SKILL.md)** | Four-tier evidence ladder (exists > substantive > wired > functional) that blocks "done" claims until the top tier is demonstrated |
| O2 | **[Debug](operating/O2-debug/SKILL.md)** | Hypothesis-first discipline with a three-attempt circuit breaker. After three failed hypotheses, stop and hand off to re-plan |
| O3 | **[Debate](operating/O3-debate/SKILL.md)** | Convenes 3-7 opposing expert personas to pressure-test a decision before committing. Ends with a decision matrix and a plain-language read |
| O4 | **[Context Gap](operating/O4-context-gap/SKILL.md)** | Search before you build. A six-bucket classifier sorts what already exists, and about 40% of requests turn out to be done already (the author's working estimate) |
| O5 | **[Second Opinion](operating/O5-second-opinion/SKILL.md)** | Packages work for a model from a different vendor, then triages what comes back. Trades the builder's blind spots for a different set |

**Memory and knowledge**

| # | Skill | What It Does |
|---|-------|-------------|
| O6 | **[Weekly Review](operating/O6-weekly-review/SKILL.md)** | Standing operational review that measures change week over week and writes dated records, so health becomes a trend |
| O7 | **[Graph Health](operating/O7-graph-health/SKILL.md)** | Diagnoses knowledge base structure (tag sprawl, link density, provisional item age) and produces a health score, independent of whether items are true |
| O8 | **[Dream](operating/O8-dream/SKILL.md)** | Consolidation pass that finds stale, contradicted or duplicated items and prunes with surgical precision (de-links dead references but never deletes surrounding words) |
| O9 | **[Ingest](operating/O9-ingest/SKILL.md)** | Transforms raw content (transcripts, documents, calls, notes) into structured knowledge items with compiled truth, an append-only timeline and wiki-links |
| O10 | **[Wrap-up](operating/O10-wrap-up/SKILL.md)** | Closes working sessions with state-level precision and a next action that passes four tests (imperative, named object, single step, resumable cold) |
| O11 | **[Context OS Setup](operating/O11-context-os-setup/SKILL.md)** | Builds the knowledge base O6 to O9 run on, where facts are defined once and referenced everywhere. Run it before those four |

**GTM strategy**

| # | Skill | What It Does |
|---|-------|-------------|
| O12 | **[GTM Engine](operating/O12-gtm-engine/SKILL.md)** | Post-launch growth systems: retrospectives, two-week sprints with ICE scoring, funnel optimization with PIE scoring, growth loops, strategic narrative |
| O13 | **[GTM Launch](operating/O13-gtm-launch/SKILL.md)** | Launch planning and execution: motion selection, channel strategy, funnel projection, launch assets, budget, war room |
| O14 | **[GTM Positioning](operating/O14-gtm-positioning/SKILL.md)** | Positioning and pricing: competitive pricing, value metric, willingness-to-pay research, April Dunford's framework, messaging house |
| O15 | **[GTM Discovery](operating/O15-gtm-discovery/SKILL.md)** | Market discovery and customer validation: beachhead segmentation, problem mapping, assumption testing, evidence-based personas |

O12 to O15 are adapted from Maja Voje's [GTM Strategist skills](https://github.com/GTM-Strategist/gtm-strategist-skills) under the MIT License. Credit is in each skill.

Every one of the 29 skills ships with a `CUSTOMIZE.md`, a paste-in interview that adapts it to your motion. Each operating skill's interview writes one small section into your profile, and the skill reads it on its next run. The full map is in [docs/how-it-fits.md](docs/how-it-fits.md).

---

## Quick Start (15 Minutes)

### Pick Your Platform

| You use... | Setup path | Status |
|---|---|---|
| **Claude Code** (CLI) | Steps below. The repo's `CLAUDE.md` auto-loads and walks you through setup conversationally. Clone it, open Claude Code in the folder, and say "help me get set up" | The primary path, and the one this repo is built and run on |
| **OpenAI Codex** (CLI) | Same steps. The mirrored `AGENTS.md` gives Codex identical instructions | Documented from Codex's published interface, not yet walked through end to end |
| **ChatGPT** | No CLI needed: **[Build your GPT](docs/chatgpt-gpt-setup.md)**, skill + profile as knowledge files | Documented, not yet walked through end to end |
| **Claude.ai / ChatGPT Projects** | Same two-file pattern as the GPT guide, as a Project | Documented, not yet walked through end to end |

### Prerequisites (CLI Path)
- [Claude Code](https://claude.ai/code) installed and authenticated

### Step 1: Clone This Repo
```bash
git clone https://github.com/rvanshur/vertical-gtm-skills.git
cd vertical-gtm-skills
```

### Step 2: Wire in Your Client Profile
Fill out the **[Client Profile Template](profiles/client-profile-template.md)** for your company (the completed [Lexora example](profiles/examples/legal-ops-example.md) shows the target density), then save it at the path every skill reads from:

```bash
cp your-completed-profile.md profiles/client-profile.md
```

That's the wiring. Every skill already includes the line that reads from this path, so there is no per-skill configuration. Want to see output before writing your own? Copy the Lexora example into place and run a skill against it:

```bash
cp profiles/examples/legal-ops-example.md profiles/client-profile.md
```

### Step 3: Pick Your Three
**Do not start with all 14.** Pick the three that hit your role's biggest friction, run them on real accounts, then expand:

| Role | Your first three |
|------|-----------------|
| **BDR / SDR** | Account Snapshot (02) · Trigger Event Outbound (04) · Daily Prospecting (07) |
| **AE** | Meeting Prep (06) · Deal Pulse (08) · Stakeholder Mapping (10) |
| **Sales Manager / VP** | Account Pre-Qualification (01) · Deal Pulse (08) · Call Coaching (13) |
| **RevOps / Enablement** | Account Pre-Qualification (01) · MEDDPICC Analysis (09) · Sales-to-CS Handoff (14) |

### Step 4: Run Your First Skill
Open Claude Code in the cloned folder and try:
```
Prep me for a discovery call with [Company Name] tomorrow at 2pm.
They're a [industry] company, [size], and we're meeting with their [title].
```

Claude reads the Meeting Prep skill, pulls from your Client Profile, and generates a structured call sheet with SPIN questions, persona-matched proof points and a meeting agenda. With the Lexora example in place, try it on Corvane Industrial and compare with the skill's own worked example.

More ways to run the skills (from your own project, as slash commands) are in [docs/getting-started.md](docs/getting-started.md#step-3-run-the-skills-from-where-you-work).

---

## How the System Works

### The Client Profile Pattern

Every skill reads from the same file, `profiles/client-profile.md`. The skills don't contain your data. They point to it. This is what makes the system portable, and what keeps 29 skills from drifting apart:

```
┌─────────────────────────────────────────┐
│      profiles/client-profile.md         │
│  Company, ICP, Personas, Competitors,   │
│  Pain Points, Value Props, Proof Points │
└──────────────────┬──────────────────────┘
                   │
    ┌──────────────┼──────────────────┐
    │              │                  │
    ▼              ▼                  ▼
┌─────────┐  ┌───────────┐  ┌──────────────┐
│ Skill 1 │  │  Skill 6  │  │   Skill 13   │
│ Qualify │  │ Meet Prep │  │ Call Coach   │
└─────────┘  └───────────┘  └──────────────┘
    │              │                  │
    ▼              ▼                  ▼
 Scorecard     Call Sheet      Coaching Report
```

**Same methodology. Same frameworks. Different vertical.** Swap the Client Profile, and every skill adapts.

### Skill Chaining

Skills compound when used together. A typical first 30 days, following one account set:

| Day | Action | Skills Used |
|-----|--------|-------------|
| 1 | Qualify your target list | Account Pre-Qualification |
| 3 | Build outbound packages for the GREENLIGHT accounts | Account Snapshot |
| 7 | Deep-dive your top enterprise targets | Research-Driven Outbound |
| 14 | SPIN discovery prep | Meeting Prep |
| 15 | Post-call coaching | Call Coaching |
| 21 | Deal health check and buying committee map | Deal Pulse + Stakeholder Mapping |
| 30 | Competitive battlecard + win plan | Competitive Strategy |

---

## Documentation

| Guide | Description |
|-------|-------------|
| **[How It Fits Together](docs/how-it-fits.md)** | The three layers, what to set up first, which operating skill to use when, and what each skill reads from the profile |
| **[Getting Started](docs/getting-started.md)** | Role-based setup (BDR, AE, Manager, consultant), first-week playbook, ways to run the skills |
| **[Client Profile Template](profiles/client-profile-template.md)** | Blank template with instructions for every section |
| **[Lexora Example Profile](profiles/examples/legal-ops-example.md)** | A completed profile, plus the cast of accounts every worked example uses |
| **[Customization Guide](docs/customization.md)** | Which profile sections to fill first, how to swap methodologies, adjust scoring and add criteria |
| **[Skill Reference](docs/skill-reference.md)** | Decision tree, input/output specs, chaining patterns, scoring systems |
| **[Starter Kit](starter-kit/)** | Folder layouts, a project `CLAUDE.md` template and a weekly operating checklist |
| **[Build Your GPT](docs/chatgpt-gpt-setup.md)** | Running any skill as a ChatGPT custom GPT, with knowledge files, loader instructions and limits stated plainly |
| **[Changelog](CHANGELOG.md)** | What changed, and when |

---

## About

Built by [Ryan Vanshur](https://ryanvanshur.com), Head of GTM Intelligence & AI Solutions. These skills were developed across a decade in vertical SaaS GTM (vocational edtech and construction fintech) and run in production on nine figures of pipeline.

This repo is the companion to the **[AI-Powered GTM Stack](https://substack.com/@verticalgtmguild)** and **Operator's Toolkit** series on the Vertical GTM Guild, which walk through the full system: skills, knowledge architecture, operations, measurement, team transformation and integrations. Each operating skill also has a page with a tutorial and a worked example at [verticalgtmguild.com/skills](https://verticalgtmguild.com/skills).

### Vertical GTM Guild
- [Substack](https://substack.com/@verticalgtmguild)
- [Website](https://verticalgtmguild.com)

---

## License

MIT. Use these skills however you want. Build on them. Adapt them. Deploy them.

If they help your team close more deals, that's the whole point.
