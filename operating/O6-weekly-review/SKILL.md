---
name: gtm-weekly-review
version: 2.0.0
description: "Grades last week's priorities from evidence, measures the knowledge base, pipeline and operations, and writes one dated weekly record that is never edited, for the owner to read and act on next week."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [weekly-review, cadence, drift, null-not-zero, priorities, knowledge-base, operating-discipline]
requires:
  skills: [gtm-graph-health, gtm-dream, gtm-wrap-up]
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Rewritten to the Memory 2.0 shared contract. The default run writes one dated record. It reads the Graph Health and Dream scores by name, lists open continuation notes from Wrap-Up, and writes null with a reason for every measure it did not check."
---

# Weekly Review

## Overview

Weekly Review answers one question once a week: **what did we promise last week, what actually happened, and what is the shape of our system right now?** It reads last week's record first, grades each priority from evidence, measures the knowledge base, the pipeline and the operations, and writes the result into a new dated file.

The skill runs six stages in a fixed order. It grades before it measures, because a grade given after the numbers is shaped by the numbers. It writes null for any measure it did not check, and it writes one record per run, named by the local date. Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Line the records up over a quarter and drift has nowhere to hide.

---

## Why This Skill Exists

Most teams review when something has already gone wrong. A review that fires only after a failure is a post-mortem, and by then the decision that caused the failure is weeks old. The published article *Memory That Compounds* makes the case for a standing weekly slot instead: a short review that asks what changed since last time and whether anything the team believes needs updating.

Three failures make a weekly review useless, and this skill is built against each one.

The first is grading from memory. A priority feels done because someone worked on it. The skill grades each priority from a file, a pull request, a command or a person who confirmed it, and it names that evidence on the line.

The second is a zero written for something nobody checked. A metric that was never measured, recorded as zero, travels into next week's plan as a fact, and the plan is built on it. The article's rule is that zero is a measurement and null is an absence. The skill writes null and gives the reason.

The third is a record that gets rewritten. If last week's file can change, the trend line that makes the reviews worth doing disappears, and nobody can say what the team believed a month ago. Records are dated and closed. A correction goes into the current record and says what was wrong.

---

## Role

You are the weekly reviewer for one knowledge base and one team's work. You read the record you wrote last time, grade what was promised, measure what you can check, and write the record that the next review will read. You refuse to:

- Grade a priority without evidence.
- Write a number nobody checked. You write null, with the reason.
- Edit any earlier record.
- Invent a priority or a next action the owner did not give you.
- Set a priority that nobody can check later.

Each refusal follows from a Hard Rule below, and each Hard Rule states its reason.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Last week's record | Required, except on the first run | Read first, before any measurement. On the first run, ask the owner to confirm this is the first record. Then continue, with the deltas written as a dash |
| The record folder | Required | The folder where dated records are kept. Set in the profile's `## Weekly Review` section. Ask if it is not set |
| Today's local calendar date | Required | Taken from the owner's machine clock, or stated by the owner. Never the UTC date (Hard Rule 3) |
| Latest Graph Health report | Optional | Source of the structure fields. Without it, those fields are null |
| Latest Dream log | Optional | Source of the content count, its band and the next run date. Without it, those fields are null |
| Items written this week | Optional | The count Ingest records for the week. Without it, `items_written` is null |
| Open continuation notes | Optional | Written by Wrap-Up. Without them, the attention section says the lookup did not run, and why |

---

## Output Contract

The record is one Markdown file per run. Its name is the local date, `YYYY-MM-DD.md`, and it sits in the record folder. Its frontmatter carries the fields below, in this order. Other skills read them by name, so the names do not change.

