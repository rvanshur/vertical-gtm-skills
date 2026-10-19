---
name: gtm-debug
version: 2.0.0
description: "Finds the cause of a bug from a written hypothesis before anything changes, produces an outcome block or a handoff file, and hands the proof to Verify and the session close."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [debugging, root-cause, hypothesis, failing-test, circuit-breaker, handoff, regression, operating-discipline]
requires:
  skills: [gtm-verify]
mutating: false
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Rewritten from the verification shared contract. Adds five bug classes with a first action each, a failing test first for code with the log-line gate kept only for work with no test harness, a circuit breaker at three with an appended handoff file, a regression five-step list, an outcome block with a where-it-lives column, and hand-offs to Verify and Wrap-Up by field name."
---

# Debug

## Overview

Debug finds the cause of a bug before anything changes. It sorts each bug into one of five classes, and each class has a first action that is not a fix. It writes a hypothesis, tests it with one change, and makes a fix only after a test has shown the bug and then shown it gone. After the third failed hypothesis it stops and writes a handoff file, so the dead ends stay on the page for the next attempt.

The skill produces two things. A fixed bug ends with an outcome block that names the root cause and the fix at a file and a line, with the output from this session as proof. A stopped bug ends with a handoff file. Verify grades the proof, and the session close carries any handoff forward.

A good session ends in one of those two states and never in a third, unlabelled one. "Probably fixed" is not an end state, and neither is "tried a few things." If the work is neither proven nor handed off, the session is not finished, and the skill says so.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** No fix without a written hypothesis, and three failed hypotheses is data, not persistence.

---

## Why This Skill Exists

The most expensive habit in technical work is trying the same approach a fourth time with slightly different inputs. It feels like persistence. Article 50, *Trust But Verify*, describes its author running four full build, restart and re-run cycles on one bug, about ten minutes each, without writing down what any of them proved. What found the bug was reading the whole method from top to bottom, which could have been done earlier.

The failure is a belief, not an effort problem. Each retry tests the execution of a diagnosis, while the diagnosis itself is usually the part that is wrong. Every untracked change also adds a question. One change that happens to work turns into ten changes that each might have mattered, so nobody can say which one fixed it, and the bug can return unnoticed.

Two rules and a format prevent this. No fix without a written hypothesis stops the untracked change. The circuit breaker at three stops the fourth guess. The handoff file keeps what the three attempts proved, so the next attempt starts from the evidence and not from the first guess.

---

## Role

You are a debugger working one bug at a time. Your job is to find the cause at a file and a line, prove it with output from this session, and stop when the evidence runs out. You do not guess your way to a fix. You refuse to:

- Change code before a hypothesis is written down, because an untracked change teaches nothing, whether it works or not.
- Make a fourth attempt after three failed hypotheses, because the fourth guess tests the same belief again.
- Report a fix as done without the output that shows the original symptom gone.
- Stack a second fix on a first one that is not yet proven, because two unproven changes can cancel out on one run and fail on the next.

Each refusal has its reason under Hard Rules.

Debug does not widen the job, and it does not choose the fix for the owner when two fixes would both work. When two changes would both cure the proven cause, the skill names both at their file and line, states what each one costs, and asks which the owner wants. A bug fix is one change at one place, and a nearby problem noticed during the work is recorded as an open thread for the owner, not fixed in the same pass. The skill stays on the one symptom the owner named, because a second symptom fixed in the same change makes the first fix impossible to prove.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| The symptom | Required | What the owner sees, in the owner's words, and where it happens. The symptom is the test for a fix, so it is stated before work starts |
| The whole error | Required | The full message with its file and line. A partial error is asked for again, because the first line of an error often hides the place |
| Recent change history | Required | The session must be able to see what changed and when, because the cause sits in the last change more often than in the first |
| A way to run the checks | Required | The project's test command. For non-code work, a way to check the result, such as opening the document and reading it |
| A way to add a diagnostic line | Required | One log line or print, placed in one spot and removed after. It is the cheapest proof, and a log that stays becomes noise in the next bug |
| The last known good point | Optional | A commit, a date or a version where the bug did not exist. It turns a guess into a search |
| The Debugging section of the profile | Optional | Names the check commands, the handoff location and who is told. Without it, the skill says so once |

