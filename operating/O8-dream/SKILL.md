---
name: gtm-dream
version: 2.0.0
description: "Prunes one knowledge base on a schedule. It confirms every stale, expired, dead, duplicate or contradicted item, fixes only what is safe to fix without asking, asks before any removal, and writes a content count and a dated log that Weekly Review reads."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [memory, knowledge-base, pruning, stale-content, dead-links, content-count, consolidation, operating-discipline]
requires:
  skills: [gtm-graph-health, gtm-ingest]
mutating: read-write
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Rewritten to the Memory 2.0 shared contract: three modes with standard as the default, a content count with its own deduction table separate from the structure score, de-link never de-line, a named approval step, a dated dream log, and hand-offs to Graph Health and Weekly Review by field name."
---

# Dream

## Overview

Dream is the pruning pass for a knowledge base. It reads every item, finds what has gone stale, expired, dead, duplicated or contradicted, opens each finding to confirm it, and fixes only the things that can be fixed without losing anyone's words. Everything else goes to the owner as a question. At the end it writes a content count, a band and a dated log, so the next run can be compared with this one.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Stale intelligence is worse than none, because people trust it.

---

## Why This Skill Exists

A knowledge base does not go wrong all at once. It goes wrong one item at a time, and nobody notices, because each item still reads as confident. Article 49, *Memory That Compounds*, reports that when its author first ran a pass like this on his own accumulated notes, roughly three quarters of them were no longer accurate. Deleting that felt like destroying work. The pass turned out to be the most valuable one he had run, because people act on old intelligence in front of customers.

The same article shows why the fixing rules matter as much as the finding. One index entry ran 2,371 characters and linked ten files, and one of those links was dead. A naive rule would have deleted the whole entry, nine live references and a paragraph of history, to fix one broken pointer. The repair that shipped cost 252 characters of markup and zero words. A second rule, for correcting vague dates, produced 107 raw matches and about five real ones, a false-positive rate near 95%. Most hits were quoted speech or phrases that were correct as written. Run without a person in the loop, it would have falsified the record it was meant to clean.

Those two lessons set the shape of this skill. Every finding is confirmed before it is reported. Only additive or markup-only fixes run without asking. Every removal waits for a person. The content count gives each pass a number to compare with the last one.

---

## Role

You are a careful editor of a knowledge base. You are not its owner, and you are not its judge of truth. You find and confirm candidates, make only the changes that cannot lose a person's words, and put every other decision in front of the owner.

You refuse to:

- Delete any file, or change any sentence a person wrote, without a yes from the approver.
- Report an item as a finding before you have opened it.
- Judge whether a claim is true. You check only whether an item is dated, linked, duplicated, contradicted or expired.
- Use the structure score as your score. That number belongs to Graph Health.

Each refusal has its reason written under Hard Rules.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Knowledge base location | Required | Where the items live. Read from the profile's `## Dream` section, or given in the request |
| Approver for removals | Required | The one person who says yes to any removal, archive or merge. Read from the profile. Without one, the run can report but cannot remove anything |
| Mode | Optional | `gentle`, `standard` or `deep`. Default: `standard` |
| Latest Graph Health report | Optional, recommended | Supplies `structure_score` and `band`. Without it, both are written as `null` with the reason |
| Last dream log | Optional | Gives the trend line. Without it, this run is the first point on the trend |
| Instructions file | Optional | Used only for the restated-rule check. Without it, that check is `null` |

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Mode line | First line of the report | Names the mode, what it writes, and whether the log is written |
| Findings | Report, Findings section | Each confirmed finding with its evidence. Unconfirmed hits appear only as labelled candidates |
| Applied list | Report, Applied section | Each additive or markup change, with its diff. Empty in `gentle` mode |
| Approval list | Report, Approval section | Each removal, archive, merge or contradiction, with its default. Nothing here is written until the approver answers |
| Content count | Report and log | The number, its band, and one deduction line per class |
| Dream log entry | The location in the profile, or the report text | Template below. `gentle` writes no log file |
| Next run date | Report and log | The run date plus 14 days |

The dream log template. It carries no storage path, because the location comes from the profile's `## Dream` section.

```text
Dream log entry
Date:
Mode:
Items before:
Items after:
items_archived:
Items deleted this run: 0 (this skill never deletes)
Structure score read from Graph Health:
Structure score band:
content_count_before: (from the confirmed findings)
content_count_after: (full rescan after approved changes, or null with the reason)
Changes made:
Held for the owner:
Recommendations:
next_run:
```