| Field | Meaning | Null allowed |
|-------|---------|--------------|
| `skill` | The name of this skill, `weekly-review` | No |
| `type` | Always `weekly-review` | No |
| `week_ending` | The local date of the run. It matches the file name | No |
| `structure_score` | The Graph Health structure score, from 0 to 100 | Yes |
| `content_count` | The Dream content count from the latest dream log, from 0 to 100. This is Dream's after-run value, the score the base had when Dream finished | Yes |
| `items_archived` | The count Dream archived in its latest run. Zero when Dream ran and archived nothing, null when Dream did not run that week | Yes |
| `tag_sprawl` | Three parts written together: `rate`, `single` and `total`. The rate is the share of unique tags used only once, written as a whole number, so 10 means 10% | Yes, all three parts together |
| `orphans` | Items with fewer than three links | Yes |
| `hubs` | Items with more than ten links | Yes |
| `emergent_past_30` | Emergent items aged 31 to 60 days, counted from `updated`. Items past 60 days are not counted here | Yes |
| `emergent_past_60` | Emergent items aged over 60 days, counted from `updated`. The two emergent fields never overlap | Yes |
| `broken_links` | Links that point at nothing | Yes |
| `items_written` | Items written this week, as new items or dated entries added to existing ones | Yes |
| `expiring_soon` | Items whose `valid_until` falls within three days of the run | Yes |
| `carried_over` | Last week's priorities that were graded not done and move into next week | Yes |
| `uncommitted_repos` | Repositories holding work that is not yet saved to the remote copy | Yes |

Two markers carry the meaning of an unchecked value:

- **`null`** means the measure was not checked. Every null has its reason beside it, as a comment on the same line, such as `# not checked: no Graph Health report in the record folder`.
- **A dash (`-`)** means there is no baseline to compare with. It appears only in the delta column of the body table. It is not a zero and it is not a null. A dash is used on the first record, and on a measure that had no value last week.

The body has four sections, in this order:

1. **Carried Over.** Last week's priorities, each with its grade and its evidence. The priorities that carry forward are marked.
2. **System Health.** The metrics table, with this week's value, last week's value, the delta and the source or n for each row.
3. **What Needs Attention.** Only the items that need a decision. Healthy items are not listed.
4. **Next Week.** At most one priority per area, each with its check.

---

## Context

The skill reads these, in this order:

1. The newest dated record in the record folder that is earlier than today's date. This is last week's record.
2. The latest Graph Health report and Dream log, from the record folder or from the place the owner names.
3. Open continuation notes from Wrap-Up, from the folder where the owner keeps them.
4. The `## Weekly Review` section of `profiles/client-profile.md`. It records where records live, the review day, the areas in use, which measures can be checked and who reads the record. The companion CUSTOMIZE file writes this section.
5. The knowledge base, only for claims that carry re-grade dates and for open bets, and only when the base holds claims.

If the profile has no `## Weekly Review` section, say so once at the start of the run. Then use the defaults in the CUSTOMIZE file, list the areas you are assuming, and continue. If a read fails, follow the degradation table in Troubleshooting. A failed read never stops the review.

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

The order is fixed. Stage 1 reads last week's record before anything is measured, so grading uses what was promised, not what the system shows now. Stage 3 measures after Stage 2 has graded, for the same reason.

### Stage 1. Read Last Week's Record

Find the newest dated file in the record folder that is earlier than today's date. Read its priorities, its numbers and its Next Week section. Keep its file name, because the new record cites it.

*Why first:* the priorities were written before this week happened. If the numbers are read first, the grades drift toward whatever the numbers suggest.

**Produces:** last week's priority list and last week's numbers, with the file name they came from.

### Stage 2. Grade Last Week

Grade each priority as one of three words:

- **Done.** The evidence shows the checkable outcome the priority named.
- **Not done.** The outcome is not there. The line says what was looked for and where.
- **Overtaken.** Something happened that made the plan irrelevant. The line names the event and where it is recorded.

Overtaken is a real category. A plan that became irrelevant is different from a plan that failed, and the team should learn which of the two it is dealing with.

Each grade names its evidence: a file path, a pull request, the output of a command, or a person who confirmed the outcome. A grade with no evidence is a feeling, and a feeling carried into the next plan becomes a fact. If nothing can be looked at, do not guess a grade. Ask the owner for it, and record the owner's word with the source "owner".

**Produces:** the graded list, one line per priority, each with its evidence.

### Stage 3. Measure System Health

Take each measure in the table below. Where a measure was not checked, write null and the reason. Where a measure has no baseline, write a dash in the delta column.

| Area | Measure | Source | Rule |
|------|---------|--------|------|
| Knowledge base | The seven Graph Health fields, the structure band, the Dream content count and band, and the next Dream run date | Graph Health report and Dream log | Copied as written, with the report's date beside them |
| Knowledge base | Items written this week | Ingest's count for the week | A count, never an estimate |
| Knowledge base | Items expiring within three days | The `valid_until` field on each item | Counted on the run date |
| Pipeline | Work items in progress, and work items blocked | The team's own list, named in the record | Each count is written with the list it came from |
| Operations | Repositories with uncommitted work | A status check on each repository | Each repository named, or the count is null |
| Operations | Dashboards not refreshed in over 30 days | The dashboard's last refresh date | Each dashboard named with its date |
| Operations | Skills whose frontmatter misses a required field | The frontmatter of each skill | Required fields are the ones the team's skill standard names |
| Operations | Published counts rechecked against their source | The source named beside the count | A count with no source is marked unverified |

