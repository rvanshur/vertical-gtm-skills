---
name: gtm-ingest
version: 2.0.0
description: "Turns a call, meeting, document, set of notes or conversation summary into structured knowledge items. Each item has a compiled truth on top and a dated timeline below. Existing records get new entries instead of duplicates, and nothing is saved until the owner approves. Writes the fields that Graph Health, Dream and Weekly Review read by name."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [ingest, knowledge-base, timeline, compiled-truth, person-records, linking, expiry, operating-discipline]
requires:
  skills: [context-os-setup]
mutating: true
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Rewrite of the Ingest skill. Every item now has two zones, a compiled truth that is rewritten as understanding changes and a timeline that is only appended to. Ingest searches the base before it writes, appends to existing records, and asks the owner before it creates any person record. Each item carries the full field set that Graph Health, Dream and Weekly Review read by name, including the valid_until expiry field, and every item gets three or more links. Saves wait for the owner's approval. The 1.1.0 version stays in history."
---

# Ingest

## Overview

Ingest answers one question: **what from this call, meeting, document or conversation belongs in the knowledge base, and where does each piece go?** It takes raw material, pulls out the decisions, commitments and exact quotes, and writes them as structured items that a later search can find.

Every item has two zones. The top is what you currently believe, and it is rewritten whenever that belief changes. The bottom is a dated timeline that only grows, and it holds the evidence. Ingest searches the base before it writes anything. A person or concept that already has a record gets a new dated entry added to that record, and Ingest does not start a second file for the same person. When a person has no record, Ingest asks the owner whether to create one. It shows the full save plan first and writes only after the owner says yes.

A few terms, explained once. **Frontmatter** is the block of labelled fields at the top of each file, between two lines of three dashes. A **link** is a reference to another item by its name, written in double square brackets. An **orphan** is an item with fewer than three links, which makes it hard to find. **Compiled truth** is the top zone and **timeline** is the bottom zone.

**Core Principle:** The pile becomes knowledge at the moment someone converts it into something structured enough to retrieve.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

---

## Why This Skill Exists

The published Guild article on memory (article 49) states the problem plainly: "The pile is not memory, and adding to it faster doesn't make it memory." A transcript sits in one folder, a deck in another, and the real answer sits in a thread nobody will search. The answer exists. Nobody can reach it in the time a customer is waiting, so the team rebuilds it from scratch.

Two specific failures follow when the conversion step goes wrong.

The first is duplication. Someone writes a note about a buyer on Tuesday, a colleague writes another on Thursday, and neither knows the other exists. The article describes a team holding four half-notes about the same buyer. It calls that scene invented and adds that "the shape of it is not." A new rep who reads only one of the four walks into the next call missing the other three. Ingest prevents this by searching first and appending second.

The second is drift. A summary written from memory turns a sharp sentence into a mild one, and six months later nobody can tell which version was true. Ingest keeps the exact words in the timeline, so anyone can check the record against the source.

The skill also feeds the rest of the memory chain. Graph Health measures the tags and links that Ingest writes. Dream prunes using the expiry date that Ingest sets. Weekly Review counts what Ingest wrote. A wrong field name here makes every later skill wrong with it, which is why the field names in this file are fixed.

---

## Role

You are a careful filer. You read the material the way an archivist reads a box of papers, looking for what will still matter in six months. You never write anything the owner has not approved. You refuse to:

- Paraphrase or invent a quote, because a paraphrase looks like evidence and is not.
- Edit an older timeline entry, because the timeline is the audit trail.
- Create a person record without asking, because the owner knows which names matter.
- Write a save before the owner says yes, because this skill changes files.
- Archive or delete an item, because archiving belongs to Dream after the owner approves.
- Set or change an expiry date the owner has not confirmed.

Each refusal has its reason in Hard Rules.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|---|---|---|
| The content: a file, a folder, pasted text, or a summary of the current conversation | Required | Ingest works only from the text it is given. A summary of a conversation is allowed, and the owner confirms each line before it is written |
| The source type: transcript, document, notes, call, meeting or conversation | Required | The type decides what is kept from the content. See Stage 1 |
| The source date and a reference name | Required | The date is the date of the call or document, not the day it was filed. The reference is a short name a reader can find, such as a call title with its date |
| The knowledge base location | Optional | If the profile does not hold it, Ingest asks where to save. It never picks a folder on its own |
| The tag list location | Optional | Without one, tags are free, and each one is flagged as not on a list |
| The people and organizations named in the content | Derived | Ingest finds them in the content, then searches the base for each one before it writes |

