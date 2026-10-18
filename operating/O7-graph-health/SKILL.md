---
name: gtm-graph-health
version: 2.0.0
description: "Measures the shape of a knowledge base (tag sprawl, link density, provisional age and broken links), returns a structure score with every deduction shown, and hands the owner a decision for each crossed threshold. Dream and Weekly Review read its score. It never edits an item and never judges whether one is true."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [graph-health, knowledge-base, structure-score, tag-sprawl, orphans, hubs, provisional-age, broken-links, operating-discipline]
requires:
  skills: [gtm-ingest]
mutating: false
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Ground-up rewrite. Measures structure only, with the score kept apart from Dream's content count. Tag, link and provisional-age measures are named by field, claims are counted by grade word when the base holds them, and the seven hand-off fields are fixed by name."
---

# Graph Health

## Overview

Graph Health answers one question about a knowledge base: **is its shape healthy enough to find things in?** It counts how many tags are used only once, how many items link to too few or too many others, how long provisional items have sat undecided, and how many links point at nothing. It turns those counts into one structure score, shows every deduction, and returns each crossed threshold to the owner as a decision.

It does not read what the items say. It cannot tell whether a note is still true, and it does not score content age or expiry. Those belong to Dream's content count. Keeping the two numbers apart tells the owner which skill to run next.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** A base can be entirely true and completely unusable. Measure the shape.

---

## Why This Skill Exists

Decay in a knowledge base is invisible. A wrong number looks exactly like a right one, and nothing throws an error, so the check has to be scheduled rather than noticed. Article 49 of the Guild, *Memory That Compounds*, names three shape problems that hide this way. Tags fragment into one-off variants that search cannot reuse. Notes sit isolated, so nobody finds them except by exact recall. Provisional notes, the ones still marked as forming, quietly become the permanent status of a third of the base because nobody forces the call. Reading one item shows none of this. Measuring the whole does.

The thresholds are the ones article 49 publishes: tag sprawl at 20% and 40%, link density at three and ten links, provisional age at 30 and 60 days.

---

## Role

You are a structural inspector. You count, you check links, you compute a score, and you report. You work from item fields and links only.

You refuse to do three things:

- **Edit an item.** Items belong to their owner and to Ingest. A check that changes what it measures stops being a measurement, and timeline entries are the audit trail.
- **Judge whether an item is true or current.** A well-linked, well-tagged note can still be wrong. Truth belongs to the owner, and content age and expiry belong to Dream.
- **Decide what to do about a finding.** Each crossed threshold comes back as a choice for the owner: link or retire, promote or retire, split or leave.

---

## Input Contract

**If a required input is missing, ask. Do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Knowledge base location | Required | The folder holding the items. Without it, the skill asks and does not start |
| Tag list location | Optional | Enables the "tag not on the list" deduction. Without it, that deduction is null, with the reason |
| Last report | Optional | Lets the report show change since the last run. Without it, deltas read as a dash, meaning no baseline |
| Content of items | Never | The skill reads the item fields and links listed below. It does not read or judge the words of an item |

Fields read from each item, by the names in the shared contract: `name` (to resolve links), `domain`, `node_type`, `status`, `created`, `updated`, `tags` and `related`. Links are read from `related` and from any `[[item]]` link in the body. A link is a distinct target, counted once, whether it appears in `related`, in the body, or in both, so the same target named twice counts once. Links to targets that do not exist are counted in Stage 5, not here.

---

## Output Contract

The report goes to the report location in the profile, or into chat when none is set. Dream and Weekly Review read the hand-off fields by name.

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Graph Health report | Report location in the profile | Dated by the local run date. Structure only |
| Hand-off fields | Last section of the report | `structure_score`, `tag_sprawl`, `orphans`, `hubs`, `emergent_past_30`, `emergent_past_60`, `broken_links` |
| Band | Structure Score section | One of the four bands in the shared contract. Dream reads it |
| Decisions | Decisions Returned section | One line per crossed threshold |

Report template:

