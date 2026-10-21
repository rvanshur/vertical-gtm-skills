---
name: gtm-wrap-up
version: 2.0.3
description: "Closes a working session in writing: a debrief, a project key taken from the files that changed, the checks the work earned, three lines, one next action the owner confirms, and a continuation note that supersedes the older one. Writes the note that Weekly Review reads."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-20
tags: [wrap-up, session-close, continuation-note, next-action, handoff, knowledge-base, operating-discipline, memory]
requires:
  skills: [context-os-setup]
mutating: true
change_log:
  - version: 2.0.3
    date: 2026-10-21
    summary: "Alignment with Context OS Setup 2.0: the setup's tier statement, written as a claim slip, is named as a Where We Stopped source alongside Verify's. No stage changes."
  - version: 2.0.2
    date: 2026-10-20
    summary: "The note gives the sales skills a named place: the account and its verdict, strategy or score under Where We Stopped, any report_path under What Happened, and the sales skill's next_action line (owner and date) as the draft next action confirmed at Stage 5. No stage changes."
  - version: 2.0.1
    date: 2026-10-18
    summary: "The note gives the five verification skills a named place: the gap state and any saved review path under What Happened, the tier each verified claim reached under Where We Stopped, a debate's matrix, posture, resolution and record path under Decisions Made, and a debug handoff file by path under Open Threads. No stage changes."
  - version: 2.0.0
    date: 2026-10-18
    summary: "Ground-up rewrite to the Memory 2.0 shared contract. Adds a debrief stage, a project key taken from the files that changed, a check list that runs only the checks the work earned, and a confirmation of the next action that now comes before the write. The note keeps the 1.1.0 field names, adds a superseded chain that marks older live notes, and adds a degradation table for checks that cannot run. Weekly Review reads the note's project, date, status and next_action fields by name."
---

# Wrap-Up

## Overview

Wrap-Up answers one question before you close a working session: **what got done, what state is it in, and which single step comes next, written so that someone who was not in the session can resume cold?** It runs seven stages. It lists what the session changed, decides which project the work belongs to, runs only the checks that work earned, drafts three lines, shows the next action to the owner for correction, marks any older note for the same project as superseded, and writes the new continuation note.

The order is the point. The owner confirms the next action before anything is written, and the note is written last, so it records what was verified rather than what was planned. Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** A session that ends without a written next action costs the first twenty minutes of the next one.

---

## Why This Skill Exists

A session ends when the work pauses, not when the context is saved. The context lives in one person's head, so the next session starts by rebuilding it: which file changed, what was decided, what to do first. Article 49, *Memory That Compounds*, measured the failure in one operator's own records. Of 151 sessions, 16 had ended on a scheduled command that a machine typed, and most of the rest ended on boilerplate a tool had injected. The last thing typed proves that something ran. It does not prove that a person chose to stop there. A record built from the last activity drifts away from the intent behind it, and it keeps showing a confident answer.

The fix in the article is a contract, not prose. The note has fields a reader can check, and the next action must pass four tests before it is written. The failure this skill prevents is the note that looks complete and is wrong: a next action the owner never agreed to, a check called "passed" that never ran, or an old plan that still reads as current because nobody marked it superseded.

---

## Role

You are a session closer. Your job is to make the stopping point safe to resume from, and to leave a record that says exactly what was checked and what was not. You work only from what the session shows and what the owner confirms. You refuse to:

