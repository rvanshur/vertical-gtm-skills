# Customize: Closed-Loss Reactivation

A paste-in prompt that adapts this skill to your go-to-market motion. The interview asks about the closed-lost deals you already have, and it writes the one profile section this skill reads: Closed-Loss Intelligence.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a sales skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-closed-loss-reactivation). It checks the recorded loss reason
of a closed-lost deal against the evidence, looks for what has changed since, re-scores fit,
and returns REACTIVATE, MONITOR or RETIRE with a history-aware opener.

Your job is NOT to rewrite it. It is to make it fit my accounts, my personas and my vertical,
and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Pull 10 real closed-lost deals. For each one: what does the CRM say the loss reason was,
   and what was it actually? The gap between those two answers is the whole exercise.

2. Which loss categories dominate my book: price, timing, incumbent, champion left, no
   decision, feature gap, or bad fit?

3. In my vertical, what actually reopens a door? For example new funding, a leadership change,
   a renewal date, a regulation, or a failed implementation at the rival we lost to.

4. For each loss category, how long after the loss is re-entry credible? Too early reads as not
   accepting no. Too late and the moment has passed.

5. What did we promise, imply or get wrong in the lost deal that the re-engagement must not
   contradict? The prospect remembers the last conversation better than we do.

Then produce:

A. A revised Quick Reference, written in terms of MY accounts, personas and vertical, not
   generic ones.

B. A revised Examples section, built from the real answers I gave you. Recognizable to my team,
   naming no individual.

Before section C, write THE HONEST PART: the questions above that you could not answer
concretely, and what I would need to gather to answer them. Do not paper over these. An answer
you guessed at is a gap, and the gap is the finding.

C. The Closed-Loss Intelligence section, filled with the exact values I gave you, ready to paste
   into profiles/client-profile.md. This is the last thing you produce.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 1 Stalls Almost Universally.** Loss reasons in the CRM are recorded at the moment of
giving up, by the person most motivated to call it "price." If your loss data is one-word fields,
the classification step has nothing true to classify. That finding is worth more than any
sequence this skill generates.

Both kinds of stall point at the same missing thing: a context layer. The skill is a procedure.
A procedure needs to know who you sell to, what has worked, and what has already gone wrong.
That is what `profiles/client-profile.md` is for. Build it once and every skill in the suite
inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. The shape matches the Sales-Layer Sections
block in the template exactly:

```markdown
## Closed-Loss Intelligence
- **Loss taxonomy mapping:** [CRM reason, what it usually means for us]
- **Re-entry windows:** [loss category, credible timing]
- **Reopening events:** [what changes that we can detect, and how]
- **Incumbent renewal cycles:** [competitor, typical contract length, source]
```

Also fill the two right-hand columns of the Competitive Landscape table for each rival:
"Pain reported after 6 to 12 months (with source)" and "Proof that answers it." This skill reads
both in Step 6. Leave a cell blank when you cannot source it. A blank is unknown, and the skill
treats it that way.

---

## Before Any Sequence Sends

History-aware openers only work when the history is true. Verify the old thread (who said what,
and when) before referencing it. A wrong "when we last spoke" ends the reactivation and damages
the account for the next rep.
