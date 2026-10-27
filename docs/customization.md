# Customization Guide

How to adapt the skills to your company, your methodology, your scoring preferences and your workflow. Work top to bottom. Most teams only ever need the first two sections.

Every example on this page uses PlotIQ, the made-up deathcare software company in [`profiles/examples/plotiq-example.md`](../profiles/examples/plotiq-example.md), so you can see each change against a complete profile.

---

## What You Can (And Should) Customize

| How often | What | Where | Effort |
|---|---|---|---|
| **Always** | Your company data | One file, `profiles/client-profile.md` | 30 minutes, once, then refresh quarterly |
| **Per skill, after a baseline** | How a skill fits your motion | That skill's `CUSTOMIZE.md` interview | 10-20 minutes per skill |
| **Sometimes** | Your sales methodology (SPIN, Challenger, MEDDPICC) | The profile's Sales Methodology section, then the skill files | An hour |
| **Rarely** | Scoring logic and workflow | The skill files themselves | Only with a strong reason, since a change ripples into every score |

---

## Step 1: Fill The Profile, In The Right Order

Your company's data lives in one file, **`profiles/client-profile.md`**, and every skill reads it through its Context section. This is the main customization point, and you touch exactly one file. The [Client Profile Template](../profiles/client-profile-template.md) walks through each section.

### Which Profile Sections Feed Which Skills

Counted from the Context sections of the 14 sales skills. Fill the top rows first, because they feed nearly everything.

| Profile section | Sales skills that read it | What happens if it is thin |
|---|---|---|
| Buyer Personas | 12 of 14 | Sequences, call sheets, buying-role maps and coaching stop matching the person in the room |
| Competitive Landscape | 10 of 14 | Battlecards, displacement sequences and objection handling go generic |
| Value Propositions | 10 of 14 | Positioning, demo stories and wedges flatten |
| Proof Points | 9 of 14 | Emails, demos and battlecards cite nothing, or cite the wrong customer |
| Qualification Criteria | 9 of 14 | Trigger timing, disqualifiers and the critical-element floors stop working |
| Core Pain Points | 7 of 14 | Discovery questions, email hooks and the listen-for phrases lose their edge |
| ICP Definitions | 5 of 14 (01, 02, 03, 05, 07) | Qualification verdicts and account scores become guesses |
| Qualification Zones | 5 of 14 (01, 02, 03, 07, 11) | Verdicts lose the zone check, so a missing must-have can pass unnoticed |
| Sales Methodology | 5 of 14 (06, 08, 09, 11, 13) | Meeting Prep, Deal Pulse, MEDDPICC, Competitive Strategy and Call Coaching fall back to their defaults |
| Qualification Stage Gates | 3 of 14 (02, 06, 07) | Stage names and the gate to the next stage come from the skill's defaults instead of yours |
| Company | all | Framing only, rarely the bottleneck |
| Product Modules | 14 Sales Handoff | Implementation scope cannot be sized |

Five columns matter more than their size suggests: "Persona Who Acts" on Buying Triggers (03 and 04 send the sequence to that person), "Discovery Question" on Core Pain Points (06, 07 and 13 ask it), the two right-hand columns on Competitive Landscape, "Pain Reported After 6 To 12 Months" and "Proof That Answers It" (05 uses them on a buyer who chose a rival 6 to 12 months ago), and Status on Proof Points (an Illustrative row never reaches a prospect, most skills also allow a Benchmark row with its source, and 05 allows only Verified).

Each sales skill also reads one section of its own, written by that skill's `CUSTOMIZE.md` interview (Fit Grid, Outbound Voice, Industry Context, Trigger Catalog, Closed-Loss Intelligence, Meeting Prep, Daily Prospecting, Deal Health, MEDDPICC, Buying Committee, Competitive Patterns And Trends, Displacement, Call Coaching, Implementation Profile). The operating skills do the same. Both maps are in [How It Fits Together](how-it-fits.md#what-each-skill-reads-from-the-profile).

### How To Know The Profile Is Good Enough

Run the three tests at the bottom of the template (the new-hire test, the swap test and the proof-point test). Then run Account Qualification (01) on three accounts you already know the answer for. If the verdicts match what you know, the ICP section is working. If not, the gap is in the profile, not the skill.

