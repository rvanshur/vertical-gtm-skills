# Customization Guide

How to adapt the skills to your company, your methodology, your scoring preferences and your workflow. Work top to bottom. Most teams only ever need the first two sections.

Every example on this page uses Lexora, the fictional legal-ops company in [`profiles/examples/legal-ops-example.md`](../profiles/examples/legal-ops-example.md), so you can see each change against a complete profile.

---

## What You Can (and Should) Customize

| How often | What | Where | Effort |
|---|---|---|---|
| **Always** | Your company data | One file, `profiles/client-profile.md` | 30 minutes, once, then refresh quarterly |
| **Per skill, after a baseline** | How a skill fits your motion | That skill's `CUSTOMIZE.md` interview | 10-20 minutes per skill |
| **Sometimes** | Your sales methodology (SPIN, Challenger, MEDDPICC) | The profile's Sales Methodology section, then the skill files | An hour |
| **Rarely** | Scoring logic and workflow | The skill files themselves | Only with a strong reason, since a change ripples into every score |

---

## Step 1: Fill the Profile, in the Right Order

Your company's data lives in one file, **`profiles/client-profile.md`**, and every skill reads it through its Context section. This is the main customization point, and you touch exactly one file. The [Client Profile Template](../profiles/client-profile-template.md) walks through each section.

### Which Profile Sections Feed Which Skills

Counted from the Context sections of the 14 sales skills. Fill the top rows first, because they feed nearly everything.

| Profile section | Sales skills that read it | What happens if it is thin |
|---|---|---|
| ICP Definitions | 13 of 14 | Qualification verdicts and account scores become guesses |
| Competitive Landscape | 12 of 14 | Battlecards, displacement sequences and objection handling go generic |
| Core Pain Points | 8 of 14 | Discovery questions and email hooks lose their edge |
| Buyer Personas | 5 of 14 | Sequences and call sheets stop matching the person in the room |
| Qualification Criteria | 4 of 14 | Trigger timing and disqualifiers stop working |
| Proof Points | 4 of 14 | Emails and demos cite nothing, or cite the wrong customer |
| Value Propositions | 3 of 14 | Positioning and demo stories flatten |
| Sales Methodology | 3 of 14 | Meeting Prep, MEDDPICC and Call Coaching fall back to their defaults |
| Company | all | Framing only, rarely the bottleneck |
| Product Modules | Sales-to-CS Handoff | Implementation scope cannot be sized |

