# Customize: Account Snapshot

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

Read the attached SKILL.md (gtm-account-snapshot). It is the BDR daily driver: rapid research, ICP quick-score, persona-mapped contacts, pain hypotheses, a 3-step email sequence, and a cold-call sheet -- one page.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which three personas do you actually get meetings with, and which persona are you told
   to target but has never once converted? Titles as they appear in YOUR vertical, not the
   generic ones.

2. Paste your best-performing cold email -- the one that got real replies. What about it is
   load-bearing (the trigger, the number, the tone)? That becomes the sequence's voice.

3. Which research sources are actually reliable in your vertical (permit databases, state
   registries, job boards, association directories, local trade press)? Where does public
   data run out?

4. What is the honest time budget per account -- five minutes or twenty-five? The snapshot
   depth has to match it or reps skip the skill.

5. What separates "call this account today" from "sequence it and wait" in your motion?

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

**Question 2 stalls** when nobody kept the winning emails -- performance lives in anecdote,
not in a swipe file. **Question 3 stalls** when research habits were inherited from a
horizontal playbook and nobody has mapped what your vertical actually exposes publicly.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Personas
- **Converting personas:** [title -> what they care about -> proof point that lands]
- **Dead persona (do not sequence):** [title + why it never converts]

## Outbound Voice
- **Reference email:** [paste the best performer]
- **Vertical research sources:** [source -> what it reliably tells you]
- **Call-today triggers:** [the facts that jump the queue]
```

---

## If the one-pager grows

The cheatsheet is one page because a BDR reads it between dials. Anything that pushes it to
two pages belongs in Research-Driven Outbound (03), which is the deep version of this skill.
