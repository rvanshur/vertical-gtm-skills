# Customize: Context OS Setup

A paste-in prompt that sets up your knowledge base. It asks where the base lives, who reads it and who approves changes, and then records your evidence for each company and competitor claim. It writes the answers into your client profile.

This runs in Claude Code, in Codex, or as a ChatGPT custom GPT. Open the assistant, paste the block below, attach SKILL.md if the tool allows it, and answer the questions one at a time.

> This companion writes three parts of `profiles/client-profile.md`: the `## Knowledge Base` section, and the `## Company` and `## Competitive Landscape` sections. It does not change any other profile section.

---

## The Prompt

```
You are helping me set up the knowledge base for my go-to-market work.

Read the attached SKILL.md (context-os-setup, version 2.0.0). The skill builds the base
from material I already have. It refuses to start without one real seed item, it asks
whether each file is still true, and it writes nothing until I approve the folder layout.

Your job is not to change the skill. It is to fill in my knowledge base settings and my
two profile sections from my answers, and to tell me where my material does not match
what the skill assumes.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where should the base folder live? Give a path, or say "none yet" and I will decide later.

2. What is the purpose of the base? Go-to-market is the default. Product, research and
   consulting are also options.

3. Who reads the base? One person, a team, or a custom GPT the team uses.

4. Who approves new tags and new folders? Name the role, not a person's name.

5. How often should the deeper review run? Every two weeks or monthly. Say which one,
   and name the role that owns it.

6. Company facts. Paste the Company section of my client profile. For each line, tell me
   the evidence behind it. Use exactly one of these grades: assumed, heard, seen, confirmed.
   Confirmed means the evidence shows it across at least five recent cases with no
   contrary case. If I say confirmed on less evidence, grade it heard and tell me why.

7. Competitive Landscape. Ask the same questions for each competitor row.

Then produce:

A. The "## Knowledge Base" section, with five fields: Location, Taxonomy file, Synthesis
   document, Owner and Maintenance cadence. Mark any field I did not answer as [ASK LATER],
   never as a guess.

B. The "## Company" and "## Competitive Landscape" sections, with every entry marked with
   its grade.

C. A short list of what does not match: a missing seed item, a profile section that is
   missing, a claim I graded higher than its evidence supports, or an owner who is not
   named by role.

Start with question 1.
```

---

## What You Should Expect

Question 1 can be answered "none yet". In that case the setup stops before it writes anything, and you come back once the folder exists. Question 4 decides who signs off on new tags and folders, so name a role and keep it stable.

Question 5 is your decision, not the skill's. Both options are sound, and the owner's role should be the one that will actually run the review.

Questions 6 and 7 are where most setups slow down, because a grade needs evidence behind it. If you cannot name the evidence for a line, its honest grade is `assumed`. An `assumed` entry is useful, because it tells the next skill not to build on that line yet.

---

## Profile Sections This Interview Writes

The interview writes these sections into `profiles/client-profile.md`. You can edit them by hand at any time.

```markdown
## Knowledge Base

- **Location:** [folder path of the base, or "none yet"]
- **Taxonomy file:** [path to `_system/taxonomy.yaml`]
- **Synthesis document:** [path to the summary page the team reads first, or "none yet"]
- **Owner:** [a role]
- **Maintenance cadence:** [the cadence you chose, with the owning role]

## Company

- **[Field]:** [value], grade: [assumed | heard | seen | confirmed], evidence: [source]

## Competitive Landscape

- **[Competitor]:** [position or detail], grade: [assumed | heard | seen | confirmed], evidence: [source]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The setup says there is no seed item | No real file has been named yet | Add one of these: a pricing sheet, a call transcript, a customer list or a competitor note |
| Every grade reads `assumed` | No source has been named for any line | Name one source for each line. `assumed` is a valid grade and marks an open bet |
| Other skills cannot find the base | The Location line is empty or holds the wrong path | Correct the Location line, then run the interview again |
| A skill reports a missing section | The heading is not exactly `## Knowledge Base` | Rename the heading to match exactly, keeping the five field names |
| The owner line names a person | Names change when staff change | Replace the name with the role that owns the base |
