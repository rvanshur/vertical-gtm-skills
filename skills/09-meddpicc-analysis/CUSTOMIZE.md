# Customize: MEDDPICC Analysis

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

Read the attached SKILL.md (gtm-meddpicc-analysis). It scores deals across all 8 MEDDPICC elements with evidence-graded rubrics, computes weighted health, and flags risk patterns.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which MEDDPICC elements does your team already speak fluently, and which are foreign
   words? (If "paper process" gets blank stares, the rubric needs your vocabulary first.)

2. Metrics: what number does a real champion carry to their boss to justify buying you?
   Not your value prop -- the number THEY use internally.

3. Map the paper process in your vertical start to finish: security review, procurement,
   legal, board approval, licensing? What is the longest it has actually taken?

4. Champion proof-of-life: what have REAL champions done for you -- set up the exec
   meeting, forwarded internal emails, defended you in a meeting you weren't in? Those
   actions become the evidence bar.

5. Which element, when weak, has actually lost you deals? Rank your top three killers from
   real losses, not from the MEDDPICC book.

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

**Question 4 stalls** on champion inflation -- every friendly contact is recorded as a
champion until the deal needs one. **Question 2 stalls** when the metric lives in your deck
but has never been heard back from a customer's mouth, which means no deal has ever truly had
the M.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## MEDDPICC
- **Element weights:** [from question 5's real killers, not defaults]
- **The champion tests:** [actions that count as proof-of-life]
- **Paper process checklist:** [step -> owner -> typical duration]
- **The metric, customer-worded:** [the number champions actually repeat]
```

---

## Keep the evidence grades

Whatever else you adapt, do not remove evidence grading. A MEDDPICC score without evidence
grades is a confidence survey of the rep, and reps are confident.
