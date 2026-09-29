# Customize: Debate

A paste-in prompt that adapts this skill to your go-to-market motion.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-debate). It convenes a panel of opposing expert personas
to pressure-test a decision, argue the trade-offs, and end with a decision matrix and a
plain-language read.

Your job is NOT to rewrite it. It is to make it fire on the kinds of decisions we actually
make at my company, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What kinds of decisions come to the table at our company? (Product direction, positioning,
   architecture, copy, pricing strategy, hiring, whatever is real for us)

2. For each type of decision, how much time do we spend arguing before committing? (15
   minutes? An hour? A whole meeting? Never?)

3. Which of those decisions have surprised us after we made them? (What cost did we not
   see coming? What assumption broke?)

4. How do we record decisions today? (A Slack thread? A doc? A meeting note? Nothing?)

5. If somebody wanted to make the case against a decision you are considering, who would
   make it and what would they look like? (Another person on the team? Someone not in the
   room? A different school of thought than yours?)

Then produce:

A. A revised "Expert Archetype Bank" where each school of thought reflects our actual
   decision-makers and how they think, not generic ones.

B. A revised "Best Practices" using MY surprise from question 3, written so it is
   recognizable to my team but names no individual.

C. A list of the decision types from question 1, and for each one, whether we should
   converge (one right answer) or diverge (real alternatives), and why.

D. THE HONEST PART: a short list of the questions above I could not answer concretely.
   If we do not have a discipline for arguing decisions before committing, that gap is the
   finding. If decisions just happen in Slack and never get recorded, that is the blocker
   this skill cannot fix alone, we have to fix that first.

Start with question 1.
```

---

## What you should expect to happen

Questions 1 and 2 usually land. Question 3 is where you get gold. Questions 4 and 5 stall
when the decision-making process is informal or personality-driven ("it depends who is in
the room," "we just decide and move").

If output section D is long, the work is not in the skill. It is in the process. This skill
assumes you have (or want to build) a deliberate decision-making discipline. If decisions
get made in the moment and the opposing case never gets stated, this skill cannot help until
you commit to stating it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once, and every skill in the suite inherits them:

```markdown
## Decision Discipline

- **Decision types:** [the kinds of decisions that come to the table, product, positioning, architecture, etc.]
- **Decision recording:** [where decisions get written and why they were made]
- **Who argues:** [who makes the case for paths not chosen]
- **Converge vs. diverge:** [for each decision type, do we seek one answer or keep real alternatives open]
```
