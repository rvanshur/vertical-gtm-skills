# Identity File Template

> **What this is:** Your project-level `CLAUDE.md` file. This tells Claude Code who you are, what you sell, and how to use the skills. Place this in the root of your project directory.

Copy this file to your project as `CLAUDE.md` and fill in the blanks.

---

```markdown
# [Your Company] GTM Intelligence

## Who We Are
- **Company:** [Your Company]
- **Product:** [What you sell, one line]
- **Vertical:** [Your industry vertical]
- **Stage:** [Seed / Series A / Growth / Enterprise]

## How to Use This System

### Available Skills
When I ask for sales-related tasks, read the relevant skill from the `skills/` directory:

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

### Methodology
- **Discovery:** [SPIN / Sandler / Gap Selling / Other]
- **Qualification:** MEDDPICC
- **Demo:** [Challenger / Other]

### Quality Rules
- Always ground scoring in evidence, not assumptions
- Flag gaps explicitly — don't hide bad news
- Output should be immediately usable by the rep (not a summary to think about)
- Use prospect's language, not our marketing language
```