The operating skills each add one small optional section of their own. That map is in [How It Fits Together](how-it-fits.md#what-each-skill-reads-from-the-profile).

### How to Know the Profile Is Good Enough

Run the three tests at the bottom of the template (the new-hire test, the swap test and the proof-point test). Then run Account Pre-Qualification (01) on three accounts you already know the answer for. If the verdicts match what you know, the ICP section is working. If not, the gap is in the profile, not the skill.

---

## Step 2: Run a Skill's CUSTOMIZE.md

Every skill, all 29 of them, ships a `CUSTOMIZE.md` next to its `SKILL.md`. It is an interview, not a form:

1. **Run the stock skill first** on 2-3 real accounts. You cannot judge a customization you have not compared to a baseline.
2. **Open the skill's `CUSTOMIZE.md`**, copy the prompt block into Claude Code (or Claude.ai, or Codex) with the `SKILL.md` attached, and answer the questions one at a time.
3. **Read section D (or the last section), "the honest part".** It lists the questions you could not answer concretely. For most teams that list is the most useful output, because it shows where the context is missing.
4. **Save what the interview produces.** For a sales skill, that is usually changes to your profile. For an operating skill, it is one new section in your profile (for example `## Review Process` for Second Opinion), which the skill reads on its next run.
5. **Verify.** Run the skill again on the same accounts and compare with the baseline. If you cannot see a difference, the customization did not take.

---

## Step 3: Swap Sales Methodologies

Start by ticking the right boxes in the profile's **Sales Methodology** section. Meeting Prep, MEDDPICC Analysis and Call Coaching read it and let it take precedence over their defaults. Only edit the skill files when you want the question banks and rubrics themselves to change.

### Replacing SPIN with Another Discovery Framework

Meeting Prep (06) and Call Coaching (13) use SPIN for discovery calls. To swap:

1. Open `skills/06-meeting-prep/SKILL.md` and find `### Discovery: SPIN / Challenger Question Framework` under `## Methodology`.
2. Replace the question structure with your framework's.
3. Open `skills/13-call-coaching/SKILL.md` and find `### Discovery: SPIN Selling Framework` under `## Methodology`, plus the discovery rubric in `### Step 2: Score Methodology Execution`. Change the rubric categories so the coaching grades what the new framework asks for.

**Example: SPIN to Sandler Pain Funnel**

```markdown
### Discovery Framework: Sandler Pain Funnel

1. **Surface Pain:** "Tell me more about how invoice review works today."
2. **Business Impact:** "What does that cost the department each quarter?"
3. **Personal Impact:** "What does it mean for you when the CFO asks about counsel spend?"
4. **Budget Commitment:** "What would you invest to get that visibility?"
5. **Decision Process:** "If you found the right solution, what happens next?"
```

**Example: SPIN to Gap Selling**

```markdown
### Discovery Framework: Gap Selling

1. **Current State:** How outside-counsel spend is tracked today, by whom, in what tools
2. **Future State:** What the GC wants to be able to answer, and by when
3. **The Gap:** What prevents the move from current to future state
4. **Impact of the Gap:** What the gap costs in overbilling, attorney hours and risk
5. **Root Cause:** Why the gap exists, and what has already been tried
```

### Replacing Challenger with Another Demo Framework

Meeting Prep (06, demo mode) and Call Coaching (13) use Challenger principles. Replace the demo section (`### Demo: Demo Framework` in 06, `### Demo: Challenger Sale Framework` in 13) with your framework's steps:

```markdown
### Demo Framework: [Your Framework]

1. **[Step 1]:** [What the rep should do and why]
2. **[Step 2]:** [What the rep should do and why]
3. **[Step 3]:** [What the rep should do and why]
```

Then update the demo rubric in Call Coaching so it grades the new steps. The demo score is out of 40 across 8 categories. If you change the number of categories, change the total and the score bands with it.

---

## Step 4: Modify Scoring (Rarely)

### Deal Pulse: Adding or Removing Signals

Deal Pulse scores 16 signals across 4 pillars (Why Anything, Why Us, Why Now, Execution). Each signal is GREEN (100), YELLOW (50) or RED (0), the health score is their average, and the risk bands are 85-100 low, 46-84 medium, 0-45 high. To modify:

1. Open `skills/08-deal-pulse/SKILL.md`.
2. Under `## Methodology`, find the four `### Signal Scoring Rubrics` sections, one per pillar.
3. Add, remove or rewrite signals in the pillar where they belong.
4. Update `### Health Score Calculation` if the count changes, and add a row for the new signal to `### Recommended Actions Framework`.

**Example: a "Security Review" signal for enterprise legal deals**

Lexora's enterprise deals add procurement and information security. Add under the Execution pillar:
```markdown
| 🟢 GREEN | Security questionnaire returned and InfoSec approval scheduled. |
| 🟡 YELLOW | Questionnaire received, not yet started. |
| 🔴 RED | Security review not yet raised with the buyer. |
```

### MEDDPICC: Adjusting Element Weights

MEDDPICC Analysis scores each of the 8 elements 1-5 and weights them into a 0-100 health score. The default weights are Economic Buyer 20%, Metrics 15%, Identified Pain 15%, Champion 15%, Decision Criteria 10%, Decision Process 10%, Paper Process 10% and Competition 5%. To change them:

1. Open `skills/09-meddpicc-analysis/SKILL.md`.
2. Edit the table in `### The Eight MEDDPICC Elements and Weights`. Keep the weights adding up to 100%.
3. Check `### Stage-Appropriate Minimums` still makes sense for your stages.

**Example:** a team selling into procurement-heavy enterprises might move Paper Process to 15% and Competition to 0%, if competition is rarely a factor and procurement is where deals stall.

### Call Coaching: Adding Custom Criteria

1. Open `skills/13-call-coaching/SKILL.md`.
2. In `### Step 2: Score Methodology Execution`, find the discovery rubric (6 categories, /30) or the demo rubric (8 categories, /40).
3. Add a category with behavioral indicators for each score, and update the total and the score bands.

```markdown
| 7 | Multi-threading | Asked about other stakeholders (Legal Ops, Finance, Procurement) and offered to include them | /5 |
```

---

## Adding Industry-Specific Qualification Criteria

Account Pre-Qualification (01) scores 8 criteria, defined in `### Qualification Criteria (ICP1)` and `### Qualification Criteria (ICP2)` under `## Methodology`. They are written to fit any vertical. Add criteria that are specific to yours.

**Example: Lexora (legal operations)**
```markdown
| 9 | Outside-Firm Fragmentation | 20+ active outside firms | Fragmentation is where visibility pain lives |
| 10 | Current e-Billing System | Competitor X, spreadsheets, or an outsourced review service | Decides which displacement play applies |
```

If you add criteria, update the GREENLIGHT and MANUAL REVIEW thresholds in `### Step 6: Deliver Qualification Verdict` (currently 6+ and 4-5 of 8), so the verdicts still mean what they say.

---

## Creating Custom Skill Combinations

### A "Weekly Pipeline Review" Macro

Instead of running Deal Pulse on each deal individually, add a wrapper to your `CLAUDE.md`:

```markdown
## Weekly Pipeline Review
When I ask for a pipeline review:
1. Read skills/08-deal-pulse/SKILL.md
2. Score each deal I provide
3. Stack-rank by health score
4. Flag any deal at 45 or below (High Risk)
5. For flagged deals, note the top 2 risks and the recommended next actions
6. Present as a table: Deal | Score | Top Risk | Next Action
```

### A "New Account Package" Macro

```markdown
## New Account Package
When I ask to package a new account:
1. Run Account Pre-Qualification (skills/01-account-qualification/SKILL.md)
2. If GREENLIGHT: run Account Snapshot (skills/02-account-snapshot/SKILL.md)
3. Present: qualification verdict, company brief, email sequences, cold call sheet
```

---

## Feeding the Skills External Data

### CRM Data (Salesforce, HubSpot and so on)

Skills work best with context. Paste relevant CRM data when you run one:

```
Score this deal with Deal Pulse. Here's the CRM data:

Account: Corvane Industrial
Stage: Demo Completed
Close Date: March 30
Amount: $180K ARR
Last Activity: Meeting with the Head of Legal Ops (3 days ago)
Next Step: Security review with InfoSec
Notes from last call: [paste notes]
Contacts: Head of Legal Ops (Champion), GC (Economic Buyer), CFO (not yet engaged)
```

### Call Transcripts

For Call Coaching, paste the full transcript or detailed notes. More context makes better coaching.

### Public Research

For Research-Driven Outbound, paste 10-K excerpts, earnings call transcripts, or posts from target executives.

---

## Version Control Tips

When customizing skills for a team:

1. **Fork this repo** for your organization.
2. **Keep one profile per engagement** in `profiles/` (for example `client-profile.md` active, `acme-profile.md` archived) and swap the active file when you change clients. `client-profile.md` is gitignored, so decide deliberately where your team's copy lives.
3. **Use branches** for experiments (for example `try-sandler-framework`).
4. **Bump the frontmatter `version`** of any skill you change, and note the change in its Changelog section.
5. **Review quarterly** to remove outdated competitors, refresh proof points and update personas.