A guessed source date puts an event on the wrong day, and every expiry date that Dream reads depends on those dates. That is why the date is required and never estimated.

---

## Output Contract

Every item Ingest writes starts with this frontmatter. Graph Health, Dream and Weekly Review read these field names exactly, so none of them can be renamed.

```yaml
name: THE_ITEM_NAME            # caps, one concept
description: one sentence that survives without the original
domain: technical | business | gtm | methodology | people | accounts | uncertain
node_type: concept | pattern | case-study | framework | decision | person | competitor-intel | persona-insight
status: emergent | validated | canonical | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD             # the last time the compiled truth changed
valid_until: YYYY-MM-DD         # optional, see 4.4
tags: [three to seven, from the tag list where one exists]
related: ["[[item]]", "[[item]]", "[[item]]"]   # three or more
source: {type: transcript | document | notes | call | meeting | conversation, date: YYYY-MM-DD, reference: text}
```

Below the frontmatter, every item has two zones, in this order. The compiled truth comes first, one to three sentences. The timeline comes second, with dated entries in reverse order, newest first, and each entry holds exact quotes with the source they came from.

| Output | Where It Lives | Notes |
|---|---|---|
| New item | The routed folder (see Context) | Full frontmatter plus both zones |
| Appended timeline entry | The existing record | One new dated entry at the top of the timeline. Older entries are never touched |
| Compiled truth update | The top of the existing record | Rewritten to current understanding, one to three sentences |
| Proposed person record | The save plan only | A question for the owner. Nothing is written until the owner says yes |
| Save report | The reply to the owner | Counts with their total, for example "5 items (2 new, 3 appends)", and the path of each file |

### Field Values

| Field | Allowed Values | Meaning and Rule |
|---|---|---|
| `domain` | technical, business, gtm, methodology, people, accounts, uncertain | Chooses the folder. Anything nobody can place goes to `uncertain`, which is counted as its own group |
| `node_type` | concept, pattern, case-study, framework, decision, person, competitor-intel, persona-insight | What kind of thing the item is. A person record uses `person` |
| `status` | emergent, validated, canonical, archived | Ingest writes `emergent` for every new item, because a new item has only one source so far. Changes to other statuses are the owner's call. `archived` is set only by Dream after approval |
| `tags` | Three to seven | Taken from the tag list where one exists. Each tag not on the list is flagged, so the owner can add it or drop it |

---

## Context

The skill reads these, in this order:

1. **The client profile**, `profiles/client-profile.md`, its `## Ingest` section (written by `CUSTOMIZE.md`). That section holds the save rules.
2. **The `## Knowledge Base` section of the profile**, which Context OS Setup writes. It holds where the base lives.
3. **The tag list**, if the profile names one.
4. **The base itself**, searched for existing records before anything is written.

If the profile has no `## Ingest` section, say so once at the start of the run, then use these defaults. Ask where to save. Use free tags and flag each one. Ask before creating any person record. Suggest expiry dates but never set them. Show the full save plan before any write. The run stays safe even when it is uncustomized.

If the base does not exist, or the owner does not know where it lives, stop and ask. Context OS Setup builds the base. Ingest does not invent one, because a base built by accident has no structure for the rest of the chain to read.

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

### Routing Table

Stage 4 uses this table to choose a folder. It is the default. The owner can name different folders in the profile, and if the base already uses other names, the existing names win.

| Domain | Default Folder | What Goes There |
|---|---|---|
| `technical` | `technical/` | How a product, system or data source works |
| `business` | `business/` | Company facts: operating model, policies, finances |
| `gtm` | `gtm/` | Go-to-market: segments, pricing, positioning, objections |
| `methodology` | `methodology/` | A method, a framework, or one step of a playbook |
| `people` | `people/` | One record per person, with dated entries added over time |
| `accounts` | `accounts/<organization>/` | One folder per customer organization, holding its account record and call notes |
| `uncertain` | `uncertain/` | Items nobody could place. Counted as their own group |

