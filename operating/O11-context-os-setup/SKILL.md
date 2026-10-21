---
name: context-os-setup
version: 2.0.0
description: "Builds the one knowledge base that other go-to-market skills read from and write to. It starts from what the team already has, checks what is still true, seeds real items before it names any tags, and finishes only after a question is answered from the files. It writes the item fields that Ingest, Graph Health, Dream and Weekly Review read by name, the Knowledge Base section Ingest and Wrap-Up read by heading, and the profile sections Discovery reads by name."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-21
tags: [knowledge-base, setup, durable-record, working-memory, taxonomy, seed-items, evidence-grades, operating-discipline]
requires:
  skills: []
mutating: true
change_log:
  - version: 2.0.0
    date: 2026-10-21
    summary: "Clean-room rewrite from the approved 2.0 spec. Seed items now come before tags. Adds the two refusals, the seven-stage workflow, the claim slip and tier statement for the final check, the Knowledge Base section, and the Company and Competitive Landscape profile sections with evidence grades. The Credits section is retired."
---

# Context OS Setup

## Overview

Context OS Setup answers one question: **where does the team's go-to-market knowledge live, and which parts of it can anyone rely on today?** It builds that place, called the base, out of material the team already holds. It sorts what is still true from what has gone stale, lays out the folders, writes the first real items, names the tags and relationship types that keep the base consistent, and then asks the base questions to prove that it answers them.

Every other go-to-market skill reads from the base and writes back to it. That makes this the one setup whose mistakes spread. A misplaced folder, a tag nobody can reuse, or a stale price left in place will reach every answer that comes after it.

Runs in Claude Code, in Codex, or as a ChatGPT custom GPT.

**Core Principle:** Keep each fact in one home, and let every other record point at that home instead of copying it.

---

## Why This Skill Exists

Teams seldom lack information. They have decks, call transcripts, one-pagers and a pricing sheet, and each file was accurate on the day someone wrote it. The damage comes when one fact sits in three places, one copy gets corrected, and the other two quietly age. An AI assistant reads all three with the same confidence, and the person asking has no way to tell which copy is current.

The published Guild article on the context audit describes the same failure in one operator's own material. A large share of the pile had gone stale, and nothing in the pile said so. Building a base quickly from everything, without first checking what is still true, moves that failure into one shared place where every later skill will read it.

Two rules prevent this. The setup will not start without one real item to check against. It will not be called finished until someone asks the base a real question and reads the answer back from the files. A base that has never answered a question has not been tested, however tidy its folders look.

---

## Role

You are a setup partner. You turn what the team already has into one base that stays checkable, working only from the material the team supplies and the answers the owner gives. You refuse to:

- Build a base on zero content, because an empty base has nothing to check its answers against.
- Call the setup finished before a question has been asked of the base and its answer read back from the files.
- Create any folder, file or profile section before the owner approves the layout.
- Grade a claim above the evidence behind it, because later skills read the grade as a fact.
- Fill a gap with a plausible name, price, date or count, because an invented detail becomes one of the base's first answers.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| The purpose of the base: go-to-market, product, research or consulting | Required | Decides the folder layout. The default for this skill is go-to-market |
| At least one real seed item | Required | A positioning document, a customer list, notes on a competitor, a call transcript or a pricing sheet. Stage 2 does not continue without one |
| Who reads the base: one person, a team, or a custom GPT the team uses | Required | Decides who approves new tags and new structure |
| The client profile, `profiles/client-profile.md` | If it exists | Its entries are claims to check, not facts |
| Existing folders or files | If they exist | Each one is a candidate seed, and each needs an answer to whether it is still true |

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Folder layout | The base folder | Created only after the owner approves the layout |
| Taxonomy of tags | `<base>/_system/taxonomy.yaml` | Five to seven tags to start, each defined in one line. Ingest and Graph Health read the tag list here once their own profile sections name this file |
| Relationship types | The same taxonomy file | Three to five named types, such as "sells to", "competes with" and "proves". Items link to each other through the `related` field |
| How to add to the base | `<base>/_system/adding-knowledge.md` | One page for a new team member. It covers the frontmatter, the two layers and the three-link rule |
| Knowledge Base section | `profiles/client-profile.md`, section `## Knowledge Base` | Where the base lives, in the five fields shown below |
| First seed items | The Durable Record | At least one, with the full frontmatter |
| Company and Competitive Landscape sections | `profiles/client-profile.md` | Each entry marked with its evidence grade |
| Tier statement | The final message. Wrap-Up records it under Where We Stopped when it closes the session | The claim, its tier and its check, or the honest sentence |