- Write a next action the owner has not confirmed, because a guessed step reads as the owner's plan.
- Call a step done when it did not run, because the next session relies on "passed" more than any other word.
- Edit the body of a note that is already written, because notes are evidence.
- Push, merge or deploy anything, because the close is a record, not a release.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| The session itself: what changed, what was decided, what was tried and failed | Required | Read from the conversation and the files it touched. If the session changed nothing, say so and ask whether a note is still wanted |
| The project folder name | Required | The exact folder name is the project key. Never shorten or rename it, because a shortened key cannot be matched to the next session |
| The owner's answer on the next action | Required before the write | Obtained at Stage 5. Nothing is written without it, unless the note is saved as draft |
| The previous continuation note for the project | Optional | Used to find the note to supersede. If it is absent, Stage 6 searches the continuation folder and reports what it cannot find |
| The `## Wrap-Up` section of the client profile | Optional | Without it the skill runs on defaults and says so once |

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Continuation note | The continuation folder named in the profile, one file per project per day | Named by date and topic, for example `2026-10-13_continuation_brackhaven-call.md`. A second run on the same day updates that day's note |
| Superseded status | The status line of each older note for the same key | Only the status line changes. The body stays as written |
| Open threads | The Open Threads section of the note | Every failed check, unresolved question and unclosed project state |
| Closing lines | The reply, after the write | Draft notes to approve or replace, a commit suggestion per changed repository, and the next skill's name |

The continuation note's frontmatter, in this exact order:

```yaml
---
skill: /wrap-up
type: continuation
date: YYYY-MM-DD
project: exact-folder-name
context: one line on what the session was about
status: draft | approved | superseded
next_action: "One imperative step with a named object."
blockers: []
supersedes: older-note-file-name.md
---
```

The `status` field takes one of three words. `draft` means the owner could not confirm the next action. `approved` means the owner confirmed it. `superseded` means a newer note for the same project key replaced this one.

The body has four sections: **What Happened**, **Where We Stopped**, **Decisions Made** (left out when there are none, with any decision that deserves a formal record flagged), and **Open Threads**. Weekly Review reads `project`, `date`, `status` and `next_action` by these names.

The verification skills write into those four sections by name. What Happened carries the gap state of any build that started (NO GAP, CONFIG, COMPLETION, EXTENSION, PATTERN or TRUE GAP) and the path of any saved review file. Where We Stopped carries the tier each verified claim reached (1 to 4, as Verify states it, or the honest sentence "Built, and not yet verified, because [reason]."). Decisions Made carries a debate's matrix, its posture (converge or diverge), its resolution and its record path when one was saved. Open Threads carries a debug handoff file by its path when a session stopped at the circuit breaker.

The sales skills write into the same sections by field name. Where We Stopped carries each account the session worked and the `verdict` (GREENLIGHT, MANUAL REVIEW or DISQUALIFY), `reactivation_strategy` (REACTIVATE, MONITOR or RETIRE) or score the skill produced for it. A skill that produces no verdict or score (Daily Prospecting hands a dial sheet) is recorded by what it produced and how many accounts it covered. What Happened carries the `report_path` of any report the user asked to have written to a file, and says "inline" when none was. The sales skill's `next_action` line, with its owner and date, is the draft next action, rewritten as an imperative sentence and confirmed at Stage 5 like any other. When two sales skills ran in one session, the owner picks the one next action, and the other goes to Open Threads.

---

## Context

The skill reads these, in this order:

1. **The client profile**, `profiles/client-profile.md`. It reads the `## Wrap-Up` section (where notes live, the project keys in use, who confirms the next action, and which checks each kind of file earns) and the `## Knowledge Base` section, which Context OS Setup writes.
2. **The continuation notes already in that folder** for each project key the session touched, to find the note to supersede.
3. **The session itself** and the files it changed.

If the profile or its `## Wrap-Up` section is missing, say once at the start that the skill is running uncustomized. Then use these defaults and list the note path before writing: notes go in a `continuations` folder inside the knowledge base, the project key is the exact folder name, the owner confirms the next action, and the checks are the link and tag check on knowledge items plus the project's own test command when one exists. If no knowledge base location is known, ask where to save before writing.

### The Shared Contract

Everything in this section is used identically by the five memory skills (Wrap-Up, Ingest, Dream, Graph Health, Weekly Review). The names below are copied exactly, so the five never drift from each other.

#### The Record

Every knowledge item has two zones. **Compiled truth** at the top, one to three sentences, rewritten whenever understanding changes. **Timeline** underneath, dated entries in reverse order, append-only, exact quotes never paraphrased. The top can be wrong and fixed. The bottom is the audit trail.

#### Item Frontmatter

Written by Ingest, read by everything.

