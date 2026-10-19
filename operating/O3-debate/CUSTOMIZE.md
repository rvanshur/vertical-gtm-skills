# Customize: Debate

A paste-in prompt that sets up the `## Debate` section of your client profile. It asks which decisions your team makes, what posture each one should take, who owns each call, and where decision records are saved, so the skill knows how to seat a panel and where to file its matrix.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up the Debate section of my client profile.

Read the attached SKILL.md (gtm-debate, version 2.0.0). Debate seats a panel of
expert views on one decision, makes them argue, and produces a decision matrix.
It advises only and never builds anything. It writes only its own decision record.

Your job is NOT to rewrite the skill. It is to record my choices, name the places
I have, and tell me honestly what the skill cannot check in my setup.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which decisions does my team make most often? List the domains, for example
   architecture, security, data, performance, UI, copy, branding, positioning, UX.
   Name at most eight.

2. For each domain I name, should the answer converge (one path) or diverge (two
   live directions)? If I am unsure, offer the default from the posture table in
   the skill and ask me to accept or change it. The defaults are: architecture,
   security, data and performance converge. UI, copy, branding and positioning
   diverge. UX is mixed.

3. Who owns each kind of decision? Give one named person or role per domain. The
   owner makes the call. The panel never does.

4. When should a decision record be saved? The default is: when I ask for one, and
   for architecture, security, data, and high-impact product calls. Accept it or
   name a different rule.

5. Where do decision records live? Give a folder or a link. If there is no folder,
   answer "text only", and the skill prints the matrix in the reply and saves
   nothing.

6. How many seats should a default panel have? The default is three, up to seven
   for a big call. The premise seat is always included, and it cannot be switched
   off.

7. Is there a notes folder for the work a debate usually touches? If yes, give its
   location, so the skill reads the notes before it argues. If no, answer "none".

Then produce:

A. The Debate section, filled in, ready to paste into profiles/client-profile.md.

B. A field check. Each field is either set, or marked "not set" with the effect of
   that on a run.

C. THE HONEST PART. A short list of what this setup cannot check. For example: no
   decision folder (so no record can be saved), a domain with no owner (so the
   owner is asked on every call), or no notes folder (so every claim about the
   work is marked unread).

Start with question 1.
```

---

## What You Should Expect

Questions 1 and 3 usually land first, because most teams know which calls they make and who signs off on them. Question 2 is where teams stall. Many have never said out loud which calls should end in one answer and which should keep two options open. The defaults in the posture table answer it, and the skill uses them for any domain you accept them for.

Question 5 decides whether a record exists at all. With "text only", the matrix lives in the chat and disappears when the session ends, so the close of a session has nothing to file under Decisions Made. A folder takes a minute to name.

Question 6 is the one most people should leave alone. Three seats is enough for most calls. Seven is for a call that is expensive to reverse.

---

## The Debate Section

Add this section to `profiles/client-profile.md` once. The skill reads only this section for its settings.

```markdown
## Debate

- **Domains the team decides in:** [list, up to eight, or "not set"]
- **Default posture by domain:** [one line per domain, as "domain: converge" or "domain: diverge". Default: the posture table in the skill]
- **Owner by domain:** [one named person or role per domain. "Not set" means the owner is asked on every call]
- **When a record is saved:** [on request, and for architecture, security, data and high-impact product calls, or your own rule]
- **Decision record location:** [folder or link, or "text only, no saved record"]
- **Default panel size:** [three, or up to seven for a big call. The premise seat is always included]
- **Notes folder for the work:** [folder or link, or "none"]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---|---|---|
| The skill says it cannot save a record | No decision record location is set | Name a folder in the record location field. Until then, the matrix stays in the reply |
| The skill asks who owns a call | The owner field is "not set" for that domain | Name one person or role for the domain. The skill does not assume an owner |
| The skill marks its claims about the work as unread | No notes folder is named | Name the folder in the notes field, so the skill reads the notes before it argues |
| The skill argues a decision the team already settled | No earlier records are saved for that subject | Save the earlier matrix to the record location, and the next debate checks it first |
| The skill ignores my posture for a domain | The posture is not set for that domain | Add the domain to the default posture field. Where a field is missing, the skill uses the posture table |