### The Knowledge Base Section

Write this section with these five field names exactly. Discovery, Ingest, Graph Health and Wrap-Up look it up by its heading and read `Location` and `Taxonomy file` by those names.

```markdown
## Knowledge Base

- **Location:** [folder path of the base, or "none yet"]
- **Taxonomy file:** [path to `_system/taxonomy.yaml`]
- **Synthesis document:** [path to the one summary page the team reads first, or "none yet"]
- **Owner:** [a role, not a name]
- **Maintenance cadence:** [the cadence agreed in Stage 7, with one owner named by role]
```

### Item Frontmatter

Every item carries these fields, with these names. The next skills find each one by name, so none of them can be renamed.

```yaml
name: THE_ITEM_NAME            # caps, one concept
description: one sentence that survives without the original
domain: technical | business | gtm | methodology | people | accounts | uncertain
node_type: concept | pattern | case-study | framework | decision | person | competitor-intel | persona-insight
status: emergent | validated | canonical | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD             # the last time the compiled truth changed
valid_until: YYYY-MM-DD         # optional, only for time-bound content
tags: [three to seven, from the taxonomy file]
related: ["[[item]]", "[[item]]", "[[item]]"]   # three or more
source: {type: transcript | document | notes | call | meeting | conversation, date: YYYY-MM-DD, reference: text}
```

Rules that follow from the fields:

- **Three or more links on every item, and ten or fewer.** An item with fewer than three links is an orphan, and one with more than ten is a hub that probably needs splitting. The structure check deducts for both. Three to ten is the connected band the setup aims for on every item.
- **`archived` is a status, not a deletion.** Archiving changes the status and keeps the file, and only Dream sets it, after the owner approves.
- **`uncertain` is a domain** for an item nobody can place. The structure check counts those items as their own group.
- **Only the listed values are allowed.** One vocabulary means every skill reads the same words.

### The Company and Competitive Landscape Sections

Each entry in these two profile sections carries one evidence grade. The four grade words and their meanings are Discovery's, quoted from its Evidence Ladder so the two skills never disagree:

| Grade | Meaning, in Discovery's words |
|-------|-------------------------------|
| `assumed` | "Somebody believes it" |
| `heard` | "A buyer said it" |
| `seen` | "It shows in behavior or data" |
| `confirmed` | "Seen across at least 5 cases, recent, and not contradicted" |

Discovery also says: "A claim cannot move to `confirmed` while a contrary case is unexplained." Two rules are this skill's own, added so the grades are checkable: a team member's belief is `assumed`, not `heard`, because `heard` is reserved for a buyer, and every grade carries its evidence beside it, so the next reader can check it: `- **Competitor:** position, grade: heard, evidence: two customer calls on named dates`.

---

## Context

The skill reads these, in this order:

1. **The client profile**, `profiles/client-profile.md`, if it exists. Its Company, ICP Definitions, Buyer Personas, Core Pain Points, Competitive Landscape and Proof Points sections are claims to check, not facts. The setup writes two of them (Company and Competitive Landscape). Discovery writes Company, ICP Definitions, Buyer Personas and Competitive Landscape on its runs. Core Pain Points and Proof Points stay with the team.
2. **The material the team names as seeds**, and the folders it already keeps.
3. **The base itself**, once it exists, so that items already in place are not written twice.

If there is no profile, say so once at the start and run the workflow anyway. Write the profile sections only once a profile exists. If the profile has no `## Knowledge Base` section, say once at the start that the run is uncustomized, and ask where the base should live before creating anything. If the operator names ChatGPT, say at Stage 1 that a custom GPT reads the base only after its files are attached to it.

---

## Core Workflow

The order is fixed, and each stage ends with what it produces. Two orders matter most. Seed items come before tags, because a tag named before any item exists is a guess about content nobody has checked. The query comes last, because only an answer read back from the files shows that the base works.

### The Two Layers

The base has two layers, and this skill builds one of them.

**The Durable Record** holds what changes when the business changes: the company, the customer archetype, the competitors, the proof points, the pricing and the client profile. Each item covers one concept and is written as a record with two zones. The compiled truth is the short current belief at the top. The timeline is the dated list of evidence underneath, with exact quotes. This skill builds the Durable Record.

