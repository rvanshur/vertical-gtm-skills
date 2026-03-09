# Vertical GTM Skills for Claude Code

**14 production-ready sales methodology skills for vertical SaaS GTM teams, built for [Claude Code](https://claude.ai/code).**

Turn Claude into your team's sales methodology engine. These aren't prompt templates. They're codified playbooks that score deals, prep meetings, coach calls, build outbound sequences, and map stakeholders, all grounded in your company's actual ICP, personas, competitors, and proof points.

One configuration block. Fourteen skills. Every GTM motion covered.

---

## What This Is

A complete AI-powered sales methodology suite designed for vertical SaaS companies. Each skill encodes proven frameworks (SPIN, MEDDPICC, Challenger) into structured Claude Code instructions that produce operational output: call sheets, deal scorecards, battlecards, outbound sequences, and coaching reports.

**The key insight:** You configure one Client Profile with your company's data. All 14 skills read from it. When you move to a new vertical or client engagement, you swap the profile. The methodology stays the same.

### Who This Is For

- **Revenue leaders** building AI-native sales teams
- **Sales ops / enablement** standardizing methodology across reps
- **GTM consultants** deploying repeatable systems across client engagements
- **Founders** who need enterprise-grade sales process without a 6-person ops team

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

## Quick Start (15 Minutes)

### Prerequisites
- [Claude Code CLI](https://claude.ai/code) installed and authenticated
- A Claude Pro, Team, or Enterprise subscription

### Step 1: Clone this repo
```bash
git clone https://github.com/rvanshur/vertical-gtm-skills.git
cd vertical-gtm-skills
```

### Step 2: Configure your Client Profile
Every skill has a `## Client Profile` section at the top. This is where you plug in your company's data.

Open the **[Client Profile Template](client-profile-template.md)** and fill it out for your company. Then copy that profile into each skill you plan to use.

> **Pro tip:** Start with 3 skills, not 14. See the [Getting Started Guide](docs/getting-started.md) for role-based recommendations.

### Step 3: Install skills in Claude Code
Copy any skill's `SKILL.md` into your Claude Code project directory:

```bash
# Example: install the Meeting Prep skill
mkdir -p ~/.claude/skills
cp skills/06-meeting-prep/SKILL.md ~/.claude/skills/meeting-prep.md
```

Or reference skills directly in your `CLAUDE.md`:
```markdown
## Skills
When I ask for meeting prep, read and follow the instructions in:
`/path/to/vertical-gtm-skills/skills/06-meeting-prep/SKILL.md`
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

Every skill reads from the same Client Profile block. This is what makes the system portable:

```
┌─────────────────────────────────────────┐
│           CLIENT PROFILE                │
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
| **[Client Profile Template](client-profile-template.md)** | Blank template with instructions for every field |
| **[Skill Reference](docs/skill-reference.md)** | Decision tree, input/output specs, chaining patterns |
| **[Starter Kit](starter-kit/)** | Pre-built templates for identity files, taxonomy, and folder structure |
| **[Customization Guide](docs/customization.md)** | How to modify skills for your methodology, add new frameworks, extend scoring |

---

## About

Built by [Ryan Vanshur](https://ryanvanshur.com), Head of GTM Intelligence & AI Solutions. These skills were developed across a decade in vertical SaaS GTM (vocational edtech and construction fintech) and deployed against $100M+ in pipeline.

This repo is the companion to the **[AI-Powered GTM Stack](https://substack.com/@verticalgtmguild)** article series on the Vertical GTM Guild, which walks through the full system: skills, knowledge architecture, operations, measurement, team transformation, and integrations.

### Vertical GTM Guild
- [Substack](https://substack.com/@verticalgtmguild)
- [Website](https://verticalgtmguild.com)

---

## License

MIT. Use these skills however you want. Build on them. Adapt them. Deploy them.

If they help your team close more deals, that's the whole point.