```text
GRAPH HEALTH REPORT, [run date]
Knowledge base: [path]. Tag list: [path, or "not supplied"]. Last report: [date, or "none, no baseline"]
Summary: [two sentences: the score, the band, and the number of decisions]

1. Inventory
   Items: [n]
   By domain: gtm [n], accounts [n], people [n], methodology [n], business [n], technical [n]
   Uncertain (own group): [n] of [items] ([rate]%)
   No domain recorded: [n] (not counted as uncertain)
   By status: emergent [n], validated [n], canonical [n], archived [n], not recorded [n]
   Claims by grade word: assumed [n], heard [n], seen [n], confirmed [n], or "not counted in this run"

2. Tag Health
   Tag sprawl: [rate]% ([single] of [total] tags used once). Band: [Healthy, Warning or Unhealthy]
   Single-use tags: [list]
   Tags not on the tag list: [list, or "null: no tag list supplied"]

3. Link Health
   Orphans (fewer than three links): [count] of [items] ([share]%)
   Connected (three to ten links): [count]
   Hubs (over ten links): [count], with each name and its link count

4. Lifecycle Health
   Emergent aged 31 to 60 days: [count]
   Emergent aged over 60 days: [count]

5. Broken Links
   [count] broken: one line per link, with the source item and the target name

6. Structure Score
   Start: 100
   [one line per deduction: class, count, value, cap, result]
   Total deduction: [n]
   Score: [n], band [Excellent, Good, Fair or Poor]

Decisions Returned
   [one line per crossed threshold, phrased as a choice for the owner]

Hand-off Fields
   structure_score: [n]
   tag_sprawl: [rate]% ([single] of [total])
   orphans: [count] ([share]%)
   hubs: [count]
   emergent_past_30: [count]
   emergent_past_60: [count]
   broken_links: [count]
```

---

## Context

Graph Health reads, in this order:

1. The `## Graph Health` section of `profiles/client-profile.md`, if it exists. It holds the knowledge base location, the tag list location, the link syntax, the run cadence and the report location. This skill's CUSTOMIZE.md writes it.
2. The item fields listed under Input Contract, for every item in the base.
3. The last report, if one is supplied.

If the profile has no `## Graph Health` section, say so once at the start, ask for the knowledge base location, and use these defaults: wiki-links in the form `[[name]]`, no tag list (so that deduction reads null), and the report returned in chat.

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

Run the six stages in order. Inventory comes first so every later rate has its denominator. The link and age measures come before the score, because the score only subtracts what the earlier stages counted. Stage 6 counts nothing itself.

### Stage 1. Inventory

Count every item by domain, node type and status. The `uncertain` domain is its own group. An item with no domain is counted as "no domain recorded", not as uncertain, because a missing value is not a judgement. If the base holds claims from Discovery, count them by grade word (assumed, heard, seen, confirmed). Assumed claims are open bets, and the count shows how much of the customer picture is still a guess.

**Produces:** the counts by domain, node type and status, and the claim counts by grade word where claims exist.

### Stage 2. Tag Sprawl

Find the share of tags used exactly once. Under 20% is Healthy, 20% to 40% is Warning, and over 40% is Unhealthy. Show the counts beside the rate, because a rate on a small base can look like a finding when it is one observation. List the single-use tags, and list any tag not on the tag list.

**Produces:** the rate with its counts, the band, the single-use list, and the off-list list (or null).

### Stage 3. Link Density

A link is a distinct target, counted once, whether it appears in the `related` field, as a wiki-link in the body, or in both. An item with three `related` entries and the same three targets in its body has three links, not six. Links to targets that do not exist are not counted here. They are counted in Stage 5 as broken links.

Each item is an orphan (fewer than three links), connected (three to ten links), or a hub (over ten links). Report orphans as a count and as a share of the base. A new call note is the usual orphan, because it is written and then never linked to the account it belongs to.

**Produces:** the orphan count and share, and the hub list with link counts.

### Stage 4. Provisional Age

Take every `emergent` item and measure its age from `updated`, never from file dates, because copies and syncs reset file dates and give a batch of items the same false age. Two bands are counted: items aged 31 to 60 days, which need a decision date, and items aged over 60 days, which are critical and need a promote or retire decision. The two bands never overlap, so an item older than 60 days is counted once, in the over-60 band.

**Produces:** the two lists, each item with its age in days.

### Stage 5. Broken Links

Resolve every link against the `name` field of the items. Before reporting a link as broken, open the item it points at and compare the exact name, because a case difference or a renamed item can look broken when it is not. A link that cannot be confirmed as broken is listed as a candidate.

**Produces:** the broken list, each entry with its source item and target name.

### Stage 6. Structure Score

Start at 100 and subtract each deduction. Show every line, including the zeros. Each class has a cap, so no single class can zero the score alone. Floor the result at zero.

| Deduction | Value | Cap |
|-----------|-------|-----|
| Single-use tag | -2 each | -10 |
| Tag not on the tag list | -3 each | -15 |
| Sprawl in Warning | -2 | One line, so no cap is needed |
| Sprawl in Unhealthy | -5 | One line, so no cap is needed |
| Orphan | -1 each | -10 |
| Hub | -2 each | -10 |
| Broken link | -4 each | -20 |
| Emergent past 30 days | -1 each | -10 |
| Emergent past 60 days | -2 each | -10 |

Band the score with the four bands in the shared contract. Then turn each crossed threshold into a decision for the owner: an orphan becomes "link or retire", an emergent item aged 31 to 60 days becomes "set a decision date", an emergent item aged over 60 days becomes "promote or retire", a hub becomes "split or leave", a broken link becomes "repair or de-link", and a sprawl warning becomes "merge the variants or keep them".

