# Customize: Sales-to-CS Handoff

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

Read the attached SKILL.md (gtm-sales-handoff). It scores implementation readiness across 6 dimensions, builds a 3-date handoff plan, flags risks with mitigations, and generates a readiness card for the CS team.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What do your implementation failures have in common? Pull the last three rocky
   onboardings -- was it data, a vanished sponsor, an unmapped workflow, a technical
   surprise?

2. Map the six dimensions (stakeholder, workflow, technical, data, resource, change
   management) to the real steps of YOUR onboarding. Which dimension is chronically the
   weak one?

3. The three dates: what are your real milestones -- kickoff, go-live, first value? How
   long does each gap honestly run for a typical deal?

4. Ask your CS team directly: what does sales never give you that you always need? Their
   answer is the readiness card's most important section.

5. Quick wins: what can a customer see working in week one that they will mention to
   their boss? Every vertical has one; name yours.

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

**Question 1 stalls** when rocky onboardings never got a post-mortem -- CS remembers them as
war stories, not patterns. **Question 4 requires actually asking CS**, and the answer usually
arrives in under five minutes because they have been saying it to each other for years.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Handoff
- **Failure patterns:** [what the rocky onboardings shared]
- **Milestones:** [kickoff -> go-live -> first value, with honest durations]
- **CS must-haves:** [what CS says sales never provides]
- **Quick-win catalog:** [week-one visible value, per segment]
```

---

## Whose score this is

The readiness score exists for the customer's onboarding, not as a gate reps learn to game.
If a deal must close mid-quarter at a 60, the skill's job is to make the risks explicit and
mitigated -- not to block the close, and not to pretend the 60 is an 85.
