# Customize: Dream

A paste-in prompt that sets up the `## Dream` section of your client profile. It asks about your knowledge base, who approves removals, and where the dream log lives, so the skill knows what it may touch before it touches anything.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up the Dream section of my client profile.

Read the attached SKILL.md (gtm-dream, version 2.0.0). Dream prunes one knowledge base.
It confirms every stale, expired, dead, duplicate or contradicted item, fixes only what
can be fixed without losing words, and asks before any removal. It never deletes a file.

Your job is NOT to rewrite the skill. It is to record my choices, name the places I
have, and tell me honestly what the skill cannot check in my setup.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where do the knowledge base items live? Give a folder or a link.

2. Which mode should be the default?
   - gentle: report only, nothing is written
   - standard: fixes that cannot lose words run, and every removal waits for my yes
   - deep: standard, plus restructuring proposals in the report
   Recommended: standard.

3. How often should Dream run? The default is every 14 days, and also whenever the
   Graph Health structure score is Fair or Poor. Accept it or name a different cadence.

4. Who approves removals, archives and merges? Give one named person. If no one is
   named, the skill can report but cannot remove anything, and it will say so.

5. Where does the dream log live? Give a file or page, or answer "text only" if you
   do not want a saved log. Without a saved log, the trend line cannot start.

6. Does the system record when each item was last used? Answer yes (and name the
   record), no, or unsure. If yes, an item used often is never archived for age alone.
   If no, that rule is skipped and the report says so.

7. Is there an instructions file that holds rules the items might restate? If yes,
   give its location. If no, answer "none", and the restated-rule check is reported
   as null.

Then produce:

A. The Dream section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect of
   that on a run.

C. THE HONEST PART. A short list of what this setup cannot check. For example: no
   Graph Health report yet (so the structure score is null), no use record (so the
   use rule is skipped), or no saved log (so the trend starts nowhere).

Start with question 1.
```

---

## What You Should Expect

Questions 1 and 4 usually land first, because most teams know where their notes live and who can say yes to a removal. Question 4 matters most. With no approver named, the skill reports and proposes, and it removes nothing.

Question 5 is where teams stall, because a saved log means a place to keep it. "Text only" is a valid answer. The skill then prints the log entry in each report, and it does not reset the cadence until a log is saved.

Question 6 often comes back "unsure". Answer it honestly. The skill will not guess use from file dates, and an unrecorded use rule is simply skipped.

---

## The Dream Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its settings. It writes back the last run date and the next run date after each saved log.

```markdown
## Dream

- **Knowledge base location:** [folder or link to the items, or "not set"]
- **Default mode:** [gentle, standard or deep. Default: standard]
- **Cadence:** [every 14 days, and whenever the Graph Health structure score is Fair or Poor. Change only with a reason]
- **Approver for removals:** [one named person. "Not set" means no removal is applied]
- **Dream log location:** [file or page, or "text only, no saved log"]
- **Use recorded:** [yes, with the record named / no / unsure]
- **Instructions file:** [location, or "none"]
- **Last run date:** [date of the last saved log, or "none yet"]
- **Next run date:** [last run date plus 14 days, or "due now"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill says it cannot remove anything | No approver is named in the profile | Name one person in the Approver field. Until then, the skill reports and proposes only |
| The structure score reads null | No Graph Health report exists yet | Run Graph Health on the base first, then run Dream |
| The skill says the run is not due | The next run date is in the future, and the score is above Fair | Accept that, or run `gentle` mode to look without writing |
| The trend line has no history | No dream log was saved before | Choose a log location in question 5, and save this run's log there |
| The use rule is skipped | Use is not recorded, or the answer was "unsure" | Name the record in question 6 if one exists. Otherwise the rule stays off, and the report says so |
| The field check shows "not set" for the location | Question 1 was not answered | Give the folder or link. The skill will not scan a place it was not told about |
