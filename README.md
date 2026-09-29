# Vertical SaaS GTM Skills for Claude Code

**A GTM methodology framework for vertical SaaS teams: 14 sales skills, one context layer, and templates for making every piece your own. Runs in [Claude Code](https://claude.ai/code), [OpenAI Codex](https://openai.com/codex/), or as a [custom GPT in ChatGPT](docs/chatgpt-gpt-setup.md).**

Turn Claude into your team's sales methodology engine. These aren't prompt templates. They're codified playbooks that score deals, prep meetings, coach calls, build outbound sequences, and map stakeholders, all grounded in your company's actual ICP, personas, competitors, and proof points.

One client profile file. Fourteen skills that read it. Every GTM motion covered.

---

## What This Is

A complete AI-powered sales methodology suite designed for vertical SaaS companies. Each skill encodes proven frameworks (SPIN, MEDDPICC, Challenger) into structured Claude Code instructions that produce operational output, like call sheets, deal scorecards, battlecards, outbound sequences, and coaching reports.

**The key insight:** Your company's data lives in **one file**, [`profiles/client-profile.md`](profiles/client-profile-template.md). All 14 skills read from it. None of them contain it. Update the profile once and every skill inherits the change on its next run. When you move to a new vertical or client engagement, you swap that one file. The methodology stays the same. The profile is the fuel.

### The System, three steps, in order

This is a framework with templates, not a pile of prompts. It is built to be walked in order:

| Step | What you do | Where |
|---|---|---|
| **1. Build your context layer** | Fill out the client profile once: ICP, personas, pains, competitors, proof points | [`profiles/client-profile-template.md`](profiles/client-profile-template.md) |
| **2. Run the motion** | The 14 skills read that one file and produce operational artifacts | [`skills/`](skills/) |
| **3. Make it yours** | Hand-craft skills to your specific go-to-market motion, keeping the anatomy | [`docs/customization.md`](docs/customization.md) + per-skill `CUSTOMIZE.md` |

Skip step 1 and every skill degrades to generic output. Do step 1 well and steps 2 and 3 compound.

### Anatomy of a Skill

Every skill in this suite has the same five parts. Learn to read one and you can read them all:

| Part | What it does |
|---|---|
| **Role** | Who the AI is for this task. A senior operator, not a generic assistant |
| **Input Contract** | What it needs before it starts, and it asks rather than guesses |
| **Output Contract** | The shape of the artifact, same sections, same order, every run |
| **Methodology** | Your playbook, in code. SPIN, MEDDPICC, Challenger, scoring rubrics |
| **Context** | The pointer to `profiles/client-profile.md`. The skill reads your data and doesn't own it |

### Who This Is For

- **Revenue leaders** building AI-native sales teams
- **Sales ops / enablement** standardizing methodology across reps
- **GTM consultants** deploying repeatable systems across client engagements
- **Founders** who need enterprise-grade sales process without a 6-person ops team

### Where This Fits: the Free Tier

This repo is the free tier of a larger GTM operating system. It's the execution layer, the bottom of that stack, not a lite version of the top.

| Layer | What it decides | Where it lives |
|---|---|---|
| **Strategy** | Who the customer actually is, how you price and position against real alternatives, how a launch runs as a system, and how growth keeps running without a hero | Written up in the [Operator's Toolkit series](https://substack.com/@verticalgtmguild) on the Vertical GTM Guild. Not in this repo. |
| **Execution** (this repo) | The work a sales team runs every day: qualification, outbound, meeting prep, deal scoring, coaching, handoff | [`skills/`](skills/) and [`operating/`](operating/) |

The 14 skills read your client profile and never write it. They assume the strategy work is already done. If your profile comes out thin because nobody has run discovery or positioning yet, that's the layer to fix first, and every skill here gets sharper once you do.

---

## The 14 Skills

Skills are organized by deal stage, matching the natural flow of a B2B sales cycle.

### Prospect (Skills 1-5)
*Find, qualify, and engage the right accounts.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 1 | **[Account Pre-Qualification](skills/01-account-qualification/SKILL.md)** | Scores accounts against 8 weighted ICP criteria → GREENLIGHT / REVIEW / DISQUALIFY | New account lands on your desk |
| 2 | **[Account Snapshot](skills/02-account-snapshot/SKILL.md)** | Company brief + persona-matched email sequences + cold call sheet | BDR daily outbound building |
| 3 | **[Research-Driven Outbound](skills/03-research-outbound/SKILL.md)** | Deep research (10-K, earnings, private co intel) → 24 persona-tailored emails | Enterprise targets, high-value accounts |
| 4 | **[Trigger Event Outbound](skills/04-trigger-event-outbound/SKILL.md)** | Time-sensitive signal detection → urgency sequences (7-14 day window) | M&A, new exec, compliance failure, earnings miss |
| 5 | **[Closed-Loss Reactivation](skills/05-closed-loss-reactivation/SKILL.md)** | Loss-reason analysis → history-aware re-engagement sequences | Revisiting dead deals with new context |

### Discover (Skills 6-7)
*Prepare for and execute high-quality conversations.*

| # | Skill | What It Does | When to Use |
|---|-------|-------------|-------------|
| 6 | **[Meeting Prep](skills/06-meeting-prep/SKILL.md)** | SPIN (discovery) or Challenger (demo) call sheet in 90 seconds | Before any customer-facing call |
| 7 | **[Daily Prospecting](skills/07-daily-prospecting/SKILL.md)** | 4-tier prioritized dial sheet with personalized openers | Every morning before you pick up the phone |

### Execute (Skills 8-12)
*Score deals, qualify rigorously, and outmaneuver competitors.*

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

## The Operating Layer

The 14 skills above are the motion. [`operating/`](operating/) is the layer that keeps the
motion honest, the disciplines that decide whether work is real before it ships. First up:

| # | Skill | What It Does |
|---|-------|-------------|
| O1 | **[Verify](operating/O1-verify/SKILL.md)** | Four-tier evidence ladder (exists > substantive > wired > works) that blocks "done" claims until the top tier is demonstrated |
| O2 | **[Debug](operating/O2-debug/SKILL.md)** | Hypothesis-first discipline with a three-attempt circuit breaker. After three failed hypotheses, stop and hand off to re-plan |
| O3 | **[Debate](operating/O3-debate/SKILL.md)** | Convene 3-7 opposing expert personas to pressure-test a decision before committing. Ends with a decision matrix and plain-language read |
| O4 | **[Context Gap](operating/O4-context-gap/SKILL.md)** | Search before you build. Six-bucket classifier sorts what already exists, and about 40% of requests turn out to be done already |
| O5 | **[Second Opinion](operating/O5-second-opinion/SKILL.md)** | Send work to a model from a different vendor for review. Trades the builder's blind spots for a different set |
| O6 | **[Weekly Review](operating/O6-weekly-review/SKILL.md)** | Standing operational review that measures change week-over-week across knowledge base, content, and systems, writes dated records so health becomes a trend |
| O7 | **[Graph Health](operating/O7-graph-health/SKILL.md)** | Diagnoses knowledge base structure (tag sprawl, link density, provisional item age) and produces a health score, independent of whether items are true |
| O8 | **[Dream](operating/O8-dream/SKILL.md)** | Consolidation pass that finds stale, contradicted, or duplicated items and prunes with surgical precision (de-links dead references but never deletes surrounding words) |
| O9 | **[Ingest](operating/O9-ingest/SKILL.md)** | Transforms raw content (transcripts, documents, calls, notes) into structured knowledge items with compiled truth, append-only timeline, and wiki-links for discovery |
| O10 | **[Wrap-up](operating/O10-wrap-up/SKILL.md)** | Closes working sessions with state-level precision and a next action that passes four tests (imperative, named object, single step, resumable cold) |
| O11 | **[Context OS Setup](operating/O11-context-os-setup/SKILL.md)** | Build a structured knowledge base where facts are defined once and referenced everywhere. Two-layer architecture (atomic concepts + strategic documents) using semantic linking |
| O12 | **[GTM Engine](operating/O12-gtm-engine/SKILL.md)** | Post-launch growth systems through retrospectives, two-week sprints with ICE scoring, funnel optimization with PIE scoring, growth loops, strategic narrative, and email automation |
| O13 | **[GTM Launch](operating/O13-gtm-launch/SKILL.md)** | Launch planning and execution. GTM motion selection, channel strategy, funnel projection, launch assets, social proof collection, budget modeling, war room coordination |
| O14 | **[GTM Positioning](operating/O14-gtm-positioning/SKILL.md)** | Market positioning and pricing strategy. Competitive pricing analysis, value metric identification, willingness-to-pay research, April Dunford framework, messaging house, validation testing |
| O15 | **[GTM Discovery](operating/O15-gtm-discovery/SKILL.md)** | Market discovery and customer validation. Beachhead segmentation, problem mapping, competitive intelligence, assumption testing, evidence-based persona creation |

Each operating skill ships with a `CUSTOMIZE.md`, a paste-in interview that adapts it to your
motion, and a "Why This Skill Exists" section, because each one exists because something broke.
The rest of the suite is being published alongside the [Operator's Toolkit series](https://substack.com/@verticalgtmguild).

---

## Quick Start (15 Minutes)

### Pick your platform

| You use... | Setup path |
|---|---|
| **Claude Code** (CLI) | Steps below. The repo's `CLAUDE.md` auto-loads and walks you through setup conversationally. Clone it, open Claude Code, and say "help me get set up" |
| **OpenAI Codex** (CLI) | Same steps. The mirrored `AGENTS.md` gives Codex identical instructions |
| **ChatGPT** | No CLI needed: **[Build your GPT](docs/chatgpt-gpt-setup.md)**, skill + profile as knowledge files |
| **Claude.ai / ChatGPT Projects** | Same two-file pattern as the GPT guide, as a Project |

### Prerequisites (CLI path)
- [Claude Code](https://claude.ai/code) or [Codex](https://openai.com/codex/) installed and authenticated

### Step 1: Clone this repo
```bash
git clone https://github.com/rvanshur/vertical-gtm-skills.git
cd vertical-gtm-skills
```

### Step 2: Wire in your Client Profile
Fill out the **[Client Profile Template](profiles/client-profile-template.md)** for your company (a completed [legal-ops example](profiles/examples/legal-ops-example.md) shows the target density), then save it at the path every skill reads from:

```bash
cp your-completed-profile.md profiles/client-profile.md
```

That's the wiring. Every skill already includes the line that reads from this path, so there is no per-skill configuration.

### Step 3: Pick your three
**Do not start with all 14.** Pick the three that hit your role's biggest friction, run them on real accounts, then expand:

| Role | Your first three |
|------|-----------------|
| **BDR / SDR** | Account Snapshot (02) · Trigger Event Outbound (04) · Daily Prospecting (07) |
| **AE** | Meeting Prep (06) · Deal Pulse (08) · Stakeholder Mapping (10) |
| **Sales Manager / VP** | Account Pre-Qualification (01) · Deal Pulse (08) · Call Coaching (13) |
| **RevOps / Enablement** | Account Pre-Qualification (01) · MEDDPICC Analysis (09) · Sales-to-CS Handoff (14) |

Then point Claude Code at the suite. Run it from the cloned repo (this keeps every skill's pointer to `profiles/client-profile.md` intact), or reference skills in your `CLAUDE.md`:
```markdown
## Skills
When I ask for meeting prep, read and follow the instructions in:
`/path/to/vertical-gtm-skills/skills/06-meeting-prep/SKILL.md`
(Client profile lives at /path/to/vertical-gtm-skills/profiles/client-profile.md)
```

### Step 4: Run your first skill
Open Claude Code and try:
```
Prep me for a discovery call with [Company Name] tomorrow at 2pm.
They're a [industry] company, [size], and we're meeting with their [title].
```

Claude reads your Meeting Prep skill, pulls from your Client Profile, and generates a structured call sheet with SPIN questions, persona-matched proof points, and a meeting agenda. In about 90 seconds.

---

## How the System Works

### The Client Profile Pattern

Every skill reads from the same file, `profiles/client-profile.md`. The skills don't contain your data. They point to it. This is what makes the system portable, and what keeps 14 skills from drifting apart:

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
┌────────┐  ┌───────────┐  ┌──────────────┐
│ Skill 1│  │  Skill 6  │  │   Skill 13   │
│ Qualify │  │ Meet Prep │  │ Call Coach   │
└────────┘  └───────────┘  └──────────────┘
    │              │                  │
    ▼              ▼                  ▼
 Scorecard     Call Sheet      Coaching Report
```

**Same methodology. Same frameworks. Different vertical.** Swap the Client Profile, and every skill adapts.

### Skill Chaining

Skills compound when used together. A typical 30-day deployment:

| Day | Action | Skills Used |
|-----|--------|-------------|
| 1 | Qualify 200 accounts | Account Pre-Qualification |
| 3 | Build 20 outbound packages | Account Snapshot |
| 7 | Deep-dive 5 enterprise targets | Research-Driven Outbound |
| 14 | SPIN discovery prep (90 seconds) | Meeting Prep |
| 15 | Post-call coaching (22/30 score) | Call Coaching |
| 21 | 16-signal deal health check | Deal Pulse + Stakeholder Map |
| 30 | Competitive battlecard + win plan | Competitive Strategy |

---

## Documentation

| Guide | Description |
|-------|-------------|
| **[Getting Started](docs/getting-started.md)** | Role-based setup (BDR, AE, Manager), first-week playbook, common patterns |
| **[Client Profile Template](profiles/client-profile-template.md)** | Blank template with instructions for every field |
| **[Legal-Ops Example Profile](profiles/examples/legal-ops-example.md)** | A completed profile showing the target density and specificity |
| **[Skill Reference](docs/skill-reference.md)** | Decision tree, input/output specs, chaining patterns |
| **[Starter Kit](starter-kit/)** | Pre-built templates for identity files, taxonomy, and folder structure |
| **[Customization Guide](docs/customization.md)** | How to modify skills for your methodology, add new frameworks, extend scoring |
| **[Build Your GPT](docs/chatgpt-gpt-setup.md)** | Run any skill as a ChatGPT custom GPT, with knowledge files, loader instructions and limits stated plainly |

---

## About

Built by [Ryan Vanshur](https://ryanvanshur.com), Head of GTM Intelligence & AI Solutions. These skills were developed across a decade in vertical SaaS GTM (vocational edtech and construction fintech) and deployed against $100M+ in pipeline.

This repo is the companion to the **[AI-Powered GTM Stack](https://substack.com/@verticalgtmguild)** article series on the Vertical GTM Guild, which walks through the full system, including skills, knowledge architecture, operations, measurement, team transformation, and integrations.

### Vertical GTM Guild
- [Substack](https://substack.com/@verticalgtmguild)
- [Website](https://verticalgtmguild.com)

---

## License

MIT. Use these skills however you want. Build on them. Adapt them. Deploy them.

If they help your team close more deals, that's the whole point.
