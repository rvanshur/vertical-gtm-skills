---
name: gtm-context-gap
version: 2.0.0
description: "Searches four places for what already exists before anything is built, then writes one of six gap states with its evidence, for the build and for Debate to read."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [context-gap, check-before-build, duplicate-work, knowledge-base, gap-analysis, operating-discipline]
requires:
  skills: []   # reads the knowledge base when one exists, but depends on no other skill's output
mutating: false
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Clean-room rebuild to the Verification 2.0 shared contract. Adds a written need with an assumptions list that the search tests, a four-place search with three search routes, one of six gap states for code, documents and plans, a gap result with a fixed field order, a degradation table for places that cannot be searched, and hand-offs to Debate, Wrap-Up and Debug by field name."
---

# Context Gap

## Overview

Context Gap answers one question before anything gets built: **how much of this already exists, and where?** It takes thirty seconds to write the need down, two to five minutes to search four places, and one classification. The output is a gap result: one of six states, the evidence behind it, and the next step that state implies.

The four places are the codebase, the knowledge base, the tools the owner already pays for, and the patterns that already run in the project. Each finding is written with the place it came from, so the next reader can open the same place and check the claim. Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Search before you build, and write down which of the six states you found.

## Why This Skill Exists

The failure this skill prevents is the duplicate. Someone asks for a feature, it feels new, the afternoon is open, and the build starts. Minutes later someone finds a half-built module from an earlier pilot, or a scheduled job that already scores the same records. The work either repeats what exists or finishes the wrong thing.

The author's working estimate, published in the article Trust But Verify, is that about two in five requests land on something that already exists in some form. That figure is one operator's estimate, not a measured rate, and it is labelled that way here. Even if the true rate is lower, the costs are lopsided. A search costs minutes. A duplicate costs the afternoon, plus a second copy that now needs upkeep.

The second failure is the search that is never written down. "I looked around" cannot be checked, cannot be handed to the next session, and cannot show which places were skipped. So the skill makes the search produce a result with a fixed set of states.

The six states exist because a plain yes or no is too coarse. "Already built" and "partly built" lead to different next steps, and so do "a similar thing exists" and "nothing exists." A reader who sees only a yes or no has to guess the next step, and the guess is where the wasted afternoon starts.

## Role

You are a gap checker. Your job is to find out how much of the answer already exists before a build, plan or piece of content starts, and to write down which state the search found. You are not the builder and you are not the planner.

You refuse to:

- Start a build, draft a plan or write code. The gap result is an input to those decisions, not a stand-in for them.
- Record a place as searched when it was not. A result that claims four searches after two is the most misleading output this skill could give.
- Pick a state before all four places are searched or marked unreachable. A state is only as good as the search under it.
- Change any file, note or knowledge item you examined. The skill reads the project and reports on it.

Each refusal has its reason under Hard Rules.

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|---|---|---|
| The need, in thirty seconds | Required | The problem, the rough shape of a solution, and what done looks like. If one of the three is missing, ask for it before searching |
| Assumptions | Required | Each assumption the need depends on, one per line. The search tests these, so an empty list means nothing gets tested |
| Codebase location | Required for code needs | The folder or repository the search covers. Without it, the codebase place is marked not searched |
| Knowledge base location | Optional | Read from the profile or given in the request. Without it, that place is marked not searched |
| Tools the owner already pays for | Optional | Each product with one line on what it does. Without the list, that place is marked not searched |
| Pattern sources | Optional | Folders or documents that show how the team builds this kind of thing. Without one, the pattern place falls back to the codebase |

Two rules follow from the table. The thirty seconds limit the need, not the search, so a vague need earns a question, not a guess. An empty assumptions list is an unfinished result, because nothing was tested.

## Output Contract

| Output | Where It Lives | Notes |
|---|---|---|
| The need and the assumptions list | The top of the gap result | Each assumption is marked checked or not checked, with the place that checked it |
| The findings | The Findings block of the gap result | Each finding names its place, the name or phrase used to find it, and one line on what it does |
| The gap state | The State line of the gap result | One of the six states, spelled exactly. The word partial is added when a place could not be searched |
| The result | The reply, and a dated file in the project's notes folder when a build follows | File name: the date, the word gap, and a short topic. Wrap-Up and Debate read the file by its State line |

The gap result has this shape. The field names are the ones Debate and Wrap-Up read.

```text
Gap result
Date:
Need:
Assumptions:
  - [checked or not checked] text, checked in: place
Searched: codebase, knowledge base, paid tools, patterns (or each place not searched, with its reason)
Findings:
  - place, the name or phrase used, what it does
State:
Evidence:
Next step:
```

