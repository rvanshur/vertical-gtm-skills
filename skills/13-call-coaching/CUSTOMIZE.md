# Customize: Call Coaching

A paste-in prompt that adapts this skill to your own sales calls. The interview asks about your category names, your demo elements, your pacing and your listen-for phrases, one question at a time, and ends by writing the Call Coaching section that the skill reads from your client profile.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a sales call coaching skill to my team's calls.

Read the attached SKILL.md (gtm-call-coaching). It grades a discovery call across 7 categories (out of 35) and a demo across 8 categories (out of 40), with a pacing check for demos and coaching points that each carry a quote or an evidence grade.

Your job is NOT to rewrite it. It is to tell me which of its defaults my team needs to change, and to tell me honestly where you cannot answer.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Discovery categories. The defaults are Pre-Call Preparation, SPIN Discovery Quality, Priority Ladder Execution, Active Listening, Value Articulation, Next Steps and Momentum, and Alternatives. Does your team call them something else? Give me your names in order, or say "defaults".

2. Demo categories. The defaults are Meeting Opening, Meeting Closing, Teach and Tailor, Pain Alignment and Proof, Question the Problem, Pain-to-Workflow Mapping, Prospect Engagement, and Resistance Handling. Give me your names in order, or say "defaults".

3. Demo elements. The defaults are Introduction, Problem Restatement, Solution, Return on Investment, and Next Steps, with questions running through the solution. Does your team name them differently? Give me your names, or say "defaults".

4. Pacing. The starting defaults are 5% to 10% for introduction, problem restatement and next steps, 40% to 50% for the solution, 15% to 20% for return on investment and for questions. Do your won calls show something different? Give me your shares for each element, or say "starting defaults". If you do not know, say so. A guessed share is a gap.

5. Listen-for phrases. The skill reads the "What to Listen For" column of your Core Pain Points. Name any phrase your buyers use on calls that is not in that column, and the pain it points to.

6. Calibration. Point me at one call you consider an A and one a C. What separates them, in your words? Answer roughly if you have to. Two calibration calls beat zero.

Then produce section C: the "## Call Coaching" section, filled with my answers, in exactly this shape, ready to paste into profiles/client-profile.md:

## Call Coaching
- **Discovery category names:** [my names in order, or "defaults"]
- **Demo category names:** [my names in order, or "defaults"]
- **Demo element names:** [my names, or "defaults"]
- **Pacing overrides:** [my shares for each element, or "starting defaults"]
- **Extra listen-for phrases:** [phrase, the pain it points to, one per line, or "none"]

Then list D: THE HONEST PART. Each question I could not answer concretely, and what I would need to gather to answer it. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 4 stalls** when nobody has measured what a won call looks like on talk time. The starting shares are a calibration point, not a verdict. Keep them until ten won calls give you your own.

**Question 6 stalls** when nobody has agreed what an A call sounds like. Every manager grades from taste, which is the inconsistency this skill removes. Answer it even roughly.

Both stalls point at the same missing thing: a profile. The skill is a procedure. It needs to know which phrases your buyers use, how your team names its categories and what your won calls look like. That is what `profiles/client-profile.md` is for. Build it once and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add these to `profiles/client-profile.md` once:

```markdown
## Call Coaching
- **Discovery category names:** [your names in order, or "defaults"]
- **Demo category names:** [your names in order, or "defaults"]
- **Demo element names:** [your names, or "defaults"]
- **Pacing overrides:** [your shares for each element, or "starting defaults"]
- **Extra listen-for phrases:** [phrase, the pain it points to, one per line, or "none"]
```

---

## Keep Scores Diagnostic

The moment scores touch compensation or stack rankings, calls get performed for the grader and the signal dies. Grade to coach. If leadership wants a number, give them the team trend, never the per-call score.
