# Customize: Competitive Strategy

A paste-in prompt that adapts this skill to your market. It interviews you one question at a time about your competitors, the patterns you have seen in them, the trends that matter, and the rules that set deadlines, then writes the profile section this skill reads.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my market.

Read the attached SKILL.md (gtm-competitive-strategy). It builds deal-specific competitive strategy for an open opportunity: the incumbent filed under one of the seven incumbent types in its Shared Contract, a gap matrix, a displacement playbook, and a win plan with a battlecard.

Your job is NOT to rewrite it. It is to make it fire on my competitors, my buyers and my market, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which three competitors do you actually face, and in roughly what share of deals? The one you fear and the one you meet are often different companies.

2. For the top one: your last three wins and last three losses against them. What actually decided each? Not the official reason, the real one.

3. Which of your claimed gaps can you PROVE (a customer who switched will say it, a side-by-side shows it), and which are sales-floor folklore?

4. What traps do they set for you? What do prospects repeat back to you that came from them?

5. What proof actually lands in this market: a reference call, a migration story with numbers, a live side-by-side? For each one, has the customer agreed to be named?

6. For each competitor type you face: what did customers say about the product 6 to 12 months after they chose it, who said it, and on what date? Count the cases. Do not call anything a pattern under five cases.

7. Which rules set a deadline in your market (a state or federal rule, a licence renewal, a filing date)? For each one: the rule's name, its citation, and the date you checked it.

Then produce:

A. A revised "Quick Reference" written in terms of MY competitors and buyers, not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my team but naming no individual.
C. The section "## Competitive Patterns and Trends", with the four fields below filled from my answers, ready to paste into profiles/client-profile.md.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 2 stalls** because the win-loss "why" was never captured within a week of the outcome, after which it becomes folklore. **Question 3 is where honesty pays**: most gap matrices are half folklore, and a rep who repeats an unprovable gap to a well-informed buyer loses the room. **Question 6 stalls** when the team has not written down what customers said after the sale. Count what you have, even if it is one case, and label it as one case.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a procedure. A procedure needs to know who you sell to, what has worked, and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. It sits beside the Competitive Landscape section.

```markdown
## Competitive Patterns and Trends
- **Failure patterns:** [pattern | cases counted and source | discovery question]. Fewer than five cases is marked observation.
- **Trends:** [trend | dated source | what it means for the incumbent's customers]. A number appears only with its source named.
- **Proof point status:** [each proof point in Proof Points, marked Verified, Benchmark or Illustrative]. Only Verified rows go into talk tracks.
- **Jurisdiction deadlines:** [rule | citation | date checked], or NONE on file.
```

---

## Evidence Tags on Every Gap-Matrix Row

Each gap-matrix row carries one of the six evidence tags: `[CRM]`, `[Call]`, `[Notes]`, `[Public: source]`, `[Inferred]` or `[Unknown]`. A claim with no tag is removed before it reaches a buyer. The matrix's job is not to make you feel armed. It is to keep a rep from confidently repeating something a prospect can disprove.
