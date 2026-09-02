# Customize: Competitive Displacement

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

Read the attached SKILL.md (gtm-competitive-displacement). It generates outbound sequences aimed at a known incumbent's customer base, built on documented failure patterns and displacement proof points.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Whose base are you targeting, and why NOW -- a price increase, an end-of-life, an
   acquisition, a support collapse? Displacement outbound without a "why now" is just
   claiming to be better.

2. Which of the incumbent's failure patterns can you PROVE -- meaning a customer you won
   away has described it in their own words? List only those.

3. Your two or three won-away stories, with numbers: what was failing, what changed after
   the switch, how long the migration took.

4. Switching-cost honesty: what does migration from this incumbent really involve -- data,
   retraining, integrations, contract exit? The sequence must survive the prospect asking.

5. Renewal timing: when do their contracts come up, and how do you find out -- public
   procurement records, asking on calls, industry chatter?

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

**Question 2 stalls** when failure patterns come from your own sales floor instead of from
won-away customers' mouths -- and that gap is dangerous, because the incumbent's customers
know their real failures better than you do. **Question 4 stalls** when nobody has documented
a migration honestly; "seamless" is not a migration plan.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Displacement
- **Target incumbent + why now:** [the event making this timely]
- **Proven failure patterns:** [pattern -> the won-away customer who said it]
- **Won-away stories:** [before -> after -> migration duration, with numbers]
- **Honest switching costs:** [what migration really takes]
- **Renewal intelligence:** [how we learn contract timing]
```

---

## The one rule

Never send a failure-pattern claim you cannot trace to a won-away customer. The people
receiving these emails LIVE in the incumbent's product; one wrong claim identifies you as a
vendor who guesses.