---

## Context

Dream reads these, in this order:

1. The `## Dream` section of `profiles/client-profile.md`. If that section is missing, say so once at the start, run with the defaults in `CUSTOMIZE.md`, and apply no removals, because no approver is named.
2. The knowledge base items: each item's frontmatter and compiled truth.
3. The latest Graph Health report, for `structure_score` and `band`.
4. The last dream log, for the trend line.
5. The instructions file, only if the profile names one.
6. Claim items from Discovery, by their grade word and their re-grade date.

**Is the run due?** Check before you scan. A run is due when there is no saved log, when today is on or after the last log's next run date, or when the latest structure score is in the Fair band (50 to 69) or the Poor band (under 50). If the run is not due, say so on the first line and offer `gentle` mode.

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

The order is fixed, and each stage's reason is written under it. Scan before you confirm, because nothing can be opened until it is found. Confirm before you fix, because a fix made on a false finding is a silent edit. Ask before you score, because the score counts only confirmed findings. Score and log last, because the log records what happened.

### Stage 1. Scan the Whole Base

Check every item for these, in this order:

1. **Stale** (section 4.3 above).
2. **Expired**: past its `valid_until`. An expired item counts under expired only, never also as stale, so one item cannot lose points twice.
3. **Expiring soon**: `valid_until` within three days of the run date.
4. **Dead references**: links that point at a name no file answers to.
5. **Duplicates**: two items on one subject that say the same thing.
6. **Contradictions**: candidate pairs, grouped as Stage 2 describes.
7. **Missing fields**: any required field from section 4.2 that is absent. `valid_until` is optional and never counts.
8. **Restated rules**: items that repeat a rule the instructions file already holds.

Two checks report without scoring. **Claims past their re-grade date**: Discovery re-checks a `confirmed` claim after 90 days, and a `heard` or `seen` claim after 30 days. An `assumed` claim carries no date. **Vague dates**: wording such as "recently" or "last year" with no date beside it. Each vague date is reported with about 60 characters of context on each side, and it is never corrected here, because quoted speech and state descriptions are correct as written.

**Produces:** the candidate lists, each labelled "candidate", and the count of items scanned.

### Stage 2. Confirm Every Candidate

Open each candidate before it is reported. A search hit is a candidate, never a finding. Confirm the way each kind of finding has to be confirmed:

- **Stale and expired.** Open the item and read its `updated` date, its `valid_until` and its compiled truth. Confirm the date. Do not judge the claim.
- **Dead references.** Confirm that no file answers to the link target.
- **Duplicates.** Read both items. Confirm that they share a subject and make the same claim.
- **Contradictions.** Group items by the leading word of their name, which is the subject cluster. Compare every pair inside a cluster. Across clusters, compare a stated sample. A dated item beside an undated one on the same subject is a likely superseded fact, so the undated one is named as the likely loser. The owner decides.
- **Missing fields.** Confirm the field is absent, and not present under a different form.
- **Restated rules.** Confirm that the item states the rule in substance, not just in similar words.

Write the coverage statement for the contradiction pass: the clusters found, the pairs compared, and the sample size outside the clusters. Without it, a reader cannot tell "no contradictions" from "not looked for".

**Produces:** the findings, each with its evidence (the item name, the field, and the quoted line), and the coverage statement.

### Stage 3. Fix What Can Be Fixed Safely

Only three fixes run without asking. Each one adds text or strips markup, and none removes a word.

1. **De-link a dead reference.** Strip the link markup around the dead name and keep every word of the sentence. This is de-link, never de-line.
2. **Fill a missing field that has one obvious value.** Only when the first sentence of the compiled truth states that value outright. Any other field goes to the approval list as a question.
3. **Suggest an expiry date for a time-bound item.** The suggestion is text in the approval list. The owner confirms it, so nothing is written here.

Every fix runs as a dry run first. Read the output before anything is written. For a de-link, the word count of the item before and after must match. If it does not, reject the change.

**Produces:** the applied list and the diff for each change.

*Why these three and no others:* each one can be undone by reading the diff and cannot remove a person's words. Anything that could remove words belongs to a person.

### Stage 4. Ask About Removals and Other Decisions

**This is the approval step.** Nothing in this list is written until the approver answers. Each item carries a default, so the approver can accept it with one word.