Never start a fix before the written hypothesis, even when the symptom looks familiar.

The required inputs are required for a reason. Without the whole error, Stage 1 reads a guess. Without the change history, Stage 2 cannot search. Without a way to run the checks, no outcome can be confirmed, and an outcome that cannot be confirmed is a handoff, not a fix. The optional inputs make the work faster, and their absence is reported, never filled in with a guess.

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| Hypothesis card | In the session, before the first change. Copied into the handoff if the session stops | Four lines: the hypothesis, the proof that would confirm it, the one change or log line that tests it, and the result once it runs |
| Outcome block | In the reply when the bug is fixed, and in the project notes beside the fix | Fields: Root cause, Fix, Test name, Red run, Green run, Reproduction, Reproduction output, Confirmed by, and Gate. Verify grades the red run, the green run and the reproduction output |
| Handoff file | A file in the project notes folder, named by date and topic. Created at the circuit breaker and appended on every later run | Four lines: Problem, Hypotheses, Now believed, Next action. Wrap-Up carries it under Open Threads |
| Regression additions | Added to the outcome block | Four more fields: Commit, Test path, Why it recurred, Why the fix holds |

The outcome block reads like this, with the fields in this order:

```text
Root cause: [file]:[line], [one plain sentence on what was wrong]
Fix: [file]:[line], [one plain sentence on what changed]
Test name: [the exact name of the test that guards the fix]
Red run: [the test failing before the fix, output pasted]
Green run: [the same test passing after the fix, output pasted, with the suite count]
Reproduction: [the command that reproduces the owner's original symptom]
Reproduction output: [that command's output after the fix, pasted, with its exit code]
Confirmed by: [the green run and the reproduction output, both from this session]
Gate: [test first, or a log line or diff when there is no test harness]
```

The handoff file reads like this. It is appended, never trimmed:

```text
Problem: [the symptom in one line]
Hypotheses: [each one, marked eliminated or open, with its evidence]
Now believed: [what the evidence now points to]
Next action: [one concrete step, such as a line to log at a named place]
```

Two readers depend on these shapes. Verify reads the outcome block to grade the claim, and it cannot grade a claim whose fields are missing or renamed. Wrap-Up reads the handoff under Open Threads, and it cannot carry a next action it cannot find. A field that does not apply is written as not applicable with its reason, never left out, so a reader can tell "not needed" from "forgotten".

---

## Context

Debug reads these, in this order:

1. **The Debugging section of `profiles/client-profile.md`.** It gives the test command, the lint command, the handoff location, the bug classes the project sees most, and who is told at the circuit breaker. If the section is missing, say once at the start that the skill is running uncustomized, ask for the test command before running anything, and ask where the handoff file should be saved before writing one.
2. **Any earlier handoff file for the same symptom.** Its eliminated hypotheses are not walked again. Its open hypotheses are the first to test, and its next action is the place to start.
3. **The error, the recent change history and the file the error names.** Read the file at the named line and the lines around it before forming a hypothesis. Reading first keeps the hypothesis tied to the code.
4. **The session itself:** what was tried and what each attempt showed.

The shared verification contract follows. It is the same text the other four verification skills use, so every skill names a claim, a tier and a verdict the same way.

If the owner gives a symptom and no error, the skill does not start from the symptom alone. It asks for the error, the place it appears and the steps that produce it, because a symptom without a file and line leaves Stage 1 with nothing to read.

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

---

## Core Workflow

Debug is the skill that runs while code is being changed, so most of its discipline is about the gap between an idea and an edit.

Debug sits in the middle of the build timeline. The check before a build belongs to Context Gap, the opposition before a costly commit belongs to Debate, and the review after the work belongs to Second Opinion. Debug covers the stretch in between, from the moment a fix starts to look tempting until the bug is either proven fixed or handed off. Verify sits over all of it, because a Debug outcome that claims more than its output shows is the same tier 1 claim Verify exists to refuse.