**The Working Memory** holds the records that other skills keep current: continuation notes, dream logs, health reports and the claim ledger. This skill never writes those records. It creates the `continuations` folder, which is the default place Wrap-Up writes to unless the profile's `## Wrap-Up` section names another, and nothing more.

### Stage 1. Take Stock

Say once that no base exists yet and that this setup will create one. Ask the purpose and the readers, as set out in the Input Contract. Inventory every place the team keeps material: folders, shared drives, the client profile and any loose files. List each file by name and location, and state the total as a count. If the operator names ChatGPT, say that a custom GPT reads the base only after the files are attached.

**Produces:** the inventory, with the file count and the places it spans.

### Stage 2. Gate on Real Content

Ask for one real seed item from the list in the Input Contract. If the operator has nothing written down, say so and stop. Name where a seed usually sits: a deck that went to a customer, a renewal email, or a pricing sheet. The setup does not continue on an empty base, because an empty base gives nothing to check against, and every answer it gave afterward would be invented.

**Produces:** the named seed item, or a stop with the list of places to look.

### Stage 3. Check What Is Still True

The team does the full inventory and the first pass of removing dead material by hand. This stage checks each file the team wants to keep. For each file, ask: "Is this still true today, and when was it last true?" Sort the files into three groups: still true, stale, and unknown. State each group as a count with its total.

- Stale and unknown files are not loaded as items. The operator decides whether to keep them outside the base.
- A time-bound fact, such as a price reviewed on a known date, takes the review date the owner gives, and its item carries that date as `valid_until`.
- A standing decision, such as who signs contracts, gets no expiry, because it stays true until someone changes it.

**Produces:** the three groups with counts, and the review dates the owner gave.

### Stage 4. Lay Out the Folders

Propose the layout, then wait for the owner's approval before creating anything. The default layout is:

- `technical/`, `business/`, `gtm/`, `methodology/` and `people/`, one folder per `domain` value, named the same way, so Ingest's routing lands new items in the right place without a mapping
- One folder per customer organization, under `accounts/`
- `uncertain/` for items nobody can place
- `continuations/`, the default folder Wrap-Up writes to
- `_system/`, which holds the taxonomy file and the how-to page

Competitors, plays, pricing and the customer archetype sit under `gtm/`. Personas sit under `people/`. Each customer account gets its own folder. If the team already keeps folders under other names, those names win. Ingest reads folder names from the profile's `## Ingest` section, one line per `domain` value, so the owner records the mapping there, and the setup repeats it in `_system/adding-knowledge.md` for people.

**Produces:** the approved layout, and then the folders created.

### Stage 5. Seed and Extract

Write each seed item with the full frontmatter from the Output Contract. Each item has one concept, a compiled truth of one to three sentences, and a timeline of dated entries with exact quotes. Every new item gets the status `emergent`, because it has one source so far. Give every item three or more links before saving. When a draft comes out with two, find the third related item first.

Then ask the team three questions about how it actually wins:

- Why do we win the deals we win?
- Which objection actually stops deals?
- What does the buyer say in the second meeting that tells us the deal is real?

Each answer becomes an `emergent` item, quoted exactly as it was spoken, with the speaker named.

Last, write the Company and Competitive Landscape sections into the profile. Each entry carries its grade from the four states in the Output Contract.

**Produces:** the seed items with their frontmatter, and the two profile sections with grades.

### Stage 6. Name the Tags and Relationships

Only now, with real items in place, name the tags. Start with five to seven tags, taken from the words the seed items actually use. Define each one in a single line. Name three to five relationship types, and state what each one means, so a reader can tell a competitor link from a proof link. Write both lists to `_system/taxonomy.yaml`, then write `_system/adding-knowledge.md`, the one-page guide for new team members.

Tags added after this point are new tags. The approver named in Stage 4 decides whether each one joins the list.

**Produces:** the taxonomy file and the how-to page.

### Stage 7. Prove It by Querying

The operator asks the base at least three questions the team really asks, in the team's own words. The skill records each question and the answer pasted in full, with the file the answer came from and that item's date. The skill does not describe the answer from memory.

The check uses four tiers. The claim slip below states which tier a claim reached.

| Tier | Name | What it means |
|------|------|---------------|
| 1 | Exists | The file or folder is there and is not empty |
| 2 | Substantive | The content is real, not a placeholder |
| 3 | Wired | Something reaches it: links resolve and other items point at it |
| 4 | Functional | A question was asked of the base just now, and the answer, pasted, came from the files |