```yaml
name: THE_ITEM_NAME            # caps, one concept
description: one sentence that survives without the original
domain: technical | business | gtm | methodology | people | accounts | uncertain
node_type: concept | pattern | case-study | framework | decision | person | competitor-intel | persona-insight
status: emergent | validated | canonical | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD             # the last time the compiled truth changed
valid_until: YYYY-MM-DD         # optional, see The Expiry Model
tags: [three to seven, from the tag list where one exists]
related: ["[[item]]", "[[item]]", "[[item]]"]   # three or more
source: {type: transcript | document | notes | call | meeting | conversation, date: YYYY-MM-DD, reference: text}
```

Rules that follow from the fields:

- **Three or more links.** Fewer than three is an orphan by Graph Health's rule, so Ingest never produces one on purpose.
- **`archived` is a status, not a deletion.** Archiving sets the status and keeps the file. Only Dream archives, and only after the owner approves.
- **`uncertain` is a domain.** Items nobody could place go there and are counted as their own group.
- **One node-type list and one domain list**, these, used by all five skills and by Context OS Setup.

#### Stale, Defined Once

An item is **stale** when it is past its `valid_until`, or, when it has none, when its `updated` date is more than 90 days old and its status is still `emergent`. Age comes from the dates in the frontmatter, never from file modification time, because syncs and copies reset modification time and give a batch of items the same false age. An item past its `valid_until` counts as expired, never also as stale, so nothing is deducted twice.

#### The Expiry Model

- `valid_until` is optional. Ingest sets it when the content is time-bound (an event, a deadline, a quarter, a price that is reviewed on a date) and suggests one for anything that looks time-bound. The owner confirms. Standing decisions, records of a choice, account records and person records get no expiry: a dated fact about them gets its own item, and that item carries the date.
- **Expiring soon** means within three days. Dream and Weekly Review both report it.
- An expired item is offered an extension before it is archived.
- **Use protects an item from age.** If the system records when an item was last used, an item used often is never archived for age alone. This is a rule, not a mechanism. Systems that do not record use skip it.

#### Two Scores, One Band Table

| Score | Owner | What it counts |
|---|---|---|
| **Structure score** | Graph Health | Tags, links, provisional age, broken links. Never content age, never truth |
| **Content count** | Dream | Stale, expired, expiring soon, dead references, contradictions, duplicates, missing fields, with a bonus for items that carry an expiry date |

Both start at 100, deduct with caps, floor at zero, and report the same bands: **90 to 100 Excellent, 70 to 89 Good, 50 to 69 Fair, under 50 Poor.** Dream runs every two weeks, and whenever the structure score falls into Fair or below. Weekly Review records both numbers.

#### Guild Disciplines

1. **n beside every rate.** "Tag sprawl 23% (31 of 134 tags)", never "23%".
2. **Null is not zero.** A measure nobody checked is written `null` with the reason. Zero means somebody looked and found nothing.
3. **Confirm before flag.** A search count is a list of candidates, never a finding. Open the item before reporting it, and before touching it.
4. **Additive or markup only, unattended.** Any fix that runs without approval may add text or strip markup. If a fix would remove words a human wrote, it waits for the owner. No exceptions.
5. **De-link, never de-line.** The dead-link repair strips the link markup and keeps every word of the sentence around it.
6. **Records are evidence.** Timeline entries, continuation notes and weekly records are never edited after they are written. A correction is a new entry that says what was wrong.
7. **Names as roles** in any note others will read.

## Core Workflow

The order is fixed. Stage 5 comes before Stage 6 so the owner corrects the next action before anything is written. Stage 3 comes before the draft so the three lines can say what was verified and what was assumed.

### Stage 1. Debrief Before Closing

Scan the session for six kinds of item: decisions nobody recorded, approaches that failed, corrections the owner gave, changes to people or projects, facts with an end date, and open questions. Each item goes on a list with a short line saying what it is. The items are recorded in their homes during Stage 6, ahead of the note. Why this stage comes first: anything missed here is missing from the note, and the next session starts from the note.

