# Customize: Call Coaching

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

Read the attached SKILL.md (gtm-call-coaching). It grades recorded calls against methodology rubrics (SPIN /30 for discovery, Challenger /40 for demos), with MEDDICC assessment, pain mapping, and coaching recommendations.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which framework do you grade against -- SPIN and Challenger as shipped, or your own
   methodology? If yours, give me its categories and what a top score in each looks like.

2. Calibration: point me at one call you consider an A and one a C (transcripts or notes).
   What separates them, in your words? Your answer calibrates every grade after it.

3. Which rubric categories does your team chronically miss -- quantifying impact, asking
   for commitment, silence after questions? The coaching sections should overweight those.

4. Who sees the scores -- the rep only, their manager, leadership? Be honest, because the
   answer changes the tone of every coaching note this skill writes.

5. Where do transcripts come from and how good are they -- speaker labels, crosstalk,
   redactions? A grader is only as good as what it can read.

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

**Question 2 stalls** when nobody has ever agreed what an A call sounds like -- every
manager grades from taste, which is precisely the inconsistency this skill exists to remove.
Answer it even roughly; two calibration calls beat zero.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Call Coaching
- **Framework + rubric:** [SPIN/Challenger as shipped, or yours with categories]
- **Calibration pair:** [the A call and the C call, and what separates them]
- **Chronic misses:** [categories to overweight in coaching]
- **Score visibility:** [who sees what]
- **Transcript source + quality:** [tool -> known limitations]
```

---

## Keep scores diagnostic

The moment scores touch compensation or stack rankings, calls get performed for the grader
and the signal dies. Grade to coach. If leadership wants a number, give them the team trend,
never the per-call score.