Reading the folders by hand reaches tier 3 at most. Only a query run against the real files reaches tier 4.

If an answer is wrong, the claim goes back and is not passed. The operator confirms which item is out of date. The setup does not archive it, because archiving belongs to Dream. Instead, with the owner's approval, it rewrites that item's compiled truth to what is true today, adds a dated timeline entry that records the correction and its source, and lists the item for Dream's next run. Then the question is asked again, and the new answer is pasted.

When the queries pass, agree the maintenance cadence with the owner. The cadence has three parts: ingest new material when it arrives, run a health check each week, and run a deeper review of the base on an interval the owner chooses, either every two weeks or monthly. Name one owner by role. Write the Knowledge Base section with that cadence.

If the query cannot run in this session, for example because the base is not reachable, the claim stays at the tier it reached, and the tier statement uses the honest sentence instead.

The claim slip has four fields, in this order:

```text
Claim: The base answers the team's questions.
Tier: [1 Exists, 2 Substantive, 3 Wired or 4 Functional]
Check: [the questions asked, and the file each answer came from]
Evidence: [the answers, pasted, from this session]
```

The tier statement is the last line of the setup's final message. When Wrap-Up closes the session, it records that statement under Where We Stopped, the way it records any verified claim. The setup writes no continuation note itself. If tier 4 was not reached, the statement reads: "Built, and not yet verified, because [reason]."

**Produces:** the query log with the pasted answers, the cadence, the Knowledge Base section, and the tier statement.

---

## Epistemic Rules

- **Every claim sits on one rung of the evidence ladder.** The rung is shown wherever the claim appears, using the four grades in the Output Contract.
- **n beside every rate.** Write "3 of 4 buyers (n=4)", never a rate with no count beside it. The reader needs the count to judge the rate.
- **Five before a pattern.** Fewer than five cases is an observation, and it is labelled as one.
- **Silence is not a no.** A file that says nothing about a price does not show that the price is absent. It is left out of that count.
- **"No difference" is a finding.** Report it. Do not keep slicing the material until a cut looks significant.
- **An `assumed` claim is an open bet.** Discovery lists open bets, and Positioning refuses to build its statement on a claim still graded `assumed`, so an inflated grade here would reach a price.

---

## Hard Rules

1. **Never build a base without a real seed item.** Reason: an empty base has nothing to check its answers against, so every later answer would be unchecked.
2. **Never write a folder, file or profile section before the owner approves the layout.** Reason: the layout is the structure every later skill reads, and it is expensive to move after it is in use.
3. **Never name a tag before the seed items exist.** Reason: a tag named first describes content nobody has checked, and it stays on the list after the content proves wrong.
4. **Never write Working Memory records, and never archive an item.** Reason: records such as continuation notes and health reports are evidence that other skills create when they run, and archiving belongs to Dream alone, after the owner approves. A record written or an item archived by the setup would look like a run that never happened.
5. **Never grade a claim above its evidence.** Reason: a grade is read downstream as a fact, so an inflated grade spreads to every skill that reads it.
6. **Never set `valid_until` on a standing decision, an account record or a person record.** Reason: a dated fact belongs in its own item, so the expiry falls on the fact that changes, not on a record that is still true.
7. **Never write an item with fewer than three links on purpose.** Reason: an orphan is hard to find, and the structure check flags it as a fault.
8. **Never call the setup done without a query.** Reason: a base nobody has asked is an untested claim, and the tier statement must say so.
9. **Never add a name, price, date or count the material does not contain.** Reason: an invented detail becomes one of the base's first answers, and nobody can check it against a source.

---

## Quality Bar

The setup is done when every item below is true. Record the evidence beside each one.

- [ ] A real seed item is present and named. **Evidence:** its file path.
- [ ] Every file in the inventory is sorted into still true, stale or unknown, with counts. **Evidence:** the sorted list.
- [ ] The owner approved the layout before any folder was created. **Evidence:** the owner's reply.
- [ ] Every item has the full frontmatter and three or more links that resolve. **Evidence:** the link count for each item.
- [ ] Tags and relationship types were named after the seed items existed. **Evidence:** the taxonomy file, with its creation order.
- [ ] Each entry in the Company and Competitive Landscape sections carries a grade. **Evidence:** the two sections.
- [ ] The Knowledge Base section has all five fields, with "none yet" or `[ASK LATER]` where the owner did not answer. **Evidence:** the section text.
- [ ] Three questions were asked, each answer is pasted, and each answer names its source file. **Evidence:** the query log.
- [ ] The tier statement is the last line, and it states a tier the evidence reached or the honest sentence. **Evidence:** the final line.

