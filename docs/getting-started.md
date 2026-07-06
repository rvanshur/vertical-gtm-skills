# Getting Started Guide

This guide gets you from zero to running skills in 15 minutes. It's organized by role because a BDR, an AE, and a sales manager need different skills on day one.

---

## Before You Start

### What You Need
1. **Claude Code CLI** installed and authenticated ([installation guide](https://claude.ai/code))
2. **This repo** cloned locally: `git clone https://github.com/rvanshur/vertical-gtm-skills.git`
3. **30 minutes** to fill out your Client Profile (you only do this once)

### How Skills Work in Claude Code

A "skill" is a markdown file (SKILL.md) that contains structured instructions Claude follows when you ask it to do something. Think of it as a playbook that Claude executes, not a prompt you paste.

Each skill in this repo has:
- **Client Profile** — your company data (ICP, personas, competitors, proof points)
- **Methodology** — the frameworks and scoring logic (SPIN, MEDDPICC, Challenger, etc.)
- **Workflow** — step-by-step process Claude follows
- **Output format** — exactly what gets generated (call sheets, scorecards, sequences, etc.)

When you tell Claude "prep me for a discovery call with Acme Corp," Claude reads the Meeting Prep skill, pulls your Client Profile data, and generates a structured output. Every time. Consistently.

---

## Step 1: Fill Out Your Client Profile

Open **[client-profile-template.md](../profiles/client-profile-template.md)** and complete every section, then save your completed copy as **`profiles/client-profile.md`** — the one path every skill reads from. This is the single most important step. The quality of every skill's output depends on the quality of your Client Profile. (A completed example: [legal-ops-example.md](../profiles/examples/legal-ops-example.md).)

### What to have ready:
- Your ICP definitions (who you sell to, who you don't)
- 3-6 buyer persona titles with their top priorities
- Your top 5-7 pain points with listening signals
- 3-5 value propositions
- Competitive landscape (3-5 competitors with your advantages)
- 2-5 proof points with named customers and metrics

### Tips:
- **Be specific.** "CFO" is a persona. "CFO at a $50M specialty contractor worried about cash flow visibility" is a useful persona.
- **Use real language.** Write pain points the way your prospects describe them, not how your marketing deck frames them.
- **Include metrics.** "Reduces processing time" is weak. "95% reduction in waiver processing time" gives Claude something to work with.
- **Start with what you have.** You don't need perfect data. Fill in what you know, run a few skills, and refine based on the output.

---

## Step 2: Choose Your Starting Skills

Don't install all 14 on day one. Start with the 3-4 that match your role and biggest time sinks.

### If You're a BDR

Your job is pipeline generation. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Account Pre-Qualification** (01) | Stop wasting time on bad-fit accounts. Score every new account in 60 seconds. |
| 2 | **Account Snapshot** (02) | Build complete outbound packages (brief + emails + call sheet) in 5-10 minutes instead of 45. |
| 3 | **Daily Prospecting** (07) | Start every morning with a prioritized dial sheet and personalized openers. |
| 4 | **Trigger Event Outbound** (04) | When you spot a signal (new exec, M&A, compliance failure), strike within the window. |

**First week:**
- Day 1: Install skills 01 and 02. Qualify 10 accounts. Build 3 outbound packages.
- Day 2: Install skill 07. Run your morning dial sheet. Compare to your old process.
- Day 3-5: Refine your Client Profile based on output quality. Add skill 04 when you spot a trigger event.

### If You're an AE

Your job is pipeline progression and closing. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Meeting Prep** (06) | Stop spending 30 minutes prepping for calls. Get a structured call sheet in 90 seconds. |
| 2 | **Deal Pulse** (08) | Know which deals are healthy and which are dying before your manager asks. |
| 3 | **MEDDPICC Analysis** (09) | Deep qualification that exposes gaps before they kill your deal at month 11. |
| 4 | **Stakeholder Mapping** (10) | Find the people you're not talking to but should be. |

**First week:**
- Day 1: Install skill 06. Prep for tomorrow's calls. Notice the difference in call quality.
- Day 2: Install skill 08. Score your top 5 deals. Find the one you thought was solid but isn't.
- Day 3-5: Run MEDDPICC on your commit deals. Install skill 10 on any deal with 3+ stakeholders.

### If You're a Sales Manager

Your job is coaching, forecasting, and process consistency. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Call Coaching** (13) | Grade calls against methodology (SPIN /30, Challenger /40) instead of vibes. |
| 2 | **Deal Pulse** (08) | Pipeline review in data, not stories. 16 signals across 4 pillars. |
| 3 | **MEDDPICC Analysis** (09) | Stop asking "how's the deal?" Start asking "show me the evidence." |
| 4 | **Sales-to-CS Handoff** (14) | Clean handoffs that don't blow up in month 2. |

**First week:**
- Day 1: Install skill 13. Coach 2 calls. Share the report with the rep.
- Day 2: Install skill 08. Score your team's top 10 deals. Stack-rank by health score.
- Day 3-5: Run MEDDPICC on every commit deal. Flag the ones with evidence gaps.

### If You're a GTM Consultant

You're deploying this across client engagements. Start with the full system:

1. Fill out a Client Profile for your client (use their language, not yours)
2. Install all 14 skills with that profile
3. Run the [30-day deployment sequence](../README.md#skill-chaining) from the README
4. When you move to a new client, swap `profiles/client-profile.md`. Everything else carries over.

---

## Step 3: Install Your Skills

### Option A: Direct reference (recommended for getting started)
Add this to your project's `CLAUDE.md` file:

```markdown
## GTM Skills
When I ask for sales-related tasks, read the relevant skill from:
/path/to/vertical-gtm-skills/skills/

Available skills:
- Meeting prep → 06-meeting-prep/SKILL.md
- Deal scoring → 08-deal-pulse/SKILL.md
- Call coaching → 13-call-coaching/SKILL.md
[add the skills you installed]
```

### Option B: Copy into your project
```bash
# Copy specific skills into your Claude Code project
cp skills/06-meeting-prep/SKILL.md ./claude-skills/meeting-prep.md
cp skills/08-deal-pulse/SKILL.md ./claude-skills/deal-pulse.md
```

### Option C: Use as Claude Code custom commands
Create command files that trigger specific skills:

```bash
mkdir -p .claude/commands
```

Create `.claude/commands/meeting-prep.md`:
```markdown
Read the skill at /path/to/vertical-gtm-skills/skills/06-meeting-prep/SKILL.md
and execute it for: $ARGUMENTS
```

Then in Claude Code, type: `/meeting-prep Discovery call with Acme Corp, meeting their VP of Engineering tomorrow`

---

## Step 4: Run Your First Skill

### Example: Meeting Prep

Open Claude Code in your project directory and type:

```
I have a discovery call tomorrow at 2pm with Sarah Chen, VP of Operations at Meridian Corp.
They're a $200M industrial equipment distributor, 12 locations across 4 states.
This is our first meeting. Prep me.
```

Claude will:
1. Read your Meeting Prep skill
2. Pull your Client Profile (ICP match, relevant personas, pain hypotheses)
3. Generate a single-page prep sheet with:
   - SPIN question bank (Situation → Problem → Implication → Need-Payoff)
   - Persona-matched proof points
   - Competitive positioning notes
   - Meeting open/close scripts
   - Risk flags and things to listen for

**Expected output time:** ~90 seconds.

### Example: Deal Pulse

```
Score the Meridian Corp deal. Here's what I know:
- Met with VP Ops and Director of IT (2 of ~5 stakeholders)
- They confirmed manual processes are costing 40+ hours/month
- No budget discussion yet
- Mentioned they looked at [Competitor] last year but didn't move forward
- Next step: demo with their team next week
```

Claude will score all 16 signals across 4 pillars (Why Anything, Why Us, Why Now, Execution), compute a health score (0-100), identify top risks, and recommend next actions.

---

## Common Questions

### "How is this different from a prompt library?"
A prompt library gives you a starting point. You paste it, tweak it, and hope for good output. A skill is a complete methodology. It has scoring logic, evidence rules, output formats, and integration points. Claude doesn't just answer your question. It runs a process.

### "Do I need all 14 skills?"
No. Start with 3-4 based on your role (see Step 2). Add more as you get comfortable. Most teams reach full deployment in 30 days.

### "How do I know the output is good?"
Every skill has built-in quality gates. Deal Pulse scores on evidence, not assumptions. Call Coaching grades against methodology criteria. MEDDPICC flags gaps. The skills are designed to surface what's missing, not just confirm what you already believe.

### "Can I modify the skills?"
Yes. They're MIT licensed. Common modifications:
- Add custom scoring criteria
- Change framework weights
- Add industry-specific qualification dimensions
- Integrate with your CRM data via copy/paste context

See the [Customization Guide](customization.md) for details.

### "What if I use a different methodology than SPIN/MEDDPICC?"
The frameworks are modular. You can swap SPIN for Sandler, Challenger for demo methodology of your choice, or add Gap Selling alongside MEDDPICC. See the [Customization Guide](customization.md).

---

## What's Next

Once you've run a few skills and refined your Client Profile:

1. **Read the [Skill Reference](skill-reference.md)** for the decision tree (which skill for which situation) and chaining patterns
2. **Try skill chaining** — run Account Qualification → Account Snapshot → Meeting Prep on the same account
3. **Read the [AI-Powered GTM Stack series](https://substack.com/@verticalgtmguild)** for the full system architecture (knowledge layer, operations, measurement, team transformation)
4. **Join the [Vertical GTM Guild](https://verticalgtmguild.com)** to connect with other operators building AI-native GTM orgs
