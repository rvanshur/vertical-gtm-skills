# Customize: Account Pre-Qualification

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

Read the attached SKILL.md (gtm-account-qualification). It scores accounts against 8 weighted ICP criteria and returns GREENLIGHT / MANUAL REVIEW / DISQUALIFY.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Describe your last 10 closed-won customers. What did they have in common BEFORE the
   first call -- size band, vertical niche, systems in place, a trigger event? Those traits
   are your real criteria, whatever the ICP slide says.

2. Name three deals your team worked that it never should have. What single fact, knowable
   on day one, would have disqualified each?

3. Which of your criteria are observable from the outside (site, filings, job posts) and
   which only surface in discovery? Outside-observable ones belong in this skill; the rest
   belong to Meeting Prep.

4. Weighting: which one criterion, when it is wrong, kills the deal no matter how good the
   rest look? Which two barely matter but everyone argues about them?

5. Where is your manual-review band -- the score range where you would still want a human
   to eyeball the account before a rep spends a morning on it?

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

Most operators answer question 1 from memory and stall on questions 2 and 4. **Question 2
stalls** when there is no loss record to reason from -- bad-fit deals are remembered as bad
luck. **Question 4 stalls** when the ICP was written by consensus, so every criterion weighs
the same and none of them decide anything.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Qualification Criteria
- **Weighted criteria (8 max):** [criterion -> weight -> how to observe it from outside]
- **Day-one tripwires:** [the facts from question 2 that auto-DISQUALIFY]
- **Manual-review band:** [the score range a human still checks]
```

---

## If you want to add a ninth criterion

Don't. Eight weighted criteria is already at the edge of what a scorer can keep honest; every
added criterion dilutes the weights of the ones that decide. If a new fact matters, ask which
existing criterion it is evidence FOR, and fold it in there.
