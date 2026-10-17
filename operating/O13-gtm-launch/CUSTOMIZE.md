# Customize: Launch

A paste-in prompt that adapts this skill to your team's launch rules, people and cost records.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**. All three read the same `SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The prompt

```
You are helping me adapt a launch skill to my company's launch rules, war room and cost records.

Read the attached SKILL.md (gtm-launch, version 2.0.0). It starts from the position that
Positioning handed over, refuses to launch a position that failed its test, scores five
motions and lets one or two of them lead, caps every unproven channel at 30% of the budget
with a 30-day kill rule, stacks proof by its real tier, and writes a plan that Engine
measures against.

Your job is NOT to rewrite the skill. It is to fit its rules to my team, name the people
and records we actually have, point the first plan at the launch we are really planning,
and tell me honestly where you cannot answer for us.

Ask me these, ONE AT A TIME, and wait for each answer:

1. In one sentence, what are we launching, and to which buyer? (This becomes the "What is
   launching" field.)

2. Which Customer archetype did Discovery name, and is it a candidate or confirmed? If
   Discovery has not run, say so, because Launch cannot choose a motion without it.

3. What is the revenue goal? Give the number, and the two dates it is measured between.

4. What launch budget, in dollars, and which people are committed? List them separately
   from what we hope for. Hoped-for resources become risks in the plan, not inputs. An
   uncommitted budget is recorded as [RECORD before launch], never estimated.

5. Who fills each war room role: Commander, Customer Response, Technical Monitor, Social
   Monitor, and Content and Comms? Give a name for each one, or say which are blank. A
   blank role fails the plan, and the plan will say so.

6. Which customers have written permission to be named in launch copy, and where is that
   permission recorded? "None" is a valid answer, and it is the honest default.

7. Which cost records do we have: gross margin, acquisition cost per won customer, and how
   many months a customer stays? A missing record is reported as "not run on real data".
   Do not give a benchmark in its place.

8. Do you accept the defaults? They are a 30% cap on any unproven channel, a 30-day kill
   rule, a five-contact volume check, and a reserve for budget no channel has earned. If you
   do not accept one, name yours and say why.

9. Who approves the motion decision and the channel caps before anything is written to the
   knowledge base?

10. Who is the launch day owner, and is the launch day date set? If the date is not set, the
    content plan uses offsets from launch day until it is.

Then produce:

A. A launch input record: one line per field, each marked present, missing or not run on real data.

B. A draft motion frame: the Customer archetype and its confidence, then the five motions
   with a proposed score for each of the four criteria. Mark every score as a judgement.

C. The cost inputs we are missing, ranked by how much each one would change the payback
   result.

D. THE HONEST PART: a short list of the questions above that you could not answer concretely,
   and which parts of the plan therefore stay as experiments. If the cost records are missing,
   the economics are "not run on real data", and that is the finding. Say so.

Start with question 1.
```

---

## What you should expect to happen

Questions 1, 3 and 9 usually land quickly, because most teams know what they are launching, their revenue goal and who signs off. Question 5 is where teams stall, because the war room names are often a hope rather than a decision. A blank role is the correct result, not a gap to fill with a placeholder name.

Question 7 is the one most likely to produce "not run on real data". Acquisition cost and retention are rarely written down. The plan will then run as capped experiments, and no channel will scale spend until the records exist. That is the correct result.

Question 4 usually produces the first [RECORD before launch] marker. The plan writes the launch budget and launch date into Part A only once they are committed. Part B, the results, is written at the day-30 review and stays empty until then.

Question 6 often comes back "none". Until a customer gives written permission, the proof stack has no named customer, and the launch leads with its strongest real tier, labelled as it is.

---

## Minimum profile fields this skill reads

Add this section to `profiles/client-profile.md` once. The skill reads the existing Company, Buyer Personas, Competitive Landscape and Proof Points sections. It also reads the `## Positioning` section that the Positioning skill writes. It writes back to its own `## Launch Plan` section after approval.

```markdown
## Launch Plan

- **Knowledge base path:** [folder where Launch nodes are written, or "none yet"]
- **Owner of the launch decision:** [the person who approves the motion decision and the channel caps before any write]
- **What is launching:** [one sentence, from question 1]
- **Motion:** [the lead motions, the experiment and the deferred motions, written after the Stage 3 score]
- **Revenue goal and window:** [the number, and the two dates it is measured between]
- **Launch day owner:** [the person who makes the launch-day calls]
- **Launch day date:** [date, or "[RECORD before launch]" until it is committed]
- **Launch budget (dollars):** [the committed launch budget in dollars, split by channel and reserve, or "[RECORD before launch]" until committed]
- **Day 30 review date:** [set from the launch day date, or "[RECORD before launch]"]
- **Unproven channel cap:** [default: 30% of budget. Change only with a reason]
- **Kill rule:** [default: 30 days from start with no signal. Change only with a reason]
- **Volume check:** [default: five contacts at the kill date]
- **Reserve:** [default: budget no channel has earned is held in reserve]
- **War room:** [five names: Commander, Customer Response, Technical Monitor, Social Monitor, Content and Comms. Blank roles stay blank]
- **Permission records:** [named customers with a recorded permission, and where the permission is kept. "None" is valid]
- **Cost records:** [gross margin, acquisition cost per won customer, months a customer stays. Missing items stay missing]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| Every economics threshold reads "not run on real data" | The cost records are missing | Supply the records and re-run. Do not enter a benchmark and report the result as a finding |
| The launch budget or launch date is not known | Neither has been committed | Mark the field "[RECORD before launch]". Do not estimate either one |
| The war room has a blank role | No one has been named for it | Leave the role blank. The plan fails the quality bar until it is named |
| The revenue goal cannot be met in the window | The sales cycle is longer than the window, and the pipeline is empty | Say so in the plan. Do not lower the goal or shorten the cycle to fit |
| A customer is named in launch copy with no permission | Permission was never recorded, or was withdrawn | Remove the name, grade the proof as assumed, and re-run once the permission is recorded |
| The archetype is a candidate, and the team wants a verdict | The beliefs or the ten-deal test are not complete | Keep the label. No verdict until the test is complete |
| The plan says the launch day date is not set | The date is not committed | Use offsets from launch day in the content plan, and set calendar dates when the date is committed |
| The plan runs past two pages | The full plan was written into the brief | Ask for the two-page brief only. The nodes hold the detail, and the brief links to them |