The measures are chosen so that every number can be traced to the report it came from. A number with no traceable source is not a measure, so it is written as null.

**Produces:** the metrics table, with this week's value, last week's value, the delta, the source and the n for each row, plus the null reason where a row was not checked.

### Stage 4. Flag Only What Needs Attention

Healthy items are not listed. A list of everything teaches the owner to skip the list, and then the one line that matters is skipped too. Apply these rules:

- **Carried over.** 0 or 1 is Fine and is not listed. 2 is Watch and is listed. 3 or more is Problem and is listed first. One carried priority is normal churn. Two means the team is starting to repeat itself. Three means the plan is not being carried out.
- **Tag sprawl.** Healthy (under 20%) is not listed. Warning (20 to 40, both ends included) is listed with its n. Unhealthy (over 40) is listed with its n. These are Graph Health's labels, so one word means one thing in both reports.
- **Structure band.** Excellent and Good are not listed. Fair and Poor are listed, because Dream runs when the structure score falls to Fair or below, and the owner should know it is due.
- **Open continuation notes older than a week.** Listed with their next action, quoted exactly as the note wrote it, and with the date the note was written.
- **Decisions still open.** Each decision Graph Health or Dream returned to the owner that has no answer yet.
- **Claims and bets, when the base holds claims.** Claims past their re-grade date, and open bets older than a month.

If a check ran and found nothing to flag, write that the check ran and found nothing. That is a finding. An empty section with no words in it looks the same as a check that never ran.

**Produces:** the attention list, one line per item, each with the source it came from.

### Stage 5. Set Next Week's Priorities

Write at most one priority per area: knowledge, content, operations and client work. An area the team does not use is left out, and the profile says which areas are in use. An area in use with no priority this week says so in words.

Each priority must pass these tests:

- It starts with a verb and names one object.
- It is a single step, not a project.
- It can be checked later by a file, a pull request, a person or a command, and the record says which one.
- It carries the date it is due, or the event that will close it.

Deliverables due in the next two weeks are listed with their next step. People appear by role in any record others will read. If the owner has not named a priority for an area, leave the area empty and say so. Do not fill it.

*Why the checkpoint matters:* a priority with no checkpoint rolls forward indefinitely. "Make progress on the migration" can never be checked. "Migrate the plot maps for the first site, checked by the import log" can.

**Produces:** the next-week priorities, at most one per area, each with its check and its due date or closing event.

### Stage 6. Write the Record

Show the owner the draft record. Write the file after the owner says yes. The file is named by the local calendar date. A second run on the same day replaces that day's file. Prior records are never edited. A correction goes into this week's record, as a line that says what was wrong and which record it corrects.

*Why the owner sees it first:* other people will read this record, and a wrong priority in it will be graded against later.

**Produces:** the record path, shown to the owner after the write.

---

## Modes

- **Full review (default).** Runs Stages 1 to 6 and writes the dated record after the owner's yes. This is the mode the weekly cadence uses.
- **Read-only review.** Runs Stages 1 to 5 and reports the result in the chat. It writes nothing, not even a draft file. Use it to look at a week before committing to it, or when the record folder cannot be written to.

Only the full review writes, and it writes one file: the dated record. It never changes the knowledge base, the continuation notes or any earlier record.

---

## Epistemic Rules

- **n beside every rate.** Write "tag sprawl 10% (6 of 61 tags)", never "10%" on its own. The n tells the reader how much weight the rate can bear.
- **Silence is not a no.** A check nobody ran is null. Zero is reserved for a check that ran and found nothing. The two look identical in a table, which is why the rule exists.
- **Confirm before flag.** A search hit is a candidate. Open the item before listing it under attention. One false line in a weekly record gets acted on by someone who trusts the record.
- **Effort is not an outcome.** Work done on a priority does not make the priority done. Grade the outcome the priority named.
- **Report the number that looks worse.** A rising measure is shown with its delta and its n. It is not explained away in the same sentence.

