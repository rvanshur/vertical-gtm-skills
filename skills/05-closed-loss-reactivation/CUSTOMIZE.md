# Customize: Closed-Loss Reactivation

A paste-in prompt that adapts this skill to *your* go-to-market motion.

Works in **Claude Code**, **OpenAI Codex**, **Claude.ai / ChatGPT Projects**, or a **custom GPT**. Attach `SKILL.md` as knowledge and paste the block below; all platforms read the same `SKILL.md` format. Open the assistant, paste the block, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-closed-loss-reactivation). It classifies why a deal died (7 loss categories), assesses what has changed, re-qualifies fit, and generates history-aware re-engagement sequences.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Pull 10 real closed-lost deals. For each: what does the CRM say the loss reason was,
   and what was it actually? (The gap between those two answers is the whole exercise.)

2. Which of the seven loss categories dominate your book -- price, timing, incumbent,
   champion left, no decision, feature gap, bad fit?

3. In your vertical, what actually reopens a door -- new funding, a leadership change, a
   renewal date, a regulation, a failed implementation of the competitor they chose?

4. Per category, how long after the loss is re-entry credible? Too early reads as not
   accepting no; too late and the moment passed.

5. What did we promise, imply, or get wrong in the lost deal that the re-engagement must
   not contradict? The prospect remembers the last conversation better than we do.

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

**Question 1 stalls almost universally**: loss reasons in the CRM are recorded at the moment
of giving up, by the person most motivated to call it "price." If your loss data is one-word
fields, the classification step has nothing true to classify -- and that finding is worth
more than any sequence this skill generates.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Closed-Loss Intelligence
- **Loss taxonomy mapping:** [CRM reason -> what it usually actually means for us]
- **Re-entry windows:** [loss category -> credible timing]
- **Reopening events:** [what changes that we can detect, and how]
- **Incumbent renewal cycles:** [competitor -> typical contract length]
```

---

## Before any sequence sends

History-aware openers only work when the history is true. Verify the old thread -- who said
what, last -- before referencing it. A wrong "when we last spoke" ends the reactivation and
salts the account.
