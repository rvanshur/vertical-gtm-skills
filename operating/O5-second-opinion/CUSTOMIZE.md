# Customize: Second Opinion

A paste-in prompt that adapts this skill to your go-to-market motion.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-second-opinion). It sends work to a model from a different
vendor for review, trading the builder's blind spots for a different set.

Your job is NOT to rewrite it. It is to make it fire on the things that actually go out the
door at my company, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What kind of work do we send out for review? (code diffs, copy, designs, strategy docs,
   proposals, whatever is real for us)

2. Who does the review today? (another team member, me, a fresh read the next day, external
   consultant, other model, nothing)

3. How often do we miss something the reviewer catches? (ballpark: almost never, maybe once
   a month, weekly, more than once a week)

4. Which vendor builds most of our work, and which OTHER vendor can we actually reach today?
   (a chat app like ChatGPT or Gemini we can paste into, another vendor's CLI installed on
   this machine, or an API key we could script against)

5. Have we ever shipped something that a second set of eyes would have caught? What was it?

Then produce:

A. A revised "Core Workflow" where each step is written in terms of MY artifact types and
   review process, not generic ones.

B. A revised "Best Practices" using MY failure from question 5, written so it is recognizable
   to my team but names no individual.

C. A filled-in review packet (the block in Step 2 of SKILL.md) for our most common artifact,
   plus which of the three routes we will use (paste, CLI or API) and why.

D. THE HONEST PART: a short list of the questions above I could not answer concretely, and
   what would need to happen to answer them. Do not paper over these. If we do not have a
   second-opinion process today, that gap is the finding.

Start with question 1.
```

---

## What you should expect to happen

Most teams have a review process today (even if it is just "reread tomorrow"), so questions
1 and 2 land easily. Question 3 stalls when nobody tracks what the second set of eyes actually
catches. Question 5 stalls when failures get remembered by person ("Dev X always misses
validation edge cases") instead of by pattern ("edge case in validation, caught in PR").

If output section D comes back long, that is worth a conversation. A team without a
second-opinion discipline is betting that the builder is never the one to miss their own
blind spot, which is the bet this skill is built to refuse.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once, and every skill in the suite inherits them:

```markdown
## Review Process

- **Builder vendor:** [the model provider that builds most of our work]
- **Second vendor and route:** [a different provider, and how we reach it: paste into its chat, its CLI, or an API call]
- **What we have missed:** [one incident where a second opinion would have caught something]
- **Review triggers:** [which artifacts get reviewed, and when]
```