---

## Hard Rules

1. **Records are never edited.** Each record is evidence of what the team knew on that date. Edit one and the trend line lies. A correction goes into the current record and says what was wrong.
2. **Null is not zero.** A zero says somebody looked and found nothing. A null says nobody looked. A metric written as zero when it was never measured becomes a fact that the next plan is built on.
3. **The local date, never the UTC date.** The file name and `week_ending` use the owner's local calendar date. The UTC date can move a Friday evening run onto the next day's file, which files the record in the wrong week.
4. **Never write a number nobody checked.** This is Rule 2 stated as the thing the skill refuses to do. A table full of unchecked numbers looks like a finished review, and nobody can see which numbers are guesses.
5. **Grade from evidence, every time.** A grade from memory is the most common way a plan looks finished when it is not. The evidence goes on the line, so the owner can check it in a minute.
6. **Never invent a priority or a next action.** The owner sets them. A priority the team never agreed to will be graded against later, and the grade will mean nothing.
7. **Every priority is checkable later.** A priority with no checkpoint rolls forward forever, and the review cannot tell whether it was done.
8. **Names as roles in any record others will read.** A shared record is read by people who were not in the room. A role keeps the record useful to them without saying who did what. A name is used only in a record that stays private to the owner.

---

## Quality Bar

A weekly record is done when all of these are true:

- [ ] Last week's record was read first, and its file name appears in the new record.
- [ ] Every priority from last week has a grade of done, not done or overtaken, and each grade names its evidence.
- [ ] Every measure in the System Health table has a value, a null with its reason, or a dash where there is no baseline.
- [ ] Every rate shows its n.
- [ ] Every null has its reason on the same line.
- [ ] Each band label comes from the band rules in Stage 4, and every value falls in exactly one band.
- [ ] Healthy items are absent from What Needs Attention, and every item that is listed names its source.
- [ ] Next Week has at most one priority per area, and each priority names its check and its due date or closing event.
- [ ] The file name is the local calendar date, and `week_ending` matches it.
- [ ] No earlier record was edited.
- [ ] The owner saw the draft before the write.

---

## Examples

The examples use the shared PlotIQ chain. Every name comes from the PlotIQ example cast. Every figure is either from the chain, which is labelled illustrative, or cited to the published article *Memory That Compounds*. Neither example is a real result for any company.

### Example 1. The Friday Record, Illustrative

**Run date:** Friday 2026-10-23, local time. The previous record is `2026-10-16.md`, and it is not edited by this run. The Graph Health report is dated 2026-10-19, and the Dream log is dated 2026-10-19.

**Carried Over.** Last week's priorities, graded:

- **Ingest the Brackhaven call and set the renewal expiry.** Done. Evidence: the account item, opened and checked.
- **Draft the Greyfield displacement sequence.** Overtaken. Greyfield paused until its January renewal, according to the Greyfield item's timeline.
- **Run the dashboard freshness check.** Not done, and its measure is null. Nobody ran it this week, so the reason is recorded. It carries into Next Week, under Operations.

The record carries one priority forward, so `carried_over` is 1, which is Fine. It is not listed as a problem.

**System Health.** This illustration shows the knowledge base rows. The 2026-10-16 record is not reproduced here, so the delta column is left out. A real record fills it in.

| Measure | This Week | Source |
|---------|-----------|--------|
| Structure score | 71, Good | Graph Health, 2026-10-19 |
| Tag sprawl | 10% (6 of 61 tags), Healthy | Graph Health, 2026-10-19 |
| Orphans | 9 (9 of 134 items, 7%) | Graph Health, 2026-10-19 |
| Hubs | 1 | Graph Health, 2026-10-19 |
| Emergent past 30 days | 2 | Graph Health, 2026-10-19 |
| Emergent past 60 days | 3 | Graph Health, 2026-10-19 |
| Broken links | 0 (0 of 134 items) | Graph Health, 2026-10-19 |
| Content count | 75, Good | Dream, 2026-10-19 |
| Next Dream run | 2026-11-02 | Dream, 2026-10-19 |
| Items written this week | 5 (two new items, three dated entries added to existing items) | Ingest |
| Items expiring within three days | 1 (`SABLE_FORK_DEMO_REQUEST`, `valid_until` 2026-10-26) | Item `valid_until` fields |
| Uncommitted repositories | null | Not checked this week. The machine was away on Thursday and Friday |

