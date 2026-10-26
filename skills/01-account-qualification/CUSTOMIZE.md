# Customize: Account Qualification

A paste-in interview that writes your Fit Grid into the client profile. The skill reads that grid to decide whether an account fits your market, so every run scores accounts the same way for your business.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

For the suite-wide setup, see [`docs/customization.md`](../../docs/customization.md) and [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me set up the Account Qualification skill (gtm-account-qualification) for my go-to-market motion.

Read the attached SKILL.md. It scores an account against 8 weighted criteria and five qualification zones, and returns GREENLIGHT, MANUAL REVIEW or DISQUALIFY. Your job is not to rewrite it. Your job is to tell it what fit looks like in my market, and to tell me honestly where you cannot answer.

Ask me these questions ONE AT A TIME, and wait for each answer before you ask the next.

1. Describe your last 10 closed-won customers. What did they have in common BEFORE the first call: size band, sub-market, systems in place, a trigger event? Those traits are your real criteria, whatever the ICP slide says.

2. Name three deals your team worked that it never should have. What single fact, knowable on day one, would have disqualified each one?

3. Which of your criteria can be seen from the outside (website, filings, job posts)? Those belong in this skill. The rest belong in meeting prep.

4. Which one criterion, when it is wrong, kills the deal no matter how good the rest look? Which two barely matter, but everyone argues about them?

5. Where is your manual-review band: the score range where you still want a person to look at the account before a rep spends a morning on it?

Then produce, in this order:

A. Which of the eight criteria your answers change, and how each one should read for my accounts.

B. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

C. The Fit Grid section, in the exact shape below, filled with my answers. Every cell must be something a rep can see from the outside or in the CRM. Include the revenue estimation values from my own history, and leave blank any value I do not have. Never invent one. Ready to paste into profiles/client-profile.md.

Start with question 1.
```

---

## What You Should Expect To Happen

Most operators answer question 1 from memory and stall on questions 2 and 4. **Question 2 stalls** when there is no loss record to reason from, because bad-fit deals get remembered as bad luck. **Question 4 stalls** when the ICP was written by consensus, so every criterion weighs the same and none of them decide anything.

Both stalls point at the same missing thing: a context layer. The skill is a procedure, and a procedure needs to know who you sell to, what has worked and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md`. The zones and the Verdict Rule go in the Qualification Zones section, which the template already has.

```markdown
## Fit Grid
| ICP | Strong | Moderate | Weak |
|---|---|---|---|
| ICP1 | [observable facts] | [observable facts] | [observable facts] |
| ICP2 | [observable facts] | [observable facts] | [observable facts] |
- **Revenue estimation values:** [per employee, per site or branch, per unit, as your own history gives them]
```

A cell left in brackets means the fact is unknown. An unknown fact makes the criterion UNKNOWN, not WEAK, so leave a cell blank rather than guessing at it.

---

## If You Want To Add A Ninth Criterion

Don't. Eight weighted criteria is already at the edge of what a scorer can keep honest, and every added criterion dilutes the weights of the ones that decide. If a new fact matters, ask which existing criterion it is evidence for, and fold it in there.