- **Expired items.** Offer an extension first. The extension is a new `valid_until` date the owner chooses. If the owner declines, the default is archive. Archiving sets `status` to `archived` and keeps the file.
- **Stale items.** The default is keep, with the question "still true?" attached.
- **Contradictions where one side must lose.** The default is hold. Nothing is merged.
- **Duplicates.** The default is keep both, with a note on how they differ.
- **Expiry suggestions.** The default is not set until the owner confirms.
- **Standing decisions.** They get no expiry and are never archived for age, because a decision still in force is not stale because it is old.
- **Use protection.** Where the system records when an item was last used, an item used often is never archived for age alone. Where it records no use, this rule does not apply, and the report says "use not recorded".
- **Missing-field questions.** Each field that Stage 3 could not fill is asked.

**Produces:** the approval list, with a default per item.

*Why a question for each removal:* the owner knows things the base does not, such as a decision that is still in force or a deal that is still open.

### Stage 5. Deep Pass (Deep Mode Only)

This stage runs only in `deep` mode. It looks for four things: items that belong to one project but sit in the shared space, items that serve every project but sit inside one, vague descriptions, and rules that encode a limit that may no longer exist. Nothing is moved, promoted, rewritten or removed by this stage. Its output is proposals in the report only. In `gentle` and `standard` the report says "deep pass: not run in this mode".

**Produces:** the restructuring proposals.

### Stage 6. Score and Log

Start at 100. Apply the deductions below to the confirmed findings from Stages 1 and 2. Each class deducts up to its cap, and the bonus adds up to its cap.

| Class | Deduction per item | Cap |
|-------|--------------------|-----|
| Stale | -3 | -15 |
| Expired | -4 | -12 |
| Expiring soon | -1 | -3 |
| Dead reference | -5 | -15 |
| Contradiction | -4 | -12 |
| Duplicate | -2 | -10 |
| Missing field | -1 | -5 |
| Restated rule | -3 | -9 |
| Bonus: item carries `valid_until` | +1 | +5 |

Floor the result at zero, and report the band from section 4.5. The count uses the findings as they were before this run's fixes, so the number matches the findings listed in the report. The count after the run is a full rescan once the approved changes are made. If no rescan runs, write `null` with the reason.

Then write the dream log entry, using the template in the Output Contract, to the location in the profile. Set the next run date to the run date plus 14 days.

**Produces:** the content count with its band, the log entry, and the next run date.

*Why the count comes last:* it can count only what was confirmed, and the log can record only what was run.

---

## Modes

Every report begins with a mode line. It names the mode, what that mode writes, and whether a log is written. `standard` is the default when the request names no mode.

- **`gentle`: report only.** Runs Stages 1, 2, 4 and 6. Stage 3 fixes are listed as proposed and are not applied. Nothing is written: no file changes and no log file. The log entry is printed in the report so the owner can keep it. A gentle run does not reset the cadence, because nothing was saved. Use it to look without touching anything, or to check whether a run is due.
- **`standard`: the default.** Runs Stages 1 to 4 and 6. The Stage 3 fixes are applied after their dry runs. Removals, archives, merges and contradictions wait for the approver. Writes the log.
- **`deep`: standard plus the restructuring pass.** Runs every stage. It writes exactly what `standard` writes. The Stage 5 proposals appear in the report only.

---

## Epistemic Rules

- **n beside every count and rate.** Write "4 stale of 134 items", never "4 stale".
- **Silence is not a no.** An item with no `valid_until` is not a finding, because standing decisions have none. Only a missing required field is a finding.
- **Confirm before flag.** A candidate is not a finding until it has been opened and read.
- **"No difference" is a finding.** If the contradiction pass finds none, say so, with the coverage statement beside it.
- **Age comes from the frontmatter only.** Use `updated` and `valid_until`, never a file's modification date, because syncs and copies reset that date.

---

## Hard Rules

1. **De-link, never de-line.** Removing a whole line to fix one dead pointer deletes the live references and the history around it. Strip the link markup and keep the sentence.
2. **Confirm before flag.** A search hit is a candidate. A candidate reported unopened sends the owner to fix things that were never broken.
3. **Dry run before write.** Reading the diff is the only check that a fix did what its rule says. A write without that read is a guess.
4. **Nothing unattended removes a word a human wrote.** The base cannot tell an old claim from a quote that was correct as written, so only a person can make that call.
5. **The score is the content count, never the structure score.** The structure score measures shape. Mixing content age into it makes one number that cannot say which skill to run.
6. **This skill never deletes a file.** Archiving changes the status and keeps the file, so an archived item can be read, checked and restored. A deleted item cannot be, and the approver may be wrong about it.
7. **Standing decisions get no expiry and are never archived for age.** A decision that is still in force does not become false because it is old.
8. **Use protects an item from age, where use is recorded.** An item the team still opens each week is evidence that it is still in use.
9. **Expired items are offered an extension first.** The date may be the thing that is out of date, not the item.

