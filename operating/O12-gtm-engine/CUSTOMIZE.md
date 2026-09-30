# Customize: GTM Engine

A paste-in prompt that adapts this skill to your growth system.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt GTM Engine to build a repeatable growth system.

Read the attached SKILL.md (gtm-engine). It guides post-launch growth through retrospectives,
experimentation frameworks, funnel optimization, growth loops, strategic narrative, and email
automation. If profiles/client-profile.md exists, read its Company, ICP Definitions, Buyer
Personas, Value Propositions and Proof Points sections first.

Your job is NOT to rewrite the framework. It is to help me identify which growth lever matters
most right now and build a system around it.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What happened in your launch? (What worked, what underperformed, what surprised you?)

2. If you had to pick one number that tells you growth is working, what is it? (Retention,
   qualified leads, revenue, churn, whatever matters most to your survival)

3. What is your current bottleneck? (Why are you not growing faster: traffic, conversion,
   retention, unit economics?)

4. Do you have a narrative about why the market is shifting that explains why you exist? If
   yes, what is it? If no, what is your hypothesis?

5. How much time can you dedicate to running a growth system? (Hours per week, team size)

Then produce:

A. Launch retrospective with channel-by-channel analysis and strategic decisions (double down,
   experiment, cut)

B. Two-week growth sprint framework with an initial experiment backlog (ICE-scored)

C. Funnel optimization backlog focused on your biggest bottleneck (PIE-scored)

D. Growth loop assessment (viral, content, paid fit for your product)

E. Three-layer strategic narrative positioning your market shift

F. The "Growth System" profile section below, filled in with my answers

G. THE HONEST PART: if retention is broken, growth will not fix it. If your bottleneck is not
   attacked directly, nothing else matters. Be clear on priority, and list the questions above
   I could not answer with a number.

Start with question 1.
```

---

## What you should expect to happen

Question 1 goes smoothly for anyone who launched in the last quarter, and badly for anyone who
launched longer ago than that, because nobody wrote the channel results down at the time.
Question 2 is where most teams discover they track five numbers and trust none of them.
Question 3 stalls more than any other, usually because the honest answer is retention, and
retention is the one lever a growth sprint cannot move on its own.

If section G comes back long, that is the finding. A growth system built on numbers nobody
measured will run experiments against noise.

---

## Minimum profile fields this skill reads

The skill starts from the profile sections every GTM skill already uses (Company, ICP
Definitions, Buyer Personas, Value Propositions, Proof Points). Add one section of its own to
`profiles/client-profile.md`:

```markdown
## Growth System

- **North-star metric:** [the one number that says growth is working, and where it is measured]
- **Current bottleneck:** [traffic, conversion, retention or unit economics, with the number]
- **Sprint cadence:** [two weeks by default; who reviews the results]
- **Narrative:** [one sentence on the market shift that explains why you exist]
```

---

## If you are stuck on any question

- **Question 1 stalls:** you have no launch record. Run a five-minute reconstruction from what
  you do have (CRM source fields, ad spend, calendar), mark every number as estimated, and start
  writing results down from this sprint on.
- **Question 2 stalls:** pick the number closest to cash that you can measure weekly. You can
  change it later. Running without one is worse than running with the wrong one for a month.
- **Question 3 stalls:** look at where the funnel loses the most people in absolute terms, not
  percentages. That is usually the bottleneck, whatever the team's favorite theory says.
- **Question 4 stalls:** go back to GTM Positioning (`operating/O14-gtm-positioning`). A
  narrative is positioning told over time, and it cannot be invented here.

---

## When you are ready to scale

After the growth system is built, you know:
- Which channels to keep investing in (and which to kill)
- What your highest-leverage experiment to run is
- Which conversion rate is holding you back the most
- Whether a loop exists that makes growth compound
- What story ties all your content together

When you have that, growth becomes predictable. Not automatic, but predictable. Same system
every month. Same cadence. Same review. That is how consistency beats brilliance.

If you skip the retrospective and just keep doing what you did at launch, you will plateau. If
you run experiments without a backlog or ICE scoring, you will chase shiny objects. If you build
content without a narrative, it will be noise.

The system is what compounds. Not the brilliance of any single tactic, but the consistency of
the system.