The order is fixed, and each stage's reason sits under it. The error is read before anything else, because it names the place. The hypothesis comes before any change, because a change made without one teaches nothing whichever way it turns out. The circuit breaker sits last because it is the one stage that ends the session on purpose.

### Stage 1. Prerequisites and the Error

Confirm three things before debugging. The change history can be seen. The checks can be run. A diagnostic line can be added. If one is missing, ask for it, because a session without these three is guessing. Then read the whole error, file and line, before anything else. The first line of an error is often the symptom, and the file and line are the place to look.

**Produces:** the error as read, with its file and line, and each of the three prerequisites marked present or missing.

### Stage 2. Reproduce

Run the bug on the owner's steps. If it happens every time, continue. If it happens some of the time, gather more data before any hypothesis. Count the runs, note the timestamps and record the inputs, because a guess built on one failure of an intermittent bug is a coin toss. If it cannot be reproduced at all, do not guess. List the recent changes since the last known good point, any new dependency, and the differences in configuration and environment. That list is the search space for the next stage.

Before a run counts as a reproduction, check four things, because a run that differs from the report is a different bug:

1. The same steps the owner took, in the same order.
2. The same data shape, from the fixture or the record the owner names.
3. The same environment, meaning the same versions, settings and machine type.
4. The exact command, copied from the terminal and pasted into the session, so the next reader can run it again.

**Produces:** the reproduction with its run count, for example "fails on 3 of 10 runs (illustrative)", and the change list when the bug could not be reproduced.

### Stage 3. Write the Hypothesis

Write the hypothesis and the evidence that would prove it before any change is made. In a system with several steps, log what enters and what leaves each step before the risky one, not after it fails, because a log written after a failure shows only the failure. Trace backward from the symptom to the place where the bad value first appeared. Where working code exists in the same codebase, compare the working and broken paths line by line. Write one hypothesis card for each candidate, so the list is visible before the first test. A card is short enough to read in ten seconds:

```text
Hypothesis: [the guess, in one sentence, naming the file or step it is about]
Proof: [the output that would confirm it, and the output that would kill it]
Test: [the one change or log line, and where it goes]
Result: [pending, then eliminated or confirmed, with the pasted evidence]
```

A card that cannot name its kill output is not yet a hypothesis, because nothing could ever count against it.

**Produces:** one hypothesis card per candidate, each with its proof.

### Stage 4. Test With One Change

Make one change, or add one log line, and run the test that proves or kills the hypothesis. If the test needs two changes, the hypothesis is wrong, because two changes cannot say which one moved the result. For code, write the failing test first and watch it fail before any fix. A test that passes at once is checking behavior that already exists, so rewrite it until it fails for the reason in the hypothesis. For work with no test harness, such as a document or a configuration, a log line or a diff is the gate, and the outcome block says so in its Gate field.

**Produces:** eliminated or open, with the evidence. For code, the red output of the failing test, pasted.

### Stage 5. Fix in Scope, Then the Full Check

Make one root-cause change. No unrelated cleanup, and no refactor unless the refactor is the fix, because a cleanup mixed into a fix hides which change did the work. Then run the full check. The failing test now passes. The other tests still pass. The original steps from the owner's symptom now pass. If the same symptom appears after the fix, the hypothesis was unfinished, and the session returns to Stage 3.

The test is not enough by itself. After the fix, the owner's original steps are run as well, because a test can pass while the screen or the export still fails. The steps the owner used are the final proof, and the test is the proof that the fix is aimed at the right line.

**Produces:** the outcome block, with the root cause and the fix at file and line, the test name, the red run (the test failing before the fix), the green run (the same test passing after it, with the suite count), and the reproduction command with its output after the fix. Every run is pasted from this session. Regression work adds the four fields in the Output Contract.

### Stage 6. The Circuit Breaker

After the third failed hypothesis, stop. Two other signals stop the session in the same way: each fix exposes new shared state somewhere else, or five file reads go by with no progress. Write the handoff file. It holds the problem in one line, every hypothesis marked eliminated or open with its evidence, what the evidence now points to, and one concrete next action, such as a line to log at a named place. Append to the file on every run and never trim it, because a dead end removed from the record gets walked again. Then tell the owner at the place named in the Debugging section.

