# Customize: Weekly Review

A paste-in prompt that adapts this skill to *your* operation.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my company's operation.

Read the attached SKILL.md (gtm-weekly-review). It is a standing review that runs
every week, measures how your system is changing, and writes a dated record so you can
see the trend.

Your job is NOT to rewrite it. It is to make it fire on the metrics that actually
matter to my operation, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What are the three areas of my operation I care most about tracking week-over-week?
   (Examples: knowledge base / content pipeline, sales pipeline, customer data, 
    system configuration, team capacity, infrastructure health, whatever is real for you)

2. For each area, what are 2-3 concrete metrics I can actually measure every week?
   (Not guesses or feelings, things I can check in git logs, file dates, dashboards,
    or command output)

3. What was the last time something drifted in my operation without me noticing until
   it was expensive to fix? What metric, measured weekly, would have caught it?

4. Of the metrics I measure every week, which ones should I compare to last week's
   numbers? (Some are absolute, like "we shipped 3 articles". Others are relative,
   like "we shipped 2 more than last week".)

5. What would "carried over" mean in my operation? (Things I set out to do last week
   and did not finish. Not all unfinished work counts. Some tasks get overtaken by
   more urgent ones. How do I tell the difference?)

Then produce:

A. A revised frontmatter template where each field matches a metric I actually track.

B. A revised "Quick Reference" table where each row is a metric from MY operation,
   not generic ones.

C. A list of the repo directories or system commands I should check every week,
   with the exact paths or commands.

D. THE HONEST PART: a short list of the questions above I could not answer
   concretely, and what I would need to measure to answer them. If I could not
   define a metric, that gap is the finding, not a reason to skip the question.

Start with question 1.
```

---

## What you should expect to happen

Most operators get through questions 1-2 comfortably and stall on question 3.

That stall is not failure. It is the skill working. **Question 3 is asking you to
remember a specific time you learned too late about something wrong.** That is an
uncomfortable question, and the question exists because that is the exact situation
a weekly review prevents.

If you cannot remember a specific incident, that is valid. Say so. It means either
you have not hit that failure yet, or you have been lucky. A weekly review is
insurance.

---

## Minimum profile fields this skill reads

Add these to your operation's context file once, and every skill that uses this one
inherits them:

```markdown
## Operational Health Metrics

- **Knowledge base location:** [path to where you store notes/KB]
- **Content pipeline:** [where articles/content status lives]
- **Key repositories:** [the 2-3 repos that matter most]
- **System checks:** [the commands that tell you if things are broken]
- **Definition of done:** [what counts as a priority actually being complete]
```

---

## If you change the structure

The weekly record format is a contract with the trend-tracking system that uses it.
Only change field names if you update the code that reads these files. The `date`
and `window` fields are non-negotiable because they key the time series.

Everything else (which metrics you track, how you name them, what you measure) is
fair game. The structure is the rails. The metrics are the cargo.
