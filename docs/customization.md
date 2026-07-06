# Customization Guide

How to adapt the skills to your methodology, scoring preferences, and workflow.

---

## What You Can (and Should) Customize

### Always Customize: Client Profile
Your company's data lives in one shared file — **`profiles/client-profile.md`** — that every skill reads via its Context section. This is the primary customization point, and you touch exactly one file. See the [Client Profile Template](../profiles/client-profile-template.md) for the full walkthrough.

### Sometimes Customize: Methodology Frameworks
The skills ship with SPIN (discovery), Challenger (demos), and MEDDPICC (qualification). If your team uses different frameworks, swap them.

### Rarely Customize: Scoring Logic and Workflow
The scoring systems (Deal Pulse's 16 signals, MEDDPICC's 8 elements, Call Coaching rubrics) are battle-tested. Modify these only if you have a strong reason and understand the downstream effects.

---

## Swapping Sales Methodologies

### Replacing SPIN with Another Discovery Framework

The Meeting Prep (06) and Call Coaching (13) skills use SPIN for discovery calls. To swap:

1. Open the skill's SKILL.md
2. Find the SPIN question framework section
3. Replace with your framework's structure

**Example: SPIN → Sandler Pain Funnel**

Replace the SPIN question bank:
```markdown
### Discovery Framework: Sandler Pain Funnel

1. **Surface Pain:** "Tell me more about that..."
2. **Business Impact:** "How does that affect the business?"
3. **Personal Impact:** "What does that mean for you personally?"
4. **Budget Commitment:** "What would you invest to solve this?"
5. **Decision Process:** "If you found the right solution, what happens next?"
```

**Example: SPIN → Gap Selling**

```markdown
### Discovery Framework: Gap Selling

1. **Current State:** Process, tools, team, metrics today
2. **Future State:** What does good look like? What changes?
3. **The Gap:** What's preventing the move from current to future?
4. **Impact of the Gap:** What is the gap costing in dollars, time, risk?
5. **Root Cause:** Why does the gap exist? What's been tried?
```

### Replacing Challenger with Another Demo Framework

Meeting Prep (06, demo mode) and Call Coaching (13) use Challenger principles. To swap:

```markdown
### Demo Framework: [Your Framework]

1. **[Step 1]:** [What the rep should do and why]
2. **[Step 2]:** [What the rep should do and why]
3. **[Step 3]:** [What the rep should do and why]
```

Update the Call Coaching rubric categories to match your new framework's evaluation criteria.

---

## Modifying Scoring Criteria

### Deal Pulse: Adding or Removing Signals

The 16-signal system covers most B2B deals. To modify:

1. Open `skills/08-deal-pulse/SKILL.md`
2. Find the `## Scoring Framework` section
3. Add, remove, or re-weight signals

**Example: Adding a "Security Review" signal for enterprise sales**

Add under the Execution pillar:
```markdown
| 17 | Security Review | Security questionnaire status, InfoSec approval | GREEN: Approved / YELLOW: In progress / RED: Not started |
```

Update the health score calculation to include the new signal.

### MEDDPICC: Adjusting Element Weights

By default, all 8 elements are equally weighted. If your deal cycle makes some elements more critical:

1. Open `skills/09-meddpicc-analysis/SKILL.md`
2. Find the scoring section
3. Add weight multipliers

```markdown
### Weighted Scoring
| Element | Weight | Max Score |
|---------|--------|-----------|
| Metrics | 1.0x | 5 |
| Economic Buyer | 1.5x | 7.5 |
| Champion | 1.5x | 7.5 |
| Paper Process | 0.5x | 2.5 |
```

### Call Coaching: Adding Custom Criteria

To add criteria specific to your methodology:

1. Open `skills/13-call-coaching/SKILL.md`
2. Find the rubric section for discovery or demo
3. Add new categories with clear behavioral indicators

```markdown
| 7 | Multi-threading | Asked about other stakeholders, offered to include them | /5 |
```

---

## Adding Industry-Specific Qualification Criteria

### Account Pre-Qualification: Vertical-Specific Dimensions

The default 8 criteria are industry-agnostic. Add criteria specific to your vertical:

**Example: Healthcare SaaS**
```markdown
| 9 | HIPAA Readiness | Has compliance officer, existing BAA process | Must be ready or deal stalls |
| 10 | EHR Integration | Uses a supported EHR (Epic, Cerner, etc.) | Technical prerequisite |
```

**Example: Construction Tech**
```markdown
| 9 | Multi-State Operations | Operating across state compliance boundaries | Higher complexity = higher need |
| 10 | Current Compliance Method | Manual, BPO, or incumbent software | Helps position against status quo |
```

---

## Creating Custom Skill Combinations

### Building a "Weekly Pipeline Review" Macro

Instead of running Deal Pulse on each deal individually, create a wrapper:

Add to your `CLAUDE.md`:
```markdown
## Weekly Pipeline Review
When I ask for a pipeline review:
1. Read skills/08-deal-pulse/SKILL.md
2. Score each deal I provide
3. Stack-rank by health score
4. Flag any deal below 60
5. For flagged deals, note the top 2 risks and recommended next actions
6. Present as a table: Deal | Score | Top Risk | Next Action
```

### Building a "New Account Package" Macro

```markdown
## New Account Package
When I ask to package a new account:
1. Run Account Pre-Qualification (skills/01-account-qualification/SKILL.md)
2. If GREENLIGHT: Run Account Snapshot (skills/02-account-snapshot/SKILL.md)
3. Present: Qualification verdict + Company brief + 3 email sequences + Cold call sheet
```

---

## Integrating with External Data

### CRM Data (Salesforce, HubSpot, etc.)

Skills work best with context. When running a skill, paste relevant CRM data:

```
Score this deal with Deal Pulse. Here's the CRM data:

Stage: Demo Completed
Close Date: March 30
Amount: $85K ARR
Last Activity: Meeting with VP Ops (3 days ago)
Next Step: Technical review with IT team
Notes from last call: [paste notes]
Contacts: VP Ops (Champion), Director IT (Technical Eval), CFO (not yet engaged)
```

### Call Transcripts

For Call Coaching, paste the full transcript or detailed notes. More context = better coaching.

### LinkedIn / Web Research

For Research-Driven Outbound, paste 10-K excerpts, earnings call transcripts, or LinkedIn posts from target executives.

---

## Version Control Tips

When customizing skills for a team:

1. **Fork this repo** for your organization
2. **Keep one profile per engagement** in `profiles/` (e.g., `client-profile.md` active, `acme-profile.md` archived) — swap the active file when you change clients
3. **Use branches** for experiments (e.g., `try-sandler-framework`)
4. **Document changes** in each skill's Changelog section
5. **Review quarterly** to remove outdated competitors, refresh proof points, update personas
