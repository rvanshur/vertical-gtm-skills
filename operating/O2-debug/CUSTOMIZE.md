# Customize: Debug

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

Read the attached SKILL.md (gtm-debug). It enforces a hypothesis-first discipline and a
circuit breaker: after three failed hypotheses, stop, write a handoff, and re-plan.

Your job is NOT to rewrite it. It is to make it fire on the bugs your team actually fixes,
and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What does a debug session usually look like? (Pick the most common: trial and error, lots
   of logs added, code reading, asking teammates, something else)

2. How often does somebody spend more than an hour on one bug without finding the root cause?

3. What was the last bug that took longer to debug than the fix took to implement? (What was
   it, and what finally found it?)

4. If you had to write down the root cause in one sentence, could you? Or does it usually
   come out as "somewhere in the data layer" and require a follow-up question?

5. How do we know a debug session is over? (Did we ship the fix? Did we have a postmortem?
   Did we move on and hope it does not happen again?)

Then produce:

A. A revised "Core Workflow" where each step is written against MY environment and tools,
   not generic ones. ("Logs" looks different in production than in local. "Test" looks
   different in a compiled language than interpreted.)

B. A revised "Best Practices" using MY time-sink from question 3, written so it is
   recognizable to my team but names no individual.

C. A map of your debugging tools and how to use them: what logs go where, what test
   infrastructure is available, what "runtime inspection" means in your stack.

D. THE HONEST PART: a short list of the questions above I could not answer concretely.
   If debug sessions usually end with "we moved on," that gap is the finding. If you cannot
   write the root cause in one sentence, the discipline is not the problem. The evidence
   gathering is. If we have not got the tools or infrastructure to prove a hypothesis, that
   is a blocker this skill cannot fix alone.

Start with question 1.
```

---

## What you should expect to happen

Questions 1 and 2 usually land. Question 3 gets you gold. Question 4 stalls when the root
cause was never actually found, just a fix that seemed to work. Question 5 stalls when
debugging is informal and nothing gets closed.

If output section D is long, the work might not be in the skill. It might be in the
infrastructure. If you cannot reproduce the bug reliably, you cannot test a hypothesis. If
you cannot see logs, you cannot gather evidence. This skill assumes you have (or can build)
the basics: reproducibility, visibility, and a hypothesis you can write down.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once, and every skill in the suite inherits them:

```markdown
## Debugging

- **Bug reproduction:** [how we reproduce bugs: manual steps, test case, CI failure, other]
- **Log visibility:** [where logs live: local, CI, production, monitoring tool]
- **Hypothesis proof:** [how we confirm a hypothesis: test that fails on unfixed code, instrumentation, other]
- **Handoff process:** [where unresolved bugs go and how they get escalated]
- **Known time sinks:** [the class of bugs that usually take longest to debug]
```
