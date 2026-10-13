# The Skill Standard

Every skill in this repository meets this standard before it ships. GTM Discovery 2.0
(`operating/O15-gtm-discovery/SKILL.md`) is the reference skill. When this page and Discovery
disagree, fix whichever one is wrong. Do not leave them disagreeing.

Version 1.0, 2026-10-13.

## 1. Frontmatter

```yaml
---
name: <slug>
version: <major.minor.patch>
description: "<one sentence: what it does, what it produces, who reads the output>"
category: <Operating-Discipline | Sales-Methodology | ...>
author: Ryan Vanshur
license: MIT
updated: <YYYY-MM-DD>
tags: [...]
requires:
  skills: [<skills whose output this one reads>]
mutating: <true | false | read-write>
change_log:
  - version: <x.y.z>
    date: <YYYY-MM-DD>
    summary: "<what changed>"
---
```

`mutating` tells the reader whether the skill only reports (`false`), writes or changes things
(`true`), or reports by default and writes only when asked (`read-write`). A `true` or
`read-write` skill names its approval step in the workflow.

## 2. Sections, in This Order

1. **Overview.** What the skill answers, in two short paragraphs, and the **Core Principle** in
   one bold line.
2. **Why This Skill Exists.** The failure it prevents, told plainly. If a real incident or
   measurement shaped a rule, give the number. Published numbers only.
3. **Role.** What the agent is, and what it refuses to do.
4. **Input Contract.** A table: input, required or optional, notes. The rule above it is always
   "If a required input is missing, ask. Do not guess."
5. **Output Contract.** A table of every output and where it lives. If another skill reads an
   output, use the exact field names that skill asks for.
6. **Context.** Which files it reads, in order, and what happens when one is missing. The
   skill reads its own section of `profiles/client-profile.md` (written by its `CUSTOMIZE.md`)
   and says once at the start when it is running uncustomized.
7. **Core Workflow.** Numbered stages or phases. Each one ends with what it **Produces**. Say
   *why* a stage comes where it does when the order matters.
8. **Modes** (when the skill has more than one way to run, for example report-only and apply).
   Say which is the default and which ones write.
9. **Epistemic Rules.** The rules that keep the output honest: n beside every rate, five cases
   before a pattern, silence is not a no, "no difference" is a finding. Include only the ones
   that apply.
10. **Hard Rules.** The few rules that are never broken, each with its reason.
11. **Common Excuses** (for discipline skills: verify, debug, debate, context gap, second opinion,
    wrap-up, dream). A table of the excuse an agent gives for skipping the step, and why the
    excuse is wrong. It sits inside the skill so the agent reads it at the moment it is tempted.
12. **Quality Bar.** "Done when all are true", as a checklist the agent runs before handing back.
13. **Examples.** At least one worked example. Mixed outcomes, not only successes. See section 4.
14. **Troubleshooting.** Symptom, likely cause, response.
15. **Best Practices.**
16. **Integration With Other Skills.** What it reads from the skill before it, what it hands to
    the skill after it, and the field names it hands over.
17. **Changelog.** Newest first.

Sections 8 and 11 are skipped when they do not apply. Every other section is required.

## 3. Writing

- Plain words a newcomer can follow. Explain any term the first time it appears.
- No em dashes. No semicolons. Numbers take "%", never the word "percent".
- Title Case for headings.
- Lists for steps and for three or more items. Never bury a list in a sentence.
- Rules carry their reason. "Never auto-merge duplicates, because two items can describe
  different stages" teaches. "Never auto-merge duplicates" only commands.

## 4. Examples

- One invented company carried through the whole example, labelled as illustrative. The
  shared example company is Lexora (`profiles/client-profile.md`).
- Every number in an example is either labelled illustrative or comes from a published source
  that is named.
- Show a failure or a contradiction, not only a clean run. A skill that only shows success
  teaches the agent to report success.

## 5. Files That Ship With Every Skill

| File | Purpose |
|------|---------|
| `SKILL.md` | The skill |
| `CUSTOMIZE.md` | A short interview that writes the skill's section of `profiles/client-profile.md` |

Every skill also states, in its README entry and on its web page, that it works in Claude Code,
in Codex, and in ChatGPT as a custom GPT (`docs/chatgpt-gpt-setup.md`).

## 6. What Never Ships

A free skill can teach any method, rule, threshold, template or report format. It never carries:

1. A real person's file paths, folder names, project names or machine setup.
2. Any employer's data, systems, numbers, people or customers.
3. Names of colleagues, clients or prospects.
4. The internals of a private automation setup: hooks, schedulers, memory indexes, recall
   counters, task tools, publishing pipelines.
5. Client deliverables or anything built under a consulting engagement.
6. Keys, endpoints or internal repository names.

When a private skill has a feature that depends on private automation, the free skill ships the
*method* and leaves the wiring to the reader. Example: a skill can teach "an item that keeps
getting used is protected from being pruned for age". It does not ship the hook that counts the
uses.

## 7. Tests Before Release

1. **Safety scan.** The packaging script runs it on every zip and refuses to build when it finds
   a key, an endpoint or a private name. Zero findings.
2. **Proprietary check.** Read every changed line against section 6.
3. **Style check.** No em dashes, no semicolons, "%" for numbers.
4. **Hand-off test.** A fresh agent runs the next skill in the chain on this skill's example
   output, with no other context. The hand-off passes when the next skill finds every field it
   asks for by name.
5. **Clean-room and overlap test**, only for skills that began as adaptations of an outside
   MIT-licensed set. Rebuilt from a written spec without the original open. Target: 0% shared
   runs of eight words with the original.
6. **Version and changelog.** The version moves (major for a rewrite, minor for new features,
   patch for fixes) and the changelog says what changed.

## 8. Shipping

After the tests pass: commit, rebuild the download zip, upload it to the skill's web page, check
the live page as a visitor, and update any page text the new version changes. Pushing the public
repository is a separate, approved step.
