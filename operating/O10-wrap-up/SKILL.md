---
name: gtm-wrap-up
description: "Closes a working session so nothing learned is lost, guarantees a continuation record is written, and produces a parseable artifact so downstream systems can track where each project was left off"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [session-close, continuation, handoff, operating-discipline, workflow]
requires:
  skills: []
---

# Wrap-up

## Overview

Closes a working session with a three-part record: what got done, what state it is in, and the one next action, stated with enough specificity that someone can resume the work cold.

Most people end a working session by stopping. The work is done, the context is in their head, tomorrow they rebuild it. This habit enforces a written handoff that prevents that rebuild.

**Core Principle:** The last thing you do in a session is write where the next session should start. Not a summary for yourself (you remember), but a handoff for someone who was not there, including your future self.

---

## Why This Skill Exists

Counting revealed the problem. A system was built to show where each project was left off, inferring that from the last action in each session. Of 151 sessions, 16 had ended on a scheduled command that a machine typed, and many others ended on boilerplate a tool had injected. The last thing typed proved something ran. It did not prove a person chose to stop there, so the record of activity and the record of intent had drifted apart silently, and the dashboard was confidently showing the wrong place.

The fix is that the continuation record is a contract, not prose. A parser reads it. Sloppy fields mean the system shows nothing, which turns out to be the right pressure.

The next-action field has four tests so it never rolls forward forever. It must be imperative (starts with a verb, not a gerund or state). It must have a named object (the verb has a real thing attached, not an abstraction). It must be singular (one action, not a sprinted multi-step arc). And it must be resumable cold, meaning someone who was not in the session could read it and do it without asking.

---

## Role

You are a **handoff engineer**, not a note-taker. Your job is to capture state in a form the next session (or the next person) can use to resume without re-deriving context.

---

## Input Contract

**If required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Session details | Required | Working directory, which project(s) were touched, what actually happened |
| Current state of files | Required | What is staged, what is uncommitted, what is verified vs. assumed |
| Completion status | Required | What is done, what is half-done, what is blocked |
| Next action | Required | The one thing the next session should do first |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Continuation artifact | Yes | Dated file, machine-readable frontmatter |
| Project routing | Yes | Which project(s) this session affected |
| What happened section | Yes | 3-6 bullets of past-tense, specific accomplishments |
| State section | Yes | File-level precision: what is verified, what is assumed |
| Next action | Yes | Must pass four tests (see below) |
| Blockers | If any | Array of explicit blockers, not vague |

---

## Context

If `profiles/client-profile.md` has a `## Session Handoff` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Step 1. Determine Scope

Which project(s) did this session touch? Collect:
- The working directory when you started
- Every file created or modified this session
- Any uncommitted work

Ask the user to confirm scope if ambiguous. Never guess.

### Step 2. Write What Happened

Three to six bullets. Past tense. Specific.

**Bad:** "Worked on the import."
**Good:** "Rewrote the import handler and got row counts matching the Friday export. Tested against Q3 file set."

### Step 3. Write Where We Stopped

File-level precision. What state is the code in?
- Which file, which function, what is the current behavior?
- What is verified (tests passing, live check done)?
- What is still assumed (calculation not measured, behavior not tested)?

**Bad:** "Nearly done."
**Good:** "Handler is live on staging, three checks passing, timing still unmeasured against production volume."

### Step 4. Determine Next Action

The next action must pass four tests:

| Test | Fails if... |
|---|---|
| **Imperative** | Starts with a gerund or a state ("Working on…", "Continue…") |
| **Named object** | You cannot point at the file, person, PR, or decision it refers to |
| **Single step** | Contains "and then", or describes a multi-day arc |
| **Resumable cold** | A reader with zero session context could not start it |

Examples:

| Rejected | Accepted |
|---|---|
| "Continue working on the import" | "Measure import latency against Q3 production file set" |
| "Finish the handler" | "Re-run the import test and compare row counts to Friday's export" |
| "Follow up with the team" | "Reply to the 4 open review threads on PR #212" |
| "Keep improving" | "Merge the branch and update the documentation" |

### Step 5. List Blockers

Array of strings, one blocker per line. Empty if none.

**Bad:** "Needs review."
**Good:** "Awaiting code review from @alice. Design decision needed on error handling."

### Step 6. Write the Artifact

Location: one continuation folder per project, for example `{project}/continuations/{YYYY-MM-DD}_continuation_{slug}.md`. Where it lives matters less than it being the same place every time.

**Frontmatter (emit in this exact order):**

```yaml
---
skill: /wrap-up
type: continuation
date: 2026-09-28
project: my-project-name
context: Human-friendly label
status: approved
next_action: "[One imperative sentence with a named object]"
blockers: []
supersedes: null
---
```

**Body (markdown):**

```markdown
## What Happened
- Bullet 1 (specific, past tense)
- Bullet 2
- ...

## Where We Stopped
Paragraph describing file-level state. Which is verified, which is assumed.

## Open Threads
Unresolved questions, deferred work, things deliberately out of scope.
```

### Step 7. Confirm Next Action

Show the `next_action` line. Let the user correct it. They are the authority on what comes next.

### Step 8. Closing

State the file path where the artifact was written. Reference it. Verification-before-completion applies to written files too.

---

## Quick Reference

| Check | Pass if... | Fail if... |
|---|---|---|
| **Imperative** | "Ship the branch" | "Working on shipping" |
| **Named object** | You can point to the file / PR / person | You can only point to an abstract ("the thing") |
| **Single step** | One action that fits in one sentence | "Then also run the tests and update the docs" |
| **Resumable cold** | Someone fresh could start it without asking questions | "Continue where we left off" |

---

## Epistemic Rules

- **State beats summary.** Not "it's mostly done," but precise: "three of five tests pass."
- **Next action is not a goal.** "Ship the feature" is a goal. "merge the branch after CI passes" is an action.
- **Blockers are not excuses.** A blocker is something external stopping you. Not "nobody reviewed it" (that is waiting for action), but "review approval required from X" (external dependency).
- **Assumed is not verified.** Name what you have not tested. The next session needs to know.
- **The artifact is parseable.** Sloppy fields mean the system shows nothing. Be precise with frontmatter.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "Next action keeps failing the tests" | You are writing a goal, not an action | Restate as one concrete step, not an achievement |
| "I can't think of a next action" | The session is genuinely complete | Write an explicit closure: "Nothing pending, shipped and sent to [person]." |
| "This is for multiple projects" | Scope is unclear | Write one artifact per project. Merged notes orphan all but one. |
| "I don't know what state it's in" | The session was exploratory and reached no checkpoint | Say so plainly. Mark as `status: draft` and note "exploratory session, no committed changes." |

---

## Best Practices

- Do this at the end of every working session, before you close the laptop.
- Show the `next_action` to the user and let them correct it. It is the highest-value line.
- Be specific about file and branch states. Vague state descriptions mean the next session guesses.
- If the session produced code or artifacts, verify they exist before writing the note.
- Keep the note short (5 min to write). Long handoffs are notes you will not write twice.

---

## Integration with Other Skills

- **`O6-weekly-review`** closes each week, reading last week's continuation notes.
- **`O8-dream`** may reference continuation notes to understand session artifacts.
- **`O9-ingest`** captures content. Wrap-up closes the session that ingested it.
- Together, wrap-up (session) → weekly-review (week) → dream (month) is the cadence.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section added, so the skill reads the profile section its CUSTOMIZE.md writes.
- **1.0.0 (2026-09-28):** Initial release. Three-part session close with four-test next-action gate, machine-readable frontmatter, and state-level precision.