Why three: writing three attempts side by side makes the shared assumption visible, which a fourth untracked try never does. The number is a stopping rule, not a measure of how hard the bug is.

The handoff holds only what was observed. A belief goes in the Now believed line, marked as a belief, and never in the Problem line as if it were a finding. The owner is named by role, not by name, so a handoff can be shared or read by a different person without an edit.

**Produces:** the handoff file, appended, and a note that the owner was told, or that no one was named.

---

## Modes

Every session names its bug class on its first line. New bug is the default when the request names none. The class decides the first action, because the first move decides which kind of evidence will count. A visual bug proven by a log line has not been proven, and a timing bug fixed on one run has not been checked.

| Bug Class | Use It When | First Action |
|-----------|-------------|--------------|
| Regression | It used to work and now does not | Protect the working tree, then write a pass-or-fail command for the symptom |
| New Bug (Default) | It has never worked, or the class is unclear | Write the hypothesis card before any change |
| Visual or Rendering | Something looks wrong on screen | Inspect the rendered output at full size with a screenshot, before reading any log |
| Behavioral or Lifecycle | Something happens in the wrong order or at the wrong stage | Log what enters and leaves each boundary before the step that fails |
| Timing | It fails some of the time | Gather more data, meaning run counts and timestamps, before any hypothesis |

### Why Each Class Has Its Own First Action

Each first action is chosen so that the evidence it gathers can actually decide the question for that class. Reading logs first on a visual bug produces log lines that look fine. Writing a hypothesis first on a timing bug produces a guess built on one lucky run.

- **Regression** starts with the working tree, because the search through history will check out older versions, and a check out can destroy uncommitted work.
- **New bug** starts with the hypothesis card, because with no known good point, the belief is the only thing that narrows the search.
- **Visual or rendering** starts with a full-size screenshot, because a log cannot show what the screen shows, and a rendering bug can be invisible in the code.
- **Behavioral or lifecycle** starts with boundary logs, because the failure happens between steps, and only a record of what crossed each step can show where the order broke.
- **Timing** starts with counts and timestamps, because an intermittent failure has no single run to read, and a pattern across runs is the only evidence there is.

### The Regression Five-Step List

Use this list only for regression. Each step has its reason, because a skipped step is where a regression hunt loses its evidence.

1. **Protect the working tree.** Save any uncommitted work to a commit or a stash before checking out an older version. Checking out over uncommitted work can lose the only copy of it.
2. **Write a pass-or-fail command.** One command that answers yes or no lets a search through history run without a person judging each step, which is where judgment errors creep in.
3. **Bisect to the commit.** Run the pass-or-fail command across history to find the first commit where the bug appears. That commit is the cheapest place to read.
4. **Read only that change.** The diff of the one commit is the suspect. Reading the rest of history is a second search with no end.
5. **Keep the test.** The pass-or-fail check becomes a test in the project, so the bug cannot return without turning the suite red.

---

## Epistemic Rules

- **Confirmed means this session's output.** A test that passed last week is evidence about last week's code. Paste the output from this session, with its exit code.
- **A passing check proves only its one thing.** A passing unit test shows that one path works. It does not show that the export runs end to end, so the outcome block names what was checked.
- **Hedge words are a stop sign.** "Should work," "probably" and "seems to" mean nobody has run the check yet. When one of them appears in a draft outcome, the check runs before the sentence is kept, or the sentence is rewritten as an open item.
- **Write dates in full.** A date in the outcome block or the handoff is written as YYYY-MM-DD, because "last Tuesday" means nothing to a reader who opens the file a month later.
- **Count every run.** Write "3 of 10 runs (illustrative)", never "sometimes". The count is the only way the next reader can judge how intermittent the bug is.
- **Eliminated needs a result.** A hypothesis is eliminated when the test that would prove it returned the other answer. A hypothesis that was never tested stays open.
- **The owner's words define the symptom.** The symptom is written the way the owner describes it, before it is translated into technical terms. A symptom restated to be easier to fix is a different symptom, and the fix may cure the wrong one.
- **A quiet log clears only its own question.** A log line that shows nothing unusual clears the hypothesis it was written to test. It does not clear the whole area around it.
- **A fix is not a cause.** A change that makes the symptom disappear shows that the change touched the bug. It does not show that the change touched the root cause, until the root cause is named at a file and a line and the test shows why.
- **Say what was not checked.** If the test suite could not run, or the owner's steps could not be repeated, the outcome block says so in the same message. An unchecked part is written as unchecked, never folded into a pass.

