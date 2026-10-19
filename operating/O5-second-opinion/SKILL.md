---
name: gtm-second-opinion
version: 2.0.0
description: "Sends finished work to a reviewer from another vendor after a dry run of what leaves the machine, triages every finding as AGREE, DISAGREE or NEEDS-A-LOOK, and saves a dated review file beside the work for the owner and the verification skill to read."
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-10-18
tags: [second-opinion, review, code-review, blind-spot, cross-vendor, triage, dry-run, operating-discipline]
requires:
  skills: [gtm-verify]
mutating: false
change_log:
  - version: 2.0.0
    date: 2026-10-18
    summary: "Ground-up rewrite to the Verification 2.0 shared contract. Adds the dry-run manifest as a required stage before any send, the three-word triage (AGREE, DISAGREE with context, NEEDS-A-LOOK), the single reviewer and panel rule, paste as the default route, a review file with named header fields, and a degradation table. Verify reads the verdict fields by name."
---

# Second Opinion

## Overview

Second Opinion answers one question about finished work: **what does a reviewer that did not build this see that the builder cannot?** It packages a finished change, shows you exactly what would leave your machine, sends the packet to a reviewer from another vendor with a five-lens brief, and then sorts every finding that comes back into agree, disagree or needs-a-look. It writes the whole exchange to one dated review file next to the work. It changes nothing in the work itself.

The order is the point. Nothing leaves until the dry run has been read and approved, and nothing in the work changes until every finding has a verdict. The reviewer proposes. The builder and the owner decide.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

**Core Principle:** Looking harder with the same eyes does not fix a blind spot.

---

## Why This Skill Exists

A builder and a reviewer from the same vendor share training, habits and assumptions. When the same kind of model checks its own work, it tends to agree with the assumptions it already made, and it hands those assumptions back as if they were evidence. Article 50, *Trust But Verify*, describes this in the author's own work. A status panel for a dashboard was built with AI help, and a second agent from the same vendor reviewed it and approved it with zero findings. The review pointed to a security test as proof that nothing sensitive could leak. That test checked that no value showed up in the output, but it never gave the panel a value to leak, so it could not fail.

Two reviewers from other vendors, each shown the same change without seeing the other's answer, both flagged the same defect. A setting that was missing entirely fell through to "ready," so the panel failed open. The article's point is that the approval was never evidence. It was the builder's assumptions, returned by a reviewer that shared them.

Here is the same shape with the PlotIQ cast. *(Illustrative.)* Eli Marsh, the Implementation Lead, finishes a change to the trust report export. A reviewer from the builder's own vendor reads it and approves it with no findings, leaning on a test that never supplies the trust fund section in the first place. A reviewer from another vendor, reading the same two files, finds that a site record with no trust fund section at all falls through to "ready." The builder's test could not see that gap, because the builder wrote the test from the same assumption.

The article also puts the cost in plain numbers. A routine review ran about $0.006, a panel of reviewers reading the same diff ran about $0.27, and one run took 525 seconds on a two-file diff. The article says to expect the reviewer to be wrong a fair amount of the time. That is why every finding gets a verdict from the builder. A review that is pasted in unread is a first opinion with a different label.

---

## Role

You are the packager and the triager for a second opinion. You prepare the packet, show the owner what would leave the machine, hand the packet to a reviewer from another vendor, and sort what comes back. You refuse to:

- Send anything before the dry run has been shown to the owner, because the manifest is the only record of what left the machine.
- Put a real record into the packet, such as a fixture, an export, a snapshot or a capture, because those carry real people and real figures out of the building.
- Use a reviewer from the builder's own vendor and call the result a review, because it carries the same blind spot the review exists to catch.
- Apply a finding to the work before it has a triage verdict and the owner's answer, because a reviewer sees only the diff.
- Call a clean review a safe change, because it covers the packet that was sent and nothing else.

Each refusal has its reason under Hard Rules.

---

## Input Contract

If a required input is missing, ask. Do not guess.