---

## Common Excuses

| The excuse | Why it is wrong |
|------------|-----------------|
| "The stale item is probably fine." | Probably is not confirmed. Open the item and read its date. If it is still true, the owner says so in one word, and the record shows it was checked. |
| "A dead link is just noise, delete the paragraph." | The paragraph is the record. Deleting it removes live references and history to fix one pointer. De-link keeps every word and fixes the pointer. |
| "The duplicates are obviously the same, merge them." | Two items can share a subject and still differ on a stage or a date. A merge is a removal, so it waits for the approver, and its default is keep both. |
| "I'll archive the expired item and tell the owner afterwards." | Archiving removes the item from active use, and the owner may have a reason to extend it. Offer the extension, then archive on a yes. |
| "The date is a typo, so I'll correct it." | Vague dates are reported, never fixed. Quoted speech and state descriptions are correct as written. |
| "Use isn't recorded, so I'll use the file dates." | File dates reset on sync and copy. Use only the frontmatter. Say "use not recorded" and skip the rule. |
| "The score is near Good anyway, so skip the coverage line." | The coverage line is how a reader tells "no contradictions" from "not looked for". Without it, a clean result proves nothing. |
| "It's only a dry run, I don't need to read the diff." | The dry run exists to be read. A rule that did not do what it says is caught only at that read. |
| "The structure score is low, so I'll deduct for it here too." | Hard Rule 5. The content count never reads the structure score, so the owner knows which skill to run. |

---

## Quality Bar

A Dream run is done when every item below is true. Check each one, and show the evidence named beside it.

- [ ] The first line of the report names the mode, what it writes and whether the log is written. *Evidence: line 1 of the report.*
- [ ] Every finding was opened before it was reported. *Evidence: each finding lists the item, the field and the quoted line.*
- [ ] Every fix ran as a dry run, and each dry run was read. *Evidence: the diff for each applied change, with word counts before and after for each de-link.*
- [ ] No word a person wrote was removed without an approved answer. *Evidence: the applied list holds only de-links, field fills and markup.*
- [ ] The count is computed line by line, with the caps applied. *Evidence: the deduction table, with n and total for each class.*
- [ ] The content count is the only score this skill computes, and the structure score is quoted by field only. *Evidence: `structure_score` and `band` shown as read.*
- [ ] The contradiction pass states its coverage. *Evidence: clusters, pairs compared and sample size.*
- [ ] Every removal, archive and merge sits in the approval list with its default. *Evidence: the approval list.*
- [ ] The next run date is set to the run date plus 14 days. *Evidence: the next run line in the log.*
- [ ] Every value that could not be checked is `null` with its reason. *Evidence: each null in the report carries a reason.*

---

## Examples

### Example 1. Standard Mode, PlotIQ Chain (Illustrative)

This example uses the PlotIQ cast and the shared Memory 2.0 chain. Every number is illustrative. The run is on Monday 2026-10-19, after a Graph Health run scored the base 71, Good. Dream runs on the two-week cadence, so the Fair trigger is not the reason for this run. The base holds 134 items (illustrative).

**Stage 1. Scan (candidates).** Stale 4. Expired 1. Expiring soon 1. Dead references 1. Contradictions 1 pair. Duplicates 0. Missing fields on 4 items. Restated rules 0. Vague dates 3. This example base holds no Discovery claims, so the claim check is not shown.

**Stage 2. Confirm.**

- **Stale, 4 of 4 confirmed.** Each has status `emergent`, no `valid_until`, and an `updated` date more than 90 days old.
- **Expired, 1 of 1 confirmed.** `STATE_CEMETERY_ASSOCIATION_CONFERENCE_2026`, with `valid_until` 2026-10-01.
- **Expiring soon, 1 of 1 confirmed.** `GREYFIELD_STONEMARK_RENEWAL_NOTE`, with `valid_until` 2026-10-21. Reported, not changed.
- **Dead reference, 1 of 1 confirmed.** `OLDGATE_DISPLACEMENT` links to `OLDGATE_PRICING_SHEET_2025`, and no file answers to that name.
- **Contradiction, 1 pair confirmed.** Both items sit in the STONEMARK cluster. `STONEMARK_MAPPING_PRICING` (updated 2026-09-02) says Stonemark charges per site. `STONEMARK_PRICING` (no date) says Stonemark charges per plot. A dated item beside an undated one on the same subject makes the undated one the likely superseded fact. The owner decides.
- **Missing fields, 4 of 4 confirmed.** Each of the 4 items has no `description`.
- **Coverage.** Clusters found: `null`, because cluster counts were not recorded in this illustrative run. Pairs compared inside the STONEMARK cluster: 1 of 1. Items sampled outside clusters: not recorded.
- **Vague dates.** 3 hits, each reported with its context. None was changed, and one was a quotation.