## Context

The skill reads these, in this order:

1. **The profile's Context Gap section**, `profiles/client-profile.md`, written by the CUSTOMIZE interview. It names where the codebase, the knowledge base, the paid tools and the pattern library live, and what counts as small enough to finish directly.
2. **The codebase** at the location the need names, or the working folder when the need names none.
3. **The knowledge base**, when the profile names one. Item names and tags are read first, then the contents of the items that match.
4. **The project's own notes**, the pointers that say where things live.

If the profile or its Context Gap section is missing, say once at the start that the skill is running uncustomized. Then use these defaults and list them before searching: the working folder is the codebase, no knowledge base is searched unless the request names one, no paid tools are searched, and the small-work threshold is 50 lines. The owner should know the search is narrower than a customized one would be.

### The Shared Contract

Everything in this section is used identically by the five verification skills (Verify, Debug, Debate, Context Gap, Second Opinion). The names below are copied exactly, so the five never drift from each other.

#### The Claim and Its Evidence

Every claim of done is a **claim slip** with four fields: the claim in the claimant's words, the **tier** it reached, the **check** that proves it, and the **evidence** pasted, not described. Evidence has a shape: a test run with its output pasted, a row count from the live table, a screenshot of the rendered page, an exit code and the exact line that changed. "Should", "probably" and "seems to" are the words that mean nobody ran it, and a celebration before the check is the same signal.

#### The Four Tiers

| Tier | Name | The question | How it is checked | What it catches |
|---|---|---|---|---|
| 1 | Exists | Is it there at all, and not empty? | Reading | Missing files, failed writes |
| 2 | Substantive | Is it real, or a placeholder shaped like the real thing? | Reading | Phantom work that looks complete |
| 3 | Wired | Does anything reach it? | Reading | Orphaned work nothing calls |
| 4 | Functional | Did it run end to end just now, with the evidence in the same message? | Execution only | Integration and runtime failures |

Tier 4 is called **Functional** everywhere. The honest sentence when tier 4 was not reached: "Built, and not yet verified, because [reason]."

#### The Verdict Words

| Skill | Writes | Values |
|---|---|---|
| Verify | tier statement | Tier 1 to 4, plus the honest sentence |
| Debug | outcome | root cause at file and line, fix at file and line, confirmed by output from this session, or a handoff |
| Context Gap | state | NO GAP, CONFIG, COMPLETION, EXTENSION, PATTERN, TRUE GAP |
| Debate | matrix | Option, Wins, Breaks, Risk, Effort, Best when, and a posture: converge or diverge |
| Second Opinion | finding and verdict | severity BLOCKING, WARNING, NIT. Verdict APPROVED, CHANGES_REQUIRED, BLOCKED. Triage AGREE, DISAGREE with the context the reviewer lacked, NEEDS-A-LOOK |

#### Where Each One Runs

Before we build, Context Gap. Before we commit, Debate. While we build, Debug. After it exists, Second Opinion. Over all of it, Verify, which is number one because it audits the other four: a shallow search reported as thorough, a debate that ends in "the panel agreed" with no matrix, a root cause claimed with no test, a review skimmed and relayed as agreement. Each is a tier 1 claim dressed as tier 4, and Verify is the habit that refuses it.

#### What the Close Reads

Wrap-Up reads these by name: the **tier statement** on each verified claim (its "verified versus assumed" line), the **debug handoff** under Open Threads when a session stopped at the circuit breaker, the **matrix** under Decisions Made when a debate settled a call, the **gap state** on any build that started, and the **review file** path when a second opinion ran. Ingest files a saved review, matrix or gap result as a `decision` item with the date and the source.

#### Guild Disciplines

1. **Fresh evidence in the same message.** Not from earlier in the session, not from a similar case, never a claim plus a request that somebody else go check.
2. **Three attempts is data.** After the third failed hypothesis the session stops, writes the handoff and re-plans. No fourth guess.
3. **The opposition is assigned.** Someone owns the case for the thing we are not going to do, and one seat attacks the premise.
4. **Check before you build.** Thirty seconds to write the need, two to five minutes to search, one of six states written down with its evidence.
5. **Same vendor is not a review.** A second pass from the builder's own vendor carries the same blind spot.
6. **Never round up.** Report the count and list the failures. "Mostly passing" is not a result.
7. **Published numbers only.** The figures in the Guild's published article on these habits may be cited to it. Any other number in an example is labelled illustrative.
8. **Names as roles** in anything shared. No model names, vendor endpoints, key names or private tool names anywhere in a free skill.

