# Customize: Deal Pulse

A paste-in prompt that adapts this skill to *your* go-to-market motion.

Works in **Claude Code**, **OpenAI Codex**, **Claude.ai / ChatGPT Projects**, or a **custom GPT**
(attach `SKILL.md` as knowledge and paste the block below) -- they all read the same `SKILL.md`
format. Open the assistant, paste the block, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-deal-pulse). It scores active deals 0-100 across 16 signals in 4 pillars, with evidence grading and next actions.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Walk the 16 signals: which are observable in YOUR sales motion, which could be with
   effort, and which never will be? An unobservable signal scores as noise forever.

2. Take your last five lost deals. Which pillar would have caught each loss earliest, and
   how many weeks before the close date did the evidence exist?

3. What counts as VERIFIED evidence in your world -- an email from the economic buyer, a
   signed order form, a calendar invite with their exec on it? And what is merely
   rep-reported? Draw the line precisely.

4. At what score do you actually intervene, and what does intervention mean -- a coaching
   session, an exec sponsor call, a re-forecast?

5. When does this run -- a weekly pipeline review, before forecast commit, ad hoc? The
   cadence decides whether trends are visible or every score is a snapshot.

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts, personas, and vertical,
   not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my
   team but naming no individual.
C. The fields this skill now needs from profiles/client-profile.md, with the exact values
   I gave you, ready to paste in.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would
   need to gather to answer them. Do not paper over these. An answer I guessed at is a
   gap, and the gap is the finding.

Start with question 1.
```

---

## What you should expect to happen

**Question 3 stalls** when the team has never separated evidence from optimism -- everything
a rep says is recorded as fact. **Question 2 stalls** when lost deals get autopsy-by-anecdote,
so nobody knows which signals actually predicted anything.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Deal Health
- **Signal availability:** [signal -> observable? -> source]
- **Evidence rules:** [what VERIFIED means here, precisely]
- **Intervention thresholds:** [score band -> who acts -> what they do]
- **Review cadence:** [when this runs, and against which deals]
```

---

## Before you re-weight the pillars

Score ten real deals with the stock weights first. Re-weighting from intuition reproduces
the intuition the scorer exists to check. After ten deals you will have actual disagreements
between score and outcome -- re-weight from those.