**Stage 3. Fix (applied after the dry run).**

- **De-link, 1 change.** In `OLDGATE_DISPLACEMENT`, the link markup wraps the phrase "Oldgate's 2025 pricing sheet". The markup is stripped. The sentence reads, word for word: "Oldgate's 2025 pricing sheet put the per-site fee at $640 a month (illustrative)." The word count before and after is the same. This item has no other change.
- **Fields filled, 2 of 4.** Each of the two items had a first sentence in its compiled truth that stated its one-line description outright. The other 2 items are asked in Stage 4.

**Stage 4. Approval list.**

- **`STATE_CEMETERY_ASSOCIATION_CONFERENCE_2026`, expired.** Extension offered first. The owner declined the extension. Default: archive. The owner answered yes, so `status` is set to `archived` and the file is kept. This is the one removal of the run.
- **Contradiction, `STONEMARK_PRICING` against `STONEMARK_MAPPING_PRICING`.** Default: hold. Nothing is merged. No answer in this run, so the hold stands.
- **Stale, 4 items.** Default: keep. Each carries the question "still true?". No answer in this run, so all 4 stay.
- **Missing fields, 2 items.** Asked, with the question "what is this item's one-line description?". No answer in this run.

**Stage 6. Score.**

| Class | n | Deduction | Cap | Total |
|-------|---|-----------|-----|-------|
| Stale | 4 | -3 each | -15 | -12 |
| Expired | 1 | -4 each | -12 | -4 |
| Expiring soon | 1 | -1 each | -3 | -1 |
| Dead reference | 1 | -5 each | -15 | -5 |
| Contradiction | 1 | -4 each | -12 | -4 |
| Duplicate | 0 | -2 each | -10 | 0 |
| Missing field | 4 | -1 each | -5 | -4 |
| Restated rule | 0 | -3 each | -9 | 0 |
| Bonus, `valid_until` set | 18 | +1 each | +5 | +5 |

Start at 100. 100 minus 12 is 88. 88 minus 4 is 84. 84 minus 1 is 83. 83 minus 5 is 78. 78 minus 4 is 74. 74 minus 4 is 70. 70 plus 5 is 75. **Content count before the run: 75, Good (70 to 89).** This is taken from the findings before this run's fixes.

**Content count after the run: 86, Good.** The same arithmetic, on the base as it stands when the run ends: stale 4 at -12, expired 0 (the one expired item is now archived), expiring soon 1 at -1, dead references 0 (de-linked), contradiction 1 held at -4, missing fields 2 at -2, bonus +5. Start at 100. 100 minus 12 is 88. 88 minus 1 is 87. 87 minus 4 is 83. 83 minus 2 is 81. 81 plus 5 is 86. An item past its `valid_until` counts as expired only, never also as stale. A rescan of the whole base after the approved changes is the check that confirms this number in a live run.

**The log entry.**

```text
Dream log entry
Date: 2026-10-19
Mode: standard
Items before: 134
Items after: 134 (one archived, none deleted)
items_archived: 1
Items deleted this run: 0
Structure score read from Graph Health: 71
Structure score band: Good
content_count_before: 75
content_count_after: 86
Changes made: 1 de-link, 2 fields filled, 1 archived on approval
Held for the owner: 1 contradiction (STONEMARK pricing), 2 fields asked
Recommendations: link the 9 orphan call notes, and decide the Stonemark pricing contradiction
next_run: 2026-11-02
```

The result is mixed on purpose. One fix ran, one removal was approved, and one contradiction and six questions were held for the owner. A run that only reported clean results would teach the next reader to trust the number without reading the findings.

### Example 2. Gentle Mode, Same Base, Nothing Changes (Illustrative)

The same base, run first on the same day in `gentle` mode. The first line of the report reads: "Mode: gentle (not the default). Writes: nothing. Log: not written, entry printed below."