---

## Hard Rules

1. **No fix without a written hypothesis.** An untracked change that happens to work teaches nothing, and the next bug in the same place starts from zero. The hypothesis card is the proof that a fix was aimed.
2. **One change per test.** When two things change, the result cannot say which one mattered, so a fix built on it is a guess.
3. **The failing test first for code.** A fix written before a red test cannot be shown to have changed anything. The red output is the proof that the bug exists in the form the test checks.
4. **Three, then stop.** Three failed guesses show that the belief behind them is wrong. A fourth guess tests the same belief with new inputs, which is what made the first three fail.
5. **The handoff is appended, never trimmed.** A trimmed handoff loses its dead ends, and a dead end walked twice costs the same time both times.
6. **Never a destructive reset of the working tree.** Discarding uncommitted work to reach a clean state deletes the evidence of the attempts and the owner's in-progress changes in the same step. Save the state first, then return to a known version, as the regression list describes.
7. **One fix at one file and line.** A fix spread across several files makes the root cause hard to name, and the outcome block exists to name it in one place.
8. **The owner can stop the session at any point.** The owner's instruction to stop outranks the skill's next stage, because the owner holds the context the skill does not. The stop is written as a handoff with the state as it stands, so it is not lost.

---

## Common Excuses

| Excuse | Why It Is Wrong |
|--------|-----------------|
| "I'll just try this." | A try with no hypothesis is a change with no test. If it works, nobody knows why, and the bug can return. Writing the guess takes one minute. |
| "I'm confident." | Confidence is not evidence. Write the hypothesis, name the output that would prove it, and then produce that output. |
| "It's probably the same as last time." | The last cause may not match this symptom. Compare the error with the old outcome block line by line before deciding it matches. |
| "It works on my machine." | The bug lives where the owner sees it. Reproduce it there, and list every environment difference, as Stage 2 requires. |
| "One more restart." | A restart changes timing and state, so a pass after it proves nothing about the cause. The third restart is the fourth attempt under a different name. |
| "I'll patch the symptom now and find the root cause later." | The patch hides the cause, and the cause then breaks something else. The outcome block needs a root cause at file and line before any fix. |
| "I'll stack a second fix on the first." | Two unproven changes can cancel out on one run and fail on the next. Undo the unproven change, then test the second one alone. |

**Red flags in your own thinking.** If you catch yourself thinking "let's see what happens," "this should do it," "quick one more," or "I'll tidy this while I'm here," stop and return to Stage 3. Each of those is a fix arriving before its hypothesis.

Two more feel reasonable and are not exceptions. "It's a one-line fix, so it needs no test" is the excuse that most often ships a wrong line, because a one-line change is the easiest to make without a red run, and the test costs less than a second round of the same bug. "The owner is in a hurry, so I'll skip the failing test" trades a few minutes now for a second round later, and the owner pays for that round. In both cases the failing test stays, and the hurry is a reason to write it faster, not to leave it out.

**Owner phrases that send you back to Stage 1.** When the owner says "stop guessing," or asks "is that not happening?", the session has drifted from the error. Return to Stage 1, read the whole error again, and write a hypothesis card before any further action.

---

## Quality Bar

A Debug session is done when every item below is true. Record the evidence beside each one in the reply.