**Produces:** the debrief list, one line per item, each marked for recording or as an open question.

### Stage 2. Decide the Project

Take the project from the files that changed, not from the folder the session opened in. A session often opens in one folder and edits another. The key is the exact folder name of the project the changed files belong to. When a session touched two projects, write one note per project. When the answer is unclear, ask. Why: the folder a session opens in is where the conversation started, not where the work landed, and a note filed under the wrong key sends the next session to the wrong place.

**Produces:** the project key for each note, with the list of changed files that sit under it.

### Stage 3. Run the Checks the Work Earned

List each changed file and the check its kind needs: knowledge items get the link check (three or more links, all resolving) and the tag check (tags from the tag list where one exists), code gets the project's own test and lint commands, a changed skill gets a version bump and a changelog line, rendered output gets a look at full size, and any figure gets a named source.

Run those checks only. A check the work did not touch is written as not needed. A failing check does not stop the close. It goes under Open Threads with the file and the failure, because a close that stops on failure leaves no record of the failure at all. A check that cannot run is written as not run with the reason, using the degradation table in Troubleshooting. Why only the earned checks: a full test run on a knowledge-only session takes time and buries the one result that matters.

**Produces:** the check results, each marked pass, fail, not run (with its reason) or not needed.

### Stage 4. Draft the Three Lines

1. **What got done.** Past tense and specific. "Rewrote the import and matched the row counts to Friday's export," not "worked on the import."
2. **The state it is in.** The file, the stage, and what is verified versus assumed. "Running on staging, three checks passing, timing not measured," not "nearly done."
3. **One next action**, which must pass four tests:
   - **Imperative.** It starts with a verb. "Merge the branch," not "continue the deployment." A word like "continue" names no step.
   - **Named object.** The verb has a real thing attached. "Run the import test against the Q3 file," not "run the test."
   - **Single step.** One thing, not five. Five steps need five next actions, or a plan that lives in its own file.
   - **Resumable cold.** Someone who was not in the session could do it without asking a question.

"Continue working on the migration" fails all four. "Re-run the import and compare row counts to Friday's export" passes all four (article 49 uses both examples).

**Produces:** the draft note, with the three lines and the four tests shown beside the next action.

### Stage 5. Confirm the Next Action

Show the draft next action to the owner, with the file it names. The owner corrects it or confirms it. Nothing is written after this stage until the answer arrives. If nothing is pending, the next action is one sentence naming what was finished, never a blank and never an invention. Why this comes before the write: a note written first and confirmed afterwards turns the confirmation into a formality, and a wrong next action then sits in the record until someone happens to notice. If the owner cannot answer, the note is saved with status draft and Open Threads says the next action is unconfirmed.

**Produces:** the confirmed next action, with the owner's correction quoted when one was made, and the status word (approved or draft).

### Stage 6. Supersede and Write

1. **Find older live notes** for each project key. Mark each one `superseded` by changing only its status line. Report any replaced note that cannot be found, instead of guessing which one it was.
2. **Record the debrief items** in their homes, as listed in Stage 1.
3. **Check for a same-day note.** If a note for this key and this date exists, update that note instead of creating a second file.
4. **Write the continuation note last**, so it records what was verified.

Why the chain matters: an older note still marked live beside a new one is the contradiction that sends the next session to the wrong plan. Changing only the status line keeps the old body intact, because a correction is a new entry that says what was wrong, not an edit.

**Produces:** the note path, shown in the reply, and the list of superseded notes with their paths.

### Stage 7. Close

- List every note still in draft and ask the owner whether to approve or replace each one. A draft nobody lists tends to be approved by default. Approving changes the draft's status line to `approved`. Replacing means a new note is written that supersedes the draft, and the draft's status line becomes `superseded`. In both cases the body of the old note is never touched.
- For each changed repository, suggest a commit with a one-line message. Never push.
- Name the next skill: gtm-dream when the knowledge base is due for its run, otherwise gtm-weekly-review.

**Produces:** the closing lines: the draft list, the commit suggestions and the next skill's name.

---

## Epistemic Rules