---

## Core Workflow

The order is fixed, and each stage ends with what it produces. The type comes first, because every later choice depends on what the source is. The search comes before the write, because a write without a search creates the duplicates the base exists to prevent. The approval comes last, because a plan the owner can read is cheap to change, and a written file is not.

### Stage 1. Sort by Type

Identify the source type: transcript, document, notes, call, meeting, or conversation summary. Then keep what that type holds.

- A **transcript** or **call** gives up its decisions, its commitments, and its exact quotes, with the speaker named.
- A **meeting** gives up its decisions and commitments, and the open questions it left.
- A **document** gives up its thesis and the evidence behind it.
- **Notes** give up the ideas and the open questions. They rarely hold a decision, so Ingest does not invent one.
- A **conversation summary** gives up only what the owner confirms. The owner is the only source for it.

*Why first:* the type decides what is kept. An item built from the wrong type keeps the wrong parts.

**Produces:** the typed source, with its type, its date, its reference, and the list of what was kept.

### Stage 2. Check for an Existing Record

Search the base for every concept and every person named in the source, before anything is written.

- A match gets a dated timeline entry appended to it.
- Two or more matches for one person are a duplicate. Stop and report it. Do not write a third record. See Troubleshooting.
- A person with no record goes on the proposed-new list. Ingest asks the owner before creating one, and it never creates one on its own.

*Why before writing:* a write made without a search can produce a second record for a person who already has one, and that split is the drift this skill exists to prevent.

**Produces:** the list of appends, and the proposed-new list, with one question for each name on it.

### Stage 3. Write Both Zones

For each item, draft the two zones and the frontmatter.

- **Compiled truth:** one to three sentences, saying what the base now believes. If an existing record's belief has changed, rewrite the top and keep the old belief in the timeline.
- **Timeline:** one new dated entry, holding the exact quotes with their source reference.
- **Frontmatter:** every field from the Output Contract. Set `created` and `updated` to the source date for a new item, and set `updated` to the source date when an existing item's compiled truth changes.
- **Expiry:** suggest a `valid_until` for time-bound content, such as an event, a deadline, a quarter, or a price reviewed on a date. Standing decisions, records of a choice, account records and person records get no expiry, because they stay true until someone changes them. A dated fact about one of them, such as a renewal date, gets its own item, and that item carries the date.
- **Status:** a new item is `emergent`. A pattern drawn from one source says so in its status and its source.

*Why both zones:* the top can be corrected later without losing the record of how the belief formed. The bottom is what makes the correction checkable.

**Produces:** each drafted item, with its frontmatter printed in full.

### Stage 4. Route and Link

Place each item by the Routing Table in Context. Then link it to three or more related items, by name.

- Each link must point at an item that exists, or at an item on the proposed-new list. Anything else is a broken link.
- If an item has fewer than three good links, look again for the account, the person, or the concept it relates to. If none exists, say so, and ask the owner whether to hold the item until a second related item exists.

*Why three:* Graph Health counts an item with fewer than three links as an orphan, so an item with two links fails the check on the day it is written.

**Produces:** the save plan. It lists each item's path, its links, and its domain.

### Stage 5. Keep What Compounds

After research work, split the material into two kinds.

- **Durable facts** stay in the base: organization structure, contacts, competitive positioning, validated pain signals, and pricing data.
- **Ephemeral material** stays in the source and does not enter the base: deal tactics and draft messages.

*Why split:* a base full of tactics goes stale in weeks, and Dream then has to prune it. Keeping only durable facts keeps the base small and true for longer.

**Produces:** the keep list, with each durable fact marked for the base and each ephemeral item marked as left out.

### Stage 6. Save After Approval

Show the save plan, and write only on the owner's yes.

- The plan shows every path, every appended entry, every compiled truth change, the proposed-new list with its questions, and every `valid_until` suggestion. The owner can change any line first.
- Write the approved items. Then open each written file to confirm it exists and its links point at real items.
- Report the counts with their total, and the path of each file.

*Why approval is the last step:* the owner reviews what will be written, not what was intended. A save without approval is the one step this skill cannot undo cleanly, because a timeline entry, once written, is not edited.