**Produces:** the score, the band, every deduction line, and the decisions.

---

## Epistemic Rules

- **n beside every rate.** "Tag sprawl 10% (6 of 61 tags)", never "10%".
- **Five before a pattern.** Below five items or five tags, a rate is an observation, and the sentence says so.
- **Null is not zero.** A measure nobody checked, such as a missing tag list or an item with no `updated` date, is written null with its reason. Zero means somebody looked and found nothing.
- **Silence is not a no.** An item with no `status` is not counted as emergent, and it is not counted as validated. It is counted under "not recorded".
- **Structure is not truth.** A score of 100 says the base is well formed. It says nothing about whether any item is right.
- **A threshold crossed is a decision, not a verdict.** The report hands the owner a choice. It does not call the item bad.
- **Confirm before flag.** A broken link is opened and checked before it is reported.

---

## Hard Rules

1. **Never edit an item.** Items and their timelines are records. A change made during a measurement would alter the thing being measured, and neither number could be trusted afterwards.
2. **Never judge whether an item is true or current.** A score that mixed shape with truth would not tell the owner whether to fix the links or check the facts.
3. **Never score content age, expiry or contradiction.** Those belong to Dream's content count. Keeping them out lets the two numbers tell the owner which skill to run.
4. **Never invent a link or a tag to clear a deduction.** A made-up link hides an orphan, and a made-up tag hides sprawl. The report would look clean and the base would be no easier to search.
5. **Never write an unchecked measure as zero.** A zero travels into Dream and Weekly Review as a fact, and nobody can see that nobody looked.

---

## Quality Bar

Done when all of these are true:

- [ ] Every rate shows its n.
- [ ] The uncertain group and the no-domain group appear on separate lines.
- [ ] Every deduction line shows its count, value, cap and result.
- [ ] The score is floored at zero, and its band comes from the four bands.
- [ ] Every crossed threshold appears under Decisions Returned as a choice for the owner.
- [ ] Every broken link was opened and checked before it was reported.
- [ ] No item was edited, and the report makes no claim about truth.
- [ ] Every unchecked measure is null with a reason, and a partial score is marked partial.
- [ ] All seven hand-off fields are filled, or each one is null with a reason.

---

## Examples

### Example 1. The PlotIQ Base at Good Structure (Illustrative)

This run is on the PlotIQ knowledge base, on Monday 2026-10-19. Every number is illustrative. The base holds the account items written on 2026-10-13, after a discovery call with Brackhaven Memorial Gardens. The base has 134 items.

**Stage 1. Inventory.** By domain: gtm 58, accounts 41, people 19, methodology 9, business 4, technical 0, uncertain 3 (2%, 3 of 134). No domain recorded: 0. By status: emergent 22, validated 71, canonical 38, archived 3. Claims are not counted in this run.

**Stage 2. Tag sprawl.** 61 unique tags, 6 used once: 10% (6 of 61). Band: Healthy, because 10% is under 20%.

**Stage 3. Link density.** Orphans: 9 of 134, which is 7% (9 of 134). All nine are call notes that were never linked to their account record. Hubs: 1, OLDGATE_DISPLACEMENT, with 14 links. Connected: 124 (134 items less 9 orphans less 1 hub).

**Stage 4. Provisional age.** Of 22 emergent items, 2 emergent items are aged 31 to 60 days, and 3 emergent items are aged over 60 days.

**Stage 5. Broken links.** None. Count: 0.

**Stage 6. Structure score.**

| Line | Count | Value | Cap | Result |
|------|-------|-------|-----|--------|
| Start | | | | 100 |
| Single-use tags | 6 | -2 each, which is -12 | -10 | -10 |
| Tags not on the tag list | 0 | -3 each | -15 | 0 (the base runs against its tag list, illustrative) |
| Sprawl | Healthy | none | none | 0 |
| Orphans | 9 | -1 each, which is -9 | -10 | -9 |
| Hubs | 1 | -2 each | -10 | -2 |
| Broken links | 0 | -4 each | -20 | 0 |
| Emergent aged 31 to 60 days | 2 | -1 each, which is -2 | -10 | -2 |
| Emergent aged over 60 days | 3 | -2 each, which is -6 | -10 | -6 |

Total deduction: -10, -9, -2, -2 and -6, which is -29. **Score: 71, band Good** (70 to 89). The floor at zero is not reached.

**Decisions returned:**

- Link or retire each of the 9 orphan call notes.
- Promote or retire the 3 emergent items aged over 60 days this week.
- Set a decision date for the 2 items aged 31 to 60 days.
- Split the hub OLDGATE_DISPLACEMENT, or leave it. This is the owner's call.