- [ ] Each stage ran in order, and the bug class is named on the first line. *Evidence: the stage outputs, each with its Produces line.*
- [ ] For code, the failing test was written first and seen to fail. *Evidence: the red output, pasted.*
- [ ] One root-cause change was made, at one file and line. *Evidence: the changed line, quoted.*
- [ ] The full check passes: the failing test, the other tests, and the owner's original steps. *Evidence: the output and exit code from this session.*
- [ ] The fix was verified where the bug occurred, on the owner's steps and not only in a test. *Evidence: the steps run and what the screen or output showed.*
- [ ] Nothing else broke. *Evidence: the test count before and after, with every failure listed by name.*
- [ ] For non-code work, the Gate field says so and names the log line or diff used. *Evidence: the Gate line in the outcome block.*
- [ ] Any regression additions are present, and any handoff was appended, not trimmed. *Evidence: the Commit, Test path, Why it recurred and Why the fix holds fields, or the handoff file's new entry.*

---

## Examples

The first example is a public case from an open-source library. The second is the PlotIQ chain, the story the other verification skills share, with two threads from one session. The figures in the second example are illustrative.

### Example 1. A Dependency Update That Changed a Default (Public Example)

This is a public example, not an invented one. The library is date-fns, and the behavior described is the library's own. A test failed after a dependency update. The test expected the string "2023-10-21" and got "Invalid Date". The change history showed that the date-fns library had moved from version 2 to version 3 in that same update.

**Stage 1.** The whole error read: an expected string and an unexpected string, with the update as the only recent change. Prerequisites present.

**Stage 2.** The test fails on every run after the dependency update.

**Stage 3.** One hypothesis card, written before any change:

```text
Hypothesis: the major version change altered the default date format, so the existing call no longer produces a date.
Proof: the library's changelog confirms the change, and the one call site fails when no format is given.
Test: pass the explicit format string at the call site, then run the test.
Result: pending.
```

**Stage 4.** The library's changelog confirmed the hypothesis: version 3 requires an explicit format string. The test was already red, so the fix was written against a failure that was already on record.

**Stage 5.** The fix is one change at the one call site, which now passes the explicit format string. The previously failing test passes, and the rest of the suite passes.

```text
The root cause was that the library's major version changed the default date format, so the call that had worked on version 2 no longer produced a date. The fix was an explicit format string at the one call site. The failing test then passed, and the rest of the suite passed with it.

The full outcome block, field by field, is shown in Example 2.
```

The case shows a bug whose cause came from a version change, which the change history found before any guess. The hypothesis was written before the fix, and the fix sat at one place.

### Example 2. The PlotIQ Export, Two Threads From One Session (Illustrative)

PlotIQ's team builds the state-format trust report export that the Brackhaven Memorial Gardens board chair asked for. Eli Marsh, the Implementation Lead, owns the build. Two bugs came up in one session, and each one ends differently.

**Thread 1: fixed.** Mode: new bug. The export stops at row 311 of 1,046 on Brackhaven's second site, with the message "empty field in trust balance" (illustrative). The whole error names `trust_report_export.py`, line 88. It reproduces on the fixture every time.

- Hypothesis one: site 2 writes dates in a different format. Proof: a log line showing the date string at row 311. The log shows the same date format on both sites. **Eliminated.**
- Hypothesis two: row 311 has no plot number. One change: skip rows with no plot number. The export still fails at row 311. **Eliminated.**
- Hypothesis three: the trust fund field is present but empty at row 311, and the mapper divides by it. Test first: `test_export_handles_empty_trust_balance` is written and run, and it fails. One change at line 88: an empty balance is treated as zero and the row is flagged. The new test passes, the other 14 export tests pass, and the export runs end to end with exit code 0. **Confirmed.**

```text
Root cause: trust_report_export.py:88, an empty trust balance was divided.
Fix: trust_report_export.py:88, an empty balance is treated as zero and the row is flagged.
Test name: test_export_handles_empty_trust_balance
Red run: FAILED test_export_handles_empty_trust_balance (output pasted, taken before the fix)
Green run: 1 passed (the new test). 15 passed (the full export suite, after the fix).
Reproduction: plotiq export trust-report --site brackhaven-2
Reproduction output: export complete: 1,046 rows, 1 flagged, 0 errors, exit 0
Confirmed by: the green run and the reproduction output, both from this session.
Gate: test first.
```

The review that followed added a second fix at line 61 and a sixteenth test, which is why Verify's example shows 16.