The pipeline and operations rows that the chain does not record are left out of this illustration. The one operations measure it does record is `uncommitted_repos`, and it is null with its reason.

**What Needs Attention.** Five items, each with its source:

- The 9 orphan call notes are not linked to their account records. Decision for the owner: link or retire each one. Source: Graph Health, 2026-10-19.
- The Sable Fork demo request, `SABLE_FORK_DEMO_REQUEST`, expires 2026-10-26, three days from this run. Source: the item's `valid_until` field.
- The Greyfield note, `GREYFIELD_STONEMARK_RENEWAL_NOTE`, expired 2026-10-21, two days before this run. Dream archives it or offers an extension on its next run. Source: Dream, 2026-10-19, and the item's `valid_until` field.
- Two items disagree on the Stonemark pricing. The dated one is `STONEMARK_MAPPING_PRICING`, updated 2026-09-02, and it says Stonemark charges per site. The undated one is `STONEMARK_PRICING`, and it says per plot. The owner decides, and nothing has been merged. Source: Dream, 2026-10-19.
- The open continuation note for `plotiq-gtm`, dated 2026-10-13, has the next action "Send Ruth Ellery the migration plan draft before 2026-10-27." This record is private to the owner, so the name stays. Source: Wrap-Up note.

**Next Week.** At most one priority per area:

- **Knowledge.** Link the 9 orphan call notes to their account records. Check: the next Graph Health report shows the orphan count it measured.
- **Content.** No priority this week. The area is in use, and it has none.
- **Operations.** Run the dashboard freshness check and record the result. Check: this record's System Health table.
- **Client work.** Draft the Brackhaven migration plan for Ruth Ellery before 2026-10-27. Check: the draft file. In a shared record this line reads "the Brackhaven champion", because shared records use roles.

**The record's frontmatter, exactly as it is written:**

```yaml
structure_score: 71
content_count: 75
items_archived: 1         # the expired conference item, archived by Dream on approval
tag_sprawl: {rate: 10, single: 6, total: 61}
orphans: 9
hubs: 1
emergent_past_30: 2
emergent_past_60: 3
broken_links: 0
items_written: 5
expiring_soon: 1          # SABLE_FORK_DEMO_REQUEST, valid_until 2026-10-26
carried_over: 1
uncommitted_repos: null   # not checked: the machine was away Thursday and Friday
```

The record shows three kinds of line. One priority is done, with its evidence. One is overtaken, with the event that made it irrelevant. One is not done, and its measure is null with the reason. Both scores are recorded with their bands. There is one priority per area at most, and the open continuation note is listed with its next action.

### Example 2. A Second Run on the Same Day

Suppose the owner runs the review again later on 2026-10-23, after linking some of the orphan call notes.

The skill does not treat today's file as last week's record. Stage 1 looks for the newest file earlier than today, so it still reads `2026-10-16.md`, and its priorities are graded from that file again. Stage 3 re-runs the Graph Health report before any measure is copied, so the orphan count is recomputed from the new report. A null from the earlier run does not carry over unless its check fails again.

The new record replaces `2026-10-23.md`. The Carried Over section says that it replaces an earlier run from the same day. The `2026-10-16.md` record is not touched.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| The Graph Health report is not in the record folder | Graph Health was not run this cycle, or its report is kept somewhere else | Write the seven structure fields as null, each with the reason. Ask the owner where the report lives. Continue the review |
| The Dream log is missing or older than the latest Graph Health report | Dream has not run since the last change | Write the content count, its band and the next run date as null, with the reason. Ask whether Dream should run before the next review |
| Last week's record cannot be read | The file was moved, renamed or damaged | Ask the owner for last week's priorities. If none can be found, write the deltas as dashes and list "no prior record found" under What Needs Attention |
| The local date is unclear | The machine clock is off, or the owner is in a different time zone | Ask the owner for the local date. Never use the UTC date to fill the gap |
| A grade cannot be backed by evidence | The outcome happened but left no file, command or message | Ask the owner for the grade. Record the owner's word with the source "owner", so the reader can see where it came from |
| Two priorities were named for the same area | The owner gave two in one area | Keep the first one named, and ask the owner which one stays. Do not merge them |
| The owner wants a trend from one record | One record cannot show a direction | Say that one record shows a level and not a trend, and that a trend needs more weeks of records to read |
| The record folder cannot be written to | Permissions, or the folder does not exist yet | Run as a read-only review, show the record in the chat, and say the file was not written and why |

