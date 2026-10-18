# Customize: Ingest

A paste-in prompt that sets how this skill saves to your knowledge base. It asks about your folders, your tags and who approves a save, then writes the answers into your client profile.

Works in **Claude Code**, in **Codex**, and in **ChatGPT as a custom GPT**. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. It writes the `## Ingest` section of `profiles/client-profile.md`. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The Prompt

```
You are helping me set up how the Ingest skill saves to my knowledge base.

Read the attached SKILL.md (gtm-ingest, version 2.0.0). It reads what I give it,
searches my base for existing records, appends to them, asks me before it creates a
person record, and writes only after I approve the save plan.

Your job is NOT to rewrite the skill. It is to fit its save rules to my base and my
habits, and to tell me where my base does not match what the skill assumes.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where does my knowledge base live? Give the folder, or say "none yet". If it is
   "none yet", stop and tell me to run Context OS Setup first. Ingest does not create
   a base.

2. Which folders does my base use for each domain? The defaults are technical,
   business, gtm, methodology, people, accounts (one folder per customer organization)
   and uncertain. Accept the defaults, or name my own for each one.

3. Where is my tag list, if I have one? If I have none, Ingest uses free tags and flags
   each one as not on a list. Do I accept that?

4. Who approves a save? Name the person whose yes is needed before any write. Usually
   that is me.

5. When a source is time-bound and gives no date, what should Ingest do?
   (a) Leave the expiry blank and ask me.
   (b) Suggest a review date that I confirm.
   Give your choice and the reason for it.

6. Person records: the default is that Ingest asks before it creates one. Keep the
   default, or name a different rule.

Then produce:

A. The "## Ingest" section, filled in from my answers. Mark any field I did not answer
   as [ASK LATER], never as a guess.

B. A short list of the folders my base uses, so I can check it against my real folders.

C. What does not match: anything in my base that differs from the skill's assumptions,
   such as a missing tag list, folder names that differ from the defaults, or records
   that already hold the same person under two names.

Start with question 1.
```

---

## What You Should Expect

Question 1 is where most setups stop, because the base is not built yet. Context OS Setup builds it, and this interview cannot run before that. Question 2 often comes back "use the defaults", which is fine, because the defaults match the folders the skill expects.

Question 4 matters most. It decides whether any write can happen without you seeing it first, and the answer should name one person. Question 5 is a judgement call. Option (a) is safer, because it never sets an expiry date you did not check. Option (b) is faster, because it fills in the date for you to confirm.

Question 6 usually stays on the default. A rule of "create by default" is the setting that fills a base with half-records, so change it only with a reason.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. The skill reads it before every run. It also reads the `## Knowledge Base` section that Context OS Setup writes, so the base location is kept in one place. The interview writes this section after your answers, and you can edit it by hand at any time.

```markdown
## Ingest

- **Knowledge base path:** [folder where items are saved, from Context OS Setup, or "none yet"]
- **Folder routing in use:** [the folder for each domain, or "defaults"]
- **Tag list location:** [file or folder holding the blessed tags, or "none, free tags flagged"]
- **Who approves saves:** [the person whose yes is needed before any write]
- **Default for time-bound content:** [leave blank and ask, or suggest a review date to confirm]
- **Person records:** [ask before creating, the default, or the rule you named]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---|---|---|
| Ingest says the base is not set up | The profile has no knowledge base path | Run Context OS Setup first, then run this interview again |
| Ingest proposes folders that do not exist | The routing answer is the default, not your real folder names | Correct the folder routing line in the `## Ingest` section |
| Every tag is flagged as not on a list | No tag list location was given | Point the profile at your tag list, or accept free tags and flags |
| Ingest keeps asking about the same person | The person record rule is set to ask, and no decision was written down | Decide once, then write that decision into the `Person records` line |
| Ingest starts without asking who approves | The `Who approves saves` line is blank | Name the approver. Without a name, the skill stops before any write |