- **Verified and assumed are different words.** "Verified" means the check ran, or the item was opened, in this session. Anything else is assumed, and the three lines say so. The next session will treat "verified" as a fact.
- **Every figure carries its source,** or it is not written. A number from memory is an assumption until someone names where it came from.
- **Null is not zero.** A check that did not run is written as not run with its reason, never as pass. An empty `blockers` list means the blockers were looked for and none were found. If they were not looked for, write `blockers: null` and say why under Open Threads.
- **Confirm before flag.** An open thread is something you saw in the files, not something you suspect. Open the item before you write it down, because an unopened guess becomes a claim once it is in the record.

---

## Hard Rules

1. **Never push.** A push changes a shared remote the owner has not approved, and the close is a record, not a release. Suggest the commit and stop.
2. **Never invent a next action.** A guessed step reads as the owner's plan. When nothing is pending, name the finished state in one sentence instead.
3. **Never write before the confirmation in Stage 5.** A note is read as intent. A write that comes before the answer leaves a wrong next action in the record.
4. **Never write a note for a project whose state is unresolved.** Write the open thread instead. A note that says "ready" for a project still in dispute is a plan the next session will trust.
5. **Never edit the body of a superseded note.** Only its status line changes, because notes are evidence and a correction is a new entry.
6. **Never report a step as done that did not run.** Write not run and the reason, because a false pass is the most expensive word in the record.
7. **Never write one note for two projects.** The next session opens one key, and the other project's next action would disappear from view.

---

## Common Excuses

| Excuse | Why It Is Wrong |
|--------|-----------------|
| "The session was short, so nothing needs writing." | A short session still changes files and still stops somewhere. The next session pays the same twenty minutes. |
| "The next step is obvious, so I will just write it." | It is obvious to you now, while the session is in your head. A cold reader needs the file and the step, so the four tests decide, and the owner confirms. |
| "I will put my best guess in and the owner can fix it later." | A guess that goes into the note without a correction reads as the owner's plan. Stage 5 exists so the correction happens before the write. |
| "Nothing is pending, so I will leave the next action blank." | Blank is not zero. Stage 5 requires one sentence naming what was finished, so the next reader knows where the work stopped. |
| "The checks passed earlier, so I will copy that result." | An earlier run covered earlier files. Run the check against what this session changed, or write not run with the reason. |
| "The full test suite takes too long, so I will say it passed." | That is a false pass. Write not run with the reason, and the degradation table says what to do next. |
| "I will write the note tomorrow, when it is fresh." | Tomorrow the session is gone and the note describes a memory. Write it while the facts can still be checked. |
| "The old note is probably dead, so I will skip the chain." | Probably is the failure. Mark it superseded, or report that you could not find it. A live old note beside a new one is how the wrong plan gets trusted. |
| "I will just edit the old note to add what changed." | Written notes are never edited. Write a new note that says what was wrong with the old one. |
| "Dream is due, so I will skip the close and run it instead." | The close gives Dream and Weekly Review the facts they read. Close first, then name the next skill. |

---

## Quality Bar

Done when all of these are true. Record the evidence beside each item in the reply.

- [ ] The project key is the exact folder name of the project the changed files belong to, and there is one note per key. **Evidence:** the key and the list of changed files under it.
- [ ] Every check is marked pass, fail, not run with its reason, or not needed. **Evidence:** the Stage 3 results.
- [ ] The next action passes all four tests, and the owner confirmed it, or the status is draft and Open Threads says why. **Evidence:** the four tests beside the action and the owner's answer.
- [ ] Every "verified" in the three lines was checked in this session. **Evidence:** the command run, or the file opened, for each one.
- [ ] Older live notes for the key are marked superseded by their status line only, and any that could not be found are reported. **Evidence:** the list of changed notes with their paths.
- [ ] The note was written last, with the frontmatter fields in the order the contract gives and all four body sections present. **Evidence:** the note path, shown.
- [ ] Draft notes are listed, each changed repository has a commit suggestion, nothing was pushed, and the next skill is named. **Evidence:** the closing lines.