---

## Step 2: Run A Skill's CUSTOMIZE.md

Every skill, all 29 of them, ships a `CUSTOMIZE.md` next to its `SKILL.md`. It is an interview, not a form:

1. **Run the stock skill first** on 2-3 real accounts. You cannot judge a customization you have not compared to a baseline.
2. **Open the skill's `CUSTOMIZE.md`**, copy the prompt block into Claude Code (or Claude.ai, or Codex) with the `SKILL.md` attached, and answer the questions one at a time.
3. **Read the section headed "The Honest Part". Its letter differs by skill (A to D), so look for the heading, not the letter.** It lists the questions you could not answer concretely. For most teams that list is the most useful output, because it shows where the context is missing.
4. **Save what the interview produces.** For a sales skill, that is usually changes to your profile. For an operating skill, it is one new section in your profile (for example `## Second Opinion` for O5 Second Opinion), which the skill reads on its next run.
5. **Verify.** Run the skill again on the same accounts and compare with the baseline. If you cannot see a difference, the customization did not take.

---

## Step 3: Swap Sales Methodologies

Start by ticking the right boxes in the profile's **Sales Methodology** section. Meeting Prep, MEDDPICC Deal Analysis and Call Coaching read it and let it take precedence over their defaults. Only edit the skill files when you want the question banks and rubrics themselves to change.

### Replacing SPIN With Another Discovery Framework

Meeting Prep (06) and Call Coaching (13) use SPIN for discovery calls. To swap:

1. Open `skills/06-meeting-prep/SKILL.md` and find `### Discovery: SPIN Question Framework` under `## Methodology`.
2. Replace the question structure with your framework's.
3. Open `skills/13-call-coaching/SKILL.md` and find `### Discovery: SPIN Selling Framework` under `## Methodology`, plus the discovery rubric in `### Step 2: Score Methodology Execution`. Change the rubric categories so the coaching grades what the new framework asks for.

**Example: SPIN To Sandler Pain Funnel**

```markdown
### Discovery Framework: Sandler Pain Funnel

1. **Surface Pain:** "Tell me more about how plot records work today."
2. **Business Impact:** "What does that cost the cemetery each year, in unsold plots or in staff time on lookups?"
3. **Personal Impact:** "What does it mean for you when the auditor asks for a trust record that is in a binder?"
4. **Budget Commitment:** "What would you invest to know exactly which plots are unsold?"
5. **Decision Process:** "If you found the right solution, what happens next?"
```

**Example: SPIN To Gap Selling**

```markdown
### Discovery Framework: Gap Selling

1. **Current State:** How plot records are kept today, by whom, in what tools
2. **Future State:** What the general manager wants to be able to answer, and by when
3. **The Gap:** What prevents the move from current to future state
4. **Impact of the Gap:** What the gap costs in unsold plots, double sales, audit exposure and staff hours
5. **Root Cause:** Why the gap exists, and what has already been tried
```

### Replacing Challenger With Another Demo Framework

Meeting Prep (06, demo mode) and Call Coaching (13) use Challenger principles. Replace the demo sections (the three `### Demo:` sections in 06, starting with `### Demo: Five Demo Habits`, and `### Demo: Challenger Sale Framework` in 13) with your framework's steps:

```markdown
### Demo Framework: [Your Framework]

1. **[Step 1]:** [What the rep should do and why]
2. **[Step 2]:** [What the rep should do and why]
3. **[Step 3]:** [What the rep should do and why]
```

Then update the demo rubric in Call Coaching so it grades the new steps. The demo score is out of 40 across 8 categories. If you change the number of categories, change the total and the score bands with it.

---

## Step 4: Modify Scoring (Rarely)

### Deal Pulse: Adding Or Removing Signals

Deal Pulse scores 16 signals across 4 pillars (Why Anything, Why Us, Why Now, Execution). Each signal is GREEN (100), YELLOW (50) or RED (0), the health score is their average, and the risk bands are 85-100 low, 46-84 medium, 0-45 high. To modify:

1. Open `skills/08-deal-pulse/SKILL.md`.
2. Under `## Methodology`, find the four pillar rubrics, headed `### Signal Scoring Rubrics (Why Anything Pillar)`, `(Why Us Pillar)`, `(Why Now Pillar)` and `(Execution Pillar)`.
3. Add, remove or rewrite signals in the pillar where they belong.
4. Update `### Health Score Calculation` if the count changes, and add a row for the new signal to `### Recommended Actions Framework`.

**Example: A "Board Date" Signal For Cemetery Deals**

PlotIQ deals over the $25K line need a board vote, so the approval date is an execution step. Add under the Execution pillar:
```markdown
| 🟢 GREEN | Board approval date set and the board packet is with the decision makers. |
| 🟡 YELLOW | Board meets within 60 days, date not yet on the calendar. |
| 🔴 RED | No board date, and the approval path is unknown. |
```

### MEDDPICC: Adjusting Element Weights

MEDDPICC Analysis scores each of the 8 elements 1-5 and weights them into a 0-100 health score. The default weights are Economic Buyer 20%, Metrics 15%, Identified Pain 15%, Champion 15%, Decision Criteria 10%, Decision Process 10%, Paper Process 10% and Competition 5%. To change them:

1. Open `skills/09-meddpicc-analysis/SKILL.md`.
2. Edit the table in `### The Eight MEDDPICC Elements And Weights`. Keep the weights adding up to 100%.
3. Check `### Stage-Appropriate Minimums` still makes sense for your stages.

**Example:** a team selling into procurement-heavy enterprises might move Paper Process to 15% and Competition to 0%, if competition is rarely a factor and procurement is where deals stall.

### Call Coaching: Adding Custom Criteria

1. Open `skills/13-call-coaching/SKILL.md`.
2. In `### Step 2: Score Methodology Execution`, find the discovery rubric (7 categories, /35) or the demo rubric (8 categories, /40).
3. Add a category with behavioral indicators for each score, and update the total and the score bands.

```markdown
| 7 | Multi-threading | Asked about other stakeholders (Operations Director, Pre-Need Sales, Finance) and offered to include them | /5 |
```

---

## Making The Qualification Criteria Fit Your Vertical

Account Qualification (01) scores 8 criteria, defined in `### Qualification Criteria (ICP1)` and `### Qualification Criteria (ICP2)` under `## Methodology`. They are written to fit any vertical. Keep the eight, and rewrite what each one looks for in your market's own words. Do not add a ninth. Every added criterion dilutes the weights of the ones that decide, so when a new fact matters, ask which existing criterion it is evidence for and fold it in there.

**Example: PlotIQ (Cemeteries And Funeral Homes)**
```markdown
| 7 | Technology Readiness | Names the plot records system in use: Stonemark Enterprise, Oldgate Ledger Pro, a spreadsheet, or none. The system decides which displacement play applies |
| 8 | Current Solution Gap | Plot records kept on paper maps, binders or pencil maps. Paper hides unsold plots, which is where the pain lives |
```

Rewriting a criterion changes the scorecard, not the verdict. The verdict comes only from the Verdict Rule in your profile's Qualification Zones, applied in `### Step 6: Deliver The Qualification Verdict`, so after you rewrite a criterion, check that the Verdict Rule still says what you mean.

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
1. Run Account Qualification (skills/01-account-qualification/SKILL.md)
2. If GREENLIGHT: run Account Snapshot (skills/02-account-snapshot/SKILL.md)
3. Present: qualification verdict, company brief, email sequences, cold call sheet
```

---

## Feeding The Skills External Data

### CRM Data (Salesforce, HubSpot And So On)

Skills work best with context. Paste relevant CRM data when you run one:

```
Score this deal with Deal Pulse. Here's the CRM data:

Account: Brackhaven Memorial Gardens
Stage: 5 Negotiate
Close Date: November 30 (illustrative)
Amount: $10,788 a year plus $5,000 setup (list price)
Last Activity: Walk-through with the Operations Director (3 days ago)
Next Step: Board date confirmation with the family board chair
Notes from last call: [paste notes]
Contacts: General Manager Ruth Ellery (Champion), family board chair (Economic Buyer), Operations Director Walt Okonkwo (skeptical of tablets)
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
