# Customize: Verify

A paste-in prompt that writes the `## Verification` section of your client profile. It asks which commands prove your project works, what a finished piece of work must pass, and which kinds of claim need which checks, so the skill grades each claim against your real checks and not against a generic one.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT. Open the assistant, paste the block below, and answer its questions one at a time.

---

## The Prompt

```
You are helping me set up the Verification section of my client profile.

Read the attached SKILL.md (gtm-verify, version 2.0.0). Verify grades every claim of done
by the tier it reached: 1 Exists, 2 Substantive, 3 Wired, 4 Functional. Tier 4 needs a run
in this session. Reading alone can reach tier 3 at most.

Your job is NOT to rewrite the skill. It is to record my project's checks and rules, and to
tell me honestly where a claim could be graded above its evidence in my setup.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What is the project, and where is its code or output? Give a folder or a link.

2. What commands prove the project works? Give the exact command for each of these: the full
   test run, the build, the lint, and any run of the real thing from start to finish. If one
   does not exist, answer "none" for that one.

3. What is the definition of done? List the checks a finished piece of work must pass, in
   the order they should run.

4. Which kinds of claim need which check? Examples: a code change needs the test run. A data
   export needs a row count from the output file. A page needs a screenshot at full size.
   List your own kinds of claim, and the check each one needs.

5. Who reads the claims, and how sensitive is that? Name the audience by role, such as a
   board, a client or the team. Say what must never appear in a shared claim, such as the
   names of people or of internal systems.

6. Which checks can you not run from this session? For each one, say why. Examples: no
   access, or the run takes too long to wait for.

Then produce:

A. The Verification section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect that has on
   a run.

C. THE HONEST PART. A short list of which claims in my setup can reach tier 4, which can
   reach only tier 3, and which need a check I cannot run. Name the specific gap for each.

Start with question 1.
```

---

## What You Should Expect

Questions 1 and 5 usually come first, because most teams know where their work lives and who reads the claims. Question 2 takes the longest. If a project has no single command that runs the real thing from start to finish, say so. The skill will then grade that project's claims at tier 3 at most, and it will say why on every claim. That is the correct result, because a reader should not get a tier 4 the project cannot produce.

Question 4 is where the setup pays off. A kind of claim with no check in the table can never reach tier 4, so a missing row is a visible gap and not a silent one.

Question 5 keeps names out of shared claims. Name people by role in anything a board or a client will read, and leave them out of the claim itself.

---

## The Verification Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its checks. Keep the commands exact, because the skill runs the command you write.

```markdown
## Verification

- **Project location:** [folder or link, or "not set"]
- **Full test command:** [exact command, or "none"]
- **Build command:** [exact command, or "none"]
- **Lint command:** [exact command, or "none"]
- **Run the real thing:** [exact command or steps that exercise the work from start to finish, or "none"]
- **Definition of done:** [the ordered checks a finished piece of work must pass]
- **Claim kinds and their checks:**
  - [claim kind]: [the check that must run, and the highest tier it can reach]
- **Audience:** [who reads the claims, by role]
- **Never in a shared claim:** [names of people, internal systems, or "not set"]
- **Checks this session cannot run:** [each one, with the reason, or "none known"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| Verify grades every claim at tier 3 | No run command is set in the section | Answer question 2 with the exact command. Until then, tier 3 is the highest tier the skill can reach for this project |
| Verify says the section is missing | The profile was never customized | Paste the section above into the profile, or run this interview again |
| The command in the section does not match the one you run | The section holds an old command | Update the command in the section, and note the date it changed |
| Verify names a check that is not in your section | It read the check from the work itself | Accept it, or add it to the section. Until then, the skill says once that the check was not customized |
| A claim cannot be matched to any check | The kind of claim is missing from the table | Add a row for that kind, with its check and the highest tier it can reach |
