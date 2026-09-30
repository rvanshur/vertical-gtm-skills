# Getting Started Guide

This guide gets you from zero to running skills in about 15 minutes. It's organized by role because a BDR, an AE and a sales manager need different skills on day one.

For how the sales skills, the operating skills and the profile connect, read [How It Fits Together](how-it-fits.md) alongside this.

---

## Before You Start

### What You Need
1. **Claude Code** installed and authenticated ([installation guide](https://claude.ai/code))
2. **This repo** cloned locally: `git clone https://github.com/rvanshur/vertical-gtm-skills.git`
3. **30 minutes** to fill out your Client Profile (you only do this once)

### How Skills Work in Claude Code

A "skill" is a markdown file (`SKILL.md`) with structured instructions Claude follows when you ask it to do something. Think of it as a playbook Claude executes, not a prompt you paste.

Each sales skill has five parts:
- **Role:** who the AI is for this task
- **Input Contract:** what it needs from you, and it asks rather than guesses
- **Output Contract:** exactly what gets produced (call sheets, scorecards, sequences), same sections every run
- **Methodology:** the frameworks and scoring logic (SPIN, MEDDPICC, Challenger and so on)
- **Context:** the pointer to your Client Profile, where your company data lives

When you tell Claude "prep me for a discovery call with Corvane Industrial," Claude reads the Meeting Prep skill, pulls your Client Profile, and produces the same structured call sheet every time.

---

## Step 1: Fill Out Your Client Profile

Open **[client-profile-template.md](../profiles/client-profile-template.md)** and complete every section, then save your copy as **`profiles/client-profile.md`**, the one path every skill reads from. This is the most important step. The quality of every skill's output depends on the quality of this file. The completed [Lexora example](../profiles/examples/legal-ops-example.md) shows the density to aim for.

### What to Have Ready
- Your ICP definitions (who you sell to, who you don't)
- 3-5 buyer persona titles with their top priorities
- Your top 3-5 pain points, in your buyers' words
- 3-5 value propositions, each with a number attached
- Your competitive landscape (3-5 competitors, including "do nothing")
- 2-5 proof points with named customers and metrics

If you only have time for two sections, do **ICP Definitions** and **Competitive Landscape** first. Between them they feed 13 of the 14 sales skills. The full map is in the [Customization Guide](customization.md#which-profile-sections-feed-which-skills).

### Tips
- **Be specific.** "General Counsel" is a persona. "General Counsel at a $3B manufacturer who can't defend outside-counsel spend to the CFO" is a useful persona.
- **Use real language.** Write pain points the way your prospects describe them, not how your marketing deck frames them.
- **Include metrics.** "Reduces legal spend" is weak. "Cuts outside-counsel spend 20% in year one" gives Claude something to work with.
- **Start with what you have.** You don't need perfect data. Fill in what you know, run a few skills, and refine based on the output.

**Want to see output first?** Copy the example into place and run any skill against it:
```bash
cp profiles/examples/legal-ops-example.md profiles/client-profile.md
```
Swap in your own profile when you're ready.

---

## Step 2: Choose Your Starting Skills

Don't start with all 14. Pick the 3-4 that match your role and biggest time sinks.

### If You're a BDR

Your job is pipeline generation. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Account Pre-Qualification** (01) | Stop spending time on bad-fit accounts. Get a scored verdict before you research anything. |
| 2 | **Account Snapshot** (02) | A complete outbound package (brief, emails, call sheet) for one account in one run. |
| 3 | **Daily Prospecting** (07) | Start every morning with a prioritized dial sheet and personalized openers. |
| 4 | **Trigger Event Outbound** (04) | When you spot a signal (new exec, M&A, compliance failure), act inside the window. |

**First week:**
- Day 1: Run 01 and 02. Qualify 10 accounts. Build 3 outbound packages.
- Day 2: Add 07. Run your morning dial sheet. Compare it to your old process.
- Days 3-5: Refine your Client Profile based on output quality. Add 04 when you spot a trigger event.

### If You're an AE

Your job is pipeline progression and closing. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Meeting Prep** (06) | A structured call sheet in about 90 seconds instead of half an hour of prep. |
| 2 | **Deal Pulse** (08) | Know which deals are healthy and which are dying before your manager asks. |
| 3 | **MEDDPICC Analysis** (09) | Deep qualification that exposes gaps before they kill the deal late. |
| 4 | **Stakeholder Mapping** (10) | Find the people you're not talking to but should be. |

**First week:**
- Day 1: Run 06. Prep for tomorrow's calls.
- Day 2: Run 08 on your top 5 deals. Find the one you thought was solid but isn't.
- Days 3-5: Run 09 on your commit deals. Run 10 on any deal with 3+ stakeholders.

### If You're a Sales Manager

Your job is coaching, forecasting and process consistency. Start here:

| Priority | Skill | Why |
|----------|-------|-----|
| 1 | **Call Coaching** (13) | Grade calls against methodology (SPIN /30, Challenger /40) instead of vibes. |
| 2 | **Deal Pulse** (08) | Pipeline review in data, not stories. 16 signals across 4 pillars. |
| 3 | **MEDDPICC Analysis** (09) | Stop asking "how's the deal?" Start asking "show me the evidence." |
| 4 | **Sales-to-CS Handoff** (14) | Clean handoffs that don't blow up in month two. |

**First week:**
- Day 1: Run 13 on 2 calls. Share the report with the rep.
- Day 2: Run 08 on your team's top 10 deals. Stack-rank by health score.
- Days 3-5: Run 09 on every commit deal. Flag the ones with evidence gaps.

### If You're a GTM Consultant

You're deploying this across client engagements. Start with the full system:

1. Fill out a Client Profile for your client (use their language, not yours).
2. Run the [30-day chaining sequence](../README.md#skill-chaining) from the README.
3. Add the operating layer: O4 Context Gap before you build anything for the client, O1 Verify before you call anything done.
4. When you move to a new client, swap `profiles/client-profile.md`. Everything else carries over.

---

## Step 3: Run the Skills From Where You Work

### Option A: Run from the cloned repo (recommended)

Open Claude Code inside the `vertical-gtm-skills` folder. The repo's `CLAUDE.md` loads automatically, knows every skill, and checks your profile first. Ask for what you need in plain language. This is the path every skill's pointer to `profiles/client-profile.md` is built for.

### Option B: Reference the skills from your own project

If you'd rather work from another project folder, add this to that project's `CLAUDE.md`, with the real path to your clone:

```markdown
## GTM Skills
When I ask for sales-related tasks, read and follow the relevant skill from:
/path/to/vertical-gtm-skills/skills/
The client profile every skill reads is at:
/path/to/vertical-gtm-skills/profiles/client-profile.md

Available skills:
- Meeting prep: 06-meeting-prep/SKILL.md
- Deal scoring: 08-deal-pulse/SKILL.md
- Call coaching: 13-call-coaching/SKILL.md
[add the skills you use]
```

Keep the profile line. The skills point to `profiles/client-profile.md` relative to the repo, so from another folder Claude needs to be told where it is. The starter kit has a fuller [identity template](../starter-kit/identity-template.md).

### Option C: Slash commands

Create a command file that triggers a skill:

```bash
mkdir -p .claude/commands
```

Create `.claude/commands/meeting-prep.md`:
```markdown
Read the skill at /path/to/vertical-gtm-skills/skills/06-meeting-prep/SKILL.md
and the client profile at /path/to/vertical-gtm-skills/profiles/client-profile.md,
then execute the skill for: $ARGUMENTS
```

Then in Claude Code, type: `/meeting-prep Discovery call with Corvane Industrial, meeting their General Counsel tomorrow`

---

## Step 4: Run Your First Skill

### Example: Meeting Prep

With the Lexora example profile in place, open Claude Code and type:

```
I have a discovery call tomorrow at 2pm with Dana Whitfield, the new General Counsel
at Corvane Industrial. $3.2B manufacturer, 38 in-house attorneys, on Competitor X
since 2019. This is our first meeting. Prep me.
```

Claude will:
1. Read the Meeting Prep skill
2. Pull the Client Profile (ICP match, the GC persona, pain hypotheses)
3. Produce a single-page prep sheet with:
   - A SPIN question bank (Situation, Problem, Implication, Need-Payoff)
   - Persona-matched proof points
   - Competitive positioning notes against Competitor X
   - Meeting open and close scripts
   - Risk flags and things to listen for

Compare it with the worked example inside `skills/06-meeting-prep/SKILL.md`. Then run the same prompt shape on one of your own accounts with your own profile in place.

### Example: Deal Pulse

```
Score the Corvane Industrial deal. Here's what I know:
- Met with the GC and the Head of Legal Ops (2 of about 5 stakeholders)
- They confirmed invoice review eats about 3 attorney-weeks a quarter
- No budget discussion yet
- They are on Competitor X and the renewal is in 7 months
- Next step: demo with the legal ops team next week
```

Claude scores all 16 signals across 4 pillars (Why Anything, Why Us, Why Now, Execution), computes a health score (0-100), names the top risks and recommends next actions.

---

## Common Questions

### "How is this different from a prompt library?"
A prompt library gives you a starting point. You paste it, tweak it and hope for good output. A skill is a complete methodology with scoring logic, evidence rules and a fixed output format. Claude doesn't just answer your question. It runs a process.

### "Do I need all 14 skills?"
No. Start with 3-4 based on your role (see Step 2), and add more as you get comfortable.

### "What are the operating skills, and do I need them?"
They are the disciplines around the sales work: checking work before calling it done (O1 to O5), keeping a team knowledge base honest (O6 to O11), and the strategy work that fills your profile with evidence (O12 to O15). You don't need them to run the sales skills. Start with O1 Verify once other people rely on what you produce, and read [How It Fits Together](how-it-fits.md) for the rest.

### "How do I know the output is good?"
Every skill has built-in quality gates. Deal Pulse scores on evidence, not assumptions. Call Coaching grades against methodology criteria. MEDDPICC grades the evidence behind every element. The skills are designed to surface what's missing, not just confirm what you already believe. The Lexora examples show what good output looks like, so compare against them.

### "Can I modify the skills?"
Yes. They're MIT licensed. Every skill ships a `CUSTOMIZE.md` interview that adapts it to your motion. Common modifications:
- Add custom scoring criteria
- Change framework weights
- Add industry-specific qualification dimensions
- Paste CRM data into the conversation as context

See the [Customization Guide](customization.md).

### "What if I use a different methodology than SPIN/MEDDPICC?"
The frameworks are modular. You can swap SPIN for Sandler, Challenger for your own demo methodology, or add Gap Selling alongside MEDDPICC. See the [Customization Guide](customization.md).

---

## What's Next

Once you've run a few skills and refined your Client Profile:

1. **Read the [Skill Reference](skill-reference.md)** for the decision tree (which skill for which situation) and chaining patterns.
2. **Try skill chaining.** Run Account Pre-Qualification, then Account Snapshot, then Meeting Prep on the same account.
3. **Add the operating layer** using [How It Fits Together](how-it-fits.md).
4. **Read the [Vertical GTM Guild](https://substack.com/@verticalgtmguild)** series for the full system architecture (knowledge layer, operations, measurement, team transformation).
5. **Join the [Vertical GTM Guild](https://verticalgtmguild.com)** to connect with other operators building AI-native GTM teams.
