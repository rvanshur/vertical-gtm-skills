# Customize: Daily Prospecting

A paste-in interview that adapts the Daily Prospecting skill to your go-to-market motion. It asks what makes an account Hot, how many dials a rep really makes, who must never appear on a BDR's sheet, and which CRM fields are trustworthy enough to tier on. Its output is the Daily Prospecting section of your client profile, which the skill reads on every run.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-daily-prospecting). It builds the morning dial sheet: four tiers (Hot, Warm, New, Recycle), per-account pre-call briefs, openers and call goals, tiered off CRM fields and the profile's Fit Grid and Qualification Zones.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas and my
vertical, and to tell me honestly where you cannot answer me.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What makes an account HOT today in my motion: an inbound signal, a trigger event, or
   engagement in the last 48 hours? Define it in facts a system could check.

2. How many dials does a rep actually make per day? The tier sizes have to match that
   capacity, or the sheet becomes a backlog, not a plan.

3. What are the exclusion rules: active opportunities, accounts owned by an AE,
   do-not-call verticals, opt-outs? Who must never appear on a BDR's sheet?

4. What does my best cold-connect opener sound like, word for word? Not the script.
   What my best rep actually says.

5. Which CRM fields are maintained well enough to tier on, and which are fiction? Tiering
   on a field nobody updates produces a confidently wrong list every morning.

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts, personas and vertical,
   not generic ones.

B. A revised "Examples" section built from the real answers I gave you, recognizable to my
   team but naming no individual.

C. The Daily Prospecting section for profiles/client-profile.md, with the exact values I
   gave you, in the shape shown under "Minimum Profile Fields This Skill Reads", ready to
   paste in.

D. THE HONEST PART: the questions above I could not answer concretely, and what I would
   need to gather to answer them. Do not paper over these. An answer I guessed at is a
   gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 5 stalls** the most and matters the most. Every tiering rule inherits the honesty of the field it reads. If "last activity date" is right for only half the reps, the tier assignments are coin flips with labels on them. Fix the two fields that matter most before customizing anything else.

**Question 1 stalls second.** A Hot definition that a system cannot check is a feeling. Ask for the window in days and the signal in fields. The profile's Hot definition is the one the skill applies first, so a vague answer here moves the whole sheet.

Both stalls point at the same missing thing: a **context layer**. The skill is a procedure. A procedure needs to know who you sell to, what has worked and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. The skill also reads Fit Grid, Qualification Zones, Core Pain Points (with its Discovery question column) and Proof Points from the same file, and those are filled in their own sections of the template.

```markdown
## Daily Prospecting
- **Hot definition:** [checkable facts, not feelings]
- **Daily capacity:** [dials a day, tier size budget]
- **Exclusion rules:** [who never appears on the sheet]
- **Opener, verbatim:** [what the best rep actually says]
- **Trustworthy CRM fields:** [field, trust level, who maintains it]
```

---

## One Page, Four Tiers

The tier count is fixed because a rep triages four buckets before the first coffee and cannot triage six. If two account types compete for Hot, sharpen the Hot definition rather than adding a tier.

The sheet is also meant to be read at a glance. A dial sheet that runs to several pages is read once and then left behind, and the value is in having it open between calls. If the answers to this interview produce a sheet too long to scan, bring that back as a question about the daily capacity answer, not as a silent cut.