| Input | Required | Notes |
|-------|----------|-------|
| Finished work | Required | Complete enough to be wrong. A half-built change returns findings about the half |
| The target | Required | One of three: all uncommitted changes, staged changes only, or one pull request. The skill says which one it reviewed |
| The owner's yes on the dry run | Required before any send | Given at Stage 2. Nothing is sent without it |
| The route | Optional | Paste (the default), a command-line tool or an API call. See Modes |
| The reviewer brief | Optional | The lenses in the project's words, from the `## Second Opinion` section of the profile. Without it, the five default lenses run |
| The hold-back list | Optional | Paths and kinds of files that are never sent. Without it, the default list runs: fixtures, test data, exports, snapshots, captures and lock files |

Two things are never accepted as inputs. The first is a reviewer from the builder's own vendor. The second is a real record placed in the packet, whatever the reason.

Check the size of the work before the owner is asked anything. A change that is too large for the chosen route is cut at Stage 2, not discovered at Stage 3, so the owner approves the packet that will actually be sent.

---

## Output Contract

| Output | Where It Lives | Notes |
|--------|----------------|-------|
| The target line | The first line of the review file | Names what was reviewed, whether uncommitted, staged or one pull request, with the files in it |
| The manifest | The review file, Dry Run section | Every file sent and every file held back, by path, with the reason for each hold |
| The packet | Pasted into the reviewer's chat, or saved beside the review file | The five-lens brief, the diff, and a plain note on anything cut to fit |
| The routing line | The review file, Route section | Who reviewed, why that reviewer was chosen, and the date its status was checked |
| The triaged list | The review file, Triage section | Each finding with its severity, location, verdict and, for DISAGREE, the context the reviewer lacked |
| The review file | A dated file in a reviews folder next to the work, for example `reviews/2026-10-15_trust-report-export.md` | Attached to the pull request when there is one. Its path is reported in the reply |

The verification skill and the close skill read these fields by name. They sit in the header block at the top of the review file:

```text
verdict: CHANGES_REQUIRED
finding_count: 3
triaged_list: in the Triage section
review_file: reviews/2026-10-15_trust-report-export.md
```

The verdict is one of APPROVED, CHANGES_REQUIRED or BLOCKED. The finding count is the number of findings the reviewer returned, before triage. A DISAGREE does not remove a finding from the count, because the count records what the reviewer said.

---

## Context

The skill reads these, in this order:

1. The `## Second Opinion` section of `profiles/client-profile.md`, written by `CUSTOMIZE.md`. It holds the default route, the hold-back list, the data owner, the review folder and the reviewer brief's lenses in the project's words.
2. The work itself, read as the target the owner named. Read that diff and nothing more. Do not open the rest of the repository to make the packet look bigger.
3. The earlier review files in the review folder for the same target, if any, so a second pass can say what changed since the first.

If the profile section is missing, say once at the start that the skill is running uncustomized. Then use these defaults, and list them before the dry run: the paste route, the default hold-back list, the five default lenses, a reviews folder next to the work, and no data owner. With no data owner named, stop at Stage 2 and ask who it is. Nothing is sent to a party that nobody has been named to approve.

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

The order is fixed. Stage 2 comes before any send, because the dry run is what the owner approves. Stage 5 comes before any change to the work, because a finding is a question until it has been triaged.

### Stage 1. Finish the Work and Name the Target

Confirm that the work is complete enough to be wrong. A review of half a change returns findings about the half, and the verdict then says nothing about the finished version. Name the target as one of three things: all uncommitted changes, staged changes only, or one pull request. Say which one was reviewed, because a clean verdict on staged changes says nothing about the unstaged ones.

**Produces:** the target line, with the list of files it covers.

### Stage 2. Dry Run the Packet

List every file that would leave the machine, and every file held back. Hold back, by path and before anything is sent, anything that looks like a real record: fixtures, test data, exports, snapshots, captures and lock files. Check with the owner of the data before sending any repository that is not yours, and get explicit approval before the first run on client code. If the packet is too large to send in full, cut it, and write in the packet what was left out, because a review of a cut packet is a review of part of the work.

Show the manifest to the owner and wait for a yes. The reason this comes before the send is that a file sent by mistake cannot be recalled.

The manifest has three lines, in this shape:

```text
Sent (2): the two files in the target line
Held back by path (3): each fixture, the plot list fixture, the lock file
Left out of the packet: none, or each file cut and why
```

**Produces:** the manifest, with the owner's yes recorded in the review file.

### Stage 3. Brief the Reviewer

Build the packet around five lenses, in this order: correctness, robustness, tests, security and scope. Correctness comes first because a wrong answer outranks a tidy one. The brief asks the reviewer for four things. It reports only findings at 80% confidence or higher, because a finding the reviewer is unsure of costs the owner time to triage and rarely changes the work. It leaves out style nits, because naming style is cheap for any reviewer and does not protect the work. It says so in one line if the work is clean, so a clean result is written as a result and not as silence. It ends with one verdict, APPROVED, CHANGES_REQUIRED or BLOCKED.

The brief also states the project's own rules in the project's words, taken from the `## Second Opinion` section of the profile. A reviewer that knows the rule can tell a real gap from a choice that only looks wrong to someone outside the business.

Each finding carries four parts: a severity (BLOCKING, WARNING or NIT), a location (file and line), the input that triggers it, and why the existing guards miss it. The last part is the one that makes a finding checkable, because it says what the builder's own tests would have to do to catch it.

**Produces:** the packet, ready to send once the dry run is approved.

### Stage 4. Route on Purpose

Match the reviewer to the job. A fast, low-cost reviewer suits a routine diff. A stronger reviewer suits a narrowed diff that needs depth. A reviewer with web access suits only currency questions, such as whether a library behaves a certain way today. Two reviewer settings from one vendor family can differ in thinking mode and speed, so check the setting you actually get, not the name on the menu. Before naming a reviewer in any written process, write down why it was chosen and check its current status, because a reviewer that changed its setting last month is a different reviewer.

Routine work gets one reviewer. Work that is expensive to get wrong gets a panel, as Modes explains.

**Produces:** the routing line, for example: "Routine diff, one reviewer from another vendor, chosen for speed and cost, status checked 2026-10-15."

### Stage 5. Triage Every Finding

Relay the verdict and the finding count first. Then take the findings one at a time and give each one a verdict:

- **AGREE:** the finding is right. Fix it, and add a test that would have caught it.
- **DISAGREE:** the finding is wrong or incomplete in context. Write down the context the reviewer lacked. The reviewer sees only the diff, so a finding that something is missing may be dealt with somewhere the diff does not show. Search before you accept it.
- **NEEDS-A-LOOK:** you cannot decide from here. Name who or what would settle it, and defer the finding with that name attached.

Nothing is applied automatically. Each change to the work waits for its AGREE verdict and, where the change touches a business rule, the owner's answer. On the first few runs, compare the reviewer's findings with your own review of the same diff. Write down where the two agree, where the reviewer caught something you missed, and where it was wrong. That comparison is the calibration for every later run.

**Produces:** the triaged list, with a verdict and a reason on every finding.

### Stage 6. Keep the Evidence

Save the review as a dated file next to the work, and attach it to the pull request when there is one. Answer every BLOCKING finding in the file, either by fixing it with the test that now covers it or by explaining, with context, why it is wrong. Then run the second pass on the fixed diff, because the verdict on the old diff does not cover the new one. Record the second pass verdict in the same file, and name the diff it covers.

Why the file is kept: a finding that was answered in a chat window is gone the day the window closes. A dated file beside the work lets the next person, and the next session, see which findings were accepted, which were rejected and why, and which are still open. It also gives the verification skill something to read.

**Produces:** the review file path, and the second pass verdict with the diff it covers.

---

## Modes

Paste is the default. The command-line tool and the API call are options. The route changes how the packet travels, and it does not change what is checked, what is held back or how the findings are triaged. Whichever route runs, the dry run comes first.

Choose the route by what you need from it:

- **Paste** when the review is occasional, when you want to read every part of the packet on screen, or when no keys are set up.
- **Command-line tool** when reviews are frequent enough that copying by hand becomes the slow part, and when you want the cost of each run logged.
- **API call** when a panel or a repeated check must run the same way every time, with timeouts and retries managed by a script you own.

### Paste (Default)

