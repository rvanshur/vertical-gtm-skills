---
name: gtm-weekly-review
description: "Runs a standing operational review every week, measures system health across knowledge and content, and writes a dated record so health becomes a trend line instead of isolated snapshots"
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [weekly-review, health-check, operations, measurement, trend-line, accountability, operating-discipline]
requires:
  skills: []
---

# Weekly Review

## Overview

Prevents silent drift by running the same operational questions every week, comparing the answers to the previous week, and writing a dated record so you can see the trajectory.

Most teams review only when something breaks. That is a post-mortem, and by then the decision that caused it is weeks old. This skill runs a standing slot whether or not anything broke. It measures what changed since last week across your knowledge base, content pipeline, and system health. Then it writes its own file, so next week's review has something to compare.

**Core Principle:** Drift is invisible when measured once. Drift becomes unmissable when measured every week, written down, and compared to the previous week. That comparison is the point.

---

## Why This Skill Exists

A team that reviews health on failure only ever learns about failure. A team that reviews health on a schedule learns about drift while it is still cheap to fix.

The skill exists because of a specific pattern. Metrics are run sporadically. When they are run, they are reported to a conversation and forgotten. The next metric is taken in isolation. A count that doubled between July and September has nowhere to hide, a line of dates exposes it, but if no one compared July to August, and August to September, the doubling is invisible until September looks impossible.

The measurement rules earned their place the hard way. First, last week's priorities are graded from evidence, not from memory. A commit in the log, a file that was touched, an artifact that is now in place. Not "roughly done", either it happened or it did not. Second, every priority for the coming week is stated with something concrete attached. A file path, a PR number, a command that will be run. Not "make progress on the thing," because "progress" rolls forward forever. "Publish three articles" is checkable. "improve the system" is not. Third, write `null` for metrics you did not actually check, never `0`. A zero written for something you did not look at travels into next week's plan as a fact.

---

## Role

You are an **operational auditor and trend analyst**, not a cheerleader. Your job is to measure change with cold precision, compare it to the previous week, and surface what is accelerating, stalling, or drifting. You do not judge whether the numbers are good or bad. You flag where the direction is unexpected.

---

## Input Contract

**If required input is missing, ask, do not guess.**

| Input | Required | Notes |
|-------|----------|-------|
| Last week's dated record | Required | The file from the previous week's review, to compare against |
| Evidence of what ran this week | Required | Git logs, file mtimes, artifacts that exist. Assumption and memory are not evidence |
| This week's completed priorities | Required | What was supposed to happen last week. Did it? (done / not done / overtaken) |
| System access | Required | Ability to check repos, knowledge base directories, pipeline status |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| Carried-over status | Yes | Last week's priorities, each marked done, not done, or overtaken |
| Metrics table | Yes | With baseline from last week and delta |
| Operational findings | Yes | What is healthy, what needs attention |
| Next week's priorities | Yes | Each one must be measurable by evidence |
| Dated record file | Yes | Written to disk for trend tracking |

---

## Context

If `profiles/client-profile.md` has a `## Operational Health Metrics` section (this skill's `CUSTOMIZE.md`
writes it), read it before starting and let it replace the generic defaults in this file.
If the section is missing, run with the defaults and say once, at the start, that the skill
is running uncustomized.

---

## Core Workflow

### Step 1. Read Last Week's Record

Before you measure anything new, read the previous week's file (or state plainly if this is the first run). Extract:
- The baseline metrics from last week's frontmatter
- The priorities that were set for this week
- Any blockers or open threads

This is not for nostalgia. It frames every comparison you make.

### Step 2. Grade Last Week's Priorities

For each priority that was set last week, check evidence:
- Did it happen? (commit log, files touched, artifacts that exist)
- Is it done, not done, or overtaken?
- Overtaken means the priority became irrelevant and was replaced. That is not a failure. It is information.

Record the baseline count of **not done** items. This is your `carried_over` metric.

### Step 3. Measure System Health

Measure three areas, comparing to last week where possible:

**Knowledge base / content**
- Total nodes / articles
- Files modified this week
- Any emergent items aging past their decision point (30 or 60 days)
- Orphan items (few or no connections)
- Tag health (single-use tags = sprawl)

**Content pipeline**
- What is in progress
- Blockers on any piece
- Ideas that came up naturally this week