### Degradation Table

When a measure cannot be checked, the review does not stop. The measure becomes null, the reason is named, and the review continues.

| Measure | If It Fails | Written As | Reason Named |
|---------|-------------|-----------|--------------|
| `structure_score` and the other Graph Health fields | No Graph Health report for this run | null | "No Graph Health report in the record folder for this run" |
| `content_count` | No Dream log for this run | null | "No Dream log found for this run" |
| `tag_sprawl` | The report lacks one of its three counts | null, for all three parts | "Graph Health report does not give the single-use count" |
| `items_written` | Ingest's count is not available | null | "No Ingest count for this week" |
| `expiring_soon` | The `valid_until` fields cannot be read | null | "Item frontmatter could not be read" |
| `carried_over` | Last week's record cannot be read | null | "No prior record found" |
| `uncommitted_repos` | The repositories cannot be checked from this machine | null | "Repository status not checked on this machine this week" |
| Open continuation notes | The folder is not reachable | No count, and the section says the lookup did not run | "Continuation note folder not reachable" |

---

## Best Practices

- **Run it on the same day each week.** A fixed slot is the difference between a cadence and a reminder. The day is set in the profile so the whole team knows when the record arrives.
- **Grade before you measure.** If the numbers come first, the grades start to match them. Keep the order even when the numbers look interesting.
- **Keep the nulls visible.** A table with honest nulls is more useful than a table with guessed zeros, because the nulls show exactly what the team is not yet looking at.
- **Write each priority so a stranger could check it.** The test is whether someone who was not in the meeting could tell, from the file, whether it happened.
- **Read the last four records together, once a month.** One record shows a level. Several records in a row show a direction, and the direction is what the team should act on.
- **Keep names out of shared records.** Roles are enough for a reader to act. A name in a shared record starts a conversation the record was not written to have.

---

## Integration With Other Skills

**Reads from gtm-graph-health, by field name:** `structure_score`, `tag_sprawl` (its `rate`, `single` and `total` counts), `orphans`, `hubs`, `emergent_past_30`, `emergent_past_60` and `broken_links`. The structure band is read with the score. These seven fields are the hand-off that Graph Health writes for this review.

**Reads from gtm-dream, by field name:** `content_count`, `items_archived` and `next_run`, plus the content band. `content_count` is Dream's after-run value from its latest log. Dream's score is the content count, and it is never mixed with Graph Health's structure score.

**Reads from gtm-wrap-up, by field name:** the open continuation notes, each with `project`, `date`, `status` and `next_action`. A note with `status: draft` is listed as a draft, not as an approved next step.

**Reads from Ingest:** the count of items written this week, taken from Ingest's save reports, and the `valid_until` field on each item, which is used to count items expiring within three days.

**Fields this review writes from its own work, not from another skill's hand-off:** `week_ending` (the run date), `items_written` (counted from Ingest's save reports for the week), `expiring_soon` (counted from `valid_until` on the run date), `carried_over` (last week's priorities graded not done) and `uncommitted_repos` (checked by this review on the machine it runs on). Look for these in this review's own stages, not in the Graph Health, Dream or Wrap-Up hand-offs.

**Reads, when the base holds claims:** the re-grade date on each claim and the open bets node. Claims past their re-grade date, and open bets older than a month, go under What Needs Attention.

**Hands to the next Weekly Review:** the record itself. The next run reads this file by its date, and the field names above do not change.

**Next step:** run gtm-graph-health before the next review, because this review reads its numbers. When the next working session ends, close it with gtm-wrap-up, so the open notes this review reads exist.

---

## Changelog

### 2.0.0 (2026-10-18)

- Rewritten to the Memory 2.0 shared contract. The record format, the field names, the stale definition, the expiry model and the two score bands are the same ones the other memory skills use.
- The default run writes one dated record after the owner's yes. The read-only run reports in the chat and writes nothing.
- Every measure that was not checked is written as null with its reason. A dash marks a missing baseline, and it is never a zero.
- Adds the carried-over bands (Fine, Watch, Problem), the tag bands (Healthy, Warning, Unhealthy) and the degradation table, so a failed check no longer stops the review.
- Reads the Graph Health and Dream scores by field name, and lists open continuation notes from Wrap-Up.
