# Customize: Meeting Prep

This interview writes the Meeting Prep section of your profile. Once it is saved, every discovery and demo prep reads your team's own vocabulary, your persona-proof map and your demo reframe, instead of generic defaults.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me fill in the profile section that a meeting-prep skill reads. The skill is attached as SKILL.md (gtm-meeting-prep). It builds one prep sheet for a discovery or demo call: the top pain, a question bank for each discovery phase, one proof point per attendee, objection scripts, a minute-by-minute call flow and a follow-up email draft.

Your job is NOT to rewrite the skill. It is to capture how my team actually runs discovery and demos, in our own words, and to tell me honestly where you cannot answer.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which discovery framework does my team run, and what does my team call its stages? Give me the vocabulary reps use on calls. Then ask: do our won calls point to a different talk-time band than the shared bands in the skill? If yes, which band, and from how many won calls?

2. My top three to five pains, as the customer says them. For each one: the sentence a buyer actually said on a real call (or say "none yet"), the phrase we listen for, and the open question that surfaces the pain on a call.

3. Which proof point lands with which persona? Give one per persona, and the status of each one: Verified, Benchmark or Illustrative. A CFO story dies in front of an operations manager, and the reverse is also true.

4. For demo calls: what is the ONE reframe that reliably works in my vertical? The thing the buyer believes that we teach them is wrong, and the evidence for it.

5. It is 1:30 and the call is at 2. What must be on the one page, and what do reps say is always on it that they never use? The second list matters as much as the first.

Then produce:

A. The discovery question for each pain, in my team's words, one per line.

B. Section C: the profile section this skill reads, filled with my answers, in exactly this shape, ready to paste into my profile:

## Meeting Prep
- **Discovery framework and team vocabulary:** ...
- **Persona-proof map:** ...
- **The demo reframe:** ...

C. THE HONEST PART: every question above that you could not answer concretely, and what I would need to gather to answer it. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 2 stalls** when the pains only exist in marketing language. "Operational inefficiency" has never been said by a buyer on a discovery call, so there is no sentence to listen for.

**Question 3 stalls** when the team has no proof for a persona. The skill then says so on the sheet and uses a research target, instead of inventing a story. A stall here is useful: it shows where the team needs its first Verified proof.

**Question 4 stalls** when there is no agreed teach. Every rep improvises a reframe, which is how demos turn into feature tours.

All three point at the same missing thing: a profile that holds what your team knows. Build the section once, and the skill inherits it on every run.

---

## Minimum Profile Fields This Skill Reads

Add this section to your profile once:

```markdown
## Meeting Prep
- **Discovery framework and team vocabulary:** [the public framework, and your own words for its stages]
- **Persona-proof map:** [persona, the proof point that lands, the one that does not]
- **The demo reframe:** [what they believe, what we teach, the evidence]
```

The skill also reads four sections that other interviews or your own edits write. Keep them current:

- **Core Pain Points:** the What to Listen For column and the Discovery question column. A pain with no discovery question gets a question built from its listen-for phrase, marked as inferred.
- **Proof Points:** the Status column (Verified, Benchmark or Illustrative). Only Verified rows can be cited to a prospect.
- **Sales Methodology:** your framework names and any talk-time override. Without an override, the shared bands apply.
- **Qualification Stage Gates:** your stage names, which the skill uses by number and name.

---

## Keep It to One Page

The sheet is read in the two minutes before the call connects. Anything cut from the page should move to the Deal Pulse (08) or Stakeholder Mapping (10) notes, not to a second page. The reason is the reader's time: a second page is not read on the call.