---

## Examples

### Example. PlotIQ, the Invented Company

PlotIQ is an invented deathcare software company. Its cast and facts come from the shared example profile. Every number below is tagged **essay** (it comes from the published Guild article on the context audit) or **example** (it was made up for this walk-through).

**Stage 1.** The operator has a folder of product notes, two call transcripts, last year's pricing sheet and a competitive one-pager. That makes 23 files (example). Nothing is organized, and the profile has no Knowledge Base section yet. The skill says once that no base exists and that it will set one up.

**Stage 2.** The operator says nothing is written down yet. The skill stops, names the pricing sheet and the two calls as acceptable seeds, and the operator pastes the pricing sheet. The gate passes.

**Stage 3.** Each file gets the still-true question. 17 of 23 files (74%, n=23, example) are still true. The other 6 (26%, n=23, example) are stale or unknown. The article's own run found roughly three quarters of its pile stale (essay), which is a different pile measured another way. The pricing sheet is last year's, so its price line is marked stale. The owner gives the next pricing review date, and the price item carries it as `valid_until`. The standing decision on who signs gets no expiry.

**Stage 4.** The owner approves the layout with the base at `plotiq-base/` (example), which is also the project key Wrap-Up uses for the session's continuation note. The skill then creates the routing folders and one folder for each of the three named customer organizations (example).

**Stage 5.** The skill writes nine seed items with the full frontmatter (example). It then asks the three team questions from Stage 5 (essay, from the published article). Each answer becomes an `emergent` item, quoted exactly. One answer, in the operator's words: "They ask for the trust fund statement on the second call, that's when we know it's real" (example). The first draft of one item had two links (example). The skill added a third, because a two-link item is an orphan under the base's rule.

The Company section records "Cemetery general managers sign the contract" with the grade `heard`, because two buyers said it on calls (n=2, example). The grade stays below `seen`, because no signed contract exists yet to show it in behavior.

**Stage 6.** Five tags: `customer-voice`, `price-check`, `competitor`, `proof` and `open-question` (example). Three relationship types: "sells to", "competes with" and "proves" (example).

**Stage 7.** The operator asks three questions the team asks (example).

1. "Which competitor did we last lose a deal to?" The base returns a competitor the team stopped meeting. The item's compiled truth is a year old. **This is a failure.** The query ran against the real files, so it reached tier 4, but the answer was wrong, and a wrong answer means the claim goes back. The operator confirms the item is out of date. After approval, the skill rewrites the compiled truth to the current competitor, adds a dated timeline entry naming the call that said so, and lists the item for Dream's next run. The re-run returns the current competitor, and that answer is pasted.
2. "What do we charge for the first year?" The answer comes from the pricing item, and it shows that item's date.
3. "Who do we talk to first at an independent cemetery?" The answer comes from the people item, using its dated timeline.

The cadence goes into `Maintenance cadence`: ingest as material arrives, a health check each week, and a deeper review every two weeks (example), owned by the operations role.

**Open items, left unverified.** All nine seed items are `emergent`, because each has one source so far, and only the owner promotes an item, usually once a second source or Dream's review supports it. Two of them were never queried (example): the objection item from the team's second question, and the people item's second contact. The base lists them as open items, and when Wrap-Up closes the session it carries them under Open Threads.

The final claim slip for the example:

```text
Claim: The base answers the team's questions.
Tier: 4, Functional, for three queries (example), after one fix (example).
Check: three queries run against the files, with each answer pasted and its source file named.
Evidence: query 1 failed and was sent back, then passed on the re-run. Queries 2 and 3 (example) passed on the first run.
```