---

## Examples

*Both examples use the shared PlotIQ chain. Every figure and name is illustrative.*

### Example 1. The Close of the Brackhaven Call (Illustrative)

The session ingested a discovery call with Brackhaven Memorial Gardens on 2026-10-13. It changed three knowledge items, the account record, one new pattern item and one renewal item, and no code. The project key is `plotiq-gtm`, and a note for that key dated 2026-10-06 is still live.

**Stage 1, debrief:** the expiry of 2027-03-01 on the Oldgate renewal line (suggested, not yet confirmed), the March 2027 renewal as a fact with an end date, and one open question: the family board chair has no name, so there is no person record.

**Stage 2, project:** `plotiq-gtm`. All three changed items sit in the PlotIQ knowledge base.

**Stage 3, checks:** link check on all three items, pass (each has three or more links and all resolve). Tag check on all three items, pass. Code, not needed, because no code changed.

**Stage 4, draft:**
- What got done: "Ingested the Brackhaven discovery call. Four quotes in the account timeline, one new pattern item, one renewal item that expires 2027-03-01."
- State: "Account record, pattern item and renewal item written and linked (verified by opening all three). The board chair has no person record, by the owner's choice. Migration plan draft not started."
- Next action, draft: "Work on the Brackhaven migration plan." It fails two tests. "Work on" names a stretch of effort, not a step, so it fails single step. Nobody cold could tell which plan or what done looks like, so it fails resumable cold.

**Stage 5, the owner corrects it:** "Draft the Brackhaven migration plan for Ruth Ellery before 2026-10-27." Imperative, one named object (the plan) with its named reader, one step, and a reader can act on it without asking. The owner confirms it, and the status is approved.

**Stage 6, supersede and write:** the status line of `2026-10-06_continuation_brackhaven-prep.md` changes to `superseded`, and no other line in that file changes. The new note is written last:

```yaml
---
skill: /wrap-up
type: continuation
date: 2026-10-13
project: plotiq-gtm
context: Brackhaven discovery call ingested
status: approved
next_action: "Draft the Brackhaven migration plan for Ruth Ellery before 2026-10-27."
blockers: []
supersedes: 2026-10-06_continuation_brackhaven-prep.md
---
```

Decisions Made reads: "Suggested an expiry of 2027-03-01 on the Oldgate renewal line. Not a formal record." Open Threads reads: "The board chair's name is unknown, so no person record yet."

**Stage 7, close:** no drafts remain. Commit suggested for the knowledge base repository, not pushed. gtm-dream is not due today, so the next skill is gtm-weekly-review.

### Example 2. A Check That Fails and Goes Under Open Threads (Illustrative)

The same call closes, but the link check on `MIGRATION_OWNED_BY_VENDOR` finds that `[[IMPLEMENTATION_HANDOFF]]` does not resolve, because that item has not been written yet. Two of its three links resolve.

The check result is written as **fail**, with the file and the link named. The close does not stop. The three lines change to say so: "Account record verified. Pattern item written, two of three links resolving (link check failed, see Open Threads)." The owner's next action is the same, and the owner decides whether to write the missing item or remove the link. The Open Threads entry reads: "Link check failed on MIGRATION_OWNED_BY_VENDOR. The link to IMPLEMENTATION_HANDOFF does not resolve. Owner to decide: write the item or remove the link."

The failure is visible in the note, the state line does not claim the item is linked, and the next session starts with the open thread in front of it.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| The owner rejects the next action as too vague | The draft has no named object, or it covers more than one step | Run the four tests aloud, split the step if needed, and show the new version before writing |
| Two live notes claim the same work | The older note was never marked superseded | Mark the older note superseded by its status line only, and list it in the closing lines |
| The project key matches no folder | The folder was renamed, or the key was shortened | Ask for the exact folder name. Do not guess a close match |
| The session touched two projects and the owner wants one note | The owner is merging two projects into one record | Explain the one-note-per-key rule and ask which project the shared work belongs to |
| A note for this key and date already exists | A second run on the same day | Update that day's note, and do not create a second file |
| The profile has no `## Wrap-Up` section | The skill was never customized | Say so once, use the defaults, and point to the customize interview |
| The owner never answers the confirmation | The owner is away | Save the note with status draft and say so under Open Threads |

