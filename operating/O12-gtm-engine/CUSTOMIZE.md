# Customize: Engine

A paste-in prompt that adapts this skill to your team's growth goal, your people and your cost records. It writes the `## Growth System` section of your client profile.

Works in **Claude Code**, **OpenAI Codex**, or as a **ChatGPT custom GPT**. All three read the same `SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The prompt

```
You are helping me adapt a growth system skill to my company's goal, my team and my cost records.

Read the attached SKILL.md (gtm-engine, version 2.0.0). It starts from the launch plan and the
launch results, finds the step that loses the most people, scores the backlog with one Guild
score, designs one loop, writes the narrative and four sequences, and grades every output on
whether it would survive if the main operator went on vacation for two weeks.

Your job is NOT to rewrite the skill. It is to name the people and records we actually have,
write the Growth System section of my profile, and tell me honestly where you cannot answer for us.

Ask me these, ONE AT A TIME, and wait for each answer:

1. In one sentence, what is the growth system for, and which buyer does it serve?

2. What is the growth goal? Give the number, and the two dates it is measured between. If the
   goal is the one Launch used, say so, and I will label it "Launch goal, not profile goal".

3. How many hours per week can the team give to growth work after launch? If you do not know,
   say so. It is recorded as [RECORD] and is never estimated. The vacation test cannot pass
   until it is recorded.

4. Which measure is the growth measure, the one number the team is judged on? If there is none
   yet, say so. Engine then uses Launch's funnel goal and marks the owner [RECORD].

5. For each measure on the Metrics board, who is the one named owner? A row with no owner is
   reported as NOT ASSIGNED, and the vacation test fails for it.

6. For each owner in question 5, who is the named backup, the person who could run the same
   task for two weeks? "None" is a valid answer. It is the honest default, and it makes the
   vacation test read NOT YET.

7. Which cost records do we have: gross margin, acquisition cost per won customer, and how
   many months a customer stays? A missing record is reported as "not run on real data". Do not
   give a benchmark in its place. Missing cost inputs rank at the top of the backlog.

8. Who approves the backlog ranking and the owner list before anything is written to the
   knowledge base? This must be the owner named in your profile's `## Launch Plan` section.

9. Do you accept the four sequences as they are: Start on day 0, Story on day 3, Invitation on
   day 7, and Keep Going monthly after day 7? Each sequence needs one owner and one stop rule.
   Name them, or say which are blank.

10. Who reviews each sprint's results at the close of the two-week sprint?

Then produce:

A. The input record: one line per field, each marked present, missing, or [RECORD].

B. A draft backlog: the cost inputs first, then each candidate item with its claim ID or
   "new claim". Show Impact, Unknown, Effort and Score for each, and label every score a judgement.

C. The owner and backup table for the Metrics board, with the vacation test result each output
   would earn today.

D. THE HONEST PART: a short list of the questions above that you could not answer concretely,
   and which parts of the growth system therefore stay as NOT RUN, NOT YET or FAIL. If the cost
   records are missing, the economics are "not run on real data", and that is the finding. Say so.

Start with question 1.
```

---

## What you should expect to happen

Questions 1, 2 and 8 usually land quickly, because most teams know what the system is for, the goal, and who approves. Question 3 is where teams stall, because team time is rarely written down. Record it as [RECORD]. Engine will not invent an hours figure.

Question 6 is the one that decides the vacation test. Most teams name an owner for each measure and no backup. That is the correct result. It reads NOT YET, and the fix is a named person, not a placeholder.

Question 7 is the one most likely to produce "not run on real data". The plan then sets a limit on paid spend, and the cost inputs go to the top of the backlog. That is the correct result.

Question 9 keeps the four sequences on their timings. Their names and their stop rules are the parts a team can change.

---

## The Growth System section to write

After the interview, Engine writes this section into `profiles/client-profile.md`. It is written only after the approval in question 8 is recorded in the brief. Replace each bracketed value with the answer from the interview. Leave [RECORD] wherever the answer is not known.

```markdown
## Growth System

- **Growth goal and window:** [the number and the two dates, or "Launch goal, not profile goal" with the Launch figure]
- **Team time for growth work:** [hours per week, or "[RECORD]" until it is known]
- **Growth measure:** [the one measure, with its owner. "[RECORD] after the first Engine run" if none is named yet]
- **Current bottleneck:** [the stage that loses the most people, with its rate and n. "not run" in a plan-only run]
- **Sprint cadence:** [two weeks, reviewed by the name from question 10]
- **Narrative:** [one sentence, with the grade of each claim it uses]
```

The approver in question 8 is not written here. It stays in your profile's `## Launch Plan` section, where Engine reads it.

---

## Minimum profile fields this skill reads

Engine reads these sections of `profiles/client-profile.md`, in this order. It writes only to its own `## Growth System` section, and only after approval.

- `## Growth System`: read first. Growth goal and window, Team time for growth work, Growth measure, Current bottleneck, Sprint cadence and Narrative.
- `## Launch Plan`: the owner of the launch decision, who approves write-back. Written by the `gtm-launch` skill.
- `## Company`, `## ICP Definitions`, `## Buyer Personas` and `## Proof Points`: read as context only.

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| Every economics threshold reads "not run on real data" | The cost records are missing | Supply the records and re-run. Do not enter a benchmark and report the result as a finding |
| The team time field is blank | No one has measured the hours | Leave it as [RECORD]. The cadence cannot pass the vacation test until it is recorded |
| A Metrics board row has no owner | No one has been named for it | Report it as NOT ASSIGNED. The vacation test fails for that row until it is named |
| An owner has no backup | No one has been named as the backup | The output reads NOT YET. Name the backup, do not put the owner's name in twice |
| The profile has no `## Launch Plan` section | The launch skill was not run on this profile | Write-back cannot name an approver. Run plan mode only, until the owner is named |
| The growth goal cannot be met in the window | The sales cycle is longer than the window, and the pipeline is empty | Say so in the output. Do not lower the goal or shorten the cycle to fit |
| The team wants a verdict on a candidate archetype | The archetype is still a candidate | Keep the label. No archetype verdict until the test is complete |
| The output runs past two pages | The full run was written into the brief | Ask for the two-page brief only. The nodes hold the detail, and the brief links to them |
