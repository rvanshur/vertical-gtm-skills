# Customize: Competitive Strategy

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

Read the attached SKILL.md (gtm-competitive-strategy). It builds deal-specific competitive strategy for an active opportunity: incumbent profile, gap matrix, displacement playbook, and a win plan with battlecard.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which three competitors do you actually face, and in roughly what share of deals? (The
   one you fear and the one you meet are often different companies.)

2. For the top one: your last three wins and last three losses against them. What actually
   decided each -- not the official reason, the real one?

3. Which of your claimed gaps are PROVABLE (a customer who switched will say it, a
   side-by-side shows it) and which are sales-floor folklore?

4. What traps do they set for you -- the talk track their reps run about your product?
   What do prospects repeat back to you that came from them?

5. What proof actually lands in this vertical -- a reference call, a migration story with
   numbers, a live side-by-side? What has moved a deal, witnessed, not assumed?

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

**Question 2 stalls** because win-loss "why" was never captured within a week of the outcome,
after which it becomes folklore. **Question 3 is where honesty pays**: most gap matrices are
half folklore, and a rep who repeats an unprovable gap to a well-informed prospect loses the
room instantly.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Competitive Landscape
- **Competitor profiles:** [competitor -> frequency -> their real strength]
- **Provable gaps:** [gap -> the proof -> source]
- **Folklore (do not say aloud):** [claims we cannot source]
- **Their traps:** [their talk track about us -> our counter]
- **Proof that lands:** [asset -> the deal it moved]
```

---

## Grade every gap-matrix row

Each row carries an evidence grade or it carries the word FOLKLORE. The matrix's job is not
to make you feel armed; it is to keep a rep from confidently repeating something a prospect
can disprove.