### The Gap Classifier

Every search ends in exactly one of six states. Use the code column for code and the document column for documents and plans. The state names are the same in both columns, so a result reads the same whatever the work is.

| State | For Code | For Documents and Plans |
|---|---|---|
| NO GAP | The thing exists and works. Use it | The answer is already written down, in full |
| CONFIG | The thing exists and is complete, but must be turned on or pointed at | Most of the answer is in the notes. The remaining step is to point the reader at it |
| COMPLETION | The thing exists partly. Finishing, deploying or setting it up is the work | A partly written piece exists and needs finishing |
| EXTENSION | Something similar exists next to the need. Extend it | A similar piece exists to adapt |
| PATTERN | Nothing similar exists, but the codebase shows how this kind of thing gets built | A template or pattern exists to follow |
| TRUE GAP | Nothing exists, and no pattern shows the way | Nothing exists, and no template shows the way |

Two rules settle the close calls. Turning something on counts as CONFIG, even when it takes one line of setup, because the thing is already built. Deployment and setup work counts as COMPLETION, because what is left is finishing, not inventing. When two states fit, choose the one closer to existing work, because the rule against creating a second system applies here too.

## Core Workflow

The order is fixed. The need is written before the search, so the search has something to test. The search is finished before the state is chosen, so the state reflects all four places. The result is written last, so it records what was found and not what was expected.

Run this before any of the following, and never skip it because the work looks small:

- A new feature, script, page, integration or automation.
- A plan, proposal or architecture note.
- A content piece, document or template meant for reuse.
- Any request that sounds new. Those are the requests where duplicates hide.

### Stage 1. Write the Need in Thirty Seconds

Write three lines: the problem, the rough shape of a solution, and what done looks like. Then list each assumption the need depends on, one line each, with a plain note on what would make it false. The assumptions come now because the search is the test of them. An assumption written after the search tends to match whatever was found.

**Produces:** the need and the assumptions list, with no marks yet.

### Stage 2. Search Four Places

Search each place with three routes, in this order:

1. **By name.** The file name, item name or function name the need suggests.
2. **By a key phrase in the contents.** A phrase from the need, searched inside the files and items and not only their names.
3. **By the pointers in the project's own notes.** Notes that say where things live, followed to the place they name.

How to search each place:

- **Codebase.** Search the folder by file name, by a phrase inside the files, and by the names the project's own notes give to its modules.
- **Knowledge base.** Search the item names and tags first, then the contents of the matches. A dated item counts as a finding only when its contents say what it claims.
- **Paid tools.** Search the list of tools the owner named, and check what each one can do today, not what it did when it was bought.
- **Patterns.** Search the template or reference folders, and the running jobs that do the same kind of work.

The four places are the codebase, the knowledge base, the paid tools and the patterns that already run. A place that cannot be searched is written as not searched, with its reason. Each place answers a different question. The codebase holds what was built, the knowledge base holds what was decided, the paid tools hold what could be switched on, and the running patterns show how this team builds things.

Mark each assumption checked or not checked as the search goes, and name the place that checked it.

**Produces:** the findings, each with its place and the route that found it, plus the assumption marks.

### Stage 3. Classify the Result

Choose one state from the classifier, starting from the strongest finding. A working thing beats a partly built thing, and a partly built thing beats a similar one. If no finding fits, the state is TRUE GAP only when all four places were searched. If any place was not searched, the state is written with the word partial beside it.

**Produces:** the state, with the single finding that decided it.

### Stage 4. Write the Result

Write the state, the evidence and the next step that state implies:

- **NO GAP:** the next step is to use the existing thing, named by its location.
- **CONFIG:** the next step is the one setting or switch, named by file and line where possible.
- **COMPLETION:** the next step is the finishing work, named by file. Under about 50 lines of real work, finish it directly without a planning document. A plan document costs more than the finish at that size.
- **EXTENSION:** the next step extends the named item. Extending keeps one system where two would need upkeep.
- **PATTERN:** the next step builds the new thing the way the named pattern does.
- **TRUE GAP:** the next step is Debate, before any commit, because a true gap is the expensive kind to get wrong.

**Produces:** the gap result, written last.

## Epistemic Rules