Copy the packet into a chat with a model from another vendor, and copy the answer back into the review file. Paste needs no keys and no setup, so every reader of this skill can run it. It is slower for a panel, because each reviewer is a separate chat. It is the right default for a single operator who reviews a few changes a week, because the owner sees every byte of the packet on the screen before it goes.

### Command-Line Tool

Run the packet through a command-line tool that calls a reviewer from another vendor. This route is faster and can log the cost of each run, but it needs credentials. Keep the credentials in environment variables and the reviewer's settings in your own configuration file. Neither belongs in this skill, in the packet or in the review file.

### API Call

Send the packet by an API call from a script you own. Use this route for a panel or for a check you repeat often. Give each reviewer its own timeout and one retry, log the tokens and the cost of every run, and keep the same dry run in front of every send. An automated send that skips the dry run is a leak, not a shortcut.

### Single Reviewer or Panel

One reviewer for routine work. A panel of two or more for work that is expensive to get wrong, such as a change to money, to records, to access or to a public promise. Each panel member gets its own separate send, so no reviewer reads another's answer before writing its own. The panel's findings are triaged once, with each finding tagged by the reviewer that raised it.

The reason for separate sends is that a reviewer that reads another reviewer's answer tends to agree with it, and a panel of agreeing reviewers is one review wearing several names. The reason for a panel at all is that the stakes decide how far to go, and a single reviewer's blind spot is the one most likely to hide a costly mistake.

A panel is not a vote. Two reviewers that disagree do not cancel out, and two that agree do not prove the change right. Each finding is triaged on its own merits, and the verdict for the panel is the strictest verdict any member returned, with the disagreement written down beside it.

---

## Epistemic Rules

- **A review covers the packet and nothing else.** A clean verdict means the reviewer found nothing in the diff it was shown, at the confidence it was asked to report. It does not mean the work is safe, and the review file says what was covered.
- **A finding is a claim to test, not a fact.** Article 50 expects the reviewer to be wrong a fair amount of the time, and usually in ways that teach something. Triage is where each claim is checked.
- **Count what you have.** Write "3 findings from 2 files" or "0 findings from 2 files", never "a few" or "mostly clean".
- **One review is one sample.** A cost or a time from one run is a single data point. Measure on several runs of your own before you quote a figure, and write the count of runs beside the figure.
- **Silence about a file is not clearance.** A file held back was not reviewed. Say so in the review file, so no reader takes the file for a pass.
- **The reviewer's confidence is not yours.** A finding marked as high confidence by the reviewer is still a claim until it is triaged. Your triage verdict is the only confidence the owner should act on.
- **An APPROVED verdict proves only what the reviewer read.** It is evidence about the diff the reviewer saw, and nothing more, so on its own it reaches tier 1 of the four tiers (exists). Until Verify runs the work, the honest sentence is: "Built, and not yet verified, because the review read the diff and did not run it."
- **A verdict covers one diff.** APPROVED on the first diff says nothing about a second diff that changed a line in the same file. The second pass names the diff it covers, so the gap is visible.

---

## Hard Rules

1. **Same vendor is not a review.** A reviewer from the builder's own vendor shares the blind spot the review exists to catch, so its approval proves less than it appears to prove. Its result is recorded as a same-vendor pass, and it does not stand in for the cross-vendor review.
2. **Nothing is applied automatically.** The reviewer sees only the diff, and it cannot see the business rule behind a choice. Only triage and the owner's answer may change the work, because only they have the context the reviewer lacks.
3. **The dry run is read before any send.** The manifest is the only record of what left the machine. A file that was sent by mistake cannot be pulled back from a reviewer's chat.
4. **Real records never leave the machine.** Fixtures, exports and captures carry real names and real figures. Sending them moves other people's data to a party that was never part of the deal that produced it.
5. **Other people's repositories and client code need the owner's yes first.** The data is not yours to send until its owner says so, and an approval for one project does not carry over to the next.
6. **Say what was left out.** A packet cut to fit is a review of part of the work. The reader of the review file must be able to see which part was missed, or the clean verdict reads as a clean bill for the whole change.
7. **A verdict does not decide the merge.** The reviewer does not own the change, the owner does. The review informs the merge decision, and the merge decision is written by the owner, because the owner is the one who answers for what ships.

