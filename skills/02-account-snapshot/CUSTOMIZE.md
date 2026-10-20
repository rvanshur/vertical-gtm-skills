# Customize: Account Snapshot

A paste-in interview that writes the Outbound Voice section of your profile. It asks one question at a time about your best email, your reliable research sources, the triggers that jump the queue, and the regions where a missed rule costs the most. It then produces that section, filled with your answers, ready to paste.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a sales methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-account-snapshot). It is the BDR daily driver: an account brief with a zone verdict, persona-ranked contacts, tagged pain hypotheses, a three-step email draft and call prep, all on one page.

Your job is NOT to rewrite the skill. It is to make it fire on my accounts, my buyers and my region, and to tell me honestly where I cannot answer you.

Ask me these questions, ONE AT A TIME, and wait for each answer:

1. Paste your best-performing cold email, the one that got real replies. What about it is load-bearing: the trigger, the number, the tone? That becomes the reference email.

2. Which research sources are actually reliable in your vertical: state registries, permit databases, job boards, association directories, local trade press? For each one, what does it reliably tell you, and where does public data run out?

3. Which facts make a rep call an account today rather than sequence it and wait? Name the specific, checkable facts, such as a new owner in a registry, a finding in the press, or an inbound form under 48 hours old.

4. Which states or regions carry the highest cost of a missed rule for your buyers, and what is the rule and its source? Which regions do you not yet know well enough to rank?

5. Which buyer titles are you told to target but have never once converted? Those go in the Buyer Personas section, not here, so keep them separate from your answers.

Then produce:

A. The honest part: the questions above that I could not answer concretely, what I would need to gather to answer them, and which of my answers are guesses. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

B. Any answer that belongs in Buyer Personas rather than Outbound Voice, written as a short list ready to paste into that section.

C. The Outbound Voice section, filled with my answers, in the exact shape below, ready to paste into profiles/client-profile.md. Every research source carries what it reliably tells you. Every region carries its source. Nothing is invented to fill a blank: a blank stays a bracketed placeholder.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 1 stalls** when nobody kept the winning emails. Performance lives in anecdote, not in a swipe file, and the reference email is the single most useful thing the skill can learn.

**Question 2 stalls** when research habits were inherited from a horizontal playbook and nobody has mapped what your vertical exposes publicly. A source with no stated lag is a source the skill cannot weigh.

**Question 4 stalls** when the team ranks regions by feel. The region map only works when each tier names its rule and its source, because the skill ranks accounts by that cost.

All three stalls point at the same missing thing: a context layer. The skill is a procedure, and a procedure needs to know who you sell to, what has worked, and where a missed rule costs the most. That is what the profile is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. The interview above writes it for you.

```markdown
## Outbound Voice
- **Reference email:** [paste the best performer]
- **Vertical research sources:** [source, what it reliably tells you]
- **Call-today triggers:** [the facts that jump the queue]
- **Region map:** [region or state, the cost of a missed rule there, the source]
```

---

## If the One-Pager Grows

The cheatsheet is one page because a BDR reads it between dials. Anything that pushes it to two pages belongs in Research Outbound (03), which is the deep version of this skill.