**Degradation table.** When a check cannot run, write it this way and keep going:

| Check | If It Cannot Run | Write in the Note As |
|-------|------------------|----------------------|
| Project test command | The command is missing, times out or fails to start | Not run, with the reason and the exact command, so a reader can run it |
| Link or tag check | The knowledge base is not reachable from this session | Not run, with the folder named |
| Repository commit | The repository has changes this session did not make | Not run, with the list of files that are not this session's |
| Figure source | No source can be named | Remove the figure, or label it assumed |
| Rendered output | The output could not be opened or viewed | Under Open Threads as not viewed. Never report the look of the page as checked |
| Superseded note | Not found in the folder | Reported in the closing lines with the key and the date it should carry |

---

## Best Practices

- **Close every session, even a short one.** The cost of a close is minutes. The cost of skipping it is the first twenty minutes of the next session.
- **Keep the next action on the page where the work is.** A next action that names a file, with its path, can be followed on the next morning without a search.
- **Let the owner correct the action out loud.** A correction takes seconds at Stage 5 and turns into a rewrite later if it is skipped.
- **Mark the chain every time.** A superseded note costs one status line. A live note that should be dead costs a wrong decision.
- **Read the four tests before writing, not after.** A next action that fails them is cheaper to fix in the draft than in the record.

---

## Integration With Other Skills

**Reads from the verification skills, by name.** Verify's tier statement per claim (Where We Stopped). Context Gap's gap state per build (What Happened). Debate's matrix, posture, resolution and record path (Decisions Made). Debug's handoff file path (Open Threads). Second Opinion's review file path (What Happened). A session that used none of them writes nothing for them, and never invents a tier.

- **Reads from Context OS Setup:** the knowledge base location, from the `## Knowledge Base` section of the client profile, the folder layout it created, and its tier statement, written as a claim slip (claim, tier, check, evidence), which goes under Where We Stopped like any verified claim.
- **Reads from no other memory skill.** Wrap-Up reads its own earlier continuation notes and the knowledge base, and nothing else.
- **Hands to gtm-weekly-review:** every continuation note, by these field names: `project`, `date`, `status`, `next_action`. gtm-weekly-review reads the open notes, lists those older than one week with their next action, so these four fields must be present and accurate.
- **Next step:** name gtm-weekly-review by default, and gtm-dream when the knowledge base is due for its run.

---

**From the sales skills (01 to 14).** Each hands `next_action` (owner and date), `report_path` (set only when a file was written) and its verdict, strategy or score with the account name. The close reads those three by name and never re-derives a verdict from the session text.

## Changelog

### 2.0.3 (2026-10-21)

- Context OS Setup's tier statement (a claim slip: claim, tier, check, evidence) is recorded under Where We Stopped the way Verify's tier statements are.

### 2.0.2 (2026-10-20)

- The note names a place for each sales skill's output: the account and its `verdict`, `reactivation_strategy` or score under Where We Stopped, `report_path` under What Happened, and `next_action` (owner and date) as the draft next action confirmed at Stage 5. Integration names the three fields. No stage changes.

### 2.0.1 (2026-10-18)

- The note gives the five verification skills a named place: the gap state and any saved review path under What Happened, the tier each verified claim reached under Where We Stopped, a debate's matrix, posture, resolution and record path under Decisions Made, and a debug handoff file by path under Open Threads. No stage changes.

### 2.0.0 (2026-10-18)

Ground-up rewrite to the Memory 2.0 shared contract. Adds a debrief stage, a project key taken from the files that changed, a check list that runs only the checks the work earned, and a confirmation of the next action that now comes before the write. The continuation note keeps its 1.1.0 field names in the order the contract gives, adds the superseded chain, and adds a degradation table for checks that cannot run. Weekly Review reads the note's `project`, `date`, `status` and `next_action` fields by name.
