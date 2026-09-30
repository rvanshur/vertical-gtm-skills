# Identity File Template

> **What this is:** a project-level `CLAUDE.md` for when you want to run the skills from a
> project folder other than the cloned repo. It tells Claude Code who you are, what you sell, and
> where the skills and your profile live. If you work straight from the cloned repo, you don't
> need this, because the repo's own `CLAUDE.md` already does the job.

Copy the block below into your project as `CLAUDE.md`, replace `/path/to/vertical-gtm-skills`
with the real path to your clone, and fill in the blanks.

---

```markdown
# [Your Company] GTM Intelligence

## Who We Are
- **Company:** [Your Company]
- **Product:** [What you sell, one line]
- **Vertical:** [Your industry vertical]
- **Stage:** [Seed / Series A / Growth / Enterprise]

## Where the System Lives
- Skills: /path/to/vertical-gtm-skills/skills/ and /path/to/vertical-gtm-skills/operating/
- Client profile (read it before running any skill): /path/to/vertical-gtm-skills/profiles/client-profile.md

## Available Skills
When I ask for a GTM task, read the matching skill in full and follow it exactly.

| Task | Skill File |
|------|-----------|
| Qualify an account | `skills/01-account-qualification/SKILL.md` |
| Build outbound package | `skills/02-account-snapshot/SKILL.md` |
| Deep research outbound | `skills/03-research-outbound/SKILL.md` |
| Trigger event sequences | `skills/04-trigger-event-outbound/SKILL.md` |
| Re-engage lost deals | `skills/05-closed-loss-reactivation/SKILL.md` |
| Prep for a meeting | `skills/06-meeting-prep/SKILL.md` |
| Morning dial sheet | `skills/07-daily-prospecting/SKILL.md` |
| Score a deal | `skills/08-deal-pulse/SKILL.md` |
| Deep qualification | `skills/09-meddpicc-analysis/SKILL.md` |
| Map stakeholders | `skills/10-stakeholder-mapping/SKILL.md` |
| Competitive battlecard | `skills/11-competitive-strategy/SKILL.md` |
| Competitive displacement | `skills/12-competitive-displacement/SKILL.md` |
| Coach a call | `skills/13-call-coaching/SKILL.md` |
| Handoff to CS | `skills/14-sales-handoff/SKILL.md` |
| Check work is done before claiming it | `operating/O1-verify/SKILL.md` |
| Check what exists before building | `operating/O4-context-gap/SKILL.md` |
| Get a review from a different AI vendor | `operating/O5-second-opinion/SKILL.md` |
| Close a working session | `operating/O10-wrap-up/SKILL.md` |
| [Add the other operating skills you use: see the repo's CLAUDE.md for the full table] | |

## Methodology
- **Discovery:** [SPIN / Sandler / Gap Selling / Other]
- **Qualification:** MEDDPICC
- **Demo:** [Challenger / Other]

## Quality Rules
- Always ground scoring in evidence, not assumptions
- Flag gaps explicitly, and don't hide bad news
- Output should be immediately usable by the rep (not a summary to think about)
- Use the prospect's language, not our marketing language
```