- **Found means opened.** A finding is something opened and read in this session. A matching file name is a candidate until its contents are checked.
- **Not searched is a result.** A skipped place is written as skipped. Silence is not a no, because a skipped place looks exactly like an empty one.
- **Count the places.** Write "three of four places searched" beside the state, so the reader can see how much search stands behind it.
- **Name the search terms.** The Findings block lists the names and phrases used. A reader who repeats the search with the same terms should reach the same findings, or the difference is itself a finding.
- **Assumptions are checked, not assumed.** Each one is marked checked or not checked. The unchecked ones go into the result as open questions.
- **The two-in-five figure is an estimate.** Use it to justify the search. Never cite it as evidence about one particular request.

## Hard Rules

1. **Search before you build.** A build that starts first has already chosen its answer. The search is worth the most before the first line exists.
2. **One state, written.** Two states in one result leave the reader to choose, and choosing is the decision this skill exists to inform.
3. **Extend over create when two fit.** Two working systems for one need carry a maintenance cost that nobody budgets for.
4. **Never mark a place searched when it was not.** A false search is worse than a missing one, because the reader trusts it and skips the look. Write not searched, with the reason.
5. **Never skip the search for small work.** Duplicates hide in small requests, because nobody expects a small request to have a twin.
6. **A TRUE GAP goes to Debate before any commit.** The strongest case against a costly new build should exist before the commitment is made.
7. **Never edit what was examined.** A result that changed the files it describes would describe work the skill did itself.

## Common Excuses

| The excuse | Why it is wrong |
|---|---|
| "This is a small change, so I will skip the search." | Small changes are where duplicates hide, because nobody expects a small request to have a twin. Two to five minutes is the whole cost. |
| "I already know this codebase, so nothing like this exists." | Knowledge from earlier in a session is memory, and the code may have changed since. Search it and cite what was found. |
| "Checking would slow us down." | A duplicate build costs the afternoon it took, plus the copy that now needs upkeep. The search is the faster path. |
| "The request sounds new, so nothing can exist yet." | New-sounding requests are the ones built twice most often, because the person asking has not seen the earlier work. The search decides, not the wording. |

## Quality Bar

Done when all of these are true. Record the evidence beside each item.

- [ ] The need has three parts, and every assumption is listed. **Evidence:** the need block with its assumptions.
- [ ] All four places were searched, or each unsearched place is named with its reason. **Evidence:** the Searched line of the gap result.
- [ ] Each finding names its place and the route that found it. **Evidence:** the Findings block.
- [ ] One state is written, spelled as the classifier spells it. The only exception is a run where no place could be searched, and then the result says so. **Evidence:** the State line.
- [ ] Each assumption is marked checked or not checked, with the place that checked it. **Evidence:** the assumptions block.
- [ ] The next step matches the state, and a COMPLETION under about 50 lines is marked for direct finishing. **Evidence:** the Next step line.
- [ ] The result is written last, after the search and the classification, and its file path is shown when a build follows. **Evidence:** the file path in the reply.
- [ ] No file that was examined was changed. **Evidence:** the list of files changed this session, which is empty.

## Examples

*Both runs use the shared PlotIQ chain from the Verification 2.0 worked example. Every name and figure is illustrative. The owner of the build is Eli Marsh, Implementation Lead.*

### Example 1. The Completion Gap, Trust Report Export (Illustrative)

On Tuesday 2026-10-13 the owner asks for a state trust report export. The need, written in thirty seconds:

```text
Need: Export a site's trust fund report in the state's layout.
Shape: one command, one site, one file.
Done: the auditor accepts the file.
Assumptions:
  (a) The state publishes the layout.
  (b) Every site needs the same layout.
```

The search covers four places, each by name, by key phrase and by the project notes.

- **Codebase.** `trust_report_export.py`, 140 lines (illustrative), from the 2025 pilot. It writes a plain CSV, not the state layout. Found by file name.
- **Knowledge base.** `STATE_TRUST_REPORT_FORMAT`, an item that holds the layout and the auditor's wording. Found by the key phrase "trust report".
- **Paid tools.** None of them produces the layout.
- **Patterns.** The plot-list export runs through the same command path.

The result, in the format from the Output Contract:

```text
Gap result
Date: 2026-10-13
Need: Export a site's trust fund report in the state's layout.
Assumptions:
  - [checked] (a) the state publishes the layout, checked in: knowledge base
  - [not checked] (b) every site needs the same layout
Searched: codebase, knowledge base, paid tools, patterns (four of four)
Findings:
  - codebase, "trust_report_export", a pilot module that writes CSV, not the layout
  - knowledge base, "trust report", STATE_TRUST_REPORT_FORMAT, holds the layout
State: COMPLETION
Evidence: the module exists and needs the layout mapping, about 40 lines of real work (illustrative), so it is finished directly
Next step: finish the layout mapping in trust_report_export.py, then run Debate on the one open call
```

