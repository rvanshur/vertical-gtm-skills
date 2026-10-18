# Customize: Graph Health

A paste-in prompt that writes the `## Graph Health` section of your client profile. It tells the skill where your base lives, where your tag list is, how your links are written, how often you run the check, and where the reports go.

Works in **Claude Code**, in **Codex**, and in **ChatGPT** as a custom GPT. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```text
You are helping me set up a structure check for my knowledge base.

Read the attached SKILL.md (gtm-graph-health, version 2.0.0). It measures the shape of the
base: tag sprawl, link density, provisional age and broken links. It returns a structure
score and a list of decisions for me. It never edits an item and never judges whether one
is true.

Your job is NOT to change the skill. It is to learn where my base lives and how my links
are written, then write my section of the client profile.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where is the knowledge base? Give the folder that holds the items, as I open it on my
   own computer or in the tool I use. If the items live in more than one folder, list them.

2. Is there a tag list? If yes, where is it? A tag list lets the skill flag any tag nobody
   chose. If there is none, the off-list deduction will read null, and the score will be
   marked partial.

3. Which link syntax does the base use? The default is wiki-links in the form [[name]].
   If mine is different, say so exactly. The skill reads only the syntax I name.

4. How often will I run it? The default is before every Dream run and before every
   Weekly Review.

5. Where should the reports go? A folder in the base, or the chat only.

6. Who owns the decisions the report returns? Name the role, not a person, if the report
   will be shared.

Then produce:

A. The ## Graph Health section, filled from my answers, in the format shown below.

B. A check of three items. Open three items I name, and for each one tell me which of these
   fields it has: name, domain, node_type, status, created, updated, tags and related.
   Any field missing on an item is reported as missing, and the skill will write it as null.

C. The honest part. List which parts of the score I cannot compute from what I gave you,
   and what stays null because of it.

Start with question 1.
```

---

## What You Should Expect

Questions 1, 4 and 5 usually land quickly. Question 2 often comes back "none", which is a valid answer. The score is then marked partial, and the off-list deduction reads null with its reason.

Question 3 is the one that most often goes wrong. If the links are written in a different syntax from the one named, every item reads as an orphan. Check the three items in part B before running the full base, and fix the syntax first.

Question 6 matters because the decisions the report returns need a named owner. A report with no owner gets read and then left alone.

---

## The Profile Section

The assistant writes this section into `profiles/client-profile.md`. The skill reads it at the start of every run.

```markdown
## Graph Health

- **Knowledge base location:** [folder path, or "not set" until it is recorded]
- **Tag list location:** [path, or "none supplied", which makes the off-list deduction read null]
- **Link syntax:** [wiki-links in the form [[name]], or the syntax named in question 3]
- **Run cadence:** [before every Dream run and before every Weekly Review, or the cadence named]
- **Report location:** [folder for reports, or "chat only"]
- **Decision owner:** [the role that receives the decisions]
- **Fields the skill reads:** name, domain, node_type, status, created, updated, tags, related
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| Every item reads as an orphan | The link syntax recorded does not match the syntax in the items | Correct the syntax in this section, then run the check again. Do not change the items to suit the skill |
| The score is marked partial | No tag list, or a required field missing on many items | Keep the partial mark. Add the tag list or fill the fields, then run the check again |
| The skill asks for the knowledge base location again | The section was not saved to the profile | Save the section, then run the prompt again |
| The report will not write | The report location is not set, or cannot be reached | Return the report in chat, and record the location once it exists |
