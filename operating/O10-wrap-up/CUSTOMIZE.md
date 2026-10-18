# Customize: Wrap-Up

A paste-in prompt that adapts this skill to your project folders, your notes location and the checks your work needs.

Works in **Claude Code**, in **Codex**, and in **ChatGPT as a custom GPT**. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. It writes the `## Wrap-Up` section of `profiles/client-profile.md`. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up the session-close skill for my projects.

Read the attached SKILL.md (gtm-wrap-up, version 2.0.0). It closes a working session in writing:
a debrief, a project key taken from the files that changed, only the checks the work earned,
three lines, a next action I confirm, and a continuation note that supersedes the older one.

Your job is NOT to rewrite the skill. It is to fit its rules to my folders and checks, and to
tell me where the rules do not fit the way I work.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where do continuation notes live? Give the folder, relative to my knowledge base or project
   root. (Default: a continuations folder inside the knowledge base.)

2. Which project keys are in use? Give the exact folder name for each project. A folder name is
   never shortened, because a shortened key cannot be matched in the next session.

3. Which projects share a folder, and can one session change files in two projects at once?
   (This decides when one session writes two notes.)

4. Who confirms the next action before a note is written? Name one person. If that person is
   not available, should the note be saved as draft? (Default: yes, saved as draft.)

5. For each kind of file I change, which check does it earn? Go through these kinds: knowledge
   items, code, a changed skill, rendered output, and any figure with a number. For each one,
   name the command or the check, or say "none".

6. Where does the knowledge base live, so the link and tag check can run? Say "none yet" if it
   does not exist.

7. Which checks can NOT run on my machine right now? For each one, the note will say "not run"
   with the reason. Tell me the reason you would expect to see.

8. Do you accept the defaults? They are: one note per project per day, a second run on the same
   day updates that day's note, a superseded note changes only its status line, and a failed
   check goes under Open Threads without stopping the close. Name any default you reject, and why.

9. Who receives the closing lines, the list of draft notes and the commit suggestions? Name one
   person, or say "me".

Then produce:

A. The `## Wrap-Up` section, in the format shown below, ready to paste into
   profiles/client-profile.md.

B. A check table: each kind of file, the check it earns, and what the note should say when that
   check cannot run.

C. THE HONEST PART: a short list of the questions you could not answer for me, and which parts
   of the close will therefore run on the defaults.

Start with question 1.
```

---

## What You Should Expect to Happen

Questions 1 and 2 usually land quickly, because most teams know where their notes go and what their project folders are called. Question 3 is where teams find that one working session often touches two projects. The skill answers that with two notes, one per key, so the answer matters.

Question 4 matters most. A close that nobody confirms is saved as draft, and the draft status says so, so the next session knows the next action is not yet agreed. Question 5 is where the checks become concrete. A check the team has no command for is recorded as "none", not invented.

---

## The Wrap-Up Section to Paste

The skill writes this section into `profiles/client-profile.md` after the interview. Fill in the brackets, or leave "none" where the answer is none.

```markdown
## Wrap-Up

- **Continuation notes folder:** [folder path, relative to the knowledge base or project root]
- **Project keys in use:** [exact folder names, one per line]
- **Shared-folder rule:** [which projects share a folder, and whether one session may write two notes]
- **Who confirms the next action:** [one person]. If unavailable: [save as draft, or name a fallback]
- **Checks by file kind:**
  - Knowledge items: [link and tag check, or "none"]
  - Code: [test and lint commands, or "none"]
  - Changed skills: [version and changelog check, or "none"]
  - Rendered output: [what to look at, or "none"]
  - Figures: [source rule, or "none"]
- **Knowledge base location:** [folder, or "none yet"]
- **Closing lines go to:** [one person, or "me"]
- **Checks that cannot run here:** [list, and what the note should say instead]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill says it is running uncustomized | The `## Wrap-Up` section is missing from the profile | The skill uses its defaults and says so once. Run this interview, then paste the section |
| A project key matches no folder | The folder was renamed, or the key was shortened | Ask for the exact folder name, and update the key in this section |
| Next actions are never confirmed | The confirming person is away or not named | Name a fallback in question 4. Until then, notes are saved as draft |
| A check says "none" for a kind of file you change | Question 5 was skipped | Answer question 5 for each file kind. "None" is a valid answer, and the note will record it |