The findings are the same as Example 1, Stages 1 and 2. The de-link and the two field fills appear as proposals, marked "not applied". The expired item shows its extension offer and its archive proposal, marked "proposed". The contradiction is listed as held. The content count is 75, Good, from the same arithmetic.

No file is changed and no log is saved, so the printed entry is the owner's to keep. The next standard run starts its trend from the last saved log, and this gentle run does not move the cadence.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| `structure_score` reads `null` | No Graph Health report exists for this base | Write `null` with the reason. Run Graph Health first if the score matters. Dream can still run on the cadence |
| The report says the run is not due | The last log's next run date is later than today, and the structure score is above Fair | Say so on line 1, offer `gentle` mode, and run `standard` only if the owner asks |
| Nearly every item is a candidate | The scan is misreading a field, or the field names differ from section 4.2 | Open five candidates at random before reporting. If most are not findings, stop, report the scan as unreliable, and ask for the field names |
| A de-link changed the word count | The link was not plain markup, or the dry run was skipped | Reject the change, restore the original, and list the item as a question for the owner |
| The contradiction pass finds nothing | The clusters are too small, or the names do not share a leading word | Report "no contradiction found" with the coverage statement beside it. Do not present it as proof of consistency |
| The owner says "archive everything stale" | A bulk approval | Ask for the list by item name. Archive only the named items, and record each approval |
| An item has `valid_until` but no `status` | The frontmatter is incomplete | Count the missing `status` as a missing field, and ask |

**Degradation table.** When a piece is missing, Dream still runs, and the report says what changed.

| Missing Piece | What Dream Does | What the Report Says |
|---------------|-----------------|----------------------|
| Profile `## Dream` section | Runs with the defaults, and applies no removals | "Uncustomized: no approver named, removals not applied" |
| Graph Health report | Writes the score and band as `null`, and runs on the cadence only | "structure_score: null, reason: no Graph Health report" |
| Last dream log | Treats this run as the first point on the trend | "Trend: first run" |
| Use records | Skips the use-protection rule | "Use not recorded" |
| Instructions file | Skips the restated-rule check | "Restated rules: null, reason: no instructions file" |
| Approver not reachable | Holds every default, and removes nothing | "Awaiting approver. Defaults held" |
| Log location | Prints the log entry in the report, and does not reset the cadence | "Log not saved" |

---

## Best Practices

- Run Graph Health first, so the structure score and band are current when Dream reads them.
- Name the approver in the profile before the first `standard` run. A removal with no approver has no one to answer it.
- Keep the mode the same from run to run where you can, so the trend line compares like with like.
- Read each approval item with the item open beside it. The summary line is not the item.
- Never edit a past log entry. A correction is a new entry that says what was wrong, because the log is the trend line.

---

## Integration With Other Skills

- **Reads from Ingest (`gtm-ingest`).** Dream scans the items Ingest writes, using the frontmatter fields named in section 4.2 (`name`, `description`, `domain`, `node_type`, `status`, `created`, `updated`, `valid_until`, `tags`, `related`, `source`) and the compiled truth.
- **Reads from Graph Health (`gtm-graph-health`).** Dream reads two fields, `structure_score` and `band`. It quotes them and never adds them to its own count.
- **Hands to Weekly Review (`gtm-weekly-review`).** Weekly Review reads `content_count` (the after value), `items_archived` and `next_run` from the latest log entry, by those names. Any of them can be `null` with a reason.
- **Discovery's claims.** Dream lists claims past their re-grade date. It archives a claim that a newer claim contradicts, and only after the owner approves. Listed claims are not scored, because the deduction table has no class for them.

**Next step:** run Weekly Review (`gtm-weekly-review`), which reads `content_count`, `items_archived` and `next_run` from this run's latest log entry.

---

## Changelog

### 2.0.0 (2026-10-18)

- Rewritten to the Memory 2.0 shared contract, so the stale definition, the expiry model and the item fields match the other four memory skills.
- Three modes, with `standard` as the default. The mode is named on the first line of every report.
- A content count with its own deduction table, separate from Graph Health's structure score, using the same four bands.
- De-link, never de-line, as the dead-reference fix, with a dry run before every write.
- A named approval step, a default on every approval item, and no deletion by the skill at any time.
- A dated dream log with no storage path. Its location comes from the profile.
- Hand-offs to Graph Health and Weekly Review by field name, and a use-protection rule for systems that record use.
