# Customize: Context Gap

A paste-in prompt that sets up the `## Context Gap` section of your client profile. It asks where your code, notes, paid tools and patterns live, and what counts as small enough to finish without a plan, so the search knows where to look before it looks.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```text
You are helping me set up the Context Gap section of my client profile.

Read the attached SKILL.md (gtm-context-gap, version 2.0.0). Context Gap writes one of six
states after it searches four places: the codebase, the knowledge base, the paid tools and
the patterns that already run. It never builds anything and never changes what it examines.

Your job is NOT to rewrite the skill. It is to record where my four places live, name what
the skill cannot reach, and set the small-work threshold.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where does my code live? Give a folder, a repository or a list of them. Say "none" if
   I do not build code.

2. Where does my knowledge base live? Give a folder or a link. Say "none" if I have not
   set one up.

3. Which tools do I already pay for that could already do part of the work? Name each
   product and give one line on what it does. Say "none" if there are none.

4. Where are the patterns that show how we build things here? For example a template
   folder, a reference project or a set of finished examples. Say "none" to fall back to
   the codebase.

5. What counts as small enough to finish directly, with no planning document? The default
   is 50 lines of real work. Accept it or give a different number, with the reason.

6. Are there any places I cannot search from this session, such as a locked drive or a
   tool that needs a login? Name each one, so the result can say "not searched" instead
   of silently skipping it.

Then produce:

A. The Context Gap section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect of that
   on a search.

C. THE HONEST PART. A short list of what this setup cannot reach. For example: no
   knowledge base yet (so that place is always marked not searched), or a paid tool that
   needs a login this session does not have.

Start with question 1.
```

---

## What You Should Expect

Questions 1 and 2 usually land first, because most people know where their files and notes live. Question 3 is the one people skip, and it is the one most likely to turn a build into a configuration change. A paid feature that is switched off is the cheapest CONFIG there is, so the list is worth ten minutes of thought.

Question 5 sets the line between finishing directly and writing a plan. A higher number lets the skill finish bigger pieces without a plan. That saves time, and it also allows a larger unplanned change. Fifty is a starting point, not a measured rule.

Question 6 is where the honest answers come from. Write down the places that will always be out of reach, even when the list feels long, because a result that says "not searched" is more useful than one that quietly looks thorough.

---

## The Context Gap Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its settings. It writes no values back, because each gap result is saved beside the work it describes.

```markdown
## Context Gap

- **Codebase location:** [folder, repository or list, or "none"]
- **Knowledge base location:** [folder or link, or "none"]
- **Paid tools that already do work:** [product name and one line on what it does, one per line, or "none"]
- **Pattern library location:** [folder or document, or "none, use the codebase"]
- **Small-work threshold:** [50 lines of real work, or the number you chose and why]
- **Places not searchable from this session:** [each place and the reason, or "none"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---|---|---|
| The result says the knowledge base was not searched | Question 2 was not answered, or the location is "none" | Give the folder or link. The skill will not search a place it was not told about |
| The result says paid tools were not searched | Question 3 was left empty | Name the tools. An empty list means the skill had nothing to check, and it says so |
| Every search comes back TRUE GAP | The codebase location is wrong or not set | Check question 1. The skill searches only the folder it was given |
| A search returns too much and the owner is overwhelmed | The codebase or knowledge base location is too broad | Narrow the codebase location to the project folder, and name the knowledge base folder instead of its root |
| The small-work line keeps sending ordinary finishing work to a plan document | The threshold is lower than the team's typical work | Raise the threshold with a stated reason, and record the change in this section |