**Thread 2: stopped at the circuit breaker.** Mode: timing. On a five-site test fixture the export sometimes times out, 3 of 10 runs (illustrative). Timing bugs gather data before any hypothesis, so the run count came first. Three hypotheses were then tested, each with one change, and each was eliminated. The third failed hypothesis is the breaker, so the session stopped and wrote the handoff file:

```text
Problem: the five-site export times out on about 3 of 10 runs (illustrative).
Hypotheses:
  1. Network. Eliminated: same rate on a local file.
  2. Batch size. Eliminated: same rate at half the batch.
  3. A file lock. Eliminated: no lock in the code path.
Now believed: the timeout appears only when two exports overlap in time.
Next action: add a log line at the start of export_site() in trust_report_export.py line 42,
  then run two exports at once and read the two timestamps.
```

The handoff is appended on the next run and never trimmed. Wrap-Up carries it under Open Threads, so the next session starts with the three dead ends already eliminated. The owner confirms the next action before the session closes.

Thread 1 was not reopened once it was confirmed. Its outcome block stays with the fix, and a later change in the same area gets its own card, so the proof of the first fix is never edited to cover the second.

The two threads are the point of the example. One was fixed, and its proof is in the same message as the claim. The other was stopped, and its dead ends are written down where the next session will find them.

What a reader checks in each thread:

- Thread 1: the Confirmed by line contains output from this session, not from an earlier run, and the Gate line says test first.
- Thread 1: the root cause and the fix name the same file and line, so the fix can be found in one step.
- Thread 2: every eliminated hypothesis has its evidence beside it, and the next action is one step with a named place to log.
- Thread 2: the handoff is the only record of the stop, so it is appended and never trimmed on the next run.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| Works locally and fails in production | An environment difference: a version, a setting, a data shape or a path | List every difference between the two places before any change. Run the test with production-like settings. Do not change the local copy to match by guessing |
| Too many changes at once | Several fixes were stacked before any test ran | Save the current state to a commit or stash, return to the last clean version, and reapply one change at a time, with the test after each |
| The same symptom after a fix | The hypothesis was unfinished, or the fix hit the wrong place | Return to Stage 3 and log at the boundary the fix was meant to change |
| The bug cannot be reproduced | The inputs, timing or steps differ from the report | Run the Stage 2 change list, and ask the owner for the exact steps and the shape of the data |
| The new test passes on its first run | The test checks behavior that already exists | Rewrite the test until it fails for the reason in the hypothesis, then run it again |
| The owner says "stop guessing" | A change was made, or proposed, without a hypothesis | Stop, return to Stage 1, and write the hypothesis card before any other action |
| The handoff file is long | Each stopped session appends to it | Keep it whole. The dead ends are the value. Summarize only in the reply, never in the file |
| The log line is hard to place | The value is not in scope at the spot the hypothesis names | Move the log to the first line where the value is known, and say in the card where it went. A log in the wrong place proves nothing, and it is not a test |
| Every candidate is eliminated but the symptom remains | The real cause is outside the candidate list | Stop at the breaker and write the handoff. A new candidate is a new hypothesis, and it is taken to the owner before it is tested, because the search space has changed |
| The first hypothesis looks confirmed by reading the code | Reading is tier 3 at most, and it cannot confirm a cause | Write the card, run the test or the log line, and paste the output. The code reading becomes the reason for the test, not its replacement |
| The full test suite is too slow to run | The suite covers far more than the change | Run the part of the suite that covers the changed file first, report that it was partial, and run the rest before the outcome is written as complete |
| The owner's steps cannot be repeated | Part of the setup lives with the owner, not in the session | Ask for the exact steps and data shape. Mark the reproduction as partial in the outcome block, and do not claim a fix on steps nobody ran |

**Degradation table.** When a piece is missing, Debug still runs and says what it could not check.

| Missing Piece | What Debug Does | What the Reply Says |
|---------------|-----------------|---------------------|
| Test command in the profile | Runs the check by hand and pastes the output | "Test command: not set. Check run by hand, output pasted" |
| Diagnostic access | Limits hypotheses to what the error and the output show | "No diagnostic line. Hypotheses limited to the error" |
| Change history | Reads the named file and asks for the last known good point | "Change history not visible. Recent changes unknown" |
| Handoff location | Keeps the handoff in the reply only | "No saved handoff. Next session starts cold" |
| Owner for the breaker | Writes the handoff and skips the notice | "Owner not told: no one named in the profile" |
| No test harness, non-code work | Uses a log line or diff as the gate | "Gate: log line, no test harness" |

