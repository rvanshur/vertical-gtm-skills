# Customize: Verify

A paste-in prompt that adapts this skill to *your* go-to-market motion.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-verify). It defines a four-tier evidence ladder (exists,
substantive, wired, works) that blocks completion claims until the top tier is demonstrated.

Your job is NOT to rewrite it. It is to make it fire on the things that actually go out the
door at my company, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What are the three artifacts my team most often calls "done" that reach someone outside
   the team? (a proposal, a dashboard, a data export, a sequence, a QBR deck, a scraped
   record set, whatever is real for us)

2. For each one, what would "tier 4, I ran it end to end just now" actually look like?
   What is the concrete act of demonstration?

3. Which of those artifacts reach a customer, an executive, or a regulator? Those cannot
   pass below tier 4.

4. What is our equivalent of a mechanical gate, a check the SYSTEM runs, not one a person
   chooses? (CI, a validation script, an approval step, a QA pass, a peer review) If we have
   none for a given artifact, say so plainly rather than inventing one.

5. What has actually gone out wrong in the last year, and which tier was it really at when
   someone called it done?

Then produce:

A. A revised "Quick Reference" table where each tier is written in terms of MY artifacts,
   not generic ones.
B. A revised "Examples" section using MY failure from question 5, written so it is
   recognizable to my team but names no individual.
C. A list of the fields this skill now needs from profiles/client-profile.md, with the exact
   values I gave you.
D. THE HONEST PART: a short list of the questions above I could not answer concretely, and
   what intelligence I would need to gather to answer them. Do not paper over these. If I
   could not tell you what tier 4 looks like for an artifact, that gap is the finding.

Start with question 1.
```

---

## What you should expect to happen

Most operators get through questions 1 to 3 comfortably and stall somewhere in 4 or 5.

That is not a failure of the exercise. It is the exercise working.

**Question 4 stalls** when there is no mechanical gate, when "done" is decided by whoever is
looking, differently each time. **Question 5 stalls** when the failures are remembered as
personalities rather than as tiers, so there is no record to reason from.

Both stalls point at the same missing thing: a **context layer**. The skill is a procedure. A
procedure needs to know what your business ships, to whom, and what has already gone wrong.
Without that, you get a generic gate that fires on nothing in particular.

If output section D comes back long, that is worth a conversation rather than a rewrite. Bring
it to the community discussion, it is the most common place this suite stops being useful, and
the fix is almost never a better prompt.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once, and every skill in the suite inherits them:

```markdown
## Verification

- **Mechanical gates:** [the commands or steps the system runs, per artifact type]
- **Customer-facing artifacts:** [the list that cannot pass below tier 4]
- **Definition of done:** [what the team has already agreed shipped means]
- **Known failure modes:** [what has gone out wrong, described by tier not by person]
```

---

## If you change the ladder itself

Don't, at first. The four tiers are ordered so each one is cheap to check and the expensive
check comes last. Reordering them means running the costly demonstration on work that fails a
free check.

The tier *names* are worth localizing. If your team already says "smoke-tested" or "in prod
and confirmed," use your words. Adoption follows vocabulary.
