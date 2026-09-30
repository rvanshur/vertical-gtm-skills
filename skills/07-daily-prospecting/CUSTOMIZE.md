# Customize: Daily Prospecting

A paste-in prompt that adapts this skill to your go-to-market motion.

Works in Claude Code, OpenAI Codex, Claude.ai/ChatGPT Projects, or a custom GPT (attach `SKILL.md` as knowledge and paste the block below). They all read the same `SKILL.md` format. Open the assistant, paste the block, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-daily-prospecting). It builds the morning dial sheet: 4-tier prioritization (Hot/Warm/New/Recycle), per-account pre-call briefs, openers, and call goals, tiered off CRM fields.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What makes an account HOT today in your motion -- an inbound signal, a trigger event,
   engagement in the last 48 hours? Define it in facts a system could check.

2. How many dials does a rep actually make per day? The tier sizes have to match that
   capacity or the sheet becomes a backlog, not a plan.

3. What are the exclusion rules -- active opportunities, accounts owned by an AE,
   do-not-call verticals? Who must never appear on a BDR's sheet?

4. What does your best cold-connect opener sound like, word for word? Not the script --
   what your best rep actually says.

5. Which CRM fields are maintained well enough to tier on, and which are fiction? Tiering
   on a field nobody updates produces a confidently wrong list every morning.

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

**Question 5 stalls** the most and matters the most: every tiering rule inherits the honesty
of the field it reads. If "last activity date" is only right for half the reps, tier
assignments are coin flips wearing labels. Fix the two fields that matter before customizing
anything else.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Daily Prospecting
- **Hot definition:** [checkable facts, not vibes]
- **Daily capacity:** [dials/day -> tier size budget]
- **Exclusion rules:** [who never appears on the sheet]
- **Opener, verbatim:** [what the best rep actually says]
- **Trustworthy CRM fields:** [field -> trust level -> who maintains it]
```

---

## Four tiers, not five

The tier count is fixed because a rep triages four buckets pre-coffee and cannot triage six.
If two account types compete for Hot, sharpen the Hot definition rather than adding a tier.
