# Customize: Second Opinion

A paste-in prompt that sets up the `## Second Opinion` section of your client profile. It asks which route you use, what must never leave the machine, who approves a send, and where review files live, so the skill knows what it may send before it sends anything.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up the Second Opinion section of my client profile.

Read the attached SKILL.md (gtm-second-opinion, version 2.0.0). Second Opinion sends
finished work to a reviewer from another vendor, after a dry run that shows me every
file that would leave my machine. It triages every finding as AGREE, DISAGREE or
NEEDS-A-LOOK, and it changes nothing in my work by itself.

Your job is NOT to rewrite the skill. It is to record my choices, name the places I
have, and tell me honestly what the skill cannot check in my setup.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which route is my default? Paste into a chat with a model from another vendor (no
   keys needed), a command-line tool, or an API call. Recommended: paste.
   If I choose either of the other two, ask me where my credentials are kept. Name the
   place only. Do not ask me to paste any key or credential into this conversation.

2. Which of my work is expensive to get wrong? Name the kinds of change that should go
   to a panel of two or more reviewers, each sent separately. Examples: money, records,
   access, a public promise.

3. What must be held back, by path or by kind? Think fixtures, test data, exports,
   snapshots, captures, lock files, and any repository that is not mine.

4. Who owns the data, and who says yes before anything is sent? Give one named person.
   If no one is named, the skill will stop before the dry run and ask.

5. Whose approval is needed before the first run on a repository that is not mine, or
   on client code? Name the person, or answer "none".

6. Where do review files live? Give a folder that sits next to the work, for example a
   reviews folder inside each project.

7. Reviewer lenses in this project's words. For each of these, give one sentence on
   what it means here: correctness, robustness, tests, security, scope. Then add any
   project rule a reviewer must know before it judges a change.

Then produce:

A. The Second Opinion section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect of
   that on a run.

C. THE HONEST PART. A short list of what this setup cannot check. For example: no
   reviewer from another vendor reachable from here (so only the same-vendor pass runs),
   no hold-back list (so the default list runs), no data owner (so nothing is sent), or
   no cost log (so cost cannot be compared across runs).

Start with question 1.
```

---

## What You Should Expect

Question 1 and question 4 usually land first. Most people know which route they want and who can say yes to a send. Question 4 matters most. With no data owner named, the skill stops before the dry run, because nothing is sent to a party nobody has been asked to approve.

Question 3 is where teams stall, because a hold-back list means remembering which files are real. Start with the default list and add to it each time a dry run shows a file you did not expect. A short list you trust beats a long list you do not read.

Question 7 is the one that makes the reviewer useful. A reviewer that knows the project's rule can tell a real gap from a choice that only looks wrong from outside. Write the rules once, in the profile, and they travel with every run.

---

## The Second Opinion Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its settings. It writes back the date of the last dry run after each saved review.

```markdown
## Second Opinion

- **Default route:** [paste, command-line tool or API call. Default: paste]
- **Where credentials live:** [name of the place, never the credential itself, or "not applicable: paste"]
- **Work that goes to a panel:** [kinds of change that are expensive to get wrong, or "none named"]
- **Hold-back list:** [paths or kinds that are never sent. Default: fixtures, test data, exports, snapshots, captures, lock files]
- **Data owner:** [one named person who says yes to every send. "Not set" means nothing is sent]
- **Approval for other repositories:** [whose yes is needed before a repository that is not mine is sent, or "none"]
- **Review files:** [folder beside the work where dated review files are saved]
- **Reviewer lenses in this project's words:**
  - Correctness: [what it means here]
  - Robustness: [what it means here]
  - Tests: [what it means here]
  - Security: [what it means here]
  - Scope: [what it means here]
  - Project rules a reviewer must know: [list, or "none"]
- **Last dry run date:** [date of the last saved review, or "none yet"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill stops before the dry run | The data owner field says "not set" | Name one person in the Data owner field. Until then, the skill prepares the manifest but sends nothing |
| The skill keeps finding a file that should be held back | The hold-back list does not name that kind of file | Add the path or the kind to the Hold-back list field. The next dry run will show it held |
| Reviews keep returning DISAGREE on the same kind of finding | The reviewer lacks a project rule | Write the rule into the project rules line of the reviewer lenses. Each run then carries it |
| The skill says it is running uncustomized | This section is missing from the profile | Paste the section above into the profile, or run this interview again |
| The skill will not use a route | The credentials are not set in this session | Use the paste route for this review, and record the route change in the review file |
| The field check shows "not set" for the review folder | Question 6 was not answered | Give a folder beside the work. The skill will not save a review to a place it was not told about |