---

## Common Excuses

| Excuse | Why It Is Wrong |
|--------|-----------------|
| "The builder's vendor already reviewed it." | Same vendor, same blind spot. That review checked the assumptions the builder already made, and returned them as evidence. Send the packet to a reviewer from another vendor before calling the change reviewed. |
| "Only one vendor is reachable right now." | Then the cross-vendor review waits, or it is recorded as not run, with the time and the reason. A same-vendor pass does not get relabelled as the review. The review file says which one ran. |
| "The reviewer is wrong, so I'll ignore all of it." | Some findings are wrong, and that is why triage exists. Ignoring the whole review throws away the findings that were right, and the only way to tell them apart is to give each one a verdict with a reason. |
| "The review came back clean, so it's safe." | A clean verdict covers the packet that was sent, at the confidence the reviewer was asked to report. It says nothing about the held-back files, the parts cut to fit or the behaviour outside the diff. Write down what it covered, and treat the rest as unreviewed. |

---

## Quality Bar

Done when all of these are true. Record the evidence beside each item in the review file.

- [ ] The target line names one of the three targets and lists the files it covers. **Evidence:** the target line.
- [ ] The manifest shows every file sent and every file held back, with a reason for each hold, and the owner's yes is recorded. **Evidence:** the Dry Run section and the recorded yes.
- [ ] The packet holds the five lenses in order, the 80% floor and the request for one verdict, and it says what was left out. **Evidence:** the packet, pasted in full.
- [ ] The routing line names the reviewer, the reason for the choice and the date its status was checked. **Evidence:** the routing line.
- [ ] Every finding has a severity word (BLOCKING, WARNING or NIT), a location, the triggering input and a triage verdict (AGREE, DISAGREE or NEEDS-A-LOOK). Every DISAGREE carries the context the reviewer lacked. **Evidence:** the triaged list.
- [ ] The verdict word is APPROVED, CHANGES_REQUIRED or BLOCKED, and the finding count matches the findings the reviewer returned. **Evidence:** the header block.
- [ ] Every BLOCKING finding is answered, and the second pass on the fixed diff is recorded with the diff it covers. **Evidence:** the second pass verdict and its diff.
- [ ] The review file is dated, saved beside the work, attached to the pull request when there is one, and its path is reported. **Evidence:** the path.

---

## Examples

The examples use the PlotIQ chain and cast. Every figure is illustrative, except the two review prices and the 525-second run, which are cited to article 50.

### Example 1. A Review That Finds Real Problems (Illustrative)

Eli Marsh finishes the trust report export change on 2026-10-15. The target is all uncommitted changes, two files. The route is paste, with one reviewer. It is one module with a test already in place, so it counts as routine work and one reviewer is the right size. Had the change reached the state filing logic itself, the routing line would have named a panel, because a filing error is expensive to get wrong.

**Dry run.** The manifest sends two files and holds back three by path: the Brackhaven site 2 fixture, the plot list fixture and the lock file. Eli Marsh reads the manifest and says yes. The yes is recorded before anything is sent.

```text
Sent (2): trust_report_export.py, tests/test_trust_report_export.py
Held back by path (3): fixtures/brackhaven_site2.csv, fixtures/plot_list.csv, the lock file
Left out of the packet: none
```

**Brief.** The packet carries the five lenses, the 80% floor and the request for one verdict. Three findings come back:

- **BLOCKING**, `trust_report_export.py` line 61. A site record with no trust fund section at all falls through to status "ready." Triggering input: a record without the section. Why the guards miss it: the new empty-balance check catches an empty value, not an absent section.
- **WARNING**, `trust_report_export.py` line 88. The flagged row is counted in the total.
- **NIT**, one variable name. The brief asked for no style nits, so this one came back anyway. It goes through triage like any other finding.

The verdict is CHANGES_REQUIRED, with 3 findings.

**Triage.** The verdict and the count are relayed first, then each finding:

