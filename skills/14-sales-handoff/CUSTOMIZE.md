# Customize: Sales Handoff

A paste-in interview that adapts this skill to your own implementations. It asks one question at a time about your past onboardings, how data moves into your product, and what sets your timing. It ends by writing the Implementation Profile section that the skill reads for the three dates and the readiness scores.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see [`docs/customization.md`](../../docs/customization.md) and [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my company's implementation process.

Read the attached SKILL.md (gtm-sales-handoff). It scores implementation readiness across six dimensions, sets three dates (kickoff, go-live and Full Adoption Date), names the risks with a mitigation for each, and writes the readiness report that the implementation lead plans from.

Your job is NOT to rewrite it. It is to make it fit my implementations, and to tell me honestly where you cannot answer me.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What do your rocky onboardings have in common? Pull the last three. Was it data, a sponsor who disappeared, an unmapped workflow, or a technical surprise?

2. Typical days from kickoff to go-live. Count them from completed deals, from the kickoff date to the day the customer goes live. If you have fewer than three completed deals, say so. The honest answer is RECORD, not a guess.

3. How does data move from the customer's system into our product? A file upload, a scheduled export, or manual entry? Name the standard format.

4. The timing variables, one at a time:
   (a) How many source systems does a typical customer run? For each system beyond the first, how many weeks does it add?
   (b) Is the customer's export format familiar to our team? If it is, how many weeks does that save?
   (c) How many days does IT usually take to name an owner and deliver an export? The skill reads this as days, the same unit as the profile's IT lead time.

5. Full adoption. Is two months from kickoff our default? If not, how many months is ours?

6. Quick wins: what can a customer see working in week one that they will mention to their boss? Every vertical has one. Name ours.

7. Ask the implementation team directly: what does sales never give you that you always need? Their answer is the most important part of the readiness report.

Then produce:

A. A revised "Quick Reference" written in terms of my implementations, not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my team but naming no individual.
C. The section "## Implementation Profile", filled with the exact values I gave you, ready to paste into profiles/client-profile.md.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 1 Stalls** when rocky onboardings never got a post-mortem. The implementation team remembers them as war stories, not as patterns. **Question 2 is where most profiles stop.** A typical duration needs completed deals, and a team with none should leave it as RECORD rather than estimate it. **Question 7 needs the implementation team to be asked directly.** The answer usually arrives quickly, because they have been saying it to each other for a long time.

All three stalls point at the same missing thing: a **context layer**. The skill is a procedure, and a procedure needs to know how your implementations actually run and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once:

```markdown
## Implementation Profile
- **Typical days, kickoff to go-live:** [number of days from completed deals, or RECORD]
- **How data moves:** [file upload, scheduled export or manual entry, and the standard format]
- **Source systems per customer:** [how many, and the weeks each extra system adds]
- **Export format familiarity:** [familiar or new to the team, and the weeks saved when familiar]
- **IT lead time:** [days from request to a named IT owner]
- **Full adoption months:** [2 unless your team differs]
- **Team quick win types:** [any types beyond the four in the skill]
```

---

## Whose Score This Is

The readiness score exists for the customer's implementation. It is not a gate that reps learn to game. If a deal must close with a score of 60, the skill's job is to make the risks explicit and mitigated. It is not to block the close, and it is not to pretend the 60 is an 85.
