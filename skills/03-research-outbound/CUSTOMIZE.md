# Customize: Research-Driven Outbound

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

Read the attached SKILL.md (gtm-research-outbound). It builds a deep-research POV brief and outbound package from 10-Ks, earnings calls, or private-company intelligence, including a quantified financial wedge.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which financial signals in your vertical actually predict a deal -- segment margins,
   backlog, headcount moves, capex lines, churn language in the risk factors? Name the ones
   you have seen precede a real opportunity.

2. Your quantified wedge: what number does your product move, and what is the honest range
   you can defend (not the best case)? What proof stands behind it?

3. Tell me about one enterprise target where research genuinely changed the message you
   sent. What did you find, and where?

4. Most of your targets are private. Which sources exist for private companies in YOUR
   vertical (state filings, permits, licensing boards, bonding records, franchise
   disclosures)?

5. Who consumes the POV brief -- the rep alone, or does part of it go in front of the
   prospect? That decides how polished section A needs to be.

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

**Question 2 stalls** most often, and it is the expensive one: a wedge number with no proof
point behind it turns the whole package into confident fiction. **Question 4 stalls** when the
team has only ever researched public companies and the private-company sources for the
vertical were never mapped.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Financial Wedge
- **The number we move:** [metric + defensible range + the proof behind it]
- **Vertical financial signals:** [signal -> where it appears -> what it predicts]
- **Private-company sources:** [source -> coverage -> reliability]
```

---

## About the 24 emails

Twenty-four persona-tailored emails is a ceiling, not a quota. If your motion runs on three
personas, produce three excellent sequences and stop. Volume that outruns your proof points
reads as spray.