**Operations**
- Uncommitted work in key repos
- Any system checks that need running (linting, documentation freshness, data refreshes)
- Stale data or dashboards (unchanged >30 days)

Compare each metric to last week's frontmatter. Record `delta` (the change) and `null` for anything you did not actually check.

### Step 4. Identify Healthy and Concerning Items

List what is working (keep monitoring). List what needs attention (specific action required).

### Step 5. Set Next Week's Priorities

Three to five priorities. Each must be:
- **Evidence-based.** Grounded in what you found, not wishes.
- **Measurable.** A PR number, a file path, a command, a person. Not abstract ("improve the system").
- **Singular.** One thing, not a bucket.

When you cannot construct a measurable priority from what actually happened, ask rather than invent one.

### Step 6. Write the Record

Write the file to one dated folder per project, for example `{project}/weekly-review/{YYYY-MM-DD}.md`. Keep it in the same place every week so next week can find it.

**Frontmatter contract (emit in this order, every week):**

```yaml
---
date: 2026-09-28
window: 2026-09-21..2026-09-28
kb_nodes: 150
kb_new: 3
kb_orphans: 2
tag_sprawl_pct: 28
repos_dirty: 1
carried_over: 1
---
```

Write `null` for metrics you did not check, never `0`. Zero is a measurement. Null is an absence.

**Body sections (markdown):**

```markdown
# Weekly Review, {date}

## Carried Over from {prior date}
- [done]      ..., evidence
- [not done]  ..., what blocked it
- [overtaken] ..., why it stopped being relevant

## System Health
| Metric | This Week | Δ | Status |
|--------|-----------|---|--------|

## What Needs Attention
- Item 1 (specific action)
- Item 2

## Next Week
1. Priority 1 (measurable)
2. Priority 2 (measurable)
3. Priority 3 (measurable)
```

### Step 7. Closing

State clearly: the file was written at {path}. This record exists, and next week you will have it to compare against.

---

## Quick Reference

| What to Measure | Healthy | Concerning | Action |
|---|---|---|---|
| **Carried-over items** | 0-1 from prior week | 3+ | Priorities were either vague or blocked. Revisit scope |
| **Knowledge nodes** | Growing or stable | Shrinking without reason | Ask what is being archived and why |
| **Aging emergent items** | <30 days | >60 days | Force a decision: promote or archive |
| **Repo uncommitted work** | 0-1 repos | 3+ repos | Stale branches. Suggest commits or cleanups |
| **Tag sprawl** | <20% | >40% | Too many one-off tags. Consolidate |

---

## Epistemic Rules

- **Evidence beats memory.** Not "I think this was done." A commit hash, a touched file, an artifact that exists.
- **Null is not zero.** If you did not check a metric, write `null`. A zero you did not measure becomes a false data point.
- **Overtaken is real.** Plans become irrelevant. That is not failure. That is information.
- **Measurable is not optional.** A priority that cannot be checked by evidence next week will roll forward forever.
- **Trend beats snapshot.** One week's metrics are noise. Three weeks of metrics show the trajectory.

---

## Troubleshooting

| Symptom | Likely cause | Response |
|---|---|---|
| "Nothing changed since last week" | Last week's record is missing or unreadable | State the file you looked for and what failed. Write `carried_over: null` |
| Every priority passes | Priorities were too vague or broad | Review them against the measurability rule |
| Metrics are all null | You did not have access to measure | Name the blockers. Next week, address them |
| Priorities keep rolling forward | They were stated without evidence attached | Revisit the measurability rule. Restate them |

---

## Best Practices

- Run this at the same time every week (Friday or Monday morning).
- **Before writing anything**, read last week's file. The delta is the point.
- Grade last week's priorities from logs and files, never by asking.
- Keep the measurement quick (15 minutes). This is not a deep dive.
- Show the written file path in your summary. You cannot verify it was written otherwise.

---

## Integration with Other Skills

- **`O8-dream`** runs deeper consolidation. This is a weekly pulse that flags what needs that deeper pass.
- **`O7-graph-health`** measures knowledge base structure in detail. This uses a lightweight version of it.
- **`O10-wrap-up`** closes each session. This closes each week.
- Together, these three skills form the cadence: session close → weekly review → monthly consolidation.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section added, so the skill reads the profile section its CUSTOMIZE.md writes.
- **1.0.0 (2026-09-28):** Initial release. Weekly operational review with trend tracking, measurable priorities, evidence-based grading, and dated records.
