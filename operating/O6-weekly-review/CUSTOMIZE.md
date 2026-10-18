# Customize: Weekly Review

A paste-in prompt that adapts this skill to where your records live, which areas your team uses, and which measures you can actually check.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me adapt a weekly review skill to my records, my areas and the measures I can actually check.

Read the attached SKILL.md (gtm-weekly-review, version 2.0.0). It grades last week's
priorities from evidence, measures what it can check, writes null for anything it did
not check, and writes one dated record that is never edited.

Your job is NOT to rewrite the skill. It is to fit its rules to my setup, name the
places my records actually live, and tell me honestly which measures I cannot check.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where do dated weekly records live? Give a folder name relative to the project,
   never a full machine path. "None yet" is a valid answer. If the folder does not
   exist, the first run creates it, after I approve.

2. Which day is the review, and what is my local calendar day? The skill never uses
   the UTC date, so tell me the time zone if it is not obvious.

3. Which areas does the team use? The four areas are knowledge, content, operations
   and client work. Name the ones in use. An area we do not use is left out of Next
   Week, and it is not filled with a placeholder.

4. Which measures can we check? Go through each one and answer yes, with where it
   lives, or no:
   - Graph Health report (where it is kept)
   - Dream log (where it is kept)
   - Ingest count of items written in the week
   - Items with an expiry date due within three days
   - The team's list of work in progress and work blocked (which list)
   - Repositories with uncommitted work
   - Dashboards not refreshed in over 30 days
   - Skills whose frontmatter misses a required field
   - Published counts rechecked against their source

5. Which frontmatter fields does our skill standard require? If we do not have a
   standard, use the fields in the SKILL.md frontmatter and say so.

6. Who reads the record? Name each reader by role. Use names only for me.

7. Do you accept the defaults? They are: carried over of 0 or 1 is Fine, 2 is Watch,
   3 or more is Problem. Tag sprawl is Healthy under 20%, Warning from 20 to 40, and
   Unhealthy over 40. Next Week holds at most one priority per area. If you do not
   accept one, name yours and say why.

Then produce:

A. A record plan: the folder, the review day, the areas in use and the file name
   pattern (YYYY-MM-DD.md).

B. A measure table: each measure marked available with its source, or null from now
   on with the reason.

C. The measures we cannot check, ranked by how much each one would change next week's
   decisions.

D. THE HONEST PART: the questions you could not answer concretely, and which parts of
   the record will stay null until we set them up.

Start with question 1.
```

---

## What You Should Expect

Question 4 is where most teams learn what they cannot check. A null row is the correct result, not a gap to fill with a guessed number. A team with no Dream log, for example, will see the content count stay null until someone runs Dream and keeps the log somewhere the review can read.

Question 3 usually lands quickly, because most teams know which areas they are working on. An area with no priority this week is also a valid result. It is written in words, and it is not left blank.

Question 7 is where the defaults get questioned. Change one only when you have a reason. A team with very few items may find that a tag band misleads, and a changed band must say what it replaces and why.

---

## Weekly Review Section for the Profile

Add this section to `profiles/client-profile.md` once. The skill reads it at the start of every run. It writes nothing back to this section, because the record itself is the output.

```markdown
## Weekly Review

- **Record folder:** [folder name, relative to the project, or "none yet"]
- **Review day:** [day of the week, and the local time zone]
- **Areas in use:** [knowledge, content, operations, client work: list the ones in use]
- **Graph Health report:** [where it is kept, or "not run"]
- **Dream log:** [where it is kept, or "not run"]
- **Measures we can check:** [each measure, with its source]
- **Measures we cannot check:** [each measure, which stays null, with the reason]
- **Required frontmatter fields:** [the fields the operations check looks for]
- **Readers of the record:** [readers, by role]
- **Accepted defaults:** [yes, or each change with its reason]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| Every operations measure reads null | No operations checks were set up | Keep them null, with the reason. Set up one check at a time, starting with the one the team would miss most |
| The record folder does not exist | This is the first run | Create the folder after the owner approves. Do not create it silently |
| The review keeps listing the same orphan notes | The fix was never assigned | Add a named next step for the notes, by role, so the item has an owner and a check |
| Next Week fills an area the team does not use | The areas list is out of date | Update the Areas in use line in the profile, then re-run the plan |
| The readers list has a name where a role belongs | The record may be shared | Replace the name with the role. Keep the name only in a record that stays private to the owner |
| A measure is marked available but the source cannot be opened | The source moved | Change the line to null, with the reason, until the source is back in place |