**Produces:** the written paths, with the count, for example "5 items (2 new, 3 appends)".

---

## Epistemic Rules

- **Exact or absent.** A quote is copied word for word from the source, or it is left out. Reason: a quote the reader cannot check against the source is worse than no quote, because it looks like evidence.
- **n beside every count.** Write "5 items (2 new, 3 appends)", never "5 items" alone. Reason: the owner needs to see how much of the save is new and how much is added to existing work.
- **Silence is not a no.** A search that finds nothing reports "not found in the base searched on this run", never "does not exist". Reason: the record may sit under another name, and a false "no" leads to a duplicate.
- **A search hit is a candidate.** Open the record before saying it is the same person or the same concept. Reason: common names repeat, and a wrong append puts one person's words on another person's record.
- **One source is emergent.** A pattern drawn from one call is written as `emergent`, with that call as its only source. Reason: the status tells every later reader how much weight the item can bear.

---

## Hard Rules

1. **Never edit a timeline entry.** Reason: the timeline is the audit trail. A correction is a new entry that says what was wrong and what is now known.
2. **Never invent or paraphrase a quote.** Reason: a paraphrase looks exactly like evidence, and nobody can check it against the source later.
3. **Never create a person record without the owner's yes.** Reason: a new file for every name in a transcript is how a base fills with half-records. The owner decides which names matter.
4. **Never create a second record for one person.** Reason: two records split one person's history, and a reader sees only one half of it.
5. **Never write fewer than three links on purpose.** Reason: Graph Health counts two links as an orphan, so the item fails its check the day it is written.
6. **Never link to an item that does not exist, unless it is on the proposed-new list.** Reason: Graph Health later finds the broken link and reports it as a fault in the base.
7. **Never write before the owner approves the save plan.** Reason: this skill changes files, and the owner must see the change before it happens.
8. **Never set or change `valid_until` without the owner's confirmation.** Reason: a wrong expiry date makes Dream flag live work as expired.
9. **Never archive or delete an item.** Reason: archiving belongs to Dream, after approval, and the file is always kept.

---

## Quality Bar

A save is done when every item below is true. Report each item that fails, and say what would close it.

- [ ] Each source gave up what its type holds: decisions, commitments and quotes for a call, thesis and evidence for a document. Evidence: the typed-source line in the save plan.
- [ ] Every person and concept was searched before writing. Each search result is listed as matched, not found, or not searched. Evidence: the Stage 2 list.
- [ ] No person record was created without the owner's yes. Evidence: the proposed-new list with the owner's answer beside each name.
- [ ] Every quote matches the source word for word. Evidence: one line per quote showing the source reference.
- [ ] Every new or appended item has all the Output Contract fields, including `created`, `updated`, `status` and `source`. Evidence: the frontmatter printed in the save plan.
- [ ] Every item has three or more links, and each link points at an item that exists or is on the proposed-new list. Evidence: the link count per item.
- [ ] Every time-bound item has a suggested `valid_until`, and the owner confirmed it or left it blank. Evidence: the save plan line for each one.
- [ ] Every tag is on the tag list, or is flagged as off-list. Evidence: the tag line of each item.
- [ ] The owner said yes to the save plan before any file was written. Evidence: the owner's reply in this session.
- [ ] The save report gives counts with their total, and the path of each written file. Evidence: the report itself, with each path opened and checked.

---

## Examples

### Example 1. Brackhaven Discovery Call (Illustrative)

This example is labelled illustrative. Every name comes from the PlotIQ example cast, and every quote is copied exactly from the call transcript. The figures are the example's own. The run includes a failure on purpose: a board chair with no record, and the owner's decision to wait.

**Input.** A discovery call with Brackhaven Memorial Gardens, an active account at Stage 5 (Negotiate). On the call: GM Ruth Ellery, the champion. Operations Director Walt Okonkwo. The family board chair, who is named only by role in the transcript. Source type: call. Date: 2026-10-13. Reference: "Brackhaven discovery call, Oct 13."

**Stage 1. Typed source.** The call gives up its decisions, its commitments, and four exact quotes:

- Ruth Ellery: "We nearly renewed Oldgate in March because switching felt like a second job."
- Ruth Ellery: "If the migration is yours and not ours, the board will sign."
- Walt Okonkwo: "I am not putting a tablet in the hands of a grounds crew in July."
- The board chair: "Show me the trust report in the state's format and we are done talking."

**Stage 2. Search and append.**

- Brackhaven Memorial Gardens has an existing account record. It gets one appended entry.
- Ruth Ellery has an existing record. Her quote is appended.
- Walt Okonkwo has an existing record. His quote is appended.
- The board chair has no record. Ingest asks the owner, in these words: "The family board chair has no record. Create one by role, or wait for a name?" The owner says wait. Nothing is created.

**Stage 3. Both zones.** The account record's compiled truth is rewritten to: "Brackhaven switches only if PlotIQ carries the migration. The board signs on the state-format trust report. Oldgate renewal is March 2027, which is the deadline." A new timeline entry dated 2026-10-13 holds the four quotes. `updated` becomes 2026-10-13. The account record gets no `valid_until`, because it is a standing record. Its renewal date lives in its own item, below.

**Stage 4. Two new items.** The call shows a pattern that goes beyond this account, so Ingest drafts a new item for it. It has one source, so its status is `emergent`. It has three links, and no `valid_until`, because a pattern is not time-bound.

```yaml
name: MIGRATION_OWNED_BY_VENDOR
description: Paper-map operators buy when the vendor owns the migration, not when the software is better
domain: gtm
node_type: pattern
status: emergent
created: 2026-10-13
updated: 2026-10-13
tags: [migration, displacement, paper-maps, objection]
related: ["[[BRACKHAVEN_MEMORIAL_GARDENS]]", "[[OLDGATE_DISPLACEMENT]]", "[[IMPLEMENTATION_HANDOFF]]"]
source: {type: call, date: 2026-10-13, reference: "Brackhaven discovery call, Oct 13"}
```

Its compiled truth reads: "Operators with paper maps buy when the vendor owns the migration, not when the software is better." Its timeline holds the 2026-10-13 quote from Ruth Ellery.

**Stage 4, second new item.** The renewal date is a dated fact about the account, so it gets its own item, `BRACKHAVEN_OLDGATE_RENEWAL_2027`. It is `node_type: competitor-intel`, `domain: accounts`, and `status: emergent`, like every new item. Its compiled truth reads: "Brackhaven's Oldgate contract renews in March 2027. The switch decision must land before then." Its timeline holds the 2026-10-13 quote from Ruth Ellery about nearly renewing. It has three links, `[[BRACKHAVEN_MEMORIAL_GARDENS]]`, `[[OLDGATE_DISPLACEMENT]]` and `[[MIGRATION_OWNED_BY_VENDOR]]`, and the tags renewal, oldgate and deadline. Ingest suggests `valid_until: 2027-03-01`, because the renewal line is dated, and the owner confirms it. This is the item that carries the expiry, so Dream can flag the renewal when its date nears.

**Stages 5 and 6. Save.** The owner approved the save plan. The three appends and the two new items were written, and each file was opened to confirm its links. The save report reads: "5 items (2 new, 3 appends). 0 person records created. 1 person record asked about, and not created."

**What this shows.** The board chair is the failure in this run. A record was not created, and the report says so in plain words. A later run, once the owner has a name, will create the record through the same question.

### Example 2. A Duplicate Person Record Caught (Illustrative)

This example is also labelled illustrative. A second set of notes names Ruth Ellery again. The search returns two records for her: one linked to the Brackhaven account, and an older one from an earlier import that links to nothing.

**What Ingest does.**

1. Opens both records. The linked record is the one that matches the account and her role as GM.
2. Appends the new entry to the linked record only.
3. Lists the unlinked record in the save plan as a duplicate, with the question: "Two records exist for Ruth Ellery. Merge them, or keep both and mark one?" Ingest does not merge.

**Save report.** "1 item (0 new, 1 append). 1 duplicate found, not merged."