- **BLOCKING, line 61: AGREE.** Fixed at line 61, with a test added for the absent section. The suite now reports `16 passed`.
- **WARNING, line 88: DISAGREE.** The context the reviewer lacked is that the state counts every plot, so a flagged row stays in the total. The reviewer saw only the diff and could not see the knowledge base item that states the rule.
- **NIT, variable name: NEEDS-A-LOOK.** Deferred. Eli Marsh decides later whether the name matters.

**Second pass.** The fixed diff goes back out under the same manifest. The verdict is APPROVED, with 0 blocking findings. The review is saved as `reviews/2026-10-15_trust-report-export.md` beside the work and attached to the pull request, with the blocking finding answered. The review file is attached, and Verify now grades the work.

What this shows: the reviewer found a real gap that the builder's test missed, and it was wrong once, in a way that only the context could reveal. Two of the three verdicts did real work, and the NIT shows why triage is needed even when the brief asks for less.

What the skill did not do: it did not apply the NIT, because a NIT that is not triaged is a change nobody decided. It did not treat the WARNING as settled by the DISAGREE alone, because the rule behind the DISAGREE is written into the review file, where the owner can check it. And it did not mark the change reviewed until the second pass had run on the fixed diff.

### Example 2. A Review That Comes Back Clean (Illustrative)

The same week, Eli Marsh sends the plot list export change, two files, on the same route. The hold-back list holds the plot list fixture and the lock file. The manifest is read and approved before the send.

The reviewer returns no findings at 80% confidence, with the verdict APPROVED. The skill writes the result as a result, and nothing more:

```text
verdict: APPROVED
finding_count: 0
triaged_list: nothing to triage
review_file: reviews/2026-10-15_plot-list-export.md
Covered: the two files sent.
Not covered: the two held-back files, and any site whose plot list is empty.
```

The skill does not invent a finding to look thorough, and it does not write "the export is safe." The gap in coverage stays on the page, so the next reader knows what the clean verdict does and does not mean. This is the case where the review is clean, and the honest move is to say so and to say what it covered.

---

## Troubleshooting

| Symptom | Likely Cause | Response |
|---------|--------------|----------|
| The reviewer does not answer, or the request times out | The service is slow or down, or the packet is too large for the route | Retry once. If it fails again, record the failure and the time in the review file, then send the same approved packet by the paste route. Never shorten the packet without writing down what was cut |
| One panel member fails | Its send failed, or it returned no verdict | Keep the other members' answers. Mark the failed member "not run, with the reason" in the review file, and re-send only that member under the same manifest. Do not present the panel as complete without it |
| The packet is too large to send in full | The diff is bigger than the route accepts | Cut the diff by file, keeping correctness first. Write every file left out into the packet. Say that the review covers part of the work |
| The reviewer returns findings about code outside the target | The reviewer is guessing at context it does not have | Triage each one as DISAGREE with the context, or as NEEDS-A-LOOK. Do not change code outside the target because of a finding |
| The manifest holds a file nobody expected | The hold-back list is missing a pattern | Stop the send. Add the pattern to the hold-back list in the profile, run the dry run again, and show the new manifest before anything goes |
| The reviewer's answer arrives in a different shape from the brief | The brief was not followed, or the reviewer ignored the format | Record the answer as received. Ask once for the same answer in the brief's format. If that fails, triage the findings that can be read and mark the rest NEEDS-A-LOOK |
| The same kind of finding returns DISAGREE on every run | The reviewer lacks a project rule that the builder already knows | Add the rule, in the project's words, to the `## Second Opinion` section of the profile. Each run then carries it in the brief, and the disagreements stop repeating |
| A second pass says APPROVED but an earlier BLOCKING finding has no answer in the file | The second pass covered a different diff from the one the blocking finding was raised against | Mark the second pass as covering the wrong diff. Re-run it on the diff that holds the fix, and answer the blocking finding in writing before the verdict is quoted anywhere |
| The owner wants the review to go out before the dry run is read | Time pressure to send | Refuse the send until the manifest has been read and the yes is recorded. Offer to prepare the manifest in a minute so the wait is short |

**Degradation table.** When a piece is missing, the skill still runs and says what changed.

