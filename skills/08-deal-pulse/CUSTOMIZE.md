# Customize: Deal Pulse

A paste-in interview that adapts this skill to your deals. It asks what your record can show about each signal, what counts as evidence, where you would intervene, and what your team calls the four methods. It writes the Deal Health section the skill reads.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a sales methodology skill to my team's deals.

Read the attached SKILL.md (gtm-deal-pulse). It scores one open deal from 0 to 100 across 16 signals in 4 pillars, with evidence tags and named next actions.

Your job is NOT to rewrite the skill. It is to make it fit my deals, my buyers and my methods, and to tell me honestly where you cannot answer.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Walk the 16 signals. Which can we see in our CRM, call notes or emails? Which could we see with effort? Which will we never see? A signal we cannot observe scores as noise every time.

2. What do we call these four methods: the rapport method, the momentum method, the urgency method, and the day-in-the-life walkthrough? If we have no name for one, say so. The skill will use its plain name.

3. What counts as evidence in our world? Which of these is the rep's word, and which is in the record: an email from the economic buyer, a signed order form, a calendar invite with their executive on it? Draw the line precisely, in terms of the six tags.

4. At what score do we actually intervene, and what does intervention mean: a coaching session, an executive call, a re-forecast?

5. When does this run: a weekly pipeline review, before forecast commit, or ad hoc? The cadence decides whether trends are visible or every score is a snapshot.

6. Take our last five lost deals. Which pillar would have caught each loss earliest, and how many weeks before the close date did the evidence exist?

Then produce:

A. A revised "Quick Reference" written in terms of MY deals, buyers and vertical, not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my team but naming no individual.
C. The Deal Health section, with the four method names I gave you, ready to paste in.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 3 Stalls** when the team has never separated evidence from optimism. Everything a rep says gets recorded as fact. **Question 6 stalls** when lost deals get autopsied by anecdote, so nobody knows which signals actually predicted anything.

Both kinds of stall point at the same missing thing: a context layer. The skill is a procedure, and a procedure needs to know who you sell to, what has worked and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once and every skill in the suite inherits it.

The answers to questions 1, 3, 4 and 5 shape the Quick Reference, the examples and the honest part. They are not profile fields, because the skill does not read them. The four method names are the only fields this skill reads from the profile.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. Leave a name blank to have the skill use its plain name.

```markdown
## Deal Health
- **Rapport method name:** [your team's name for it]
- **Momentum method name:** [your team's name for it]
- **Urgency method name:** [your team's name for it]
- **Day in the Life method name:** [your team's name for it]
```

---

## Before You Re-Weight The Pillars

Score ten real deals with the stock weights first. Re-weighting from intuition reproduces the intuition the scorer exists to check. After ten deals you will have actual disagreements between score and outcome, and re-weight from those.
