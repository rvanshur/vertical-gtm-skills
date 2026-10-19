# Customize: Debug

A paste-in prompt that sets up the `## Debugging` section of your client profile. It asks how you run the checks, where the handoff file lives, which bugs your project sees most, and who is told when the circuit breaker fires. The skill then knows what it may run and where it writes before it starts a session.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up the Debugging section of my client profile.

Read the attached SKILL.md (gtm-debug, version 2.0.0). Debug finds the cause of a bug
from a written hypothesis before any change. It tests one change at a time, fixes at one
file and line, and stops after three failed hypotheses to write a handoff file.

Your job is NOT to rewrite the skill. It is to record my choices, name the checks I have,
and tell me honestly what the skill cannot do in my setup.

Ask me these, ONE AT A TIME, and wait for each answer:

1. How do I run the project's checks? Give the test command, and the lint or build command
   if there is one. If there is no test command, say so.

2. Is this project code, non-code work such as documents or configurations, or both?

3. Where should the handoff file live? Give a folder or a page. Answer "text only" if you
   do not want a saved file. Without a saved file, a stopped thread cannot be picked up
   in the next session.

4. Which bug classes does this project see most? Choose any of: regression, new bug,
   visual or rendering, behavioral or lifecycle, timing.

5. When the circuit breaker fires, who is told? Give one name or role. If nobody, answer
   "none", and the skill will record that the owner was not told.

6. Can you add a diagnostic line and paste its output here? Answer yes, no or unsure.

7. Does the team record a last known good point, such as a release tag, a deploy date or
   a version number? If yes, name where it lives.

Then produce:

A. The Debugging section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect of that
   on a session.

C. THE HONEST PART. A short list of what this setup cannot check. For example: no test
   command (so every check is run by hand and pasted), no handoff location (so a stopped
   thread is not carried forward), or no diagnostic access (so hypotheses are limited to
   what the output shows).

Start with question 1.
```

---

## What You Should Expect

Question 1 usually lands first, because most teams know their test command. Question 3 is where teams stall, because a saved handoff means a place to keep it. "Text only" is a valid answer. The skill then keeps the handoff in the reply, and it tells you the next session starts cold.

Question 5 matters more than it looks. The circuit breaker is the moment a session stops and hands work to a person, and a stop with no one named is a stop nobody reads. Answer with one name or one role, not a team.

Question 6 often comes back "unsure". Answer it honestly. The skill will not invent a diagnostic line it was not allowed to add, and it limits its hypotheses to what the error and the output already show.

---

## The Debugging Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its settings. It does not write to it.

```markdown
## Debugging

- **Test command:** [the command that runs the project's tests, or "not set, check run by hand"]
- **Lint or build command:** [the command, or "not set"]
- **Work type:** [code, non-code or both. Non-code uses the log-line or diff gate]
- **Handoff location:** [folder or page for handoff files, or "text only, no saved handoff"]
- **Common bug classes:** [the classes the project sees most, from the five in SKILL.md]
- **Diagnostic access:** [yes, no or unsure]
- **Last known good point:** [where the team records it, or "not set"]
- **Told at the circuit breaker:** [one name or role, or "none, owner not told"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill says the owner was not told | No one is named in question 5 | Name one person or role. Until then, each handoff records that the owner was not told |
| The skill runs every check by hand | No test command was given | Give the command in question 1. Until then, each check is run by hand and its output pasted |
| A stopped thread disappears between sessions | No handoff location was set | Answer question 3. Without it, the handoff stays in the reply only |
| The skill works only from the error and the output | Diagnostic access is "no" or "unsure" | Add a diagnostic line yourself, paste its output, or accept that hypotheses stay within what the error shows |
| The gate is a log line on code work | Work type was set to non-code | Set question 2 to code. For code, the failing test is the gate |
| The regression steps do not run | No last known good point is recorded | Answer question 7. Without it, the skill can still bisect, but it has no known starting commit |