**Hand-off:** `structure_score` 71, `tag_sprawl` 10% (6 of 61), `orphans` 9 (7%), `hubs` 1, `emergent_past_30` 2, `emergent_past_60` 3, `broken_links` 0.

Dream runs next, on its own cadence. A Good score is above the Fair trigger, so this score does not start an extra Dream run.

### Example 2. Excellent Structure, Poor Content Count (Illustrative)

This second case uses a base of 60 items, every number illustrative. It shows that the two scores answer different questions.

**Graph Health.** Tag sprawl 5% (2 of 40 tags used once), Healthy, no deduction. One orphan of 60 items, which is 2% (1 of 60), -1. No hubs, no broken links, no emergent items aged 31 to 60 days or over 60 days. **Score: 99, band Excellent** (90 to 100). The decision returned is one line: link or retire the orphan.

**Dream's content count on the same base** (illustrative, computed by Dream from its own table, not by this skill): **47, band Poor** (under 50). Stale items 4 (-12). Expired items 6 (-24, capped at -12). Dead references 3 (-15). Contradictions 3 (-12). Duplicates 2 (-4). Missing fields 3 (-3). Bonus for items carrying an expiry date, +5 (capped at the maximum). Total: 100 less 12, 12, 15, 12, 4 and 3, plus 5, which is 47.

**What this shows.** Graph Health scored the six expired items at nothing, because expiry is content and this skill does not score content. The structure score says the links and tags are sound, so a shape repair would be the wrong job. The content count says six items are past their expiry and three links are dead, so Dream is the right run. The first number asks whether the base is well formed. The second asks whether what it says is still current.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| Tag sprawl looks high on a small base | Fewer than five tags in use, so the rate is one or two tags | Label the rate an observation, with its n. Do not call it a trend |
| A link reported as broken exists | A case difference, a renamed item, or a typo in the link | Open the target and compare the exact name. Report it as a candidate until confirmed |
| Orphan count jumps after a large ingest | New notes were written without links to their account record | Expected. Return the orphan list as decisions. Ingest adds the links after the owner approves |
| The score falls into Fair or below | Several deductions at once | Report every line. Say in the summary that Dream runs on this score |
| The owner asks whether an item is still true | A request for a truth judgement | Decline in one sentence. Point to the owner's review and to Dream's content count |
| The owner asks the skill to link the orphans now | A request to edit | Decline, and return the list. Linking belongs to Ingest, with approval |

Degradation table. When an input is missing, the report still runs, and it says what it could not check:

| Missing | What the Report Writes | What It Says |
|---------|------------------------|--------------|
| Tag list | The off-list line and its -3 deduction | "null: no tag list supplied". The score is marked partial |
| `updated` on an item | That item's age | Null, listed by name, and left out of both age counts |
| `status` on an item | That item's lifecycle counts | "not recorded". It is not counted as emergent or validated |
| `related` and no body links | Orphan status | Counted as an orphan, because zero links is a measured fact |
| Knowledge base folder cannot be read | Inventory, tags, links and age | Every count is null, with the reason. No score is written |
| Last report | Change since the last run | A dash, meaning no baseline |

---

## Best Practices

- Run Graph Health before Dream and before Weekly Review, because both read its number.
- Read the counts, not only the score. A score of 71 with nine orphans points to a different job than a score of 71 with one stale tag.
- Keep the tag list short and written down. A tag nobody chose is the usual off-list tag.
- Give every new item at least three links at the moment it is written. Ingest does this by default.
- Compare reports over time. One score is a snapshot, and the trend across runs is the finding.

---

## Integration With Other Skills

- **Reads from gtm-ingest:** the item fields `name`, `domain`, `node_type`, `status`, `created`, `updated`, `tags` and `related`, as the shared contract defines them.
- **Hands to gtm-dream:** `structure_score` and `band`, which Dream reads when it decides whether to run on the Fair trigger. Dream's content count is computed separately and is never merged into this score.
- **Hands to gtm-weekly-review:** `structure_score`, `tag_sprawl`, `orphans`, `hubs`, `emergent_past_30`, `emergent_past_60` and `broken_links`, by those names. Weekly Review writes null for any field left empty.
- **Discovery claims:** when the base holds claims, the grade-word counts in Stage 1.

**Next skill:** gtm-dream. Run it after this report, using the structure score and band it reads.

---

## Changelog

### 2.0.0 (2026-10-18)

- Ground-up rewrite. Measures structure only, with the score kept apart from Dream's content count.
- Tag, link and provisional-age measures named by field, with the four bands and the capped deductions in one table.
- Claims counted by grade word when the base holds them.
- Seven hand-off fields fixed by name, with nulls and reasons for any measure not checked.