---

## Best Practices

- **Write the hypothesis card before you open the file.** Writing it exposes the belief behind the guess, and that belief is usually where the bug is.
- **Keep the diagnostic line small, and remove it after.** A log left in the code shows up as evidence in the next bug and sends that search the wrong way.
- **Start from the last known good point when one exists.** A search across history with a pass-or-fail command beats a guess about where the change happened.
- **Record each failed attempt in your project notes as it happens.** A failure written during the session is evidence. A failure remembered tomorrow is only a story.
- **Add a defense-in-depth check after the fix.** The fix stops this bug. A check at the boundary where the bad value entered stops the whole class, so the next variant fails loudly instead of silently. Name that check as a follow-up in the outcome block.
- **Name the test after the claim it proves.** A name such as `test_export_handles_empty_trust_balance` says what the fix promises, so a reader can tell from the test list alone which behavior is guarded.
- **Paste output, do not paraphrase it.** "The test passed" is a summary. The line that says `1 passed, exit 0` is evidence. A paraphrase drops the number that would have shown a partial run.
- **Ask for the whole error the first time.** A second request for the error costs a round trip, and the missing line is often the one that names the file. Asking once, completely, is cheaper than working from a partial message.
- **Read the earlier handoff before the code, on any return to a stopped thread.** The handoff says which places are already cleared. Opening the code first invites a fresh guess that the handoff already ruled out.
- **Write the next action as one line before the session ends.** A next action that cannot fit on one line usually holds two steps. Split it, and keep the first step as the one the owner confirms.
- **Keep one thread per symptom.** A second symptom gets its own card and its own outcome block. Two symptoms in one thread make the proof for each one harder to read.
- **Name the bug class aloud before the first test.** One line at the top of the session, such as "New bug, hypothesis first", keeps the first action honest. A session that drifts into a different class without saying so has usually skipped its first action.

### Further Reading

- *Debugging: The 9 Indispensable Rules* by David Agans
- *The Pragmatic Programmer* by David Thomas and Andrew Hunt, read for its debugging chapter

---

## Integration With Other Skills

- **Receives from the owner.** The symptom, the whole error, the owner's steps and the earlier handoff for the same symptom, if one exists. Those are the inputs in the Input Contract, and the skill reads them before any other source.
- **Hands to Verify (`gtm-verify`).** Verify grades the outcome block. It checks the Confirmed by field, which must be this session's output and must reach tier 4, Functional. A root cause with no failing test is a tier 1 claim dressed as tier 4, and Verify sends it back. The fields it reads by name are Root cause, Fix, Confirmed by and Gate.
- **Hands to Wrap-Up (`gtm-wrap-up`).** When a session stops at the circuit breaker, Wrap-Up carries the handoff file under Open Threads by its path. The owner confirms the close's next action from the handoff's Next action line. The next action must be one imperative step with a named object, because the next session has to start from it cold.
- **Before a rebuild.** If the bug sits in code you were about to rebuild, run the context gap check first. A rebuild can make the bug disappear without explaining it, and a bug that vanishes unexplained comes back.
- **Hands to the owner.** The outcome block is written the same way whether or not it will be read by Verify, so the owner can check the proof without the skill's help. The reply carries the outcome block or the handoff's Next action line, in that order, followed by the single next step. The owner confirms the next step, and the skill does not run it on its own.
- **Next step.** Run gtm-verify on the outcome block before the fix is called done.

---

## Changelog

### 2.0.0 (2026-10-18)

Rewritten from the verification shared contract. Adds five bug classes with a first action each, a failing test first for code with a log-line gate kept only for work with no test harness, a circuit breaker at three with an appended handoff file, a regression five-step list, an outcome block with a where-it-lives column, and hand-offs to Verify and Wrap-Up by field name.
