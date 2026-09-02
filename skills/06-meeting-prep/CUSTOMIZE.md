# Customize: Meeting Prep

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

Read the attached SKILL.md (gtm-meeting-prep). It builds a one-page call sheet: SPIN-structured discovery or Challenger-structured demo, pain hypotheses, persona-matched proof, and a scripted open and close.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which discovery framework does your team actually run -- SPIN as shipped, or your own
   words for the same moves? Give me the vocabulary your reps use on calls.

2. Your top 5-7 pains AS THE CUSTOMER SAYS THEM -- the sentence a prospect said on a real
   call, not the marketing translation of it. One real quote per pain if you have them.

3. Which proof point lands with which persona? A CFO story dies in front of an ops manager
   and vice versa. Map them.

4. For demo calls: what is the ONE reframe that reliably works in your vertical -- the
   thing the prospect believes that you profitably teach them is wrong?

5. It is 1:30pm and the call is at 2. What must be on the one page, and what do reps say
   is always on it that they never use? The second list is as important as the first.

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

**Question 2 stalls** when pains only exist in marketing language -- "operational
inefficiency" has never been said by a human on a discovery call. **Question 4 stalls** when
there is no agreed teach: every rep improvises their own reframe, which is how demos become
feature tours.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Meeting Prep
- **Discovery framework + team vocabulary:** [SPIN or yours, in your words]
- **Pains, verbatim:** [pain -> the customer's sentence -> listening signal]
- **Persona-proof map:** [persona -> the proof point that lands -> the one that doesn't]
- **The demo reframe:** [what they believe -> what we teach -> the evidence]
```

---

## Keep it to one page

The call sheet is read in the two minutes before the call connects. Anything cut from the
page should move to Deal Pulse (08) or Stakeholder Mapping (10) notes, not to page two.