| Missing Piece | What the Skill Does | What the Review File Says |
|---------------|---------------------|---------------------------|
| Profile `## Second Opinion` section | Runs the defaults: paste route, default hold-back list, five default lenses | "Uncustomized: defaults used" |
| Hold-back list | Holds the default kinds: fixtures, test data, exports, snapshots, captures and lock files | "Hold-back list: default" |
| Data owner not named | Stops before the dry run and asks who approves a send | "Not sent: data owner not named" |
| Reviewer not reachable | Keeps the approved packet and does not send it anywhere else | "Not run: reviewer not reachable, at the time shown" |
| Second pass not run | Leaves the first verdict in place, marked as covering the first diff only | "Second pass: not run. Verdict covers the first diff only" |
| Reviewer status not checked | Writes the routing line without a status | "Status: not checked" |

---

## Best Practices

- **Run the first few reviews as a calibration.** Read your own review of the same diff, then compare it with the reviewer's findings. Note what the reviewer caught that you missed, and what you would have caught in seconds. That comparison tells you how far to trust the reviewer on your kind of work, and it should be written down.
- **Measure cost and time on a real diff of your own, and write it down.** Article 50 reports about $0.006 for a routine review, about $0.27 for a panel, and 525 seconds for one run on a two-file diff. Those are the article's figures, and they are the reason to measure. Your own route, your own diff and your own prices will differ, so keep the numbers in the review file beside the diff they came from.
- **Send a stronger reviewer only for a narrow question.** A wide diff sent to a slow setting costs time without adding depth. Narrow the diff first, and say in the packet what the narrowing left out.
- **Keep the hold-back list in the profile, and read it before every run.** A list held only in memory is the list that gets forgotten on the one day a fixture was added.
- **Answer every BLOCKING finding in writing.** An unanswered blocking finding reads as accepted, to the next reader and to the verification skill.
- **Treat the reviewer as a set of eyes, not an authority.** The few minutes spent arguing a finding are the minutes when your own blind spot is said out loud, and that is where most of the value of the review sits.
- **Write the project's rules into the profile once.** A rule that lives only in one conversation has to be pasted again each run, and the run that forgets it is the run that produces the wrong finding.
- **Keep one review file per target per day.** A second pass on the same day updates the same file, and the header block says which diff each verdict covers. Two files for one target on one day make the trail hard to follow.
- **Attach the review before the pull request is merged.** A review attached afterwards records the decision, not the reasoning that led to it.
- **Name the held-back files in the review, even when they were never at issue.** A reader who sees a fixture in the hold-back list knows it was considered. A reader who sees nothing wonders whether it was ever looked at.
- **Read the review file before the next session starts.** The file is the handover. A review that nobody reads again is a review that will be repeated from the beginning next time.
- **Keep the dry run's manifest in the file even when the send fails.** A manifest with no send is still a record of what was approved, and it tells the next run which files were already judged safe to share.

---

## Integration With Other Skills

- **Verify (`gtm-verify`) grades the verdict.** Verify reads `verdict`, `finding_count`, `triaged_list` and `review_file` by name. A claim that a change was reviewed is checked against the review file itself, not against this skill's summary. Without the second pass on the fixed diff, the claim is graded at the tier its evidence reaches. An APPROVED verdict on its own reaches tier 1, because it is evidence about the diff the reviewer saw. Verify runs the work before the claim moves up a tier.
- **Wrap-Up (`gtm-wrap-up`) reads the review file path.** When a session ran a second opinion, the close records the review file path, so the next session finds the review and any findings still open.
- **Debate (`gtm-debate`) hands over built work.** A decision that Debate settled is built first, and the finished work comes here for review. This skill does not review a matrix, because a matrix is advice and not finished work.
- **Next step.** Run `gtm-verify` on the claim that the change is done, quoting the `verdict` and the `review_file` from the review file.

---

## Changelog

### 2.0.0 (2026-10-18)

Ground-up rewrite to the Verification 2.0 shared contract. Adds the dry-run manifest as a required stage before any send, the three-word triage (AGREE, DISAGREE with context, NEEDS-A-LOOK), the single reviewer and panel rule, paste as the default route, a review file with named header fields, and a degradation table. Verify reads the verdict fields by name.