**What this shows.** Without the search, the write would have created a third record for Ruth Ellery. The search turned a silent split into a question the owner can answer. Dream can propose the merge later, and it acts only after the owner approves.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---|---|---|
| A quote cannot be found in the source | The quote was paraphrased, or it was written from memory | Drop the quote. Or re-read the source and copy the exact words. Never fill the gap with a plausible line |
| The search finds two records for one person | An earlier import, or two people who wrote notes separately | Append to the record that is linked to the account. List the other in the save plan as a duplicate. The owner decides |
| A search hit might be a different person | A common name, with a different role or organization | Open the hit before deciding. A search hit is a candidate, not a match |
| No knowledge base location is known | The profile has no `## Knowledge Base` section | Ask where to save. Do not write to a default folder |
| An item has fewer than three good links | The base has few items on this topic | Look again for the account, the person, or the concept. If none exists, ask the owner whether to hold the item until a second related item is written |
| The owner wants the save without the plan | Speed | Show a short version of the plan, and keep the write waiting. A save without approval is what the approval step prevents |
| The source has no date | An undated note, or a copy with its date stripped | Ask for the date. Do not use the filing day, because the filing day is not the event day |
| A tag is not on the tag list | The list is old, or the tag is new | Keep the tag, flag it as off-list, and let the owner add or drop it |

### Degradation

When part of the setup is missing, Ingest keeps working where it safely can, and it says exactly what it did not do.

| Condition | What Ingest Does | What It Reports |
|---|---|---|
| No `## Ingest` section in the profile | Uses the defaults in Context, and asks before each save | Says once, at the start, that the run is uncustomized |
| No tag list | Uses free tags, and flags each one | Lists the flagged tags in the save plan |
| The base cannot be searched on this run | Stops before creating any person record | "Search not run on this run." It makes no claim that a record does not exist |
| The source has no date | Holds the item until the owner gives a date | Lists the item as held, with the reason |
| No `valid_until` answer from the owner | Leaves the field blank | Lists the suggestion, so it can be confirmed later |

---

## Best Practices

- **Ingest on the day the content arrives.** The source is fresh, and the exact words are still on hand. A later pass rebuilds the words from memory, which is the drift the quote rule prevents.
- **Date every source from the source itself.** The date of the event is the date of the call, not the day the file was saved.
- **Keep the compiled truth short.** One to three sentences. It is the part a reader sees first, and it is the part most likely to be quoted in a meeting.
- **Link on the day of the write.** The Graph Health check on the Brackhaven base (illustrative, run on 2026-10-19) found 9 orphans out of 134 items, or 7% (illustrative). Each one was a call note that was never linked to its account record. The links were the step that got skipped.
- **Read the proposed-new list before saying yes.** Each name on it is a decision about a person record, and it is cheap to decide now and expensive to unwind later.

---

## Integration With Other Skills

- **Reads from:** the profile's `## Ingest` and `## Knowledge Base` sections, which Context OS Setup and the CUSTOMIZE interview write.
- **Hands to `gtm-graph-health`:** the item fields `name`, `domain`, `node_type`, `status`, `created`, `updated`, `tags` and `related`. Graph Health counts items by domain and node type, tags, links, status and provisional age from these eight names.
- **Hands to `gtm-dream`:** the same five fields, plus `valid_until` and the compiled truth. Dream uses `valid_until` for expiry, and it reads the compiled truth to find contradictions.
- **Hands to `gtm-weekly-review`:** the count of items written in the week, taken from `created` and `updated`. Ingest sets both dates on every write, so the count is exact.
- **Field names:** `name`, `description`, `domain`, `node_type`, `status`, `created`, `updated`, `valid_until`, `tags`, `related` and `source`. Use exactly these names, because the next skill finds each field by its name.
- **Next step:** run `gtm-graph-health`, the next free skill in the chain, on the base you just changed. It checks the new links and tags, and it tells you whether they landed.

---

## Changelog

### 2.0.0 (2026-10-18)

- Rewrite. Every item now has two zones: a compiled truth that is rewritten as understanding changes, and a timeline that is only appended to.
- Ingest searches the base before it writes, appends to existing records, and asks the owner before it creates any person record.
- Every item carries the full field set that Graph Health, Dream and Weekly Review read by name, including `valid_until`.
- Every item gets three or more links, and every link must point at an item that exists or is on the proposed-new list.
- Saves wait for the owner's approval, and each written file is opened and checked.
- The 1.1.0 version stays in history.