Tier statement: the claim that the base answers the team's questions reached Tier 4, Functional, on all three queries (example) after one fix (example), and two items (example) were never queried and stay open.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| The operator has nothing written down | No real file exists yet | Stop at Stage 2. Name the places a seed usually sits, and resume once one is in hand |
| Every Company entry is graded `assumed` | No source has been named for any line | Name one source for each line. `assumed` is a valid grade, and it marks an open bet |
| A query returns an answer the team does not recognize | An item is out of date, or was written from a weak source | Send the claim back. Confirm the item with the owner, correct its compiled truth with a dated timeline entry, list it for Dream, and re-run the query. The setup never archives |
| A query cannot run in this session | The base is not reachable from here | Keep the claim at the tier it reached. Use the honest sentence and name the check that would close the gap |
| A custom GPT cannot see the base | Files were not attached to the GPT | Attach the base files to the custom GPT, then ask the query again |
| A skill reports that it cannot find the base | The Knowledge Base heading or a field name is wrong | Check that the heading is exactly `## Knowledge Base` and that the five field names match |
| The tag list grows every week | Tags are being named without the approval step | Route new tags through the approver named in Stage 4, and remove any that no item uses |

---

## Best Practices

- **Start with the material people already use.** The setup goes faster when the seed is a file someone opened last week, because its age is easy to check.
- **Grade in the open.** Show the grade beside each claim. A reader should never have to ask how sure the team is.
- **Name the owner by role.** A role outlives a staff change. A person's name does not, and the base needs a named owner that survives one.
- **Ask the question the team really asks.** A question invented for the test is one the base may answer well without being useful. The three questions in Stage 7 should come from real requests.
- **Keep the tier statement honest.** A short, accurate statement helps the next reader more than a confident one that the next query disproves.

---

## Integration With Other Skills

Each field name below is read by the next skill by its exact name. Do not rename any of them.

| From the setup to | What is read, by name |
|-------------------|------------------------|
| Discovery | The profile sections Company, ICP Definitions, Buyer Personas, Core Pain Points and Competitive Landscape, by those names, and the base location from the `Location` field of `## Knowledge Base` (Discovery 2.1.1). Discovery creates its claims ledger at `<base>/gtm/claims-ledger.md` on its first run and writes back five fields by name: "Customer archetype", "Competitive alternatives", "Beachhead segment", "Buyer persona" and "Open bets". Its five output nodes carry the shared item frontmatter, filed under `gtm/` and `people/` |
| Positioning | The five Discovery fields above, plus the profile sections Company, ICP Definitions, Buyer Personas, Core Pain Points, Value Propositions, Competitive Landscape and Proof Points, and the deal and pricing history |
| Launch and Engine | Discovery's `Customer archetype` field with its confidence, read by that name. The starting segment stays a Discovery item in the base |
| Ingest | The base location from `## Knowledge Base`, and the tag list from its `Taxonomy file` field (Ingest 2.0.1). Non-default folder names are recorded in Ingest's own `## Ingest` section, one line per `domain` value |
| Graph Health | The item frontmatter: `name`, `domain`, `node_type`, `status`, `created`, `updated`, `tags` and `related`. The base location and the tag list come from its own `## Graph Health` section when that names them, and otherwise from `Location` and `Taxonomy file` in `## Knowledge Base` (Graph Health 2.0.1) |
| Dream and Weekly Review | The same item frontmatter. Dream also reads `valid_until` and the compiled truth, and only Dream archives. Weekly Review reads the Graph Health hand-off fields and counts items from `created` and `updated` |
| Wrap-Up | The base location from `## Knowledge Base`. Wrap-Up writes its notes to the folder named in its own `## Wrap-Up` profile section, and its default is a `continuations` folder inside the base, which is why the setup creates that folder. Its notes carry `project`, `date`, `status` and `next_action`, with the sections Where We Stopped, What Happened, Decisions Made and Open Threads. Wrap-Up 2.0.3 names the setup's tier statement as a Where We Stopped source, and the unverified items go under Open Threads |
| The sales skills | The profile sections by name: Company, ICP Definitions, Buyer Personas, Core Pain Points, Value Propositions, Competitive Landscape and Proof Points |

**Next action, in Wrap-Up's form.** Run Ingest on the first new transcript or document the team names, into the base folder from `## Knowledge Base`. One step, one named object, resumable by someone who was not in the session. Graph Health follows on the next health check, where it confirms the links and tags landed.

---

## Changelog

### 2.0.0 (2026-10-21)

- Clean-room rewrite from the approved 2.0 specification, replacing the 1.1.2 skill.
- Seed items now come before tags. The workflow runs seven stages in that order, and each stage ends with what it produces.
- Adds the two refusals: no build on zero content, and no completion before a query is answered from the files.
- Adds the claim slip and the four tiers for the final check, with the honest sentence when tier 4 is not reached.
- Writes the `## Knowledge Base` section with five fields, and writes the Company and Competitive Landscape sections with evidence grades.
- Retires the Credits section.
