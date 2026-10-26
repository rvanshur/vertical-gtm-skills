# Customize: MEDDPICC Analysis

A paste-in interview that adapts this skill to your own go-to-market motion. It asks its questions one at a time, then writes the MEDDPICC section of your client profile.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT. Paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-meddpicc-analysis). It scores deals across all 8 MEDDPICC elements from the CRM record, computes weighted health, and recommends ADVANCE, HOLD, DOWNGRADE or DISQUALIFY.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which MEDDPICC elements does your team already speak fluently, and which are foreign
   words? (If "paper process" gets blank stares, the rubric needs your vocabulary first.)

2. Metrics: what number does a real champion carry to their boss to justify buying you?
   Not your value prop, but the number THEY use internally.

3. Map the paper process in your vertical start to finish: security review, procurement,
   legal, board approval, licensing? What is the longest it has actually taken?

4. Champion proof-of-life: what have REAL champions done for you, such as setting up the
   exec meeting, forwarding internal emails, or defending you in a meeting you were not in?
   Those actions become the evidence bar. Do not restate the shared champion tests. Give me
   your team's own examples of each.

5. Which element, when weak, has actually lost you deals? Rank your top three killers from
   real losses, not from the MEDDPICC book.

6. Do you use the default stage minimums, or does your team set its own? If you set your own,
   give me the health score and critical elements for each stage.

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts, personas, and vertical,
   not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my
   team but naming no individual.
C. The MEDDPICC section for profiles/client-profile.md, with the exact values I gave you,
   ready to paste in. Use the field names in "Minimum Profile Fields This Skill Reads".
D. THE HONEST PART: the questions above I could not answer concretely, and what I would
   need to gather to answer them. Do not paper over these. An answer I guessed at is a
   gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 4 stalls** on champion inflation, where every friendly contact is recorded as a
champion until the deal needs one. **Question 2 stalls** when the metric lives in your deck
but has never been heard back from a customer's mouth, which means no deal has ever truly had
the M.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for. Build it once and every skill
in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. Each field is read by a named step of the skill:

```markdown
## MEDDPICC
- **Stage minimums:** [the team's own health and critical-element minimums, or "default" to use the skill's table]
- **Paper process steps:** [step, owner, typical duration. Read by Paper Process scoring]
- **Metric, customer-worded:** [the number a champion repeats back. Read by Metrics scoring]
- **Champion proof-of-life:** [the team's own examples of champion actions it has seen in won deals. Read by Champion scoring]
- **Deal killers from real losses:** [the elements that lost deals, ranked. Read by the gap ranking in Step 4]
```

---

## Keep The Evidence Grades

Whatever else you adapt, do not remove evidence grading. A MEDDPICC score without evidence
grades is a confidence survey of the rep, and reps are confident.