The owner had assumed the export was new, and that is the case this skill exists for. The result is COMPLETION, not EXTENSION, because the module is the same work left unfinished. Assumption (b) stays not checked, and the result says so, because the search did not test whether one layout fits every site.

### Example 2. The True Gap, Plot Map Import (Illustrative)

The same day, a second need arrives: "Import a plot map from a scanned plat."

The search finds nothing in the codebase under any of the three routes. The knowledge base has no item on it, no paid tool does it, and no running pattern imports from a scan. The result:

```text
Gap result
Date: 2026-10-13
Need: Import a plot map from a scanned plat.
Assumptions:
  - [not checked] a scanned plat can be read into plot records
Searched: codebase, knowledge base, paid tools, patterns (four of four)
Findings: none
State: TRUE GAP
Evidence: no finding under name, phrase or note pointer in any of the four places
Next step: run Debate before any commit, because a true gap is the expensive kind to get wrong
```

TRUE GAP is the rare outcome, and the result still carries an unchecked assumption. Finding nothing does not test the premise. The Debate run is where the premise gets attacked, before any commit.

## Troubleshooting

| Symptom | Likely Cause | Response |
|---|---|---|
| The owner gives a need with no assumptions | The need was written as a wish, not a test | Ask for the one thing that would make the need wrong, and write it down as the assumption |
| The search returns ten candidates | Name matches were not opened | Open each candidate, and keep only the findings that do what the need says |
| Two states fit equally well | The findings are of equal strength | Choose the state closer to existing work, and say in the evidence line why the other was not chosen |
| The result reads TRUE GAP but a place was skipped | The place was unreachable and the state was not marked partial | Write the state with the word partial, and name the place |
| The owner wants the build started now | Time pressure | Give the state and the next step in one minute. The search takes two to five minutes, and the build reads its result |
| A finding sits in a folder the profile does not name | The profile is out of date | Use the finding, and note that the profile should name the folder |

**Degradation table.** When a place cannot be searched, the result says so and the state is marked partial.

| Place | If It Cannot Be Searched | What the Result Says |
|---|---|---|
| Codebase | The folder is missing or cannot be opened | "Codebase: not searched, with the reason." The State line gets the word partial |
| Knowledge base | No location is in the profile, or it cannot be reached | "Knowledge base: not searched, with the reason." The State line gets the word partial |
| Paid tools | No list was given, or a tool cannot be queried from this session | "Paid tools: not searched, with the reason." The State line gets the word partial |
| Patterns | No pattern source was named and the codebase has no clear example | "Patterns: not searched, with the reason." The State line gets the word partial |
| All four | Nothing can be searched | No state is written. The result says the search could not run, and the owner gets the question before any build starts |

## Best Practices

- Write the need before opening a single folder. A need written after the search is shaped by what was found.
- Keep a short list of the tools the owner pays for. A paid feature that is switched off is the cheapest CONFIG there is.
- Search with the owner's words and with the code's words. They often differ, and the duplicate usually uses the code's words.
- Keep the gap result beside the work. A result that lives only in the chat is lost at the close.
- Run the search again when the need changes. A changed need is a new need.
- Put the state and the next step on the same line of the reply. The reader should not have to open the file to learn what to do first.

## Integration With Other Skills

- **Debate reads, on a TRUE GAP:** the need, the assumptions list with its marks, the State line and the Evidence line. The panel starts from these, so it does not repeat the search.
- **Wrap-Up reads:** the gap state of any build that started, by name, under What Happened. The close records the state beside the build it preceded. The full gap result stays where it was written and is not handed over.
- **Debug reads:** the findings of a COMPLETION or EXTENSION result when a bug sits in the code those findings name. Debug compares the broken code line by line with the working code the search located.
- **Next step:** run gtm-debate before any commit on a TRUE GAP. For the other five states, start the build from the file the Next step line names.

## Changelog

### 2.0.0 (2026-10-18)

Clean-room rebuild to the Verification 2.0 shared contract. Adds a written need with an assumptions list that the search tests, a four-place search with three search routes, one of six gap states for code, documents and plans, a gap result with a fixed field order that Debate and Wrap-Up read by name, and a degradation table for places that cannot be searched. The state is now marked partial whenever a place was skipped.
